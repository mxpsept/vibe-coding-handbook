# FlowOps — Requirements Glossary v0.1

> Synthetic Teaching Case。术语来自 Discovery Findings，状态为 Draft，需 Human Review 后冻结。

| Term | Definition | Not the same as | Trace | Status |
| --- | --- | --- | --- | --- |
| Supervision Item | 被正式纳入组织重点跟踪范围的工作事项 | 普通个人 Todo | F-008 | Draft |
| Accountable Department | 对事项交付结果承担组织责任的部门 | Executor / Collaborator | F-002 | Draft |
| Executor | 部门内部实际承担具体执行工作的人员 | Accountable Department | F-002 | Draft |
| Collaborator | 对事项交付提供协作、材料或其他输入的参与方 | Accountable Department | F-007 | Draft |
| Progress Update | 对事项最新执行情况的一次不可覆盖的过程记录 | Lifecycle State | F-003 | Draft |
| Progress Percentage | 对完成程度的数值表达；是否进入 MVP 仍待验证 | Status / Risk | F-003 | Candidate |
| Last Progress Update Time | 最近一条有效 Progress Update 的时间 | 实际工作最后发生时间 | F-004 | Draft |
| Stale Update | 进度信息超过约定时间未更新形成的 Attention Signal | Delayed / Overdue | F-004 | Draft |
| Due Date | 当前有效的要求完成日期 | Near-due threshold | F-006 | Draft |
| Near Due | 距有效 Due Date 进入约定关注窗口 | Lifecycle State | BR-C007 | Draft |
| Overdue | 已超过有效 Due Date 且事项未处于终态 | Closure | BR-C006 | Draft |
| Attention Flag | 提示需要关注或核验的独立信号 | Lifecycle State | F-003/F-004 | Draft |
| Completion Claim | 责任方声明执行工作已经完成 | Closure | F-006 | Draft |
| Closure | 经适用规则确认后，事项正式结束督办生命周期 | Completion Claim | F-006 | Draft |
| Effective Due Date | 考虑已批准延期后当前用于期限判断的日期 | Original Due Date | BR-C004 | Draft |
| Business Rule | 不依赖具体 UI/技术实现的业务约束 | Implementation Decision | Stage 02 | Draft |

## Ambiguities to resolve

1. 是否所有事项都必须存在 Executor？
2. Progress Percentage 是否具有统一业务语义？
3. Collaborator 与 Dependency 是否需要拆成两个概念？
4. Closure Authority 是固定角色还是按事项类型变化？
5. Near Due 阈值是全局、按类型还是按事项配置？

## Rule

后续 Artifact 如果使用未在本 Glossary 定义且存在业务歧义的词，应先补充定义，而不是让 AI 自行解释。
