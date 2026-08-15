# 01 — Discovery Log

## Problem Statement

企业重点工作散落在会议纪要、表格、聊天和个人记录中。管理者难以及时发现风险，执行人员重复汇报，督办人员大量时间用于人工汇总。

## Actors

| Actor | Job | Pain |
| --- | --- | --- |
| 任务下达人 | 明确事项和责任 | 下达后缺少持续反馈 |
| 执行责任人 | 推进任务并反馈 | 重复汇报、优先级不清 |
| 督办人员 | 跟踪、提醒、汇总 | 手工筛选临期/超期 |
| 管理者 | 识别风险并协调 | 信息滞后、报表与事实脱节 |

## Fact / Assumption / Unknown / Decision

### Facts for the fictional case
- 任务有明确责任主体和计划完成时间；
- 执行过程中需要多次进度反馈；
- 管理者关注异常而不是每条操作日志。

### Assumptions to validate
- 百分比进度对所有任务都有意义；
- 每个任务只有一个主责任人；
- 临期规则可以全企业统一。

### Unknowns
- 谁能修改完成时间？
- 责任人提交“完成”后是否立即结束任务？
- 协办人是否可修改主进度？
- 是否需要外部消息渠道？

### Decisions for MVP
- Completion Claim 与 Closure 分离；
- 外部通知不进入第一 Slice；
- Attention 与 Lifecycle 分离建模；
- UI 第一目标是“下一步行动清晰”，不是做大屏。

## Risks if We Skip Discovery

Coding Agent 很可能自行决定：
- `status = overdue`；
- 100% 自动等于已办结；
- 所有人都能看到所有任务；
- 临期固定 3 天；
- 首页先做大量 KPI 卡片。

这些都可能“看起来合理”，但都不是已批准业务事实。
