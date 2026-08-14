# INT-003 — 管理者访谈

> **Synthetic Teaching Case**：以下内容完全虚构，仅用于演示 Discovery 方法。

## Metadata

- Source ID: INT-003
- Stakeholder: 管理者
- Evidence base level: E2

## Interview Excerpt

**研究者：** 在经营会上，你通常最关注重点任务的什么信息？

**管理者：** 我不需要看所有过程。我想知道哪些事情按计划，哪些可能完不成，为什么，需要我协调什么。

**研究者：** 现在这些信息怎么获得？

**管理者：** 会前办公室会整理材料。会上如果某个事项有问题，再让责任部门解释。有时候材料写“正常推进”，但一问才知道还卡着其他部门。

**研究者：** 你希望看到什么图表？

**管理者：** 图表不是最重要的。最好一眼能看到真正需要处理的问题，不要几十个指标。

**研究者：** 什么情况下需要你介入？

**管理者：** 跨部门协调、重要节点可能延误，或者责任一直不明确的时候。普通执行问题部门自己解决就行。

## Analysis

### Job Candidate J-003

```text
在有限时间内识别真正需要管理层干预的重点任务，
理解风险原因并决定是否协调资源。
```

### Pain Candidate P-004

```text
汇报材料中的“正常推进”等概括状态可能隐藏真实阻塞，
管理者需要在会上进一步询问才能发现问题。
Evidence: INT-003 / E2
```

### Design implication — NOT UI Requirement

这段访谈并不能证明“必须开发驾驶舱”。

它证明的是一个 Job：

```text
快速识别需要管理层干预的问题。
```

未来可以通过 Dashboard、风险清单、周报、会议材料甚至 AI Summary 实现。

### Business Rule Candidate BR-C001

管理层介入候选条件：

- 跨部门协调；
- 重要节点可能延误；
- 责任长期不明确。

Status: Candidate only. Need validation with process owner.
