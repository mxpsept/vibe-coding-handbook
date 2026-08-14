# FlowOps — Data Model v0.1

## Principles
`Database schema != Domain Model`; evidence/history is append-oriented; migrations are version controlled.

## Candidate Tables
`supervision_item`, `progress_record`, `completion_claim`, `closure_decision`, `audit_evidence`.

`supervision_item` owns lifecycle/accountability/deadline/version facts. Never store `OVERDUE` as lifecycle. `progress_record` preserves historical reports rather than replacing them with one latest-progress field. Completion claims and closure decisions remain separate records.

Attention should initially be calculated/query-derived; add a persisted projection only when scale/SLA proves the need.

Indexes follow real query patterns. Schema changes require migrations; destructive changes require explicit review. Shared database does not permit cross-module access to every table.