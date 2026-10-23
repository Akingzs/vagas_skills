---
name: triagem-vagas
description: Avalia e pontua de 0 a 100 as vagas com status nova no vagas.csv confrontando com perfil.md e curriculo-base.md, descartando incompatibilidades e promovendo as aprovadas. Use para filtrar, classificar, ranquear ou priorizar vagas encontradas.
---

# Triagem de vagas

Avalia as vagas recém-coletadas (`status = nova`), convertendo-as para `descartada`, `triada` ou `aprovada`. A decisão baseia-se unicamente nas diretrizes de `perfil.md` e nas qualificações reais de `curriculo-base.md`.

## Fluxo de Avaliação

1. Carregue `perfil.md`, `curriculo-base.md` e as linhas com `status = nova` de `vagas.csv`.
2. **Filtro Eliminatório Direto** (Nota 0, `status = descartada`, justificando o `motivo`):
   - Empresa listada na blacklist.
   - Regime, modelo de trabalho ou cidade incompatíveis com o perfil.
   - Salário anunciado formalmente abaixo do piso estipulado no perfil.
   - Requisito mandatório ausente (ex.: ausência de graduação específica quando estritamente exigida, idioma fluente requerido quando o candidato possui básico).
   - Vaga expirada ou link quebrado.
   - Indícios de anúncio falso ou golpe.
3. **Cálculo de Pontuação (0 a 100):**

| Dimensão de Análise | Peso |
|---|---|
| Alinhamento de Cargo e Nível de Senioridade | 25 |
| Aderência aos Requisitos Obrigatórios | 30 |
| Match de Competências Desejáveis/Diferenciais | 10 |
| Condições Práticas (Modelo, Localidade, Regime e Salário) | 20 |
| Reputação/Setor da Empresa e Fricção de Aplicação | 10 |
| Recorrência e Recência da Publicação | 5 |

4. Elabore uma `justificativa` direta de até duas frases destacando os prós e os gaps identificados.
5. **Classificação Final:**
   - Se `nota >= nota_minima`: marque `aprovada`.
   - Se `nota < nota_minima`: marque `triada`.
   - Em caso de ambiguidade crítica em requisitos: marque `triada` com anotação na justificativa.
6. Atualize o `vagas.csv` e apresente o ranking das 10 melhores oportunidades avaliadas.

## Regras

- Não presuma habilidades ausentes em `curriculo-base.md`. Se o currículo não explicita a ferramenta ou metodologia, considere lacuna.
- A pontuação deve ser estritamente analítica e orientada à tomada de decisão, sem vieses otimistas infundados.
