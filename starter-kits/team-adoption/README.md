# Team Adoption Starter Kit

目标：让一个团队在不大规模改造流程的情况下，用 4 个阶段把 AI Coding 从个人技巧变成可重复团队实践。

## Phase 1 — One Pilot Slice

选择：
- 真实业务；
- 低到中风险；
- 1–2 周可完成；
- 能覆盖需求、UI/API、测试。

引入最少资产：

```text
AGENTS.md
Feature Spec
Implementation Packet
Verification Report
```

不要第一天建立 30 个模板。

## Phase 2 — Team Conventions

复盘 Pilot：
- Agent 最常猜错什么？
- 哪些 Context 每次重复解释？
- Review 最常发现什么？
- 哪些测试最缺？

把高频稳定答案固化到：

```text
Repository Instructions
Architecture Context
Design System
Checklists
```

## Phase 3 — Quality Gates

根据风险逐步自动化：
- build/test/lint；
- secret/dependency checks；
- architecture constraints；
- required PR evidence；
- production readiness。

不要自动化一个团队自己都解释不清的规则。

## Phase 4 — Scale & Governance

当多个项目采用后再建立：
- organization AI policy；
- approved tool/data rules；
- shared templates；
- metrics；
- maturity assessment；
- training/onboarding。

## 30-Day Candidate Plan

```text
Week 1  choose pilot + baseline + minimal artifacts
Week 2  run first vertical slice with Codex
Week 3  review rework/failures + harden repo instructions
Week 4  repeat second slice + decide team standard
```

## What to Measure

不要以 Token 或 AI LOC 为成功标准。观察：
- cycle time；
- review rework；
- escaped defect；
- context/spec gaps；
- developer/reviewer effort；
- business outcome。

## Exit Criteria

团队准备扩大使用前，应能回答：

1. Agent 从哪里读取 Source of Truth？
2. 哪些决策不能由 Agent 自主做？
3. 完成如何被验证？
4. 谁能 merge/deploy/访问生产？
5. 新成员能否不用历史聊天接手任务？

如果回答不清楚，先强化工程系统，而不是增加 Agent 数量。
