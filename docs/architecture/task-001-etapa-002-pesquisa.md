# TASK-001 — Etapa 002 — Resolução de pendências e pesquisa técnica

Data da pesquisa: 2026-10-05. Status: proposta documental; nenhuma decisão de negócio ou compatibilidade prática foi aprovada.

## PD-010 — Correção da data entre anos

O número da reunião é anual, imutável e baseado no ano da reunião. A data continua corrigível enquanto o processo está aberto, portanto uma correção pode mudar o ano associado ao número.

Alternativas que exigem decisão explícita:

1. Preservar o número original, mesmo que o ano deixe de coincidir com a data corrigida. Mantém imutabilidade, mas permite divergência visível.
2. Impedir correção que atravesse o ano. Mantém a invariável número/ano, mas restringe a correção cadastral.
3. Outra regra institucional explicitamente aprovada. Não renumerar automaticamente e não reutilizar números.

Decisão explícita do usuário: aplicar a alternativa 1. Se a correção mudar o ano, preservar o número original, mesmo com divergência visível entre o ano do número e a data corrigida. Não renumerar nem reutilizar; registrar a correção e a divergência na auditoria. Esta pendência está resolvida.

## PD-007 — Verificação de arquivos

Limites já aprovados: 26.214.400 bytes por arquivo; uma ata PDF e até dez anexos por versão; o total aritmético de 288.358.400 bytes não é quota de histórico.

Proposta para decisão: scanner ClamAV local em contêiner privado, com clamd/FreshClam, bytes enviados pelo protocolo INSTREAM e assinaturas persistidas em volume. A proposta mantém o scanner sem porta pública e não envia documentos a serviço externo. A aprovação do scanner, seus parâmetros e sua licença ainda não ocorreu.

Fluxo proposto: `QUARANTINED` → validação de tamanho/formato/conteúdo → exame completo → `ACCEPTED` ou `REJECTED`. Timeout, erro, exame incompleto, assinatura vencida ou limite interno de inspeção produzem `VERIFICATION_PENDING`/indisponível; nunca equivalem a arquivo limpo. Publicação e download só aceitam `ACCEPTED`. Os limites de upload são distintos dos limites de extração de contêineres Office/ODF.

Parâmetros que precisam ser fechados em contrato: StreamMaxLength, MaxFileSize, MaxScanSize, profundidade/quantidade de itens extraídos, timeout, retentativa, limiar de defasagem de assinaturas e operação quando o scanner estiver indisponível. Nenhum scanner foi instalado ou testado nesta etapa.

Fontes oficiais consultadas: https://docs.clamav.net/manual/Installing/Docker.html, https://docs.clamav.net/manual/Usage/ClamdProtocol.html, https://docs.clamav.net/manual/Usage/Scanning.html e https://docs.clamav.net/. A proposta existente em `pd-007-verificacao-arquivos.md` continua com status PROPOSTA.

## PD-006 — Recuperação excepcional do único Administrador

Decisões vigentes: equipe de TI verifica a identidade e autoriza a recuperação por arquivos de configuração; a alteração exige justificativa e auditoria, revoga sessões/códigos e o próximo login exige senha e MFA. Nenhum mecanismo pode desligar o MFA.

Detalhamento proposto para decisão técnica: registrar identificador da solicitação, responsável da TI, evidência/resultado da verificação sem armazenar documento desnecessário, aprovador, timestamp UTC, parâmetro alterado, valor anterior sem expor segredo, valor posterior minimizado, motivo, correlação e revisão. Aplicar alteração em procedimento controlado, com dupla conferência, backup seguro da configuração, rollback delimitado e invalidação de sessões/códigos. O procedimento exato, parâmetros permitidos e tarefa própria de MFA ainda precisam ser aprovados; esta proposta não autoriza alterar configuração real.

## PD-011 — Pesquisa de stack

| Componente | Evidência oficial consultada em 2026-10-05 | Candidato documental | Estado/limitação |
|---|---|---|---|
| Node.js | https://nodejs.org/en/about/previous-releases; https://nodejs.org/en/blog | Node.js 24.21.0 LTS; Node 26 é Current | Candidato. Confirmar runtime dos pacotes e fixar imagem/digest no início da implementação. |
| TypeScript | https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-9.html | Linha TypeScript 5.9 | Candidato. A página oficial consultada confirma a linha 5.9, mas o patch exato deve ser verificado no momento de fixação. |
| React | https://react.dev/versions | React 19.3 | Candidato. A página oficial identifica 19.3 como versão mais recente; compatibilidade com MUI/Nest e toolchain ainda não foi construída. |
| Material UI | https://mui.com/material-ui/getting-started/versions/; https://mui.com/material-ui/getting-started/support/ | Material UI v9 | Candidato. v9 é o major estável recomendado; verificar peers, React e TypeScript antes de fixar. |
| NestJS | https://docs.nestjs.com/first-steps; https://docs.nestjs.com/migration-guide | NestJS v12 | Candidato. A documentação atual descreve migração 11→12 e exige Node 20.19+, ou 22.12+ na linha 22; validar todos os pacotes do monólito. |
| MySQL/InnoDB | https://dev.mysql.com/doc/refman/26.7/en/mysql-releases.html; https://www.mysql.com/news-and-events/ | MySQL 9.7 LTS (ou linha LTS compatível após revisão) | Candidato. O modelo LTS/Innovation e a mudança para versionamento calendário exigem validar driver, imagem e compatibilidade SQL; não há banco para teste nesta etapa. |

O candidato não é uma seleção aprovada. A compatibilidade entre React 19.3, MUI 9, TypeScript 5.9, NestJS 12, Node 24 LTS e MySQL 9.7 não foi compilada nem executada. A seleção deve ser repetida e fixada com versões exatas, lockfile, imagem e digest em tarefa posterior autorizada.

## Matriz de rastreabilidade

| Decisão/pendência | Fonte/autorização | Impacto | Arquivo a consolidar | Estado |
|---|---|---|---|---|
| Correção de data entre anos | ADR-011, alternativa 1 decidida pelo usuário | Número, cadastro e auditoria | data-model.md, api.md, README/ADR | RESOLVIDA |
| Scanner e indisponibilidade | PD-007; solução ainda proposta | Upload, publicação, operação e segurança | pd-007-verificacao-arquivos.md, api.md, security.md | PROPOSTA/PENDENTE |
| Recuperação único Admin | ADR-012; procedimento técnico pendente | Segurança, auditoria, operação e futura TASK MFA | ADR-012, security.md, operations.md, TASKS.md | PROPOSTA/PENDENTE |
| Versões e licenças | PD-011; fontes oficiais acima | Bootstrap, CI, runtime, banco e manutenção | references.md e ADR técnico futuro | CANDIDATA/PENDENTE |

## Gate da etapa

WF-002: BLOQUEADO. Critérios concluídos: 2/5 — PD-010 complementar resolvida e pesquisa documental produzida. Critérios pendentes: PD-007 não aprovada; PD-006/tarefa própria não delimitadas; PD-011 ainda sem compatibilidade prática; DoR da TASK incompleta. Nenhuma proposta técnica foi tratada como aprovação.
