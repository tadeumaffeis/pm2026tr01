# ADR-006 — Fila transacional e Microsoft Graph

## Status
ACCEPTED

## Contexto
Planejamento v1.0 aprovado explicitamente em 17/09/2026. Alternativas: envio síncrono ou broker dedicado.

## Problema
Sustentar o fluxo institucional auditável sem decisões de negócio implícitas ou complexidade operacional injustificada.

## Alternativas consideradas
Alternativas: envio síncrono ou broker dedicado.

## Decisão
Persistir intenção com a operação; trabalhador com retentativas e Graph; fila inicial no banco.

## Justificativa
Falha de e-mail não pode desfazer ou perder silenciosamente uma operação já confirmada.

## Consequências
Entrega externa não é exatamente uma vez; resultado incerto e duplicação potencial devem ser tratados; Graph depende de PD-005.

## RF/RN/RNF/UC relacionados
Consultar matriz do README e catálogo reverso em TASKS.md. RF-014; RN-022; RNF-009, RNF-011; UC-014.
