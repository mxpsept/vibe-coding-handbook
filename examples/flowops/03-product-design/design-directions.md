# FlowOps — Visual Design Directions v0.1

> Wireframe 决定结构；Design Direction 决定视觉语言。不要把两者混在一次 Prompt 中。

## Shared Brand Intent

FlowOps 希望呈现：

```text
可信
克制
清晰
现代企业软件
适合长期高频使用
```

不追求：

```text
赛博朋克
大屏科技感
玻璃拟态
强渐变
高饱和装饰
营销网站风格
```

---

# Direction A — Enterprise Neutral

## Character

```text
neutral surfaces
clear borders
moderate density
restrained brand color
small radius
minimal shadow
```

## Suitable for
- All Items；
- Configuration；
- dense operational pages。

## Risk
如果 Typography / spacing 做得不好，会显得普通甚至“传统后台”。

---

# Direction B — Modern Operational

## Character

```text
strong information hierarchy
soft surface separation
moderate whitespace
attention-aware visual language
compact contextual cards
```

强调：
- 当前上下文；
- Attention Reason；
- Timeline；
- Work Queue。

## Suitable for
- My Work；
- Attention；
- Item Detail。

## Risk
卡片过度使用后会失去信息密度。

**Recommended as FlowOps primary direction.**

---

# Direction C — Executive Minimal

## Character

```text
more whitespace
fewer simultaneous controls
larger key typography
focus on intervention candidates
secondary analytics subdued
```

## Suitable for
- Management Review。

## Risk
如果复制到运营列表，会降低工作效率。

---

# Proposed Product Strategy

不是选择一个视觉模板覆盖所有页面，而是：

```text
One Design System
      ↓
Different Density / Composition by Job
```

推荐：

```text
Base language: Modern Operational
Operational lists: borrow Enterprise Neutral density
Management Review: borrow Executive Minimal composition
```

这样既保持同一产品感，又避免所有角色看到完全相同的信息密度。

---

# Visual Review Heuristics

## Hierarchy
第一眼是否落在 Primary Job 相关信息？

## Restraint
去掉装饰后页面是否仍然成立？

## Density
是否为了“高级”把企业数据做得过于稀疏？

## Semantic color
颜色是否表达稳定语义，而不是随机装饰？

## Repetition
是否每个区域都被包成 Card？

## Typography
是否依靠字号/字重/间距建立层级，而不是只靠颜色？

## Alignment
相同信息是否沿稳定 Grid 对齐？

---

# Anti-patterns

### Gradient Header Syndrome

```text
蓝紫渐变顶部 + 发光数字 + 白色大卡片
```

除非品牌明确需要，否则不作为企业工作系统默认语言。

### Card Everywhere

```text
Page
└── Card
    ├── Card
    ├── Card
    └── Card
```

Surface 应表达信息分组，不是默认容器。

### Random Status Colors

同一个 `IN_PROGRESS` 不应在不同页面分别是蓝、绿、紫。

### Decorative Analytics

图表必须回答真实问题；没有 Decision Value 的图表删除。
