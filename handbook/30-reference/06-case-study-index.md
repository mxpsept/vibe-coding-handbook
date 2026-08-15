# Case Study Index

案例的目标不是展示“最终答案”，而是展示工程决定如何一步步形成。

## FlowOps Core Journey

从 `examples/flowops/` 开始，按项目 Artifact 演进查看 Discovery、Requirement、Design、Architecture、Implementation 与 Verification。

## Brownfield — Completion Claim

`examples/flowops/13-brownfield/completion-claim-change.md`

学习：已有系统新增业务动作时，如何保护 Claim != Closure 的关键语义，并控制改动范围。

## Production — Attention Workspace Release

`examples/flowops/14-production/attention-workspace-release.md`

学习：Feature 合并后如何进入 Security、Performance、Observability、Smoke Test、Rollback 和生产反馈。

## End-to-End — Overdue Escalation

`examples/flowops/15-end-to-end/overdue-escalation-feature.md`

学习：一句模糊需求如何经过 Discovery → Rule → UI → Architecture → Agent → Test → Production。

## Integration — External Notification

`examples/flowops/15-end-to-end/external-notification-integration.md`

学习：Timeout、Retry、Idempotency、Provider Adapter、Secret、Runbook 等企业集成问题。

## Brownfield Refactor — Legacy Deadline Rule

`examples/flowops/15-end-to-end/legacy-rule-refactor.md`

学习：AI 重构前如何 Characterize Behavior，找到 Domain Owner，再逐步迁移消费者。

## How to Read a Case

每次都问：

1. 原始需求缺了哪些事实？
2. 哪个 Artifact 成为 Source of Truth？
3. Agent 被允许决定什么？
4. 哪些情况触发 Stop Condition？
5. 用什么 Evidence 证明完成？
6. 生产反馈如何进入下一轮？

如果只复制案例中的字段/目录而不理解这些问题，就失去了案例的主要价值。
