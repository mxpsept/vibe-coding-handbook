# FlowOps — Critical User Flows v0.1

> User Flow 先描述用户如何完成 Job，再决定页面和组件。

## UF-001 — Responsible Participant Updates Progress

```text
My Work
  ↓
Locate item needing action
  ↓
Item Detail
  ↓
Review current context + previous progress
  ↓
Update Progress
  ↓
Enter update
  ↓
Validate
 ├─ invalid → explain + preserve input
 └─ valid
      ↓
Submit
      ↓
Success feedback
      ↓
Timeline shows appended record
```

### UX goals
- 高频路径短；
- 提交失败不丢输入；
- 更新前能看到当前上下文；
- 提交后立即确认历史已追加。

### Anti-pattern

```text
My Work → Progress Management → Search Task → Edit Current Progress → Save
```

这会让业务对象上下文丢失，并诱导覆盖历史。

---

## UF-002 — Supervision Specialist Reviews Attention

```text
Attention
  ↓
Choose attention view/filter
  ↓
Scan queue
  ↓
Select item
  ↓
Understand WHY attention exists
  ↓
Inspect latest progress / responsibility / deadline
  ↓
Human decision
 ├─ no follow-up needed
 ├─ contact responsible party
 └─ escalate / coordinate outside system (MVP)
```

### UX goals
- Attention Reason 第一屏可理解；
- `STALE_UPDATE` 不展示成“执行延期”；
- 尽量减少 Queue ↔ Detail 往返。

### Candidate pattern
Split View 值得优先验证。

---

## UF-003 — Create and Issue Item

```text
All Items / Workbench
  ↓
Create Item
  ↓
Draft form
  ↓
Save Draft
  ↓
Review required issue information
  ↓
Issue
  ↓
Server validates BR-002 / BR-003 / permission
 ├─ invalid → field/business error
 └─ valid → ISSUED + audit
```

### Design question
Create 和 Issue 不应被错误合并成“保存后自动下达”，因为 Lifecycle 明确区分 Draft 与 Issued。

---

## UF-004 — Submit Completion Claim

```text
Item Detail (IN_PROGRESS)
  ↓
Submit Completion
  ↓
Completion Summary
  ↓
Evidence if applicable
  ↓
Confirm Claim
  ↓
Validation
  ↓
PENDING_CLOSURE
  ↓
Success state explains:
“已提交办结申请/完成声明，等待正式确认”
```

### Critical copy rule
不能显示：

```text
任务已完成 / 已办结
```

因为 Closure 尚未发生。

---

## UF-005 — Closure Review

```text
Closure Review Queue
  ↓
Open pending item
  ↓
Review completion summary
  ↓
Review progress / evidence / key facts
  ↓
Approve Closure
  ↓
CLOSED
```

Reject/Return path remains DESIGN_SPEC_GAP because Requirements 未确认。

设计不得自行增加“驳回”按钮并定义业务效果。

---

## UF-006 — Manager Finds Intervention Item

```text
Management Review
  ↓
Scan prioritized attention
  ↓
Select item
  ↓
Understand:
- why attention
- accountable department
- deadline
- latest progress
- blocker/dependency if known
  ↓
Decide whether management intervention is needed
```

### UX success metric candidate
不是“图表数量”，而是：

```text
Time to identify and understand intervention candidates
```

具体量化目标需后续 usability test 建立 baseline。

---

## Flow Review Questions

对每条 Critical Flow Review：

1. 用户从哪里开始？
2. 是否需要重复寻找同一对象？
3. 是否出现无意义页面跳转？
4. 操作前是否有足够上下文？
5. 失败是否可恢复？
6. 成功反馈是否表达正确业务语义？
7. 是否有权限/状态导致动作不可用？
8. 是否存在 SPEC_GAP？
