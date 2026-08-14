# FlowOps — Stakeholder Map

> Evidence status: Synthetic teaching case based on the FlowOps CASE-SPEC. This is not real user research.

## 1. Discovery Goal

验证 Northstar Group 重点任务督办问题的真实流程、主要角色、决策关系和高频痛点，为后续 Requirements 提供 Evidence。

## 2. Stakeholders

| ID | Stakeholder | Current role hypothesis | Pain exposure | Decision power | Usage frequency | Interview priority |
| --- | --- | --- | --- | --- | --- | --- |
| ST-001 | 督办专员 | 汇总、跟踪、催办重点事项 | High | Med | High | P0 |
| ST-002 | 部门负责人 | 接收事项、协调部门执行 | Med | Med | Med | P0 |
| ST-003 | 执行人员 | 实际办理并反馈进展 | High | Low | High | P0 |
| ST-004 | 管理者 | 关注整体执行和风险事项 | Med | High | Med | P0 |
| ST-005 | 督办负责人 | 负责督办规则和重大事项协调 | High | High | High | P0 |
| ST-006 | 系统管理员 / IT | 后续可能维护用户权限和系统运行 | Low | Low | Med | P2 |

## 3. 为什么不能只访谈管理者

如果只问管理者，可能得到：

```text
我要一个驾驶舱。
我要看到红黄绿状态。
我要自动生成周报。
```

但执行人员可能真正面对的是：

```text
不知道哪些事项必须更新；
重复在 Excel 和群里填相同内容；
任务责任发生变化但没有同步；
填报字段与实际工作不匹配。
```

两类 Evidence 都重要，但回答的是不同问题。

## 4. Decision Owner Hypotheses

| Decision area | Candidate owner | Status |
| --- | --- | --- |
| 哪些事项属于督办范围 | 督办负责人 / 管理层 | Validate |
| 任务如何下达 | 督办负责人 | Validate |
| 临期与超期规则 | 督办负责人 | Validate |
| 部门内部责任分配 | 部门负责人 | Validate |
| 最终办结规则 | Unknown | Validate |
| 数据可见范围 | Unknown | Validate |

## 5. Coverage Decision

第一轮 Discovery 优先：

1. ST-001 督办专员；
2. ST-003 执行人员；
3. ST-002 部门负责人；
4. ST-004 管理者；
5. ST-005 督办负责人。

原因：先理解高频真实流程，再让 Decision Owner 对规则和差异进行确认。
