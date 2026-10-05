# Estratégia e catálogo de testes planejados

Nenhum teste de software foi executado nesta etapa. Identificadores TEST são cenários planejados, não arquivos existentes. Cada grupo deve conter positivos e negativos significativos; não espelhar apenas implementação.

| Teste | RF/RN/UC | Cenários mínimos | Tarefa |
|---|---|---|---|
| TEST-001 | RF-001; RN-002, RN-021; UC-001 | Último Administrador protegido; redefinição revoga sessões; conta desativada não reativa por recuperação. | TASK-006 |
| TEST-002 | RF-002; RN-002, RN-023; UC-002 | Campos obrigatórios validados; sigla única; unidade inativa não aceita novos vínculos; correção após publicação tem justificativa. | TASK-009 |
| TEST-003 | RF-003; RN-001, RN-005, RN-006, RN-007, RN-008; UC-003 | Recusa não contornável; composição congelada imutável; remoção revoga apenas autorização correspondente. | TASK-014 |
| TEST-004 | RF-004; RN-001, RN-019, RN-020; UC-004 | 10min/5 tentativas/60s aplicados; contrato de duração/inatividade da sessão bloqueado até esclarecer PD-010; recuperação não altera participação nem expõe links na página. | TASK-007 |
| TEST-005 | RF-005; RN-003, RN-004, RN-014, RN-025; UC-005 | Upload não publica; só um rascunho; descarte não remove arquivos publicados. | TASK-012 |
| TEST-006 | RF-006; RN-015, RN-017, RN-025; UC-006 | Conteúdo e extensão verificados; PDF com senha rejeitado; limites novos não invalidam arquivos existentes. | TASK-011 |
| TEST-007 | RF-007; RN-003, RN-004, RN-005, RN-009, RN-014, RN-016; UC-007 | Sem dois ciclos correntes; rollback integral em falha; novo ciclo exige novos aceites, preservando links ativos. | TASK-013 |
| TEST-008 | RF-008; RN-005, RN-006, RN-007, RN-019, RN-020; UC-008 | Aceite autenticado; recusa explícita sem sessão; prazo/estado impedem resposta inválida; recusa definitiva. | TASK-014 |
| TEST-009 | RF-009; RN-012, RN-013, RN-016, RN-019; UC-009 | Texto exigido nas três decisões; versão e composição registradas; autorização e prazo revalidados ao persistir. | TASK-016 |
| TEST-010 | RF-010; RN-007, RN-009, RN-010, RN-011; UC-010 | Congelar somente prazos abertos; não reabrir convites; vencimento suspende mesmo com unanimidade. | TASK-017 |
| TEST-011 | RF-011; RN-015, RN-016; UC-011 | Ciclo publicado só altera suspenso e sem manifestações; caso contrário exige nova versão/ciclo. | TASK-017 |
| TEST-012 | RF-012; RN-003, RN-013, RN-014, RN-025; UC-012 | Sucesso exige ciclo ativo e unanimidade na transação; insucesso justificado; processo não reabre; links invalidados no encerramento definitivo. | TASK-016 |
| TEST-013 | RF-013; RN-018, RN-019, RN-023, RN-024; UC-013 | Histórico antigo só por participação aceita no ciclo ativo e configuração; conteúdo individual oculto só ao autor autenticado; estados bloqueadores prevalecem. | TASK-019 |
| TEST-014 | RF-014; RN-004, RN-011, RN-016, RN-022; UC-014 | 8h e janela 8h–23h (23h incluído) respeitadas; interrupção de pendências; não afirmar entrega apenas por aceitação do provedor. | TASK-018 |
| TEST-015 | RF-015; RN-012, RN-013, RN-014, RN-023, RN-024; UC-015 | CSV filtra criação/situação/Organizador; aprovação contém ressalvas vigentes; distinguir unanimidade de oficialização. | TASK-021 |
| TEST-016 | RF-016; RN-024, RN-025; UC-016 | Arquivar revoga acesso de Organizadores; recuperação nunca reabre; remoção exige verificação; exclusão interna exige confirmação externa e auditoria. | TASK-022 |
| TEST-017 | RF-017; RN-017, RN-020, RN-021, RN-022; UC-017 | Exceção por reunião justificada; teto técnico respeitado; mudanças registradas e não retroativas. Parâmetros operacionais protegidos definidos no contrato. | TASK-009 |
| TEST-018 | RF-018; RN-001, RN-008, RN-012, RN-014, RN-016, RN-023, RN-024, RN-025; UC-018 | Operações mutáveis relevantes auditadas; logs técnicos sem segredos; histórico não editável por operações comuns. | TASK-019 |

## Suítes transversais

| Suíte | RNFs | Evidência esperada | Tarefas |
|---|---|---|---|
| TEST-X01 concorrência | RNF-002, RNF-003 | Publicar duas vezes; encerrar vs alterar decisão; aceitar vs fechar prazo; nunca sucesso inválido | TASK-013, TASK-014, TASK-016, TASK-017 |
| TEST-X02 temporal | RNF-010 | Relógio controlado; antes/no/depois do limite; suspensão; reativação; atraso de agendador | TASK-017, TASK-018 |
| TEST-X03 segurança | RNF-001, RNF-004, RNF-005, RNF-006, RNF-015 | Acesso cruzado, sessão de outro autor, token reutilizado, logs limpos, upload/importação hostil | TASK-008, TASK-023 |
| TEST-X04 interface | RNF-007, RNF-008 | Teclado, celular, leitor de tela, navegadores e fluxo completo | TASK-023, TASK-024 |
| TEST-X05 e-mail | RNF-009, RNF-011 | Reinício, indisponibilidade, resultado incerto, deduplicação e cancelamento de pendência | TASK-018 |
| TEST-X06 recuperação | RNF-003, RNF-012, RNF-015 | Round-trip de pacote e restauração operacional; hashes e permissões | TASK-022, TASK-027 |
| TEST-X07 carga | RNF-013 | Medidas contra metas PD-002 aprovadas | TASK-026 |
| TEST-X08 engenharia/operação | RNF-014, RNF-016, RNF-011 | Build/lint/tipos, instalação limpa, configuração externa, probes | TASK-002, TASK-025 |

## Fluxos E2E obrigatórios

1. Administrador ativa conta, cadastra unidade/reunião; Organizador prepara e publica; apreciador aceita e aprova; fecha convite; encerramento formal bem-sucedido.
2. Dez convidados, dois aceitam/aprovam; antes do fechamento sem unanimidade; depois conjunto de dois elegíveis; zero aceites nunca sucesso.
3. Recusa definitiva; remoção/reinclusão não contorna; ciclo seguinte permite decisão nova.
4. Aprovação com ressalvas e reprovação; alteração gera história e muda unanimidade; documento exato preservado.
5. Suspensão congela convite, bloqueia consulta, para lembretes; reativação retoma; vencimento da manifestação exige novo prazo.
6. Anexo em ciclo ativo rejeitado; suspenso sem manifestações pode mudar; com qualquer manifestação exige novo ciclo.
7. Encerrar ciclo sem sucesso deixa processo aberto sem consulta de apreciador; nova publicação usa mesmo link; encerrar processo invalida links.
8. Arquivar tira acesso de Organizador; importar pacote recupera somente consulta de Administrador; remoção mantém auditoria mínima.

## Evidência

Registrar ambiente, versões, comando, resultado, data e limitações no relatório da TASK. Relatórios PDF exigem inspeção visual. Acessibilidade não é comprovada apenas por ferramenta automática. Testes de carga sem metas não autorizam produção. Nenhum gate obrigatório com falha pode ser marcado DONE.

## Complemento de 01/10/2026

Revisão 01/10/2026: acrescentar casos de texto com 1.000/1.001 caracteres, aceite exatamente às 23h e imediatamente após, calendário America/Sao_Paulo e ausência de campos adicionais. Casos de MFA, sessão/inatividade, título, correção de e-mail e destinatários dependem de PD-006/010. Retenção de 90 dias e backup de 7 dias não autorizam testes com política de exclusão ou frequência presumida. Nenhum teste de software executado.

## Decisões posteriores PD-010
Prevalece a [consolidação ADR-011](../adr/ADR-011-consolidacao-pd-010.md) sobre os trechos anteriores sob revisão: sessões sem duração máxima/inatividade em todos os perfis; título 100–200; número institucional anual pelo ano da reunião; correção de e-mail da mesma identidade com bloqueio de colisão e revogação; distribuição de avisos aprovada; fim exclusivo dos prazos; correção entre anos preserva o número original, com divergência visível e auditoria, sem renumeração. Estas são especificações, não evidências de implementação.

## Cenários aprovados PD-006 (ainda não executados)
Validar MFA obrigatório em novo login para ambos os perfis; ausência de nova solicitação em sessão já conectada; validade de 10 minutos; invalidação após 5 erros; reenvio após 60 segundos invalidando código anterior; correção de e-mail com verificação, justificativa, auditoria e revogação; próximo login com senha e MFA. Recuperação do único Administrador requer procedimento a detalhar. Ver ADR-012; nenhum PASS de software atribuído.
