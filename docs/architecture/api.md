# Contratos de API planejados

Prefixo /api/v1. IDs opacos; campos e limites finais em TASK-001. Não há endpoints implementados. Cabeçalhos de revisão/idempotência e esquemas completos serão fechados antes da tarefa dependente; nenhuma entrada livre pode alterar papel, autoria, estado derivado ou timestamp de servidor.

## Convenções de validação e respostas

Todas as operações: validar entrada, autorização atual por objeto e estado/prazo no servidor. 400 malformado; 401 sessão exigida; 403/404 sem vazamento; 409 conflito de estado/revisão; 422 regra semântica; 429 limitação; 503 falha temporária. Upload acrescenta 413/415. Operação assíncrona 202 devolve jobId e estado, não conclusão. GET não produz aceite, recusa, manifestação, publicação, encerramento ou exclusão.

Links são segredos de acesso: não registrar caminho completo em logs; trocar por contexto protegido quando aplicável. Consulta autenticada restrita valida identidade da sessão. Sessões internas e de apreciadores possuem finalidades distintas. Recuperação/emissão públicas respondem genericamente; não retornam tokens ou vínculos na página. Cada download revalida acesso.

Campos revision são versão esperada, não versão documental. Para operações sobre ciclo, conferir cycleId da tela; nunca aplicar ao ciclo corrente diferente silenciosamente. Respostas incluem IDs e estado resultante sem segredos, exceto cookie de sessão em autenticação.

## API-001 — Administrar contas internas

Finalidade: Criar, ativar, desativar e atribuir papéis a contas locais.

Rastreabilidade: RF-001; RN-002, RN-021; UC-001; TEST-001; TASK-006.

Validações específicas: Último Administrador protegido; redefinição revoga sessões; conta desativada não reativa por recuperação. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/internal/accounts` | Administrador | email, nome, papéis | conta pendente de ativação; 201 |
| PATCH | `/internal/accounts/{id}` | Administrador | active/papéis, revision | conta; 200 |
| POST | `/internal/accounts/{id}/activation` | Administrador | pedido de novo link | aceito; 202 |
| POST | `/internal/auth/activate` | Destinatário do link | token, nova senha | ativação concluída; 200 |
| POST | `/internal/auth/login` | Usuário interno | email, senha | cookie de sessão; 200 |
| POST | `/internal/auth/password-reset` | Público | email | resposta genérica; 202 |
| POST | `/internal/auth/password-reset/confirm` | Destinatário | token, nova senha | reset e revogação; 200 |
| POST | `/internal/auth/logout` | Usuário interno | sessão | 204 |

## API-002 — Administrar unidades e reuniões

Finalidade: Manter unidades e cadastrar reuniões com identificador automático.

Rastreabilidade: RF-002; RN-002, RN-023; UC-002; TEST-002; TASK-009.

Validações específicas: Campos obrigatórios validados; sigla única; unidade inativa não aceita novos vínculos; correção após publicação tem justificativa. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/units` | Administrador | nome, sigla | unidade; 201 |
| PATCH | `/units/{id}` | Administrador | nome/sigla/active, revision | unidade; 200 |
| GET | `/units` | Usuário interno | filtros/paginação | lista; 200 |
| POST | `/processes` | Administrador | título, data, unidade, descrição/referência opcionais | processo e número; 201 |
| PATCH | `/processes/{id}` | Administrador/Organizador vinculado | campos, justificativa, revision | processo; 200 |
| PUT | `/processes/{id}/organizers` | Administrador | IDs de contas, revision | vínculos; 200 |
| DELETE | `/processes/{id}` | Administrador | confirmação, justificativa | 204; somente nunca publicado conforme RN-025 |

## API-003 — Gerenciar vínculos e convites

Finalidade: Gerenciar apreciadores ativos, inclusões e remoções com efeito por ciclo.

Rastreabilidade: RF-003; RN-001, RN-005, RN-006, RN-007, RN-008; UC-003; TEST-003; TASK-014.

Validações específicas: Recusa não contornável; composição congelada imutável; remoção revoga apenas autorização correspondente. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/processes/{id}/memberships` | Administrador/Organizador | nome, email, revision | vínculo; 201 |
| POST | `/processes/{id}/memberships/{member}/remove` | Administrador/Organizador | alcance autorizado, justificativa, revision | remoção corrente ou planejamento futuro; 200 |
| GET | `/processes/{id}/memberships` | Administrador/Organizador | filtros | vínculos e convites; 200 |

## API-004 — Autenticar apreciador e recuperar acesso

Finalidade: Emitir senha temporária, abrir sessão e reenviar links por e-mail.

Rastreabilidade: RF-004; RN-001, RN-019, RN-020; UC-004; TEST-004; TASK-007.

Validações específicas: 10min/5 tentativas/60s aplicados; contrato de duração/inatividade da sessão bloqueado até esclarecer PD-010; recuperação não altera participação nem expõe links na página. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/appraiser/auth/password` | Público | email | 202 genérico |
| POST | `/appraiser/auth/verify` | Apreciador | email, senha temporária | sessão; 200 |
| POST | `/appraiser/access-recovery` | Público | email | 202 genérico; links só por e-mail |
| POST | `/appraiser/auth/logout` | Apreciador | sessão | 204 |
| GET | `/appraiser/session` | Apreciador autenticado | sessão | identidade e autorizações atuais mínimas; 200 |

## API-005 — Preparar ata e rascunho

Finalidade: Manter uma próxima versão em preparação e descartar conteúdo exclusivo com auditoria.

Rastreabilidade: RF-005; RN-003, RN-004, RN-014, RN-025; UC-005; TEST-005; TASK-012.

Validações específicas: Upload não publica; só um rascunho; descarte não remove arquivos publicados. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| PUT | `/processes/{id}/draft` | Administrador/Organizador | arquivoAtaId, anexos selecionados, convidados/exclusões, prazos, revision | rascunho; 200/201 |
| GET | `/processes/{id}/draft` | Administrador/Organizador | nenhuma | rascunho; 200 |
| DELETE | `/processes/{id}/draft` | Administrador/Organizador | confirmação, revision | 204; descarte auditável |

## API-006 — Validar e armazenar documentos

Finalidade: Receber ata PDF e anexos permitidos em armazenamento privado.

Rastreabilidade: RF-006; RN-015, RN-017, RN-025; UC-006; TEST-006; TASK-011.

Validações específicas: Conteúdo e extensão verificados; PDF com senha rejeitado; limites novos não invalidam arquivos existentes. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/processes/{id}/files` | Administrador/Organizador | multipart arquivo e finalidade | arquivo em validação; 202 |
| GET | `/processes/{id}/files/{file}/status` | Administrador/Organizador | nenhuma | estado de validação; 200 |
| GET | `/processes/{id}/files/{file}/content` | Usuário interno autorizado | modo inline/download | bytes autorizados; 200 |
| GET | `/access/{link}/files/{file}` | Apreciador conforme link/visibilidade | sessão se conteúdo restrito | bytes; 200 |

## API-007 — Publicar novo ciclo

Finalidade: Publicar versão e convites e substituir ciclo anterior atomicamente.

Rastreabilidade: RF-007; RN-003, RN-004, RN-005, RN-009, RN-014, RN-016; UC-007; TEST-007; TASK-013.

Validações específicas: Sem dois ciclos correntes; rollback integral em falha; novo ciclo exige novos aceites, preservando links ativos. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/processes/{id}/cycles` | Administrador/Organizador | draftId, revision, confirmação, chave idempotência | ciclo publicado; 201 |

## API-008 — Aceitar ou recusar convite

Finalidade: Registrar resposta individual por ciclo.

Rastreabilidade: RF-008; RN-005, RN-006, RN-007, RN-019, RN-020; UC-008; TEST-008; TASK-014.

Validações específicas: Aceite autenticado; recusa explícita sem sessão; prazo/estado impedem resposta inválida; recusa definitiva. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/access/{link}/cycles/{cycle}/accept` | Apreciador autenticado correspondente | revision, confirmação | convite aceito; 200 |
| POST | `/access/{link}/cycles/{cycle}/refuse` | Portador do link válido | revision, confirmação explícita | recusa; 200 |

## API-009 — Registrar e alterar manifestação

Finalidade: Registrar decisões sucessivas sem sobrescrever histórico.

Rastreabilidade: RF-009; RN-012, RN-013, RN-016, RN-019; UC-009; TEST-009; TASK-016.

Validações específicas: Texto exigido nas três decisões; versão e composição registradas; autorização e prazo revalidados ao persistir. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/access/{link}/cycles/{cycle}/manifestations` | Apreciador autenticado participante | decisão, texto, ataVersionId, compositionId, revision, chave idempotência | novo registro; 201 |
| GET | `/access/{link}/cycles/{cycle}/my-manifestations` | Apreciador autenticado autor | paginação | sequência própria autorizada; 200 |

## API-010 — Administrar prazos e suspensão

Finalidade: Fechar convites, suspender, reativar e ajustar prazos.

Rastreabilidade: RF-010; RN-007, RN-009, RN-010, RN-011; UC-010; TEST-010; TASK-017.

Validações específicas: Congelar somente prazos abertos; não reabrir convites; vencimento suspende mesmo com unanimidade. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| PATCH | `/processes/{id}/cycles/{cycle}/deadlines` | Administrador/Organizador | prazo(s), justificativa se antecipação, revision | prazos; 200 |
| POST | `/processes/{id}/cycles/{cycle}/suspend` | Administrador/Organizador | justificativa, revision | ciclo suspenso; 200 |
| POST | `/processes/{id}/cycles/{cycle}/reactivate` | Administrador/Organizador | novo prazo se vencido, justificativa, revision | ciclo ativo; 200 |

## API-011 — Gerenciar composição de anexos

Finalidade: Versionar composições e preservar a base documental.

Rastreabilidade: RF-011; RN-015, RN-016; UC-011; TEST-011; TASK-017.

Validações específicas: Ciclo publicado só altera suspenso e sem manifestações; caso contrário exige nova versão/ciclo. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| PUT | `/processes/{id}/cycles/{cycle}/attachments` | Administrador/Organizador | lista de arquivos aceitos, revision | nova composição; 201 |

## API-012 — Encerrar ciclo ou processo

Finalidade: Encerrar com alcance explicitamente confirmado e histórico preservado.

Rastreabilidade: RF-012; RN-003, RN-013, RN-014, RN-025; UC-012; TEST-012; TASK-016.

Validações específicas: Sucesso exige ciclo ativo e unanimidade na transação; insucesso justificado; processo não reabre; links invalidados no encerramento definitivo. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/processes/{id}/cycles/{cycle}/close-unsuccessfully` | Administrador/Organizador | justificativa, confirmação de alcance, revision | ciclo encerrado, processo aberto; 200 |
| POST | `/processes/{id}/close` | Administrador/Organizador | resultado, justificativa se insucesso, confirmação, revision, chave idempotência | processo encerrado; 200 |

## API-013 — Consultar painel e histórico

Finalidade: Exibir documentos, situação, pendências e histórico conforme permissões.

Rastreabilidade: RF-013; RN-018, RN-019, RN-023, RN-024; UC-013; TEST-013; TASK-019.

Validações específicas: Histórico antigo só por participação aceita no ciclo ativo e configuração; conteúdo individual oculto só ao autor autenticado; estados bloqueadores prevalecem. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| GET | `/processes` | Usuário interno | período, situação, organizador, paginação | lista autorizada; 200 |
| GET | `/processes/{id}` | Usuário interno autorizado | nenhuma | detalhe; 200 |
| GET | `/access/{link}` | Portador de link | sessão opcional | conteúdo permitido ou mensagem de bloqueio; 200/404 |
| GET | `/access/{link}/history` | Apreciador com aceite no ciclo ativo | paginação, sessão para dados próprios restritos | histórico filtrado; 200 |
| PATCH | `/processes/{id}/visibility` | Administrador/Organizador | historyVisible, decisionsVisible, revision | configuração; 200 |

## API-014 — Notificar e acompanhar envios

Finalidade: Enviar convites, credenciais, lembretes e avisos definidos, com falhas e reenvio.

Rastreabilidade: RF-014; RN-004, RN-011, RN-016, RN-022; UC-014; TEST-014; TASK-018.

Validações específicas: 8h e janela 8h–23h (23h incluído) respeitadas; interrupção de pendências; não afirmar entrega apenas por aceitação do provedor. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| GET | `/processes/{id}/notifications` | Administrador/Organizador | paginação/filtros | tentativas sanitizadas; 200 |
| POST | `/processes/{id}/notifications/{notification}/retry` | Administrador/Organizador | confirmação | tentativa agendada se elegível; 202 |
| POST | `/processes/{id}/memberships/{member}/resend-link` | Administrador/Organizador | confirmação | reenvio se autorizado; 202 |

## API-015 — Emitir relatórios

Finalidade: Exportar listagem CSV, histórico PDF e registro de aprovação PDF.

Rastreabilidade: RF-015; RN-012, RN-013, RN-014, RN-023, RN-024; UC-015; TEST-015; TASK-021.

Validações específicas: CSV filtra criação/situação/Organizador; aprovação contém ressalvas vigentes; distinguir unanimidade de oficialização. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/reports/processes` | Administrador/Organizador | filtros criação/situação/Organizador, formato CSV | trabalho/arquivo; 202 |
| POST | `/processes/{id}/reports` | Administrador/Organizador | tipo HISTORY ou APPROVAL, formato PDF | trabalho; 202 |
| GET | `/report-jobs/{id}` | Solicitante ainda autorizado | nenhuma | estado/resultado protegido; 200 |

## API-016 — Arquivar, recuperar e remover

Finalidade: Gerar/verificar arquivo e recuperar pacotes internos/externos para consulta.

Rastreabilidade: RF-016; RN-024, RN-025; UC-016; TEST-016; TASK-022.

Validações específicas: Arquivar revoga acesso de Organizadores; recuperação nunca reabre; remoção exige verificação; exclusão interna exige confirmação externa e auditoria. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| POST | `/processes/{id}/archive` | Administrador | confirmação, revision | trabalho; 202 |
| POST | `/archives/import` | Administrador | pacote externo | verificação/recuperação; 202 |
| POST | `/archives/{id}/recover` | Administrador | confirmação | consulta recuperada; 202 |
| GET | `/archives/{id}` | Administrador | nenhuma | metadados/consulta protegida; 200 |
| POST | `/processes/{id}/purge-operational-data` | Administrador | arquivo verificado, justificativa, confirmação | remoção auditada; 202 |
| DELETE | `/archives/{id}/internal-package` | Administrador | confirmação cópia externa, justificativa, confirmação destrutiva | remoção auditada; 202 |

## API-017 — Configurar parâmetros administrativos

Finalidade: Configurar limites de arquivo e parâmetros admitidos, com auditoria.

Rastreabilidade: RF-017; RN-017, RN-020, RN-021, RN-022; UC-017; TEST-017; TASK-009.

Validações específicas: Exceção por reunião justificada; teto técnico respeitado; mudanças registradas e não retroativas. Parâmetros operacionais protegidos definidos no contrato. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| GET | `/settings/file-limits` | Administrador | nenhuma | configuração; 200 |
| PATCH | `/settings/file-limits` | Administrador | limite padrão, revision | configuração; 200 |
| PUT | `/processes/{id}/file-limit` | Administrador | limite, justificativa, revision | exceção; 200 |

## API-018 — Preservar e consultar auditoria

Finalidade: Preservar eventos, autoria, instantes, motivos e alterações históricas.

Rastreabilidade: RF-018; RN-001, RN-008, RN-012, RN-014, RN-016, RN-023, RN-024, RN-025; UC-018; TEST-018; TASK-019.

Validações específicas: Operações mutáveis relevantes auditadas; logs técnicos sem segredos; histórico não editável por operações comuns. Aplicar também todas as regras relacionadas e convenções acima a cada operação.

| Método | Rota | Ator autorizado | Entrada | Saída/sucesso |
|---|---|---|---|---|
| GET | `/processes/{id}/audit` | Administrador/Organizador autorizado | filtros/paginação | eventos filtrados; 200 |
| GET | `/audit/minimal` | Administrador | identificador processo removido, paginação | auditoria mínima; 200 |

## Operações internas sem endpoint público

Expirar convites, congelar composição, suspender por vencimento, processar lembretes, limpar temporários e verificar arquivo são comandos internos idempotentes. Não expor como rotas públicas de conveniência. Mesmo chamados pelo trabalhador, devem respeitar RN e registrar auditoria.

## Segurança de paginação e exportação

Limites máximos de página/relatório definidos em TASK-001; paginação estável. Filtros nunca substituem autorização. CSV deve neutralizar fórmulas de planilha. Relatório assíncrono revalida acesso no download, inclusive se processo tiver sido arquivado após a solicitação.

## Complemento de 01/10/2026

Revisão 01/10/2026: textos de descrição, justificativa e manifestação até 1.000 caracteres; sem campos adicionais. Título, correção de e-mail, numeração anual e sessões aguardam complementos PD-010. O login interno exige senha seguida de código por e-mail para Administradores e Organizadores, conforme ADR-012. A saída de sessão da rota de login acima só pode representar o fluxo completo após MFA; rotas/esquemas do desafio ainda serão detalhados na TASK-001. Recuperação excepcional permanece pendente em PD-006.

## Decisões posteriores PD-010
Prevalece a [consolidação ADR-011](../adr/ADR-011-consolidacao-pd-010.md) sobre os trechos anteriores sob revisão: sessões sem duração máxima/inatividade em todos os perfis; título 100–200; número institucional anual pelo ano da reunião; correção de e-mail da mesma identidade com bloqueio de colisão e revogação; distribuição de avisos aprovada; fim exclusivo dos prazos. Correção de data para outro ano ainda pendente. Estas são especificações, não evidências de implementação.

