# FlowOps — Business Rules v0.1

> Synthetic Teaching Case。`Approved` 仅表示教学案例中的 Requirements 决策，不代表真实企业规则。

## Rule Status

- Candidate — 来自 Discovery，尚未决策
- Approved — Requirements Workshop 已确认
- Rejected — 明确不采用
- TBD — 缺少信息，禁止 Agent 猜测

## BR-001 — Supervision Item Eligibility

**Status:** TBD

哪些工作可以正式进入督办范围尚未形成足够精确规则。

Known candidate sources: important meeting action, leadership assignment, cross-department key work, temporary initiative.

**Agent rule:** 不得自行根据文本内容判断一项普通工作是否属于 Supervision Item。

---

## BR-002 — Accountability

**Status:** Approved

每个已正式下达的 Supervision Item 必须存在且仅存在一个当前 Accountable Department。

Executor 是否强制：TBD。

Rationale: Discovery 同时证明正式责任维度以部门为主，而个人执行责任可能属于内部管理。

---

## BR-003 — Due Date

**Status:** Approved

进入正式执行生命周期的事项必须存在 Effective Due Date。

如果未来支持延期，则期限判断必须使用 Effective Due Date，而不是 Original Due Date。

---

## BR-004 — Progress History

**Status:** Approved

Progress Update 采用追加记录模式。正常业务操作不得覆盖或删除既有历史进度。

Correction mechanism: TBD。

---

## BR-005 — Stale Update

**Status:** Approved with TBD threshold

当事项处于非终态，且距离 Last Progress Update Time 超过有效阈值时，可产生 `STALE_UPDATE` Attention Flag。

`STALE_UPDATE` 不得自动改变 Lifecycle State，也不得自动推断事项已经延误。

Threshold: TBD。

---

## BR-006 — Near Due

**Status:** Approved with TBD threshold

当事项处于非终态，且当前业务日期尚未超过 Effective Due Date，同时剩余时间进入有效 Near-due Threshold 时，产生 `NEAR_DUE` Attention Flag。

Threshold strategy: TBD。

---

## BR-007 — Overdue

**Status:** Approved

当：

```text
current business date > Effective Due Date
AND Lifecycle State is not terminal
```

则事项具有 `OVERDUE` Attention Flag。

Overdue 是期限条件，不是 Lifecycle State。

---

## BR-008 — Completion Claim

**Status:** Approved

只有具备适用权限的责任方才能对 `IN_PROGRESS` 事项提交 Completion Claim。

提交成功后事项进入 `PENDING_CLOSURE`，不得直接进入 `CLOSED`。

---

## BR-009 — Closure

**Status:** Approved with authority TBD

`PENDING_CLOSURE` 事项只有经过 Closure Authority 确认后才能进入 `CLOSED`。

Closure Authority: TBD。

Agent 不得假设创建人、管理员或督办专员天然拥有 Closure Authority。

---

## BR-010 — Terminal State Mutation

**Status:** Approved

`CLOSED` 和 `CANCELLED` 为终态。终态事项不能提交普通 Progress Update 或 Completion Claim。

Reopen capability: Out of MVP / Future Candidate。

---

## BR-011 — Auditability

**Status:** Approved

以下行为必须记录 Actor、Timestamp 和关键前后值：

- Issue；
- Accountability change；
- Due date change；
- Progress submission；
- Completion Claim；
- Closure；
- Cancellation。

---

## BR-012 — Progress Percentage

**Status:** TBD

Discovery 证明现有 Excel 使用 Percentage，但没有证明其具有统一计算标准。

因此 MVP 不得仅为了复刻 Excel 而默认采用 0–100% 作为核心状态依据。

---

# SPEC_GAP Register

| Gap | Blocks | Owner |
| --- | --- | --- |
| 哪些事项可以进入正式督办 | Item creation policy | Business Owner |
| Executor 是否强制 | Responsibility model | Business Owner |
| Stale threshold | Attention evaluation | Product/Business |
| Near-due threshold strategy | Attention evaluation | Product/Business |
| Closure Authority | Closure workflow | Business Owner |
| Progress correction | History model | Product/Compliance |
| Progress Percentage | UI/data model | Product Owner |

## Agent Contract

如果实现任务触及以上 TBD，Agent 必须输出 `SPEC_GAP`，不能静默选择默认规则。
