# Test Complexity Rubric / Rubrica de Complexidade de Teste

## English

The complexity column in the per-feature table is a **qualitative** classification
of ours. We did not compute numeric metrics. Instead we adapted the web-application
testability criteria of Bureš (2015) and the observability/controllability factors
of Garousi et al. (2019) into a five-factor rubric, evaluated each feature against
it, and assigned the label that predominated.

### The five factors

| Factor | Low | Medium | High |
|---|---|---|---|
| Interaction flow (Bureš) | single screen | 2–3 steps | multi-step across screens |
| Business logic | absent | localized | extensive |
| Result observability (Garousi) | visible in the UI | derived state | backend only |
| Controllability: setup & data (Garousi) | minimal | partial | heavy (seed/state needed) |
| Element identifiability (Bureš) | stable selectors | partial | fragile / text-based |

**How to read it.** For each feature we judged where it fell on each row. A feature
sitting mostly in the left column was labeled *low*; mostly center, *medium*; mostly
right, *high*. The label is the predominant column, not an average score — a single
very fragile or very backend-dependent factor could pull an otherwise simple feature
up, and we noted such cases when reviewing.

### Resulting classification

| Feature | Complexity | Main driver |
|---|---|---|
| CRUD Empresa | low | single-screen CRUD, UI-visible result |
| Categorias | low | short CRUD flow |
| Produtos | low | CRUD with simple persistence check |
| Fornecedores | low | CRUD, stable selectors |
| Lançamento de Estoque | medium | derived total to verify |
| Cotação | medium | value calculation, few cases |
| Resposta de Fornecedor | high | multi-step, backend state |
| Realizar Pedidos | high | contextual rules, multi-step |
| Compra Manual | medium | partial logic, heavier setup |
| Confirmação de Pedidos | high | backend status change |
| Finalização de Pedidos | high | price update + status, backend |
| Painel Gerencial | high | aggregated/derived data, fragile selectors |

**Important.** Complexity and failure rate do not move together. Compra Manual is
*medium* and failed a lot; Resposta de Fornecedor is *high* and barely failed. That
is why we treat the within-session quality decay as a **hypothesis**, not a proven
cause — if complexity alone drove failures, the high-complexity features would fail
most, and they did not.

### References

- Bureš, M. (2015). *Metrics for Automated Testability of Web Applications.*
  CompSysTech '15. doi:10.1145/2812428.2812458
- Garousi, V.; Felderer, M.; Kılıçaslan, F. N. (2019). *A Survey on Software
  Testability.* Information and Software Technology 108.
  doi:10.1016/j.infsof.2018.12.003

---

## Português

A coluna de complexidade na tabela por funcionalidade é uma classificação
**qualitativa** nossa. Não calculamos métricas numéricas. Em vez disso, adaptamos os
critérios de testabilidade de aplicações web de Bureš (2015) e os fatores de
observabilidade e controlabilidade de Garousi et al. (2019) em uma rubrica de cinco
fatores, avaliamos cada funcionalidade e demos o rótulo que predominava.

### Os cinco fatores

| Fator | Baixa | Média | Alta |
|---|---|---|---|
| Fluxo de interação (Bureš) | tela única | 2 a 3 etapas | multi-etapa entre telas |
| Lógica de negócio | ausente | pontual | extensa |
| Observabilidade do resultado (Garousi) | visível na interface | estado derivado | só no backend |
| Controlabilidade: setup e dados (Garousi) | mínima | parcial | alta (precisa de seed/estado) |
| Identificabilidade dos elementos (Bureš) | seletores estáveis | parcial | frágil / baseada em texto |

**Como ler.** Para cada funcionalidade, julgamos em que coluna ela caía em cada
linha. Predominância à esquerda → *baixa*; ao centro → *média*; à direita → *alta*.
O rótulo é a coluna predominante, não uma média — um único fator muito frágil ou
muito dependente do backend podia puxar para cima uma funcionalidade simples, e
anotamos esses casos na revisão.

### Classificação resultante

| Funcionalidade | Complexidade | Fator principal |
|---|---|---|
| CRUD Empresa | baixa | CRUD de tela única, resultado visível na UI |
| Categorias | baixa | fluxo CRUD curto |
| Produtos | baixa | CRUD com checagem de persistência simples |
| Fornecedores | baixa | CRUD, seletores estáveis |
| Lançamento de Estoque | média | total derivado a verificar |
| Cotação | média | cálculo de valor, poucos casos |
| Resposta de Fornecedor | alta | multi-etapa, estado no backend |
| Realizar Pedidos | alta | regras contextuais, multi-etapa |
| Compra Manual | média | lógica parcial, setup mais pesado |
| Confirmação de Pedidos | alta | mudança de status no backend |
| Finalização de Pedidos | alta | atualização de preço + status, backend |
| Painel Gerencial | alta | dados agregados/derivados, seletores frágeis |

**Importante.** Complexidade e taxa de falha não andam juntas. Compra Manual é
*média* e falhou muito; Resposta de Fornecedor é *alta* e quase não falhou. Por isso
tratamos o decaimento de qualidade ao longo da sessão como **hipótese**, e não como
causa comprovada — se só a complexidade explicasse as falhas, as funcionalidades de
alta complexidade falhariam mais, e não foi o que ocorreu.

### Referências

- Bureš, M. (2015). *Metrics for Automated Testability of Web Applications.*
  CompSysTech '15. doi:10.1145/2812428.2812458
- Garousi, V.; Felderer, M.; Kılıçaslan, F. N. (2019). *A Survey on Software
  Testability.* Information and Software Technology 108.
  doi:10.1016/j.infsof.2018.12.003
