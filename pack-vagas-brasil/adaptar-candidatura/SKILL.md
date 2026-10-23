---
name: adaptar-candidatura
description: Prepara pacotes de candidatura personalizados (currículo formatado para ATS em coluna única, métricas de impacto e respostas a formulários) em candidaturas/<id>/ para vagas aprovadas. Use sempre que for necessário customizar documentos, gerar currículos por vaga ou responder perguntas de triagem.
---

# Adaptação de candidatura

Gera o diretório `candidaturas/<id>/` para cada oportunidade `aprovada`, preparando os artefatos textuais e atualizando o status para `pacote_pronto`.

## Diretriz de Integridade

A customização restringe-se a **reorganizar, priorizar e enfatizar** informações verídicas documentadas em `curriculo-base.md`. Nenhuma qualificação, certificação ou métrica pode ser inventada.

## Estrutura do Pacote (`candidaturas/<id>/`)

1. **`curriculo.md`:**
   - **Layout ATS estrito:** Estrutura em coluna única, sem tabelas, sem caixas de texto laterais, sem ícones ou gráficos, facilitando o parsing de sistemas como Gupy, Taleo, Workday e Kenoby.
   - Resumo executivo (3 a 4 linhas) direcionado ao escopo da vaga.
   - Destaque das competências técnicas solicitadas na vaga que o candidato comprovadamente domine, empregando a mesma nomenclatura exata da descrição.
   - Histórico profissional em ordem cronológica reversa, priorizando bullets estruturados no formato: `[Verbo de ação forte] + [Métrica/Resultado alcançado] + [Ferramenta/Contexto]`.
2. **`carta.md`:**
   - Texto de 120 a 180 palavras em português claro, profissional e objetivo:
     - Razão de interesse pela empresa/vaga.
     - Duas realizações sólidas extraídas do histórico.
     - Fechamento com disponibilidade para diálogo.
3. **`respostas.md`:**
   - Respostas prontas para questionários cadastrais usando estritamente os dados de `perfil.md` (separando pretensão CLT de PJ quando questionado).
   - Para qualquer pergunta sem base prévia aprovada, registre categoricamente: `PRECISA_DO_USUARIO`.
4. **`check.md`:**
   - Rastreabilidade interna: lista cada argumento usado em `curriculo.md` e a linha correspondente de onde foi derivado em `curriculo-base.md`.
5. **Conversão de Documentos:**
   - Disponibilize a versão texto plano para preenchimento de campos online e, se o ambiente local tiver ferramentas como Pandoc/Python disponíveis, compile para `curriculo.pdf`. Caso contrário, mantenha a formatação Markdown limpa pronta para exportação.

## Regras

- Se houver divergência entre a exigência da vaga e o perfil, mantenha o currículo focado no que existe; não simule conformidade.
- Atualize a linha da vaga no `vagas.csv` para `status = pacote_pronto`.
