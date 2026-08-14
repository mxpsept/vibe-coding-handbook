# Stage 05 — AI Feature Delivery

## Loop
`Select story → Implementation Packet → repository inspection → plan → smallest vertical slice → tests → self-review → specialist review → PR/merge`.

Every task contains Goal, Read First, Scope, AC, architecture/design constraints, states, Reuse, Do Not, Stop Conditions and Verification.

Prefer thin end-to-end slices over building all controllers/services/pages separately. Avoid unrelated refactors; split large refactors from feature changes.

Agent rules: inspect before editing, reuse before inventing, explain dependencies, preserve ADRs, never silently close spec gaps, and report actual verification evidence.

Definition of Done is not compilation: AC, states, tests, architecture constraints and review evidence must be satisfied.