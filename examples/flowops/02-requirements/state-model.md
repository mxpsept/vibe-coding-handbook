# FlowOps — Lifecycle & Attention Model v0.1

> 核心目标：不要用一个 `status` 字段同时表示生命周期、期限、风险和进度。

## 1. Lifecycle State

```text
DRAFT
  │ Issue
  ▼
ISSUED
  │ Start / Acknowledge execution
  ▼
IN_PROGRESS
  │ Submit Completion Claim
  ▼
PENDING_CLOSURE
  │ Approve Closure
  ▼
CLOSED
```

取消路径候选：

```text
DRAFT / ISSUED / IN_PROGRESS / PENDING_CLOSURE
                    ↓
                 CANCELLED
```

Cancellation Rule / Authority: TBD。

## 2. State Definitions

| State | Meaning | Terminal |
| --- | --- | --- |
| DRAFT | 尚未正式下达，可继续准备 | No |
| ISSUED | 已正式下达，但尚未进入实际办理 | No |
| IN_PROGRESS | 正在执行，可提交 Progress Update | No |
| PENDING_CLOSURE | 责任方已声明完成，等待正式确认 | No |
| CLOSED | 已完成适用确认并正式结束 | Yes |
| CANCELLED | 已取消，不再继续执行 | Yes |

## 3. Attention Flags — Independent Dimension

```text
STALE_UPDATE
NEAR_DUE
OVERDUE
BLOCKED (Candidate)
```

同一个事项可能同时：

```text
Lifecycle = IN_PROGRESS
Attention = [STALE_UPDATE, NEAR_DUE]
```

也可能：

```text
Lifecycle = PENDING_CLOSURE
Attention = [OVERDUE]
```

因此不能把“超期”设计成 State。

## 4. Progress — Independent Dimension

最低 MVP 可仅使用：

```text
Progress Update History
```

而不是强制 Percentage。

如果后续批准 Percentage：

```text
Progress Percentage != Lifecycle State
Progress Percentage != Closure
```

即使 `100%` 也不能自动进入 `CLOSED`。

## 5. Transition Table

| Transition | From | To | Actor | Preconditions | Effects |
| --- | --- | --- | --- | --- | --- |
| Issue | DRAFT | ISSUED | Authorized issuer | Accountable Department + Effective Due Date exist | audit |
| Start | ISSUED | IN_PROGRESS | TBD | item valid | start timestamp + audit |
| Submit Progress | IN_PROGRESS | IN_PROGRESS | Authorized party | content valid | append progress + refresh last update + audit |
| Submit Completion | IN_PROGRESS | PENDING_CLOSURE | Authorized accountable party | completion data valid | claim timestamp + audit |
| Approve Closure | PENDING_CLOSURE | CLOSED | Closure Authority TBD | applicable evidence accepted | closure actor/time + audit |
| Cancel | non-terminal | CANCELLED | TBD | cancellation reason | audit |

## 6. Forbidden Transitions

Unless a future rule explicitly approves them:

```text
DRAFT → CLOSED            forbidden
ISSUED → CLOSED           forbidden
IN_PROGRESS → CLOSED      forbidden
CLOSED → IN_PROGRESS      forbidden in MVP
CANCELLED → IN_PROGRESS   forbidden in MVP
```

## 7. Why this matters to Coding Agent

错误 Prompt：

```text
给任务表增加 status：待处理、处理中、临期、超期、完成。
```

更好的 Context：

```text
Lifecycle State and Attention Flags are separate dimensions.
Do not add NEAR_DUE or OVERDUE to lifecycle enum.
Do not infer CLOSED from progress percentage.
Follow state-model.md and business-rules.md.
```

这类约束可以直接阻止大量后期重构。
