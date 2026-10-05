# ADR-012 — Política de MFA interno

## Status
ACCEPTED para as decisões explícitas; procedimento excepcional de recuperação pendente.

## Contexto e alternativas
O método por e-mail já estava escolhido no ADR-010. Na análise PD-006, o usuário escolheu obrigatoriedade para Administradores e Organizadores em todo novo login, em vez de apenas Administradores ou uso opcional. Confirmou individualmente validade, tentativas, reenvio e política de recuperação.

## Decisão
MFA por código enviado por e-mail obrigatório para Administradores e Organizadores em todo novo login, após validar a senha. Sessões já conectadas não exigem novo código, conforme PD-010. Código válido por 10 minutos; 5 tentativas incorretas o invalidam; reenvio permitido após 60 segundos e invalida imediatamente o código anterior, com nova validade de 10 minutos. Perda de acesso ao e-mail: outro Administrador pode corrigir o endereço após verificar a identidade, com justificativa e auditoria. A correção revoga sessões e códigos anteriores; próximo login exige senha e MFA no novo e-mail. Se for o único Administrador, recuperação por procedimento operacional controlado, sem acesso alternativo que dispense MFA.

## Justificativa e consequências
Concretiza as respostas explícitas sem alterar a permanência das sessões aprovada na PD-010. O contrato de senha temporária dos Apreciadores é independente. Preservam-se os mecanismos de segurança existentes. Não se considera login concluído apenas pela senha quando MFA é obrigatório.

## Pendências
Responsável definido pelo usuário em 01/10/2026: a equipe de TI verifica a identidade e autoriza a recuperação do único Administrador, atuando nos arquivos de configuração do sistema. Permanecem justificativa, auditoria, revogação de sessões/códigos anteriores e novo login com senha e MFA. O procedimento técnico deve especificar como registrar a verificação da identidade, quais parâmetros de configuração permitem a recuperação e como aplicar a alteração de forma controlada, sem dispensar MFA. Planejar a tarefa específica e suas dependências antes da implementação; nenhuma implementação autorizada por esta decisão.
Esta decisão complementa ADR-009/010 e preserva o histórico. Não há implementação nem comprovação de testes.

## Rastreabilidade
PD-006, PD-010; RF-001; RN-021; RNF-001/004/005; UC-001; TASK-001/006/008/025. Tarefa de MFA ainda não criada: seu escopo será fechado após o complemento excepcional.


## Complemento explícito de 01/10/2026
A indicação da equipe de TI e dos arquivos de configuração resolve a escolha do responsável e do meio operacional de recuperação. Substitui a pendência anterior de responsável indefinido; o detalhamento técnico permanece para TASK-001, sem presumir um mecanismo de desativação do MFA.
