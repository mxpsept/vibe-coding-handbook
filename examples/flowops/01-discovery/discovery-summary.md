# FlowOps — Discovery Summary & Gate 1

> **Synthetic Teaching Case**。本 Summary 展示如何从多来源 Evidence 进入 Requirements，而不是宣称完成真实用户研究。

## 1. Problem Reframing

Stage 00 的问题最初可以概括为：

```text
重点任务通过 Excel、即时通讯、邮件和会议跟踪，
信息分散、责任不清、进度更新不及时、风险发现困难。
```

Discovery 后，问题被进一步重构为：

> Northstar Group 的重点任务执行信息跨多个组织层级和工具流转，责任、执行、进度更新、风险表达和最终办结之间缺少稳定语义与一致的事实来源。高频人工 Handoff 导致重复反馈、状态滞后、风险确认成本高，并使管理层难以及时获得可信的干预信息。

这个 Problem Statement 比“需要一个督办系统”更接近后续产品设计的真实基础。

## 2. What We Learned

### 关于责任

责任不是一个简单的“负责人”字段，至少需要继续区分：

```text
Accountable Department
Executor / Assignee
Collaborator / Dependency
Contact
```

是否全部进入系统仍需 Requirements 决策。

### 关于进度

必须避免：

```text
Progress = Status = Risk
```

Discovery 已显示信息更新时间、实际执行进展、任务状态和交付风险存在不同语义。

### 关于管理视图

“领导驾驶舱”目前不是已确认 Requirement。

已确认的是管理 Job：

> 快速识别需要干预的事项、风险原因和协调需求。

### 关于办结

“部门说完成”可能不是流程结束。Requirements 必须定义 Closure 的业务语义和权限。

## 3. What We Still Do Not Know

- 正式下达权；
- 是否签收；
- 是否强制个人责任人；
- 协办规则；
- 临期算法；
- 延期流程；
- 办结确认；
- 数据权限；
- 任务类型差异；
- 量化 Outcome Baseline。

这些 Unknown 不阻止我们进入 Requirements，但会成为 Requirements Workshop 的输入。

## 4. Requirements Input Candidates

下一阶段应该正式定义：

1. Task / Supervision Item 的业务边界；
2. Source / Type；
3. Accountability Model；
4. Lifecycle / State Model；
5. Progress Update Model；
6. Attention / Risk Model；
7. Deadline / Overdue / Near-due semantics；
8. Collaboration / Dependency；
9. Completion / Acceptance / Closure；
10. Permission / Data Scope；
11. Audit / History；
12. Reporting Jobs；
13. NFR 与企业约束。

## 5. Gate 1

### Problem Evidence
- [x] 核心 Problem 有多来源教学 Evidence 支撑
- [x] Pain 已覆盖多个角色
- [x] 主要 Jobs 已形成

### Stakeholders
- [x] 管理、督办、部门、执行视角均覆盖
- [x] Process Owner Candidate 已覆盖
- [ ] IT / Security 尚未深入（Requirements/NFR 前补充）

### Process
- [x] 已形成 As-Is v0.1
- [x] 已识别主要 Handoff
- [ ] 异常路径仍不完整

### Evidence Quality
- [x] Interview 与 Artifact / Observation 分开
- [x] Candidate 未自动升级为 Rule
- [x] 冲突被显式保留
- [x] 所有案例明确标记 Synthetic Teaching Case

### Decision

- [x] **PASS — Enter Requirements Engineering**
- [ ] HOLD
- [ ] PIVOT
- [ ] STOP / PARK

## 6. Human Gate Note

Gate 1 的 PASS 不表示“需求已经明确”。

它表示：

> 我们已经对 Problem Space 有足够理解，可以开始把被验证的问题转换为明确的系统边界、业务规则和 Acceptance Criteria。

下一阶段仍然必须允许新 Evidence 让团队返回 Discovery。

```text
Discovery → Requirements
      ↑           │
      └───────────┘
        New Unknown
```

这不是流程失败，而是正常迭代。
