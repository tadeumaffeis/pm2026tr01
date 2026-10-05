Este documento define as regras obrigatórias para qualquer agente de programação que opere neste repositório.

# Contrato operacional

## 1. Estado inicial e autorização

Este repositório contém planejamento, não implementação. A aprovação dos artefatos não autoriza iniciar software ou implantar. Quando o usuário autorizar execução, selecionar a primeira TASK elegível; por padrão executar apenas uma e parar após relatório. Execução contínua somente se explicitamente autorizada.

## 2. Ordem de leitura e fontes

Antes de cada TASK ler: AGENTS.md; README.md; TASKS.md; ADRs relacionados; código existente; testes existentes.

- README.md: requisitos, regras, domínio, arquitetura, APIs e escopo.
- TASKS.md: backlog, dependências, prioridade, estados, Scope Guard e critérios operacionais.
- AGENTS.md: processo, comportamento e restrições do agente.
- docs/adr/: decisões arquiteturais; docs/architecture/ detalha contratos incorporados ao README.

Orientação: requisitos aprovados → ADRs aceitos → contrato operacional → ficha da tarefa → código. Conflitos relevantes não são resolvidos silenciosamente por essa ordem: PARAR E SOLICITAR DECISÃO. Instruções explícitas posteriores do usuário devem ser registradas nas fontes afetadas; não usar código existente como autorização para alterar requisito.

## 3. Seleção e Definition of Ready

Consultar primeira tarefa READY na ordem, prioridade e fase estabelecidas. Confirmar requisitos, contratos, critérios de aceitação, testes, decisões, ausência de pendências bloqueantes e os três componentes do Scope Guard. Se nenhuma elegível, informar impedimento e parar.

Para cada DEPENDS_ON, confirmar DONE, existência de artefatos e implementação aplicável, testes correspondentes passando e ausência de regressão conhecida. Dependência documental exige documento/evidência em vez de código inexistente. Se falhar: BLOCKED, registrar motivo e parar; não pular dependência. Promover BLOCKED para READY apenas após DoR completa, sem inferir autorização para iniciar.

## 4. Branches e início

Não desenvolver em main. Padrões: feature/TASK-xxx-descricao-curta, fix/TASK-xxx-descricao-curta, chore/TASK-xxx-descricao-curta. Uma tarefa por branch preferencialmente. Inspecionar estado do repositório; preservar alterações alheias. Depois da autorização e DoR, criar branch e atualizar READY → IN_PROGRESS em TASKS.md (índice e ficha). Não atualizar README apenas para estado operacional.

## 5. Scope Guard

Allowed Changes é escopo primário esperado. Incidental Changes são exceções mínimas diretamente causadas pela tarefa. Forbidden Changes é limite forte e prevalece sobre ambos, conveniência e refatoração.

Antes de mudar fora de Allowed Changes perguntar: “Esta alteração somente se tornou necessária como consequência direta da TASK atual?” Se não, não pertence à tarefa.

Teste incidental, todos aplicáveis obrigatórios:
1. Necessária para implementar, compilar, testar ou integrar a tarefa.
2. Causada diretamente pela tarefa.
3. Menor mudança razoável e localizada.
4. Não introduz funcionalidade independente.
5. Não cria ou altera regra de negócio.
6. Não modifica arquitetura relevante.
7. Não quebra contrato público.
8. Não altera comportamento relevante de segurança/autenticação/autorização/proteção de dados.
9. Não viola Forbidden Changes.

MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED permite só o que passar no teste. NO_INCIDENTAL_CHANGES proíbe exceção. Imports, exports, tipos, registro de componente e fixtures diretamente afetados podem ser incidentais; não são licença para reorganização, atualização oportunista, limpeza geral, bugs alheios ou refatoração ampla.

Múltiplos módulos não relacionados, mudança estrutural, arquitetural, contratual ou de negócio excedem o orçamento incidental: PARAR. Uma proibição necessária impede avanço até decisão. Na definição das tarefas, caminhos são categorias precisas de responsabilidade, não sandbox cego.

## 6. Scope Escalation

Apresentar quando necessário e aguardar decisão para o trabalho dependente:

```text
## SCOPE ESCALATION
TASK: TASK-xxx
Necessidade identificada: ...
Motivo: ...
Arquivos/módulos afetados: ...
Allowed Changes atual: ...
Forbidden Changes relacionado: ...
Por que não é uma Incidental Change: ...
Impacto se não realizada: ...
Alternativas: ampliar Allowed Changes; nova TASK; rever dependências; ADR; revisão arquitetural; outra justificada.
Recomendação: ...
Decisão necessária: ...
```

Não implementar tarefa futura. Se descobrir necessidade, avaliar incidental; localizar tarefa existente ou propor nova com rastreabilidade e dependências. IDs nunca reutilizados ou renumerados. Não inventar decisões de negócio para resolver PD.

## 7. Qualidade e DoD

GATE-01 Build (inclui tipos); GATE-02 Lint; GATE-03 Unit Tests; GATE-04 Integration Tests; GATE-05 API Tests; GATE-06 Security Checks; GATE-07 Acceptance Criteria; GATE-08 Regression Tests.

Executar os gates aplicáveis, registrar comandos, ambiente, resultado e evidência. N/A exige justificativa, não pode dispensar gate obrigatório. Tarefa documental pode justificar gates de software como N/A. Nunca afirmar execução não realizada, remover testes ou desabilitar validações para obter aprovação.

DoD global: implementação/artefato concluído; gates aplicáveis passam; critérios satisfeitos; regras e APIs preservadas; segurança e erros adequados; documentação necessária atualizada; sem regressão conhecida; commits rastreáveis; TASKS atualizado; diffs primários no escopo; incidentais aprovados pelo teste; nenhum proibido; nenhuma mudança colateral injustificada ou scope creep.

Antes de IN_REVIEW → DONE classificar todo arquivo alterado PRIMARY ou INCIDENTAL; validar semântica além do caminho. Falha obrigatória impede DONE. Ao concluir implementação usar IN_REVIEW; só promover depois da validação. Checkpoint final de cada fase bloqueia a seguinte enquanto não DONE.

## 8. Commits

Conventional Commits: <tipo>(<escopo>): <descrição> [TASK-xxx]. Tipos: feat, fix, test, refactor, docs, chore, build, ci. Commits pequenos, coesos e da tarefa; não misturar mudanças alheias. Não realizar merge, publicação ou implantação além da autorização vigente.

## 9. Parada e blockers

Parar por ambiguidade relevante, contradição, dependência ausente, regra indefinida, decisão arquitetural relevante não registrada, expansão significativa, necessidade de Forbidden Changes, Scope Guard inviável, risco de segurança/perda de dados, quebra de contrato ou testes anteriores falhando por causa externa.

```text
## BLOCKER
TASK: TASK-xxx
Problema: ...
Impacto: ...
RF/RN/RNF/UC/ADR afetados: ...
Alternativas: ...
Recomendação: ...
Decisão necessária: ...
```

Atualizar BLOCKED quando depende de decisão externa. Falha de implementação/validação: FAILED; registrar diagnóstico, corrigir e revalidar antes de retornar IN_REVIEW. Fluxo normal BLOCKED → READY → IN_PROGRESS → IN_REVIEW → DONE. CANCELLED preserva ID e motivo.

## 10. Relatório final obrigatório

### Gravação obrigatória em validation

Ao final de cada tarefa ou tentativa de execução, antes da resposta final e antes de iniciar outra tarefa, gerar e gravar um resumo em Markdown na pasta `validation/`, localizada na raiz do projeto. Criar a pasta se ainda não existir. A obrigação também vale para tarefas documentais, falhas, bloqueios, cancelamentos e entregas em revisão; apresentar o resumo somente no chat não atende a esta regra.

- Nome do arquivo: `validation/TASK-xxx_YYYY-MM-DD_HH-mm-ss.md`. Em solicitações sem ID no backlog, usar `validation/avulsa-descricao-curta_YYYY-MM-DD_HH-mm-ss.md`, sem inventar ou reutilizar IDs de TASK.
- Preservar resumos anteriores. Cada tentativa gera um novo arquivo; se houver colisão de nome, acrescentar um sufixo sequencial.
- Registrar identificação e objetivo da tarefa, data/hora com fuso, status final, resumo do que foi realizado, arquivos alterados, decisões, verificações realmente executadas e resultados, pendências/bloqueios e próximo passo. Informar branch e commits quando existirem; caso contrário, declarar que não se aplicam ou não foram criados.
- Para tarefas do backlog, incluir os campos do TASK Execution Report abaixo; o mesmo arquivo pode conter o resumo e o relatório completo. Referenciar o caminho do resumo no registro da tarefa em TASKS.md.
- Não incluir senhas, tokens, credenciais ou dados pessoais desnecessários. Testes não executados devem ser identificados; N/A exige justificativa.
- A gravação do resumo da própria tarefa em `validation/` é uma alteração documental primária obrigatória de todas as tarefas, inclusive quando a ficha não listar esse caminho e quando a política for NO_INCIDENTAL_CHANGES. Essa autorização não permite alterar resumos de outras tarefas nem ampliar o escopo funcional.
- Conferir a existência e o conteúdo do arquivo após gravá-lo. A Definition of Done exige o resumo persistido e verificado. Se a gravação falhar, informar o impedimento e não declarar a tarefa DONE.

Na resposta final, informar o nome do resumo gravado. Esta regra complementa o registro operacional em TASKS.md e os relatórios de verificação existentes.

### Modelo do relatório

```text
## TASK Execution Report
TASK: TASK-xxx
Status: DONE | FAILED | BLOCKED | IN_REVIEW
Branch: ...
Commits: ...
### Primary Changes
...
### Incidental Changes
| Arquivo/Componente | Alteração | Justificativa |
|---|---|---|
Ou Incidental Changes: NONE
### Tests Executed
Comandos, ambiente e evidências reais.
### Quality Gates
| Gate | Resultado |
|---|---|
| Build | PASS/FAIL/N/A justificado |
| Lint | PASS/FAIL/N/A justificado |
| Unit Tests | PASS/FAIL/N/A justificado |
| Integration Tests | PASS/FAIL/N/A justificado |
| API Tests | PASS/FAIL/N/A justificado |
| Security | PASS/FAIL/N/A justificado |
| Acceptance Criteria | PASS/FAIL |
| Regression | PASS/FAIL/N/A justificado |
### Scope Validation
Allowed Changes: PASS/FAIL
Incidental Changes: PASS/FAIL/NONE
Forbidden Changes: PASS/FAIL
Scope Creep: NONE ou descrição do desvio
### Definition of Done
PASS | FAIL
### Next Eligible TASK
TASK-xxx | NONE
```

Depois do relatório identificar próxima tarefa e PARAR, salvo autorização expressa de continuidade. Repetir integralmente validação em cada tarefa, mesmo em execução contínua.

## 11. Atualizações documentais

TASKS recebe estados, execução, commits, gates e checkpoints. README muda só por especificação/escopo/arquitetura/API/modelo/documentação estrutural. ADR significativo individual; marcar substituição, nunca apagar justificativa histórica. Testes e código são consequência do planejamento, não sua fonte de requisitos.
