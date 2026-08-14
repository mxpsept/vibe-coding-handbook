# 01 — Vibe Coding 时代的软件架构：给 AI 自由，但不给架构漂移自由

> Stage 04 的目标不是提前设计所有技术细节，而是建立一个足够稳定的技术决策边界，让人和 Coding Agent 可以持续开发，而不会每个 Prompt 都重新发明项目。

## 1. 为什么 AI Coding 更需要 Architecture

传统开发中的架构漂移通常是渐进的；AI Coding 会把它放大。

常见现象：

```text
Sprint 1: axios
Sprint 2: 新 Agent 引入另一个 request wrapper
Sprint 3: React Query / Pinia / custom store 混用
Sprint 4: Service + Repository + Manager + Handler 同时存在
Sprint 5: DTO / VO / BO / Command / Query 命名失控
Sprint 6: 每个模块有自己的错误处理方式
```

每一次局部修改可能都“能运行”，但系统整体正在失去一致性。

因此：

```text
Working Code != Coherent System
```

## 2. Architecture 的真正作用

Architecture 不是一张复杂图，而是一组：

```text
Boundaries
Decisions
Constraints
Contracts
Quality Attributes
Evolution Rules
```

它回答：

```text
系统被分成什么？
模块之间如何依赖？
哪些技术选择已经决定？
哪些仍然开放？
数据和权限在哪里做最终判断？
错误如何跨边界传播？
未来变化应该落在哪里？
Coding Agent 什么情况下必须停止？
```

## 3. Architecture Workflow

```text
Requirements + Product Design
↓
Quality Attributes
↓
System Context
↓
Architecture Drivers
↓
Candidate Architecture
↓
Technical Spikes where uncertainty is high
↓
Architecture Decisions / ADR
↓
Container / Module Boundaries
↓
Domain + Data Model
↓
API / Error / Permission Contracts
↓
Frontend + Backend Architecture
↓
Security / Observability / Deployment
↓
Architecture Review
↓
Implementation Guardrails
```

## 4. Architecture Drivers before Framework Choice

不要先问：

```text
Vue 还是 React？
MyBatis 还是 JPA？
Redis 要不要上？
要不要微服务？
```

先提取 Drivers：

```text
Expected scale
Security sensitivity
Consistency requirements
Auditability
Availability
Integration constraints
Team capability
Deployment environment
Change frequency
Operational complexity tolerance
```

技术是对 Driver 的响应，不是架构的起点。

## 5. Prefer the simplest architecture that protects the domain

企业 MVP 常见误区：

```text
AI 很会写代码
→ 我们可以直接微服务
→ Kafka + Redis + Elasticsearch + Gateway + Scheduler
```

结果是 AI 同时维护更多边界、配置、失败模式和测试组合。

推荐原则：

```text
Start simple
Make boundaries explicit
Keep evolution paths open
Add distributed complexity only for a proven driver
```

对于 FlowOps 这类案例，Modular Monolith 往往比“为了架构感而微服务”更适合作为初始候选。

## 6. Architecture Artifact Set

Stage 04 推荐最小集合：

```text
architecture-overview.md
quality-attributes.md
system-context.md
module-boundaries.md
domain-model.md
data-model.md
api-contract.md
permission-model.md
error-model.md
frontend-architecture.md
backend-architecture.md
security.md
observability.md
deployment.md
ADRs/
```

不是每个项目都需要同等深度，但核心决策必须有 Source of Truth。

## 7. ADR — 防止 AI 重复讨论已经决定的问题

Architecture Decision Record 记录：

```text
Context
Decision
Alternatives
Consequences
Status
```

例如：

```text
ADR-001: Start as Modular Monolith
ADR-002: REST JSON API for MVP
ADR-003: Server is authorization source of truth
ADR-004: Append-oriented progress history
```

以后 Coding Agent 不应该每次重新问：

```text
要不要改成微服务？
```

除非新的 Architecture Driver 使 ADR 失效。

## 8. Decision vs Preference

必须区分：

```text
Architecture Decision
Architecture Guideline
Implementation Preference
Open Question
```

例如：

```text
Decision: 服务端负责最终权限校验
Guideline: 业务模块避免跨模块直接访问内部 Repository
Preference: 优先使用已有 utility
Open: 是否需要 Redis cache
```

如果所有内容都写成“必须”，Architecture 会僵化；如果全部是建议，AI 会漂移。

## 9. Dependency Direction

一个稳定系统必须能回答：

```text
谁可以依赖谁？
谁不可以依赖谁？
```

例如模块化单体候选：

```text
Web/API
  ↓
Application
  ↓
Domain
  ↑
Infrastructure implements ports
```

以及业务模块之间通过公开 Application/API Contract 协作，而不是：

```text
module-a service
→ module-b repository
→ module-c mapper
```

## 10. AI Stop Conditions

Coding Agent 应在以下情况停止并报告：

```text
需要引入新的 framework/library category
需要改变已批准 ADR
需要跨越模块边界访问内部实现
API 无法表达 Requirement
Data Model 与 State Model 冲突
权限语义未知
需要新的 distributed component
需要改变 transaction boundary
需要新增新的全局 abstraction
```

Stop 不是失败，而是 Architecture Governance。

## 11. Architecture Fitness

架构不是文档写完就结束。

后续可以通过：

```text
lint rules
module dependency tests
architecture tests
API schema validation
migration checks
security tests
CI gates
```

把一部分规则自动化。

目标：

```text
Architecture as executable constraints where practical
```

## 12. Stage 04 Exit

进入大规模 Feature Implementation 前至少回答：

- 系统边界是什么？
- 模块如何划分？
- 核心 Domain Model 是否稳定？
- Lifecycle 如何持久化？
- API Contract 如何表达业务语义？
- 权限最终在哪里校验？
- Error Contract 是否统一？
- 前后端依赖规则是什么？
- 关键技术选择是否有 ADR？
- 部署/安全/可观测性是否满足 MVP？
- Coding Agent 的 Architecture Stop Conditions 是否明确？

如果这些问题都交给每个 Coding Prompt 临时决定，项目实际上还没有准备好进入 AI 高速开发。
