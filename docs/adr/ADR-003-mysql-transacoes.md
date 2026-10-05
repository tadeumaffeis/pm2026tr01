# ADR-003 — MySQL/InnoDB e invariantes transacionais

## Status
ACCEPTED

## Contexto
Planejamento v1.0 aprovado explicitamente em 17/09/2026. Alternativas: MongoDB ou outro banco relacional; domínio possui relacionamentos e operações coordenadas.

## Problema
Sustentar o fluxo institucional auditável sem decisões de negócio implícitas ou complexidade operacional injustificada.

## Alternativas consideradas
Alternativas: MongoDB ou outro banco relacional; domínio possui relacionamentos e operações coordenadas.

## Decisão
MySQL/InnoDB; controle concorrente e restrições para publicação, participação e encerramento.

## Justificativa
Consistência entre decisão vigente, participantes e encerramento é central.

## Consequências
Escolher driver/migrações em PD-011; testar com banco real, não apenas mocks.

## RF/RN/RNF/UC relacionados
Consultar matriz do README e catálogo reverso em TASKS.md. RF-003, RF-007, RF-009, RF-012; RN-003, RN-007, RN-013, RN-014; RNF-002; UC-003, UC-007, UC-009, UC-012.
