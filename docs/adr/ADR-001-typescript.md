# ADR-001 — TypeScript em frontend e backend

## Status
ACCEPTED

## Contexto
Planejamento v1.0 aprovado explicitamente em 17/09/2026. JavaScript permitiria execução com menor configuração; TypeScript permite verificar contratos antes da execução.

## Problema
Sustentar o fluxo institucional auditável sem decisões de negócio implícitas ou complexidade operacional injustificada.

## Alternativas consideradas
JavaScript permitiria execução com menor configuração; TypeScript permite verificar contratos antes da execução.

## Decisão
TypeScript com verificação estrita; validação de entradas também em execução.

## Justificativa
Estados e contratos complexos justificam a verificação estática.

## Consequências
Build/verificação de tipos obrigatórios; não elimina testes ou validação de dados.

## RF/RN/RNF/UC relacionados
Consultar matriz do README e catálogo reverso em TASKS.md. RNF-014, RNF-016; todos os contratos RF-001 a RF-018.
