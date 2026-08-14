# FlowOps — My Work Wireframe Directions v0.1

## Primary Actor
Responsible Participant

## Primary Job
知道哪些事项与我相关、哪些现在需要行动，并快速进入更新或完成声明。

---

# Direction A — Personal Dashboard

```text
[我的任务 12] [临期 3] [超期 1] [待办结 2]

任务趋势图
任务类型图
最近任务表格
```

### Problem
统计占据首屏，但执行者真正需要的是“现在做什么”。

**Decision: Reject as default.**

---

# Direction B — Action-first Work Queue

```text
┌──────────────────────────────────────────────────────────────┐
│ 我的工作                                                     │
│ 这里是当前与你相关、可能需要行动的事项。                     │
├──────────────────────────────────────────────────────────────┤
│ Needs My Action                                              │
│                                                              │
│ Item A                                  [更新进度]            │
│ Dept · Due Apr 30 · 8 天未更新                               │
│ Latest: 已完成初稿，等待协同部门反馈……                       │
│ -----------------------------------------------------------  │
│ Item B                                  [提交完成声明]        │
│ Dept · Due May 02 · IN_PROGRESS                              │
├──────────────────────────────────────────────────────────────┤
│ Relevant Items                                               │
│ [办理中] [临期] [全部]                                      │
│ compact list                                                 │
└──────────────────────────────────────────────────────────────┘
```

### Strengths
- Action 优先于统计；
- 用户不必从全部任务里找自己；
- 高频动作可 Contextual Access；
- Latest Progress 帮助用户恢复上下文。

### Critical Constraint
“Needs My Action”的计算规则目前不能由 UI/AI 自行发明。

如果只是根据权限和已知 Attention 组合，应明确规则；否则标记 `DESIGN_SPEC_GAP`。

**Decision: Recommended direction, pending action-rule clarification.**

---

# Direction C — Calendar-first

```text
Calendar
├── Apr 28 Item A
├── Apr 30 Item B
└── May 02 Item C
```

### Strength
期限感强。

### Weakness
督办工作不只由 Due Date 驱动；Stale Update、Completion Claim 等无法自然表达。

**Decision: Calendar may be secondary view, not primary.**

---

# Contextual Actions

Candidate actions:

```text
Open Detail
Update Progress
Submit Completion Claim
```

动作显示必须同时考虑：

```text
Lifecycle
+ Permission
+ applicable Business Rule
```

例如：

```text
CLOSED → no normal Update Progress
PENDING_CLOSURE → no duplicate normal Completion Claim
```

# Mobile Future Consideration

My Work 是最可能优先进入移动端的场景之一。

移动端可重新排序为：

```text
Needs My Action
↓
Attention / Due Context
↓
Quick Update
↓
Relevant Items
```

而不是缩小桌面 Table。
