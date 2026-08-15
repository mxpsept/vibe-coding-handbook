# Project Playbook — 一张路线图跑完整个企业 AI 项目

## Gate 0 — Should We Build It?

Output：Product Brief / actors / problem / success / non-goals / constraints。

**Gate:** 问题和用户不清楚，不进入设计开发。

## Gate 1 — Do We Understand It?

Output：Discovery Evidence、Glossary、workflow、assumptions、unknowns。

**Gate:** Blocking unknowns 被识别并有 owner。

## Gate 2 — Is Behavior Specified?

Output：Requirements、AC、Business Rules、State、Permission、Edge Cases。

**Gate:** Critical flow 可以被 Test Designer 转成测试。

## Gate 3 — Is Experience Designed?

Output：User Flow、wireframes、chosen direction、Design System、Page Spec、UI State Matrix。

**Gate:** Frontend 不需要从一句需求猜页面结构和所有状态。

## Gate 4 — Can We Build It Safely?

Output：Architecture Drivers、boundaries、domain/data/API/error/security/observability、ADR。

**Gate:** 重要技术选择有理由，Agent 知道代码 Owner 和禁止边界。

## Gate 5 — Is the Slice Agent-ready?

Output：Implementation Packet：

```text
Goal
Read First
Scope / Non-goals
AC
Constraints
Stop Conditions
Verification
```

**Gate:** Fresh Agent Session 能解释任务而无需历史聊天。

## Gate 6 — Is It Implemented?

Agent：inspect → plan → implement → local verify → report。

**Gate:** 没有 hidden gap、unrelated refactor 或未经批准的新 dependency。

## Gate 7 — Is It Proven?

Evidence：
- unit/domain；
- integration/contract；
- UI/component/e2e as risk requires；
- negative/permission/state paths；
- build/lint/typecheck。

**Gate:** AC 有可追踪 Evidence。

## Gate 8 — Is It Reviewable?

Independent Reviewer：correctness → security → business → architecture → regression → test adequacy。

**Gate:** Material findings resolved/accepted。

## Gate 9 — Is It Production-ready?

Security、performance、migration、config、observability、runbook、rollback、owner。

**Gate:** READY / READY_WITH_ACCEPTED_RISK / HOLD。

## Gate 10 — Did Production Validate Our Assumptions?

观察：business outcome、errors、latency、incidents、support/user feedback。

将 Evidence 转为：

```text
new requirement
bug
technical/context debt
ADR revisit
runbook/test improvement
```

然后循环。

## Brownfield Shortcut

已有项目不是跳过所有 Gate，而是复用已有 Artifact/代码 Evidence，并从 Repository Reconnaissance 开始确认哪些 Gate 已有可信答案。

## Golden Rule

```text
AI accelerates execution.
The engineering system must accelerate trustworthy decisions and verification with it.
```
