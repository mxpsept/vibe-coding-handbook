# FlowOps — Module Boundaries v0.1

> 模块不是菜单、Controller 或数据库表的另一种名字。模块应该围绕稳定业务能力、变化原因和依赖边界形成。

## 1. Candidate Modules

```text
flowops
├── identityaccess
├── supervision
├── progress
├── closure
├── attention
└── audit
```

这些是 Architecture Candidate，不代表必须拆成六个 Maven module 或六个 deployable service。

## 2. Responsibility Map

### identityaccess
Owns:
- current actor identity abstraction；
- roles / scopes required by FlowOps；
- authorization policy integration boundary。

Does not own:
- enterprise HR master data；
- arbitrary business rules。

### supervision
Owns:
- Supervision Item aggregate/core lifecycle facts；
- title/content/source；
- accountability；
- effective deadline facts；
- issue/edit rules belonging to the item。

### progress
Owns:
- append-oriented progress records；
- latest progress query capability；
- progress evidence/history semantics。

Does not directly change Item lifecycle unless an approved application workflow coordinates it.

### closure
Owns application capability around:
- completion claim；
- formal closure decision；
- closure authority validation integration。

It consumes Item state through a public contract; it does not update supervision tables through private repository access.

### attention
Owns:
- Attention query/calculation semantics；
- STALE_UPDATE / NEAR_DUE / OVERDUE projections based on approved rules；
- Attention-oriented read models if later justified。

Attention does not own Lifecycle.

### audit
Owns:
- append-oriented audit evidence for important business actions；
- audit query capability；
- actor/action/time/entity context。

Audit is not a replacement for operational logging.

## 3. Public vs Internal

Each module should conceptually expose:

```text
module
├── api / application contract       ← allowed dependency surface
├── domain                           ← module-owned semantics
└── internal infrastructure          ← not imported by other modules
```

Exact package names depend on language/framework, but the boundary principle remains.

## 4. Allowed Dependency Candidate

```text
Web/API adapters
      ↓
Application capabilities
      ↓
Domain

closure ──public contract──▶ supervision
attention ─public query────▶ supervision/progress
all key actions ───────────▶ audit port
```

Identity/authorization is a cross-cutting boundary consumed through explicit policy abstractions.

## 5. Forbidden Dependency Examples

```text
closure.service
  → supervision.repository.ItemMapper       ❌

attention.service
  → progress.persistence.ProgressEntity     ❌

controller
  → database mapper directly                ❌

supervision.domain
  → web DTO                                 ❌
```

## 6. Cross-module Workflow

Example Completion Claim:

```text
HTTP Request
↓
Closure Application Capability
├── authorize actor
├── read Item state via supervision contract
├── validate transition/business rule
├── persist claim / coordinate transaction
└── append audit evidence
↓
Response
```

具体 transaction boundary 在 backend architecture 中确定。

## 7. Shared Code Rule

不要因为两个模块都需要一个类，就立即创建：

```text
common/
utils/
shared/
```

优先判断：

```text
Is it truly generic infrastructure?
Is it a duplicated domain concept that actually has an owner?
Is duplication temporarily cheaper than a wrong abstraction?
```

Allowed shared candidates:
- technical error envelope；
- clock/id abstractions；
- framework-level security context；
- pagination primitives if stable。

Domain semantics should normally have an owner.

## 8. AI Boundary Rule

Coding Agent modifying one module must:
1. identify owning module；
2. inspect its public contracts；
3. avoid importing another module's internals；
4. report when a new cross-module dependency is required；
5. avoid moving code into `common` solely to resolve a dependency error。

## 9. Boundary Review Questions

- Does the module have one understandable business responsibility?
- Can a new engineer/agent identify where a change belongs?
- Are internal persistence types leaking?
- Are circular dependencies emerging?
- Is a module actually just a technical layer?
- Are we splitting one invariant across modules unnecessarily?

## 10. Open Questions

The exact ownership of Completion Claim persistence and transaction orchestration remains an architecture design point. Do not force a module split that makes a single business invariant impossible to enforce atomically.
