# P-001 — Workbench Page Specification

## Purpose
为不同角色提供进入当前最重要工作的起点，而不是把整个系统压缩成一个 Dashboard。

## Route
`/workbench`

## Primary Principle

```text
Workbench = role-aware launch point
Workbench != miniature version of every module
```

## Role Composition

### Responsible Participant
优先：

```text
Needs My Action
Attention / Due Context
Recent Relevant Items
```

### Supervision Specialist
优先：

```text
Attention needing review
Recently changed supervision items
Quick access to All Items
```

### Manager
优先：

```text
Intervention candidates
Concise management context
Entry to Management Review
```

如果同一用户有多个角色，应通过稳定优先级/组合规则解决，不由前端随机拼卡片。

## Layout Candidate

```text
Greeting / Role Context
↓
Primary Work Section
↓
Secondary Context
↓
Recent / Resume Work
```

## Metrics
允许少量、可解释的 Context Metric，但每个 Metric 必须回答：

```text
Why does this help the current role decide or act?
```

不能为了视觉平衡固定“四张卡片”。

## Quick Actions
只提供真正高频且有权限的入口，例如：

```text
Create Item — authorized supervision role
Open My Work
Open Attention
```

不要复制整个侧边栏。

## Personalization
MVP 不默认支持用户拖拽 Dashboard、自定义 Widget。除非 Requirement 明确，否则保持产品控制的信息层级。

## States

```text
loading
role-with-no-work
partial-section-error
unauthorized
long-content
```

### No Work

```text
当前没有需要你处理的事项。
```

并提供自然的下一入口，而不是空白大屏。

## Forbidden AI Decisions
- 为每个模块创建统计卡；
- 无 Requirement 添加趋势图；
- 根据用户历史自行“AI 推荐任务”；
- 将 Workbench 设计成领导大屏并给所有角色复用。

## Readiness
`READY_WITH_GAPS` — multi-role composition priority should be confirmed during implementation planning。
