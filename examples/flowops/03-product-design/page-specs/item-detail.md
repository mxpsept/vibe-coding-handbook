# P-005 — Item Detail Page Specification

## 1. Purpose

帮助授权用户快速理解一个督办事项的当前上下文、责任、期限、进展历史与 Attention，并执行当前允许的动作。

## 2. Trace

```text
Requirements: US-005 / US-008 and related stories
Rules: BR-005 / BR-006 / BR-007 / BR-008
State: state-model.md
Wireframe: ../wireframes/item-detail-directions.md → Direction B
Design: ../design-system.md
States: ../ui-state-matrix.md
```

具体 ID 以 Stage 02 Artifact 为 Source of Truth；发现不一致时返回 Requirements 修正，不在本文件重新定义规则。

## 3. Route Candidate

```text
/items/:id
```

## 4. Primary Job

```text
Understand what is happening now → understand why → take an allowed action
```

## 5. Layout Contract

```text
Page Context / Back Navigation
↓
Title + Lifecycle + Attention + Primary Actions
↓
Responsibility + Effective Due Date
↓
Current Context
├── Latest Progress
└── Attention Explanation
↓
Main Content
├── Progress Timeline
└── Key Facts / Supporting Context
↓
Secondary History / Audit
```

## 6. Component Hierarchy

```text
ItemDetailPage
├── PageHeader
│   ├── ItemTitle
│   ├── LifecycleBadge
│   ├── AttentionSummary
│   └── ContextualActions
├── ResponsibilityDeadlineSummary
├── CurrentContextPanel
│   ├── LatestProgress
│   └── AttentionExplanation
├── ProgressTimeline
├── KeyFacts
└── AuditSection
```

组件名称是设计语义，不强制对应最终代码文件。

## 7. Information Priority

### Primary
- Title；
- Lifecycle；
- Attention；
- Accountable Department；
- Effective Due Date；
- Latest Progress。

### Secondary
- Source；
- Created / Issued metadata；
- supporting information。

### Tertiary
- Audit history。

## 8. Actions

### Update Progress

Display candidate when:

```text
permission allows
AND lifecycle allows normal progress update
```

服务端仍为最终授权来源。

### Submit Completion Claim

```text
IN_PROGRESS + permission + BR-008
```

提交成功后的 Copy：

```text
完成声明已提交，等待正式办结确认。
```

### Closure
仅 Closure Authority + valid lifecycle；角色规则未确认部分保持 SPEC_GAP。

## 9. Lifecycle / Attention Presentation

禁止：

```text
Status: OVERDUE
```

要求同时表达：

```text
Lifecycle: IN_PROGRESS
Attention: OVERDUE — 已超过有效截止日期 N 天
```

多个 Attention Flags 可并存。

## 10. Interaction Rules

- Progress Timeline 默认按最新优先或时间轴方向需统一产品规则；
- Audit 默认 Secondary / collapsed candidate；
- Attention Reason 必须 human-readable；
- 长标题允许多行，不因保持单行而隐藏核心含义；
- Action Pending 时避免重复提交；
- Server validation error 不丢失用户输入。

## 11. States

Must design:

```text
loading
not-found
unauthorized
read-only
in-progress
pending-closure
closed
error
conflict
long-content
many-progress-records
```

## 12. Responsive

Desktop candidate:

```text
main content + context/facts column
```

Narrow viewport:

```text
single column
Current Context → Timeline → Key Facts → Audit
```

不得仅缩小双栏宽度。

## 13. Accessibility

- Lifecycle / Attention 不只靠颜色；
- Action 有可读 Label；
- Timeline 保持语义顺序；
- Focus state 可见；
- Tooltip 不承载唯一关键业务信息。

## 14. Forbidden AI Decisions

Coding Agent 不得自行：
- 把 Progress Percentage 作为 Source of Truth；
- 将 Completion Claim 自动映射 CLOSED；
- 创造新的 Attention 类型；
- 增加“驳回/催办/升级”业务动作；
- 根据 UI 隐藏代替服务端权限。

## 15. Implementation Readiness

Status: `READY_WITH_GAPS`

Blocking gap candidate:
- Closure Authority / reject-return semantics if Closure action included。
