# Execução da TASK-001 — PM2026_TR01

Atue como agente responsável pelo projeto PM2026_TR01 e execute exclusivamente a **TASK-001 — Fechar contratos e decisões técnicas de implementação**, conforme as fontes atuais do repositório. Esta instrução autoriza o trabalho documental da TASK-001; não autoriza implementar software, executar TASK-002 ou posteriores, publicar, fazer merge ou implantar. Não considere pendências aprovadas pelo simples pedido de execução.

## 1. Leitura e diagnóstico obrigatório

1. Leia, nesta ordem: `AGENTS.md`, `README.md`, `TASKS.md`, ADRs relacionados e, se existentes, código e testes. Leia integralmente a ficha da TASK-001 e as regras globais do backlog. Consulte especialmente ADR-001/002/003 e ADR-010, além dos ADRs afetados por identidade, segurança, documentos, notificações e tempo.
2. Leia os contratos relevantes em `docs/architecture/`, incluindo system, api, data-model, state-machines, security, operations, test-plan e references. Consulte as evidências documentais anteriores sem presumir que comprovam implementação.
3. Inspecione o diretório e o estado Git; preserve alterações preexistentes. Se não houver repositório Git, registre a limitação e solicite decisão sobre inicialização ou localização do checkout correto. Não execute `git init` nem simule branch/commit por inferência.
4. A precedência é: requisitos aprovados → ADRs aceitos → contrato operacional → ficha → código. Conflitos relevantes exigem parada e decisão explícita; não os resolva silenciosamente.
5. Revalide o estado atual: na elaboração deste prompt, a TASK-001 estava BLOCKED, sem dependências, por PD-010, contratos PD-007/011 e esclarecimentos PD-006. Este retrato não substitui a leitura dos arquivos na execução.

## 2. Elegibilidade, bloqueios e decisões

A TASK-001 é a atividade de resolução das pendências, mas não pode ser declarada READY ou DONE com lacunas bloqueantes. Faça o diagnóstico e apresente questões objetivas necessárias à resolução, agrupadas por decisão e acompanhadas de alternativas, recomendação e impacto. Não repita perguntas já respondidas nas fontes ou nesta sessão.

Se a DoR não estiver satisfeita, mantenha BLOCKED, registre o motivo e solicite as decisões necessárias. Não avance no trabalho dependente nem pule para outra tarefa. Propostas devem permanecer explicitamente pendentes, sem atualizar regras aprovadas como se tivessem sido aceitas. A ausência de resposta não é aprovação.

Verifique os seguintes pontos, sem transformar a lista em novos requisitos:

- **PD-010 — Sessões:** esclarecer o alcance de retirar sessões/inatividade: apenas expiração por inatividade, também duração máxima ou o próprio mecanismo de sessão autenticada. Não remover login, autorização, revogação ou proteção de autoria por inferência; não reconfirmar automaticamente os limites antigos de 8h/30min.
- **PD-010 — Cadastros:** obter mínimo/máximo exatos do título; formato do número acompanhado do ano, reinício e escopo da sequência, mantendo unicidade, imutabilidade e não reutilização conforme decisão aprovada. Esclarecer correção de e-mail da mesma pessoa versus troca de identidade, colisões e preservação de autoria/histórico após manifestação.
- **PD-010 — Avisos e tempo:** fechar catálogo e destinatários de todos os eventos administrativos; esclarecer fronteiras temporais ainda propostas. Preservar o lembrete imediato no aceite exatamente às 23h, limites de 1.000 caracteres já aprovados e ausência de campos adicionais. Não converter a proposta de fim exclusivo em regra aprovada sem resolver a decisão correspondente.
- **PD-006 — MFA:** esclarecer perfis, obrigatoriedade, validade, tentativas, reenvio e recuperação do código por e-mail. Após fechar o escopo, planejar tarefa específica e dependências conforme ADR-010, com ID inédito e sem implementar MFA nesta TASK. Distinguir bloqueios de desenvolvimento dos de implantação.
- **PD-007 — Arquivos:** confirmar unidade exata de 25 MB, sem assumir 25.000.000 bytes; esclarecer quantidade/volume quando necessários ao contrato. Definir proposta de serviço/adaptador de verificação, respostas e tratamento de indisponibilidade, preservando armazenamento privado, validação anterior à disponibilização e formatos aprovados. Separar complementos exigidos agora daqueles exigidos apenas antes da produção.
- **PD-011 — Tecnologia:** pesquisar fontes oficiais atuais para versões estáveis compatíveis de TypeScript, React, Material UI, NestJS, MySQL/InnoDB e Node.js LTS; avaliar acesso SQL/migrações, PDF e ferramentas de testes. Registrar versões exatas, data da consulta, URLs, suporte, licenças, restrições de compatibilidade e justificativas. Diferenciar compatibilidade documentada de compatibilidade comprovada por execução. Se não for possível verificar, registrar a pendência; não inventar versões. Documentar estratégia de fixação e atualização; não instalar dependências nem criar manifests, locks ou imagens nesta tarefa documental.

Não ampliar a resolução para todas as PDs de produção indiscriminadamente. Registre o impacto de PD-001 a PD-008 somente quando houver dependência real dos contratos da TASK-001. Preserve America/Sao_Paulo e armazenamento de instantes em UTC, sem fixar permanentemente UTC-3.

## 3. Início e escopo autorizado

Depois de resolvidas as condições de entrada e confirmada a DoR, registre BLOCKED → READY quando aplicável; crie uma branch adequada, por exemplo `chore/TASK-001-contratos-tecnicos`, e atualize READY → IN_PROGRESS no índice e na ficha. Não desenvolva em main. Se a branch já existir, inspecione-a antes de reutilizar; não sobrescreva trabalho alheio.

**Allowed Changes:** `docs/architecture/**`, `docs/adr/**`, `TASKS.md` e `README.md` somente para decisões explicitamente aprovadas. O relatório próprio em `validation/` é alteração documental primária obrigatória autorizada pelo AGENTS.md.

**Incidental Changes Policy:** `NO_INCIDENTAL_CHANGES`.

**Forbidden Changes:** implementar software; alterar requisito/regra sem decisão explícita; apresentar proposta como aprovada; executar tarefas futuras; implantar; inserir credenciais reais. Não alterar AGENTS.md, prompts ou outros arquivos fora do escopo para facilitar a execução.

Se alguma mudança necessária ultrapassar esses limites, use integralmente o modelo SCOPE ESCALATION do AGENTS.md, apresente alternativas e aguarde decisão. Para bloqueios, use o modelo BLOCKER e mantenha o registro operacional coerente.

## 4. Entrega documental

Com as decisões necessárias disponíveis, consolide os contratos técnicos previstos, sem antecipar código:

1. Registre decisões explícitas e sua origem nas fontes afetadas. Atualize o README apenas nos requisitos/contratos aprovados; registre estados, execução e evidências em TASKS.md.
2. Feche os detalhes pendentes de transações, ordem de bloqueios, revisão concorrente, idempotência, identificação física, erros e fronteiras temporais que os contratos atribuem à TASK-001. Preserve invariantes, APIs e arquitetura aprovadas; decisões arquiteturais relevantes exigem ADR individual e rastreável.
3. Documente convenção de diretórios compatível com as categorias de responsabilidade do backlog. Não crie estrutura de implementação nem amplie escopos funcionais futuros.
4. Sincronize modelo, APIs, segurança, estados, operação e plano de testes apenas onde diretamente afetados. Mantenha rastreabilidade RF/RN/RNF/UC/ADR/PD/TASK e cenários verificáveis para cada contrato fechado.
5. Preserve justificativas históricas dos ADRs; marque substituições expressamente. Não renumere nem reutilize IDs.
6. Registre pendências remanescentes, responsáveis pela decisão quando conhecidos e tarefas bloqueadas por elas. Não encerre artificialmente uma PD parcialmente resolvida.

## 5. Validação e encerramento

Ao terminar os artefatos, passe para IN_REVIEW. Revise o conteúdo e todas as alterações, classificando cada arquivo como PRIMARY; nenhuma alteração incidental é permitida. Confira referências, IDs, links locais, coerência entre documentos, índice/ficha, contratos, critérios de aceitação e ausência de decisões presumidas.

Execute verificações documentais adequadas e registre os comandos, ambiente e resultados reais. Avalie GATE-01 a GATE-08 individualmente: gates de software podem ser N/A nesta tarefa documental, sempre com justificativa específica; revisão documental e critérios de aceitação são obrigatórios. Não alegue build, testes, segurança operacional ou compatibilidade executada sem evidência. Falha de implementação/validação deve seguir FAILED → correção → revalidação → IN_REVIEW; decisão externa pendente mantém BLOCKED.

Faça commits pequenos e restritos à tarefa, quando as condições Git permitirem, no padrão `docs(contratos): <descrição> [TASK-001]`. Não inclua alterações alheias. Registre referências verificáveis em TASKS.md; ausência de commits deve ser explicitada e avaliada contra a DoD, nunca ocultada.

Antes da resposta final, inclusive em bloqueio ou tentativa incompleta:

- Grave um novo `validation/TASK-001_YYYY-MM-DD_HH-mm-ss.md`, com horário e fuso, sem sobrescrever relatórios; use sufixo sequencial em caso de colisão.
- Inclua objetivo, status final, alterações, decisões, verificações reais, pendências, branch e commits, além de todos os campos do TASK Execution Report do AGENTS.md: Primary Changes, Incidental Changes, Tests Executed, Quality Gates, Scope Validation, Definition of Done e Next Eligible TASK.
- Referencie o resumo no registro da TASK-001 em TASKS.md e confira existência e conteúdo do arquivo gravado.
- Só promova IN_REVIEW → DONE depois da validação completa e DoD satisfeita, com relatório persistido e verificado. Se houver impedimento, declare-o sem afirmar conclusão.
- Na resposta final, informe o resultado, decisões ou bloqueios relevantes, verificações, branch/commits e caminho do relatório. Identifique a próxima tarefa realmente elegível após sua DoR, ou NONE. TASK-002 não se torna automaticamente READY por depender da TASK-001.

**Pare ao concluir esta tarefa ou registrar seu bloqueio. Não execute a próxima tarefa sem autorização expressa.**
