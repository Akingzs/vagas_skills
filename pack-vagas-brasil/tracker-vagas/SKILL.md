---
name: tracker-vagas
description: Gerencia e consolida o vagas.csv com delimitador de ponto e virgula para Excel brasileiro, prove metricas diarias de conversao, monitora follow-ups e gerencia as transicoes de status das oportunidades. Use para consultar status, gerar relatorios de envio, atualizar retornos de processos ou revisar pendencias.
---

# Tracker de vagas

Controlador central do arquivo `vagas.csv`. Todas as operações de leitura e gravação pelas demais skills seguem a taxonomia e estrutura aqui definidas.

## Estrutura do Arquivo vagas.csv

- **Codificação:** UTF-8 com BOM (garante abertura correta de acentuação no Excel).
- **Delimitador:** Ponto e vírgula (`;`), nativo do formato regional PT-BR.
- **Colunas:**
```csv
id;plataforma;titulo;empresa;local;modelo;regime;url;data_publicacao;tipo_candidatura;faixa_salarial;nota;justificativa;status;motivo;data_candidatura;motivo_trava;follow_up;notas_usuario;descricao_resumo
```

- `id`: Formato `AAAAMMDD-NNN` (ex: `20261023-001`).
- `regime`: `CLT`, `PJ` ou `Nao informado`.
- Datas no formato ISO: `AAAA-MM-DD`.

## Ciclo de Estados (status)

- `nova` -> `descartada`
- `nova` -> `triada`
- `nova` -> `aprovada` -> `pacote_pronto` -> `enviada` -> `entrevista` / `recusada` / `sem_resposta`
- `pacote_pronto` -> `precisa_de_voce` -> `enviada` (após ação manual)

Regras de transição:
- Status `descartada` e `precisa_de_voce` exigem obrigatoriamente preenchimento dos campos `motivo` ou `motivo_trava`.
- Registros nunca são deletados para manter o histórico contra candidaturas duplicadas.

## Resumo e Acompanhamento

Ao final de um ciclo de busca/envio ou quando solicitado pelo usuário, estruture o relatório consolidado:
1. Volume minerado no dia por plataforma.
2. Quantidade aprovada x descartada.
3. Total de envios submetidos com sucesso hoje (`x / limite_diario`).
4. Lista detalhada de itens em `precisa_de_voce` com link direto e a pendência exata (ex.: teste da Gupy, campo salarial específico, validação de 2FA).
5. Alertas de `follow_up` vencidos (padrão: 7 dias pós-envio sem atualização).

## Regras de Integridade

- Respeite anotações inseridas manualmente pelo usuário na coluna `notas_usuario`.
- Ao registrar avanço para entrevista ou recusa comunicada pela empresa, anote a data do evento em `notas_usuario`.
