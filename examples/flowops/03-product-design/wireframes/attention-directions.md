# FlowOps — Attention Workspace Wireframe Directions v0.1

## Primary Actor
Supervision Specialist

## Primary Job
快速核验需要关注的事项，理解 Attention 原因，并决定是否需要人工跟进。

---

# Direction A — Filtered Table

```text
重点关注
[全部] [超期] [临期] [长时间未更新]

事项 | 责任部门 | Attention | 截止日期 | 最近更新 | 操作
-------------------------------------------------------
A    | Dept A   | 超期3天   | Apr 30   | 昨天     | 查看
B    | Dept B   | 8天未更新 | May 05   | 8天前    | 查看
```

### Strengths
- 熟悉；
- 扫描大量事项效率尚可；
- 实现简单。

### Weaknesses
- Attention 原因只能压缩成标签；
- 每次理解上下文都要进入 Detail；
- 容易退化成 All Items 的重复页面。

---

# Direction B — Attention Split View

```text
┌───────────────────────────────────────────────────────────────┐
│ 重点关注                 [全部][超期][临期][未更新] [筛选]   │
├────────────────────────────┬──────────────────────────────────┤
│ Attention Queue            │ Selected Item Context            │
│                            │                                  │
│ Item A                     │ Item A                           │
│ OVERDUE · 3 days           │ [IN_PROGRESS]                    │
│ Dept A · updated yesterday │ Attention reason                │
│                            │ · 已超过有效截止日期 3 天        │
│ Item B                     │                                  │
│ STALE · NEAR_DUE           │ Responsibility / Due Date        │
│ Dept B · updated 8d ago    │ Latest Progress                  │
│                            │ Progress Timeline preview        │
│ Item C                     │                                  │
│ ...                        │ [打开完整详情]                   │
└────────────────────────────┴──────────────────────────────────┘
```

### Strengths
- Queue → Why → Context 几乎无跳转；
- 适合督办人员逐项核验；
- 多 Attention 可以同时表达；
- 不需要把 Attention 当 Lifecycle。

### Risks
- 需要控制右侧信息量；
- 小屏需要切换为单栏；
- 不应在右侧偷偷加入未定义“催办/升级”业务动作。

**Decision: Recommended.**

---

# Direction C — Kanban by Attention Type

```text
STALE UPDATE     NEAR DUE        OVERDUE
[Item]           [Item]          [Item]
[Item]           [Item]          [Item]
```

### Problem
同一 Item 可以同时拥有多个 Attention Flags，因此 Kanban 强迫一个事项归属一个列，会扭曲 Domain Model 或产生重复卡片。

**Decision: Reject for primary model.**

---

# Attention Copy Rules

Bad:

```text
状态：异常
状态：超期
风险任务
```

Better:

```text
办理中
Attention: 已超过有效截止日期 3 天
```

For STALE_UPDATE:

```text
8 天未收到新的进展信息
```

而不是：

```text
任务已停滞 8 天
```

因为系统只有信息新鲜度 Evidence，没有真实执行停滞 Evidence。

# Human Review Questions

1. 每次核验通常处理多少事项？
2. 是否需要在 Queue 中展示 Latest Progress 摘要？
3. 是否需要人工标记“已核验”？当前 Requirements 未定义。
4. 是否需要系统内催办？若需要必须返回 Requirements。
5. Attention Queue 是否需要 Saved Filters？
