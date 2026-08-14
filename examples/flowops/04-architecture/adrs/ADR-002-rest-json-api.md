# ADR-002 — Use REST/JSON as the MVP Application API

- Status: Proposed
- Date: 2026-08-15

## Context

FlowOps is initially a browser-based enterprise application. MVP interactions are request/response oriented and no validated Driver currently requires GraphQL, bidirectional streaming or event-driven client APIs.

## Decision

Use HTTPS REST/JSON for the primary frontend-backend application API.

Design endpoints around resources and meaningful domain actions, not database CRUD alone.

Examples:

```text
GET  /items/{id}
GET  /items
POST /items
POST /items/{id}/progress-updates
POST /items/{id}/completion-claims
POST /items/{id}/closure
```

Exact paths remain API design work; examples communicate intent.

## Alternatives

### GraphQL
Not selected because current UI does not demonstrate query-shape complexity sufficient to justify schema/resolver/tooling overhead.

### Generic CRUD API
Rejected because `PUT status=CLOSED` hides lifecycle semantics and authorization/business transition rules.

### WebSocket-first
No real-time collaboration/streaming Driver yet.

## Consequences

Positive:
- familiar enterprise tooling；
- straightforward HTTP semantics/testing；
- OpenAPI candidate；
- easy observability and integration。

Costs:
- endpoint evolution/versioning discipline needed；
- complex aggregated views may require purpose-built query endpoints/read models。

## Guardrails

- API must not expose persistence entities directly by default；
- domain actions should not be modeled as arbitrary field mutation；
- error envelope must be consistent；
- authorization remains server-side；
- adding GraphQL/WebSocket requires a demonstrated Driver and ADR review。

## Revisit Triggers

- validated high-frequency realtime collaboration；
- client query flexibility causing material endpoint explosion；
- external integration contract requires another protocol。
