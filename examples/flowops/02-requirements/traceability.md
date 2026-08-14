# FlowOps — Requirement Traceability v0.1

> Traceability 的目的不是制造文档负担，而是回答：**为什么做、规则来自哪里、如何证明做对了。**

## 1. Traceability Chain

```text
Evidence
  ↓
Finding / Job
  ↓
Scope / User Story
  ↓
Business Rule
  ↓
State / Use Case
  ↓
Acceptance Criteria
  ↓
Product Design
  ↓
Architecture / Code
  ↓
Test
```

当前阶段只追踪到 Acceptance Criteria；后续 Stage 会继续补链。

## 2. Matrix

| Evidence | Finding / Job | Story / Scope | Rule | Use Case / State | AC | Status |
| --- | --- | --- | --- | --- | --- | --- |
| INT-004, ART-001 | F-002 responsibility layers | US-002 / S-003 | BR-002 | UC-001 | Issue validation TBD AC | Ready with executor gap |
| INT-001, INT-002, OBS-001 | F-004 stale != delayed | US-005 / S-007 | BR-005 | UC-003 | AC-US005 | Threshold gap |
| INT-001, INT-005 | J-001 deadline attention | US-006 / S-007 | BR-006, BR-007 | Attention Model | AC-006-* | Near-due gap |
| INT-005, OBS-001 | F-006 completion != closure | US-008 / S-008 | BR-008 | UC-004 / IN_PROGRESS→PENDING_CLOSURE | AC-008-* | Ready |
| INT-005, OBS-001 | F-006 completion != closure | US-009 / S-009 | BR-009 | UC-005 / PENDING_CLOSURE→CLOSED | AC-009-* | Closure authority gap |
| INT-003 | J-003 management intervention | US-007 / S-012 | BR-C001 | UC-006 | Product-level AC pending | Needs design |
| INT-001, OBS-001 | F-001 fragmented information | US-004, US-010 | BR-004, BR-011 | UC-002 | AC-004-* | Ready |

## 3. Example — Full Chain

```text
INT-005 + OBS-001
      ↓
F-006
Completion Claim != Closure
      ↓
US-008
Submit Completion Claim
      ↓
BR-008
Valid claim moves IN_PROGRESS → PENDING_CLOSURE
      ↓
UC-004
Submit Completion Claim
      ↓
AC-008-01 / 02 / 03
      ↓
[Stage 03] Completion UX Flow
      ↓
[Stage 05] API / Domain Design
      ↓
[Stage 08] Implementation
      ↓
[Stage 09] Integration / E2E Test
```

未来如果开发者提出：

```text
progress = 100 自动 CLOSED
```

Traceability 会立刻暴露冲突：它违反 F-006、BR-008 和 AC-008-02。

## 4. Orphan Requirement Detection

任何 Requirement 如果无法回答：

```text
Which Evidence / Job does this serve?
```

标记：

```text
ORPHAN_REQUIREMENT
```

处理方式：
1. 找到真实 Trace；
2. 降级为 Future Candidate；
3. 返回 Discovery；
4. 删除。

## 5. Orphan Evidence Detection

反过来，如果高价值 Finding 没有任何 Requirement 承接，也需要 Review。

例如：

```text
F-007 跨部门依赖
```

目前只有部分 Scope Candidate，没有完整 MVP Requirement。

Decision：保留为 `OPEN_TRACE_GAP`，在 MVP Review 决定是否结构化支持 Collaborator/Dependency。

## 6. Change Impact

当 BR-009 Closure Authority 被确认时，应沿链检查：

```text
Glossary
→ Business Rule
→ UC-005
→ AC-009
→ Permission Model
→ Product UI
→ API
→ Test
```

这就是 Artifact Graph 的实际价值：需求变化不再依赖“大家记得改哪些文档”。
