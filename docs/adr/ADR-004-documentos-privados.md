# ADR-004 — Documentos privados e composições imutáveis

## Status
ACCEPTED

## Contexto
Planejamento v1.0 aprovado explicitamente em 17/09/2026. Alternativas: binários no banco ou armazenamento público; anexos mudam a base consultada.

## Problema
Sustentar o fluxo institucional auditável sem decisões de negócio implícitas ou complexidade operacional injustificada.

## Alternativas consideradas
Alternativas: binários no banco ou armazenamento público; anexos mudam a base consultada.

## Decisão
Arquivos privados fora do banco; metadados/hashes no banco; composição versionada referenciada por manifestação.

## Justificativa
Preservar bytes e rastrear o conjunto exato da decisão.

## Consequências
Armazenamento depende de PD-001; recuperação exige banco e arquivos consistentes; referências impedem descarte indevido.

## RF/RN/RNF/UC relacionados
Consultar matriz do README e catálogo reverso em TASKS.md. RF-006, RF-011; RN-015, RN-016, RN-017; RNF-003, RNF-006; UC-006, UC-011.
