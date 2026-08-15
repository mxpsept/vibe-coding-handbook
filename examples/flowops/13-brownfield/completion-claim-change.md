# FlowOps Brownfield Example — 在已有系统增加 Completion Claim

## Scenario

系统已上线 Item Detail、Progress Update。新 Requirement：执行人员可以提交完成声明，但提交声明不等于正式办结。

目标是演示存量仓库中如何让 Codex 安全修改，而不是重建系统。

## 1. Repository Reconnaissance

Agent 先定位：

```text
Item Detail page
existing progress action/modal
API client convention
backend supervision module
permission policy
state transition tests
audit mechanism
```

输出 Repository Map 后再编码。

## 2. Behavior Contract

### Preserve
- Item Detail existing read behavior；
- Progress Update behavior；
- current authorization model；
- Lifecycle display。

### Add

```text
Authorized participant
→ Submit Completion Claim
→ Item enters/reflects pending closure semantics
→ Formal Closure still requires Closure Authority
```

### Non-goals
- redesign Item Detail；
- replace state management；
- add notification；
- refactor all lifecycle code。

## 3. Change Map

Candidate:

```text
Frontend
Item Detail
→ action visibility
→ confirmation/form
→ API call
→ pending/success/error state

Backend
Closure application capability
→ authorization
→ read current Item state
→ transition validation
→ persistence
→ audit

Tests
→ allowed actor
→ forbidden actor
→ invalid lifecycle
→ claim does not equal CLOSED
→ duplicate/concurrent behavior if applicable
```

## 4. Critical Semantic Test

必须有 Evidence 保护：

```text
submitCompletionClaim(item)
!=
closeItem(item)
```

如果现有数据库只有一个 `status` 且无法表达该语义，Agent 必须报告 Data/Domain Gap，而不是偷偷把状态改成 CLOSED。

## 5. UI

Page Spec 决定按钮和反馈；不要因为新增动作顺便把整个详情页换成另一套 UI。

Success copy candidate：

```text
完成声明已提交，等待正式办结确认。
```

## 6. Review Findings to Look For

Reviewer 主动检查：
- frontend-only permission；
- generic `PUT status` bypass；
- closure authority bypass；
- audit missing；
- retry creates duplicate claim；
- stale client state overwrites newer server state；
- success message falsely says “已办结”。

## 7. Final Trace

```text
Requirement
→ Business Rule: Claim != Closure
→ Page Spec
→ API action
→ Application use case
→ Domain transition
→ Persistence/Audit
→ Tests
→ Review
```

这个链路比“让 Codex 增加一个完成按钮”多了很多约束，但正是这些约束让 AI 适合长期企业开发，而不是只适合 Demo。
