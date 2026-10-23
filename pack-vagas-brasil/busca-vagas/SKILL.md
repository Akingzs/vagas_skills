---
name: busca-vagas
description: Executa a busca e mineração de vagas no Brasil (LinkedIn, Gupy, Indeed, InfoJobs, Catho, Vagas.com) com base no perfil.md e grava as oportunidades no vagas.csv com status nova, priorizando vagas recém-publicadas (primeiras 24-48h). Use sempre que o usuário solicitar busca, varredura ou monitoramento de oportunidades no mercado.
---

# Busca de vagas

Consulta `perfil.md` e minera vagas recentes nas plataformas ativas, salvando-as de forma normalizada em `vagas.csv` com status `nova`. Esta skill é exclusivamente extratora; o ranqueamento fica a cargo de `triagem-vagas`.

## Pré-requisitos

- Existência confirmada de `perfil.md` (se ausente, direcione para `perfil-candidato`).
- Ferramenta de navegação ativa no ambiente (browser automation / Playwright / extensão). O usuário deve estar pré-autenticado nas plataformas que requerem login (LinkedIn, Catho). Caso encontre tela de login, solicite a autenticação manual e aguarde.

## Fluxo de Execução

1. **Janela de Tempo Crítica (Early Bird Strategy):**
   - Vagas recebem centenas de candidaturas nas primeiras 72 horas. Filtre preferencialmente por anúncios publicados nas **últimas 24 a 48 horas** (máximo definido por `idade_maxima_da_vaga_dias`, padrão: até 7 dias). Anúncios com mais de 14 dias têm alta probabilidade de serem "vagas fantasma" (ghost jobs) ou processos já encerrados.
2. **Geração de Consultas:**
   - Combine cargos-alvo com palavras-chave essenciais em português e termos técnicos em inglês.
   - Aplique os filtros nativos da plataforma para modalidade (remoto/híbrido) e localidade.
3. **Estratégia por Plataforma:**
   - **LinkedIn / Indeed / Catho:** Busque pelas listagens nativas filtradas por data de publicação recente (últimas 24h/semana).
   - **Gupy:** Além do portal oficial, use buscas estruturadas por dorks: `site:*.gupy.io "<cargo>" "<cidade ou remoto>"`.
4. **Extração de Dados:**
   - Abra a página individual de cada vaga para obter a descrição integral e identificar o hiring manager / recrutador quando disponível.
5. **Normalização e Deduplicação:**
   - Padronize os campos: `plataforma;titulo;empresa;local;modelo;regime;url;data_publicacao;tipo_candidatura;faixa_salarial`.
   - `tipo_candidatura`: `simplificada`, `gupy_portal`, `formulario_plataforma` ou `site_externo`.
   - Deduplique verificando a `url` exata e a combinação `titulo + empresa` já registrada em `vagas.csv`.
6. **Gravação e Relatório:**
   - Insira os novos registros em `vagas.csv` com status `nova`.
   - Emita resumo com foco na recência das vagas encontradas.

## Regras

- Registre apenas vagas com URLs ativas e verificáveis.
- Em caso de CAPTCHA ou rate-limit, interrompa a plataforma específica e continue com as outras.
- Mantenha pausas randômicas (3 a 8 segundos) entre requisições.
- Descarte anúncios com cobrança de taxa ou sinais de fraude (`descartada`, motivo: `suspeita_golpe`).
