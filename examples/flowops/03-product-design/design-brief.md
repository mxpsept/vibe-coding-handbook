# FlowOps — Product Design Brief v0.1

> Synthetic Teaching Case。设计必须消费 Stage 02 Specification，不得静默改变 Business Rule。

## 1. Product Context

FlowOps 是企业重点事项督办与执行跟踪产品。MVP 关注：事项建立、组织责任、进度更新、Attention、Completion Claim、Closure 与历史追踪。

## 2. Design Problem

当前痛点不是“缺少一个 Dashboard”，而是不同角色难以在分散信息中快速找到：

```text
What needs my action?
What needs verification?
What needs management intervention?
What happened to this item?
What can I do now?
```

## 3. Primary Personas / Jobs

### Supervision Specialist
高频使用；需要跨事项扫描、筛选、核验和跟进。

Design priority:
- scanability；
- efficient filtering；
- attention context；
- low navigation cost。

### Responsible Participant
需要快速知道“我的工作”和提交真实进展。

Design priority:
- clarity；
- low-friction update；
- mobile-friendly future potential。

### Department Manager
需要理解部门承担的事项、内部执行和阻塞。

### Manager
低频但高价值；需要在短时间识别需要干预的事项。

Design priority:
- decision support；
- lower density than operator views；
- explain why an item needs attention。

### Closure Authority
需要核验 Completion Claim 并做正式 Closure Decision。

Concrete role remains SPEC_GAP。

## 4. Product Design Principles

### DP-001 — Decision before decoration
布局首先服务任务与决策，而不是视觉效果。

### DP-002 — Attention is explainable
任何 Attention 表达必须能回答“为什么需要关注”。

### DP-003 — Lifecycle and Attention are visually distinct
例如 `IN_PROGRESS + OVERDUE` 必须可以同时理解，而不是只显示一个“超期状态”。

### DP-004 — Reading view != edit form
详情页优先阅读、理解、行动，不机械复刻编辑表单。

### DP-005 — Progressive disclosure
高频信息优先，低频历史与审计按需展开。

### DP-006 — Dense where comparison matters
列表和运营工作区允许合理信息密度；管理视图更聚焦。

### DP-007 — No invented metrics
UI 不得为了填满 Dashboard 创造没有 Requirement 的 KPI。

## 5. Visual Intent

Desired:

```text
professional
calm
structured
modern enterprise
high scanability
restrained brand expression
```

Avoid defaulting to:

```text
blue gradient everywhere
neon glow
large decorative charts
oversized cards
excessive rounded containers
marketing-site whitespace
```

## 6. Technical Context

Future frontend candidate: Vue 3 + enterprise component system（具体技术在 Architecture 阶段确认）。

Design 不应被某个组件库现有 Demo 限制，但最终 Pattern 应具备现实可实现性。

## 7. Key Design Questions

1. 首页应该是“工作入口”还是“统计看板”？
2. Attention 应作为独立工作区还是列表 Saved View？
3. Manager 是否需要独立 Management Review？
4. Item Detail 如何同时表达 Lifecycle + Attention + Current Context + History？
5. 高频 Progress Update 最少需要几步？
6. Closure Review 应独立队列还是嵌入 Attention？
7. Navigation 如何避免“每个业务动作一个菜单”？

## 8. Constraints from Requirements

设计不能违反：

```text
OVERDUE != Lifecycle State
STALE_UPDATE != Delayed
Completion Claim != Closure
Progress Update is append-oriented
Terminal items reject normal progress update
```

如设计过程中发现这些规则不足，创建 `DESIGN_SPEC_GAP` 并返回 Requirements，而不是由 Designer/AI 自行决定。
