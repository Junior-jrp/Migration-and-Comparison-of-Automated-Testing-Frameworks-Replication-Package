# How the AI Was Used / Como a IA Foi Utilizada

## English

This section describes how artificial intelligence was employed at each stage of the migration process and presents representative prompts. The examples are illustrative approximations rather than verbatim records of the interactions. They are intended to provide a reproducible reference for readers interested in following a similar workflow. The models used were **Claude Opus 4.8** as the primary model and **Gemini 3.1 Pro** as an auxiliary model. Both were accessed through the command line from within the project repository.

### Stage 1 — Mass migration

The initial migration was conducted over approximately two to three extended sessions with Claude, each organized around a specific objective. The first session focused on mapping the existing test cases and documenting their behavior so that the model could establish the purpose of each test. The second focused on the bulk conversion of Robot Framework files to Cypress. The final session was dedicated to reviewing and validating the generated tests. This staged approach avoided relying on a single generic prompt and allowed each phase to provide context for the next.

### Stage 2 — Targeted corrections

The subsequent work focused on individual cases. For tests that had already been converted, the prompts described the identified problem, specified the expected result, and indicated the relevant files and directories. For tests that had not been converted, the corresponding Robot Framework directory was provided alongside the related function and variable files. The model was then instructed to convert the tests in the relevant suite.

### Lessons learned

As the codebase expanded, the amount of human intervention required also increased. The AI tended to produce functions that were longer and more complex than necessary. In several cases, the generated implementation had to be revised because a straightforward action had been implemented in an unnecessarily complicated manner. The experience suggests that AI assistance was most effective when applied selectively to clearly delimited code segments.

Alternating between Codex and Claude introduced additional inconsistencies and increased the need for manual intervention. Frequent changes across successive prompts also made it more difficult to track the modifications made to the codebase. By contrast, the AI was effective at reproducing patterns that had already been corrected manually, including value corrections, string checks, and concrete details such as page addresses.

### A broader application requiring careful validation

AI was also used to compare the Cypress tests with the original Robot Framework tests and identify which cases had been migrated. The initial comparison overestimated the extent of the migration. Some tests classified as converted were trivial, such as tests that checked only the page title, while others covered only part of the behavior implemented by the original Robot Framework test. A subsequent manual review produced substantially lower figures than those initially reported by the AI. The revised comparison is available in the spreadsheet's `Comparativo` worksheet.

### Example prompts

The following prompts illustrate the types of instructions used throughout the process. They are representative examples and should not be interpreted as verbatim interaction logs.

#### Stage 1 — Mapping and documentation

1. "Scan the `tests/robot/` folder and list every test suite with its test cases. For each case, summarize in one line what it validates."
2. "Read the suite `empresa.robot` and the resources it imports. Write, for each test case, the business rule being checked and the expected end state."
3. "Build a table mapping each custom Robot keyword to the UI action it performs, so it can be reused as a reference during the migration."
4. "Go through the `resources/` keywords and identify which ones depend on test data or setup that will require a Cypress equivalent."

#### Stage 1 — Mass migration

5. "Convert the test cases in `produtos.robot` to Cypress, keeping the same assertions. Preserve the business validation, not just the success message."
6. "Migrate `fornecedores.robot` to Cypress. Use `data-*` selectors where the DOM provides them instead of text labels, and keep one `it()` per original test case."
7. "Translate the suite `categorias.robot`. For each converted test, add a comment with the name of the original Robot test it came from."
8. "Convert `lancamento_estoque.robot`. Where the Robot test reads a value and checks a derived total, reproduce that calculation check in Cypress rather than replacing it with a generic assertion."

#### Stage 1 — Validation

9. "Review the Cypress files you just generated and list any test that passes without asserting the business result, such as a test that only checks whether a message appears."
10. "Compare the converted `pedidos` specs against the original Robot cases and flag any assertion that was dropped or weakened during translation."
11. "Run the converted suite and, for each failure, indicate whether it is caused by a syntax issue, an incorrect assertion, or a missing selector."

#### Stage 2 — Targeted corrections to converted tests

12. "In `confirmacao_pedidos.cy.js`, the test passes but does not verify the status change in the backend. The original Robot test checked both the price update and the status. Update the Cypress test to assert both. Files involved: `confirmacao_pedidos.cy.js` and `support/pedidos.js`."
13. "This converted test uses `contain` where it should use `have.text`. Correct the comparator and restore the intermediate assertions that were removed."
14. "The selector `cy.contains('Remover')` is fragile, and 'Remover' here means *deactivate*, not delete the row. Replace it with a stable selector and assert that the item becomes inactive rather than disappears."
15. "Refactor this function because it is unnecessarily long. The required action is simple: fill in the form, submit it, and assert that the record was created. Keep the implementation concise and direct."

#### Stage 2 — Converting tests that were not migrated

16. "This folder contains the Robot code for `compra_manual` along with its function and variable files. Convert the tests in this suite to Cypress, reusing the existing `support/` helpers."
17. "Convert `finalizacao_pedidos.robot`, which was omitted from the first pass. Preserve the price-update and status-change checks performed by the original test."
18. "The `painel_gerencial` suite was not generated. Use the provided Robot files and related resources to convert every test case without omitting any."

#### Reapplying corrected patterns and comparing results

19. "Apply the same correction used in `produtos.cy.js`—a stable selector and a persistence assertion—to the equivalent tests in `categorias.cy.js` and `fornecedores.cy.js`."
20. "Compare the Cypress specs with the Robot suites and list which Robot tests have a genuine Cypress counterpart. Mark as *partial* any Cypress test that covers only part of the original, and as *trivial* any test that checks only page loading."

---

## Português

Esta seção descreve como a inteligência artificial foi empregada em cada etapa do processo de migração e apresenta exemplos representativos de prompts. Os exemplos são aproximações ilustrativas, e não registros literais das interações. Seu objetivo é oferecer uma referência reproduzível para leitores interessados em adotar um fluxo de trabalho semelhante. Foram utilizados o **Claude Opus 4.8**, como modelo principal, e o **Gemini 3.1 Pro**, como modelo auxiliar. Ambos foram acessados por meio da linha de comando, no diretório do repositório do projeto.

### Etapa 1 — Migração em massa

A migração inicial foi conduzida em aproximadamente duas a três sessões extensas com o Claude, cada uma organizada em torno de um objetivo específico. A primeira sessão teve como foco o mapeamento dos casos de teste existentes e a documentação de seus comportamentos, de modo a estabelecer a finalidade de cada teste. A segunda foi dedicada à conversão em massa dos arquivos do Robot Framework para Cypress. Por fim, a terceira sessão concentrou-se na revisão e na validação dos testes gerados. Essa abordagem em etapas evitou a dependência de um único prompt genérico e permitiu que cada fase fornecesse o contexto necessário à fase seguinte.

### Etapa 2 — Correções pontuais

Na etapa seguinte, o trabalho passou a se concentrar em casos individuais. Para os testes já convertidos, os prompts descreviam o problema identificado, especificavam o resultado esperado e indicavam os arquivos e diretórios relevantes. Para os testes ainda não convertidos, eram fornecidos o diretório correspondente do Robot Framework e os arquivos relacionados a funções e variáveis. A partir desse material, solicitava-se a conversão dos testes da suíte em questão.

### Lições aprendidas

Com a expansão da base de código, também aumentou a necessidade de intervenção humana. A IA tendia a produzir funções mais longas e complexas do que o necessário. Em diversos casos, as implementações geradas precisaram ser revisadas, pois ações relativamente simples haviam sido implementadas de maneira excessivamente elaborada. A experiência indica que o uso da IA foi mais eficaz quando aplicado de forma seletiva a trechos de código bem delimitados.

A alternância entre Codex e Claude introduziu inconsistências adicionais e ampliou a necessidade de intervenção manual. Além disso, as mudanças frequentes realizadas a cada novo prompt dificultaram o acompanhamento das modificações na base de código. Em contrapartida, a IA demonstrou eficácia na reprodução de padrões previamente corrigidos de forma manual, incluindo ajustes de valores, verificações de strings e detalhes objetivos, como endereços de páginas.

### Aplicação de escopo mais amplo que exigiu validação cuidadosa

A IA também foi utilizada para comparar os testes em Cypress com os testes originais do Robot Framework e identificar quais casos haviam sido migrados. A comparação inicial superestimou a extensão da migração. Alguns testes classificados como convertidos eram triviais, como aqueles que verificavam apenas o título da página, enquanto outros contemplavam somente parte do comportamento implementado pelo teste original. Uma revisão manual posterior produziu quantitativos consideravelmente inferiores aos inicialmente apresentados pela IA. A comparação revisada está disponível na aba `Comparativo` da planilha.

### Exemplos de prompts

Os prompts a seguir ilustram os tipos de instruções utilizados ao longo do processo. São exemplos representativos e não devem ser interpretados como transcrições literais das interações.

#### Etapa 1 — Mapeamento e documentação

1. "Examine a pasta `tests/robot/` e liste todas as suítes e seus respectivos casos de teste. Para cada caso, resuma em uma linha o que é validado."
2. "Leia a suíte `empresa.robot` e os recursos importados por ela. Para cada caso de teste, descreva a regra de negócio verificada e o estado final esperado."
3. "Elabore uma tabela que relacione cada palavra-chave personalizada do Robot à ação de interface executada, para que ela possa ser utilizada como referência durante a migração."
4. "Examine as keywords de `resources/` e identifique aquelas que dependem de dados de teste ou de configurações iniciais que precisarão de um equivalente em Cypress."

#### Etapa 1 — Migração em massa

5. "Converta os casos de teste de `produtos.robot` para Cypress, preservando as mesmas asserções. Mantenha a validação da regra de negócio, e não apenas a verificação da mensagem de sucesso."
6. "Migre `fornecedores.robot` para Cypress. Utilize seletores `data-*` quando estiverem disponíveis no DOM, em vez de rótulos textuais, e mantenha um `it()` para cada caso de teste original."
7. "Converta a suíte `categorias.robot`. Para cada teste convertido, adicione um comentário com o nome do teste original do Robot Framework que lhe deu origem."
8. "Converta `lancamento_estoque.robot`. Quando o teste Robot ler um valor e verificar um total derivado, reproduza essa verificação de cálculo em Cypress, em vez de substituí-la por uma asserção genérica."

#### Etapa 1 — Validação

9. "Revise os arquivos Cypress gerados e liste os testes que são aprovados sem verificar o resultado de negócio, como aqueles que apenas verificam se uma mensagem é exibida."
10. "Compare as especificações convertidas de `pedidos` com os casos originais do Robot Framework e identifique as asserções removidas ou enfraquecidas durante a conversão."
11. "Execute a suíte convertida e, para cada falha, indique se a causa é um problema de sintaxe, uma asserção incorreta ou a ausência de um seletor."

#### Etapa 2 — Correções pontuais em testes já convertidos

12. "Em `confirmacao_pedidos.cy.js`, o teste é aprovado, mas não verifica a alteração de status no backend. O teste original do Robot Framework verificava tanto a atualização do preço quanto o status. Corrija o teste Cypress para validar ambos. Arquivos envolvidos: `confirmacao_pedidos.cy.js` e `support/pedidos.js`."
13. "Este teste convertido utiliza `contain` quando deveria utilizar `have.text`. Corrija o comparador e restaure as asserções intermediárias que foram removidas."
14. "O seletor `cy.contains('Remover')` é frágil, e, neste contexto, 'Remover' significa *desativar*, e não excluir a linha. Substitua-o por um seletor estável e verifique se o item se torna inativo, em vez de verificar se ele desaparece."
15. "Refatore esta função, pois ela está excessivamente longa. A ação necessária é simples: preencher o formulário, enviá-lo e verificar a criação do registro. Mantenha a implementação concisa e direta."

#### Etapa 2 — Conversão de testes ainda não migrados

16. "Esta pasta contém o código Robot da suíte `compra_manual`, além dos arquivos de funções e variáveis correspondentes. Converta os testes dessa suíte para Cypress, reutilizando os helpers existentes em `support/`."
17. "Converta `finalizacao_pedidos.robot`, que não foi incluído na primeira etapa. Preserve as verificações de atualização de preço e de alteração de status realizadas pelo teste original."
18. "A suíte `painel_gerencial` não foi gerada. Utilize os arquivos Robot fornecidos e os recursos relacionados para converter todos os casos de teste, sem omissões."

#### Reaplicação de padrões corrigidos e comparação dos resultados

19. "Aplique aos testes equivalentes de `categorias.cy.js` e `fornecedores.cy.js` a mesma correção utilizada em `produtos.cy.js`: um seletor estável e uma asserção de persistência."
20. "Compare as especificações Cypress com as suítes Robot e liste os testes Robot que possuem correspondentes efetivos em Cypress. Classifique como *parcial* cada teste Cypress que contemple apenas parte do teste original e como *trivial* aquele que verifique apenas o carregamento da página."
