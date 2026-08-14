# 04 — 从零开始：没有 UI 思路时如何完成企业系统设计

> 这一节专门解决一个高频 Vibe Coding 问题：**我知道系统要做什么，但完全不知道页面应该长什么样。**

答案不是先打开 Codex 说“帮我设计一个现代化页面”，而是把 UI 创意问题拆成一条可以重复执行的工作流。

---

## 1. 先接受一个事实：你不需要先成为视觉设计师

企业软件的 UI 质量主要来自四件事：

```text
正确的信息架构
+ 正确的用户流程
+ 正确的信息层级
+ 一致的视觉系统
```

视觉创意当然重要，但它不是第一步。

如果前三项错误，再漂亮的颜色、圆角、图表也只能得到一个“漂亮但难用”的系统。

---

# 2. Zero-to-UI Workflow

```text
Requirement
↓
Job Extraction
↓
Reference Research
↓
Pattern Library
↓
IA / Navigation
↓
Critical Flow
↓
Page Inventory
↓
Information Priority
↓
2–3 Wireframe Directions
↓
Human Selection
↓
Visual Direction
↓
Design System
↓
High-fi / Prototype
↓
UX Review
↓
Page Spec
↓
Frontend Handoff
↓
Codex Implementation
↓
Visual + Functional QA
```

后续每个新系统都可以重复这条链路。

---

# 3. Step 1 — 不要先找“好看的后台”，先提取 Job

假设我们准备设计一个企业督办系统 FlowOps。

错误起点：

```text
我要做一个任务管理系统，帮我设计首页。
```

AI 很可能生成：

```text
4 KPI Cards
2 Charts
1 Ranking
1 Recent Tasks Table
```

正确起点先问：

```text
谁在用？
他为什么打开这个页面？
他离开页面前希望完成什么？
```

例如：

```text
督办人员：找到需要核验的事项，并判断是否需要跟进。
执行人员：知道自己现在需要做什么，并提交真实进展。
管理者：找到需要管理干预的事项，并快速理解原因。
```

此时页面结构已经开始自然出现。

---

# 4. Step 2 — Reference Research：不要抄产品，研究 Pattern

没有设计灵感时，参考成熟产品是正确做法，但不要搜索：

```text
best admin dashboard UI
```

然后复制一张 Dribbble 图。

应该按 Job 搜索 Pattern，例如：

```text
issue triage interface
project task detail timeline
approval queue enterprise UX
work management inbox
incident management dashboard
enterprise data table filters
```

## 推荐学习来源

- urlMobbinhttps://mobbin.com/：观察真实产品 Flow 与页面 Pattern。
- urlPage Flowshttps://pageflows.com/：研究真实用户流程，而不是孤立截图。
- urlFigma Communityhttps://www.figma.com/community：查找 Design System、Enterprise UI 与 Wireframe 参考。
- urlMaterial Designhttps://m3.material.io/：学习组件、状态、布局和交互原则。
- urlAnt Designhttps://ant.design/：企业中后台 Pattern 与组件设计参考。
- urlAtlassian Design Systemhttps://atlassian.design/：复杂协作型企业产品的重要参考。
- urlIBM Carbon Design Systemhttps://carbondesignsystem.com/：大型企业软件的信息密度、组件和设计体系参考。
- urlNielsen Norman Grouphttps://www.nngroup.com/：UX 原则、研究和可用性方法。

研究时记录的不是“这个蓝色很好看”，而是：

```text
Reference
Pattern
Why it works
Which Job it serves
What not to copy
Applicable page
```

---

# 5. Step 3 — 建立 Reference Board

为项目建立：

```text
design-references.md
```

示例：

| Reference Pattern | Observation | FlowOps Use |
| --- | --- | --- |
| issue triage split view | list + selected context reduces navigation | Attention |
| activity timeline | preserves event history | Item Detail |
| inbox/action queue | action-first instead of analytics-first | My Work |
| dense enterprise table | efficient comparison | All Items |
| executive review | intervention first, analytics second | Management Review |

关键规则：

> **Borrow patterns, not pixels.**

---

# 6. Step 4 — 先画信息，不画视觉

Wireframe 阶段禁止讨论：

```text
蓝色还是紫色
圆角 8 还是 12
阴影多重
渐变方向
```

只讨论：

```text
什么应该第一眼看到？
什么应该一起出现？
什么应该隐藏到下一层？
动作在哪里？
```

例如 Item Detail 第一版：

```text
Title
Lifecycle + Attention
Responsibility + Deadline
Latest Progress
Timeline
Facts
Actions
```

这比直接让 AI 生成“高级详情页”稳定得多。

---

# 7. Step 5 — 强制 AI 一次给 3 个结构方向

不要问：

```text
帮我设计这个页面。
```

改成：

```text
基于 Primary Job，提出三个明显不同的信息结构方案。
每个方案必须说明：
- information hierarchy
- primary interaction
- strengths
- weaknesses
- suitable user
- risk

此阶段不要定义颜色、字体、阴影。
不要改变 Business Rules。
```

例如 Management Review：

```text
A Executive Overview
B Attention Split View
C KPI-first Dashboard
```

然后进行 Human Selection。

AI 的价值在这里不是替你决定，而是扩大你的设计搜索空间。

---

# 8. Step 6 — 用 Job 选择方案，不用“我觉得漂亮”

评价每个方案：

| Dimension | Question |
| --- | --- |
| Job Fit | 是否最快支持 Primary Job？ |
| Scanability | 用户能否快速找到重点？ |
| Context | 操作前是否理解上下文？ |
| Navigation Cost | 是否频繁跳页面？ |
| Density | 是否适合数据规模？ |
| Rule Integrity | 是否扭曲业务模型？ |
| Scalability | 数据变多后是否仍成立？ |
| Mobile Potential | 是否存在自然移动端策略？ |

这样 UI Review 从：

```text
我感觉不好看
```

升级为：

```text
这个方案把 Attention 放在第三屏，与 Manager 的 Primary Job 不匹配。
```

---

# 9. Step 7 — 再选择视觉方向

结构批准后才进入 Visual Direction。

可以要求 AI 给出：

```text
A Enterprise Neutral
B Modern Operational
C Executive Minimal
```

每个方向描述：

```text
Typography
Density
Surface
Border
Radius
Color usage
Hierarchy
Suitable pages
Risks
```

不要用：

```text
现代、科技、高端、大气
```

这种无法执行的形容词作为全部 Design Brief。

---

# 10. Step 8 — 建 Design System，而不是逐页 Prompt

如果系统有 30 个页面，却对每个页面分别告诉 AI：

```text
设计得现代一点
```

最终一定产生 Style Drift。

应先定义：

```text
Color semantics
Typography roles
Spacing scale
Radius
Elevation
Density
Page Header
Filter Bar
Table/List
Form
Lifecycle Badge
Attention Indicator
Timeline
Empty/Error State
```

以后页面只消费规则。

---

# 11. Step 9 — High-fi 不是终点

High-fi 完成后，主动测试：

```text
0 条数据
100 条数据
超长标题
超长部门名
多个 Attention
接口失败
无权限
只读
提交中
重复点击
终态事项
窄屏
```

如果设计只在“完美 Demo 数据”下成立，它还没有准备好开发。

---

# 12. Step 10 — 让另一个 AI 扮演 UX Reviewer

不要让生成方案的同一个上下文直接宣布自己通过。

Reviewer 应寻找：

```text
business semantic violation
weak hierarchy
unnecessary navigation
missing states
random design tokens
fake metrics
AI-default dashboard
form-like detail
card everywhere
```

然后由 Human Review 决定。

---

# 13. Step 11 — 转换成 Page Spec

设计图批准后不要立即 Coding。

把设计转换成：

```text
Primary Job
Trace
Information Priority
Layout Contract
Component Hierarchy
Actions
Permissions
Validation
States
Responsive
Accessibility
Forbidden Assumptions
```

这就是 Design → Code Contract。

---

# 14. Step 12 — 给 Codex 一个受控 Implementation Packet

推荐任务结构：

```text
Goal
Read First
Implement
Reuse
Acceptance Criteria
UI States
Do Not
Stop Conditions
Verification
```

而不是：

```text
做一下这个页面，参考附件。
```

---

# 15. 完整 FlowOps 小案例

需求：

```text
督办人员需要核验超期、临期和长时间未更新事项。
```

### Job

```text
快速知道哪些事项需要关注、为什么、最新发生了什么。
```

### Pattern Research

发现：
- Table：扫描快但理解上下文需要跳转；
- Split View：Queue + Context 适合连续核验；
- Kanban：一个事项多 Attention 时语义冲突。

### Wireframe Decision

```text
Attention Split View
```

### Visual Direction

```text
Modern Operational
```

### Design System

```text
LifecycleBadge != AttentionIndicator
```

### Page State

```text
Loading
Empty
Filter No Result
Error
Selected Item Error
Multiple Attention
Long Content
```

### Page Spec

定义 Queue、Selected Context、Actions、Forbidden Assumptions。

### Codex

实现批准 Pattern，不自行新增“催办”和“风险评分”。

### Review

发现如果页面把 `STALE_UPDATE` 写成“任务停滞”，则 RETURN，因为 Evidence 只证明“没有新的进展信息”。

这就是从 Requirement 到 Production UI 的完整闭环。

---

# 16. 当你真的毫无思路时，使用这个启动脚本

```text
1. 不生成 UI。
2. 阅读 Requirements。
3. 列出 Actor + Primary Jobs。
4. 为每个 Job 推荐应研究的成熟 UX Pattern。
5. 给出 Reference Research keywords。
6. 建 Page Inventory。
7. 选择一个 Critical Page。
8. 只做 3 个低保真结构方案。
9. 对比优缺点。
10. 等待 Human Decision。
```

这十步完成后，你通常已经不再处于“完全没 UI 思路”的状态。

---

# 17. 核心结论

Vibe Coding 时代，UI 能力不再意味着你必须独立画出每一个像素。

更重要的新能力是：

```text
提出正确问题
找到正确参考
识别正确 Pattern
约束 AI 搜索空间
比较多个方案
做出 Human Decision
沉淀 Design System
把设计转换成 Code Contract
```

因此真正稳定的方法不是：

```text
Prompt → Pretty UI
```

而是：

```text
Requirement
→ Job
→ Research
→ Pattern
→ Structure
→ Alternatives
→ Decision
→ System
→ Specification
→ Code
→ Review
```

这套过程才具有可重复性。
