# 02 — Glossary & Critical Workflow

## Glossary

| Term | Definition | Not the same as |
| --- | --- | --- |
| Task Item | 被正式下达并需要跟踪的工作事项 | 普通个人 Todo |
| Owner | 对推进结果承担主要责任的人/角色 | Creator |
| Progress Update | 某时点的执行事实和说明 | Task lifecycle |
| Completion Claim | 执行方声明工作已完成，等待确认 | Closed |
| Closure | 有权限角色确认事项结束 | 100% progress |
| Attention | 基于事实派生的关注原因 | Lifecycle status |
| Overdue | 当前时间超过 dueAt 且事项仍满足 active 条件 | 一个永久 status |

## Critical Workflow

```text
Draft
  ↓ publish
Active
  ↓ progress updates
Active
  ↓ completion claim
Pending Closure
  ├─ reject → Active
  └─ approve → Closed
```

Attention 独立派生：

```text
Item facts + Clock + approved policy
→ NORMAL / DUE_SOON / OVERDUE / STALE_UPDATE ...
```

## Primary User Journey

### Execution
1. 责任人进入“我的待办”；
2. 看到需要行动的事项及风险原因；
3. 打开详情确认目标、时限、责任关系；
4. 填报进度与说明；
5. 完成后提交 Completion Claim。

### Supervision
1. 督办人员进入 Attention Workspace；
2. 优先查看 OVERDUE / DUE_SOON 等异常；
3. 进入事项查看最近进展；
4. 执行提醒/协调等动作；
5. 对完成声明进入 Closure Flow。

## Why Workflow before Menu

如果先问 AI“督办系统应该有哪些菜单”，很容易得到：Dashboard、Task Management、Statistics、Settings 等通用后台结构。

Workflow 先回答“人要完成什么”，菜单随后才是这些任务的导航实现。
