# FlowOps — Design System Foundation v0.1

> 目标：让几十个页面由不同 AI / Developer 实现后，仍然像同一个产品。

本文件定义语义与约束，不要求具体前端框架。

## 1. Design Principles

```text
Consistency > novelty
Hierarchy > decoration
Semantic color > colorful UI
Readable density > oversized whitespace
Reusable pattern > page-specific invention
```

## 2. Token Layers

推荐三层：

```text
Primitive Tokens
    ↓
Semantic Tokens
    ↓
Component Tokens
```

例如：

```text
blue-600
  ↓
color.action.primary
  ↓
button.primary.background
```

业务代码优先消费 Semantic / Component Token，而不是直接写 Hex。

## 3. Color Semantics

### Surface

```text
color.bg.page
color.bg.surface
color.bg.subtle
color.border.default
color.border.strong
```

### Text

```text
color.text.primary
color.text.secondary
color.text.muted
color.text.inverse
color.text.link
```

### Action

```text
color.action.primary
color.action.primaryHover
color.action.danger
```

### Lifecycle

Lifecycle 使用稳定但克制的表达。具体色值在视觉实现阶段确定。

```text
color.lifecycle.draft
color.lifecycle.issued
color.lifecycle.inProgress
color.lifecycle.pendingClosure
color.lifecycle.closed
color.lifecycle.cancelled
```

### Attention

```text
color.attention.stale
color.attention.nearDue
color.attention.overdue
```

重要：Lifecycle Color 与 Attention Color 属于不同 Token Namespace。

## 4. Typography

建议建立角色而不是页面自定义字号：

```text
type.pageTitle
type.sectionTitle
type.cardTitle
type.body
type.bodyStrong
type.secondary
type.caption
type.metric
```

原则：
- 正文保持高可读性；
- Metric 只用于真正关键数字；
- 不使用过多 Font Weight；
- 中文企业 UI 注意行高，不要为了紧凑牺牲可读性。

## 5. Spacing

采用固定 Scale，例如：

```text
space.1
space.2
space.3
space.4
space.5
space.6
space.8
space.10
```

具体 px/rem 在实现阶段确定。

禁止：

```css
margin-top: 13px;
padding: 19px 27px;
```

除非存在明确布局原因。

## 6. Radius

控制 Radius 数量：

```text
radius.sm
radius.md
radius.lg (rare)
```

企业工作系统避免所有容器“大圆角卡片化”。

## 7. Elevation

优先：

```text
spacing + background + border
```

再使用 Shadow。

建议：

```text
elevation.none
elevation.overlay
elevation.floating
```

普通内容区不默认加阴影。

## 8. Layout

### Application Shell

```text
Global Navigation
Page Header
Content Region
Optional Context Panel
```

### Content Width

- Table / operational workspace：允许宽内容；
- Form：限制阅读宽度；
- Management Review：使用稳定 Grid；
- Detail：主内容 + facts/context candidate。

## 9. Density

```text
density.comfortable
density.default
density.compact
```

Recommended:

| Context | Density |
| --- | --- |
| Management Review | Comfortable |
| Item Detail | Default |
| My Work | Default |
| Attention Split View | Default/Compact |
| All Items | Compact/Default |
| Configuration | Default |

## 10. Page Header Pattern

```text
Breadcrumb / context (optional)
Page Title
Description / scope context
Primary Action
Secondary Actions
```

不要每页都同时放 Breadcrumb + 大标题 + 副标题 + Tabs + Toolbar，除非确有需要。

## 11. Filter Pattern

高频筛选：直接显示。

低频筛选：More Filters。

```text
Search
Quick Views
Frequent Filters
More Filters
Clear / Save View candidate
```

避免 2–3 行搜索表单长期占据页面顶部。

## 12. Table / List Pattern

每个列表必须定义：

```text
Primary identifier
Comparison fields
State presentation
Attention presentation
Row action
Sort
Filter
Empty states
Long-content behavior
```

不要默认 `所有字段 = 所有列`。

## 13. Lifecycle Badge Pattern

Badge 表达 Lifecycle：

```text
[办理中]
[待办结确认]
[已办结]
```

Attention 独立表达：

```text
已超期 3 天
8 天未更新
距离截止 2 天
```

不要把两者压缩成一个 Tag。

## 14. Attention Pattern

Attention 组件至少包含：

```text
Type
Human-readable reason
Optional time context
```

例如：

```text
OVERDUE
已超过有效截止日期 3 天
```

比单独红色 `超期` 标签信息量更高。

## 15. Timeline Pattern

Progress Timeline：

```text
Timestamp
Actor
Progress content
Optional attachment/evidence
```

Audit Timeline 与 Progress Timeline 不混合显示为同一种业务内容。

## 16. Form Pattern

Form 按用户 Mental Model 分组：

```text
What is this work?
Who is accountable?
When is it due?
Supporting context
```

而不是按照数据库列顺序。

### Validation
- field validation close to field；
- business validation clearly explained；
- server remains source of truth。

## 17. Feedback Pattern

### Success
说明“发生了什么”。

Bad:

```text
操作成功
```

Better:

```text
进展已提交，并已追加到进度记录
```

### Completion Claim

```text
完成声明已提交，等待正式办结确认
```

不能写成“办结成功”。

## 18. Empty State Pattern

Empty State = 状态解释 + 下一步（若存在）。

区分：
- truly empty；
- filter no result；
- permission no data；
- view currently empty。

## 19. Icon Rule

Icon 用于：
- 提高识别速度；
- 表达常见动作；
- 辅助状态。

不要为了“丰富 UI”给每个 Label 配 Icon。

## 20. AI Implementation Contract

Coding Agent 必须：

```text
reuse tokens
reuse approved patterns
avoid new arbitrary colors
avoid new spacing values
avoid new badge semantics
avoid page-local design systems
```

如果现有 Design System 无法表达需求：

```text
DESIGN_SYSTEM_GAP
```

而不是自行创建新的视觉规则。
