# FlowOps — Management Review Wireframe Directions v0.1

> 同一 Requirement 先探索多个结构方向。此阶段只比较信息结构，不讨论最终颜色与视觉装饰。

## Design Brief

**Actor:** Manager  
**Primary Job:** 在有限时间内识别需要管理干预的事项，并理解原因。  
**Secondary Job:** 获取整体执行背景。

---

# Direction A — Executive Overview

```text
┌──────────────────────────────────────────────────────────────┐
│ Management Review                            [Period][Scope] │
│ 需要您关注：6 项 · 其中 2 项存在跨部门阻塞                  │
├──────────────────────────────────────────────────────────────┤
│ Context Summary                                                │
│ Active 28 | Need Attention 6 | Pending Closure 3              │
├──────────────────────────────────────────────────────────────┤
│ Priority Attention                                             │
│ ┌──────────────────────────────────────────────────────────┐ │
│ │ 事项 A  [OVERDUE]                                        │ │
│ │ Why: 超过有效截止日期 3 天                               │ │
│ │ Dept A · Latest: ... · Updated yesterday                 │ │
│ └──────────────────────────────────────────────────────────┘ │
│ ┌──────────────────────────────────────────────────────────┐ │
│ │ 事项 B [STALE_UPDATE] [NEAR_DUE]                         │ │
│ │ Why: 8 天未更新；距离截止 2 天                           │ │
│ └──────────────────────────────────────────────────────────┘ │
├───────────────────────────────┬──────────────────────────────┤
│ Department Attention Context  │ Deadline Context             │
│ compact ranking/list          │ compact trend/distribution   │
└───────────────────────────────┴──────────────────────────────┘
```

### Strengths
- 适合会议/管理角色；
- Priority Attention 是 Hero；
- 少量统计提供背景但不抢主任务。

### Risks
- 如果 Priority 规则没有定义，AI 容易自行“智能排序”；
- Context 图表可能逐渐膨胀成传统 Dashboard。

### Recommendation
**Strong candidate for Manager.**

---

# Direction B — Attention Split View

```text
┌──────────────────────────────────────────────────────────────┐
│ Management Review                  [All][Overdue][Near Due]  │
├──────────────────────────┬───────────────────────────────────┤
│ Attention Queue          │ Selected Item                     │
│                          │                                   │
│ ● Item A                 │ Item A                            │
│   OVERDUE · Dept A       │ Why attention                    │
│                          │ Responsibility                    │
│ ● Item B                 │ Effective due date               │
│   STALE · Dept B         │ Latest progress                  │
│                          │ Blocker/dependency                │
│ ● Item C                 │ Progress timeline                │
│                          │                                   │
└──────────────────────────┴───────────────────────────────────┘
```

### Strengths
- Attention → Understanding 路径极短；
- 适合逐项 Review；
- 不需要大量跳转详情页。

### Risks
- 更像运营工作台，可能对低频 Manager 过于密集；
- 整体背景感较弱。

### Recommendation
更适合 Supervision Specialist，或 Manager 的深度 Review 模式。

---

# Direction C — KPI-first Dashboard

```text
┌──────────────────────────────────────────────────────────────┐
│ [Total] [In Progress] [Near Due] [Overdue]                  │
├──────────────────────────────┬───────────────────────────────┤
│ Pie Chart                    │ Bar Chart                     │
├──────────────────────────────┼───────────────────────────────┤
│ Trend Chart                  │ Department Ranking            │
├──────────────────────────────┴───────────────────────────────┤
│ Attention Table                                             │
└──────────────────────────────────────────────────────────────┘
```

### Strengths
- 熟悉；
- 容易实现；
- 演示时视觉元素丰富。

### Weaknesses
- 用户真正要处理的 Attention 被压到页面底部；
- 图表可能回答“有多少”，但不能回答“我应该干预什么”；
- 很容易为了填满页面创造无价值 KPI；
- `Near Due` / `Overdue` 容易被误当 Lifecycle State。

### Recommendation
**Reject as default direction.**

不是因为 Dashboard 一定错误，而是它与当前 Primary Job 匹配度最低。

---

# Direction Decision

推荐组合：

```text
Primary: Direction A — Executive Overview
Deep Review interaction: borrow Direction B split-view idea
Reject: KPI-first as page foundation
```

## Human Review Questions

1. Manager 是否主要在会议中使用？
2. Manager 每次通常需要 Review 多少事项？
3. 是否存在正式的 Priority 规则？如果没有，UI 不能称“Top Priority”。
4. Department Context 是否真的支持管理决策？
5. Manager 是否需要直接执行系统动作，还是只查看后线下协调？
