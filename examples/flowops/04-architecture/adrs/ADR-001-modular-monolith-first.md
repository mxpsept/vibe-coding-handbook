# ADR-001 — Start FlowOps as a Modular Monolith

- Status: Proposed
- Date: 2026-08-15
- Owners: Architecture / Engineering

## Context

FlowOps MVP contains several business capabilities but currently has no validated requirement for independent service scaling, independent deployment, multi-region isolation or separate team ownership that would justify distributed services.

The project values business correctness, auditability, maintainability and rapid delivery.

AI-assisted implementation increases the cost of ambiguous boundaries: without an explicit architecture, agents may create cross-module coupling even inside one codebase.

## Decision

Start FlowOps backend as a **modular monolith**:

```text
one deployable backend
one primary relational database boundary initially
explicit business modules
controlled module dependencies
module internals not accessed directly by unrelated modules
```

Modules collaborate through approved application/domain contracts rather than arbitrary repository access.

## Not Chosen

### Microservices from day one
Rejected for MVP because current Drivers do not justify:
- distributed transactions；
- service discovery/network failure modes；
- multiple deployments；
- cross-service observability overhead；
- contract/version management overhead。

### Unstructured layered monolith

```text
controller/
service/
repository/
```

for the entire application without feature/domain boundaries is also rejected because it makes ownership and dependency rules difficult to preserve as AI-generated code grows.

## Consequences

### Positive
- simpler deployment/testing；
- local transactions；
- explicit domain boundaries；
- easier repository navigation for humans/agents；
- future extraction remains possible if real Drivers appear。

### Negative
- module discipline must be enforced inside one process；
- shared database can tempt direct cross-module table access；
- independent scaling is not available without later extraction。

## Guardrails

Coding Agent must not:
- create a new deployable service for a feature without ADR review；
- access another module's internal repository merely for convenience；
- introduce MQ/service discovery because “microservices best practice”；
- treat modular monolith as a single global service package。

## Revisit Triggers

Reconsider when evidence shows:
- materially different scaling needs；
- independent deployment cadence/team ownership；
- isolation/compliance boundary；
- availability boundary；
- integration load that should be independently isolated。

Until a trigger exists, “microservices are more scalable” is not sufficient reason to reverse this ADR.
