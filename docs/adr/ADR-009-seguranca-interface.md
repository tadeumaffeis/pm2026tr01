# ADR-009 — Segurança e interface verificáveis

## Status
ACCEPTED

## Contexto
Planejamento v1.0 aprovado explicitamente em 17/09/2026. Alternativas: interface desktop apenas; acessibilidade informal; tokens persistentes no navegador sem revogação.

## Problema
Sustentar o fluxo institucional auditável sem decisões de negócio implícitas ou complexidade operacional injustificada.

## Alternativas consideradas
Alternativas: interface desktop apenas; acessibilidade informal; tokens persistentes no navegador sem revogação.

## Decisão
Fluxo responsivo, WCAG 2.2 AA, matriz aprovada, Argon2id e sessões revogáveis; ativação 24h e reset 30min configuráveis.

## Justificativa
Atende uso móvel e reduz riscos de credenciais e controle de acesso.

## Consequências
Complementado pelo ADR-010: método de MFA por código de e-mail escolhido; perfis e parâmetros dependem de PD-006; sessões/inatividade sob revisão em PD-010; PDFs enviados têm política própria; matriz concreta PD-008.

## RF/RN/RNF/UC relacionados
Consultar matriz do README e catálogo reverso em TASKS.md. RF-001, RF-004, RF-006, RF-013; RN-019, RN-020, RN-021; RNF-004, RNF-005, RNF-007, RNF-008; UC-001, UC-004, UC-006, UC-013.
