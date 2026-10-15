# Coverage Classification / Classificação de Cobertura

## English

This is the criterion we used to decide whether a migrated test counted as
*covered* (Section 5.1 of the paper).

### The rule

A converted test was accepted as having **acceptable coverage** when it met both
conditions:

1. **It passed the pipeline** — the Cypress test ran green in CI.
2. **It kept the essential assertions of the original Robot test** — it validated
   the same business result, not just something superficial such as the presence of
   a success message. A test that passed without checking the expected effect did
   **not** count.

Verification was manual, comparing the Robot test and the Cypress test side by side.
Each case was recorded in one of **three migration states**:

| State | Meaning |
|---|---|
| **Success** | Passed and preserved the essential business assertions. |
| **Partial** | Passed but weakened or dropped part of the original validation; counted as problematic until fixed. |
| **Incomplete** | Not converted, or converted but not runnable/meaningful. |

### Results

- 151 Robot tests in scope (per-feature count on the `Indicadores` sheet).
- 113 reached acceptable coverage → **74.8%**.
- 38 were not converted.
- 6 were converted but incomplete.
- 38 + 6 = **44 problematic cases**, which is the figure on the `Indicadores` sheet.

In the paper, the independent effort-based estimate (heavy refactoring or rewrite,
plus the ignored tests) converges on the same band of roughly 25% problematic — two
routes to a consistent number.

### A note on subjectivity

Deciding whether a kept assertion is "essential" involves judgment, especially for
the *partial* cases. We flag this in the threats to validity: the boundary between
*partial* and *success* is the most subjective one, and a different reviewer might
move a few cases across it. The three-state scheme exists precisely so that these
borderline cases are visible rather than hidden inside a binary pass/fail.

---

## Português

Este é o critério que usamos para decidir se um teste migrado contava como
*coberto* (Seção 5.1 do artigo).

### A regra

Um teste convertido era aceito como tendo **cobertura aceitável** quando cumpria as
duas condições:

1. **Passava na pipeline** — o teste Cypress rodava verde no CI.
2. **Mantinha as asserções essenciais do teste Robot original** — validava o mesmo
   resultado de negócio, não só algo superficial como a presença da mensagem de
   sucesso. Um teste que passava sem checar o efeito esperado **não** contava.

A verificação era manual, comparando lado a lado o teste Robot e o Cypress. Cada caso
foi registrado em um de **três estados de migração**:

| Estado | Significado |
|---|---|
| **Sucesso** | Passou e preservou as asserções essenciais de negócio. |
| **Parcial** | Passou mas enfraqueceu ou removeu parte da validação original; conta como problemático até ser corrigido. |
| **Incompleto** | Não convertido, ou convertido mas sem rodar/sem significado. |

### Resultados

- 151 testes Robot no escopo (contagem por funcionalidade na aba `Indicadores`).
- 113 atingiram cobertura aceitável → **74,8%**.
- 38 não foram convertidos.
- 6 foram convertidos porém incompletos.
- 38 + 6 = **44 casos problemáticos**, que é o valor da aba `Indicadores`.

No artigo, a estimativa independente por esforço (refatoração pesada ou reescrita,
somada aos ignorados) converge para a mesma faixa de cerca de 25% problemáticos —
dois caminhos para um número consistente.

### Uma nota sobre subjetividade

Decidir se uma asserção mantida é "essencial" envolve julgamento, sobretudo nos casos
*parciais*. Registramos isso nas ameaças à validade: a fronteira entre *parcial* e
*sucesso* é a mais subjetiva, e outro revisor poderia mover alguns casos de um lado
para o outro. O esquema de três estados existe justamente para que esses casos de
fronteira fiquem visíveis, em vez de escondidos num binário passou/não passou.
