# Failure Taxonomy / Taxonomia de Falhas

## English

The six failure types that most often appeared in the machine translation (Table 7
of the paper). We did not start from a ready-made taxonomy: we annotated problems
during the correction work and, in the retrospectives, grouped the recurring ones
until the set stabilized.

### The six types

**F1 — Syntax failures.** Commands that do not exist in the Cypress API, wrong
imports, and misuse of async. Frequent at the start, resolved by hand or in short
cycles with the model.
*Example:* a Robot keyword translated to a non-existent `cy.*` command, or an
assertion chained after an un-awaited command so it ran against a stale DOM.

**F2 — Loss of business logic.** The most serious case. Specific rules (value
calculation in quotes, contextual blocking in orders) turned into generic
validations.
*Typical example:* in Finalização de Pedidos the original test checked the price
update and the status change; the translation ended up checking only the success
message, without confirming the backend change.

**F3 — Incorrect assertions.** A swapped comparator (`contain` instead of
`have.text`, for instance) and intermediate assertions that disappeared. In the
worst cases the test passed without really checking anything.

**F4 — Ignored or untranslated tests.** About 10% of cases were left out in the
first translation, for two reasons: silent omission (the model returned only part of
the scope, without warning) and loss of context in the long sessions. It
concentrated toward the end of the session; in Painel Gerencial the omission was
total.

**F5 — API and business hallucinations.** The model proposed touching classes,
functions, and components that did not exist. It dropped considerably when we moved
from the IDE extension to the command line. There was also hallucination of meaning:
"Remover" (Remove) was interpreted as making the row disappear from the screen, when
in the system it only meant deactivating the item.

**F6 — Fragile, unmapped selectors.** Instead of Robot's stable XPaths, the
translation used text labels and context strings, and did not create a reusable
component layer. Result: changing one label requires touching several files.

### Two patterns that emerged later

After the six types were settled, two more patterns showed up and are worth naming:

- **Trivial tests to inflate coverage** — checking that a screen loaded, with no
  real validation. This is one of the things the `Comparativo` sheet exposes.
- **Over-engineered solutions to simple problems** — functions that grew far beyond
  what the action required and had to be trimmed by hand.

### Where to see them

Each note in the `Rastreabilidade` sheet references the relevant failure code (F1–F6)
so the taxonomy can be traced to concrete cases.

---

## Português

Os seis tipos de falha que mais apareceram na tradução automática (Tabela 7 do
artigo). Não partimos de categorias prontas: fomos anotando os problemas durante a
correção e, nas retrospectivas, agrupando os que se repetiam até o conjunto
estabilizar.

### Os seis tipos

**F1 — Falhas de sintaxe.** Comandos que não existem na API do Cypress, imports
errados e uso indevido de assíncrono. Frequente no começo, resolvido na mão ou em
ciclos curtos com o modelo.
*Exemplo:* uma keyword do Robot traduzida para um comando `cy.*` inexistente, ou uma
asserção encadeada após um comando sem `await`, rodando contra um DOM desatualizado.

**F2 — Perda de lógica de negócio.** O caso mais sério. Regras específicas (cálculo
de valor em cotações, bloqueio contextual em pedidos) viravam validações genéricas.
*Exemplo típico:* em Finalização de Pedidos, o teste original checava a atualização
de preços e a mudança de status, e a tradução passou a checar só a mensagem de
sucesso, sem confirmar a mudança no backend.

**F3 — Asserções incorretas.** Troca de comparador (`contain` no lugar de
`have.text`, por exemplo) e asserções intermediárias que sumiram. Nos casos piores o
teste passava sem checar nada de verdade.

**F4 — Testes ignorados ou não traduzidos.** Cerca de 10% dos casos ficaram de fora
na primeira tradução, por dois motivos: omissão silenciosa (o modelo devolvia só
parte do escopo, sem avisar) e perda de contexto nas sessões longas. Concentrou-se no
fim da sessão; no Painel Gerencial a omissão foi total.

**F5 — Alucinações de API e de negócio.** O modelo propunha mexer em classes, funções
e componentes que não existiam. Diminuiu bastante quando trocamos a extensão de IDE
pela linha de comando. Também houve alucinação de significado: "Remover" foi
interpretado como sumir a linha da tela, quando no sistema significava apenas
desativar o item.

**F6 — Seletores frágeis, sem mapeamento.** Em vez dos XPath estáveis do Robot, a
tradução usou rótulos de texto e strings de contexto, e não criou uma camada de
componentes reutilizáveis. Resultado: mudar um rótulo exige mexer em vários arquivos.

### Dois padrões que apareceram depois

Depois que os seis tipos já estavam fechados, surgiram mais dois padrões que vale
nomear:

- **Testes triviais para inflar cobertura** — verificar que uma tela carregou, sem
  validação de fato. É uma das coisas que a aba `Comparativo` expõe.
- **Soluções complicadas demais para problemas simples** — funções que cresceram
  muito além do que a ação exigia e precisaram ser enxugadas na mão.

### Onde vê-los

Cada observação na aba `Rastreabilidade` remete ao código de falha pertinente (F1–F6),
para que a taxonomia possa ser rastreada até casos concretos.
