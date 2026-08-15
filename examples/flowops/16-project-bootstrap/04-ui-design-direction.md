# 04 — UI Design Direction

## Design Goal

FlowOps 不是“数据大屏”。核心设计目标：

> 让用户快速知道 **现在最需要处理什么、为什么需要处理、下一步能做什么**。

## Information Hierarchy

### Level 1 — Attention
临期、超期、待确认、长时间未更新等需要行动的信息。

### Level 2 — Work Context
事项名称、责任关系、完成时限、最近进展、当前生命周期。

### Level 3 — Evidence
历史进展、附件、审计、变更记录。

## First Workspace Direction

```text
┌──────────────────────────────────────────────┐
│ Page title        Scope / filter     Actions │
├──────────────────────────────────────────────┤
│ Attention summary (compact, actionable)      │
├───────────────┬──────────────────────────────┤
│ Filters       │ Work list                    │
│               │ reason | item | owner | due  │
│               │ latest update | next action  │
├───────────────┴──────────────────────────────┤
│ Pagination / result context                  │
└──────────────────────────────────────────────┘
```

不是先放 8 个 KPI Card + 6 张图表。

## Visual Principles

- enterprise neutral，避免过度科技蓝发光；
- spacing 和 typography 建立清晰层级；
- status/attention color 只用于语义，不作为装饰；
- table/list 保持高信息密度但避免所有字段同权重；
- primary action 每个上下文尽量唯一；
- destructive/high-risk action 明确二次确认。

## Required Page States

每个关键页面必须设计：

```text
Loading
Empty
Data
Filtered Empty
Error
Permission Denied
Partial/Degraded (when relevant)
```

## UI Review Questions

1. 5 秒内能否看出最重要信息？
2. 用户是否知道下一步动作？
3. Attention 和 lifecycle 是否视觉混淆？
4. Empty/Error 是否像真正产品，而不是开发占位？
5. 不看颜色时信息是否仍可理解？
6. Agent 是否擅自引入了新的视觉体系或组件库？

## Before Frontend Coding

至少批准：User Flow、Wireframe direction、Design tokens/component convention、Page State Matrix。之后 Coding Agent 的工作是实现设计，而不是替代设计阶段。
