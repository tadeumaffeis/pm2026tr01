# Modelo inicial de dados

Base: MySQL/InnoDB. PKs internas imutáveis, FKs explícitas e índices propostos abaixo. Convenções de tipos, driver, migrações e tratamento de unicidade condicional em TASK-001. Tabelas auditáveis mutáveis possuem created_at/created_by, updated_at/updated_by e revision quando aplicável; eventos imutáveis possuem occurred_at/actor. Não executar migrações nesta etapa.

| Tabela | Atributos/chaves | Restrições e índices |
|---|---|---|
| internal_account | id PK; email_normalized UNIQUE; password_hash; active; activated_at; revision | Papéis por account_role(account_id FK, role), PK composta; não apagar autoria. |
| internal_session | id PK; account_id FK; token_hash UNIQUE; created_at; last_activity_at; expires_at; revoked_at | Índices account_id/revoked_at e expires_at; nunca token claro. |
| account_action_token | id PK; account_id FK; kind; token_hash UNIQUE; expires_at; used_at; revoked_at | Ativação/reset; nova emissão invalida anterior utilizável na mesma finalidade; prazo configurado. |
| unit | id PK; name; acronym_normalized UNIQUE; active; revision | Unidade referenciada não excluível; índices active/name. |
| process | id PK; number UNIQUE; title; meeting_date; unit_id FK; description; external_reference; state; current_cycle_id FK nullable; history_visible; decisions_visible; closed_at; archived_at; revision | Número imutável, reserva não reutilizada; FKs de ciclo devem pertencer ao processo. Índices created_at/state, unit_id, closed_at. |
| process_organizer | process_id FK; account_id FK; active; linked_at; unlinked_at | PK/ID de histórico; impedir dois vínculos ativos iguais; índice account_id/active/process_id. |
| appraiser_identity | id PK; email_normalized UNIQUE; name; revision | Não aplicar equivalência de aliases; IDs preservados em reinclusão. Dados exibidos em registros históricos têm snapshot. |
| appraiser_session | id PK; identity_id FK; token_hash UNIQUE; created_at; last_activity_at; absolute_expires_at; revoked_at | Sessão global; autorização por vínculo em cada operação; índices identity_id e expiração. |
| validation_password | id PK; identity_id FK; secret_digest; emitted_at; expires_at; failed_attempts; used_at; invalidated_at | Uso único e invalidação concorrente; índice identity_id/emitted_at. Proteção de segredo curto com chave de servidor; não guardar senha clara. |
| process_membership | id PK; identity_id FK; process_id FK; participation_number; link_token_hash UNIQUE; active; ended_at; end_reason | UNIQUE process_id/identity_id/participation_number; impedir dois vínculos ativos por identidade/processo. Índice process_id/active. |
| draft | id PK; process_id FK UNIQUE; ata_file_id FK nullable; revision; prepared_deadlines | Um rascunho por processo. Tabelas draft_member e draft_attachment com FKs; exclusões futuras explícitas. |
| cycle | id PK; process_id FK; version_number; state; invitation_deadline; manifestation_deadline; invitation_closed_at; suspended_at; invitation_remaining; manifestation_remaining; suspension_reason; current_composition_id FK; revision | UNIQUE process_id/version_number; deadline de manifestação posterior; corrente é coordenado pelo processo; índices state/deadlines. |
| ata_version | id PK; cycle_id FK UNIQUE; file_id FK; published_at; content_hash | Um documento de ata por ciclo; arquivo imutável; mesma referência pode ser reutilizada em novo ciclo sem reaproveitar decisões. |
| invitation | id PK; cycle_id FK; identity_id FK; membership_id FK; state; answered_at; removed_at; removal_reason; name_snapshot; email_snapshot | UNIQUE cycle_id/identity_id preserva recusa contra reinclusão; vínculo histórico não pode apagar essa decisão. Índice cycle_id/state. |
| frozen_participant | cycle_id FK; invitation_id FK; identity_id FK; frozen_at | PK cycle_id/identity_id; conjunto criado no fechamento, somente convites aceitos elegíveis; imutável depois. |
| file_object | id PK; storage_key UNIQUE; original_name; detected_type; byte_size; sha256; validation_state; uploaded_by; created_at | Chave privada, integridade; índice validation_state. Bytes não em coluna BLOB por padrão. |
| attachment_composition | id PK; cycle_id FK; sequence; created_at; created_by | UNIQUE cycle_id/sequence; conjunto imutável e inclusive vazio. |
| attachment_item | composition_id FK; file_id FK; display_name; position | PK composta adequada; não duplicar mesmo arquivo inadvertidamente; associação preservada nas composições anteriores. |
| manifestation | id PK; cycle_id FK; invitation_id FK; identity_id FK; ata_version_id FK; composition_id FK; decision; text; recorded_at; actor_snapshot | Append-only; todas as FKs documentais pertencem ao mesmo ciclo. Índice cycle_id/identity_id/recorded_at. Ponteiro vigente em current_manifestation(cycle_id,identity_id,manifestation_id), PK composta. |
| audit_event | id PK; process_id referência lógica; cycle_id referência lógica; actor_id; actor_kind; event_type; occurred_at; before_data; after_data; reason; correlation_id | Append-only para operações comuns; minimização/retencão por política. Referências mínimas sobrevivem a purge autorizado sem FKs que apaguem auditoria em cascata. |
| outbox_job | id PK; kind; aggregate_id; payload; deduplication_key UNIQUE; state; available_at; attempts; lease_until | Confirmado junto com negócio; índices state/available_at e lease_until. Dados sensíveis mínimos e protegidos. |
| notification_attempt | id PK; job_id FK; recipient; attempted_at; provider_reference; result; sanitized_error | Tentativas auditáveis; resultado aceito não equivale a entregue; índice job_id/attempted_at. |
| archive_package | id PK; process_id referência; storage_location; manifest_hash; schema_version; verified_at; archived_by; external_copy_confirmed_at; removed_at | Histórico de verificação, geração e exclusão; cópia recuperada em namespace de consulta, sem inserir fluxo operacional ativo. |
| configuration | key PK; value; revision; changed_by; changed_at | Histórico em audit_event. Exceção process_file_limit(process_id FK UNIQUE, bytes, reason, changed_by); teto técnico separado. |

## Integridade e cardinalidades

Unidade 1:N processos; processo N:M contas organizadoras via vínculo; identidade 1:N vínculos históricos; processo 1:N ciclos; ciclo 1:1 ata; ciclo 1:N convites/composições; convite 1:N manifestações; composição N:M arquivos. Processo 0:1 rascunho e 0:1 ciclo corrente. Identidade 1:N sessões; não vincular sessão a um único processo.

Restrições compostas ou validações transacionais devem impedir referências entre ciclos diferentes. MySQL não oferece a mesma forma de índice parcial de outros bancos: unicidade de vínculos ativos deve ser resolvida por estratégia explícita (coluna derivada/índice ou tabela corrente), aprovada tecnicamente em TASK-001, não por SELECT prévio sem bloqueio.

Não aplicar ON DELETE CASCADE a manifestações/documentos/auditoria para exclusões comuns. Remoção operacional após arquivamento usa procedimento específico, verificado e auditável. Ponteiros correntes podem mudar; eventos históricos não.

## Decisões ainda dependentes

- Formato legível do número da reunião e limites de texto: PD-010.
- Precisão temporal, convenção de fim exclusivo e saldo: contrato em TASK-001, preservando regras aprovadas.
- Índices finais orientados a consultas reais; não criar particionamento sem PD-002.
- Armazenamento de payload de envio com segredo temporário exige proteção e expurgo técnico definido; não colocar senha em audit_event ou logs.
- Snapshots históricos de nome/e-mail não são atualizados por correção cadastral posterior.
- Arquivo recuperado guarda referência à versão de esquema e executa apenas consultas autorizadas; migração de pacote não altera conteúdo original.

## Complemento de 01/10/2026

Revisão 01/10/2026: descrição, justificativas e manifestações até 1.000 caracteres; número com ano, formato/reinício pendentes; título 100 a 200 caracteres com interpretação pendente. Preservar snapshots na correção de e-mail; contrato dessa correção e alcance da retirada de sessões/inatividade aguardam PD-010. Campos de sessão acima são modelo anterior sob revisão, não autorização para implementar decisão pendente.

## Decisões posteriores PD-010
Prevalece a [consolidação ADR-011](../adr/ADR-011-consolidacao-pd-010.md) sobre os trechos anteriores sob revisão: sessões sem duração máxima/inatividade em todos os perfis; título 100–200; número institucional anual pelo ano da reunião; correção de e-mail da mesma identidade com bloqueio de colisão e revogação; distribuição de avisos aprovada; fim exclusivo dos prazos. Correção de data para outro ano ainda pendente. Estas são especificações, não evidências de implementação.

Os campos expires_at e absolute_expires_at das sessões não representam mais validade da sessão e devem ser retirados do modelo de sessão na consolidação física. last_activity_at, se mantido como metadado, não causa expiração. Validades de credenciais temporárias são independentes.

