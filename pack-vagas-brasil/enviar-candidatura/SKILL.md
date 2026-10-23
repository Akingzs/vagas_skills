---
name: enviar-candidatura
description: Executa o envio supervisionado de candidaturas com status pacote_pronto via automação de navegador (LinkedIn, Gupy, Indeed, Catho, InfoJobs, Vagas.com), pausando e solicitando intervenção manual diante de testes online, entrevistas assíncronas em vídeo, CAPTCHAs, 2FA ou perguntas inéditas. Use para submeter aplicações prontas dentro dos limites operacionais.
---

# Envio de candidaturas

Realiza o preenchimento e a submissão no modelo **automático supervisionado**: submete as candidaturas padronizadas e interrompe o fluxo diante de exceções, preservando a integridade da conta e o cadastro do usuário.

## Pré-requisitos

- Registros no `vagas.csv` com `status = pacote_pronto`, nota maior ou igual a `nota_minima` e diretório correspondente pronto.
- Acesso ao navegador via automação (Playwright, Selenium ou extensão do navegador), com sessões previamente logadas pelo usuário nas plataformas alvo.

## Checklist Pré-Envio (por vaga)

1. Total de candidaturas no dia menor que `limite_diario` (apurado via `vagas.csv` na data atual).
2. Verificação de integridade da vaga (URL ativa e confirmada para a mesma empresa/cargo).
3. Inexistência de candidatura idêntica registrada nos últimos 90 dias.
4. Ausência de marcações `PRECISA_DO_USUARIO` em `respostas.md` para campos mandatórios daquela tela.

## Protocolo por Tipo de Plataforma

### 1. LinkedIn (Candidatura Simplificada / Easy Apply)
- Faça upload do currículo gerado no pacote.
- Responda aos formulários com os dados de `respostas.md`.
- Conclua a submissão e capture a confirmação visual na tela.

### 2. Gupy e Portais de ATS com Testes (Kenoby, Mindsight, etc.)
- **Etapa 1 (Cadastro e Currículo):** Preencha os dados biográficos, faça upload do documento e responda perguntas discursivas padrão.
- **Etapa 2 (Testes Online / Fit Cultural / Raciocínio / Vídeo Unilateral):** **NÃO tente responder automaticamente.**
  - Pare o processo nesta vaga.
  - Atualize o status em `vagas.csv` para `precisa_de_voce`.
  - Registre em `motivo_trava: requer_teste_online` ou `requer_video_unilateral`.
  - Guarde a URL direta da etapa de teste para o usuário completar manualmente se desejar.

## Interrupções Obrigatórias (Travas de Segurança)

Pare a automação imediatamente na vaga em caso de:
- Detecção de CAPTCHA, validação humana ou solicitação de autenticação em dois fatores (2FA).
- Perguntas discursivas ou eliminatórias sem correspondência direta em `perfil.md`.
- Solicitação de gravação de vídeo, envio de áudio ou redação aberta não prevista.
- Qualquer exigência de cobrança de taxa de cadastro ou confirmação financeira.
- Redirecionamento inesperado para domínios desconhecidos fora da plataforma original.

## Cadência Operacional

- Aplique intervalos randômicos entre envios com base no parâmetro `pausa_entre_envios_segundos` (ex.: 45 a 120 segundos).
- Em caso de aviso de restrição temporária ou excesso de requisições na plataforma, aborte o lote inteiro do dia e notifique o usuário.

## Conclusão de Envio

- Confirmação positiva: atualize em `vagas.csv` para `status = enviada` e grave a `data_candidatura`.
- Envio inconclusivo ou sem tela de sucesso: marque `status = precisa_de_voce` com `motivo_trava = envio_nao_confirmado`.
- Ao final do lote, exiba o relatório de envios bem-sucedidos e pendências manuais.
