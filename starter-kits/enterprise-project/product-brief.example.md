# Product Brief — Example

## Product
FlowOps — 企业任务督办与协同平台（虚构案例）

## Problem
跨部门重点任务通过会议纪要、表格和聊天消息分散管理，管理人员难以及时识别临期/超期事项，执行人员也缺少统一的责任、进度和反馈入口。

## Primary Actors
- Task Owner：推进和反馈任务；
- Responsible Manager：关注负责范围内执行情况；
- Supervisor：创建/督办/核验事项；
- Leadership Viewer：查看汇总与重点风险。

## Outcomes
- 重点事项拥有统一责任和时限；
- 执行状态可以被持续追踪；
- 临期/超期风险能被主动识别；
- 管理者无需人工汇总多个表格即可查看关键风险。

## Non-goals — First Release
- 不建设通用 OA/BPM 平台；
- 不替代即时通讯；
- 不实现复杂绩效考核；
- 不接入所有第三方消息渠道；
- 不通过 AI 自动决定业务责任或处罚。

## Constraints
- Web-first enterprise application；
- 权限必须由服务端执行；
- 审计关键业务动作；
- 第三方通知属于后续独立 Integration Slice。

## First Critical Workflow

```text
Supervisor creates item
→ responsible actor sees it
→ actor submits progress
→ system derives attention
→ supervisor reviews current situation
```

## First Vertical Slice Candidate

```text
authorized task list
→ task detail
→ progress update
→ persisted result
→ audit/evidence
```

## Unknowns
- 组织权限的最终粒度；
- 是否需要正式“签收”动作；
- 超期升级等级阈值；
- 外部通知 provider。

这些 Unknown 不应由 Coding Agent 自动补齐。
