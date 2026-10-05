# TASK-001 — ETAPA 002 — Resolução de pendências e pesquisa técnica

## 1. OBJETIVO

Executar exclusivamente a etapa de resolução de pendências e pesquisa técnica, conforme procedimento e critérios abaixo, produzindo evidências sem antecipar etapas.

## 2. CONTEXTO

TASK-001 — Fechar contratos e decisões técnicas de implementação; PHASE-01; CRITICAL; DEPENDS_ON: NONE. Estado observado em 05/10/2026: BLOCKED. É documental: consolidar contratos não significa implementar software. RNF-001/002/003/014 e ADR-001/002/003 são relações diretas; ADR-010/011/012 complementam decisões. RF/RN/UC constam N/A na ficha técnica, mas contratos afetados devem preservar rastreabilidade às regras concretas do README.

Decisões vigentes: sessões sem duração máxima/inatividade, com logout/revogação; título 100–200; número institucional anual imutável pelo ano da reunião; correção de e-mail somente da mesma identidade, sem fusão; distribuição de avisos por papel/vínculo; fim exclusivo. PD-006 já escolheu MFA por e-mail e TI/configuração para recuperação; PD-007 já fixou 26.214.400 bytes e ata + 10 anexos. Pendências: correção de data entre anos, scanner/indisponibilidade, detalhamento MFA/tarefa própria, PD-011 e contratos técnicos. Revalidar este retrato contra fontes posteriores.

## 3. PRÉ-CONDIÇÕES

WF-001 APROVADO com relatório/evidências; todos os predecessores continuam válidos.
Leia AGENTS.md, README.md, TASKS.md, ADRs relacionados, código e testes existentes nessa ordem. Não presumir ausência de software sem inventário. Etapas 001–002 são preparação da resolução, não início formal em IN_PROGRESS; etapas posteriores exigem decisões, DoR e autorização correspondentes. Evidência obrigatória ausente bloqueia avanço.

## 4. ENTRADAS NECESSÁRIAS

AGENTS.md; README.md (arquitetura, pendências e consolidação PD-010); TASKS.md (regras/gates/ficha TASK-001); docs/adr/ADR-001-typescript.md, ADR-002-monolito-modular.md, ADR-003-mysql-transacoes.md, ADR-010-revisao-2026-10-01.md, ADR-011-consolidacao-pd-010.md, ADR-012-mfa-interno.md; demais ADRs relacionados; contratos docs/architecture; relatórios validation relativos à TASK-001 e PDs. Receber decisões posteriores e evidências de gates predecessores quando aplicável. Relato histórico não é aprovação atual.

## 5. ARQUIVOS E COMPONENTES ENVOLVIDOS

Contratos system.md, data-model.md, api.md, security.md, operations.md, test-plan.md, references.md e pd-007-verificacao-arquivos.md em docs/architecture; ADRs; README; TASKS; validation. Impactos documentais sobre persistência, interface/API, segurança e notificações futuras; nenhum componente implementado nesta TASK. Modificar somente o subconjunto exigido pelo procedimento.

## 6. PROCEDIMENTO DETALHADO

1. Use a matriz da etapa 001. Prepare resolução documental sem READY → IN_PROGRESS enquanto DoR incompleta. A seção Gates de pendências de TASKS.md trata TASK-001 como atividade de resolução; não dispensa decisões nem autoriza software.
2. PD-010: apresente decisão sobre correção de data para outro ano diante de número anual imutável: preservar número original, impedir correção entre anos ou outra regra explícita. Explique impactos e recomendação; aguarde resposta para trabalho dependente. Preserve as seis decisões de ADR-011.
3. PD-007: releia docs/architecture/pd-007-verificacao-arquivos.md. Prepare decisão concreta sobre ClamAV local ou alternativa e indisponibilidade. Detalhe quarentena, estados, timeout, retentativas, limites de inspeção/extração e assinaturas desatualizadas. ClamAV permanece PROPOSTA até aprovação. Não instalar scanner. Não alterar 26.214.400 bytes por arquivo nem uma ata + 10 anexos; 275 MiB não é quota de histórico.
4. PD-006: detalhe proposta de verificação de identidade registrada pela TI, parâmetros de configuração de recuperação, autorização, aplicação controlada, proteção contra repetição, auditoria, revogação e novo login com senha + MFA. Nunca desligar MFA. 10min/5 erros/60s, perfis e responsável já aprovados. Submeta lacunas de negócio/segurança relevantes, sem inventar procedimento institucional de identificação.
5. PD-011: pesquise em fontes oficiais atuais TypeScript, React, Material UI, NestJS, MySQL/InnoDB, Node.js, driver/acesso SQL, migrações, PDF, testes e complementos necessários. Registre URL, data, versão exata estável, suporte, requisitos de runtime/peers, licença, alternativas e compatibilidade documental. Valide a referência MySQL existente, sem tratá-la como versão escolhida. Não instalar pacotes nem gerar package.json/lockfile.
6. Documente versões/digests verificáveis de imagens aplicáveis e política de atualização/revalidação no início da implementação. Não usar latest nem alegar build executado. Dado não confirmado permanece pendente. Prova prática pertence às tarefas futuras.
7. Produza matriz decisão → autorização/fonte → impacto → arquivo → pendência. Propostas em docs/architecture/ADRs com status correto; README somente decisões explicitamente aprovadas. Decisão arquitetural significativa exige ADR individual.
8. Após fechar escopo, planeje tarefa própria de MFA e dependências em TASKS.md. Confira maior ID; nunca reutilize/renumere. Não implemente. Expansão funcional ou mudança não autorizada de segurança exige SCOPE ESCALATION.
9. Registre respostas nas fontes afetadas. Só promova BLOCKED → READY após DoR completa e evidências; READY não autoriza execução. Se faltar resposta, mantenha BLOCKED e este gate bloqueado. Não transformar silêncio em aprovação.

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

- [ ] PD-010 complementar decidida explicitamente
- [ ] PD-007 decidida no necessário aos contratos
- [ ] PD-006 detalhada e tarefa própria delimitada
- [ ] PD-011 pesquisada com fontes e versões verificáveis
- [ ] DoR completa e decisões rastreáveis

Todos obrigatórios, com evidência por item. Pendência/falha bloqueia próximo passo. Diagnóstico aprovado não resolve DoR da TASK.

## 12. GATE DA ETAPA

Gate WF-002: marcar itens da seção 11 OK/FALTA/FALHOU, informar critérios concluídos/total e pendentes/total. Inicialmente NÃO EXECUTADO. Resultado APROVADO/REPROVADO/BLOQUEADO por evidências. Próxima etapa HABILITADA somente com todos os critérios/predecessores satisfeitos; nunca iniciá-la automaticamente.

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

Gravar novo validation/TASK-001_YYYY-MM-DD_HH-mm-ss.md com fuso, status real da TASK, WF-002, objetivo, PRIMARY, Incidental Changes NONE, decisões, comandos/ambiente/resultados, oito gates de qualidade, Scope Validation, DoD, branch/commits ou ausência, pendências e próxima elegível. Incluir todos os campos do TASK Execution Report de AGENTS.md; referenciar em TASKS.md e conferir existência/conteúdo. Preservar relatórios; sufixo sequencial em colisão. Não marcar DONE por concluir etapa intermediária. AGUARDANDO TESTES MANUAIS é situação do relatório, não novo enum em TASKS.

Finalizar resposta com caminho do resumo e bloco preenchido:

```text
==================================================
TASK: TASK-001
ETAPA: 002
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
PRÓXIMA ETAPA: prompt-task-001-etapa-003-planejamento.md
PRÓXIMA ETAPA HABILITADA: SIM | NÃO
MOTIVO: ...
==================================================
```

Parar após o relatório da etapa. Na conclusão, não executar a próxima TASK.
