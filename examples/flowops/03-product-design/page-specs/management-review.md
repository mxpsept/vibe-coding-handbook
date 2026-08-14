# P-009 — Management Review Page Specification

## Purpose
帮助 Manager 在短时间内识别并理解需要管理干预的事项。

## Route Candidate
`/management-review`

## Primary Job

```text
Attention → Understanding → Management Decision
```

而不是：

```text
Statistics → Charts → More Charts
```

## Recommended Composition

```text
Page Header + Scope/Period Context
↓
Attention Summary Sentence
↓
Priority Attention / Intervention Candidates
↓
Selected/Expanded Context
↓
Secondary Management Context
```

## Hero Content
不是 KPI Cards，而是需要关注的具体事项及原因。

Example presentation:

```text
Item A
[IN_PROGRESS]
已超过有效截止日期 3 天
Accountable: Dept A
Latest: ...
```

## Context Metrics
允许少量指标帮助建立背景，例如 Active / Attention / Pending Closure，但：
- 必须有真实 Requirement/Data Definition；
- 不为了对称固定四张卡片；
- Attention 数字不等同 Lifecycle 数量。

## Priority Rule
如果系统没有已确认 Priority Algorithm：

禁止：

```text
AI 智能排序
风险评分 92
Top 5 Critical
```

可使用可解释排序：

```text
explicit user sort
known overdue duration
known due date
known last-update time
```

具体默认排序仍需 Product Rule。

## Secondary Analytics
任何 Chart 必须记录：

```text
Question it answers
Decision it supports
Data definition
```

无法回答三项则删除。

## Interaction
Manager 可打开 Item Detail 获取完整上下文。

是否提供系统内“协调/批示/督办”动作属于未来 Requirement，不由设计阶段增加。

## States

```text
loading
no-attention
scope-no-result
partial-data-error
unauthorized
long-title
multiple-attention
```

## Density
Comfortable；但不是营销页面级大留白。

## Readiness
`READY_WITH_GAPS` — default priority/sort rule needs Product confirmation before claiming prioritized intelligence。
