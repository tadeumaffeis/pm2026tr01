# Backlog executável e estado operacional

Versão inicial: planejamento aprovado; implementação não iniciada. TASK-001 recebeu atualização documental parcial em 01/10/2026 e está BLOCKED pelos esclarecimentos PD-006/010 e complementos PD-007/011; nenhuma tarefa está pronta para implementação. Nenhuma implementação está autorizada pela aprovação do planejamento.

## Índice de execução

| Ordem | TASK | Fase | Prioridade | Dependências | Estado |
|---:|---|---|---|---|---|
| 1 | TASK-001 — Fechar contratos e decisões técnicas de implementação | PHASE-01 | CRITICAL | NONE | BLOCKED |
| 2 | TASK-002 — Preparar estrutura e ferramentas | PHASE-01 | HIGH | TASK-001 | BLOCKED |
| 3 | TASK-003 — Criar fundação de persistência e auditoria | PHASE-01 | CRITICAL | TASK-002 | BLOCKED |
| 4 | TASK-004 — Preparar contratos de armazenamento e trabalhos assíncronos | PHASE-01 | HIGH | TASK-003 | BLOCKED |
| 5 | TASK-005 — Checkpoint PHASE-01 | PHASE-01 | HIGH | TASK-002, TASK-003, TASK-004 | BLOCKED |
| 6 | TASK-006 — Implementar contas internas e ativação | PHASE-02 | HIGH | TASK-005 | BLOCKED |
| 7 | TASK-007 — Implementar identidade e sessão de apreciadores | PHASE-02 | HIGH | TASK-005 | BLOCKED |
| 8 | TASK-008 — Integrar autorização e fronteiras de sessão | PHASE-02 | CRITICAL | TASK-006, TASK-007 | BLOCKED |
| 9 | TASK-009 — Implementar cadastros e parâmetros administrativos | PHASE-02 | HIGH | TASK-008 | BLOCKED |
| 10 | TASK-010 — Checkpoint PHASE-02 | PHASE-02 | HIGH | TASK-006, TASK-007, TASK-008, TASK-009 | BLOCKED |
| 11 | TASK-011 — Implementar documentos privados e validação | PHASE-03 | HIGH | TASK-010 | BLOCKED |
| 12 | TASK-012 — Implementar rascunhos e preparação | PHASE-03 | HIGH | TASK-011 | BLOCKED |
| 13 | TASK-013 — Implementar publicação transacional | PHASE-03 | CRITICAL | TASK-012 | BLOCKED |
| 14 | TASK-014 — Implementar convites e composição dos participantes | PHASE-03 | HIGH | TASK-013 | BLOCKED |
| 15 | TASK-015 — Checkpoint PHASE-03 | PHASE-03 | HIGH | TASK-011, TASK-012, TASK-013, TASK-014 | BLOCKED |
| 16 | TASK-016 — Implementar manifestações e encerramentos | PHASE-04 | CRITICAL | TASK-015 | BLOCKED |
| 17 | TASK-017 — Implementar prazos, suspensão e composições documentais | PHASE-04 | HIGH | TASK-016 | BLOCKED |
| 18 | TASK-018 — Implementar notificações e Microsoft Graph | PHASE-04 | HIGH | TASK-017 | BLOCKED |
| 19 | TASK-019 — Implementar consulta, visibilidade e auditoria | PHASE-04 | HIGH | TASK-017 | BLOCKED |
| 20 | TASK-020 — Checkpoint PHASE-04 | PHASE-04 | HIGH | TASK-016, TASK-017, TASK-018, TASK-019 | BLOCKED |
| 21 | TASK-021 — Implementar relatórios CSV e PDF | PHASE-05 | HIGH | TASK-020 | BLOCKED |
| 22 | TASK-022 — Implementar arquivamento, recuperação e remoção | PHASE-05 | CRITICAL | TASK-021 | BLOCKED |
| 23 | TASK-023 — Validar segurança, acessibilidade e compatibilidade | PHASE-05 | HIGH | TASK-022 | BLOCKED |
| 24 | TASK-024 — Checkpoint PHASE-05 | PHASE-05 | HIGH | TASK-021, TASK-022, TASK-023 | BLOCKED |
| 25 | TASK-025 — Preparar implantação institucional | PHASE-06 | HIGH | TASK-024 | BLOCKED |
| 26 | TASK-026 — Validar capacidade e critérios operacionais | PHASE-06 | HIGH | TASK-025 | BLOCKED |
| 27 | TASK-027 — Ensaiar backup, restauração e retenção | PHASE-06 | HIGH | TASK-025 | BLOCKED |
| 28 | TASK-028 — Checkpoint PHASE-06 e liberação | PHASE-06 | CRITICAL | TASK-026, TASK-027 | BLOCKED |

## Regras operacionais

Estados: BLOCKED, READY, IN_PROGRESS, IN_REVIEW, DONE, FAILED, CANCELLED. Seguir AGENTS.md. Índice e ficha devem refletir o mesmo estado. Dependências transitivas também se aplicam. Ordem é topológica; primeira elegível tem precedência. Cada fase seguinte depende do checkpoint anterior.

DoR: requisitos, contratos, critérios, testes e Scope Guard completos; dependências DONE com artefatos e testes comprovados; decisões necessárias resolvidas; sem pendência bloqueante. Uma dependência DONE não promove automaticamente a tarefa se outras condições falharem.

DoD: critérios da ficha e gates aplicáveis aprovados; sem regressão conhecida; diffs classificados PRIMARY/INCIDENTAL; nenhuma mudança proibida; commits rastreáveis; relatório registrado. Nenhum resultado abaixo foi executado.

## Gates de pendências

- TASK-001: atividade própria de resolução, não pressupõe PD resolvidas; só conclui quando contratos necessários ao desenvolvimento estão fechados. Questões de negócio exigem resposta, não escolha unilateral.
- TASK-011: unidade exata de limite e contrato de validação (PD-007); adaptador de verificação definido.
- TASK-017/018: fuso de teste definido; produção usa America/Sao_Paulo (PD-009 resolvida como decisão); fronteiras de calendário aprovadas em TASK-001.
- TASK-018: validação real depende de PD-005. Testes simulados não comprovam configuração institucional.
- TASK-023/024: matriz PD-008 fechada; testes de homologação correspondentes.
- TASK-025: PD-001/005/006/007 resolvidas. Método MFA por e-mail escolhido; detalhar PD-006 e criar tarefa própria/dependência antes da implementação e liberação.
- TASK-026: PD-002/009 resolvidas. TASK-027: PD-003/004 resolvidas. TASK-028: todas as pendências de produção fechadas.

## Fichas

### TASK-001 — Fechar contratos e decisões técnicas de implementação

#### Status
BLOCKED

#### Phase
PHASE-01

#### Priority
CRITICAL

#### Objetivo
Resolver PD-010/011 e partes de PD-007 que afetam contratos; detalhar propostas sem inventar negócio.

#### Dependências
DEPENDS_ON: NONE

Bloqueio atual: decisões parcialmente incorporadas; esclarecer PD-010 (sessões, título, correção de e-mail, numeração, destinatários) e fechar contratos técnicos PD-007/011. PD-006 exige detalhamento antes da implementação dependente.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Resolver PD-010/011 e partes de PD-007 que afetam contratos; detalhar propostas sem inventar negócio. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- docs/architecture/**
- docs/adr/**
- TASKS.md
- README.md somente para decisões explicitamente aprovadas

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
NO_INCIDENTAL_CHANGES

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Implementar software; alterar requisitos ou regras de negócio sem decisão explícita; tratar proposta pendente como aprovada.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Contratos completos, decisões técnicas justificadas; pendências de negócio resolvidas pelo usuário antes de alterações dependentes; revisão de referências e compatibilidade.

#### Testes necessários
Revisão documental de contratos, rastreabilidade e decisões; build/lint de software N/A com justificativa.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates de software N/A nesta tarefa documental; integridade documental obrigatória.

#### Registro de execução
Atualização documental parcial em 01/10/2026 autorizada pelo usuário. Decisões incorporadas ao README, contratos e ADR-010; conclusão bloqueada pelos complementos descritos. Sem software implementado, sem commits e sem testes de software. Incidental Changes: NONE. Ver docs/verification/revision-2026-10-01.md.

Tentativa de execução do prompt em 2026-10-01 14:42:09 -03:00: BLOCKED na verificação de elegibilidade; pendências PD-006/007/010/011 mantidas e Git não reconhecido neste diretório. Branch não criada; commits e testes de software: nenhum. Alterações PRIMARY: este registro e o relatório; Incidental Changes: NONE. DoD: FAIL. Próxima elegível: NONE. Resumo: [validation/TASK-001_2026-10-01_14-42-09.md](validation/TASK-001_2026-10-01_14-42-09.md).

Consolidação posterior PD-010: seis decisões explícitas registradas em docs/adr/ADR-011-consolidacao-pd-010.md; pendente correção da data para outro ano diante da numeração imutável. Mantido BLOCKED pelos complementos e demais PDs. Registro documental de respostas, sem implementação, branch ou commits. Resumo: [validation/avulsa-decisoes-pd-010_2026-10-01_14-48-33.md](validation/avulsa-decisoes-pd-010_2026-10-01_14-48-33.md).

Consolidação PD-006: política geral aprovada em ADR-012; falta responsável/verificação de identidade na recuperação do único Administrador e planejamento da tarefa própria. TASK-001 permanece BLOCKED. Resumo: [validation/avulsa-decisoes-pd-006_2026-10-01_14-50-48.md](validation/avulsa-decisoes-pd-006_2026-10-01_14-50-48.md).

Análise PD-007: 25 MiB e até 11 arquivos por versão aprovados; proposta de verificação em docs/architecture/pd-007-verificacao-arquivos.md aguarda decisão. TASK-001 permanece BLOCKED. Resumo: [validation/avulsa-proposta-pd-007_2026-10-01_14-56-26.md](validation/avulsa-proposta-pd-007_2026-10-01_14-56-26.md).

Complemento PD-006: equipe de TI verifica/autoriza recuperação do único Administrador por arquivos de configuração; responsável e meio operacional definidos, detalhamento técnico pendente em ADR-012. Nenhum software alterado; TASK-001 permanece BLOCKED. Resumo: [validation/avulsa-responsavel-pd-006_2026-10-01_15-02-18.md](validation/avulsa-responsavel-pd-006_2026-10-01_15-02-18.md).

Execução da Etapa 001 do workflow gerado em 2026-10-05: diagnóstico de recontextualização concluído (WF-001, 4/4 critérios documentados), sem alteração de contratos ou software. TASK-001 permanece BLOCKED por DoR incompleta e pendências PD-006/007/010/011. Branch: chore/avulsa-prompt-task-000-inicio; commits: nenhum. Incidental Changes: NONE. Resumo: [validation/TASK-001_2026-10-05_14-18-00.md](validation/TASK-001_2026-10-05_14-18-00.md).

Execução da Etapa 002 em 2026-10-05: propostas documentais para PD-010/PD-007/PD-006 e pesquisa oficial preliminar de PD-011 registradas em [docs/architecture/task-001-etapa-002-pesquisa.md](docs/architecture/task-001-etapa-002-pesquisa.md). WF-002 BLOCKED (1/5 critérios plenamente concluído; 1 parcial; 4 pendentes). Nenhum pacote, scanner, banco ou software executado; Incidental Changes: NONE. Resumo: [validation/TASK-001_2026-10-05_14-32-00.md](validation/TASK-001_2026-10-05_14-32-00.md).

Decisão posterior do usuário para PD-010: aplicar a alternativa 1. Se a correção da data mudar o ano, preservar o número original, mesmo com divergência visível entre o ano do número e a data corrigida; não renumerar nem reutilizar e auditar a correção. A pendência 1 do WF-002 está resolvida; PD-006/007/011, contratos técnicos e DoR permanecem pendentes. Artefatos atualizados: ADR-011, README e contratos de arquitetura. Incidental Changes: NONE.

### TASK-002 — Preparar estrutura e ferramentas

#### Status
BLOCKED

#### Phase
PHASE-01

#### Priority
HIGH

#### Objetivo
Preparar workspace React/Material UI/TypeScript/NestJS e ferramentas aprovadas.

#### Dependências
DEPENDS_ON: TASK-001

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Preparar workspace React/Material UI/TypeScript/NestJS e ferramentas aprovadas. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- package.json
- arquivos de lock e configuração
- src/*/bootstrap/**
- tests/support/**
- .github/workflows/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Build, tipos, lint e teste básico executam; nenhum comportamento de negócio antecipado; instalação reproduzível.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-003 — Criar fundação de persistência e auditoria

#### Status
BLOCKED

#### Phase
PHASE-01

#### Priority
CRITICAL

#### Objetivo
Estabelecer transações, migrações, armazenamento de eventos e mecanismo de concorrência.

#### Dependências
DEPENDS_ON: TASK-002

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Estabelecer transações, migrações, armazenamento de eventos e mecanismo de concorrência. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/infrastructure/database/**
- src/infrastructure/audit/**
- database/**
- tests/integration/foundation/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Migrações em banco real; rollback comprovado; unicidade concorrente e evento transacional; não implementar casos de uso futuros.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-004 — Preparar contratos de armazenamento e trabalhos assíncronos

#### Status
BLOCKED

#### Phase
PHASE-01

#### Priority
HIGH

#### Objetivo
Implementar portas técnicas, fila transacional e adaptadores de teste, sem envio real.

#### Dependências
DEPENDS_ON: TASK-003

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Implementar portas técnicas, fila transacional e adaptadores de teste, sem envio real. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/infrastructure/storage/**
- src/infrastructure/jobs/**
- tests/integration/infrastructure/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Reinício não perde trabalho; acesso privado; falhas simuladas e retentativas técnicas; sem credenciais reais.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-005 — Checkpoint PHASE-01

#### Status
BLOCKED

#### Phase
PHASE-01

#### Priority
HIGH

#### Objetivo
Validar fundação antes dos módulos de identidade.

#### Dependências
DEPENDS_ON: TASK-002, TASK-003, TASK-004

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Validar fundação antes dos módulos de identidade. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- TASKS.md
- docs/verification/PHASE-01.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
NO_INCIDENTAL_CHANGES

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar implementação para esconder falhas; modificar requisitos/contratos; qualquer código de produção.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Build/tipos/lint, testes de fundação, arquitetura, segurança, documentação e rastreabilidade aprovados.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-006 — Implementar contas internas e ativação

#### Status
BLOCKED

#### Phase
PHASE-02

#### Priority
HIGH

#### Objetivo
Entregar contas, papéis, ativação, recuperação e proteção do último Administrador.

#### Dependências
DEPENDS_ON: TASK-005

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-001. RN: RN-002, RN-021. RNF: RNF-001, RNF-004, RNF-005. UC: UC-001. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar contas, papéis, ativação, recuperação e proteção do último Administrador. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/internal-auth/**
- src/web/internal-auth/**
- database/migrations/*internal_auth*
- tests/**/internal-auth/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Ativação única; reset revoga sessões; último Admin protegido sob concorrência; autorização por papel; testes negativos.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-001. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-007 — Implementar identidade e sessão de apreciadores

#### Status
BLOCKED

#### Phase
PHASE-02

#### Priority
HIGH

#### Objetivo
Entregar senha temporária, sessão global e recuperação de links.

#### Dependências
DEPENDS_ON: TASK-005

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-004. RN: RN-001, RN-019, RN-020. RNF: RNF-001, RNF-004, RNF-005. UC: UC-004. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar senha temporária, sessão global e recuperação de links. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/appraiser-auth/**
- src/web/appraiser-auth/**
- database/migrations/*appraiser_auth*
- tests/**/appraiser-auth/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Expiração/5 tentativas/60s; contrato de duração/inatividade de sessão condicionado ao esclarecimento de PD-010; proteção de identidade; recuperação sem enumeração; vínculo individual revogado sem logout global.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-004. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-008 — Integrar autorização e fronteiras de sessão

#### Status
BLOCKED

#### Phase
PHASE-02

#### Priority
CRITICAL

#### Objetivo
Aplicar política comum sem confundir contas internas e identidades de apreciadores.

#### Dependências
DEPENDS_ON: TASK-006, TASK-007

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Aplicar política comum sem confundir contas internas e identidades de apreciadores. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/security/**
- src/modules/internal-auth/authorization/**
- src/modules/appraiser-auth/authorization/**
- tests/**/authorization/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Matriz de acesso cruzado; conta interna desativada não implica decisão silenciosa sobre participação externa; contratos aprovados em TASK-001.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-009 — Implementar cadastros e parâmetros administrativos

#### Status
BLOCKED

#### Phase
PHASE-02

#### Priority
HIGH

#### Objetivo
Entregar unidades, reuniões, vínculos de Organizadores e limites administrativos.

#### Dependências
DEPENDS_ON: TASK-008

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-002, RF-017. RN: RN-002, RN-017, RN-020, RN-021, RN-022, RN-023. RNF: RNF-001, RNF-003, RNF-004, RNF-010, RNF-011. UC: UC-002, UC-017. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar unidades, reuniões, vínculos de Organizadores e limites administrativos. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/registry/**
- src/web/registry/**
- database/migrations/*registry*
- tests/**/registry/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Cadastro só por Admin; campos e número; unidade inativa; correção justificada; limite não retroativo; exceção no teto.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-002, TEST-017. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-010 — Checkpoint PHASE-02

#### Status
BLOCKED

#### Phase
PHASE-02

#### Priority
HIGH

#### Objetivo
Validar identidade, autorização e cadastros.

#### Dependências
DEPENDS_ON: TASK-006, TASK-007, TASK-008, TASK-009

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-001, ADR-002, ADR-003.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Validar identidade, autorização e cadastros. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- TASKS.md
- docs/verification/PHASE-02.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
NO_INCIDENTAL_CHANGES

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar implementação para esconder falhas; modificar requisitos/contratos; qualquer código de produção.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Testes de segurança e fluxo interno/apreciador; revisão de permissões e auditoria; gates aplicáveis aprovados.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-011 — Implementar documentos privados e validação

#### Status
BLOCKED

#### Phase
PHASE-03

#### Priority
HIGH

#### Objetivo
Entregar upload privado, validação e visualização da ata.

#### Dependências
DEPENDS_ON: TASK-010

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-006. RN: RN-015, RN-017, RN-025. RNF: RNF-003, RNF-006. UC: UC-006. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar upload privado, validação e visualização da ata. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/documents/**
- src/web/documents/**
- database/migrations/*documents*
- tests/**/documents/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Formatos reais, PDF protegido, macros, limite e arquivo malicioso; download autorizado; visualização móvel; PD-007 resolvida no necessário.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-006. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-012 — Implementar rascunhos e preparação

#### Status
BLOCKED

#### Phase
PHASE-03

#### Priority
HIGH

#### Objetivo
Entregar única próxima versão e descarte seguro de arquivos exclusivos.

#### Dependências
DEPENDS_ON: TASK-011

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-005. RN: RN-003, RN-004, RN-014, RN-025. RNF: RNF-001, RNF-003. UC: UC-005. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar única próxima versão e descarte seguro de arquivos exclusivos. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/drafts/**
- src/web/drafts/**
- database/migrations/*drafts*
- tests/**/drafts/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Rascunho único concorrente; seleção explícita de anexos; descarte não elimina arquivo referenciado; sem publicação automática.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-005. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-013 — Implementar publicação transacional

#### Status
BLOCKED

#### Phase
PHASE-03

#### Priority
CRITICAL

#### Objetivo
Entregar abertura e substituição de ciclos com convites por ciclo.

#### Dependências
DEPENDS_ON: TASK-012

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-007. RN: RN-003, RN-004, RN-005, RN-009, RN-014, RN-016. RNF: RNF-002, RNF-003, RNF-009, RNF-010. UC: UC-007. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar abertura e substituição de ciclos com convites por ciclo. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/publication/**
- src/web/publication/**
- database/migrations/*publication*
- tests/**/publication/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Falha reverte conjunto; dois publicadores não criam dois ciclos correntes; prazos/ata/convidado obrigatórios; intenção de envio durável.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-007. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-014 — Implementar convites e composição dos participantes

#### Status
BLOCKED

#### Phase
PHASE-03

#### Priority
HIGH

#### Objetivo
Entregar aceite, recusa, remoção e sincronização com rascunho.

#### Dependências
DEPENDS_ON: TASK-013

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-003, RF-008. RN: RN-001, RN-005, RN-006, RN-007, RN-008, RN-019, RN-020. RNF: RNF-001, RNF-002, RNF-003, RNF-004, RNF-010. UC: UC-003, UC-008. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar aceite, recusa, remoção e sincronização com rascunho. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/participation/**
- src/web/participation/**
- database/migrations/*participation*
- tests/**/participation/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Recusa definitiva por identidade/ciclo; aceite autenticado; não contornar por reinclusão; exclusões futuras preservadas; prazo validado no servidor.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-003, TEST-008. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-015 — Checkpoint PHASE-03

#### Status
BLOCKED

#### Phase
PHASE-03

#### Priority
HIGH

#### Objetivo
Validar preparação/publicação e participação.

#### Dependências
DEPENDS_ON: TASK-011, TASK-012, TASK-013, TASK-014

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Validar preparação/publicação e participação. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- TASKS.md
- docs/verification/PHASE-03.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
NO_INCIDENTAL_CHANGES

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar implementação para esconder falhas; modificar requisitos/contratos; qualquer código de produção.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
E2E publicação/convite; concorrência e arquivos privados; auditoria, rastreabilidade e escopo aprovados.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-016 — Implementar manifestações e encerramentos

#### Status
BLOCKED

#### Phase
PHASE-04

#### Priority
CRITICAL

#### Objetivo
Entregar decisões versionadas, unanimidade e encerramento transacional.

#### Dependências
DEPENDS_ON: TASK-015

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-009, RF-012. RN: RN-003, RN-012, RN-013, RN-014, RN-016, RN-019, RN-025. RNF: RNF-001, RNF-002, RNF-003, RNF-010. UC: UC-009, UC-012. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar decisões versionadas, unanimidade e encerramento transacional. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/decisions/**
- src/modules/closure/**
- src/web/decisions/**
- src/web/closure/**
- database/migrations/*decisions*
- database/migrations/*closure*
- tests/**/decisions/**
- tests/**/closure/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Quatro decisões; texto; base documental; disputa manifestação/encerramento; zero participantes; convites abertos; sucesso suspenso rejeitado.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-009, TEST-012. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-017 — Implementar prazos, suspensão e composições documentais

#### Status
BLOCKED

#### Phase
PHASE-04

#### Priority
HIGH

#### Objetivo
Entregar relógio de domínio, congelamento, reativação e alterações autorizadas de anexos.

#### Dependências
DEPENDS_ON: TASK-016

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-010, RF-011. RN: RN-007, RN-009, RN-010, RN-011, RN-015, RN-016. RNF: RNF-002, RNF-003, RNF-006, RNF-009, RNF-010. UC: UC-010, UC-011. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar relógio de domínio, congelamento, reativação e alterações autorizadas de anexos. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/lifecycle/**
- src/modules/attachments/**
- src/web/lifecycle/**
- src/web/attachments/**
- database/migrations/*lifecycle*
- tests/**/lifecycle/**
- tests/**/attachments/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Limites temporais com relógio controlado; vencimento unânime suspende; arquivo só muda suspenso e sem manifestação; snapshots preservados.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-010, TEST-011. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-018 — Implementar notificações e Microsoft Graph

#### Status
BLOCKED

#### Phase
PHASE-04

#### Priority
HIGH

#### Objetivo
Entregar catálogo aprovado, trabalhador, lembretes, retentativas e painel de falhas.

#### Dependências
DEPENDS_ON: TASK-017

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-014. RN: RN-004, RN-011, RN-016, RN-022. RNF: RNF-009, RNF-010, RNF-011. UC: UC-014. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar catálogo aprovado, trabalhador, lembretes, retentativas e painel de falhas. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/notifications/**
- src/infrastructure/mail/**
- src/web/notifications/**
- tests/**/notifications/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Deduplicação por pendência/dia; eventos cancelam lembrete; 8h/janela; falha e aceitação distintas de entrega; contrato Graph testado. Credencial real depende de PD-005.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-014. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-019 — Implementar consulta, visibilidade e auditoria

#### Status
BLOCKED

#### Phase
PHASE-04

#### Priority
HIGH

#### Objetivo
Entregar painel, histórico documental e visibilidade por acesso.

#### Dependências
DEPENDS_ON: TASK-017

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-013, RF-018. RN: RN-001, RN-008, RN-012, RN-014, RN-016, RN-018, RN-019, RN-023, RN-024, RN-025. RNF: RNF-001, RNF-003, RNF-007, RNF-008, RNF-011, RNF-015. UC: UC-013, UC-018. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar painel, histórico documental e visibilidade por acesso. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/queries/**
- src/web/dashboard/**
- src/web/history/**
- tests/**/queries/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Participação aceita habilita histórico; autor autenticado vê conteúdo próprio oculto; bloqueios prevalecem; estado arquivado restringe Organizador.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-013, TEST-018. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-020 — Checkpoint PHASE-04

#### Status
BLOCKED

#### Phase
PHASE-04

#### Priority
HIGH

#### Objetivo
Validar fluxo completo de apreciação e encerramento.

#### Dependências
DEPENDS_ON: TASK-016, TASK-017, TASK-018, TASK-019

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-001, RNF-002, RNF-003, RNF-014. UC: N/A. ADR: ADR-002, ADR-003, ADR-004, ADR-005, ADR-006, ADR-007.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Validar fluxo completo de apreciação e encerramento. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- TASKS.md
- docs/verification/PHASE-04.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
NO_INCIDENTAL_CHANGES

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar implementação para esconder falhas; modificar requisitos/contratos; qualquer código de produção.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
E2E com nova versão, recusa, suspensão, mudança de decisão e encerramento; testes de concorrência; revisão segurança e notificações.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-021 — Implementar relatórios CSV e PDF

#### Status
BLOCKED

#### Phase
PHASE-05

#### Priority
HIGH

#### Objetivo
Entregar três relatórios aprovados e rastreáveis.

#### Dependências
DEPENDS_ON: TASK-020

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-015. RN: RN-012, RN-013, RN-014, RN-023, RN-024. RNF: RNF-001, RNF-003, RNF-015. UC: UC-015. ADR: ADR-004, ADR-008, ADR-009.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar três relatórios aprovados e rastreáveis. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/reports/**
- src/web/reports/**
- tests/**/reports/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Filtros e autorização; ressalvas; unanimidade separada de sucesso; CSV seguro; PDF revisado visualmente e legível.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-015. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-022 — Implementar arquivamento, recuperação e remoção

#### Status
BLOCKED

#### Phase
PHASE-05

#### Priority
CRITICAL

#### Objetivo
Entregar pacote verificável, recuperação somente leitura e exclusões autorizadas.

#### Dependências
DEPENDS_ON: TASK-021

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: RF-016. RN: RN-024, RN-025. RNF: RNF-001, RNF-003, RNF-006, RNF-012, RNF-015. UC: UC-016. ADR: ADR-004, ADR-008, ADR-009.

Justificativa técnica: entrega funcional diretamente rastreada aos RFs listados.

#### Artefatos esperados
Entregar pacote verificável, recuperação somente leitura e exclusões autorizadas. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- src/modules/archive/**
- src/web/archive/**
- database/migrations/*archive*
- tests/**/archive/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Round-trip mantém conteúdo e hashes; pacote externo hostil rejeitado; arquivo tira acesso organizador; confirmação externa; auditoria mínima; sem exclusão automática.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: TEST-016. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-023 — Validar segurança, acessibilidade e compatibilidade

#### Status
BLOCKED

#### Phase
PHASE-05

#### Priority
HIGH

#### Objetivo
Executar verificações transversais e corrigir defeitos diretamente associados aos critérios.

#### Dependências
DEPENDS_ON: TASK-022

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-005, RNF-007, RNF-008, RNF-011, RNF-012, RNF-013, RNF-015, RNF-016. UC: N/A. ADR: ADR-004, ADR-008, ADR-009.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Executar verificações transversais e corrigir defeitos diretamente associados aos critérios. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- tests/security/**
- tests/accessibility/**
- tests/compatibility/**
- docs/verification/**
- correções localizadas nos fluxos avaliados sem mudar contratos
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
WCAG/teclado/celular e matriz PD-008; credenciais/logs/CSRF/uploads; defeitos de arquitetura ou regra exigem TASK própria; não ampliar escopo como incidental.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-024 — Checkpoint PHASE-05

#### Status
BLOCKED

#### Phase
PHASE-05

#### Priority
HIGH

#### Objetivo
Concluir homologação funcional e documental.

#### Dependências
DEPENDS_ON: TASK-021, TASK-022, TASK-023

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-005, RNF-007, RNF-008, RNF-011, RNF-012, RNF-013, RNF-015, RNF-016. UC: N/A. ADR: ADR-004, ADR-008, ADR-009.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Concluir homologação funcional e documental. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- TASKS.md
- docs/verification/PHASE-05.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
NO_INCIDENTAL_CHANGES

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar implementação para esconder falhas; modificar requisitos/contratos; qualquer código de produção.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Relatórios e arquivo auditados; testes de aceitação; pendências de homologação resolvidas; nenhuma alegação de produção liberada.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-025 — Preparar implantação institucional

#### Status
BLOCKED

#### Phase
PHASE-06

#### Priority
HIGH

#### Objetivo
Configurar implantação no ambiente aprovado, segredos, envio real e observabilidade.

#### Dependências
DEPENDS_ON: TASK-024

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-005, RNF-007, RNF-008, RNF-011, RNF-012, RNF-013, RNF-015, RNF-016. UC: N/A. ADR: ADR-004, ADR-008, ADR-009.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Configurar implantação no ambiente aprovado, segredos, envio real e observabilidade. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- infrastructure/**
- docs/architecture/runbooks/**
- tests/deployment/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
PD-001/005/006/007 resolvidas; ambiente limpo; bootstrap seguro; saúde/logs/alertas; aprovação de implantação conforme autorização vigente.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-026 — Validar capacidade e critérios operacionais

#### Status
BLOCKED

#### Phase
PHASE-06

#### Priority
HIGH

#### Objetivo
Medir desempenho e limites no ambiente representativo.

#### Dependências
DEPENDS_ON: TASK-025

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-005, RNF-007, RNF-008, RNF-011, RNF-012, RNF-013, RNF-015, RNF-016. UC: N/A. ADR: ADR-004, ADR-008, ADR-009.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Medir desempenho e limites no ambiente representativo. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- tests/performance/**
- docs/verification/capacity.md
- ajustes locais de configuração operacional
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
PD-002/009 resolvidas; metas aprovadas medidas; gargalo que exige arquitetura gera ADR/TASK; sem inventar números.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-027 — Ensaiar backup, restauração e retenção

#### Status
BLOCKED

#### Phase
PHASE-06

#### Priority
HIGH

#### Objetivo
Comprovar recuperação consistente e procedimentos de retenção.

#### Dependências
DEPENDS_ON: TASK-025

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-005, RNF-007, RNF-008, RNF-011, RNF-012, RNF-013, RNF-015, RNF-016. UC: N/A. ADR: ADR-004, ADR-008, ADR-009.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Comprovar recuperação consistente e procedimentos de retenção. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- docs/architecture/runbooks/**
- tests/recovery/**
- infrastructure/backup/**
- TASKS.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
MINIMAL_DIRECTLY_CAUSED_CHANGES_ALLOWED

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar requisitos ou regras aprovadas; implementar tarefas futuras; modificar contratos públicos não relacionados; mudanças de segurança fora do objetivo; refatoração ampla; excluir histórico publicado.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
PD-003/004 resolvidas; ensaio de perda e restauração mede RPO/RTO; arquivo funcional não substitui backup; cópias e auditoria preservadas.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.

### TASK-028 — Checkpoint PHASE-06 e liberação

#### Status
BLOCKED

#### Phase
PHASE-06

#### Priority
CRITICAL

#### Objetivo
Avaliar liberação com evidências completas e decisão institucional.

#### Dependências
DEPENDS_ON: TASK-026, TASK-027

Bloqueio inicial: dependências ainda não implementadas; verificar também gates de pendências acima.

#### Requisitos relacionados
RF: N/A. RN: N/A. RNF: RNF-005, RNF-007, RNF-008, RNF-011, RNF-012, RNF-013, RNF-015, RNF-016. UC: N/A. ADR: ADR-004, ADR-008, ADR-009.

Justificativa técnica: fundação, verificação ou operação necessária à arquitetura aprovada; não introduz funcionalidade independente.

#### Artefatos esperados
Avaliar liberação com evidências completas e decisão institucional. Evidências dos critérios e testes aplicáveis; documentação técnica diretamente afetada; relatório em TASKS.md.

#### Allowed Changes
ALLOWED_CHANGES:
- TASKS.md
- docs/verification/PHASE-06.md
- docs/architecture/runbooks/release.md

Os caminhos de código são categorias planejadas, não arquivos existentes. Ajustar a convenção em TASK-001 antes de implementar; não ampliar a responsabilidade funcional por conveniência.

#### Incidental Changes Policy
NO_INCIDENTAL_CHANGES

#### Forbidden Changes
FORBIDDEN_CHANGES:
- Alterar implementação para esconder falhas; modificar requisitos/contratos; qualquer código de produção.
- Implantar em produção sem autorização de implantação.
- Credenciais reais em código, fixtures ou relatório.

#### Critérios de aceitação
Todas PD de produção resolvidas; gates, recuperação, capacidade, segurança e operação aprovados; liberação documentada; nenhuma implantação inferida da aprovação do planejamento.

#### Testes necessários
Gates aplicáveis e cenários específicos descritos nos critérios acima; integração com banco real para transações; negativos de autorização para APIs; E2E nos fluxos de interface.
Catálogo funcional: N/A. Checkpoints executam regressão da fase e dependências, sem atribuir PASS a teste não executado.

#### Definition of Done
Critérios desta ficha verificados; DoD global satisfeita; pendências necessárias resolvidas; evidências e limitações registradas; nenhuma expansão de escopo. Gates obrigatórios não podem ser dispensados para contornar falhas.

#### Registro de execução
Não iniciado. Branch: não criada. Commits: nenhum. Testes: não executados. Incidental Changes: NONE.





