# ADR-011 — Consolidação das respostas da PD-010

## Status
ACCEPTED para as sete decisões explícitas registradas; PD-006/007/011 e outros complementos técnicos permanecem pendentes.

## Contexto e justificativa
Respostas diretas do usuário na análise da PD-010 em 01/10/2026. Complementa ADR-005/007/009/010 e substitui suas ressalvas de ambiguidade somente nos pontos respondidos. Preserva justificativas históricas.

## Consolidação PD-010 — respostas explícitas de 01/10/2026

As decisões abaixo substituem as descrições anteriores que as tratavam como ambíguas; não autorizam implementação.

- Sessões: Administradores, Organizadores e Apreciadores permanecem conectados até sair, sem expiração por inatividade ou duração máxima. Logout e revogação por segurança permanecem. Não se alteram as validades de senha temporária, ativação ou recuperação. Os antigos limites de sessão 8h/30min estão substituídos.
- Título: mínimo de 100 e máximo de 200 caracteres.
- Número: sequência única institucional, formato exemplificado por 0001/2026, reinício anual pelo ano em que a reunião ocorreu; número completo imutável e não reutilizável.
- Correção de e-mail após manifestação: somente para a mesma pessoa, preservando ID, autoria, manifestações e snapshots históricos. Colisão com e-mail de outra identidade bloqueia a correção, sem fusão. Correção válida invalida links e acessos anteriores da identidade e exige nova autenticação pelo e-mail corrigido. Não transfere manifestações para outra pessoa.
- Notificações: contas, unidades e configurações gerais notificam Administradores; reunião/processo notifica Administradores e Organizadores vinculados; eventos que afetem convite, acesso, documentos ou prazos notificam também Apreciadores afetados. Respeitar permissões e não revelar conteúdo restrito. Todos os eventos administrativos continuam sujeitos à notificação.
- Prazos de convites e manifestações: fim exclusivo; instante do servidor igual ao vencimento já impede aceitar/recusar convite e registrar/alterar manifestação, conforme o prazo. Preservada a regra de lembrete imediato às 23h quando o aceite for elegível.

### Complemento ainda necessário
A data da reunião é corrigível enquanto o processo está aberto, mas seu número incorpora o ano da ocorrência e é imutável. Decisão explícita posterior: se a correção mudar o ano, preservar o número original, mesmo que o ano exibido no número diverja da data corrigida. Não renumerar, não reutilizar e não transferir o número. A divergência deve permanecer visível e auditada. O catálogo concreto de eventos deverá ser conferido contra a distribuição aprovada antes do fechamento técnico da TASK-001.

PD-010: DEFINIDA quanto às sete decisões registradas, incluindo correção entre anos; TASK-001 permanece BLOCKED por PD-006/007/011 e contratos técnicos restantes.

## Rastreabilidade
RF-001/002/003/004/008/009/014; RN-001/009/019/020/021/022/023; RNF-001/003/004/010; TASK-001/006/007/009/014/016/018. Nenhum software ou teste executado.
