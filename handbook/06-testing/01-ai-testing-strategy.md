# Stage 06 — Testing & Quality Engineering

AI makes generating tests cheap; the hard part is testing the right contracts.

Use domain-rule, application, API-contract, persistence/integration, frontend component, critical E2E, architecture, visual/accessibility tests.

Prioritize lifecycle transitions, authorization/scope leakage, time boundaries, concurrency, audit evidence and destructive actions. For every critical happy path ask: unauthorized, invalid state, stale version, dependency failure, duplicate submit, empty/long data?

Reject tests that merely assert mocks, duplicate implementation logic, or create brittle snapshots without decision value. CI must produce reproducible evidence.