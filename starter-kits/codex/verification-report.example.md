# Verification Report — Example

## Feature
`FEAT-001 Overdue Attention List`

## Acceptance Evidence

| AC | Evidence | Result |
| --- | --- | --- |
| AC1 active overdue visible | `AttentionPolicyTest.activeAfterDue` + API test | PASS |
| AC2 boundary semantics | `AttentionPolicyTest.atDueBoundary` | PASS |
| AC3 closed excluded | query integration test | PASS |
| AC4 scope protected | permission integration test | PASS |
| AC5 UI states | component/manual evidence | PASS / PARTIAL |

## Commands Run

```text
<project test command>
<project build/typecheck command>
<project lint command>
```

Record real command output/result; do not write “tests passed” if they were not executed.

## Negative Paths
- unauthorized user;
- closed item;
- no overdue data;
- API failure;
- time boundary.

## Not Verified
Example:

```text
E2E browser test not available in repository.
External notification intentionally out of scope.
```

## Risks / Review Focus
- verify query uses the same time semantics as domain policy;
- verify no frontend fallback re-implements overdue rule;
- inspect query plan if dataset is large.

## Completion Statement

Use one:

```text
VERIFIED — all required evidence executed and passed.
PARTIALLY VERIFIED — implementation complete, listed evidence unavailable.
BLOCKED — cannot verify because <reason>.
```

Never convert PARTIALLY VERIFIED into VERIFIED because the code “looks correct”.
