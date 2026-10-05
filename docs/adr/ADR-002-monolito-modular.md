# ADR-002 — Monólito modular com NestJS

## Status
ACCEPTED

## Contexto
Planejamento v1.0 aprovado explicitamente em 17/09/2026. Alternativas: backend mínimo com organização manual; microsserviços com operação distribuída.

## Problema
Sustentar o fluxo institucional auditável sem decisões de negócio implícitas ou complexidade operacional injustificada.

## Alternativas consideradas
Alternativas: backend mínimo com organização manual; microsserviços com operação distribuída.

## Decisão
NestJS modular, React/Material UI, API HTTP/JSON; trabalhador do mesmo produto em processo separado.

## Justificativa
Separação de responsabilidades com transações locais e menor custo operacional inicial.

## Consequências
Fronteiras explícitas; escalar API/trabalhador conforme necessidade; não criar serviços independentes sem evidência.

## RF/RN/RNF/UC relacionados
Consultar matriz do README e catálogo reverso em TASKS.md. RF-001 a RF-018; RNF-014, RNF-016; UC-001 a UC-018.
