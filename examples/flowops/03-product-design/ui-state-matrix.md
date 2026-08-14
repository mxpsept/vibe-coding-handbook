# FlowOps — UI State Matrix v0.1

> High-fi 截图只展示一个瞬间；真实产品必须覆盖状态空间。

## 1. Global State Categories

```text
Loading
Empty
No Result
Error
Partial Error
Unauthorized
Forbidden Action
Read-only
Submitting
Success
Conflict
Long Content
Large Data
Terminal State
```

## 2. Page Matrix

| Page | Loading | Empty | No Result | Error | Unauthorized | Read-only | Submitting | Conflict |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Workbench | Yes | role-specific | n/a | Yes | Yes | n/a | n/a | n/a |
| My Work | Yes | Yes | Yes | Yes | Yes | Yes | progress action | Yes |
| All Items | Yes | Yes | Yes | Yes | Yes | Yes | create/edit | Yes |
| Attention | Yes | Yes | Yes | Yes | Yes | Yes | future actions | n/a |
| Item Detail | Yes | n/a | n/a | Yes | Yes | Yes | Yes | Yes |
| Create/Edit | Yes(edit) | n/a | n/a | Yes | Yes | n/a | Yes | Yes |
| Closure Review | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Management Review | Yes | Yes | filter state | Partial possible | Yes | Yes | n/a | n/a |

## 3. Item Detail State Variants

### Loading
使用结构化 Skeleton，避免页面跳动。

### Not Found

```text
未找到该事项，或事项已不存在。
```

不要和 Permission Error 混淆。

### Unauthorized

```text
你没有权限查看该事项。
```

不要泄露敏感详情。

### Read-only
展示完整可见上下文，但不展示或禁用不适用动作；具体采用 hide vs disabled 由动作语义决定。

### IN_PROGRESS
可能动作：Update Progress / Submit Completion Claim。

### PENDING_CLOSURE
明确：

```text
完成声明已提交，等待正式办结确认
```

普通 Completion Action 不可重复执行。

### CLOSED
终态展示；普通 Progress Action 不可用。

## 4. Attention States

### No attention items

```text
当前没有需要核验的事项。
```

这是积极业务状态，不要只写“暂无数据”。

### Filter no result

```text
当前筛选条件下没有关注事项。
[清除筛选]
```

### Multiple flags

一个 Item 允许：

```text
STALE_UPDATE + NEAR_DUE
```

UI 不得强制选择其中一个作为“状态”。

## 5. Form States

### Field validation
紧邻字段。

### Business validation
例如 Issue 时缺少 Accountable Department，应明确说明无法下达原因。

### Server failure
保留用户输入，允许 Retry。

### Duplicate submit
提交按钮进入 Pending，服务端仍需处理幂等/并发语义。

## 6. Conflict State

例如用户打开 Item 后，另一用户修改了责任或期限。

具体并发策略由 Architecture 决定，但 UI 至少应预留：

```text
数据已发生变化，请刷新后重新确认操作。
```

不要静默覆盖。

## 7. Long Content Tests

High-fi / Frontend 至少测试：

```text
80+ char title
multi-paragraph progress
long department name
multiple attention flags
many progress records
many attachments candidate
```

禁止只用 `测试任务1`、`张三` 作为 UI 验证数据。

## 8. Large Data Tests

列表设计至少验证：

```text
0
1
10
100+
```

条记录的视觉和交互表现。

真实分页/虚拟化策略由 Architecture 根据数据规模决定。

## 9. Partial Failure

Management Review 如果未来包含多个独立数据源/图表：

```text
one widget failure != whole page failure
```

但是否采用独立请求由 Architecture 决定。

## 10. State Coverage Rule

任何 Page Spec 进入 Frontend Implementation 前必须声明：

```text
supported states
not-applicable states
unresolved states
```

未设计状态不能由 Coding Agent 自由决定。
