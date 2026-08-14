# FlowOps — Frontend Architecture v0.1

## Goal

让页面、业务语义、Design System 与 API 调用有稳定归属，避免随着 AI 开发不断出现新的目录风格、请求封装和状态管理方式。

## 1. Candidate Structure

以 Vue/React 均可映射的概念结构示意：

```text
src/
├── app/
│   ├── router/
│   ├── providers/
│   └── shell/
├── design-system/
│   ├── tokens/
│   ├── primitives/
│   └── patterns/
├── features/
│   ├── workbench/
│   ├── my-work/
│   ├── supervision-items/
│   ├── attention/
│   └── management-review/
├── api/
│   ├── client/
│   └── generated-or-contract/
└── shared/
    └── small technical utilities only
```

具体目录必须适配现有项目，不应为了符合文档强制重构成熟仓库。

## 2. Feature Locality

一个 Feature 尽量让 Agent 在局部目录理解：

```text
features/attention/
├── pages/
├── components/
├── queries-or-services/
├── models/
└── tests/
```

不要把同一功能拆散到：

```text
views/
components/
api/
store/
types/
utils/
```

五个全局目录后再让 Agent 全仓库搜索。

## 3. Design System Ownership

Global visual semantics belong to Design System:

```text
LifecycleBadge
AttentionIndicator
PageHeader
FilterBar
EmptyState
Typography / spacing / color tokens
```

Feature-specific business composition stays inside Feature。

不要把：

```text
AttentionSelectedItemContext
```

因为“可能复用”过早放进 global components。

## 4. API Access

Choose one project-wide API strategy.

```text
Feature
↓
approved query/service layer
↓
shared API client
↓
Backend
```

Avoid:
- component direct fetch in some pages；
- global request wrapper elsewhere；
- second HTTP library for one feature；
- response envelope parsing duplicated everywhere。

## 5. Server State vs Client UI State

Do not put all data into a global store by default.

Separate conceptually:

```text
Server State
UI State
Form State
Cross-feature Session/App State
```

Use the project's selected tooling consistently. New state-management technology requires a Driver, not preference.

## 6. Domain Semantics in UI

Frontend may present known rules, but server remains source of truth.

Example:

```text
canShowCompletionClaim = UX derivation
POST completion claim authorization = backend decision
```

Do not encode a second independent business engine in the browser.

## 7. Type/Contract Strategy

API contract types should be generated or centrally modeled where practical.

Avoid multiple manually drifting definitions:

```text
ItemDto
TaskItem
SupervisionItemVO
ItemModel
```

representing the same API payload in unrelated folders without reason.

## 8. Page Composition

Pages orchestrate feature components and data states.

Avoid 1,500-line pages containing:

```text
API calls
business rules
formatters
all modal code
all table columns
all CSS
```

But also avoid splitting every 5-line fragment into a component. Extract around stable semantics and meaningful testing/reuse boundaries.

## 9. Styling

Preferred order:

```text
Design System token
→ approved component/pattern
→ feature-local composition style
```

Forbidden by default:

```text
random hex
random spacing
new shadow
new radius
new status color
```

When needed: `DESIGN_SYSTEM_GAP`.

## 10. Routing / Permission

Route visibility and button visibility improve UX but are not security controls.

Frontend should handle:

```text
unauthorized route
forbidden action response
expired session
read-only state
```

without leaking protected data.

## 11. Error Handling

Global infrastructure handles technical common cases; Feature handles domain-relevant recovery.

Example:

```text
401 → session/auth flow
network unavailable → common feedback
409 conflict → feature explains data changed and refresh required
business validation → action/form context
```

## 12. AI Rules

Coding Agent must not:
- create another HTTP client；
- introduce another global state library；
- add page-local design tokens；
- duplicate a stable Design System component；
- move feature code into `shared` merely to avoid imports；
- encode new business rules from UI assumptions；
- perform broad architecture refactor during a page task without approval。

## 13. Frontend Architecture Fitness Candidates

- import boundary lint rules；
- token lint/style rules；
- TypeScript strictness where applicable；
- API schema/type validation；
- component/unit tests；
- visual regression for stable critical components；
- route/access tests。
