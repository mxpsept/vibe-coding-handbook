# Vibe Coding 实战：AI Native 企业级软件开发实践手册

> 从模糊业务想法到可验证、可部署、可持续演进的软件系统。

## 1. 项目定位

`vibe-coding-handbook` 是一套面向企业软件开发的 AI Native
实践手册。它不把重点放在"如何写一个更长的
Prompt"，而是建立一套可复用的软件工程流程，使 ChatGPT、Codex、Claude
Code、Cursor、Gemini CLI 等 AI
工具在明确的业务、设计、架构和验证约束下工作。

目标读者：

-   软件工程师、架构师、技术负责人；
-   已经使用 AI Coding，但经常遇到需求漂移、UI
    不稳定、代码越改越乱等问题的开发者；
-   希望在企业团队中建立 AI 辅助研发规范的人；
-   希望从"Vibe Coding"进一步走向 Spec-Driven / Artifact-Driven /
    Verification-Driven Development 的团队。

## 2. 核心问题

本手册围绕一个问题展开：

> 当我们只有一个模糊的软件想法，甚至不知道 UI 应该长什么样时，如何利用
> AI，把想法逐步转化为真正可以上线的软件？

本手册不推荐：

``` text
Idea → Prompt → Code
```

推荐：

``` text
Idea
 ↓
Discovery
 ↓
Specification
 ↓
Product Design
 ↓
UI/UX Design
 ↓
Architecture
 ↓
Planning
 ↓
Build
 ↓
Verification
 ↓
Ship
 ↓
Feedback
 ↓
Next Specification
```

## 3. 核心原则

### 3.1 Human defines intent

人负责目标、价值判断、关键决策和最终验收。

### 3.2 Spec defines truth

重要需求和决策不能只存在聊天记录中。经确认的 Artifact 才是 Project
Truth。

### 3.3 AI executes within constraints

AI 是强大的研究者、设计协作者、实现者、Reviewer
和测试协作者，但不应在缺乏约束时自行决定企业系统的核心业务规则。

### 3.4 Verification closes the loop

"AI 说完成了"不等于完成。代码、UI、接口、测试和 Acceptance Criteria
都需要可验证证据。

### 3.5 Chat is temporary; Artifacts persist

``` text
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

## 4. 全生命周期模型

本手册采用：

> **Idea → Discovery → Spec → Design → Architecture → Plan → Build →
> Verify → Ship → Iterate**

并进一步引入：

-   Product Discovery
-   Specification Driven Development
-   Artifact Driven Development
-   Context Engineering
-   Design System
-   Architecture Decision Records
-   Contract First API
-   Agentic Coding Workflow
-   Verification Engineering
-   Human-in-the-loop
-   AI Native Application Engineering

## 5. 贯穿案例：FlowOps

全书使用完全虚构的企业案例：

> **FlowOps --- 企业任务督办与协同管理平台**

背景：

某中大型企业长期通过
Excel、即时通讯、邮件和线下会议管理重点任务，逐渐出现任务来源分散、责任边界模糊、办理进度难跟踪、临期超期发现不及时、管理者缺乏整体视图等问题。

项目从一句模糊需求开始：

> 希望建设一套重点任务督办系统，把重点工作统一管理起来，明确责任、跟踪进度、自动提醒临期和超期事项，并帮助管理者掌握整体执行情况。

手册不会提前把完整答案交给读者，而是陪同 FlowOps 依次经历
Discovery、PRD、业务建模、IA、User Flow、Wireframe、Design
System、Architecture、Coding、Testing 和 Production。

FlowOps 不使用任何真实企业名称、人员、数据、内部系统截图或专有业务资料。

## 6. Handbook 组成

``` text
vibe-coding-handbook/
├── handbook/       # 方法论和完整教程
├── templates/      # PRD、ADR、Feature Spec 等模板
├── prompts/        # 分阶段 AI Prompt
├── checklists/     # Quality Gate 检查表
├── examples/       # FlowOps 等案例产物
├── resources/      # 学习路线和外部资源
└── assets/         # 图、截图、示意图
```

四类内容分别解决：

  内容         回答的问题
  ------------ ----------------------------
  Handbook     应该怎样开发？
  Templates    规范产物应该怎样写？
  Prompts      怎样让 AI 协助完成？
  Checklists   怎样判断真的完成？
  Examples     一个真实企业案例怎样落地？

## 7. AI Coding 成熟度模型

### Level 1 --- Prompt Driven

``` text
帮我开发一个督办系统。
```

适合探索和原型，不适合作为复杂企业项目的长期工作方式。

### Level 2 --- Context Driven

AI 在开发前读取项目上下文、业务规则、设计规范和架构约束。

### Level 3 --- Spec Driven

Feature 开发由 Feature Spec、Acceptance Criteria、API Contract、Design
Spec 和 Architecture Constraints 驱动。

### Level 4 --- Agentic Workflow

``` text
Explore → Plan → Implement → Test → Review → Fix → Verify
```

Human 主要负责 Decision、Approval、Risk 和 Acceptance。

## 8. 如何阅读

### 路线 A：准备开发一个新系统

按 Stage 00 → 12 顺序阅读，并同步创建自己的项目 Artifact。

### 路线 B：已经在使用 Codex 等 Coding Agent

重点阅读：

1.  Foundations
2.  UI/UX
3.  Context Engineering
4.  Planning
5.  AI Coding
6.  Testing & Review

### 路线 C：团队建立 AI 研发规范

重点阅读：

1.  Spec-Driven Development
2.  Artifact Governance
3.  Context Engineering
4.  Architecture
5.  Quality Gates
6.  Verification Engineering
7.  Team / Multi-Agent Workflow

## 9. 外部学习资源原则

手册中的资源分为：

-   **Level A --- Primary Source**：官方文档、正式标准、项目官方资料；
-   **Level B --- High Quality
    Community**：高质量开源项目、工程团队文章、会议、大学课程；
-   **Level C --- Inspiration**：设计灵感、社区经验和案例参考。

任何社区经验都不应自动升级为项目规范。

## 10. 当前状态

当前版本：`Foundation v1.0`

当前 Sprint：

> **Sprint 0 --- Handbook Foundation**

首批 Artifact：

-   `README.md`
-   `MASTER-OUTLINE.md`
-   `CONTRIBUTING.md`
-   `examples/flowops/CASE-SPEC.md`
-   `resources/learning-roadmap.md`

下一 Sprint：

> **Sprint 1 --- Foundations：从 Vibe Coding 到 AI Native Software
> Engineering**

------------------------------------------------------------------------

**核心信条**

> Human defines intent. Spec defines truth. AI executes. Verification
> closes the loop.
