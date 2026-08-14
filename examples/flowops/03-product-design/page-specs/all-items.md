# P-003 — All Supervision Items Page Specification

## Purpose
帮助督办人员在组织范围内快速定位、比较和进入具体事项。

## Recommended Pattern
`Work Views + Progressive Filters + Dense List/Table`。

## Route Candidate
`/items`

## Layout

```text
Page Header                                  [+ 新建事项]
Search
Quick Views
Frequent Filters                    [More Filters]
Result Context / Sort
Item List or Table
Pagination / load strategy (Architecture decision)
```

## Quick View Candidates

```text
全部
办理中
需关注
待办结
```

每个 View 必须映射已确认业务语义。不得由前端自行创造复杂规则。

## Primary Columns / Fields

```text
Title / Identifier
Accountable Department
Effective Due Date
Lifecycle
Attention
Last Update / Latest Progress Cue
```

Secondary fields 进入 Column Preference / Detail，而不是全部默认显示。

## Critical Semantic Rule

不要提供一个含义模糊的：

```text
状态
```

如果筛选同时涉及 Lifecycle 和 Attention，应拆分：

```text
办理状态
关注类型
```

## Row Interaction

Primary:
`open Item Detail`

Contextual action candidate:
`Update Progress` only for applicable user/state。

不要默认增加“编辑/删除/催办/办结”四件套操作列。

## Filters

High-frequency candidate:
- search；
- accountable department；
- effective due date；
- lifecycle；
- attention。

Low-frequency → More Filters。

## States

```text
loading
truly-empty
filter-no-result
quick-view-empty
unauthorized
error
large-data
long-title
multiple-attention
```

### Truly Empty

```text
还没有督办事项。
[新建事项] — only if authorized
```

### No Result

```text
没有符合当前筛选条件的事项。
[清除筛选]
```

## Density
Default / Compact。

## Responsive
Desktop 为主要工作场景。移动端若未来支持，不复制完整宽表；应根据 Mobile Jobs 重新设计。

## Forbidden AI Decisions
- 所有数据库字段自动变成列；
- `OVERDUE` 当 Lifecycle；
- 为了 UI 丰富增加统计卡片；
- 没有 Job 就增加 Bulk Actions；
- 未确认就实现 Saved View 持久化。

## Readiness
`READY_WITH_GAPS` — Saved View / bulk behavior remain candidates, not MVP commitments。
