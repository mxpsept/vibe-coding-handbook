# 第 2 章：Requirements Engineering——把 Evidence 转换成 AI 可执行的 Specification

> Discovery 的目标是理解 Problem Space；Requirements 的目标是明确 **系统必须做什么、不能做什么、在什么条件下算正确**。

在 Vibe Coding 时代，这一阶段比过去更重要。因为模糊需求交给人类开发者，人会主动开会、追问、补上下文；模糊需求交给 Coding Agent，它往往会非常高效地替你做决定。

---

# 0. 本章目标

完成本章后，你应该能够：

- 把 Discovery Finding 转换为 Requirement Candidate，而不是凭空列功能；
- 区分 Goal、Requirement、Business Rule、User Story、Use Case、Acceptance Criteria；
- 明确 Functional / Non-functional Requirements；
- 建立 Scope / Out of Scope / MVP；
- 使用状态机描述关键生命周期；
- 将模糊词转换为可验证规则；
- 建立 Requirement Traceability；
- 为 Coding Agent 准备稳定、分层、可验证的 Spec；
- 识别 AI 生成 PRD 时最常见的“合理性幻觉”；
- 使用 Gate 2 判断需求是否足以进入 Product Design。

---

# 1. Why：为什么 AI 时代不能弱化需求，反而要强化需求

传统开发中，一个模糊需求可能是：

```text
做一个任务进度填报功能。
```

人类开发者会自然产生很多问题：

```text
谁能填？
填什么？
多久填一次？
可以修改历史记录吗？
进度百分比怎么算？
100% 是否自动办结？
附件是否必须？
别人能看到吗？
```

Coding Agent 也可能发现这些问题，但它还有另一种能力：**自己选一个合理答案然后继续 Coding。**

于是你得到：

```text
页面正常
接口正常
数据库正常
测试也可能正常
```

但业务语义是错的。

因此：

> **AI 提高了 Implementation Speed，也提高了错误假设被快速固化成代码的速度。**

Requirements Engineering 的价值，就是减少 Agent 可以随意发挥的决策空间。

---

# 2. 从“需求文档”升级为 Specification System

不要把 PRD 当成唯一真相文件。

企业项目的 Requirement System 更适合拆成：

```text
Discovery Evidence
      ↓
Glossary
      ↓
Scope
      ↓
Business Rules
      ↓
Domain / Lifecycle
      ↓
User Stories / Use Cases
      ↓
Acceptance Criteria
      ↓
NFR
      ↓
Traceability
      ↓
PRD Summary
```

原因很简单：Coding Agent 需要的不是一篇漂亮文章，而是**可定位、可引用、低歧义、可验证的 Context**。

例如不要只写：

```text
系统支持任务办结。
```

而应该能继续追踪到：

```text
Term: Completion Claim
Rule: BR-021
State Transition: IN_PROGRESS → PENDING_CLOSURE
Actor: Accountable Department
Acceptance Criteria: AC-021-01 ~ 04
Evidence: F-006 / INT-005 / OBS-001
```

这才开始接近 Agent-ready Spec。

---

# 3. Requirement Stack：不同 Artifact 回答不同问题

| Artifact | 回答的问题 |
| --- | --- |
| Goal / Outcome | 为什么值得做？ |
| Scope | 这次解决什么、不解决什么？ |
| Glossary | 这些词到底是什么意思？ |
| Business Rule | 业务在什么条件下必须怎样运行？ |
| User Story | 某角色为什么需要某能力？ |
| Use Case | 一次完整交互如何发生？ |
| State Model | 对象如何从一个状态变到另一个状态？ |
| Acceptance Criteria | 什么结果才算实现正确？ |
| NFR | 性能、安全、可靠性等质量约束是什么？ |
| Traceability | 这个需求为什么存在、如何验证？ |

这些内容可以在小项目中合并，但概念不能混乱。

---

# 4. 第一步：先建立 Glossary

企业项目最危险的 Bug 经常不是代码 Bug，而是**同一个词大家理解不同**。

FlowOps Discovery 已经出现：

```text
完成
办结
进度
状态
风险
临期
超期
责任人
责任部门
协办
```

例如如果不定义“完成”：

- 执行人员可能理解为“我的工作做完了”；
- 部门负责人理解为“部门已经交付”；
- 督办人员理解为“成果已确认”；
- 开发人员可能理解为 `progress == 100`。

因此 Requirements 第一个 Artifact 应该是 Glossary。

推荐格式：

| Term | Definition | Not the same as | Source | Status |
| --- | --- | --- | --- | --- |
| Completion Claim | 责任方声明工作已完成 | Closure | F-006 | Draft |

原则：

> **先统一语言，再统一功能。**

---

# 5. 第二步：Scope / Out of Scope

AI 特别容易“顺手多做一点”。

你说：

```text
做任务督办。
```

它可能顺手生成：

```text
组织管理
消息中心
AI 总结
日历
文件中心
流程引擎
BI Dashboard
移动端
大屏
知识库
```

这些都可能合理，但合理不等于本期需要。

因此明确：

```text
In Scope
Out of Scope
Future Candidate
Unknown
```

FlowOps MVP 示例候选：

```text
In Scope Candidate
- 督办事项建立
- 责任关系
- 截止时间
- 进度更新
- 风险关注
- 办结
- 查询与基础统计

Out of Scope Candidate
- 通用 BPM 流程引擎
- AI 自动决策
- 项目管理甘特图
- 企业即时通讯
- 完整文档管理平台
```

注意：这些必须经过 Human Review 后才能成为正式 Scope。

---

# 6. 第三步：Business Rules——这是企业软件的核心

页面会变，技术会变，Business Rule 往往更稳定。

一个弱规则：

```text
任务快到期时提醒用户。
```

问题：

```text
什么叫快到期？
提醒谁？
什么时候计算？
已完成还提醒吗？
延期后按哪个日期？
不同任务是否一样？
```

一个更好的 Rule：

```text
BR-014 Near-due Evaluation

Given:
- Supervision Item has an effective due date;
- Item is not in a terminal state.

When:
- remaining calendar days <= configured near-due threshold.

Then:
- item receives attention flag NEAR_DUE.

Notes:
- Near-due is an Attention Flag, not lifecycle Status.
- Threshold source is defined separately.
```

这样 UI 可以显示橙色、邮件可以提醒、API 可以筛选，但 Business Rule 不依赖 UI。

---

# 7. Business Rule 不等于代码实现

不要写：

```text
使用 Redis 定时扫描任务。
```

这不是 Business Rule，是 Implementation Decision。

Rule 应该写：

```text
系统应能够识别满足临期条件且尚未处于终态的事项。
```

后面 Architecture 再决定：

```text
SQL query?
Scheduler?
Event-driven?
Redis?
Materialized field?
```

这条边界对 Vibe Coding 极其重要，因为 AI 很容易把 Requirements 和 Architecture 一次性“做完”。

---

# 8. 第四步：状态机——不要用一个 status 字段承载整个世界

FlowOps Discovery 已经发现：

```text
Progress
≠ Update Freshness
≠ Delivery Risk
≠ Lifecycle Status
≠ Completion Claim
≠ Closure
```

如果需求阶段没有建模，开发阶段很容易得到：

```text
status:
0 待处理
1 处理中
2 临期
3 超期
4 已完成
5 已办结
```

这里已经混入至少三个维度：

```text
Lifecycle: 待处理 / 处理中 / 已办结
Deadline Condition: 临期 / 超期
Completion: 已完成
```

更合理的候选模型可能是：

```text
Lifecycle State
DRAFT
ISSUED
IN_PROGRESS
PENDING_CLOSURE
CLOSED
CANCELLED

Attention Flags
STALE_UPDATE
NEAR_DUE
OVERDUE
BLOCKED

Progress
0..100 or structured progress — still needs validation
```

具体状态仍需 Business Review，但至少不要把不同维度塞进一个枚举。

---

# 9. 状态转换必须定义 Actor + Preconditions + Effects

不要只画：

```text
处理中 → 已办结
```

应该定义：

```text
Transition: Submit Completion
Actor: Accountable Party
From: IN_PROGRESS
To: PENDING_CLOSURE
Preconditions:
- required completion summary exists
- actor has permission
Effects:
- create audit record
- record submission timestamp

Transition: Approve Closure
Actor: Closure Authority
From: PENDING_CLOSURE
To: CLOSED
Preconditions:
- completion evidence satisfies applicable rule
Effects:
- record closure actor/time
```

如果“谁拥有 Closure Authority”仍 Unknown，就标记 Unknown，不要让 AI 自己选。

---

# 10. 第五步：User Story——有用，但不要让它承担全部需求

经典格式：

```text
As a <role>,
I want <capability>,
so that <outcome>.
```

FlowOps 示例：

```text
As a supervision specialist,
I want to identify items whose progress information may be stale,
so that I can verify them before the management meeting.
```

它很好地表达价值，但没有回答：

```text
多久算 stale？
哪些状态参与计算？
更新时间取哪个字段？
是否自动提醒？
```

因此 User Story 必须连接 Business Rule 和 Acceptance Criteria。

---

# 11. 第六步：Use Case——复杂企业流程仍然需要它

User Story 很轻，但遇到多角色流程时 Use Case 更清楚。

例如：`UC-007 Submit Completion`。

```text
Primary Actor: Accountable Party
Goal: 声明事项执行工作已完成并提交办结确认
Preconditions:
- item is IN_PROGRESS

Main Flow:
1. Actor opens item.
2. Actor enters completion summary.
3. Actor attaches required evidence when applicable.
4. Actor submits completion claim.
5. System validates required information.
6. System records claim.
7. Lifecycle changes to PENDING_CLOSURE.

Alternative:
A1. Required evidence missing → reject submission.
A2. Actor lacks permission → deny action.
```

这比“增加办结按钮”更接近真正可开发需求。

---

# 12. 第七步：Acceptance Criteria——把“做完”变成可验证

弱 AC：

```text
用户可以提交进度。
```

更好：

```gherkin
Scenario: Submit a valid progress update
Given the item is IN_PROGRESS
And the current user has update permission
When the user submits non-empty progress content
Then a new progress record is created
And the previous progress history remains unchanged
And the item last-progress-update time is refreshed
And an audit event is recorded
```

边界场景：

```gherkin
Scenario: Closed item cannot receive progress update
Given the item is CLOSED
When a user attempts to submit progress
Then the operation is rejected
And no progress record is created
```

Acceptance Criteria 是后面 AI Coding 与 AI Testing 之间最重要的契约之一。

---

# 13. Example：一句模糊需求如何逐步 Spec 化

原始需求：

```text
任务超期后显示红色。
```

## Step 1 — 找到 Problem

管理者需要快速识别需要关注的交付风险。

## Step 2 — 去掉 UI 假设

```text
系统需要识别已经超过有效截止时间且未进入终态的事项。
```

## Step 3 — Business Rule

```text
BR-018 Overdue Evaluation

An item is OVERDUE when:
- current business date > effective due date;
- lifecycle state is not terminal.
```

## Step 4 — AC

```gherkin
Given due date is 2026-09-30
And item state is IN_PROGRESS
When business date becomes 2026-10-01
Then attention flag OVERDUE is true
```

## Step 5 — Product Design Later

UI 阶段再决定：

```text
红色 Tag？
红色文字？
风险卡片？
筛选入口？
```

这就是：

```text
Problem → Rule → Verification → UI
```

而不是：

```text
“显示红色” → Coding
```

---

# 14. 第八步：Functional Requirement 与 NFR

Functional Requirement 描述系统行为，例如：

```text
FR-021 系统应允许授权责任方提交事项进度记录。
```

NFR 描述质量属性和约束，例如：

```text
NFR-SEC-001 用户只能访问其数据权限范围内的事项。
NFR-AUD-001 状态转换必须保留操作者、时间和前后状态。
NFR-PERF-001 典型查询在约定数据规模下满足响应时间目标。
```

不要写假的数字：

```text
所有接口必须 200ms。
```

如果没有业务依据，应写：

```text
Performance target: TBD through workload analysis.
```

AI 特别喜欢生成“99.99%”“500ms”“1000 QPS”这类看起来专业的数字。没有 Evidence 就不要批准。

---

# 15. 第九步：MVP 不是“少做几个页面”

MVP 的核心是最小可验证业务闭环。

FlowOps 的 MVP 不应该简单理解为：

```text
先做 5 个菜单，后面再加 5 个菜单。
```

应该问：

```text
最小什么能力可以让一条重点事项
从建立 → 责任 → 执行 → 更新 → 风险识别 → 办结
形成闭环？
```

一个候选 Vertical Slice：

```text
Create / Issue Item
      ↓
Assign Accountability
      ↓
Track Due Date
      ↓
Submit Progress
      ↓
Identify Attention
      ↓
Submit Completion
      ↓
Close Item
      ↓
Audit History
```

这比按“后台管理、统计页面、消息中心”拆 MVP 更符合业务价值。

---

# 16. Priority：不要让 MoSCoW 变成“所有都是 Must”

常见结果：

```text
Must: 37
Should: 3
Could: 1
Won't: 0
```

这等于没有优先级。

优先级应结合：

- 是否支撑核心 Job；
- 是否是业务闭环必要步骤；
- 风险；
- Evidence 强度；
- 使用频率；
- 实现成本；
- 是否可以手工兜底；
- 是否影响后续架构。

推荐每个 MVP Requirement 都回答：

```text
如果本期不做，会导致核心闭环无法成立吗？
```

---

# 17. Requirement Traceability——防止 AI 需求膨胀

建立最简单的链：

```text
Evidence
  ↓
Finding
  ↓
Requirement
  ↓
Business Rule
  ↓
Acceptance Criteria
  ↓
Design
  ↓
Code
  ↓
Test
```

例如：

```text
OBS-001
 ↓
F-006 Completion Claim != Closure
 ↓
REQ-LIFE-006
 ↓
BR-008
 ↓
AC-008-01/02/03
 ↓
Completion Flow
 ↓
API / Domain Service
 ↓
Integration Test
```

以后 AI 提出：

```text
“建议增加一键批量办结。”
```

团队可以先问：

```text
它对应哪个 Finding？
哪个 Job？
哪个 Requirement？
```

如果没有，就进入 Candidate Backlog，而不是直接 Coding。

---

# 18. Spec for Human 与 Spec for Agent

同一需求需要同时满足两类消费者。

## Human 需要

- 业务语义；
- 决策原因；
- Scope；
- 风险；
- 可读流程。

## Agent 需要

- 明确术语；
- 精确状态；
- 输入输出；
- Preconditions；
- Forbidden behavior；
- Edge Cases；
- AC；
- 文件 / Artifact 路径；
- 不允许自行决定的 Unknown。

因此一个优秀 Handbook 不是教你写“更长 Prompt”，而是教你构建**Agent 可以引用的 Context System**。

---

# 19. Coding Agent Contract

当 Requirement 尚未批准时，Prompt 应明确：

```text
You are not authorized to invent business rules.

If implementation requires a decision that is not defined in:
- glossary.md
- business-rules.md
- state-model.md
- acceptance-criteria.md

stop and report it as SPEC_GAP.
Do not choose a reasonable default silently.
```

这是后面 Coding Stage 会反复使用的机制。

目标不是让 AI 什么都不做，而是：

```text
Known → Implement
Unknown → Escalate
Conflict → Report
Assumption → Label
```

---

# 20. AI Requirement Review：让 AI 扮演 Challenger，而不是作者

生成完需求后，换一个上下文让 AI Review：

```text
检查以下 Specification：

1. Ambiguous terms
2. Missing actor
3. Missing precondition
4. Missing permission
5. Missing error path
6. Missing state transition
7. Conflicting business rules
8. Untraceable requirement
9. UI detail incorrectly treated as business rule
10. Architecture decision leaking into requirement
11. Unverified numeric NFR
12. Requirement without acceptance criteria
13. Acceptance criteria that cannot be tested
14. Hidden assumption

不要重写需求。
先输出问题清单和严重程度。
```

这种 Reviewer 模式通常比让同一个 Prompt “自己检查自己”效果更好。

---

# 21. 更多案例：从口头需求到可执行 Spec

## Case A — “超过 7 天没更新就算异常”

Discovery Evidence 已经告诉我们这是危险的。

错误：

```text
7 天未更新 → status = ABNORMAL
```

更合理：

```text
7 天只是候选 threshold；
STALE_UPDATE 是 Attention Signal；
是否构成 Delivery Risk 需要其他 Evidence。
```

## Case B — “进度 100% 自动办结”

错误：

```text
if progress == 100:
    status = CLOSED
```

Discovery 已发现 Completion Claim 与 Closure 可能不同。

因此必须先定义 Closure Rule。

## Case C — “领导需要驾驶舱”

错误：

```text
Requirement: 开发 12 张统计图表。
```

真实 Job：

```text
快速识别需要管理干预的事项。
```

Product Design 阶段再决定最合适的信息结构。

## Case D — “责任人必须填”

Discovery 表明正式责任可能只到部门，而个人执行属于内部管理。

因此不能因为数据库常见字段有 `user_id` 就创造 Business Rule。

---

# 22. Bad Practice

## 22.1 One-shot PRD

输入一句业务想法，让 AI 输出 50 页 PRD，然后直接开发。

问题不是 AI 写得差，而是它必须自行补大量 Unknown。

## 22.2 CRUD Requirement

```text
新增任务
修改任务
删除任务
查询任务
```

这是操作列表，不是业务需求。

## 22.3 UI-driven Requirement

```text
页面顶部放四个卡片。
```

如果还没完成 Product Design，这通常过早。

## 22.4 Architecture Leakage

```text
使用 Redis 实现提醒。
```

Requirements 不应该替 Architecture 做决定。

## 22.5 Fake Precision

```text
响应时间必须 < 200ms
可用性 99.999%
支持 10000 并发
```

没有依据的精确数字比 TBD 更危险。

## 22.6 Happy-path-only AC

只定义成功路径，没有权限、终态、重复提交、并发、边界条件。

---

# 23. Recommended Artifact Set

```text
requirements/
├── glossary.md
├── scope.md
├── prd.md
├── business-rules.md
├── state-model.md
├── user-stories.md
├── use-cases.md
├── acceptance-criteria.md
├── nfr.md
└── traceability.md
```

小项目可以合并，但大型企业项目建议保持关键规则独立，因为后续 AI Agent 可以精准加载需要的 Context，而不是每次读取一个超长 PRD。

---

# 24. Gate 2 — Requirements → Product Design Readiness

## Language
- [ ] 核心 Glossary 已定义
- [ ] 同义词和易混词已处理
- [ ] 不存在关键模糊词无人负责

## Scope
- [ ] In Scope / Out of Scope 已明确
- [ ] MVP 形成业务闭环
- [ ] Future Candidate 没有混入 MVP

## Business Rules
- [ ] 核心规则有 ID
- [ ] Rule 可以回溯 Finding / Evidence
- [ ] Rule Owner / Human Review 明确
- [ ] Unknown 没有被 AI 偷偷补齐

## Lifecycle
- [ ] 核心对象状态已定义
- [ ] 状态与 Attention / Risk 等维度分离
- [ ] 关键 Transition 有 Actor / Preconditions / Effects
- [ ] Terminal State 明确

## Functional Requirements
- [ ] 核心 Job 有对应 Requirement
- [ ] Requirement 不是单纯页面清单
- [ ] 权限和异常路径已考虑

## Acceptance
- [ ] MVP Requirement 有可验证 AC
- [ ] 包含关键 Negative / Edge Case
- [ ] AC 不依赖未定义术语

## NFR
- [ ] 安全 / 审计 / 性能 / 可用性等已评估
- [ ] 没有未经依据的精确指标
- [ ] TBD 有 Owner 和后续动作

## Traceability
- [ ] Evidence → Requirement 可追踪
- [ ] Requirement → AC 可追踪
- [ ] 被删除 / 延后的需求有 Decision Record

## Decision
- [ ] PASS — Enter Product Design
- [ ] HOLD — Resolve Specification Gaps
- [ ] RETURN — More Discovery Needed

---

# 25. 本章闭环

```text
Discovery Evidence
      ↓
Glossary
      ↓
Scope
      ↓
Business Rules
      ↓
Lifecycle
      ↓
Stories / Use Cases
      ↓
Acceptance Criteria
      ↓
NFR
      ↓
Traceability
      ↓
Human Review
      ↓
Gate 2
      ↓
Product Design
```

最重要的变化是：

```text
过去：
需求 → 开发者理解 → Code

AI Native：
Evidence → Spec → Verification Contract → Agent → Code → Test
```

---

# 26. Learning Resources

## IREB — Requirements Engineering

https://www.ireb.org/

用于系统学习 Requirements Engineering 的专业知识体系。

## Agile Alliance — User Stories

https://agilealliance.org/glossary/user-stories/

用于理解 User Story 的价值和边界，避免把所有需求都压缩成一句 Story。

## Cucumber — Gherkin Reference

https://cucumber.io/docs/gherkin/reference

用于学习 Given / When / Then 和可执行 Acceptance Criteria 的表达方式。

## Martin Fowler — GivenWhenThen

https://martinfowler.com/bliki/GivenWhenThen.html

理解行为场景与验证契约之间的关系。

## GitHub Docs — About GitHub Copilot coding agent

https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent

用于理解现代 Coding Agent 如何围绕任务、代码库和验证工作，从而反向思考为什么 Specification 必须更加清晰。

---

# 27. 下一步：FlowOps Requirements 实战

下一组 Artifact 将不再停留在理论：

```text
templates/requirements/
prompts/requirements/
checklists/requirements/
examples/flowops/02-requirements/
```

FlowOps 会正式完成：

```text
Glossary
Scope / MVP
Business Rules
Lifecycle State Machine
User Stories
Use Cases
Acceptance Criteria
NFR
Traceability
PRD
```

并重点演示：

> 如何把 `findings.md` 中仍然带有冲突和 Unknown 的内容，逐步转化成 Coding Agent 可以执行、Human 可以 Review、Test Agent 可以验证的 Specification。
