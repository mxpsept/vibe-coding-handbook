# 第 1 章：Product Discovery——先发现真正的问题，再定义系统

> Stage 00 回答“这个想法是否值得继续探索”。Stage 01 要回答一个更难的问题：**我们究竟在解决谁的什么问题？**

## 0. 本章目标

完成本章后，你应该能够：

- 理解 Discovery 与 Requirements、Design、Coding 的边界；
- 使用 AI 辅助 Stakeholder Mapping、访谈准备、访谈整理和问题归纳；
- 建立 `Fact / Evidence / Assumption / Unknown` 的证据链；
- 描述 As-Is Process，而不是直接设计 To-Be System；
- 从访谈中提取 Pain Point、Job、Constraint 和 Business Rule Candidate；
- 避免 AI 把“常见行业做法”伪装成真实需求；
- 为 FlowOps 形成第一版 Discovery Artifact；
- 使用 Gate 1 判断项目是否具备进入 Requirements Engineering 的条件。

---

# 1. Why：为什么不能直接问用户“你想要什么功能”

企业软件最常见的需求收集方式之一是：

```text
你们需要哪些功能？
```

然后得到：

```text
任务新增
任务编辑
任务查询
催办
消息提醒
统计分析
导出 Excel
领导驾驶舱
```

这看起来已经可以开发，但它存在一个根本问题：**Feature 是用户想到的 Solution，不一定是问题本身。**

例如用户说：

```text
我们需要一个“自动催办”功能。
```

背后的真实问题可能完全不同：

- 执行人员不知道任务已经临期；
- 责任人变更后没有同步；
- 督办人员每天人工筛 Excel；
- 任务状态长期没有更新；
- 管理者只在会议前才发现风险；
- 当前催办没有记录，事后无法追溯。

如果直接接受“自动催办”，我们可能很快开发出一个错误但功能完整的 Solution。

因此 Discovery 的第一原则是：

> **Do not start from features. Start from observed problems, jobs, behaviors and evidence.**

---

# 2. Discovery 不是“写 PRD 前开几个会”

Product Discovery 的目标不是快速收集一个功能清单，而是降低几个关键不确定性：

```text
Value Risk       用户真的需要吗？
Usability Risk   用户能否理解和使用？
Feasibility Risk 在现实约束下能否实现？
Viability Risk   对组织和业务是否可持续？
```

在企业项目中，还经常存在第五种风险：

```text
Process Risk     我们理解的流程是真实流程，还是会议室里的理想流程？
```

因此 Discovery 的输出不是“最终需求”，而是越来越可靠的 Evidence。

```text
Idea
 ↓
Questions
 ↓
Stakeholders
 ↓
Evidence Collection
 ↓
As-Is Process
 ↓
Pain Points / Jobs
 ↓
Validated Findings
 ↓
Discovery Gate
```

---

# 3. Discovery、Requirements、Design 的边界

这三个阶段非常容易混在一起。

| 阶段 | 核心问题 | 典型输出 |
| --- | --- | --- |
| Discovery | 问题真实是什么？谁受影响？为什么？ | Findings / As-Is / Evidence |
| Requirements | 系统必须满足什么？边界是什么？ | PRD / Rules / AC / NFR |
| Product Design | 用户如何通过产品完成任务？ | IA / User Flow / Page Spec |

例如：

```text
Discovery Finding:
督办人员每天需要从多个 Excel 中筛选即将到期任务，通常耗时 30～60 分钟。

Requirement Candidate:
系统应能够识别满足临期规则的任务。

Product Design Candidate:
工作台提供“临期事项”入口和数量提示。

UI Candidate:
使用橙色状态 Tag 展示剩余天数。
```

如果 Discovery 阶段直接跳到橙色 Tag，我们就过早跨越了多个决策层。

---

# 4. Evidence Ladder：不要让所有信息拥有相同可信度

AI Native 项目必须特别重视信息来源，因为 AI 非常擅长把“合理推测”写得像“已确认事实”。

建议使用以下证据层级：

```text
E0 — Unknown
E1 — Assumption
E2 — Stakeholder Statement
E3 — Observed Behavior / Existing Artifact
E4 — Repeated Evidence
E5 — Validated Business Fact
```

例如：

```text
“执行人员不愿意填报进度”
```

如果只是项目经理猜测：E1。

如果一个督办人员这么说：E2。

如果我们观察到 100 条任务中 62 条超过 7 天未更新：E3。

如果多个部门访谈和历史数据都支持这个结论：E4。

经过业务负责人 Review 后，可以作为当前 Project Truth：E5。

这能防止：

```text
AI suggestion
    ↓
Sounds reasonable
    ↓
Written into PRD
    ↓
Becomes “requirement”
```

---

# 5. 第一步：Stakeholder Mapping

不要只访谈提出项目的人。

企业系统通常存在：

```text
Decision Maker
Process Owner
Operator
Executor
Collaborator
Administrator
Compliance / Security
IT / Operations
Downstream Consumer
```

对于 FlowOps，我们当前只有角色假设：管理者、督办人员、部门负责人、执行人员、系统管理员。

Discovery 要验证：

- 这些角色是否真实存在；
- 是否遗漏关键角色；
- 谁拥有业务规则决定权；
- 谁是高频使用者；
- 谁承担流程成本；
- 谁可能抵触新系统；
- 谁只是看数据，不参与流程。

一个简单的 Stakeholder Map：

| Stakeholder | Role in process | Pain exposure | Decision power | Usage frequency | Interview priority |
| --- | --- | --- | --- | --- | --- |
| A |  | High/Med/Low | High/Med/Low |  | P0/P1/P2 |

AI 可以帮助排序，但不能凭空决定真实组织关系。

---

# 6. 第二步：准备访谈，而不是让 AI 替你访谈

AI 非常适合生成 Interview Guide，但真实 Evidence 应来自真实 Stakeholder、数据或现有业务材料。

## 6.1 不好的问题

```text
你觉得做一个督办系统好吗？
你需要自动提醒吗？
你需要领导驾驶舱吗？
```

这些问题具有明显诱导性。

## 6.2 更好的问题

```text
请回忆最近一次需要督办的重点任务。
它最初从哪里产生？
谁把它记录下来？
之后信息经过了哪些人？
你在哪里查看截止时间？
上一次任务超期是什么时候发现的？
你当时做了什么？
哪一步最耗时间？
有没有出现过 Excel 与群消息不一致？
如果今天停止使用现有 Excel，会造成什么影响？
```

重点是询问**过去真实发生的行为**，而不是让用户预测未来想要什么。

---

# 7. 第三步：重建 As-Is Process

企业项目中一个非常重要的 Discovery Artifact 是当前流程，而不是未来系统流程。

例如 FlowOps 可能通过访谈得到如下候选流程：

```text
会议形成重点事项
      ↓
督办人员整理会议记录
      ↓
录入 Excel
      ↓
通过群 / 电话通知部门
      ↓
部门内部安排责任人
      ↓
执行人员开展工作
      ↓
督办人员定期询问进度
      ↓
更新 Excel
      ↓
会议前人工汇总
      ↓
管理者查看风险事项
```

注意：这只是示例。Discovery 必须通过 Evidence 验证。

As-Is Process 建议对每个步骤记录：

| Step | Actor | Input | Action | Tool | Output | Pain | Evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |  |

这张表往往比几十条功能需求更有价值，因为它揭示了系统真正要介入的位置。

---

# 8. 第四步：从抱怨中提取 Pain Point

用户会说：

```text
这个 Excel 太麻烦。
```

不要直接记录成：

```text
Requirement: 替换 Excel。
```

继续拆解：

```text
麻烦在哪里？
什么时候最明显？
多久发生一次？
谁受到影响？
造成什么后果？
现在如何绕过去？
```

最终可能得到：

```text
Pain Point:
每周经营会前，督办人员需要从 5 个部门分别收集最新 Excel，
手工合并约 80 条重点事项，平均耗时约 2 小时，且经常出现版本不一致。
```

这才是可以进入 Project Truth 的候选 Finding。

建议每个 Pain Point 至少包含：

```text
Who
When
Current behavior
Pain
Impact
Frequency
Evidence
Confidence
```

---

# 9. 第五步：识别 Job，而不是只记录 Pain

只知道用户痛苦还不够，还需要知道用户真正试图完成什么。

例如：

```text
Feature request:
我要一个 Dashboard。

Pain:
每次领导问“哪些重点工作有风险”，我都要临时整理 Excel。

Job:
在管理会议前快速识别需要领导关注的重点事项，并说明风险原因。
```

Job 比 Feature 更稳定。

未来 Dashboard、报告、搜索、AI Summary 都可能完成同一个 Job。

因此 Discovery 应尽量形成：

```text
When <situation>,
I want to <job>,
so I can <outcome>.
```

但不要为了套模板而扭曲真实业务语言。

---

# 10. 第六步：识别 Constraint 和 Business Rule Candidate

访谈中经常出现这样的句子：

```text
这个任务只有办公室才能下达。
跨部门事项必须由分管领导确认。
任务延期要说明原因。
办结后不能直接删除。
```

不要立即全部写入正式 Business Rules。

先标记为：

```text
Business Rule Candidate
Source
Evidence Level
Need Validation
```

原因是不同 Stakeholder 可能给出不同版本。

例如：

```text
督办人员：所有延期都需要审批。
部门负责人：普通事项延期不用审批。
```

Discovery 的任务是暴露冲突，而不是让 AI 选择一个“看起来更合理”的答案。

---

# 11. AI 在 Discovery 中最适合做什么

AI 的强项不是替代真实 Evidence，而是加速 Evidence Processing。

适合：

- 根据 Project Idea 生成 Stakeholder 候选；
- 生成 Interview Guide；
- 对访谈记录进行结构化；
- 提取 Pain / Job / Rule Candidate / Unknown；
- 比较多份访谈中的一致与冲突；
- 生成 As-Is Process 草案；
- 发现遗漏问题；
- Challenge 团队假设；
- 生成下一轮访谈问题；
- 维护 Traceability。

不适合直接决定：

- 真实业务流程；
- 最终业务规则；
- Stakeholder 的真实优先级；
- 用户是否真的需要某 Feature；
- 组织内部权责关系。

一个重要原则：

> **AI can synthesize evidence; AI cannot manufacture evidence.**

---

# 12. Context Pattern：如何把访谈交给 AI

不要只输入：

```text
帮我分析这份访谈。
```

推荐：

```text
Context:
- 当前处于 Product Discovery；
- 目标是理解现状，不设计未来系统；
- 已知 Project Idea：<artifact path>

Source:
- Stakeholder role: <role>
- Interview date: <date>
- Interview transcript: <content>

Rules:
1. 只基于 Source 提取信息；
2. 不补充行业常识作为事实；
3. 每个 Finding 标注 Evidence；
4. 不确定内容标记 Unknown；
5. 冲突内容不得自动合并；
6. Feature Request 必须继续追问背后的 Problem / Job。

Output:
- Facts
- Pain Points
- Jobs
- Business Rule Candidates
- Constraints
- Contradictions
- Unknowns
- Follow-up Questions
```

这就是 Context Engineering 在 Discovery 阶段的早期形态。

---

# 13. FlowOps Discovery：我们应该调查什么

FlowOps 在 Gate 0 已批准进入 Discovery，但以下内容仍然未知：

```text
真实任务来源
真实角色边界
真实 As-Is Process
任务如何下达
进度如何更新
临期如何定义
超期如何处理
是否存在延期
完成与办结关系
数据权限
管理者真正需要的信息
```

因此我们不会开始画 Dashboard。

第一轮 Discovery Plan 可以是：

| Activity | Target | Goal |
| --- | --- | --- |
| Interview | 督办人员 | 理解端到端现状和高频成本 |
| Interview | 部门负责人 | 理解接收、分派、协调过程 |
| Interview | 执行人员 | 理解实际办理和进度反馈行为 |
| Interview | 管理者 | 理解决策 Job，而不是收集图表偏好 |
| Artifact Review | Excel / 会议纪要 / 催办记录 | 验证字段、流程和历史行为 |
| Observation | 周会前汇总过程 | 发现访谈中没有说出的真实操作 |

这比“让 AI 设计一套督办系统”慢一点，但获得的是未来所有 Spec 的证据基础。

---

# 14. FlowOps 示例：一次访谈如何转成 Finding

假设我们有一段**教学用虚构访谈**：

```text
督办专员：每周四下午我要准备周五的经营会材料。
各部门会把自己的 Excel 发给我，但模板有时候被改过。
我一般要花两个小时合并，还要在群里问没有更新的事项。
有时候负责人说已经完成了，但 Excel 还是上周的状态。
领导最关心的是哪些任务可能超期，以及为什么。
```

AI 不应该直接输出：

```text
系统需要自动催办、Dashboard、Excel 导入和风险预测。
```

正确提取应该类似：

### Facts / Statements

- 每周四准备周五经营会材料；
- 部门通过 Excel 提交信息；
- Excel 模板存在不一致；
- 需要人工询问未更新事项；
- 状态信息可能滞后于实际进展。

### Pain Candidate

```text
Who: 督办专员
When: 周会前
Behavior: 合并部门 Excel + 群内询问
Pain: 信息格式和状态不一致
Impact: 约 2 小时人工整理，并存在状态滞后风险
Evidence: Interview-DO-001
Confidence: E2，待 Artifact / Observation 验证
```

### Job Candidate

```text
在经营会前快速形成可信的重点任务风险清单，
以便管理者聚焦需要干预的事项。
```

### Unknown

```text
“2 小时”是否具有普遍性？
所有部门是否都使用 Excel？
什么条件被认为“可能超期”？
负责人为何不及时更新？
```

### Feature Requests

此时：**None confirmed.**

---

# 15. Discovery Artifact Set

对于典型企业项目，本 Handbook 推荐 Stage 01 至少形成：

```text
discovery/
├── stakeholder-map.md
├── discovery-plan.md
├── interview-guide.md
├── interviews/
│   └── ...
├── as-is-process.md
├── findings.md
└── discovery-summary.md
```

小项目可以合并文件。

重点不是目录完整，而是以下信息必须可追踪：

```text
Finding
   ↓
Evidence
   ↓
Source
   ↓
Confidence
   ↓
Open Question
```

---

# 16. Prompt：Discovery Interview Analyzer

```text
你是 Product Discovery Analyst。

当前阶段：Discovery。
目标：理解真实现状和问题，不设计最终系统。

Project Idea:
<引用 project-idea.md>

Interview Source:
- Interview ID: <ID>
- Stakeholder Role: <role>
- Date: <date>
- Transcript / Notes:
<content>

规则：
1. 只把 Source 明确支持的内容列为 Evidence；
2. 不使用行业常识补充事实；
3. 区分 Fact / Statement / Assumption / Unknown；
4. Feature Request 不直接升级为 Requirement；
5. 尝试追溯 Feature Request 背后的 Problem / Job；
6. 冲突信息单独列出；
7. Business Rule 只标记 Candidate；
8. 每个 Finding 给出 Evidence Level；
9. 如果证据不足，明确写“需要验证”。

输出：
A. Summary
B. Facts / Statements
C. Pain Points
D. Jobs
E. Business Rule Candidates
F. Constraints
G. Feature Requests（仅记录，不批准）
H. Contradictions
I. Unknowns
J. Follow-up Questions
K. Suggested Evidence to collect next

最后 Self Review：
- 是否把推测写成事实？
- 是否提前设计 Solution？
- 是否遗漏冲突？
- 是否能从每个关键 Finding 回溯到 Source？
```

---

# 17. Bad Practice：Discovery 最常见的 AI 失控

## 17.1 Synthetic User Trap

让 AI 扮演 10 个用户，然后把模拟访谈当真实用户研究。

AI Persona 可以帮助准备问题，但不能替代 Evidence。

## 17.2 Consensus Hallucination

三份访谈有冲突，AI 为了生成“漂亮总结”自动合并成统一流程。

冲突本身可能就是最重要的 Finding。

## 17.3 Feature Gravity

一看到 Pain 就开始设计功能。

```text
Pain → Feature
```

中间至少应该经过：

```text
Pain → Cause → Job → Evidence → Requirement Candidate
```

## 17.4 HiPPO Becomes Truth

最高职位的人说一句话，就直接成为系统需求。

管理者拥有 Decision Power，但不一定最了解高频操作流程。

## 17.5 Document Theater

AI 一次生成几十页“调研报告”，但所有内容都来自最初 5 句话。

文档长度不能替代 Evidence。

---

# 18. Review：Discovery Review 应该问什么

不要只 Review 文档格式。

重点问：

```text
我们访谈了正确的人吗？
有没有只听管理者，没有听执行者？
哪些 Finding 有 Evidence？
哪些只是单一 Stakeholder Statement？
有没有真实 Artifact 支撑？
As-Is 是真实流程还是制度流程？
有没有关键冲突没有解决？
哪些 Pain 是高频、高影响？
哪些 Feature Request 其实没有 Problem Evidence？
是否已经知道“为什么现在的方式不够好”？
```

---

# 19. Gate 1：Discovery → Requirements Readiness

## Problem Evidence

- [ ] 核心 Problem 已有 Evidence 支撑；
- [ ] 不再仅依赖项目发起人的主观描述；
- [ ] 关键 Pain Point 已识别 Who / When / Impact；
- [ ] 已识别主要 Job。

## Stakeholders

- [ ] 主要 Stakeholder 已识别；
- [ ] 高 Decision Power 与高 Usage Frequency 角色均被覆盖；
- [ ] 已识别 Business Rule Owner。

## Process

- [ ] 已形成可 Review 的 As-Is Process；
- [ ] 流程关键步骤有 Source；
- [ ] 制度流程与真实操作差异已记录。

## Evidence Quality

- [ ] Fact / Assumption / Unknown 已分开；
- [ ] 关键 Finding 可回溯到 Evidence；
- [ ] 冲突没有被 AI 擅自消除；
- [ ] 关键假设已有验证计划或结果。

## Scope Readiness

- [ ] 已能描述主要问题域；
- [ ] Feature Request 仍与正式 Requirement 分开；
- [ ] 已识别明显 Out of Scope 候选；
- [ ] 已知道 Requirements 阶段最需要定义哪些规则。

## Decision

- [ ] PASS — Enter Requirements Engineering
- [ ] HOLD — Continue Discovery
- [ ] PIVOT — Reframe Problem
- [ ] STOP / PARK

---

# 20. 本章形成的闭环

```text
Project Idea
     ↓
Stakeholder Map
     ↓
Interview / Observation / Artifact Review
     ↓
Evidence
     ↓
As-Is Process
     ↓
Pain / Job / Rule Candidate
     ↓
Discovery Findings
     ↓
Human Review
     ↓
Gate 1
     ↓
Requirements Engineering
```

从这里开始，我们已经不再依赖一句“帮我开发督办系统”。

未来的 Requirement、UI、Architecture 和 Code 都应该能够逐步回溯到这里的真实问题。

---

# 21. Learning Resources

## Level A — Primary / Official

### Atlassian Team Playbook — Customer Interview

https://www.atlassian.com/team-playbook/plays/customer-interview

**为什么阅读：** 学习如何组织访谈、准备问题并围绕真实用户经验收集信息。

### GOV.UK Service Manual — User Research

https://www.gov.uk/service-manual/user-research

**为什么阅读：** GOV.UK 对持续用户研究、研究计划、招募和研究方法提供了非常工程化的实践资料，尤其适合理解“Evidence 而不是意见”的工作方式。

### Nielsen Norman Group — User Interviews

https://www.nngroup.com/articles/user-interviews/

**为什么阅读：** 理解访谈适合回答什么、不适合回答什么，以及如何减少诱导问题。

## Level B — High Quality Product Sources

### Product Talk — Continuous Discovery

https://www.producttalk.org/

**为什么阅读：** 理解 Discovery 不应该只是项目开始前的一次活动，而应成为持续降低产品风险的机制。

### Strategyzer — Jobs to Be Done

https://www.strategyzer.com/library/jobs-to-be-done

**为什么阅读：** 帮助从 Feature Request 转向用户真正试图完成的 Job 和 Outcome。

---

# 22. 下一步

本章正文完成后，下一组 Artifact 将把方法真正落到 FlowOps：

```text
templates/discovery/stakeholder-map.template.md
templates/discovery/interview-guide.template.md
templates/discovery/findings.template.md
prompts/discovery/interview-analyzer.prompt.md
checklists/discovery/requirements-readiness.md
examples/flowops/01-discovery/
```

FlowOps 会使用完全虚构的访谈资料演示完整 Discovery，但会明确标记 Synthetic Case Evidence，避免把教学模拟数据误认为真实用户研究。
