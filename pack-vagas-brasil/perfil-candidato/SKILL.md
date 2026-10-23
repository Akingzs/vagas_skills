---
name: perfil-candidato
description: Cria e mantém o perfil de candidato (perfil.md) que alimenta toda a busca e candidatura a vagas no Brasil — currículo-base, cargos-alvo, faixa salarial (CLT/PJ), modelo de trabalho, cidades, blacklist de empresas e travas de automação. Use sempre que o usuário quiser configurar, atualizar ou revisar o perfil de busca, currículo-base, pretensão salarial, filtros de vagas ou limites de envio.
---

# Perfil do candidato

O `perfil.md` é a **única fonte de verdade** das demais skills do pack (busca-vagas, triagem-vagas, adaptar-candidatura, enviar-candidatura, tracker-vagas). Se uma informação não estiver nele, nenhuma skill pode inventá-la.

## Pasta de trabalho

Todo o pack opera em uma pasta unificada (padrão: `Vagas/`):
- `perfil.md` — gerado e atualizado por esta skill
- `curriculo-base.md` — currículo completo e fidedigno fornecido pelo usuário
- `vagas.csv` — gerenciado pelo tracker-vagas
- `candidaturas/<id-da-vaga>/` — pacotes customizados por vaga

## Fluxo

1. Verifique a existência de `perfil.md`:
   - Se já existir, leia o conteúdo e pergunte apenas os pontos que precisam de atualização.
   - Se não existir, conduza uma entrevista estruturada e objetiva em blocos curtos.
2. Solicite o currículo atual do usuário e salve-o como `curriculo-base.md`, preservando a íntegra de experiências, datas e resultados sem modificações ou floreios.
3. Preencha o `perfil.md` seguindo o modelo abaixo.
4. Exiba o resumo completo e peça confirmação expressa antes de gravar.

## Modelo do perfil.md

```markdown
# Perfil de candidatura

## Identidade
- Nome:
- Cidade/UF:
- E-mail para contato:
- Telefone/WhatsApp:
- LinkedIn / GitHub / Portfólio:

## Alvo
- Cargos-alvo (em ordem de prioridade):
- Palavras-chave obrigatórias:
- Palavras-chave a evitar:
- Senioridade visada:
- Setores de interesse:

## Condições de Trabalho
- Modalidades aceitas: remoto | híbrido | presencial
- Cidades/Regiões aceitas (se presencial ou híbrido):
- Regime contratual: CLT | PJ | Ambos
- Faixa salarial CLT (R$/mês bruta): mínimo ___ / desejada ___
- Faixa salarial PJ (R$/mês ou R$/hora): mínimo ___ / desejada ___
- Disponibilidade de início:
- Idiomas e nível de proficiência:

## Critérios Eliminatórios (descarte sumário)
- ...

## Blacklist de Empresas (não aplicar sob hipótese alguma)
- ...

## Respostas Padrão para Formulários
- Pretensão CLT informada: R$
- Pretensão PJ informada: R$
- Possui CNPJ ativo?: sim | não
- Aceita modelo de terceirização?: sim | não
- Aviso prévio / início imediato?:
- Autorização legal para trabalhar no Brasil: Sim
- Disponibilidade para viagens?: sim | não
- Disponibilidade para mudança?: sim | não
- Como soube da vaga?: Outros / Busca Ativa
- Grau de escolaridade concluído:

## Travas Operacionais de Automação
- nota_minima: 80
- limite_diario: 10
- pausa_entre_envios_segundos: 45-120
- plataformas_ativas: LinkedIn, Gupy, Indeed, Catho, InfoJobs, Vagas.com
- idade_maxima_da_vaga_dias: 14
```

## Regras

- **Dados Sensíveis e LGPD:** Campos como gênero, raça/etnia, PCD, estado civil, CPF, RG e data de nascimento só constam em "Respostas Padrão" com autorização explícita e fornecimento voluntário do usuário. Caso contrário, permaneçam vazios para que o envio pause e solicite confirmação manual.
- **Remuneração:** Nunca arbitre ou deduza valores de pretensão salarial; utilize estritamente o informado pelo usuário.
- **Segurança de Acesso:** Jamais armazene senhas, tokens ou dados de autenticação em disco.
- Mantenha no cabeçalho a data da última revisão: `Última atualização: AAAA-MM-DD`.
