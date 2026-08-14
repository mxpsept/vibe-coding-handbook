# Stage 09 — Continuous Evolution

Production feedback must update source-of-truth artifacts, not only code: `feedback/incident → classify → Requirement/Architecture change → ADR/Spec → implementation → tests → release`.

Track product/spec, design-system, architecture, code, test and operational debt separately.

For AI refactoring, state the invariant and measurable goal, protect behavior with tests first, and separate refactor from feature changes where practical.

Reopen ADRs only when documented triggers occur; supersede instead of rewriting history. Periodically remove stale prompts and contradictory docs. A fresh Agent session should be able to identify the current source of truth.