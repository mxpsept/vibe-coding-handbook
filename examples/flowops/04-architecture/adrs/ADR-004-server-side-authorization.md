# ADR-004 — Server-side Authorization Is the Security Source of Truth

- Status: Proposed
- Date: 2026-08-15

## Context

FlowOps UI varies actions and data by role/scope. Browser code is controlled by the client and cannot enforce security. AI-generated frontend code may easily confuse hidden buttons with authorization unless the boundary is explicit.

## Decision

All protected reads and business actions are authorized on the backend.

Frontend permission logic is used for user experience only:

```text
Frontend
→ hide/disable/explain based on known capability

Backend
→ authenticate
→ authorize scope/action
→ validate business state
→ execute or reject
```

## Scope

Must cover at least:
- item read scope；
- create/edit/issue；
- progress update；
- completion claim；
- closure；
- management/audit views where restricted。

## Alternatives

### Frontend-only permissions
Rejected: trivially bypassable and unsafe.

### Role-name checks scattered in controllers
Rejected as primary model because policy becomes duplicated and hard to evolve/test.

## Consequences

Positive:
- reliable security boundary；
- API safe for multiple clients；
- centralized/testable policy semantics。

Costs:
- frontend and backend capability presentation need coordination；
- scoped queries must prevent data leakage, not only action endpoints。

## Guardrails

Coding Agent must not:
- rely on route guards/button hiding as security；
- trust actor/user IDs supplied by client when identity should come from authenticated context；
- duplicate arbitrary role-name conditions across features；
- return protected entity data then merely hide fields in UI。

## Verification

- authorization unit/policy tests；
- API integration tests for forbidden actors/scopes；
- query scope tests；
- security review for new privileged actions。

## Revisit

The implementation mechanism may change with enterprise IAM/SSO, but the server-side source-of-truth principle remains unless the system trust model fundamentally changes.
