# 01 — 企业团队如何落地 Vibe Coding 工程体系

> 前面的章节解决“如何做”；这一章解决“团队如何真正用起来”。

## 1. 不要一次性改变整个研发流程

推荐三阶段 adoption：

```text
Pilot
↓
Standardize
↓
Scale
```

### Pilot
选择一个低风险、真实、有完整生命周期的小项目或独立 Feature。目标不是证明 AI 能写多少代码，而是验证 Artifact → AI → Verification 的闭环。

### Standardize
把 Pilot 中稳定的实践固化为：
- Repository instructions；
- templates；
- prompts；
- quality gates；
- ADR；
- Definition of Done。

### Scale
扩展到更多项目，并通过度量发现哪些环节真正提高交付质量与速度。

## 2. 团队角色重新分工

AI 不取消角色，而是改变角色的工作重心。

```text
Product / Business
→ intent, priority, acceptance

Designer
→ research, alternatives, system, review

Architect / Tech Lead
→ boundaries, decisions, quality attributes

Engineer
→ implementation strategy, verification, integration

AI Agents
→ research, drafting, implementation, review, test assistance
```

人类应把更多时间放到不可轻易外包给模型的判断上。

## 3. Repository as Shared Context

不要让核心项目知识只存在：
- 某个人脑中；
- Chat 会话；
- IM 消息；
- 一张截图。

推荐仓库至少维护：

```text
requirements/
design/
architecture/
adrs/
implementation-notes/
tests/
runbooks/
```

AI Agent 每次开始工作时先读取相关 Source of Truth。

## 4. AI Work Item Size

最适合 Agent 的任务通常是：

```text
一个明确 Goal
+ 有限 Context
+ 清晰边界
+ 可验证结果
```

避免一次 Prompt：

```text
“把整个系统做完。”
```

更推荐：

```text
实现 Attention Workspace 查询与页面
```

并提供 Requirements / Page Spec / API / Tests。

## 5. Human Review 重点变化

不要把 Review 时间全部用于检查语法和格式。

重点检查：

```text
Business correctness
Architecture boundary
Security
Data semantics
Failure behavior
Unintended scope
Test quality
```

AI 可以帮助 Review，但最终责任不能因为“代码是 AI 写的”而消失。

## 6. Suggested Metrics

不要只统计：

```text
AI generated lines of code
```

更有价值：
- lead time；
- change failure rate；
- escaped defects；
- review rework；
- requirement clarification frequency；
- architecture drift findings；
- test coverage of critical rules；
- time from issue to verified change。

## 7. Team Policy Example

```text
1. Blocking business gaps must not be guessed by AI.
2. New architecture categories require ADR/review.
3. Every feature must have acceptance evidence.
4. AI-generated code receives the same review standard as human code.
5. Secrets/production data must follow organization AI/data policy.
6. Repository instructions override ad-hoc agent preference.
7. Verification is part of implementation, not a later optional phase.
```

## 8. Adoption Anti-patterns

### Buy licenses and call it transformation
工具可用 ≠ 工程体系建立。

### Every developer invents their own workflow
短期灵活，长期无法协作和复用。

### Prompt library without artifacts
Prompt 再完整，如果输入的业务事实不稳定，输出仍然漂移。

### AI speed hides review debt
生成速度提高后，Review/Testing 若不升级，缺陷只会更快进入主干。

## 9. 30-Day Pilot Candidate

### Week 1
- 选择 Pilot；
- 建 Foundation；
- 完成 Discovery/Requirements；
- 定义 AI usage rules。

### Week 2
- Product Design；
- Architecture；
- 建立 ADR / implementation packet。

### Week 3
- AI-assisted implementation；
- tests；
- PR review。

### Week 4
- release；
- production feedback；
- retrospective；
- 将稳定实践回写 Handbook/Project Template。

## 10. 最终目标

成熟团队不是“AI 用得最多”的团队，而是：

> 能让 AI 在明确意图、稳定约束和强验证下持续产生可信软件的团队。
