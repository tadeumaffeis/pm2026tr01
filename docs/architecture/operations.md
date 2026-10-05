# Operação, notificações e recuperação

## Ambientes e condições

Desenvolvimento/testes com dados sintéticos, MySQL e adaptadores locais. Homologação representativa sem expor dados reais sem autorização institucional. Produção somente após PD-001 a PD-009 aplicáveis resolvidas e checkpoint final. Infraestrutura não está configurada nesta entrega.

## E-mail e processamento

Graph com remetente institucional restrito. Credencial e permissões aprovadas pela TI; não solicitar acesso genérico a todas as caixas quando é possível restringir ao remetente. Resposta 202 do provedor indica aceitação, não entrega comprovada. Registrar tentativa e resultado sanitizado.

Catálogo mínimo confirmado: convite na publicação/inclusão elegível; senha temporária solicitada; ativação/reset interno; recuperação/reenvio de links; lembrete de convite e de manifestação; aviso de nova versão; aviso de mudança de anexos na reativação. Todos os eventos administrativos devem gerar notificação conforme decisão de 01/10/2026. Catálogo concreto e destinatários permanecem em PD-010; não inferir distribuição a todos os usuários.

Lembrete diário às 8h no fuso institucional; imediato após aceite entre 8h e 23h, incluindo exatamente 23h; fora da janela aguardar 8h seguinte. Cota por pendência/dia local: lembrete de convite e manifestação são pendências diferentes. Antes de enviar, revalidar ciclo ativo, convite/aceite e ausência de manifestação conforme tipo. Reinício não deve duplicar trabalho lógico; timeout de provedor pode tornar resultado incerto e deve ser exibido corretamente.

## Observabilidade

Logs estruturados com correlationId; métricas de erro, latência, fila pendente, idade do trabalho, falhas Graph e uso de armazenamento. Probes de liveness/readiness separados. Limites e destinatários de alerta operacionais em PD-001/002. Auditoria funcional não é log de depuração.

## Arquivo funcional

Pacote contém esquema/versionamento, metadados, ciclos, participantes, convites, manifestações, composições, arquivos e auditoria necessária. Manifesto relaciona conteúdo e hashes. Validar integridade e capacidade de recuperar antes de remover original. Recuperação separada, somente leitura por Administrador; nunca emitir links antigos nem executar trabalho contido no pacote.

Armazenamento interno e exportação externa devem ser suportados conforme contrato. Confirmação administrativa de cópia externa é registro de responsabilidade, não garantia técnica de permanência. Eliminação do pacote interno mantém auditoria mínima. Retenção do pacote externo depende da instituição.

## Backup operacional

Backup cobre banco, bytes, configurações e segredos recuperáveis por procedimento seguro; restauração mantém referências e integridade. Não confundir pacote de um processo com backup da aplicação. RPO/RTO, frequência e local das cópias pendentes. Executar ensaio antes da produção e guardar medidas; não declarar recuperável apenas porque backup foi criado.

## Runbooks planejados

Implantação limpa; bootstrap seguro; rotação de segredo; indisponibilidade de Graph; fila parada; arquivo inválido; restauração consistente; recuperação de acesso administrativo; retenção/remoção; rollback operacional. Escrever comandos reais somente quando ambiente estiver definido.

## Complemento de 01/10/2026

Ambiente escolhido: Docker em WSL com Ubuntu 24; produção, volumes persistentes, suporte e segredos ainda dependem de PD-001. Capacidade informada: um usuário (conta versus simultaneidade pendente). Fuso: America/Sao_Paulo. Retenção informada: 90 dias, com marcos e destinação em PD-003. Backup: valor de 7 dias ainda sem atribuição a frequência/RPO/RTO/retenção. Token Microsoft 365 fornecido pelo titular, com tipo, permissões, renovação e armazenamento pendentes. Nenhuma infraestrutura foi implantada.

## Decisões posteriores PD-010
Prevalece a [consolidação ADR-011](../adr/ADR-011-consolidacao-pd-010.md) sobre os trechos anteriores sob revisão: sessões sem duração máxima/inatividade em todos os perfis; título 100–200; número institucional anual pelo ano da reunião; correção de e-mail da mesma identidade com bloqueio de colisão e revogação; distribuição de avisos aprovada; fim exclusivo dos prazos; correção entre anos preserva o número original, com divergência visível e auditoria, sem renumeração. Estas são especificações, não evidências de implementação.

## Recuperação de MFA interno — decisão PD-006
MFA por código enviado por e-mail obrigatório para Administradores e Organizadores em todo novo login, após validar a senha. Sessões já conectadas não exigem novo código, conforme PD-010. Código válido por 10 minutos; 5 tentativas incorretas o invalidam; reenvio permitido após 60 segundos e invalida imediatamente o código anterior, com nova validade de 10 minutos. Perda de acesso ao e-mail: outro Administrador pode corrigir o endereço após verificar a identidade, com justificativa e auditoria. A correção revoga sessões e códigos anteriores; próximo login exige senha e MFA no novo e-mail. Se for o único Administrador, recuperação por procedimento operacional controlado, sem acesso alternativo que dispense MFA.
Responsável definido pelo usuário em 01/10/2026: a equipe de TI verifica a identidade e autoriza a recuperação do único Administrador, atuando nos arquivos de configuração do sistema. Permanecem justificativa, auditoria, revogação de sessões/códigos anteriores e novo login com senha e MFA. O procedimento técnico deve especificar como registrar a verificação da identidade, quais parâmetros de configuração permitem a recuperação e como aplicar a alteração de forma controlada, sem dispensar MFA. Planejar a tarefa específica e suas dependências antes da implementação; nenhuma implementação autorizada por esta decisão.
Ver [ADR-012](../adr/ADR-012-mfa-interno.md).

