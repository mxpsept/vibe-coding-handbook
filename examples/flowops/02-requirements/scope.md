# FlowOps — Scope & MVP v0.1

> Synthetic Teaching Case。Scope 由 Discovery Evidence 推导，但仍需要 Product Owner / Business Owner Review。

## 1. Product Outcome

让重点事项从建立、责任、执行更新、期限关注到正式办结形成可信的组织级闭环，并降低周会前人工汇总与风险确认成本。

## 2. MVP Business Loop

```text
Create Item
  ↓
Issue / Establish Accountability
  ↓
Execute
  ↓
Progress Update
  ↓
Attention Evaluation
  ↓
Completion Claim
  ↓
Closure
  ↓
Audit / History
```

## 3. In Scope — MVP

| ID | Capability | Why |
| --- | --- | --- |
| S-001 | 建立督办事项 | 闭环起点 |
| S-002 | 记录事项来源与要求 | 支撑可追踪性 |
| S-003 | 维护责任部门 | Discovery 已证明核心责任维度 |
| S-004 | 设置有效截止日期 | 支撑期限管理 |
| S-005 | 下达/进入执行状态 | 建立正式生命周期 |
| S-006 | 提交追加式 Progress Update | 减少状态覆盖造成的信息丢失 |
| S-007 | 识别 Near Due / Overdue / Stale Update 等 Attention | 支撑风险核验 Job |
| S-008 | 提交 Completion Claim | 区分“执行完成”与正式结束 |
| S-009 | Closure 确认 | 形成督办闭环 |
| S-010 | 查询我的/部门/关注事项 | 支撑不同角色工作入口 |
| S-011 | 查看历史与审计 | 企业过程可追溯 |
| S-012 | 基础管理视图 | 支撑识别需干预事项的 Job，而非预设大量图表 |

## 4. Conditional MVP Candidates

以下内容在规则确认后决定是否纳入：

- Executor 个人责任；
- Collaborator 结构化管理；
- Progress Percentage；
- 延期申请/审批；
- 附件作为办结证据；
- 自动消息提醒。

## 5. Out of Scope — MVP

- 通用 BPM / 工作流设计器；
- 甘特图、资源排期、成本管理等完整项目管理能力；
- 企业即时通讯；
- 通用文档管理系统；
- AI 自动决定任务是否应该办结；
- AI 自动修改责任关系；
- 自定义 BI 报表平台；
- 原生移动 App；
- 面向外部客户的协作门户。

## 6. Future Candidates

- 企业微信/邮件/消息平台集成；
- AI 周报与风险摘要；
- 跨事项依赖；
- 多级督办体系；
- 复杂 SLA；
- 移动端；
- 高级统计分析。

## 7. Explicit Non-goals

FlowOps MVP 不试图替代：

```text
Project Management System
Document Management System
Instant Messaging
Generic Workflow Engine
ERP
```

它解决的是“组织重点事项督办闭环”。

## 8. Scope Change Rule

任何新增 MVP 能力必须回答：

1. 对应哪个 Job / Finding？
2. 不做是否导致核心闭环不成立？
3. 是否存在低成本人工兜底？
4. 是否需要新增 Business Rule？
5. 是否影响当前 Gate 2？

不能仅因为“AI 很容易实现”就进入 MVP。
