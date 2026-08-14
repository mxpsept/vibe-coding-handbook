# 第 0 章：从 Vibe Coding 到 AI Native Software Engineering

> 本章不是劝你停止使用 Vibe Coding，而是帮助你判断：什么时候可以“跟着感觉快速做”，什么时候必须把 AI 纳入工程约束。

## 0. 本章目标

完成本章后，你应该能够：

- 区分 Vibe Coding、AI-assisted Development 与 AI Native Software Engineering；
- 理解为什么“功能能跑”不等于“企业软件可以交付”；
- 识别 AI Coding 中最常见的需求、UI、架构、代码和验证失控模式；
- 建立 Human / AI 的职责边界；
- 从 `Idea → Prompt → Code` 转向 `Intent → Artifact → Execution → Verification`；
- 在真正写代码前形成第一个项目 Artifact：`project-idea.md`；
- 使用 Gate 0 判断一个想法是否值得进入 Product Discovery。

---

# 1. Why：为什么需要重新理解 Vibe Coding

AI Coding 最容易给开发者一种错觉：软件开发已经从复杂工程活动变成了自然语言输入问题。

例如，我们可以直接告诉 Coding Agent：

```text
帮我开发一个企业督办管理系统。

要求：
- Vue 3 + Element Plus；
- Spring Boot；
- 支持任务创建、下达、进度填报、催办、办结；
- 有领导驾驶舱；
- 页面专业、美观、有高级感。
```

几分钟后，AI 可能已经创建：

- 登录页；
- Dashboard；
- 菜单；
- CRUD；
- 数据表；
- API；
- 图表；
- 权限代码。

第一次运行甚至可能“看起来不错”。

问题在于：**生成速度掩盖了决策缺失。**

AI 在生成这些内容时，不得不替项目做大量没有被明确授权的决定：

```text
谁可以创建督办事项？
谁负责下达？
任务是否需要签收？
一个任务能否有多个责任部门？
延期是否需要审批？
什么叫“临期”？
任务达到 100% 是否等于办结？
办结是否需要审核？
领导驾驶舱真正需要回答什么问题？
不同角色看到的数据范围是否相同？
```

如果这些问题没有答案，Coding Agent 仍然可以继续写代码。

它只是会用自己的假设填补空白。

于是项目很容易出现一种危险状态：

> **代码已经非常具体，而需求仍然非常模糊。**

这正是企业项目中需要警惕的 AI Coding 失控点。

---

# 2. Concepts：Vibe Coding 到底是什么

“Vibe Coding”一词由 Andrej Karpathy 在 2025 年提出。它最初描述的是一种高度放手的编程方式：开发者主要通过自然语言与模型交互，接受生成结果、运行程序、继续描述问题，而不再把阅读和理解每一段生成代码作为核心活动。

这种模式的价值是真实存在的。

它特别适合：

- 周末实验；
- 一次性工具；
- 技术可行性验证；
- UI 概念探索；
- Demo；
- Throwaway Prototype；
- 快速验证“这个想法能不能工作”。

但要注意一个非常重要的概念边界：

> **使用 AI 写代码，不等于 Vibe Coding。**

如果 AI 写了大量代码，但工程师仍然阅读变更、理解设计、执行测试、检查安全风险并对最终结果负责，那么这更准确地属于 AI-assisted Software Development，而不是原始意义上的 Vibe Coding。

Martin Fowler 对 Vibe Coding 的讨论也强调了类似风险：不阅读 AI 生成代码的方式可以用于低风险、可丢弃的软件，但在可维护性、正确性和安全性要求更高的生产系统中会产生明显问题。

因此，本 Handbook 不把“Vibe Coding”当成贬义词，也不把它泛化成所有 AI Coding。

我们使用下面的区分：

| 模式 | 核心特征 | 典型场景 |
| --- | --- | --- |
| Vibe Coding | 目标驱动、快速生成、低审查、允许丢弃 | Prototype / Experiment |
| AI-assisted Development | AI 参与编码，但 Human 对代码和决策负责 | 日常软件研发 |
| Agentic Development | Agent 可自主 Explore / Plan / Implement / Test，但在约束和 Gate 内运行 | Feature Delivery |
| AI Native Software Engineering | AI 贯穿 Discovery、Design、Architecture、Coding、Verification，Artifact 和 Gate 维持工程秩序 | 企业级长期项目 |

这些不是互相排斥的工具选择，而是不同的**工程控制级别**。

---

# 3. When：什么时候可以 Vibe，什么时候必须工程化

一个简单判断方法是看“失败成本”。

## 3.1 可以大胆 Vibe 的场景

如果一个软件满足大部分条件：

- 生命周期很短；
- 用户很少；
- 没有敏感数据；
- 没有关键业务规则；
- 出错不会产生严重损失；
- 代码未来可以直接丢弃；
- 目标是学习或验证想法；

那么快速 Vibe Coding 往往是合理选择。

此时过早建立几十份文档、ADR 和复杂测试体系，反而可能成为浪费。

## 3.2 应该进入工程模式的场景

当系统开始出现以下特征时，应逐步增加工程约束：

- 多角色；
- 多部门；
- 权限和数据权限；
- 复杂状态流转；
- 审批或审计；
- 长期维护；
- 多人协作；
- 前后端协作；
- 外部系统集成；
- 数据不可随意丢失；
- 安全、合规或性能要求；
- 需要持续迭代数年。

这时真正的问题已经不再是：

> AI 能不能把这个页面写出来？

而是：

> 我们如何保证 AI 每一次快速执行，都仍然服务于正确的业务目标，并且不会破坏系统已经确认的事实？

---

# 4. 为什么 Prototype 成功不代表 Enterprise Software 成功

Prototype 通常回答：

> **Can it work?**

企业软件还必须回答：

```text
Should we build it?
Are we building the right thing?
Does it match the real workflow?
Can different roles use it correctly?
Is the UI understandable?
Is the architecture sustainable?
Is the data correct?
Is it secure?
Can it be tested?
Can it be operated?
Can another engineer maintain it six months later?
Can we safely change it?
```

因此：

```text
Prototype Success
        ≠
Product Success
        ≠
Production Readiness
        ≠
Long-term Maintainability
```

AI 极大降低了 Prototype 的成本，但没有自动消除后面这些工程问题。

某种意义上，它反而让这些问题更容易被推迟，因为“看得见的功能”出现得太快。

---

# 5. AI Coding 的五类典型失效模式

## 5.1 Requirement Hallucination：AI 替业务做决定

输入：

```text
开发一个督办系统。
```

AI 可能直接生成：

```text
待发布 → 已发布 → 进行中 → 已完成
```

但真实业务也许需要：

```text
拟稿 → 下达 → 签收 → 办理 → 申请办结 → 审核办结
```

问题不是 AI “写错代码”，而是项目根本没有给它足够的业务事实。

### 原则

> Unknown 应保持 Unknown，不能因为 AI 能生成答案，就把猜测升级为 Requirement。

---

## 5.2 UI by Guessing：功能正确，界面却不好用

常见 Prompt：

```text
页面太丑了，帮我优化得高级一点。
```

Agent 可能：

- 改成渐变背景；
- 增加阴影；
- 加大圆角；
- 添加更多卡片；
- 换一套颜色。

结果仍然不满意。

因为真正缺失的可能不是 CSS，而是：

```text
Page Goal
Information Hierarchy
Layout
Visual Reference
Design Direction
Design Token
Component Pattern
State
Interaction
```

因此 UI 问题不能长期靠“再漂亮一点”解决。

后续 Stage 03 / 04 会把 UI 从主观感觉转换为可讨论、可复用、可验证的 Design Artifact。

---

## 5.3 Architecture Drift：每次功能都合理，系统整体越来越乱

Agent 在 Task A 中可能选择一种实现；Task B 又选择另一种；Task C 为了快速完成再引入一个新的 Library。

单次 Diff 都能解释，但累计以后可能出现：

```text
Controller 直接写业务
Service 又有另一套规则
DTO / VO / Entity 混用
错误响应格式不统一
权限校验散落各处
重复工具类越来越多
前端每个页面都有自己的请求封装
```

根因往往不是模型不会写代码，而是缺少持续有效的 Architecture Context。

---

## 5.4 Context Drift：聊天越来越长，项目事实越来越模糊

典型过程：

```text
第 1 天：讨论需求
第 3 天：修改需求
第 7 天：重新讨论 UI
第 12 天：换一个 Agent
第 20 天：没人记得哪次讨论才是最终结论
```

如果项目事实只存在聊天记录中，AI 和 Human 都会逐渐失去可靠上下文。

因此 Handbook 建立一个核心原则：

> **Chat is temporary; Artifacts persist.**

```text
Conversation
    ↓
Decision
    ↓
Artifact
    ↓
Git
    ↓
Project Truth
```

---

## 5.5 Completion Illusion：AI 说完成了，但没有证据

Agent 常见输出：

```text
已完成任务管理功能：
✓ 新增
✓ 编辑
✓ 删除
✓ 权限控制
✓ 异常处理
```

这不是 Verification Evidence。

真正的验证可能包括：

```text
Build Result
Unit Test Result
Integration Test Result
API Response
E2E Result
Screenshot
Visual Comparison
Acceptance Criteria Mapping
Security / Performance Evidence
```

因此本书采用：

> **Agent completion ≠ Verified completion.**

---

# 6. 从“Prompt 写得更长”到“Context 组织得更好”

面对 AI 输出不稳定，一个常见反应是继续增加 Prompt：

```text
请使用 Vue3...
请遵守 RESTful...
请使用统一返回结构...
页面要专业...
按钮放右边...
代码必须规范...
不要修改其他文件...
数据库字段使用...
权限规则是...
```

最终形成一个几千字的超级 Prompt。

它同时承担：

- PRD；
- Design Spec；
- Architecture；
- Coding Convention；
- Task Spec；
- Acceptance Criteria。

这是一种脆弱的 Context 管理方式。

更稳定的方式是：

```text
Current Task
     +
Relevant Artifacts
     +
Explicit Constraints
     +
Acceptance Criteria
     +
Verification Requirements
```

例如：

```text
实现“督办事项列表”Feature。

开始前读取：
- features/task-list/spec.md
- docs/design-system.md
- api/openapi.yaml
- docs/architecture/frontend.md

仅实现 tasks.md 中 T01-T04。
不要修改任务状态模型。
完成后运行指定测试并报告 Verification Evidence。
```

这里 Prompt 变短了，但 Context 反而更强。

---

# 7. 从 Prompt-Driven 到 Spec-Driven

GitHub Spec Kit 是当前值得研究的 Spec-Driven Development 实践之一。它把核心过程组织为：

```text
Spec → Plan → Tasks → Implement
```

并通过 Clarify、Checklist、Analyze、Converge 等步骤增加质量控制。

本 Handbook 不要求项目必须采用 Spec Kit，也不会照搬它的目录结构。

我们吸收的是一个更重要的思想：

> **先让 Intent 逐步变成可审查的 Artifact，再让 Agent 根据 Artifact 执行。**

对于完整企业系统，仅有 Feature Spec 仍然不够，因此 Handbook 将生命周期扩展为：

```text
Idea
 ↓
Discovery
 ↓
Requirements
 ↓
Product Design
 ↓
UI / UX
 ↓
Context Engineering
 ↓
Architecture
 ↓
Planning
 ↓
AI Coding
 ↓
Testing & Review
 ↓
DevOps
 ↓
Evolution
```

注意：这不是要求所有项目执行瀑布式流程。

Artifact 可以迭代，阶段可以回退，小型项目也可以合并阶段。

关键不是“流程越多越专业”，而是：

> 在高成本决策发生前，把对应的不确定性降低到可接受水平。

---

# 8. 从 Chat-Driven 到 Artifact-Driven

## 8.1 Chat 的作用

Chat 非常适合：

- 探索；
- Brainstorm；
- 提问；
- 比较方案；
- Challenge 假设；
- Review；
- 临时推理。

但 Chat 不应该天然成为 Project Truth。

## 8.2 Artifact 的作用

Artifact 是经过确认、可以持续引用的项目资产，例如：

```text
project-idea.md
vision.md
prd.md
business-rules.md
user-flows.md
design-system.md
openapi.yaml
ADR-001.md
feature-spec.md
tasks.md
test-plan.md
```

Artifact 的价值不只是“写文档”。

它承担三个作用：

### 对 Human

让团队可以 Review、讨论、批准和追踪决策。

### 对 AI

提供稳定、结构化、版本化的 Context。

### 对项目

形成可以随着代码一起演进的 Project Truth。

因此：

```text
Good Conversation
      ↓
Decision
      ↓
Persist
      ↓
Artifact
      ↓
Version Control
      ↓
Reusable Context
```

---

# 9. Human 与 AI 的职责边界

AI 能力越来越强，因此职责边界不应该定义为：

```text
Human 写需求
AI 写代码
```

AI 完全可以参与需求分析、UI、架构、测试和 Review。

真正的边界是**决策责任**。

| 工作 | AI | Human |
| --- | --- | --- |
| 发现未知问题 | 强 | 确认哪些问题值得调查 |
| 搜集候选方案 | 强 | 判断适用性 |
| 需求草拟 | 强 | 对业务事实负责 |
| UI 方案探索 | 强 | 判断目标用户和设计方向 |
| 架构候选 | 强 | 对 Trade-off 和长期成本负责 |
| 编码 | 强 | 对合入代码负责 |
| 测试生成 | 强 | 定义关键风险与验收标准 |
| Review | 强 | 对最终 Acceptance 负责 |
| 业务规则决策 | 提供建议 | **最终决策** |
| 风险接受 | 分析风险 | **最终决策** |

可以概括为：

```text
Human defines intent.
Spec defines truth.
AI executes within constraints.
Verification closes the loop.
Human accepts the outcome.
```

Human-in-the-loop 的意义不是每一步都人工操作，而是在关键 Decision Gate 上保留明确责任。

---

# 10. AI Native Software Engineering

本 Handbook 使用 **AI Native Software Engineering** 描述一种工程工作方式，而不是某个具体产品或正式行业标准。

在本书中，它指：

> 将 AI 作为贯穿软件生命周期的工程协作者，同时使用 Artifact、Context、Version Control、Quality Gate 与 Verification 来约束和验证 AI 的执行，使 Human 能够把更多精力放在 Intent、Decision、Risk 和 Acceptance 上。

核心模型：

```text
              Human Intent
                   │
                   ▼
             Discovery / Spec
                   │
                   ▼
            Project Artifacts
                   │
                   ▼
          Context Selection
                   │
                   ▼
              AI Execution
                   │
                   ▼
             Verification
                   │
             ┌─────┴─────┐
             │           │
           Fail         Pass
             │           │
        Fix / Update   Human Gate
             │           │
             └─────┬─────┘
                   ▼
               Next Slice
```

AI Native 并不意味着“AI 自己开发整个系统”。

更成熟的状态恰恰是：**AI 获得更大的执行空间，同时系统拥有更明确的约束、证据和责任边界。**

---

# 11. 从“生成代码”到 Verification Loop

传统的一次性 AI Coding 循环经常是：

```text
Prompt → Generate → Run → Looks OK → Done
```

本 Handbook 推荐：

```text
Explore
  ↓
Plan
  ↓
Implement
  ↓
Test
  ↓
Review
  ↓
Fix
  ↓
Verify
  ↓
Acceptance
```

Verification 不应该等到项目最后才发生。

不同阶段有不同证据：

| 阶段 | Verification Example |
| --- | --- |
| Discovery | Stakeholder 是否确认问题存在 |
| Requirements | Acceptance Criteria 是否明确 |
| Product Design | User Flow 是否覆盖关键任务 |
| UI | Screenshot / Visual Review |
| Architecture | ADR / Architecture Review |
| API | Contract Test |
| Coding | Build / Unit / Integration Test |
| Feature | E2E + Acceptance Criteria Mapping |
| Release | Release Checklist / Smoke Test |

这意味着 Verification 是生命周期，而不是测试部门最后的一道工序。

---

# 12. 企业 AI Coding 成熟度模型

成熟度不是看团队用了多少 AI 工具，而是看 AI 产生的变更是否越来越**可控、可验证、可持续**。

## Level 1 — Prompt-Driven

```text
Idea → Prompt → Code
```

特征：

- 依赖聊天上下文；
- 需求大量隐含；
- 经常 Accept All；
- UI 靠反复描述调整；
- 测试不稳定。

适合快速实验。

## Level 2 — Context-Driven

```text
Task + Repository Context → Agent
```

开始有：

- README；
- Coding Rules；
- AGENTS.md；
- Architecture Notes；
- Design Guidelines。

Agent 不再每次从零猜测项目。

## Level 3 — Spec / Artifact-Driven

```text
Intent
 ↓
Artifact
 ↓
Review
 ↓
Agent Execution
```

Feature 有明确：

- Scope；
- Business Rules；
- Design Spec；
- API Contract；
- Acceptance Criteria；
- Task Plan。

## Level 4 — Verification-Driven Agentic Workflow

```text
Spec
 ↓
Agent Plan
 ↓
Implement
 ↓
Automated Verification
 ↓
Reviewer Agent
 ↓
Human Gate
```

Agent 获得更大自主性，但“完成”必须有 Evidence。

## Level 5 — AI Engineering Operating Model

团队进一步建立：

- Artifact Governance；
- Multi-Agent Workflow；
- 自动 Quality Gate；
- Context Freshness；
- Traceability；
- Security Boundary；
- AI Engineering Metrics；
- 持续改进机制。

本 Handbook 的目标不是要求每个项目都达到 Level 5，而是让团队知道：

> **什么时候应该增加哪一种工程能力。**

---

# 13. FlowOps Case：如果我们直接让 AI 开发督办系统

现在正式进入贯穿全书的虚构案例 FlowOps。

当前唯一经过确认的初始事实是：

> Northstar Group 长期通过 Excel、即时通讯、邮件和会议跟踪重点任务，随着任务增加出现信息分散、责任不清、进度更新不及时、临期超期发现困难以及管理者缺少整体执行视图等问题，希望探索一套重点任务督办系统。

此时我们故意做两个实验。

## 13.1 实验 A：直接 Coding

Prompt：

```text
使用 Vue3 + Element Plus + Spring Boot 开发一个企业督办系统。

包含：
- Dashboard
- 督办事项
- 我的任务
- 催办
- 统计分析
- 系统管理

页面要求专业、美观。
```

Agent 很可能能够迅速生成系统骨架。

但我们立刻 Review：

```text
为什么是这些菜单？
谁定义了任务状态？
谁拥有催办权限？
任务来源有哪些？
责任人与责任部门是什么关系？
是否存在协办？
延期如何处理？
什么叫完成？
Dashboard 的指标是谁提出的？
页面信息优先级来自哪里？
```

如果这些答案只是“AI 认为通常应该这样”，那么生成结果不是 Project Truth。

实验 A 的结论不是“AI 不好用”，而是：

> **我们让执行能力进入得太早。**

## 13.2 实验 B：禁止 Coding，先暴露 Unknowns

Prompt：

```text
我们正在探索一个企业任务督办系统。

当前只知道：
某中大型企业长期通过 Excel、即时通讯、邮件和会议跟踪重点任务，
存在信息分散、责任不清、进度更新不及时、临期超期发现困难、
管理者缺少整体执行视图等问题。

现在禁止：
- 设计数据库；
- 选择技术架构；
- 生成页面代码；
- 假设最终功能；
- 替业务方决定流程。

请：
1. 区分已知事实、假设和未知项；
2. 找出在进入 Product Discovery 前最需要澄清的问题；
3. 判断这个想法目前是否值得继续探索；
4. 输出一个简短 project-idea 草案。
```

这一次 AI 的价值从“替我们生成系统”变成：

> **帮助 Human 更快发现自己还不知道什么。**

这将是 FlowOps 的正确起点。

---

# 14. Practice：把你的项目压缩成 3～5 句话

在打开 Coding Agent 之前，先完成一个练习。

不要写功能清单。

尝试只回答：

```text
1. 谁正在遇到问题？
2. 现在是怎样工作的？
3. 最大的问题是什么？
4. 为什么现在值得解决？
5. 希望产生什么业务结果？
```

例如，不要写：

```text
我要做一个任务系统，有工作台、任务列表、统计分析、消息提醒、权限管理……
```

而应该先写：

```text
某中大型企业通过 Excel、会议和即时通讯跟踪跨部门重点工作。
随着任务增加，责任关系、进度和截止日期难以持续跟踪。
督办人员需要频繁人工询问，管理者也难以快速识别风险事项。
团队希望探索一种统一的数字化方式，让重点任务的责任、进展和风险更透明。
当前尚未确认具体流程、角色边界和最终功能范围。
```

第二种描述故意保留 Unknown。

这是好事。

---

# 15. Prompt：Idea Analysis Prompt

下面的 Prompt 可以用于任何新项目的 Stage 00。

```text
你是我的 Product Discovery 协作者。

我们目前处于 Idea 阶段，不是 Implementation 阶段。

【项目想法】
<用 3～5 句话描述业务背景、当前问题和期望结果>

你的目标不是帮我立即设计完整系统，而是帮助我判断这个想法是否值得进入 Discovery。

请严格遵守：
1. 不编写代码；
2. 不设计数据库；
3. 不自行确定技术栈；
4. 不把常见行业做法直接当作我们的需求；
5. 不把你的推测写成事实；
6. 明确区分 Fact / Assumption / Unknown；
7. 如果信息不足，保留 Unknown，而不是补齐答案。

请输出：

A. Problem Statement
B. Target Users / Stakeholders（当前假设）
C. Known Facts
D. Assumptions
E. Unknowns
F. Expected Outcomes
G. Major Risks
H. Discovery Questions
I. 是否建议进入 Discovery，以及原因
J. project-idea.md 草案

最后执行一次 Self Review：
- 是否偷偷发明了业务规则？
- 是否过早定义了解决方案？
- 是否把 Feature 当成 Problem？
- 是否存在必须由 Human 确认的关键假设？
```

注意：Prompt 只是执行入口。

最终确认的内容应该进入 Artifact，而不是永远留在聊天记录里。

---

# 16. Expected Artifact：project-idea.md

Stage 00 不需要 PRD。

第一个 Artifact 应该足够轻量：

```markdown
# Project Idea

## 1. Background

## 2. Problem Statement

## 3. Target Users / Stakeholders

## 4. Known Facts

## 5. Assumptions

## 6. Unknowns

## 7. Expected Outcomes

## 8. Constraints

## 9. Risks

## 10. Discovery Questions

## 11. Decision
- [ ] Enter Discovery
- [ ] Need more information
- [ ] Stop / Park

## 12. Human Approval
```

为什么不是直接写 PRD？

因为此时我们的目标不是证明“已经知道要开发什么”，而是准确表达：

> **我们为什么考虑做这件事，以及还有什么不知道。**

---

# 17. Bad Practice：Stage 00 最常见的错误

## 错误 1：把功能清单当需求发现

```text
用户管理
任务管理
统计分析
消息中心
```

这是 Solution Inventory，不是 Problem Discovery。

## 错误 2：让 AI 一次性生成完整系统方案

```text
请完整设计需求、UI、数据库、接口、架构并生成代码。
```

速度很快，但所有层级的假设混在一次输出中，很难 Review。

## 错误 3：为了“专业”制造大量文档

Artifact-Driven 不等于 Documentation-Heavy。

一个两天的内部工具可能只需要：

```text
README + Feature Spec + Tests
```

而不是 30 份文档。

## 错误 4：把 AI 建议自动升级为项目事实

AI 可以说：

```text
督办系统通常需要延期审批。
```

正确记录方式是：

```text
Assumption / Discovery Question:
我们的业务是否存在延期？如果存在，是否需要审批？
```

而不是直接写入 Requirement：

```text
系统必须支持三级延期审批。
```

## 错误 5：过早讨论技术栈

如果连问题是否值得解决都没有确认，争论 PostgreSQL 还是 MySQL、微服务还是单体通常没有意义。

技术约束可以作为 Constraint 被记录，但 Architecture Decision 应在拥有足够业务上下文后发生。

---

# 18. Review：如何判断 Stage 00 做得是否合格

Review `project-idea.md` 时，不要问“写得专业吗”，而要问：

```text
Problem 是否比 Solution 更清楚？
Fact 与 Assumption 是否分开？
Unknown 是否被诚实保留？
是否知道需要找哪些 Stakeholder？
是否知道下一步应该调查什么？
是否过早冻结 Feature？
是否过早冻结 UI？
是否过早冻结 Architecture？
```

一个优秀的 Idea Artifact 不一定答案很多。

它往往只是让团队非常清楚地知道：

> **我们知道什么、认为可能是什么、还不知道什么，以及下一步应该向谁求证。**

---

# 19. Gate 0：是否值得进入 Discovery

在进入 Stage 01 前，由 Human 做最终判断。

## Gate 0 Checklist

### Problem

- [ ] 能用 3～5 句话描述业务问题；
- [ ] 描述没有退化成功能清单；
- [ ] 至少能识别主要受影响人群；
- [ ] 有理由相信问题真实存在。

### Context

- [ ] 已知事实与假设已经分开；
- [ ] 关键 Unknown 已记录；
- [ ] 没有让 AI 自行补齐核心业务规则。

### Value

- [ ] 能说明为什么值得继续调查；
- [ ] 有初步 Expected Outcome；
- [ ] 没有把“上线一个系统”本身当作唯一 Outcome。

### Scope Control

- [ ] 尚未把候选功能误认为最终范围；
- [ ] 尚未因为 AI 已经能写代码就提前进入 Build；
- [ ] 技术方案没有反过来绑架业务问题。

### Next Step

- [ ] 知道下一阶段需要访谈或确认哪些 Stakeholder；
- [ ] 已形成 Discovery Questions；
- [ ] Human 明确批准进入 Discovery。

如果关键项无法通过，不意味着项目失败。

正确动作通常是：

```text
More Information
      ↓
Update project-idea.md
      ↓
Review Again
```

而不是：

```text
信息不够
  ↓
让 AI 猜
  ↓
开始 Coding
```

---

# 20. 本章形成的第一个完整闭环

至此，我们完成了 Handbook 的第一个工程循环：

```text
Business Idea
     ↓
AI-assisted Analysis
     ↓
Fact / Assumption / Unknown
     ↓
project-idea.md
     ↓
Human Review
     ↓
Gate 0
     ↓
Product Discovery
```

这套流程看起来比“一句话让 AI 开始开发”慢。

但对于长期企业项目，它通常是在用几十分钟或几个小时的显式思考，避免未来数天甚至数周围绕错误假设生成代码。

真正需要追求的不是：

> **How fast can AI generate code?**

而是：

> **How fast can Human + AI move from uncertainty to verified value without losing engineering control?**

这也是后续所有章节的主线。

---

# 21. Learning Resources

以下资料用于进一步理解本章概念。资源等级遵循本仓库 `CONTRIBUTING.md` 的 Level A / B / C 规则。

## Level A — Primary Source

### GitHub Spec Kit

- Documentation: https://github.github.com/spec-kit/
- What is Spec-Driven Development: https://github.github.com/spec-kit/concepts/sdd.html
- Quick Start: https://github.github.com/spec-kit/quickstart.html
- Agentic SDD Reference: https://github.github.com/spec-kit/reference/agentic-sdd.html

**为什么阅读：** 观察一个成熟工具如何把 `Spec → Plan → Tasks → Implement` 组织为 Agent 可执行流程，并在中间增加 Clarify、Checklist、Analyze、Converge 等质量环节。

**本章阅读深度：** 理解思想即可，暂时不需要安装。

## Level B — High Quality Engineering Source

### Martin Fowler — Vibe Coding

- https://martinfowler.com/bliki/VibeCoding.html

**为什么阅读：** 理解 Vibe Coding 在低风险、可丢弃软件与生产软件之间的适用边界，以及可维护性、正确性和安全性问题。

### Simon Willison — Vibe Coding / Agentic Engineering

- https://simonwillison.net/2025/Mar/19/vibe-coding/
- https://simonwillison.net/guides/agentic-engineering-patterns/what-is-agentic-engineering/

**为什么阅读：** 理解“AI-assisted programming 不等于 Vibe Coding”，以及为什么工程师仍然需要对 AI 生成的软件承担理解、测试和交付责任。

---

# 22. 下一章

Gate 0 通过后，不应该立即创建 Vue 或 Spring Boot 项目。

下一步进入：

> **Stage 01 — Discovery：从模糊想法发现真正的问题**

FlowOps 将第一次真正面对 Stakeholder、As-Is Process、Pain Point、Jobs To Be Done 和业务访谈。

同时，我们会把本章定义的轻量 Artifact 真正落地为：

```text
templates/project/project-idea.template.md
examples/flowops/00-project/project-idea.md
prompts/foundations/idea-analysis.prompt.md
checklists/foundations/discovery-readiness.md
```

从下一步开始，Handbook 不只是“讲方法”，而是逐步形成一套可以直接复制到新企业项目中的 AI Native Engineering Toolkit。
