# Replication Package / Pacote de Replicação

> **Migrating and Comparing Automated Test Frameworks from Robot to Cypress
> with Generative-AI Assistance** — supporting material for the experience report.
>
> **Migração e Comparação de Frameworks de Testes Automatizados de Robot para
> Cypress Assistida por IA Generativa** — material de apoio do relato de experiência.

---

## English

This repository is the supporting material for an experience report on migrating
an end-to-end (E2E) test suite from Robot Framework to Cypress with the help of
generative AI. It is meant to help readers follow the process and see concrete
examples of what was done. Everything is anonymized and the application source
code is not included.

### Contents

| Path | What it is |
|---|---|
| `data/traceability.xlsx` | Anonymized tracking spreadsheet, four sheets (see below). |
| `prompts/ai-use.md` | How the AI was used at each stage, plus 20 example prompts. |
| `criteria/complexity-rubric.md` | The qualitative rubric used to label test complexity. |
| `criteria/coverage-classification.md` | How we decided whether a migrated test counted as covered. |
| `criteria/failure-taxonomy.md` | The six failure types (F1–F6) observed in the machine translation. |

### The spreadsheet

`data/traceability.xlsx` has three sheets:

- **Indicators** — counts per feature (Robot tests, converted,
  incomplete, problematic) and the metrics used in the paper. The per-feature
  counts reconcile to 151 Robot tests and 113 converted with acceptable coverage
  (74.8%); the 44 problematic cases are the not-converted plus the
  converted-but-incomplete.
- **Traceability** — a curated set of ~36 representative test
  cases, each with its feature, a **migration status** (Success / Partial /
  Incomplete) and a note referencing the relevant failure
  code (F1–F6). This is a readable sample, not the full suite.
- **Comparison** — the manual review that cross-checked which Robot
  tests had a Cypress counterpart and vice-versa. It is what showed that the AI's
  automatic "converted" count was inflated (many partial or trivial conversions).



## Português

Este repositório é o material de apoio de um relato de experiência sobre a migração
de uma suíte de testes de ponta a ponta (E2E) do Robot Framework para o Cypress com
apoio de IA generativa. A ideia é ajudar quem lê o artigo a acompanhar o processo e
ver exemplos concretos do que foi feito. Tudo está anonimizado e o código-fonte da
aplicação não está incluído.

### Conteúdo

| Caminho | O que é |
|---|---|
| `data/traceability.xlsx` | Planilha de acompanhamento anonimizada, quatro abas (ver abaixo). |
| `prompts/ai-use.md` | Como a IA foi usada em cada etapa, com 20 exemplos de prompt. |
| `criteria/complexity-rubric.md` | A rubrica qualitativa usada para classificar a complexidade. |
| `criteria/coverage-classification.md` | Como decidimos se um teste migrado contava como coberto. |
| `criteria/failure-taxonomy.md` | Os seis tipos de falha (F1–F6) observados na tradução automática. |

### A planilha

`data/traceability.xlsx` tem três abas:

- **Indicadores** — contagens por funcionalidade (testes Robot, convertidos,
  incompletos, problemáticos) e as métricas usadas no artigo. A contagem por
  funcionalidade fecha em 151 testes Robot e 113 convertidos com cobertura
  aceitável (74,8%); os 44 casos problemáticos são os não convertidos somados aos
  convertidos porém incompletos.
- **Rastreabilidade** — um conjunto curado de ~36 casos representativos, cada um com
  a funcionalidade, um **status da migração** (Sucesso / Parcial / Incompleto) e uma observação que remete ao código de falha
  pertinente (F1–F6). É uma amostra de exemplo, não a suíte original de testes.
- **Comparativo** — a revisão manual que cruzou quais testes Robot tinham
  correspondente em Cypress e vice-versa. É o que mostrou que a contagem automática
  de "convertidos" feita pela IA vinha inflada (muitas conversões parciais ou
  triviais).

