# P-004 — Attention Workspace Page Specification

## Purpose
让 Supervision Specialist 高效核验 Attention，而不是浏览另一个重复任务表格。

## Route
`/attention`

## Recommended Pattern
Desktop Split View。

```text
Attention Filters
↓
┌──────────────────────┬───────────────────────────────┐
│ Attention Queue      │ Selected Item Context         │
│                      │ Why Attention                 │
│                      │ Responsibility / Due          │
│                      │ Latest Progress               │
│                      │ Timeline Preview              │
└──────────────────────┴───────────────────────────────┘
```

## Queue Item Minimum Information

```text
Title
Accountable Department
Attention Flags
Effective Due Date context
Last Update context
```

## Selected Context
必须优先回答：

```text
Why is this item here?
What is its lifecycle?
Who is accountable?
What is the effective deadline?
What was the latest progress?
```

## Attention Semantics

### STALE_UPDATE
允许表达：

```text
8 天未收到新的进展信息
```

禁止推断：

```text
已停滞 8 天
```

### OVERDUE

```text
已超过有效截止日期 N 天
```

### Multiple Flags
同时展示，不互斥。

## Actions
MVP 默认：

```text
Open Full Detail
```

“催办、确认已核验、升级、忽略”等动作均需 Requirement 支持；当前不得由 UI Agent 发明。

## Empty State

```text
当前没有需要核验的事项。
```

这是积极业务状态。

## States

```text
loading
empty
filter-no-result
error
unauthorized
selected-item-error
long-content
many-items
```

## Responsive
Narrow screen：Queue → Item Context 使用 drill-in，而不是并排压缩。

## Readiness
`READY_WITH_GAPS` — follow-up action semantics remain SPEC_GAP if requested。
