# 第 3 章：Product Design & UX——让 AI 从“会做页面”升级为“会设计产品”

> 本章解决 Vibe Coding 中最常见、也最容易被低估的问题：**功能实现正确，但页面像一个临时后台。**

AI Coding Agent 很擅长把字段、接口和组件快速拼成页面，但“能生成页面”不等于“完成产品设计”。如果输入只有 PRD 和一句“做得美观一点”，AI 通常会回到它最熟悉的企业后台模式：侧边栏、顶部筛选、四张 KPI 卡片、表格、弹窗、新增表单。

真正专业的 UI，起点不是颜色，而是信息、任务、层级和决策。

---

# 0. 本章目标

完成本章后，你应该能够：

- 在自己没有 UI 灵感时知道第一步做什么；
- 从 Requirements 推导 Information Architecture，而不是直接画页面；
- 建立 Navigation、Page Inventory 和 User Flow；
- 区分业务对象、用户任务和菜单；
- 先做 Low-fidelity Wireframe，再进入视觉设计；
- 建立适合企业系统的 Design System / Design Tokens；
- 使用参考产品而不是盲目让 AI“自由发挥”；
- 把“美观”转换成可讨论、可 Review 的设计维度；
- 让 AI 生成多个 Design Direction 而不是一次定稿；
- 建立 UI State Matrix，覆盖 Loading / Empty / Error / Permission / Long Content；
- 把 High-fidelity Design 转换成 Frontend Specification；
- 使用 Gate 3 判断设计是否真的可以进入前端实现。

---

# 1. 为什么“功能对，但 UI 不好看”如此常见

假设你给 Codex：

```text
开发一个企业督办系统工作台，展示任务总数、办理中、临期、超期、责任单位排名、任务趋势和重点事项。
技术栈 Vue 3 + Element Plus。
```

AI 很可能生成：

```text
┌──────────────────────────────────────────┐
│ KPI │ KPI │ KPI │ KPI                   │
├───────────────────┬──────────────────────┤
│ 饼图              │ 柱状图               │
├───────────────────┴──────────────────────┤
│                    表格                  │
└──────────────────────────────────────────┘
```

功能一个不少。

但你仍然觉得：

> “不高级。”

原因通常不是 `border-radius` 不够漂亮，而是设计过程缺失：

```text
Requirement
   ↓
直接 Coding
```

中间少了：

```text
Information Architecture
User Flow
Page Purpose
Information Priority
Layout Strategy
Interaction Model
Visual Direction
Design System
UI States
```

AI 只能用训练数据里最常见的模式替你补这些决策。

---

# 2. 没有 UI 思路时，第一步不是找颜色

很多工程师打开设计工具后首先想：

```text
蓝色还是绿色？
卡片圆角多少？
背景做不做渐变？
要不要科技感？
```

顺序反了。

第一步应该问：

> **这个页面帮助谁，在什么场景下，完成什么决定或动作？**

例如 FlowOps 管理视图：

错误起点：

```text
我要设计一个领导驾驶舱。
```

更好的起点：

```text
Actor: Manager
Context: 周度管理会议前 / 会议中
Job: 在几分钟内发现需要管理干预的事项
Decision: 哪些事项需要追问、协调资源或升级处理？
```

于是页面设计目标变成：

```text
不是：展示尽可能多的数据
而是：缩短 Attention → Understanding → Action 的路径
```

这就是 Product Design 的起点。

---

# 3. Product Design Pipeline

推荐流程：

```text
Requirements
    ↓
Design Brief
    ↓
Information Architecture
    ↓
Navigation Model
    ↓
Page Inventory
    ↓
Critical User Flows
    ↓
Page Purpose + Information Priority
    ↓
Low-fi Wireframe
    ↓
Design Direction
    ↓
Design System / Tokens
    ↓
High-fi UI
    ↓
State Matrix
    ↓
UX Review
    ↓
Frontend Specification
```

不要跳过前半段直接：

```text
Prompt → 高保真 UI → Vue Code
```

因为越早生成高保真，团队越容易被视觉细节绑架。

---

# 4. Design Brief：把需求翻译成设计任务

设计之前，为每个核心场景建立简短 Design Brief。

FlowOps 示例：

```text
Page: Management Attention View
Primary Actor: Manager
Primary Job: 找出需要管理干预的事项
Primary Action: 打开事项并决定是否协调/追问
Secondary Job: 理解整体执行健康度
Critical Information:
- 为什么需要关注
- 责任部门
- 截止时间
- 最新进展
- 阻塞/依赖
- 最近更新时间
Constraints:
- 桌面 Web
- 会议场景下需要快速扫读
- 不允许把 STALE_UPDATE 等同于 DELAYED
```

这个 Brief 比：

```text
设计一个蓝色科技感驾驶舱
```

对 AI 有价值得多。

---

# 5. Information Architecture：先设计“信息世界”

IA 回答：

```text
系统里有哪些核心对象？
它们是什么关系？
用户如何找到它们？
哪些信息属于同一上下文？
```

FlowOps 可能存在：

```text
Supervision Item
├── Source
├── Accountability
├── Due Date
├── Progress History
├── Attention Flags
├── Completion Claim
└── Audit History
```

注意，这与菜单不是一回事。

错误：

```text
需求有“进度” → 创建“进度管理”菜单
需求有“超期” → 创建“超期管理”菜单
需求有“办结” → 创建“办结管理”菜单
```

最终会出现菜单爆炸。

更合理的是围绕用户 Mental Model 组织：

```text
Work
├── My Work
├── All Supervision Items
└── Attention

Management
└── Management Review

Administration
└── Configuration
```

具体 Navigation 后续通过 Card Sorting / Task Analysis 验证。

---

# 6. 菜单不是数据库表，也不是后端 Controller

AI 生成企业后台时常出现：

```text
任务管理
任务进度管理
任务状态管理
任务类型管理
任务附件管理
任务日志管理
```

这通常是数据库结构泄漏到 UI。

用户并不想“管理任务进度表”。

用户想：

```text
查看任务
更新进度
处理风险
申请办结
```

因此 Navigation 应围绕 **用户任务和业务对象**，而不是技术模块。

---

# 7. Page Inventory：先列页面，不要先画页面

Page Inventory 示例：

| ID | Page | Actor | Primary Job | Priority |
| --- | --- | --- | --- | --- |
| P-001 | My Work | Responsible Participant | 找到需要我处理的事项 | MVP |
| P-002 | Supervision Items | Supervision Specialist | 管理全部事项 | MVP |
| P-003 | Item Detail | Multiple | 理解单项完整上下文 | MVP |
| P-004 | Create / Edit Item | Authorized Staff | 建立事项 | MVP |
| P-005 | Attention | Supervision Specialist | 核验需关注事项 | MVP |
| P-006 | Management Review | Manager | 找到需干预事项 | MVP |
| P-007 | Closure Review | Closure Authority | 审核办结 | MVP candidate |

Page Inventory 能立刻暴露：

```text
重复页面
缺失页面
角色无入口
菜单过多
同一 Job 被拆散
```

---

# 8. Critical User Flow：页面设计前先画路径

例如“责任方提交进度”：

```text
My Work
   ↓
Item Detail
   ↓
Submit Progress
   ↓
Validation
   ↓
Success
   ↓
History Updated
```

设计 Review 时问：

```text
真的需要跳到单独页面吗？
能否在 Detail 内完成？
用户提交后最想看到什么？
失败后输入内容是否保留？
```

再例如 Manager：

```text
Management Review
   ↓
Attention Item
   ↓
Understand Why
   ↓
Inspect Context
   ↓
Decision / Follow-up
```

这比先决定“做 8 张图表”更有效。

---

# 9. Page Purpose：每个页面只能有一个 Primary Job

一个常见失败页面：

```text
Dashboard
├── KPI
├── 趋势
├── 排名
├── 最新任务
├── 我的待办
├── 公告
├── 日历
├── 快捷入口
├── 消息
└── AI 助手
```

看起来“丰富”，但没有焦点。

建议每页定义：

```text
Primary Job
Primary Action
Primary Information
Secondary Information
Rare Actions
```

如果所有信息都是 Primary，实际上没有 Primary。

---

# 10. Information Priority：先排序，再布局

FlowOps Item Detail 可以先建立：

### Level 1 — 决策信息

```text
事项标题
Lifecycle
Attention
责任
Effective Due Date
```

### Level 2 — 当前执行上下文

```text
最新进展
阻塞
更新时间
Completion Claim 状态
```

### Level 3 — 历史与参考

```text
Progress Timeline
附件
Audit
来源材料
```

然后布局自然出现。

如果不排序，AI 往往把所有字段做成同样的：

```text
label: value
label: value
label: value
```

页面就会像数据库详情页。

---

# 11. Wireframe：低保真阶段解决结构，不解决美术

Low-fi Wireframe 应回答：

```text
什么在上面？
什么更重要？
操作在哪里？
哪些内容常驻？
哪些折叠？
滚动后什么仍可见？
```

例如 Item Detail：

```text
┌────────────────────────────────────────────┐
│ Breadcrumb                                  │
│ Task title              [Attention] [State] │
│ Accountable Dept · Due Date                 │
│                         [Update] [Complete]  │
├────────────────────────────────────────────┤
│ Latest Progress / Current Context            │
├─────────────────────────┬──────────────────┤
│ Progress Timeline       │ Key Facts         │
│                         │ Responsibility    │
│                         │ Due Date          │
│                         │ Source            │
├─────────────────────────┴──────────────────┤
│ Audit / Supporting Information              │
└────────────────────────────────────────────┘
```

此时不要讨论阴影、渐变、插画。

---

# 12. 为什么 Wireframe 应至少探索 2–3 个方向

不要让 AI 第一版就成为答案。

例如 Management Review：

### Direction A — Risk Queue

```text
左侧 Attention Queue
右侧 Selected Item Context
```

适合高频逐项处理。

### Direction B — Executive Overview

```text
Summary
↓
Priority Attention
↓
Department / Trend Context
```

适合管理会议。

### Direction C — Workboard

```text
按 Attention / Responsibility 分组的工作板
```

适合协同运营。

让 AI 比较：

```text
哪种更符合 Primary Job？
各自牺牲了什么？
```

比让 AI“再美化一点”有效得多。

---

# 13. Reference-driven Design：不会设计时不要凭空设计

工程师没有成熟 UI 灵感非常正常。

更稳定的方法：

```text
需求场景
   ↓
找 3–5 个同类优秀产品
   ↓
拆解 Pattern
   ↓
提取原则
   ↓
重新组合
```

不是截图照抄，而是分析：

```text
Navigation 怎么组织？
页面密度如何？
详情页如何处理层级？
状态如何表达？
表格操作如何收敛？
Dashboard 如何突出重点？
空状态如何处理？
```

推荐关注成熟 Enterprise Design Systems：

- Ant Design
- Material Design
- Carbon Design System
- Atlassian Design System
- Microsoft Fluent 2

它们的价值不是“组件好看”，而是大量企业交互问题已经被系统化解决。

---

# 14. Moodboard / Design Direction：先定义视觉语言

在 High-fi 前定义 2–3 个方向，例如：

### Direction A — Enterprise Neutral

```text
高信息密度
中性色为主
品牌色克制
边界清晰
适合日常办公
```

### Direction B — Modern Operational

```text
更强的信息层级
轻量卡片
更大的关键数字
Attention 色突出
适合运营/督办
```

### Direction C — Executive Minimal

```text
留白更大
信息更聚焦
减少装饰
强调关键决策信息
适合管理视图
```

不同角色甚至可以共享 Design System，但采用不同 Density Strategy。

---

# 15. Design System：不要每个页面重新“让 AI 发挥”

没有 Design System 时：

```text
Page A 圆角 4
Page B 圆角 8
Page C 圆角 12

蓝色：#1677ff
蓝色：#409eff
蓝色：#2f80ed
```

AI 每次都可能做出“合理但不同”的选择。

Design System 应至少定义：

```text
Color
Typography
Spacing
Radius
Border
Shadow
Icon
Density
Layout/Grid
Component Pattern
State Color
```

---

# 16. Design Tokens：让设计真正可被代码消费

例如：

```text
color.bg.page
color.bg.surface
color.text.primary
color.text.secondary
color.border.default
color.brand.primary
color.attention.nearDue
color.attention.overdue

space.1
space.2
space.3
...

radius.sm
radius.md
```

注意：Token 命名应表达语义，而不是：

```text
blue1
blue2
red3
```

以后换主题、品牌色、暗色模式会容易很多。

---

# 17. 企业系统“高级感”通常来自什么

不是大量：

```text
渐变
发光
玻璃拟态
3D
大圆角
动画
```

企业 UI 的成熟感通常来自：

1. **清楚的信息层级**；
2. **稳定的一致性**；
3. **合理的信息密度**；
4. **克制的颜色**；
5. **准确的对齐与间距**；
6. **高质量 Typography**；
7. **状态表达清楚**；
8. **操作位置可预测**；
9. **复杂信息仍然容易扫描**；
10. **异常状态被认真设计**。

换句话说：

> “高级”更多是秩序感，而不是装饰感。

---

# 18. Density：企业后台不能一味追求“大留白”

AI UI 很容易受到营销网站风格影响：

```text
大标题
大卡片
大留白
每屏只有少量信息
```

但企业操作系统可能需要高频比较和批量处理。

建议定义 Density：

```text
Comfortable
Default
Compact
```

例如：

- Manager Review：偏 Comfortable；
- Task List：Default / Compact；
- Configuration：Default。

不要让所有页面使用同一种视觉密度。

---

# 19. Table Design：企业系统最值得认真设计的组件之一

“Element Plus Table 能显示”不等于 Table UX 完成。

需要考虑：

```text
默认列是什么？
哪些列最重要？
长标题怎么处理？
责任部门如何扫读？
Attention 是否可组合？
操作列是否固定？
筛选是否高频？
是否支持 Saved View？
空状态是什么？
批量操作是否必要？
窄屏怎么办？
```

坏例子：

```text
序号 | 编号 | 标题 | 类型 | 来源 | 部门 | 人员 | 状态 | 进度 | 临期 | 超期 | 时间 | 创建人 | 创建时间 | 操作
```

所有字段都显示通常不是专业，而是没有做信息设计。

---

# 20. Status Design：不要只靠颜色

例如：

```text
红 = 超期
橙 = 临期
灰 = 未更新
```

还需要：

```text
Text label
Icon/shape when useful
Tooltip / explanation
Accessible contrast
Multiple attention handling
```

FlowOps 特别要避免：

```text
红色 = Lifecycle State
```

因为 `OVERDUE` 是 Attention，不是 Lifecycle。

UI 必须延续 Requirements 的语义模型。

---

# 21. UI State Matrix：别只设计“有数据且成功”的截图

每个核心页面至少考虑：

| State | Example |
| --- | --- |
| Loading | 首次加载 |
| Empty | 没有任务 |
| No Search Result | 筛选无结果 |
| Error | API 失败 |
| Partial Error | 图表失败但列表正常 |
| Unauthorized | 无访问权限 |
| Read-only | 有查看权无编辑权 |
| Long Content | 超长标题/进展 |
| Large Data | 大量记录 |
| Pending Action | 正在提交 |
| Success Feedback | 更新成功 |
| Conflict | 数据已被他人修改 |

AI 生成高保真图通常只生成 Happy Path，所以 State Matrix 必须独立存在。

---

# 22. Responsive Strategy：不是简单缩小桌面版

如果产品需要移动端，先问移动场景的 Job 是否相同。

Desktop：

```text
管理大量任务
复杂筛选
比较
会议分析
```

Mobile：

```text
查看我的待办
快速填报进度
查看提醒
审批/确认
```

因此可能是：

```text
Same Domain
Different Task Priority
Different IA
```

而不是把 1440px 表格压进 390px。

---

# 23. 从设计到 Frontend Specification

设计完成后，不应该只交一张 PNG 给 Codex。

至少需要：

```text
Page Purpose
Route
Role / Permission
Layout
Component hierarchy
Design Tokens
Interaction rules
Responsive behavior
UI State Matrix
Validation
Data fields
Business Rule references
Acceptance Criteria references
```

例如：

```text
Page: P-003 Item Detail
Route: /items/:id
Primary Job: understand and act on one supervision item
Lifecycle source: state-model.md
Attention source: BR-005/006/007
Actions:
- Update Progress: only when permitted + IN_PROGRESS
- Submit Completion: BR-008
States:
- loading
- forbidden
- not-found
- read-only
- normal
- pending-closure
- closed
```

这才是 Coding Agent 真正需要的 UI Spec。

---

# 24. AI 在设计阶段的正确角色

AI 可以承担多个角色，但不要混在一个 Prompt：

### IA Agent

负责：信息结构、导航、Page Inventory。

### UX Flow Agent

负责：关键任务路径、异常路径、交互成本。

### Visual Direction Agent

负责：视觉方向和参考 Pattern。

### UI Generator

负责：Wireframe / High-fi 候选方案。

### UX Reviewer

负责：挑战层级、密度、一致性、状态覆盖、可用性。

### Frontend Spec Agent

负责：把批准设计转成实现约束。

推荐：

```text
Generate → Review → Decide → Refine
```

而不是：

```text
Generate → Code
```

---

# 25. 一个更有效的 UI Prompt 结构

弱 Prompt：

```text
帮我设计一个好看的督办系统首页，蓝色科技感。
```

更好的 Prompt：

```text
Role:
You are a senior enterprise product designer.

Product:
FlowOps, enterprise supervision tracking.

Actor:
Manager.

Context:
Weekly management review.

Primary Job:
Identify items requiring management intervention within minutes.

Critical Information:
- attention reason
- accountable department
- effective due date
- latest progress
- blocker/dependency
- last update time

Business Semantics:
- OVERDUE is an attention flag, not lifecycle state.
- STALE_UPDATE does not mean delayed.
- Completion Claim is different from Closure.

Design Goal:
High scanability, professional enterprise UI, restrained visual language.

Do not:
- fill the page with decorative charts;
- use gradients/glow as the primary visual identity;
- show every available field;
- invent business metrics.

Task:
First propose 3 different information/layout directions.
For each explain trade-offs.
Do not produce final visual design yet.
```

这个 Prompt 把 AI 从“画图工具”变成“设计协作者”。

---

# 26. UI Review：不要只问“好不好看”

Review 应拆成：

### Business Semantics
- 是否违反 Business Rule？
- State 是否表达正确？

### Information Architecture
- 用户能否找到目标？
- 页面是否重复？

### Hierarchy
- 第一眼看到的是最重要信息吗？

### Task Efficiency
- 高频动作需要几步？

### Density
- 信息太稀还是太挤？

### Consistency
- 同一概念是否一致表达？

### States
- Loading / Empty / Error / Permission 是否覆盖？

### Visual Quality
- Typography、Spacing、Alignment、Color 是否稳定？

### Accessibility
- 是否只靠颜色？
- 对比度、字号、点击区域是否合理？

于是“我觉得不好看”可以逐渐变成可执行 Feedback。

---

# 27. Case：为什么“四张 KPI 卡片”不是默认答案

需求：

```text
管理者需要了解督办情况。
```

AI 默认：

```text
总任务 36
办理中 18
临期 6
超期 3
```

但应该先问：

```text
管理者下一步要做什么？
```

如果 Job 是“发现需要干预的事项”，那么最重要区域可能是：

```text
Needs Intervention
├── 跨部门阻塞
├── 已超期且无解决计划
├── 临近关键节点
└── 长时间信息未确认
```

KPI 只是 Context，不一定是 Hero Content。

这就是从 Dashboard Thinking 转向 Decision-support Thinking。

---

# 28. Case：列表页不是“搜索表单 + 表格”

传统 AI 页面：

```text
[名称][状态][部门][日期][搜索][重置]

---------------- Table ----------------
```

更成熟的设计可能考虑：

```text
Saved Views
Quick Filters
Attention Views
Search
Column Preferences
Bulk Actions
Sort
Contextual Actions
```

例如：

```text
我的关注 | 临期 | 超期 | 待办结 | 全部
```

但每个 Quick View 都必须有业务语义来源，不能凭设计师想象。

---

# 29. Case：详情页为什么经常“像表单”

AI 很容易复用 Form Layout：

```text
任务名称：xxx
责任部门：xxx
完成时间：xxx
任务来源：xxx
状态：xxx
```

因为实现简单。

但详情页目标是阅读和决策，不是编辑。

可以重新组织：

```text
Title + State + Attention
        ↓
Current Situation
        ↓
Responsibility + Deadline
        ↓
Progress Timeline
        ↓
Supporting Context
```

Display Model 不应该机械复制 Edit Form Model。

---

# 30. Anti-pattern：一开始就让 AI 写 Vue 页面

错误流程：

```text
PRD
 ↓
Codex
 ↓
Vue + Element Plus
 ↓
“不好看”
 ↓
让 Codex 美化
 ↓
不断改 CSS
```

推荐：

```text
PRD
 ↓
IA / Flow
 ↓
Wireframe alternatives
 ↓
Human Decision
 ↓
Design System
 ↓
High-fi
 ↓
UX Review
 ↓
Frontend Spec
 ↓
Codex
```

这样“审美问题”会大幅减少，因为你把设计决策提前了。

---

# 31. Gate 3 — Product Design → Architecture / Implementation Readiness

## IA
- [ ] 核心业务对象与导航关系明确
- [ ] 菜单不是数据库表映射
- [ ] Page Inventory 完整

## User Flow
- [ ] 核心 Job 有完整 Flow
- [ ] 高频操作路径足够短
- [ ] Error / Permission / Cancel 等路径已考虑

## Page Design
- [ ] 每页有 Primary Job
- [ ] Information Priority 已定义
- [ ] 页面不是简单字段平铺
- [ ] Detail / List / Workbench 有明确 Pattern

## Visual
- [ ] Design Direction 已由 Human 选择
- [ ] Token / Typography / Spacing / State Color 一致
- [ ] 不依赖装饰制造“高级感”

## State Coverage
- [ ] Loading
- [ ] Empty
- [ ] No Result
- [ ] Error
- [ ] Unauthorized / Read-only
- [ ] Long Content
- [ ] Pending / Success

## Requirement Integrity
- [ ] UI 没有改变 Business Rule
- [ ] Attention 与 Lifecycle 表达没有混淆
- [ ] UI 新增业务概念已返回 Requirements Review

## Frontend Handoff
- [ ] Route / Component hierarchy 明确
- [ ] Action permission 明确
- [ ] Responsive strategy 明确
- [ ] Design Tokens 可实现
- [ ] AC / Rule Trace 可定位

## Decision
- [ ] PASS
- [ ] PASS WITH GAPS
- [ ] HOLD
- [ ] RETURN TO REQUIREMENTS

---

# 32. Learning Resources

## Nielsen Norman Group
https://www.nngroup.com/articles/ten-usability-heuristics/

重点学习可用性启发式原则，用来建立 UX Review 的基础框架。

## Ant Design
https://ant.design/docs/spec/introduce/

非常适合企业中后台产品，建议重点研究 Layout、Table、Form、Feedback、Data Display，而不只是复制组件代码。

## Material Design 3
https://m3.material.io/

适合理解 Design Tokens、Color、Typography、Layout 和组件状态体系。

## IBM Carbon Design System
https://carbondesignsystem.com/

非常值得研究复杂企业产品的信息密度、Data Table、Structured List、Notification 等 Pattern。

## Atlassian Design System
https://atlassian.design/

适合研究任务型 SaaS 产品、Navigation、Tokens、Content Design 和复杂协作界面。

## Microsoft Fluent 2
https://fluent2.microsoft.design/

适合理解大型生产力软件的 Design System 思路。

## Figma
https://www.figma.com/

用于 Wireframe、Design System、Component、Prototype 与 Developer Handoff。

## Mobbin
https://mobbin.com/

用于研究真实产品界面 Pattern。重点是拆解 Pattern，不是照抄页面。

## Page Flows
https://pageflows.com/

适合研究真实产品 User Flow 和交互路径。

---

# 33. 下一步：FlowOps Product Design 实战

下一组 Artifact：

```text
examples/flowops/03-product-design/
├── design-brief.md
├── information-architecture.md
├── navigation.md
├── page-inventory.md
├── user-flows.md
├── page-specs/
├── wireframes/
├── design-directions.md
├── design-system.md
├── ui-state-matrix.md
└── frontend-handoff.md
```

同时补充：

```text
templates/product-design/
prompts/product-design/
checklists/product-design/
```

我们不会直接从“做一个漂亮首页”开始，而是先设计 FlowOps 的信息结构、页面职责和关键任务流，再逐渐进入真正的 UI。
