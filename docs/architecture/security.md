# Segurança e privacidade

## Identidade e autorização

Contas internas locais e identidades de apreciador são contextos distintos mesmo com mesmo e-mail; não fundir privilégios. Identidade de apreciador é única por normalização aprovada. Sessão global não concede acesso sem vínculo ativo; autorizações verificadas a cada operação e download. Primeiro Administrador ativado por procedimento controlado, nunca senha padrão.

Sessões opacas revogáveis; cookie Secure/HttpOnly/SameSite apropriado; proteção CSRF em mutações autenticadas por cookie; HTTPS. Não guardar token de sessão em localStorage. Password hashing interno Argon2id com parâmetros revistos no ambiente. Ativação 24h e reset 30min, uso único e configuráveis. A retirada de sessões/inatividade solicitada em 01/10/2026 está registrada em PD-010; esclarecer alcance antes da implementação. Limites anteriores de 8h/30min ficam sob revisão; login, autorização e revogação não são removidos por inferência.

Senha temporária de validação: 10min, 5 tentativas, 60s entre emissões, uso único. Usar aleatoriedade segura; proteger digest de segredo curto com chave do servidor e limites por identidade/origem. Nunca salvar segredo claro em logs. Se outbox precisar transportar credencial temporária, criptografar payload, restringir acesso e remover segredo após fim da utilidade; definir solução em TASK-001. Expiração não congela por suspensão.

Link de acesso: token de alta entropia por vínculo; persistir hash; ocultar em logs e cabeçalhos de referência; não incluir em analytics. Revogação por encerramento do vínculo/processo. Não é autenticação inequívoca. Recusa sem sessão é regra aprovada, só por POST e confirmação explícita; jamais em clique automático de scanner de e-mail via GET. Auditoria registra que houve posse do link, não senha validada.

## Dados e arquivos

Storage privado; validação real e verificação de segurança; PDF de ata sem senha. Não expor URLs permanentes públicas. Isolar temporários e validar pacotes externos com limites contra extração excessiva e caminhos fora do destino. Criptografia em trânsito; proteção em repouso e gestão de chaves conforme ambiente PD-001. Segredos fora de código/fixtures; acesso mínimo do trabalhador e da conta Graph.

Autorização vigente governa histórico, não modifica registro original. Dados próprios ocultos só sessão do autor; informações administrativas nunca para apreciadores. Logs técnicos minimizados; auditoria funcional protegida. Não presumir retenção infinita, conformidade legal ou disponibilidade pública.

## MFA e decisões institucionais

MFA por código enviado por e-mail obrigatório para Administradores e Organizadores em todo novo login, após validar a senha. Sessões já conectadas não exigem novo código, conforme PD-010. Código válido por 10 minutos; 5 tentativas incorretas o invalidam; reenvio permitido após 60 segundos e invalida imediatamente o código anterior, com nova validade de 10 minutos. Perda de acesso ao e-mail: outro Administrador pode corrigir o endereço após verificar a identidade, com justificativa e auditoria. A correção revoga sessões e códigos anteriores; próximo login exige senha e MFA no novo e-mail. Se for o único Administrador, recuperação por procedimento operacional controlado, sem acesso alternativo que dispense MFA. Responsável definido pelo usuário em 01/10/2026: a equipe de TI verifica a identidade e autoriza a recuperação do único Administrador, atuando nos arquivos de configuração do sistema. Permanecem justificativa, auditoria, revogação de sessões/códigos anteriores e novo login com senha e MFA. O procedimento técnico deve especificar como registrar a verificação da identidade, quais parâmetros de configuração permitem a recuperação e como aplicar a alteração de forma controlada, sem dispensar MFA. Planejar a tarefa específica e suas dependências antes da implementação; nenhuma implementação autorizada por esta decisão. Ver [ADR-012](../adr/ADR-012-mfa-interno.md). Política de senha interna, limites de tentativas e incidentes definida tecnicamente em TASK-001, com aprovação institucional quando exigida.

## Verificações obrigatórias

- Acesso cruzado de processos, papéis e autores; usuário removido com sessão ainda válida.
- Vazamento por erro, paginação, arquivo, relatório e recuperação pública.
- CSRF, XSS por textos, injeção SQL/CSV, upload hostil e importação de pacote.
- Reutilização/concorrência de senha temporária e token de reset.
- Revogação de Organizador ao arquivar; bloqueio de apreciador em suspensão/encerramento.
- Segredos em logs, URLs, telemetria ou histórico técnico.

Achados e evidências em docs/verification apenas quando executados. Nunca declarar PASS por análise documental.

## Decisões posteriores PD-010
Prevalece a [consolidação ADR-011](../adr/ADR-011-consolidacao-pd-010.md) sobre os trechos anteriores sob revisão: sessões sem duração máxima/inatividade em todos os perfis; título 100–200; número institucional anual pelo ano da reunião; correção de e-mail da mesma identidade com bloqueio de colisão e revogação; distribuição de avisos aprovada; fim exclusivo dos prazos. Correção de data para outro ano ainda pendente. Estas são especificações, não evidências de implementação.


