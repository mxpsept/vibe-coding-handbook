# Implementation Packet — Example

## Feature
`FEAT-001 Overdue Attention List`

## Goal
Show authorized users active items that are overdue according to the approved domain rule.

## Read First
- `docs/features/FEAT-001/feature-spec.md`
- `docs/architecture/architecture-context.md`
- existing item query/service tests

## Approved Facts
- `OVERDUE` is an attention reason, not lifecycle status.
- Closed/cancelled items do not appear as active overdue attention.
- Server owns permission/data-scope enforcement.

## Acceptance Criteria
- AC1: active item after due time appears in overdue query.
- AC2: item before/equal approved due boundary follows specified comparison rule.
- AC3: closed item does not appear.
- AC4: unauthorized scope does not leak data.
- AC5: UI renders loading/empty/error/data states.

## Scope
- attention query/application path;
- API response required by workspace;
- workspace rendering;
- relevant tests.

## Non-goals
- notification sending;
- changing lifecycle model;
- redesigning global table component;
- new scheduler/cache/search infrastructure.

## Constraints
- reuse existing Clock/date abstraction if present;
- reuse existing authorization policy;
- do not calculate authorization in UI;
- do not invent escalation threshold.

## Reconnaissance Questions
Before editing, report:
1. owning modules;
2. similar query patterns;
3. permission mechanism;
4. existing test fixtures;
5. potential conflicts with this packet.

## Stop Conditions
Stop and report if:
- approved overdue boundary is absent/contradictory;
- permission scope cannot be determined;
- required change crosses an unapproved module boundary;
- migration/new infrastructure is required;
- repository evidence contradicts an Approved Fact.

## Verification
Expected minimum:
```text
rule/unit tests
permission integration test
API/application test
UI state tests where project supports them
build/typecheck/lint
```

## Completion Evidence
Map each AC to test/manual evidence and list anything not verified.
