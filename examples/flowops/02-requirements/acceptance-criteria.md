# FlowOps — Acceptance Criteria v0.1

> 目标：让 Requirement 成为 Human、Coding Agent 和 Test Agent 共享的 Verification Contract。

## AC-US004 — Submit Progress

### AC-004-01 Valid progress update

```gherkin
Given an item is IN_PROGRESS
And the current actor is authorized to submit progress
When the actor submits a valid non-empty progress update
Then a new progress record is appended
And existing progress records remain unchanged
And Last Progress Update Time reflects the accepted record
And an audit event is recorded
```

### AC-004-02 Closed item rejects update

```gherkin
Given an item is CLOSED
When an actor attempts to submit a normal progress update
Then the operation is rejected
And no progress record is created
```

### AC-004-03 Unauthorized actor

```gherkin
Given an item is IN_PROGRESS
And the current actor does not have progress update permission
When the actor submits progress
Then access is denied
And no business data is changed
```

## AC-US006 — Deadline Attention

### AC-006-01 Overdue

```gherkin
Given Effective Due Date is 2026-09-30
And Lifecycle State is IN_PROGRESS
When the business date is 2026-10-01
Then OVERDUE attention is active
And Lifecycle State remains IN_PROGRESS
```

### AC-006-02 Closed item is not overdue

```gherkin
Given Effective Due Date is 2026-09-30
And Lifecycle State is CLOSED
When the business date is 2026-10-01
Then OVERDUE attention is not active
```

### AC-006-03 Near-due threshold unresolved

Cannot finalize until BR-006 threshold strategy is approved.

Status: `BLOCKED_BY_SPEC_GAP`.

## AC-US008 — Completion Claim

### AC-008-01 Valid claim

```gherkin
Given an item is IN_PROGRESS
And the actor has completion claim permission
And required completion information is valid
When the actor submits a completion claim
Then Lifecycle State becomes PENDING_CLOSURE
And the item does not become CLOSED
And claim actor and timestamp are recorded
And an audit event is recorded
```

### AC-008-02 100 percent does not auto-close

```gherkin
Given an item is IN_PROGRESS
And progress percentage is 100 if percentage is enabled
When no valid completion claim and closure approval have occurred
Then the item must not become CLOSED automatically
```

### AC-008-03 Duplicate completion claim

```gherkin
Given an item is PENDING_CLOSURE
When an actor attempts to submit another normal completion claim
Then the operation is rejected
```

## AC-US009 — Closure

### AC-009-01 Authorized closure

Blocked until Closure Authority is resolved. Expected semantic behavior:

```gherkin
Given an item is PENDING_CLOSURE
And the actor is an authorized Closure Authority
When the actor approves closure
Then Lifecycle State becomes CLOSED
And closure actor and timestamp are recorded
And an audit event is recorded
```

Status: `BLOCKED_BY_SPEC_GAP` for concrete permission implementation.

## AC-US005 — Stale Information

The semantic rule is accepted, but threshold is unresolved.

Important invariant:

```gherkin
Given an item has STALE_UPDATE attention
Then the system must not infer that the item is OVERDUE solely from STALE_UPDATE
And the system must not change Lifecycle State solely because of STALE_UPDATE
```

## Acceptance Quality Checklist

每个 Implementation-ready Story 至少检查：

- happy path；
- unauthorized path；
- invalid state；
- repeated action；
- terminal state；
- data history effect；
- audit effect；
- rule-specific boundary；
- unresolved SPEC_GAP。
