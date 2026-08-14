# FlowOps — Backend Architecture v0.1

## Goal

建立一种对企业业务、测试、长期维护和 Coding Agent 都友好的后端结构，而不是追求目录层级最多。

## 1. Recommended Shape

以 Spring Boot 风格示意，但原则不绑定框架：

```text
com.example.flowops
├── bootstrap
├── sharedkernel        # very small, technical only
├── identityaccess
│   ├── api
│   ├── application
│   ├── domain
│   └── infrastructure
├── supervision
│   ├── api
│   ├── application
│   ├── domain
│   └── infrastructure
├── progress
├── closure
├── attention
└── audit
```

## 2. Layer Responsibilities inside a Module

### api
Inbound/outbound module contract candidates:
- HTTP adapter/controller DTO mapping where project convention chooses；
- public application interfaces/events exposed to other modules。

### application
Use-case orchestration:

```text
IssueItem
UpdateProgress
SubmitCompletionClaim
CloseItem
QueryAttention
```

It coordinates domain, authorization and ports. It should not become a dumping ground for every helper.

### domain
Business semantics:
- entities/value objects；
- invariant/transition rules；
- domain policies where appropriate。

Avoid dependencies on Spring MVC, persistence entities or frontend DTOs.

### infrastructure
Technical adapters:
- database implementation；
- external identity adapter；
- clock/storage/integration implementations。

## 3. Avoid the Global Layered Package Trap

Avoid:

```text
controller/
  50 controllers
service/
  80 services
mapper/
  70 mappers
entity/
  100 entities
utils/
  everything else
```

This groups code by technical type, not by business change. An AI Agent must search the whole repository for one feature.

Prefer feature/domain locality.

## 4. Naming Rules

Names should express business intent.

Prefer:

```text
SubmitCompletionClaimHandler / Service
AttentionQueryService
SupervisionItem
ProgressRecord
```

Avoid vague chains:

```text
TaskManager
TaskProcessor
TaskHelper
TaskCommonService
TaskUtils
```

If a class name cannot explain its responsibility, adding another suffix rarely fixes the design.

## 5. DTO Rules

Do not automatically create:

```text
Entity
DTO
VO
BO
PO
Command
Query
Response
```

for every concept.

Create boundary models when boundaries genuinely differ.

Candidate conventions:
- HTTP Request/Response models at API boundary；
- Command/Query models for meaningful application use cases；
- Domain objects inside domain；
- persistence records/entities inside infrastructure。

Mapping cost is accepted when it protects a meaningful boundary, not as ceremony.

## 6. Repository Rules

Repository interface should express domain/application needs rather than expose arbitrary database operations.

Bad:

```text
BaseMapper<T> available everywhere
```

Better:

```text
SupervisionItemRepository
  findById(...)
  save(...)
  search(specification/page...)
```

Exact abstraction depends on implementation, but other modules must not import internal mapper implementations.

## 7. Transaction Rules

Transaction boundary normally follows an application use case requiring atomic consistency.

Avoid:

```text
@Transactional on every service because template says so
```

and avoid distributed/event complexity unless a real boundary requires it.

State transition + associated required evidence should be designed so partial success does not violate business correctness.

## 8. Error Strategy

Business rejection, authorization rejection, input validation and infrastructure failure are distinct categories.

Do not throw generic:

```text
RuntimeException("操作失败")
```

from every layer.

Detailed Error Contract follows `error-model.md`.

## 9. Time

Deadline/Attention rules depend on time. Avoid scattered direct calls to system time in domain logic.

Candidate abstraction:

```text
Clock / BusinessClock
```

This improves deterministic tests for NEAR_DUE / OVERDUE / STALE_UPDATE.

## 10. Tests

Recommended pyramid by concern:

```text
Domain rule tests
Application use-case tests
Repository/integration tests
API contract tests
Architecture dependency tests
A smaller number of end-to-end tests
```

AI-generated code is not complete merely because it compiles.

## 11. New Library Rule

Before adding a dependency, Coding Agent must state:

```text
problem being solved
existing capability checked
candidate dependency
maintenance/security impact
why standard library/current stack is insufficient
```

Major new framework/category requires Architecture review/ADR.

## 12. AI-friendly Repository Navigation

Each module should ideally include a concise README or architecture note describing:

```text
Responsibility
Public contracts
Key domain concepts
Allowed dependencies
Important rules/tests
```

This reduces repeated repository archaeology and makes fresh Agent sessions safer.
