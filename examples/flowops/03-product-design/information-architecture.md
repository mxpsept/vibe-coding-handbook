# FlowOps — Information Architecture v0.1

## 1. Domain-centered IA

核心对象：

```text
Supervision Item
├── Identity / Source
├── Accountability
├── Deadline
├── Progress History
├── Attention
├── Completion Claim
└── Audit History
```

辅助对象候选：

```text
Department
User
Attachment
Notification (future)
Configuration
```

## 2. User Mental Models

### Responsible Participant

```text
我需要处理什么？
→ 任务是什么？
→ 什么时候完成？
→ 现在是否需要我更新？
→ 如何提交进展/完成？
```

### Supervision Specialist

```text
现在有哪些重点事项？
→ 哪些需要关注？
→ 为什么？
→ 最近发生了什么？
→ 是否需要跟进？
```

### Manager

```text
哪些事情需要我介入？
→ 为什么？
→ 谁负责？
→ 卡在哪里？
→ 我需要做什么决定？
```

## 3. Proposed IA

```text
Home / Workbench
│
├── My Work
│   ├── Needs My Action
│   └── Relevant Items
│
├── Supervision
│   ├── All Items
│   ├── Attention
│   └── Closure Review (permission-based candidate)
│
├── Management
│   └── Management Review
│
└── Administration
    └── Configuration
```

`Item Detail` 是跨入口共享的业务对象页面，不单独成为一级菜单。

## 4. Why not CRUD IA

Rejected candidate:

```text
Task Management
Progress Management
Status Management
Deadline Management
Attachment Management
Audit Management
```

Reason:
- 把数据模型暴露给用户；
- 一个业务对象被拆散；
- 用户必须理解系统内部结构才能完成任务；
- 菜单数量随数据库表增长。

## 5. Attention IA Decision

Attention 是业务维度，不是 Lifecycle State。

UI 可以提供：

```text
Attention workspace
or
Saved View / Quick Filter
```

v0.1 建议 Supervision Specialist 拥有独立 `Attention` 工作入口，因为它对应 J-001 的高频核验任务；同时 All Items 中仍可使用 Attention Filter。

## 6. Management IA Decision

Management Review 不等于普通 Dashboard。

它是面向 J-003 的 Decision-support View，因此可以独立存在，并采用与运营列表不同的信息密度。

## 7. Cross-cutting Context

以下能力不建议默认成为一级菜单：

```text
Search
Notifications
Profile
Help
```

它们属于 Global Utility。

## 8. IA Validation Questions

- Responsible Participant 能否在一个入口找到主要工作？
- Supervision Specialist 是否能在两步内进入 Attention Item？
- Manager 是否需要理解“任务管理”结构才能找到干预事项？
- Item History 是否始终与 Item Context 绑定？
- 权限变化后 Navigation 是否仍然自然？
