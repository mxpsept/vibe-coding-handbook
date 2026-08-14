# FlowOps — All Items Wireframe Directions v0.1

## Primary Actor
Supervision Specialist

## Primary Job
快速定位、比较和管理组织范围内的督办事项。

---

# Direction A — Traditional Search Form + Table

```text
[任务名称____] [状态▼] [部门▼] [开始日期] [结束日期] [查询][重置]

┌─────────────────────────────────────────────────────────────┐
│ 序号 │ 编号 │ 标题 │ 状态 │ 进度 │ 部门 │ 日期 │ 操作 │
└─────────────────────────────────────────────────────────────┘
```

### Strength
容易实现，用户熟悉。

### Problems
- 高频关注条件和低频筛选权重相同；
- 顶部表单占用大量空间；
- “状态”容易混合 Lifecycle / Attention；
- 所有字段倾向进入 Table。

---

# Direction B — Work Views + Progressive Filters

```text
┌──────────────────────────────────────────────────────────────┐
│ 督办事项                                      [+ 新建事项]   │
│ [搜索事项...................................]                │
│                                                              │
│ Views: [全部] [办理中] [需关注] [待办结]                     │
│        ─────────────────────────────────────                 │
│ [责任部门▼] [截止日期▼] [更多筛选 3]       [保存视图]候选   │
├──────────────────────────────────────────────────────────────┤
│ 事项                                                         │
│                                                              │
│ 标题 / 编号       责任           期限       Lifecycle  Attention│
│ ------------------------------------------------------------ │
│ Item A             Dept A       Apr 30     办理中     超期3天 │
│ 最新进展摘要...                                              │
│ ------------------------------------------------------------ │
│ Item B             Dept B       May 05     待确认     —       │
└──────────────────────────────────────────────────────────────┘
```

### Strengths
- 高频工作视图优先；
- 高级筛选按需展开；
- Lifecycle 与 Attention 分列/分层；
- 标题可携带最新上下文，减少纯字段表格感。

### Risks
- Quick View 必须有稳定业务语义；
- Saved View 是否进入 MVP 需要 Scope 决策。

**Decision: Recommended foundation.**

---

# Direction C — Card Grid

```text
[Item Card] [Item Card] [Item Card]
[Item Card] [Item Card] [Item Card]
```

### Strengths
视觉轻松，单项可展示较多摘要。

### Weaknesses
- 大量事项比较效率低；
- 批量扫描困难；
- 企业运营场景信息密度不足。

**Decision: Reject for primary desktop list.**

---

# Column Priority

### Always visible candidate

```text
Title / Identifier
Accountable Department
Effective Due Date
Lifecycle
Attention
Last Update / Latest Progress cue
```

### Optional / secondary

```text
Source
Creator
Created Time
Executor (if approved)
Progress Percentage (if approved)
```

不要因为数据库有字段就默认展示。

# Interaction Candidates

- Row click → Item Detail；
- contextual quick action → Update Progress（仅适用角色）；
- Advanced Filters drawer/popover；
- sort by Effective Due Date / Last Update；
- column preferences future candidate；
- bulk action only when a validated Job exists。

# Empty States

区分：

```text
No items exist
No result for current filters
No items in this saved/quick view
Permission scope contains no items
```

它们不能全部显示“暂无数据”。
