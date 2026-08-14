# ADR-003 — Use a Relational Database for Core MVP Data

- Status: Proposed
- Date: 2026-08-15

## Context

FlowOps core data is structured and relational: Items, accountability, deadlines, progress records, lifecycle/closure evidence and audit context. Correctness and transactional consistency are more important than unproven extreme scale.

## Decision

Use one supported relational database as the primary persistence technology for MVP core data.

The exact vendor/product should follow organization constraints and team stack; this ADR decides the persistence model category, not a fashionable product.

## Alternatives

### Document database first
No current aggregate/document-shape Driver outweighs relational consistency/query needs.

### Multiple databases by module
Rejected for MVP because modules are not independently deployed services and distributed persistence adds unnecessary operational/transaction complexity.

### Elasticsearch as primary store
Rejected. Search/index technology may be added later as a derived projection if real search requirements justify it; it is not the core source of truth.

## Consequences

Positive:
- transactions；
- constraints/indexes；
- mature tooling；
- straightforward audit/query support。

Costs:
- schema migration discipline required；
- large analytical workloads may eventually need projections/warehouse/search technology。

## Guardrails

- database schema is not the domain model；
- modules do not gain permission to access all tables directly merely because they share a database；
- migrations are version controlled；
- no new datastore category without Driver + architecture review。

## Revisit Triggers

- search/analytics requirements exceed relational approach materially；
- module extraction creates independent persistence ownership；
- scale characteristics prove a specialized datastore is necessary。
