# Arquitetura detalhada

## Fronteiras

Frontend: apresentação, acessibilidade, confirmação de ações e validações de conveniência. API: contratos e autorização de entrada. Aplicação: transações e orquestração. Domínio: estados, prazos, elegibilidade e invariantes. Infraestrutura: SQL, arquivos, Graph, relógio e trabalhos. Validação no frontend nunca substitui servidor.

| Módulo | Responsabilidade | Fronteira |
|---|---|---|
| internal-auth | Contas e sessões internas | Não concede participação externa automaticamente |
| appraiser-auth | Identidade, senha temporária e sessão | Não decide acesso a processo sem vínculo |
| registry | Unidades, reunião, Organizadores e configuração | Não altera conteúdo de ata publicada |
| drafts/documents | Preparação e validação de arquivos | Não publica por upload |
| publication/participation | Ciclo corrente, convites e conjunto de participantes | Não transfere aceite entre ciclos |
| decisions/closure | Histórico de manifestações, unanimidade e encerramento | Não ignora prazo nem estado |
| lifecycle/attachments | Prazos e composição documental | Não modifica base de manifestação existente |
| queries/reports | Projeções, visibilidade e exportação | Não amplia acesso por ter ID/URL |
| notifications | Intenções, retentativas e lembretes | Não altera resultado de negócio por falha de entrega |
| archive | Pacotes e consulta recuperada | Não reabre nem reativa links |

## Transações e concorrência

Coordenação por processo/ciclo no banco. Estratégia recomendada: serializar operações críticas com bloqueio de linha do processo/ciclo e validar revision esperada. Ordem uniforme de bloqueios: processo → ciclo → convite/participação → ponteiros de manifestação. Fixar detalhe técnico em TASK-001. Unicidade e FKs complementam, não substituem, validações.

- Publicação: validar rascunho/arquivos/prioridade temporal; encerrar predecessor; criar ciclo, versão, composição, convites; apontar corrente; registrar auditoria e outbox; commit único.
- Manifestação: confirmar ciclo esperado, sessão, participação, prazo e base documental; acrescentar evento; atualizar ponteiro vigente; recalcular condição; auditoria; commit.
- Encerramento: revalidar prazo dos convites fechado e participantes congelados, decisões vigentes e estado ATIVO; encerrar; revogar vínculos operacionais; marcar descarte de rascunho; commit. Limpeza de bytes só depois e somente se não referenciados.
- Fechamento de convites: uma única consolidação idempotente; expirar pendentes; fixar conjunto de participantes; registrar instante lógico de fechamento e processamento.
- Pedido repetido: chave de idempotência proposta nas operações críticas evita duplicação; payload diferente com mesma chave gera conflito. Contrato exato em TASK-001.

Se manifestação não aprovativa ganha a disputa, encerramento de sucesso falha. Se encerramento confirmado ganha, manifestação posterior falha por processo encerrado. Não existir período de sucesso com decisão vigente incompatível.

## Relógio e trabalhos

Relógio do servidor é fonte; UTC persistido e fuso IANA para calendário local. Prazo é intervalo com fim exclusivo proposto: em instante igual ao fim, já encerrado. Esta convenção deve ser registrada no fechamento de contratos TASK-001.

Agendador materializa vencimentos e lembretes, mas APIs verificam os limites mesmo se estiver atrasado. Suspensão salva saldo somente de prazo ainda aberto; prazo fechado nunca recebe saldo positivo. Reativação manual usa saldo; vencimento exige novo prazo.

Fila no banco com estado, tentativa, disponível_em, bloqueio temporário, erro sanitizado e chave de deduplicação. Trabalhador verifica elegibilidade antes de enviar. Entrega externa exatamente uma vez não é prometida: timeout após aceitação pode gerar resultado incerto. Política de reenvio e visibilidade do resultado deve evitar falso sucesso.

## Armazenamento e integridade

Bytes não são públicos. Toda leitura passa por autorização; preferir streaming autenticado/autorizado para permitir revogação imediata, inclusive durante suspensão. Caso URL assinada seja adotada, discutir seu período de revogação antes de mudar esta garantia.

Upload temporário → validação de tamanho/tipo/conteúdo e segurança → aceito ou rejeitado. Somente aceito participa da publicação. Não confiar no MIME declarado. Office/ODF exigem inspeção do contêiner e rejeição de macros/conteúdo incompatível. Arquivo importado de arquivamento é fluxo separado, com limites de extração e verificação, não anexo genérico permitido.

Composição é conjunto de referências imutáveis; publicação cria composição inclusive vazia. Hash de cada arquivo e manifesto de composição. Não usar hash como assinatura digital ou prova de autoria. Banco e bytes exigem backup consistente.

## Tratamento de erros

400 contrato malformado; 401 sessão ausente/inválida; 403 ação negada quando existência pode ser revelada; 404 recurso não encontrado/não revelável; 409 revisão ou estado conflitante; 413 tamanho excedido; 415 formato; 422 regra/validação semântica; 429 limite; 503 dependência temporariamente indisponível. Envelope: error.code, message, correlationId e detalhes seguros. Nunca enviar stack/segredo ao usuário.

## Evolução

Broker dedicado, microserviços, troca de banco ou autenticação corporativa exigem novo ADR e escopo aprovado. Não antecipar otimização sem metas e medições. Estrutura fonte planejada em TASKS; nenhuma pasta de implementação é criada nesta entrega.

## Complemento de 01/10/2026

Decisões de 01/10/2026: Docker/WSL Ubuntu 24; America/Sao_Paulo para calendário; stack nas versões estáveis mais recentes compatíveis no início da implementação, a selecionar e fixar. Ver ADR-010 e PD-001/009/011. Não usar tags flutuantes como evidência de reprodução.

## Decisões posteriores PD-010
Prevalece a [consolidação ADR-011](../adr/ADR-011-consolidacao-pd-010.md) sobre os trechos anteriores sob revisão: sessões sem duração máxima/inatividade em todos os perfis; título 100–200; número institucional anual pelo ano da reunião; correção de e-mail da mesma identidade com bloqueio de colisão e revogação; distribuição de avisos aprovada; fim exclusivo dos prazos. Correção de data para outro ano ainda pendente. Estas são especificações, não evidências de implementação.
