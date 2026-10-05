# ADR-007 — Relógio do servidor e estados separados

## Status
ACCEPTED

## Contexto
Planejamento v1.0 aprovado explicitamente em 17/09/2026. Alternativas: depender apenas de agendador ou usar único estado para processo/ciclo.

## Problema
Sustentar o fluxo institucional auditável sem decisões de negócio implícitas ou complexidade operacional injustificada.

## Alternativas consideradas
Alternativas: depender apenas de agendador ou usar único estado para processo/ciclo.

## Decisão
Processo, ciclo, convite e vínculo distintos; prazos no servidor e saldos congelados em suspensão.

## Justificativa
Evita aceitar operações vencidas e confundir substituição com encerramento definitivo.

## Consequências
Agendador materializa eventos; operação revalida prazo mesmo se agendador atrasar; fuso America/Sao_Paulo decidido em 01/10/2026 (PD-009; complemento no ADR-010).

## RF/RN/RNF/UC relacionados
Consultar matriz do README e catálogo reverso em TASKS.md. RF-010, RF-012; RN-007, RN-009, RN-010, RN-011, RN-014; RNF-002, RNF-010; UC-010, UC-012.
