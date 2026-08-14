# P-002 — My Work Page Specification

## Purpose
帮助 Responsible Participant 快速识别与自己相关、当前需要处理的督办事项，并低成本进入进展更新或完成声明。

## Route Candidate
`/my-work`

## Primary Job

```text
Know what needs my action → recover context → act
```

## Recommended Composition

```text
Page Header
↓
Needs My Action
↓
Relevant Items / Views
```

统计数字只能作为辅助上下文，不能替代 Action Queue。

## Needs My Action

这是一个业务语义区域，不允许 UI Agent 自行定义复杂规则。

若 Requirements 仅确认了以下 Evidence：

```text
Lifecycle
Attention
Responsibility
Permission
```

则只能使用已确认组合规则；否则标记 `DESIGN_SPEC_GAP`。

## Queue Item Information

```text
Title
Lifecycle
Attention if any
Effective Due Date
Latest Progress cue
Accountability context
```

## Contextual Actions

Candidate:

```text
Update Progress
Submit Completion Claim
Open Detail
```

Action visibility = approved lifecycle semantics + permission；服务端最终校验。

## Relevant Items

可提供：

```text
办理中
临近期限
全部相关
```

但每个 View 的计算定义必须可追踪。

## Interaction Rules

- Action Queue 不以 KPI Card 替代；
- Latest Progress 用于帮助用户恢复上下文；
- 快捷操作不能绕过业务确认；
- 提交失败保留输入；
- Completion Claim 成功后显示“等待正式办结确认”。

## States

```text
loading
no-action-needed
no-relevant-items
filter-no-result
error
unauthorized
read-only
submitting
success
conflict
long-title
long-progress
```

### No Action Needed

```text
当前没有需要你处理的事项。
```

不要显示成错误或普通“暂无数据”。

## Mobile Direction
My Work 是移动端优先候选。移动版应保持 Action-first，而不是缩小桌面列表。

## Forbidden AI Decisions
- 自行计算“智能优先级”；
- 用任务数量卡片替代工作队列；
- 将 OVERDUE 作为 Lifecycle；
- 自动认定 Stale Update = 执行停滞；
- 创建未批准快捷动作。

## Readiness
`READY_WITH_GAPS` — Needs My Action 的精确计算规则需要 Product/Requirements 确认后才能成为稳定 Contract。
