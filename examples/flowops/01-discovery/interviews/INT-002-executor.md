# INT-002 — 执行人员访谈

> **Synthetic Teaching Case**：以下内容完全虚构，仅用于演示 Discovery 方法。

## Metadata

- Source ID: INT-002
- Stakeholder: 执行人员
- Evidence base level: E2

## Interview Excerpt

**研究者：** 最近一次你收到重点任务后，是怎么知道自己要做什么的？

**执行人员：** 部门负责人一般在群里转会议要求，有时候会把 Excel 截图发出来，然后告诉我负责哪一项。

**研究者：** 你会直接维护那份 Excel 吗？

**执行人员：** 不一定。我们部门一般有一个人统一汇总。我把进展发给他，他再改表。有时候督办那边又在群里问，我就再发一次。

**研究者：** 为什么有些任务很久没有更新？

**执行人员：** 有时候工作一直在推进，但没什么阶段性结果，我不知道该写什么。还有就是同样的进展已经给部门汇总人说过，再填一次觉得重复。

**研究者：** 什么情况下你会主动报告问题？

**执行人员：** 如果需要其他部门配合，或者时间肯定来不及，我会跟负责人说。但这个不一定会写进 Excel，通常先在群里或者电话说。

**研究者：** 如果让你设计系统，你希望有什么？

**执行人员：** 最好别让我填很多东西，能把我真正要做的任务列清楚就行。

## Analysis

### Pain Candidate P-002

```text
Who: 执行人员
Pain: 同一进展可能需要通过部门汇总和督办询问重复反馈
Evidence: INT-002 / E2
Need validation: Cross-interview + observation
```

### Pain Candidate P-003

```text
Who: 执行人员
Situation: 工作持续推进但没有明显阶段成果
Pain: 不清楚什么内容值得作为“进度更新”
Potential consequence: 系统/Excel状态可能长时间不更新，但真实工作仍在推进
Evidence: INT-002 / E2
```

### Job Candidate J-002

```text
清楚知道自己负责什么、什么时候需要反馈，
并用尽可能低的重复成本让相关人员知道真实进展和阻塞。
```

### Important contradiction candidate

INT-001 将“长时间未更新”视为风险信号；INT-002 表明“未更新”并不必然代表“未推进”。

因此未来不能简单定义：

```text
未更新 = 任务异常
```

需要在 Requirements 阶段进一步定义风险语义。

### Unknowns

- 部门汇总角色是否普遍存在？
- 重复填报频率多高？
- 是否所有进展都必须结构化记录？
- 跨部门阻塞当前如何升级？
