# 03 — Business Rules, State & Permission

## Business Rules

### BR-01 Completion is a claim
执行人提交完成只产生 `Completion Claim`，不会直接关闭事项。

### BR-02 Closure requires authorization
只有具有 Closure 权限且数据范围覆盖该事项的用户才能确认办结。

### BR-03 Attention is derived
`OVERDUE` 等关注原因由 Item facts + Clock + approved policy 派生，不写成主生命周期。

### BR-04 Progress does not drive lifecycle automatically
进度百分比用于表达执行估计，不允许 `progress = 100` 自动触发 Closed。

### BR-05 Deadline change is auditable
计划完成时间变更必须记录 old/new value、actor、time、reason。

## State Model

```text
DRAFT
  → ACTIVE
ACTIVE
  → PENDING_CLOSURE
PENDING_CLOSURE
  → ACTIVE       (claim rejected)
  → CLOSED       (claim approved)
DRAFT/ACTIVE/PENDING_CLOSURE
  → CANCELLED    (authorized cancellation)
```

任何未列出的 transition 默认不允许，直到业务批准。

## Permission Model

不要只维护“按钮权限”。至少拆成：

```text
Action Permission
×
Data Scope
×
State Constraint
```

示例：

| Action | Role Capability | Data Scope | State |
| --- | --- | --- | --- |
| view | viewer | visible organization/items | allowed |
| update progress | executor | assigned item | ACTIVE |
| claim completion | executor | assigned item | ACTIVE |
| approve closure | supervisor | supervised scope | PENDING_CLOSURE |
| change due date | authorized manager | managed scope | non-terminal |

## Test Consequence

每个重要动作至少测试：
- allowed role + allowed scope + allowed state；
- wrong role；
- wrong scope；
- wrong state。

前端隐藏按钮只是 UX，服务端仍必须执行同一业务授权语义。
