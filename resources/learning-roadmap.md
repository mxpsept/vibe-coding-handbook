# Vibe Coding Handbook --- Learning Roadmap v1.0

> 本文件是学习地图，不是"100
> 个网站收藏夹"。每个资源必须回答：为什么学、什么时候学、学到什么程度。

## 1. 学习顺序

``` text
Software Engineering Foundations
        ↓
Product Discovery
        ↓
Requirements / Specification
        ↓
Product Design
        ↓
UI / UX / Design System
        ↓
Architecture
        ↓
Context Engineering
        ↓
AI Coding
        ↓
Testing / Verification
        ↓
DevOps
        ↓
AI Application Engineering
```

不要求成为每个领域的专家，但必须具备足以做正确决策的基础能力。

------------------------------------------------------------------------

# 2. Spec-Driven Development

## 学习目标

理解为什么 AI Coding 不应该从代码开始，以及
Spec、Plan、Tasks、Implementation 之间的关系。

### Level A --- Primary Source

**GitHub Spec Kit**

-   Website: https://github.github.com/spec-kit/
-   Repository: https://github.com/github/spec-kit
-   SDD Concepts: https://github.github.com/spec-kit/concepts/sdd.html

重点学习：

-   Spec → Plan → Tasks → Implement；
-   Constitution / governing principles；
-   Clarification；
-   Checklist；
-   Cross-artifact analysis；
-   如何让 Artifact 为下一阶段提供 Context。

注意：Handbook 会吸收其思想，但不会要求所有项目必须使用 Spec Kit。

------------------------------------------------------------------------

# 3. AI Coding / Codex

## 学习目标

理解 Coding Agent 的正确使用方式，而不是记忆某一版 UI。

### Level A --- Primary Source

**OpenAI Codex**

-   Codex: https://openai.com/codex/
-   OpenAI Developers: https://developers.openai.com/
-   Codex GitHub: https://github.com/openai/codex

重点学习：

-   Agent 如何读取仓库；
-   Repository instructions；
-   AGENTS.md；
-   Plan / Execute / Verify；
-   Tool usage；
-   Sandbox / permission boundaries。

工具会持续变化，因此 Handbook 只把工具文档作为"当前实现参考"，不把产品
UI 写入长期方法论。

------------------------------------------------------------------------

# 4. Product Discovery / Requirements

## 学习目标

从"客户想做一个系统"转向理解：

-   谁的问题；
-   为什么值得解决；
-   当前怎么做；
-   目标结果是什么；
-   哪些是假设；
-   哪些是规则；
-   怎样验收。

### 推荐主题

-   Stakeholder Mapping
-   Persona
-   Jobs To Be Done
-   User Story
-   Use Case
-   Business Rule
-   Acceptance Criteria
-   MVP
-   Prioritization

### 建议资源类型

优先寻找：

-   Atlassian Product / Agile 官方学习资料；
-   Product discovery 领域成熟书籍；
-   Scrum / Agile 官方或权威资料；
-   高质量产品团队实践。

本 Handbook 后续会对具体资源逐一审核后加入，而不是一次性堆积链接。

------------------------------------------------------------------------

# 5. UI / UX

## 学习目标

不是培养职业 UI Designer，而是让工程师能够：

1.  分析优秀界面；
2.  建立信息层级；
3.  创建 Wireframe；
4.  选择 Design Direction；
5.  建立 Design System；
6.  判断 AI 生成 UI 是否合格。

### Level A --- Primary Source

**Figma Design Systems**

-   https://www.figma.com/design-systems/
-   https://help.figma.com/hc/en-us/articles/14552901442839-Overview-Introduction-to-design-systems

重点：

-   Styles；
-   Variables；
-   Components；
-   Libraries；
-   Design Tokens；
-   Design / Code consistency。

**Material Design**

-   https://m3.material.io/

重点：

-   Layout；
-   Color；
-   Typography；
-   Component；
-   Interaction；
-   Accessibility。

**Apple Human Interface Guidelines**

-   https://developer.apple.com/design/human-interface-guidelines/

适合学习：

-   Hierarchy；
-   Feedback；
-   Platform conventions；
-   Accessibility；
-   Interaction principles。

**Ant Design**

-   https://ant.design/

适合企业后台、数据密集型应用设计参考。

**Element Plus**

-   https://element-plus.org/

FlowOps Vue Reference App 的基础组件实现参考。

### Level C --- Inspiration

可以研究成熟 SaaS：

-   Linear: https://linear.app/
-   Jira: https://www.atlassian.com/software/jira
-   Asana: https://asana.com/
-   Notion: https://www.notion.com/

研究重点不是"复制皮肤"，而是：

-   信息密度；
-   Navigation；
-   Status；
-   List / Detail；
-   Empty State；
-   Command / Shortcut；
-   Progressive Disclosure。

------------------------------------------------------------------------

# 6. Architecture

## 学习目标

让架构成为 AI Coding 的约束，而不是事后补画的图。

### Level A --- Primary Source

**C4 Model**

-   https://c4model.com/

重点：

``` text
System Context
→ Container
→ Component
→ Code（按需）
```

理解不同抽象层级，而不是在一张图里塞所有技术。

**Architecture Decision Records**

建议学习 ADR 的基本思想：

``` text
Context
Decision
Consequences
```

后续 Handbook 将补充权威 ADR 资源与模板。

------------------------------------------------------------------------

# 7. API Design

## Level A --- Primary Source

**OpenAPI Initiative**

-   https://www.openapis.org/

**OpenAPI Specification**

-   https://spec.openapis.org/oas/latest.html

重点：

-   Contract First；
-   Paths；
-   Schema；
-   Error Model；
-   Examples；
-   API documentation；
-   Frontend / Backend parallel development。

------------------------------------------------------------------------

# 8. Testing / Verification

## 学习目标

建立：

> Agent completion ≠ verified completion

的工程意识。

### Level A --- Primary Source

**Playwright**

-   https://playwright.dev/

重点：

-   E2E；
-   Browser automation；
-   Assertions；
-   Trace；
-   Screenshot；
-   Visual comparison。

其他需要掌握：

-   Unit Test；
-   Integration Test；
-   API Test；
-   Contract Test；
-   Static Analysis；
-   Security Test；
-   Performance Test。

最终形成 Verification Pyramid / Matrix，而不是依赖一种测试。

------------------------------------------------------------------------

# 9. Git / Delivery

## 学习目标

AI 产生的变更必须可审查、可回滚、可追踪。

建议掌握：

-   Git；
-   Branch；
-   Commit；
-   Pull Request；
-   Conventional Commits；
-   CI；
-   Artifact；
-   Container；
-   Environment；
-   Rollback。

核心原则：

``` text
Small Task
  ↓
Small Diff
  ↓
Verification
  ↓
Small Commit
```

------------------------------------------------------------------------

# 10. Context Engineering

## 学习目标

理解真正影响 Coding Agent 表现的不只是 Prompt，而是：

``` text
What context?
How much?
From where?
Which version?
What priority?
For which task?
```

Handbook 将 Context 分成：

1.  Business Context
2.  Product Context
3.  Design Context
4.  Architecture Context
5.  Development Context
6.  Task Context

建议把 Context Engineering
作为贯穿其他阶段的能力，而不是单独的"提示词技巧"。

------------------------------------------------------------------------

# 11. AI Application Engineering

在 FlowOps 基础业务稳定后再学习。

推荐顺序：

``` text
LLM API
 ↓
Structured Output
 ↓
Tool Calling
 ↓
RAG
 ↓
Evaluation
 ↓
MCP
 ↓
Agent
 ↓
Human-in-the-loop
```

原则：

> 不要因为项目使用 AI Coding，就强行给最终产品增加 AI 功能。

AI Feature 必须解决真实业务问题。

------------------------------------------------------------------------

# 12. 推荐学习策略

## 第 1 层：知道概念

能够解释：

-   为什么需要；
-   解决什么问题；
-   什么时候不需要。

## 第 2 层：能够实践

能够独立创建：

-   PRD；
-   Wireframe；
-   Design System；
-   Architecture；
-   Feature Spec；
-   Test Plan。

## 第 3 层：能够 Review AI

这是本 Handbook 最重要的目标。

你不一定需要亲手完成所有工作，但必须能够判断：

> AI 给出的结果是否正确、是否完整、是否值得进入下一 Gate。

------------------------------------------------------------------------

# 13. 学习资源维护规则

每个新增网站必须记录：

-   Category；
-   Level（A/B/C）；
-   Why；
-   Recommended stage；
-   Last reviewed date。

优先级：

``` text
Official / Standard
      ↓
High-quality Engineering Source
      ↓
Community
      ↓
Inspiration
```

避免把搜索引擎排名等同于内容质量。

------------------------------------------------------------------------

# 14. Sprint 1 建议阅读

进入 Handbook Stage 00 前，建议先阅读：

1.  GitHub Spec Kit --- Spec-Driven Development；
2.  GitHub Spec Kit --- workflow；
3.  OpenAI Codex / AGENTS.md 相关官方资料；
4.  Figma --- Introduction to Design Systems。

目标不是立即使用这些工具，而是建立四个意识：

> Specification、Artifact、Context、Verification。
