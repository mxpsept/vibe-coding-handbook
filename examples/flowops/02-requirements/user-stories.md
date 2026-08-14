# FlowOps — User Stories v0.1

> User Story 用来表达角色价值，不单独承担完整 Specification。

## Epic A — Establish Work

### US-001 Create supervision item
As a supervision specialist, I want to record a candidate supervision item with its source and expected outcome, so that important work can enter a controlled tracking process.

Trace: F-008 / Scope S-001,S-002。

### US-002 Establish accountability
As a supervision specialist, I want an issued item to have an accountable department, so that organizational responsibility is explicit.

Trace: F-002 / BR-002。

## Epic B — Execute & Update

### US-003 View responsibilities
As a responsible participant, I want to see the supervision items relevant to my responsibility scope, so that I know what needs attention.

Trace: J-002/J-004。

### US-004 Submit progress
As an authorized responsible participant, I want to append a progress update without destroying previous updates, so that stakeholders can understand how the work evolved.

Trace: F-001/F-003 / BR-004。

## Epic C — Attention

### US-005 Verify stale information
As a supervision specialist, I want to identify items whose progress information may be stale, so that I can verify them before management review.

Trace: F-004 / BR-005。

### US-006 Identify deadline attention
As a supervision specialist, I want to identify near-due and overdue items, so that potential delivery issues can be reviewed early.

Trace: J-001 / BR-006,BR-007。

### US-007 Management intervention view
As a manager, I want to focus on items that may require management intervention and understand why they need attention, so that limited meeting time is spent on decisions rather than reading every task.

Trace: J-003 / F-005,F-007。

Note: This story does **not** require a specific dashboard layout.

## Epic D — Completion & Closure

### US-008 Submit completion claim
As an authorized accountable party, I want to declare that execution work is complete and provide the required completion information, so that the item can enter closure review.

Trace: F-006 / BR-008。

### US-009 Confirm closure
As a closure authority, I want to review a completion claim and formally close the item when applicable conditions are satisfied, so that “work reported complete” and “supervision officially ended” remain distinguishable.

Trace: F-006 / BR-009。

Actor is semantically known but concrete role remains SPEC_GAP.

## Epic E — Traceability

### US-010 Review history
As an authorized stakeholder, I want to review key changes and progress history, so that I can understand who changed what and when.

Trace: F-001 / BR-011。

## Story Readiness Rule

Story 只有同时满足以下条件才可进入 Implementation Ready：

```text
Story
+ Business Rule
+ Permission
+ State impact
+ Acceptance Criteria
+ no blocking SPEC_GAP
```

否则它只是 Product Backlog Item，不是 Coding Instruction。
