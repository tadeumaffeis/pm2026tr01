# TASK-001 — ETAPA 007 — Validação final e conclusão

## 1. OBJETIVO

Executar exclusivamente a etapa de validação final e conclusão, conforme procedimento e critérios abaixo, produzindo evidências sem antecipar etapas.

## 2. CONTEXTO

TASK-001 — Fechar contratos e decisões técnicas de implementação; PHASE-01; CRITICAL; DEPENDS_ON: NONE. Estado observado em 05/10/2026: BLOCKED. É documental: consolidar contratos não significa implementar software. RNF-001/002/003/014 e ADR-001/002/003 são relações diretas; ADR-010/011/012 complementam decisões. RF/RN/UC constam N/A na ficha técnica, mas contratos afetados devem preservar rastreabilidade às regras concretas do README.

Decisões vigentes: sessões sem duração máxima/inatividade, com logout/revogação; título 100–200; número institucional anual imutável pelo ano da reunião; correção de e-mail somente da mesma identidade, sem fusão; distribuição de avisos por papel/vínculo; fim exclusivo. PD-006 já escolheu MFA por e-mail e TI/configuração para recuperação; PD-007 já fixou 26.214.400 bytes e ata + 10 anexos. Pendências: correção de data entre anos, scanner/indisponibilidade, detalhamento MFA/tarefa própria, PD-011 e contratos técnicos. Revalidar este retrato contra fontes posteriores.

## 3. PRÉ-CONDIÇÕES

WF-006 APROVADO com relatório/evidências; todos os predecessores continuam válidos.
Leia AGENTS.md, README.md, TASKS.md, ADRs relacionados, código e testes existentes nessa ordem. Não presumir ausência de software sem inventário. Etapas 001–002 são preparação da resolução, não início formal em IN_PROGRESS; etapas posteriores exigem decisões, DoR e autorização correspondentes. Evidência obrigatória ausente bloqueia avanço.

## 4. ENTRADAS NECESSÁRIAS

AGENTS.md; README.md (arquitetura, pendências e consolidação PD-010); TASKS.md (regras/gates/ficha TASK-001); docs/adr/ADR-001-typescript.md, ADR-002-monolito-modular.md, ADR-003-mysql-transacoes.md, ADR-010-revisao-2026-10-01.md, ADR-011-consolidacao-pd-010.md, ADR-012-mfa-interno.md; demais ADRs relacionados; contratos docs/architecture; relatórios validation relativos à TASK-001 e PDs. Receber decisões posteriores e evidências de gates predecessores quando aplicável. Relato histórico não é aprovação atual.

## 5. ARQUIVOS E COMPONENTES ENVOLVIDOS

Contratos system.md, data-model.md, api.md, security.md, operations.md, test-plan.md, references.md e pd-007-verificacao-arquivos.md em docs/architecture; ADRs; README; TASKS; validation. Impactos documentais sobre persistência, interface/API, segurança e notificações futuras; nenhum componente implementado nesta TASK. Modificar somente o subconjunto exigido pelo procedimento.

## 6. PROCEDIMENTO DETALHADO

1. Releia AGENTS e ficha; confira seis gates anteriores e artefatos. Se documentos mudaram após revisão/testes, repita os casos afetados.
2. Execute git status --short, git diff --check, git diff, git diff --cached e inventário de novos arquivos; classifique todo arquivo/hunk próprio PRIMARY e Incidental Changes NONE. Preserve mudanças alheias.
3. Confirme contratos completos, justificativas técnicas, decisões de negócio explícitas, referências/compatibilidade revisadas, PDs necessárias resolvidas e pendências exclusivas de produção rastreadas. Revisão documental não comprova implementação.
4. Preencha os oito gates de qualidade de AGENTS com evidências reais e N/A justificados de software. Segurança/regressão documentais precisam de revisão. WF não substitui esses gates.
5. Grave/releia validation/TASK-001_YYYY-MM-DD_HH-mm-ss.md com relatório completo e referencie em TASKS. Preserve anteriores, usando sufixo se colidir.
6. Prepare commit rastreável apenas dos próprios artefatos: docs(contratos): fecha contratos de implementação [TASK-001]. Stage por arquivos/hunks revisados; não git add . com alterações alheias. Sem commit ou com gate obrigatório pendente, não declarar DoD completa. Não push/merge/implantar.
7. Só promover IN_REVIEW → DONE no índice/ficha após todas as condições, incluindo resumo verificado e rastreabilidade. Registre hash do commit dos artefatos no fechamento; registro final pode ter commit próprio sem referência circular ao próprio hash.
8. Apresente matriz WF-001 a WF-007, oito gates de qualidade, contagens reais, testes manuais 8/8, DoD e próxima elegível. TASK-002 é candidata: verificar sua DoR após dependência DONE; senão NONE com motivo. PARAR sem iniciar TASK-002.

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

- [ ] Gates de workflow e qualidade satisfeitos
- [ ] Testes manuais válidos sobre documentos atuais
- [ ] Relatório persistido/verificado e commits rastreáveis
- [ ] Índice/ficha consistentes; próxima elegível avaliada sem execução

Todos obrigatórios, com evidência por item. Pendência/falha bloqueia próximo passo. Diagnóstico aprovado não resolve DoR da TASK.

## 12. GATE DA ETAPA

Gate WF-007: marcar itens da seção 11 OK/FALTA/FALHOU, informar critérios concluídos/total e pendentes/total. Inicialmente NÃO EXECUTADO. Resultado APROVADO/REPROVADO/BLOQUEADO por evidências. Próxima etapa HABILITADA somente com todos os critérios/predecessores satisfeitos; nunca iniciá-la automaticamente.

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

Gravar novo validation/TASK-001_YYYY-MM-DD_HH-mm-ss.md com fuso, status real da TASK, WF-007, objetivo, PRIMARY, Incidental Changes NONE, decisões, comandos/ambiente/resultados, oito gates de qualidade, Scope Validation, DoD, branch/commits ou ausência, pendências e próxima elegível. Incluir todos os campos do TASK Execution Report de AGENTS.md; referenciar em TASKS.md e conferir existência/conteúdo. Preservar relatórios; sufixo sequencial em colisão. Não marcar DONE por concluir etapa intermediária. AGUARDANDO TESTES MANUAIS é situação do relatório, não novo enum em TASKS.

Finalizar resposta com caminho do resumo e bloco preenchido:

```text
==================================================
TASK: TASK-001
ETAPA: 007
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
PRÓXIMA ETAPA: Nenhuma etapa seguinte; avaliar TASK-002 ou NONE e PARAR.
PRÓXIMA ETAPA HABILITADA: SIM | NÃO
MOTIVO: ...
==================================================
```

Parar após o relatório da etapa. Na conclusão, não executar a próxima TASK.
