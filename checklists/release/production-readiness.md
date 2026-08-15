# Production Readiness Gate

## Product
- [ ] Acceptance Criteria verified
- [ ] critical UX states covered
- [ ] operational/business owner known

## Architecture / Data
- [ ] migrations reviewed and reversible/recoverable
- [ ] compatibility considered
- [ ] capacity/performance assumptions validated
- [ ] failure modes understood

## Security
- [ ] auth/authz verified
- [ ] sensitive data handling reviewed
- [ ] secrets/config managed outside code
- [ ] privileged actions audited where required
- [ ] dependency/security checks completed

## Quality
- [ ] build/lint/typecheck pass
- [ ] required automated tests pass
- [ ] critical regression paths pass
- [ ] known gaps have explicit accepted risk

## Operations
- [ ] health/readiness signals available
- [ ] logs/metrics/traces sufficient for critical flow
- [ ] alert ownership defined
- [ ] runbook exists for material failure modes
- [ ] rollback/recovery procedure known

## Release
- [ ] version/artifact identifiable
- [ ] config/environment diff reviewed
- [ ] migration order defined
- [ ] smoke test defined
- [ ] rollback trigger defined
- [ ] responsible release owner known

## AI-specific
- [ ] generated changes received normal review standard
- [ ] Agent did not introduce unapproved dependency/architecture
- [ ] verification claims have actual command/evidence
- [ ] unresolved SPEC/ARCH/DESIGN gaps are not hidden

## Decision

```text
READY
READY_WITH_ACCEPTED_RISK
HOLD
```
