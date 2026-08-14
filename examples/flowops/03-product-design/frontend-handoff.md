# FlowOps — Product Design → Frontend Handoff v0.1

> 目标不是把一张截图“交给前端还原”，而是交付可实现、可验证、可追踪的 Design Contract。

## 1. Required Handoff Package

每个 Implementation-ready 页面至少包含：

```text
Page ID
Purpose / Primary Job
Actor
Route candidate
Requirement trace
Business Rule trace
Lifecycle / Attention semantics
Wireframe decision
Design Direction
Layout contract
Component hierarchy
Information priority
Interaction rules
Permission rules
Validation
UI states
Responsive behavior
Accessibility
Design System references
Forbidden assumptions
Open gaps
```

## 2. Source Priority

发生冲突时不要由 Coding Agent 猜测。

推荐优先级：

```text
Approved Business Rule / State Model
        ↓
Approved Acceptance Criteria
        ↓
Approved Page Spec
        ↓
Design System
        ↓
Wireframe / High-fi
        ↓
Implementation convenience
```

如果 High-fi 与 Business Rule 冲突，Business Rule 胜出，并创建 Design Issue。

## 3. Screenshot is not Specification

截图不能完整表达：

```text
permission
loading
empty
error
validation
responsive
long content
multiple attention flags
concurrency
business semantics
```

因此禁止仅使用：

```text
“按照这张图 1:1 实现”
```

作为完整开发任务。

## 4. Frontend Implementation Packet Example

```text
Feature: Item Detail

Read first:
- 02-requirements/state-model.md
- 02-requirements/business-rules.md
- 03-product-design/page-specs/item-detail.md
- 03-product-design/design-system.md
- 03-product-design/ui-state-matrix.md

Implement:
- approved page structure
- lifecycle and attention presentation
- progress timeline
- contextual actions
- loading/error/read-only states

Do not implement:
- new business actions
- invented attention types
- auto-close on completion claim
- arbitrary local design tokens

Stop and report if:
- permission semantics are missing
- API contract cannot express required state
- page spec conflicts with business rules
```

## 5. Component Reuse Strategy

Coding Agent 应优先寻找/建立跨页面 Pattern：

```text
LifecycleBadge
AttentionIndicator
PageHeader
FilterBar
EmptyState
ProgressTimeline
ResponsibilitySummary
```

但不要因为“可复用”过早抽象所有内容。

Rule of thumb:

```text
stable repeated semantics → shared component candidate
visual coincidence → not necessarily shared component
```

## 6. Design Token Contract

禁止页面局部任意新增：

```text
hex color
font size
radius
shadow
spacing scale
status semantics
```

需要新增时创建：

```text
DESIGN_SYSTEM_GAP
```

并说明：
- use case；
- existing token why insufficient；
- proposed semantic token。

## 7. UI State Contract

Coding Agent 在 PR 中应声明已实现状态：

```text
[ ] loading
[ ] empty/no-result if applicable
[ ] error
[ ] unauthorized/read-only if applicable
[ ] pending action
[ ] success feedback
[ ] long content
[ ] terminal lifecycle
```

## 8. Visual QA

不要只检查“像不像截图”。

Review：
- hierarchy；
- alignment；
- spacing；
- typography；
- density；
- token usage；
- semantic state；
- long data；
- empty/error states；
- responsive behavior。

## 9. Traceability

最终应形成：

```text
Finding
→ Requirement
→ Business Rule
→ Acceptance Criteria
→ User Flow
→ Page Spec
→ Component/API
→ Code
→ Test
```

这使 UI Bug 可以区分为：

```text
Visual defect
Interaction defect
Specification defect
Business-rule defect
API contract defect
```

而不是全部变成“前端再改一下”。

## 10. Handoff Gate

进入 Coding 前确认：

- [ ] Primary Job 清楚；
- [ ] approved Wireframe direction；
- [ ] Business semantics 无冲突；
- [ ] critical states covered；
- [ ] unresolved blocking gaps = 0；
- [ ] Design System references available；
- [ ] AC 可定位；
- [ ] Coding Agent stop conditions 已声明。
