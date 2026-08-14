# FlowOps — Architecture Overview v0.1

> Synthetic Teaching Case。此文档消费 Requirements 与 Product Design，不重新定义业务规则。

## 1. Architecture Goals

FlowOps MVP 的架构目标：

```text
Protect business semantics
Support fast enterprise feature delivery
Keep module boundaries understandable to humans and AI
Provide auditable state transitions
Avoid premature distributed complexity
Make permissions enforceable server-side
Make future integration possible
```

## 2. Architecture Drivers

### Business
- 企业督办事项全生命周期；
- Progress History 可追踪；
- Completion Claim 与 Closure 分离；
- Attention 可解释；
- 多角色访问。

### Quality
- Correctness > extreme throughput；
- Auditability 高；
- Security / authorization 高；
- Maintainability 高；
- Availability 中高；
- horizontal scale 暂非首要 Driver。

### Delivery
- MVP 需要快速迭代；
- 团队需要降低部署和分布式调试成本；
- Coding Agent 必须在稳定 Boundary 中工作。

## 3. Initial Architecture Candidate

```text
Browser
   ↓ HTTPS
Frontend Web Application
   ↓ REST/JSON
FlowOps Backend — Modular Monolith
   ├── Identity / Access boundary
   ├── Supervision Item module
   ├── Progress module/boundary
   ├── Attention query capability
   ├── Closure capability
   └── Audit capability
   ↓
Relational Database
```

Module 划分仍需通过 Domain Model 进一步验证；上图不是数据库表拆模块。

## 4. Why Modular Monolith First

当前没有明确 Driver 证明需要独立微服务。

Modular Monolith 提供：
- 单部署单元；
- 本地 transaction 简单；
- 较低 operational cost；
- 明确模块边界；
- 后续可按真实变化/扩展压力拆分。

它不等于：

```text
one giant package
all services call all repositories
```

模块边界仍需治理。

## 5. Frontend Candidate

```text
App Shell
├── Routing / Access UI
├── Shared Design System
├── Feature Modules
│   ├── workbench
│   ├── my-work
│   ├── supervision-items
│   ├── attention
│   └── management-review
├── API Client
└── Shared Infrastructure
```

页面可以复用 Domain-aware components，但避免建立一个无法理解的 `components/common` 巨型目录。

## 6. Data

MVP 首选 Relational Database，因为：
- Lifecycle / responsibility / deadline 结构化；
- transaction consistency 有价值；
- audit/query 需求明确；
- 当前没有文档数据库 Driver。

具体数据库产品在 ADR 中决定。

## 7. API

MVP candidate：REST + JSON。

原则：

```text
API expresses domain actions
!=
CRUD-only table endpoints
```

例如候选：

```text
POST /items/{id}/progress-updates
POST /items/{id}/completion-claims
POST /items/{id}/closure
```

优于用一个万能：

```text
PUT /items/{id} { status: ... }
```

直接修改状态。

## 8. Authorization

```text
Frontend visibility = UX
Backend authorization = security source of truth
```

需要建立 Permission Model，至少覆盖：
- read scope；
- create/edit/issue；
- progress update；
- completion claim；
- closure。

## 9. Attention

Attention 首先视为由业务事实计算/查询的维度，而不是 Item Lifecycle 字段。

实现策略（实时计算、查询投影、持久化 projection）需结合数据规模和规则复杂度决定，不在 Product Design 中拍脑袋。

## 10. Audit

关键业务动作必须产生可追踪 Evidence：

```text
who
what action
when
entity
before/after or semantic event context where appropriate
```

Audit 不等同应用日志。

## 11. External Systems

MVP 暂无强制外部集成。未来通知、组织目录/SSO 等通过明确 Integration Boundary 引入。

不要提前因为“以后可能接”就加入 MQ / ES / Redis。

## 12. Open Architecture Questions

```text
ARCH_GAP-001: Identity/SSO source for teaching case?
ARCH_GAP-002: Closure Authority mapping?
ARCH_GAP-003: expected item/progress data scale?
ARCH_GAP-004: Attention calculation frequency / SLA?
ARCH_GAP-005: attachment storage in MVP?
ARCH_GAP-006: notification channel in MVP?
```

这些 Gap 在影响实现前解决；不能由 Coding Agent默认选择。
