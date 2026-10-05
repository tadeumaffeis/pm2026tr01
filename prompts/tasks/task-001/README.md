# TASK-001 — Fechar contratos e decisões técnicas de implementação

Objetivo: resolver PD-010/011 e partes contratuais de PD-007, detalhando propostas sem inventar negócio. PHASE-01; CRITICAL; DEPENDS_ON: NONE. Estado inicial consultado em 05/10/2026: BLOCKED. Nenhuma etapa executada nesta geração.

Workflow gerado exclusivamente para TASK-001. Etapas 001–002 preparam diagnóstico/resolução; não pressupõem READY. Consolidação formal exige DoR e autorização. A geração não implementa software nem autoriza implantação.

## Sequência

| Ordem | Etapa | Arquivo | GATE | Dependência |
|---:|---|---|---|---|
| 001 | Recontextualização e histórico | [prompt-task-001-etapa-001-recontextualizacao.md](prompt-task-001-etapa-001-recontextualizacao.md) | WF-001 | — |
| 002 | Resolução de pendências e pesquisa técnica | [prompt-task-001-etapa-002-resolucao-pendencias.md](prompt-task-001-etapa-002-resolucao-pendencias.md) | WF-002 | WF-001 |
| 003 | Pré-condições e planejamento documental | [prompt-task-001-etapa-003-planejamento.md](prompt-task-001-etapa-003-planejamento.md) | WF-003 | WF-002 |
| 004 | Consolidação dos contratos | [prompt-task-001-etapa-004-consolidacao-documental.md](prompt-task-001-etapa-004-consolidacao-documental.md) | WF-004 | WF-003 |
| 005 | Revisão documental e preparação da validação | [prompt-task-001-etapa-005-revisao.md](prompt-task-001-etapa-005-revisao.md) | WF-005 | WF-004 |
| 006 | Testes manuais documentais | [prompt-task-001-etapa-006-testes-manuais.md](prompt-task-001-etapa-006-testes-manuais.md) | WF-006 | WF-005 |
| 007 | Validação final e conclusão | [prompt-task-001-etapa-007-conclusao.md](prompt-task-001-etapa-007-conclusao.md) | WF-007 | WF-006 |

Executar um prompt por vez; habilitar não significa iniciar. Falha exige diagnóstico, correção autorizada e revalidação. WF distingue workflow dos oito gates de qualidade de AGENTS.

## Decisões e bloqueios

ADR-011 resolveu sessões, título, numeração, identidade/e-mail, destinatários e fim exclusivo. ADR-012 já define MFA e TI/configuração na recuperação. Não repetir perguntas respondidas. Faltam correção entre anos, scanner/indisponibilidade, detalhamento MFA/tarefa própria, PD-011 e contratos técnicos. Relato histórico sem Git não reflete inspeção desta geração; revalidar checkout/sincronização na etapa 001.

## Escopo e conclusão

docs/architecture/**, docs/adr/**, TASKS.md, README apenas decisões aprovadas e validation obrigatório. NO_INCIDENTAL_CHANGES. Sem software/tarefas futuras. Roteiro e auxiliares documentais, se necessários, em docs/architecture.

Concluir exige contratos completos, decisões rastreáveis, referências/compatibilidade revisadas, sete gates WF e oito gates de qualidade aplicáveis, oito casos manuais aprovados, resumo persistido/verificado, commits rastreáveis e ausência de expansão de escopo. TASK-002 é candidata após TASK-001 DONE e sua própria DoR; não iniciar automaticamente.

## Testes manuais previstos

T001 escopo; T002 PD-010; T003 MFA; T004 arquivos/scanner; T005 versões/licenças; T006 integridade/concorrência; T007 tempo/notificações; T008 rastreabilidade/regressão documental. Windows → WSL → Linux. Etapa 006 contém comandos, procedimentos e esperados para gerar roteiro completo em docs/architecture. Não são testes funcionais da aplicação.

## Estado inicial

GATES TOTAIS: 7; CONCLUÍDOS: 0; PENDENTES: 7; BLOQUEADOS: 0 (workflow não executado). TASK: BLOCKED. Testes previstos: 8; executados/aprovados/reprovados/bloqueados: 0; pendentes: 8.
