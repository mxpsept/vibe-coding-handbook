# FlowOps — PRD v0.1

> 本 PRD 是 Specification System 的入口和摘要，不复制所有规则。详细语义以同目录 Artifact 为准。

## 1. Product

FlowOps — Enterprise Supervision & Execution Tracking

## 2. Problem

重点事项执行信息跨组织层级和多个工具流转，责任、进度更新、期限关注、风险表达与最终办结之间缺少稳定语义和可信事实来源，导致重复反馈、状态滞后、风险确认成本高，并影响管理层及时获得可行动信息。

Trace: `../01-discovery/discovery-summary.md`。

## 3. Product Outcome

建立一条可追踪的重点事项督办闭环：

```text
Establish
→ Accountability
→ Execute
→ Update
→ Attention
→ Completion Claim
→ Closure
→ History
```

## 4. Primary Users

- Supervision Specialist；
- Accountable Department / Responsible Participant；
- Department Manager；
- Manager；
- Closure Authority（具体角色 TBD）。

## 5. MVP Scope

详见 `scope.md`。

核心：
- Item establishment；
- Accountability；
- Due date；
- Progress history；
- Attention evaluation；
- Completion Claim；
- Closure；
- Query / management attention view；
- Audit/history。

## 6. Core Product Principles

### P-001 — Single status is forbidden as universal model
Lifecycle、Attention、Progress、Completion 不得混成一个业务枚举。

### P-002 — History over overwrite
进度更新优先保留过程历史，而不是反复覆盖“当前进展”。

### P-003 — Attention is not judgment
`STALE_UPDATE` 等信号用于提示核验，不自动推断真实执行失败。

### P-004 — Completion is not Closure
执行完成声明与督办正式结束分离。

### P-005 — Unknown is explicit
未确认 Business Rule 使用 `SPEC_GAP/TBD`，Coding Agent 不得自行补齐。

## 7. Lifecycle

See `state-model.md`。

```text
DRAFT → ISSUED → IN_PROGRESS → PENDING_CLOSURE → CLOSED
                         ↘
                      CANCELLED (rule TBD)
```

Attention Flags independent:

```text
STALE_UPDATE / NEAR_DUE / OVERDUE / BLOCKED(candidate)
```

## 8. Functional Requirements Summary

| Area | Requirement |
| --- | --- |
| Establish | create and issue valid supervision items |
| Accountability | maintain accountable department |
| Execution | expose relevant work to authorized actors |
| Progress | append progress history |
| Attention | evaluate stale / near-due / overdue independently |
| Completion | submit completion claim |
| Closure | authorized formal closure |
| Management | focus on items requiring attention/intervention |
| Audit | preserve key action history |

Detailed Stories: `user-stories.md`。  
Detailed Flows: `use-cases.md`。  
Rules: `business-rules.md`。

## 9. Acceptance

Acceptance Criteria: `acceptance-criteria.md`。

Implementation-ready feature must have:

```text
Story
+ Rule
+ State impact
+ Permission
+ AC
+ no blocking SPEC_GAP
```

## 10. NFR

See `nfr.md`。

Key themes:
- server-side authorization；
- auditability；
- data integrity；
- observability；
- workload-based performance targets；
- no invented SLA/RPO/RTO。

## 11. Open Product Decisions

1. Supervision Item eligibility；
2. Authorized Issuer；
3. Executor requirement；
4. Collaborator/Dependency MVP support；
5. Stale threshold；
6. Near-due strategy；
7. Progress Percentage；
8. Progress correction；
9. Closure Authority；
10. Completion rejection/return；
11. Cancellation authority/rule；
12. quantitative outcome baseline。

## 12. Explicit Non-goals

FlowOps MVP is not:
- generic project management；
- generic BPM；
- instant messaging；
- document management；
- AI autonomous management decision system。

## 13. Traceability

See `traceability.md`。

PRD 中任何新增 Requirement 都必须进入 Traceability Matrix。

## 14. Product Design Handoff

Product Design 的任务不是“美化 PRD”，而是根据 Job / Use Case / State / Attention 设计：

- Information Architecture；
- Navigation；
- Task flows；
- Page hierarchy；
- Interaction；
- Empty/loading/error/permission states；
- Management information presentation；
- Responsive strategy；
- Visual system。

Product Designer 可以挑战 Requirement，但不得静默改变 Business Rule。
