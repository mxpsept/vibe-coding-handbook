# FlowOps — Quality Attributes v0.1

## Why

“高性能、高可用、安全、可扩展”不是可执行架构要求。Quality Attribute 应尽量描述 Scenario 和 Trade-off。

## QA-001 — Business Correctness

**Priority:** Critical

Scenario:

```text
Given an item is IN_PROGRESS
When an authorized participant submits a Completion Claim
Then the system must not mark it CLOSED automatically
And the transition/evidence must be auditable
```

Architecture impact:
- domain action endpoint；
- transition validation server-side；
- tests around state transitions。

## QA-002 — Authorization

**Priority:** Critical

```text
A user must not perform an action merely because the frontend exposes/calls the endpoint.
```

Architecture impact:
- server authorization；
- permission model；
- scoped queries；
- security tests。

## QA-003 — Auditability

**Priority:** High

For key lifecycle-changing actions, authorized auditors/operators can determine:

```text
who
did what
on which item
when
with relevant semantic context
```

Audit evidence must survive ordinary UI changes.

## QA-004 — Maintainability / AI Coherence

**Priority:** High

Scenario:

```text
A new feature is implemented by a Coding Agent.
It should be possible to identify the owning module, allowed dependencies, API conventions and test location without inventing a new project structure.
```

Fitness candidates:
- module dependency rules；
- naming conventions；
- architecture tests；
- PR checklist。

## QA-005 — Performance

**Priority:** Medium until scale confirmed

Initial UX target candidate, not final SLA:
- common list/detail interactions should feel responsive under expected enterprise load；
- large result sets must use bounded queries/pagination strategy。

Exact p95/p99 targets require ARCH_GAP-003 scale data before becoming contractual.

## QA-006 — Availability

**Priority:** Medium/High

MVP should tolerate ordinary application restart/deployment without data corruption. Exact uptime SLA is not yet defined.

Do not infer multi-region architecture without an availability Driver.

## QA-007 — Observability

**Priority:** High

Production support must distinguish:

```text
request failure
business validation rejection
authorization rejection
database/infrastructure failure
```

and correlate a user-visible failure with server logs/trace context.

## QA-008 — Security

**Priority:** High

- HTTPS in deployed environment；
- secrets outside source code；
- input validation；
- authorization at server；
- dependency vulnerability process；
- audit of sensitive actions。

Detailed threat model follows Security Architecture.

## QA-009 — Evolvability

**Priority:** High

Architecture should permit future integrations such as SSO/organization directory/notification without forcing core domain code to depend directly on vendor SDKs.

Use explicit ports/adapters or integration boundaries where justified.

## Trade-off Order

When choices conflict, MVP default priority:

```text
Business correctness
> Security / authorization
> Auditability
> Maintainability
> Delivery speed
> Performance optimization beyond proven need
> architectural novelty
```

This order is a teaching-case decision and should be revisited when real project drivers differ.
