# FlowOps — Domain Model v0.1

## Core Concepts
`SupervisionItem`, `ProgressRecord`, `CompletionClaim`, `ClosureDecision`, derived `AttentionFlag`, and `AuditEvidence`.

## Invariants
- Lifecycle remains the Requirements source of truth.
- `Lifecycle != Attention`.
- `Completion Claim != Closure`.
- Progress history is append-oriented evidence.
- Lifecycle-changing commands validate current state and authorization.
- Do not split one atomic invariant across modules for diagram symmetry.

## Attention
Attention is derived from business facts such as lifecycle, effective deadline and latest progress time. It must remain explainable; `STALE_UPDATE` means no new progress information, not proven execution stagnation.

## Concurrency
Use optimistic concurrency/version checks where stale writes could violate lifecycle correctness; expose a conflict rather than silently overwriting.

## Test Focus
Valid/invalid transitions, completion claim semantics, deadline boundaries, attention time boundaries, and concurrent lifecycle commands.