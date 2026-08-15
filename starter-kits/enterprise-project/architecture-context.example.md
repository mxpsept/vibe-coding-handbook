# Architecture Context — Example

## System Shape

```text
Web UI
→ Application/API
→ Domain/Policy
→ Persistence / Integration Ports
→ Infrastructure Adapters
```

具体框架不是本 Artifact 的重点；重点是 Owner 和 Dependency Direction。

## Domain Ownership

| Concern | Owner |
| --- | --- |
| task lifecycle/source facts | Item/Task domain |
| progress submission | Progress capability |
| derived attention | Attention policy |
| authorization/data scope | Authorization policy/service |
| external messages | Notification integration |

## Rules
- frontend 不作为 permission/domain rule Source of Truth；
- attention reason 不污染 lifecycle enum；
- external provider DTO 不进入 core domain；
- shared utility 不能成为无边界业务逻辑垃圾桶；
- 跨模块读取/写入必须遵守 approved contract。

## Data
- timestamps 存储/传输策略必须统一；
- audit-sensitive mutations 记录 actor/time/intent/result；
- schema migration 必须可评估 rollback/compatibility；
- 不因 UI 方便而重复持久化可可靠派生的数据，除非有明确 performance/history driver。

## API
API 表达稳定业务语义，而不是直接暴露数据库表结构。

Errors 至少区分：validation、authorization、conflict/state、not found、integration/system failure。

## Quality Drivers
第一阶段重点：correctness、authorization、auditability、maintainability、可观测的 integration failure。

## ADR Triggers
遇到以下情况写 ADR：
- 新数据库/消息中间件/搜索引擎；
- authentication/authorization strategy；
- sync vs async integration；
- significant module boundary change；
- irreversible data model choice；
- organization-wide framework/convention。

## Agent Boundary
Coding Agent 可以在既有边界内实现 Feature；不能因为局部实现方便就改变 Domain Owner、引入基础设施或重定义 Permission Model。
