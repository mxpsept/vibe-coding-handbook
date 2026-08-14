# FlowOps — Item Detail Wireframe Directions v0.1

## Primary Job

理解一个 Supervision Item 当前发生了什么，并完成当前允许的动作。

---

# Direction A — Form-like Detail

```text
任务名称：安全文化建设体系梳理
任务编号：FO-001
任务状态：处理中
责任部门：党委工作室
截止时间：2026-04-30
进度：80%
任务来源：会议安排
创建人：...
创建时间：...

[编辑] [更新进度] [办结]
```

### Why AI often generates this

它与 CRUD / Form Schema 一一对应，实现成本低。

### Problems
- 所有信息视觉权重相同；
- 当前情况不突出；
- Progress History 被压缩成一个数字；
- Attention / Lifecycle 容易混合；
- 阅读体验像“查看数据库记录”。

**Decision: Reject as primary reading model.**

---

# Direction B — Context-first Detail

```text
┌──────────────────────────────────────────────────────────────┐
│ ← All Items                                                  │
│ 安全文化建设体系梳理                                         │
│ [IN_PROGRESS]   Attention: [STALE_UPDATE] [NEAR_DUE]        │
│ 责任：党委工作室 · Effective Due: 2026-04-30                │
│                                         [更新进度][提交完成] │
├──────────────────────────────────────────────────────────────┤
│ Current Context                                               │
│ Latest progress                                               │
│ “已完成体系框架梳理，等待相关部门反馈……”                    │
│ Updated 8 days ago                                            │
│ Attention explanation:                                       │
│ · 8 days without progress update                             │
│ · 2 days until effective due date                            │
├────────────────────────────────┬─────────────────────────────┤
│ Progress Timeline              │ Key Facts                   │
│                                │ Source                      │
│ ● Apr 20 ...                   │ Accountable Department      │
│ ● Apr 12 ...                   │ Effective Due Date          │
│ ● Apr 03 ...                   │ Created / Issued            │
│                                │ Supporting information      │
├────────────────────────────────┴─────────────────────────────┤
│ Audit / secondary history [collapsed]                        │
└──────────────────────────────────────────────────────────────┘
```

### Strengths
- 第一屏回答“现在是什么情况”；
- Lifecycle 与 Attention 同时表达；
- Timeline 强化 append-only progress mental model；
- 操作与当前状态绑定。

### Risks
- 右侧 Facts 在较窄桌面需要响应式重排；
- Attention explanation 需要真实规则支持。

**Decision: Recommended.**

---

# Direction C — Tab-heavy Detail

```text
Title + Status + Actions

[基本信息] [进度记录] [附件] [办结信息] [操作日志]
```

### Strengths
- 内容分类明确；
- 大量信息时扩展方便。

### Weaknesses
- 用户需要频繁切 Tab 才能形成完整上下文；
- Current Situation 被拆散；
- 很容易演化成“一个数据表一个 Tab”。

### Decision
只在内容规模验证后采用。MVP 优先 Progressive Disclosure，而不是默认 Tab 化。

---

# Action Rules in UI

```text
Update Progress
→ visible/enabled only when permission + valid lifecycle

Submit Completion
→ only IN_PROGRESS + permission

Approve Closure
→ only PENDING_CLOSURE + Closure Authority
```

UI 不拥有最终权限判断权。

## Copy examples

Bad:

```text
状态：超期
```

Better:

```text
Lifecycle: 办理中
Attention: 已超过有效截止日期 3 天
```

Bad after Completion Claim:

```text
办结成功
```

Better:

```text
完成声明已提交，等待正式办结确认
```

## Human Review Questions

1. Progress Timeline 是否是核心阅读区域？
2. Source Information 的使用频率多高？
3. Audit 是否默认折叠？
4. Supporting files 是否与 Progress Record 关联？
5. Long title / long progress content 的展示策略是什么？
