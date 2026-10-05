# TASK-001 — ETAPA 006 — Testes manuais documentais

## 1. OBJETIVO

Executar exclusivamente a etapa de testes manuais documentais, conforme procedimento e critérios abaixo, produzindo evidências sem antecipar etapas.

## 2. CONTEXTO

TASK-001 — Fechar contratos e decisões técnicas de implementação; PHASE-01; CRITICAL; DEPENDS_ON: NONE. Estado observado em 05/10/2026: BLOCKED. É documental: consolidar contratos não significa implementar software. RNF-001/002/003/014 e ADR-001/002/003 são relações diretas; ADR-010/011/012 complementam decisões. RF/RN/UC constam N/A na ficha técnica, mas contratos afetados devem preservar rastreabilidade às regras concretas do README.

Decisões vigentes: sessões sem duração máxima/inatividade, com logout/revogação; título 100–200; número institucional anual imutável pelo ano da reunião; correção de e-mail somente da mesma identidade, sem fusão; distribuição de avisos por papel/vínculo; fim exclusivo. PD-006 já escolheu MFA por e-mail e TI/configuração para recuperação; PD-007 já fixou 26.214.400 bytes e ata + 10 anexos. Pendências: correção de data entre anos, scanner/indisponibilidade, detalhamento MFA/tarefa própria, PD-011 e contratos técnicos. Revalidar este retrato contra fontes posteriores.

## 3. PRÉ-CONDIÇÕES

WF-005 APROVADO com relatório/evidências; todos os predecessores continuam válidos.
Leia AGENTS.md, README.md, TASKS.md, ADRs relacionados, código e testes existentes nessa ordem. Não presumir ausência de software sem inventário. Etapas 001–002 são preparação da resolução, não início formal em IN_PROGRESS; etapas posteriores exigem decisões, DoR e autorização correspondentes. Evidência obrigatória ausente bloqueia avanço.

## 4. ENTRADAS NECESSÁRIAS

AGENTS.md; README.md (arquitetura, pendências e consolidação PD-010); TASKS.md (regras/gates/ficha TASK-001); docs/adr/ADR-001-typescript.md, ADR-002-monolito-modular.md, ADR-003-mysql-transacoes.md, ADR-010-revisao-2026-10-01.md, ADR-011-consolidacao-pd-010.md, ADR-012-mfa-interno.md; demais ADRs relacionados; contratos docs/architecture; relatórios validation relativos à TASK-001 e PDs. Receber decisões posteriores e evidências de gates predecessores quando aplicável. Relato histórico não é aprovação atual.

## 5. ARQUIVOS E COMPONENTES ENVOLVIDOS

Contratos system.md, data-model.md, api.md, security.md, operations.md, test-plan.md, references.md e pd-007-verificacao-arquivos.md em docs/architecture; ADRs; README; TASKS; validation. Impactos documentais sobre persistência, interface/API, segurança e notificações futuras; nenhum componente implementado nesta TASK. Modificar somente o subconjunto exigido pelo procedimento.

## 6. PROCEDIMENTO DETALHADO

1. Esta etapa é MANUAL, executada pelo responsável. Prepare o roteiro em docs/architecture; o agente não substitui o responsável. Comandos auxiliam leitura, não aprovam semântica. Não instalar Node, MySQL, Docker ou ClamAV para estes testes.
2. No PowerShell, responsável executa wsl --status e wsl -l -v e abre distribuição disponível com wsl. No Linux: cd /mnt/c/Users/amaffeis/Documents/git-repositories/pm2026tr01 (ajustar se mudou), pwd, command -v git, command -v rg, git status --short, git rev-parse HEAD. Se rg faltar, usar grep; WSL/Git ausente: BLOQUEADO, não inventar execução nem instalar automaticamente.
3. Registrar data/fuso, distribuição, branch/HEAD e sha256sum README.md TASKS.md docs/architecture/*.md docs/adr/*.md para identificar a revisão mesmo não commitada. Usar evidências sem credenciais/dados pessoais desnecessários.
4. Expandir cada linha abaixo em um caso completo e pedir execução/registro manual:

| Teste | Objetivo e pré-condição | Comandos de apoio | Procedimento e resultado esperado |
|---|---|---|---|
| T001 | Escopo; baseline disponível | git status --short; git diff --check; git diff; git diff --cached; git ls-files --others --exclude-standard | Ler também novos arquivos, comparar baseline e classificar PRIMARY; nenhuma mudança alheia incluída, software ou escopo proibido. |
| T002 | PD-010; resposta sobre ano registrada | rg -n 'PD-010\|sess\|ano\|título' README.md docs/architecture docs/adr | Conferir seis decisões de ADR-011 e complemento do ano; documentos concordam e versões substituídas estão identificadas. |
| T003 | MFA; procedimento definido | cat docs/adr/ADR-012-mfa-interno.md docs/architecture/security.md | Conferir perfis, novo login, 10min/5 erros/60s, TI/configuração, verificação, auditoria/revogação, ausência de bypass e tarefa futura. |
| T004 | Arquivos; scanner aprovado | cat docs/architecture/pd-007-verificacao-arquivos.md | Comparar 25 MiB, ata+10 anexos, limites de inspeção e estados/indisponibilidade com decisão explícita; nenhuma proposta tratada como aceita sem fonte. Não testar malware nesta TASK. |
| T005 | PD-011; pesquisa registrada | cat docs/architecture/references.md; rg -n 'versão\|licença\|compatibilidade\|digest' docs/architecture docs/adr | Abrir fontes oficiais registradas; comparar versões, suporte, peers/runtime, licenças, seleção/atualização; sem latest ou alegação de build executado. |
| T006 | Integridade/concorrência; contratos completos | cat docs/architecture/system.md docs/architecture/data-model.md docs/architecture/api.md | Traçar no papel publicação repetida, payload divergente, manifestação versus encerramento e vínculo ativo duplicado; resultado/erro/atomicidade/locks/histórico definidos. |
| T007 | Tempo/notificações; catálogo fechado | cat docs/architecture/operations.md docs/architecture/api.md | Traçar antes/no/depois do vencimento, aceite elegível às 23h e após, suspensão/reativação, destinatários e resultado incerto; respeitar ADR-011 e regras. |
| T008 | Rastreabilidade; documentos revisados | cat docs/architecture/test-plan.md; rg -n 'TASK-001\|TASK-002\|MFA\|DEPENDS_ON' TASKS.md | Conferir links locais, RNF-001/002/003/014, teste por critério, dependências sem ciclos e pendências de produção separadas; nenhum PASS/DONE indevido. |

5. Para cada linha, preencher formulário no roteiro (o ID varia de T001 a T008):

```text
TESTE: T001
Objetivo: [objetivo específico da linha]
Pré-condições: [decisões/gates/documentos exigidos]
Comandos: [comandos do caso; código esperado e tratamento de saída]
Procedimento:
1. Executar comandos e guardar saída/código.
2. Ler os documentos e comparar com as fontes da decisão.
3. Registrar divergências e resultado semântico.
Resultado esperado: [critério específico da tabela]
Resultado obtido: [PREENCHER MANUALMENTE]
Evidência: [PREENCHER MANUALMENTE: data, revisão/hashes, trechos e saídas]
STATUS:
[x] NÃO EXECUTADO
[ ] APROVADO
[ ] REPROVADO
[ ] BLOQUEADO
```

6. Após cada teste, mostrar PREVISTOS: 8; EXECUTADOS; APROVADOS; REPROVADOS; BLOQUEADOS; PENDENTES. EXECUTADOS = APROVADOS + REPROVADOS; 8 = EXECUTADOS + BLOQUEADOS + PENDENTES. Inicial: 0 executados/aprovados/reprovados/bloqueados, 8 pendentes.
7. Receber evidências do responsável e conferir revisão atual. Reprovação: diagnóstico → correção mínima autorizada → revisão → reexecução MANUAL do caso e afetados. Corrigir não aprova teste. Mudança posterior invalida evidências afetadas.
8. Aprovar gate somente com 8/8 executados e aprovados, zero reprovados/bloqueados/pendentes. Sem evidências, gate BLOQUEADO; TASK IN_REVIEW com situação AGUARDANDO TESTES MANUAIS. Decisão externa bloqueante exige BLOCKED conforme AGENTS. Auxiliares não substituem julgamento manual.

## 7. RESTRIÇÕES

ALLOWED CHANGES: docs/architecture/**, docs/adr/**, TASKS.md; README.md somente para decisões explicitamente aprovadas. validation/ é PRIMARY obrigatório por AGENTS.md. NO_INCIDENTAL_CHANGES: nenhuma alteração incidental permitida.

FORBIDDEN CHANGES: implementar software; alterar requisitos/negócio sem decisão explícita; tratar proposta como aprovada; implantar sem autorização; credenciais reais em arquivos/relatórios. Não criar aplicação, migrations, endpoints, package.json, lockfile ou testes funcionais da aplicação.

Não alterar AGENTS.md, prompts, docs/verification ou docs/diagrams na execução da TASK sem autorização de escopo. A geração avulsa destes prompts tem autorização própria e não amplia a ficha da TASK. Não inferir execução de READY/aprovação documental. Não iniciar automaticamente próxima etapa. Preservar alterações alheias e histórico. Conflito relevante sem substituição explícita: PARAR E SOLICITAR DECISÃO.

## 8. VALIDAÇÕES

Registrar comando, ambiente, data/fuso, saída/código e evidência. Conferir referências, coerência, decisões explícitas e escopo semântico. Build/lint/unitários/integração/API de software N/A nesta tarefa documental com justificativa, nunca PASS. Segurança e regressão documentais exigem revisão real; não comprovam software. Testes da etapa 006 são MANUAIS pelo responsável e não substituíveis por automação. Não dispensar gate obrigatório aplicável.

## 9. TRATAMENTO DE FALHAS

Interrompa avanço; registre operação/comando, código de saída, erro sanitizado, causa provável e evidência. Determine escopo da correção; proponha menor mudança e execute somente se autorizada. Repita validação e atualize gate/contagens. Falha de implementação documental/validação: FAILED, corrigir/revalidar antes de IN_REVIEW. Decisão externa: BLOCKED. Não ignorar falha, desabilitar validação ou inventar PASS. Em causa externa, emitir BLOCKER com TASK, problema, impacto, RF/RN/RNF/UC/ADR afetados, alternativas, recomendação e decisão necessária. Gravar tentativa em validation mesmo ao parar.

## 10. SCOPE ESCALATION

Antes de mudar fora do escopo, pare trabalho dependente e aguarde decisão. NO_INCIDENTAL_CHANGES não permite atalho. Apresente:

```text
## SCOPE ESCALATION
TASK: TASK-001
Necessidade identificada / Problema: ...
Motivo: ...
Arquivos/módulos afetados: ...
Allowed Changes atual: ...
Forbidden Changes relacionado: ...
Por que não é uma Incidental Change: ...
Alteração necessária e riscos: ...
Impacto se não realizada: ...
Alternativas: ampliar escopo; nova TASK; dependências; ADR; outra justificada.
Recomendação: ...
Decisão necessária: ...
```

## 11. CRITÉRIOS DE APROVAÇÃO

- [ ] Oito casos executados manualmente pelo responsável
- [ ] Oito aprovações com evidências da revisão atual
- [ ] Nenhuma reprovação, bloqueio ou pendência
- [ ] Correções revistas e reexecutadas manualmente

Todos obrigatórios, com evidência por item. Pendência/falha bloqueia próximo passo. Diagnóstico aprovado não resolve DoR da TASK.

## 12. GATE DA ETAPA

Gate WF-006: marcar itens da seção 11 OK/FALTA/FALHOU, informar critérios concluídos/total e pendentes/total. Inicialmente NÃO EXECUTADO. Resultado APROVADO/REPROVADO/BLOQUEADO por evidências. Próxima etapa HABILITADA somente com todos os critérios/predecessores satisfeitos; nunca iniciá-la automaticamente.

## 13. STATUS ACUMULADO DOS GATES

WF identifica workflow, distinto de GATE-01 a GATE-08 de qualidade de AGENTS.md. Atualizar pelos relatórios, nunca pré-aprovar:

| Gate | Etapa | Status |
|---|---|---|
| WF-001 | Recontextualização e histórico | PENDENTE — preencher pela evidência |
| WF-002 | Resolução de pendências e pesquisa técnica | PENDENTE — preencher pela evidência |
| WF-003 | Pré-condições e planejamento documental | PENDENTE — preencher pela evidência |
| WF-004 | Consolidação dos contratos | PENDENTE — preencher pela evidência |
| WF-005 | Revisão documental e preparação da validação | PENDENTE — preencher pela evidência |
| WF-006 | Testes manuais documentais | PENDENTE — preencher pela evidência |
| WF-007 | Validação final e conclusão | PENDENTE — preencher pela evidência |

GATES CONCLUÍDOS: X/7; GATES PENDENTES: Y/7 (todos não concluídos, incluindo bloqueados); GATES BLOQUEADOS: Z/7 (subconjunto dos pendentes). Inicial da geração: 0 concluídos, 7 pendentes, 0 bloqueados no workflow ainda não executado; TASK BLOCKED. Reprovação não conta como conclusão.

## 14. RESULTADO OBRIGATÓRIO

Gravar novo validation/TASK-001_YYYY-MM-DD_HH-mm-ss.md com fuso, status real da TASK, WF-006, objetivo, PRIMARY, Incidental Changes NONE, decisões, comandos/ambiente/resultados, oito gates de qualidade, Scope Validation, DoD, branch/commits ou ausência, pendências e próxima elegível. Incluir todos os campos do TASK Execution Report de AGENTS.md; referenciar em TASKS.md e conferir existência/conteúdo. Preservar relatórios; sufixo sequencial em colisão. Não marcar DONE por concluir etapa intermediária. AGUARDANDO TESTES MANUAIS é situação do relatório, não novo enum em TASKS.

Finalizar resposta com caminho do resumo e bloco preenchido:

```text
==================================================
TASK: TASK-001
ETAPA: 006
STATUS DA ETAPA: APROVADA | REPROVADA | BLOQUEADA
==================================================
GATE DA ETAPA: APROVADO | REPROVADO | BLOQUEADO
GATES TOTAIS: 7
GATES CONCLUÍDOS: X
GATES PENDENTES: Y
GATES BLOQUEADOS: Z
PROBLEMAS ENCONTRADOS:
- ...
CORREÇÕES REALIZADAS:
- ...
PENDÊNCIAS:
- ...
TESTES RELACIONADOS:
- ...
PRÓXIMA ETAPA: prompt-task-001-etapa-007-conclusao.md
PRÓXIMA ETAPA HABILITADA: SIM | NÃO
MOTIVO: ...
==================================================
```

Parar após o relatório da etapa. Na conclusão, não executar a próxima TASK.
