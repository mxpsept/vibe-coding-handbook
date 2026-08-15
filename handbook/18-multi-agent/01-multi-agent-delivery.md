# 01 — Multi-Agent Delivery：按职责分离上下文，而不是让更多 AI 同时写代码

Multi-Agent 的价值主要来自 **separation of concerns + independent review**，不是 Agent 数量。

## Recommended Pipeline

```text
Planner
↓
Implementation Agent
↓
Test / Verification Agent
↓
Reviewer Agent
↓
Human Gate
```

小任务不必强制五个 Agent；角色可以由不同 Session 承担。

## Planner

输入 Requirements / Architecture / Repository Evidence。
输出：
- change map；
- impacted contracts；
- implementation slices；
- risks；
- verification plan；
- stop conditions。

Planner 默认不写代码。

## Implementation Agent

只消费批准范围，负责：
- repository inspection；
- implementation；
- local tests；
- change report。

不得因为发现技术债自动扩大范围。

## Test Agent

从 Acceptance Criteria 和风险出发，而不是只根据 Implementation Agent 写了什么测试。

重点寻找：
- missing negative path；
- boundary cases；
- permission；
- state transition；
- regression。

## Reviewer Agent

以 skeptical reviewer 身份独立检查：

```text
correctness
business semantics
architecture
security
failure behavior
test adequacy
scope creep
```

Reviewer 不应该因为实现来自另一个 AI 就降低标准。

## Human Gate

人类负责：
- product/architecture decisions；
- accepted risk；
- merge/release accountability；
- unresolved ambiguity。

## Shared Context vs Independent Context

共享：批准 Artifact、repository instructions、Task Packet。

不要共享：Implementation Agent 的自我评价作为 Reviewer 的事实。

Reviewer 应直接看 diff + Source of Truth + tests。

## Avoid Agent Telephone Game

不要：

```text
Agent A summary
→ Agent B summary of summary
→ Agent C implements
```

关键角色应读取原始 Source of Truth，Summary 只是导航。

## Parallel Work

只有边界独立时才并行。例如：

```text
API contract approved
├── backend slice
└── frontend slice
```

如果 Contract 仍在变化，并行只会放大返工。

## Merge Strategy

多 Agent 并行时，每个 worktree/branch 应有单一责任。共享文件冲突（schema、router、global config）提前指定 owner。

## Multi-Agent Done

最终不是“所有 Agent 都说完成”，而是：

```text
accepted artifacts
+ integrated code
+ passing verification
+ resolved review findings
+ human merge decision
```
