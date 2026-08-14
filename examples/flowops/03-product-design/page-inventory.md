# FlowOps — Page Inventory v0.1

| ID | Page | Primary Actor | Primary Job | Core Content | MVP |
| --- | --- | --- | --- | --- | --- |
| P-001 | Workbench | all roles | 快速进入当前最重要工作 | action summary, attention entry, recent context | Yes |
| P-002 | My Work | responsible participant | 找到与我相关且需要处理的事项 | task views, due/attention, quick action | Yes |
| P-003 | All Supervision Items | supervision specialist | 查询和管理组织重点事项 | saved views, filters, table/list | Yes |
| P-004 | Attention | supervision specialist | 核验需要关注的事项 | attention queue, reason, context | Yes |
| P-005 | Item Detail | multiple | 理解单项完整上下文并执行允许动作 | header, current context, timeline, facts | Yes |
| P-006 | Create/Edit Item | authorized staff | 准备事项并完成正式下达前信息 | structured form | Yes |
| P-007 | Completion Claim | accountable party | 提交执行完成声明 | summary, evidence candidate | Yes |
| P-008 | Closure Review | closure authority | 审核待办结事项 | claim, evidence, history, decision | Conditional |
| P-009 | Management Review | manager | 找到需要管理干预的事项 | priority attention + explanation | Yes |
| P-010 | Configuration | administrator | 维护已批准的系统配置 | threshold etc. only after rule approval | Conditional |

## Page consolidation decisions

### Progress Update

不默认创建 `Progress Management` 页面。

建议作为：

```text
Item Detail → Update Progress
```

或 My Work 中的 Contextual Action。

### Overdue

不创建 `Overdue Management` 独立业务模块。

它可以是：

```text
Attention View
All Items Quick View
Management Review Context
```

### Audit

不创建普通用户一级 `Audit Management` 菜单。

Audit 与 Item Detail 绑定；系统级审计能力如未来有合规需求再独立设计。

## Page-level Design Questions

### P-001 Workbench
- 不应变成所有模块的缩略版。
- 需要根据角色决定内容优先级。

### P-003 All Items
- 需要决定 Default Columns / Quick Views / Advanced Filters。

### P-004 Attention
- 需要比较 Queue vs Table vs Split View 三种方向。

### P-005 Item Detail
- 必须避免 Form-like Reading Experience。

### P-009 Management Review
- 不默认要求图表；首先验证 Decision-support 信息结构。

## Route Candidates

```text
/workbench
/my-work
/items
/items/:id
/items/new
/attention
/closure-review
/management-review
/settings
```

Route 是设计候选，最终与 Frontend Architecture 对齐。
