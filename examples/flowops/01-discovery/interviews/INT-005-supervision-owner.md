# INT-005 — 督办负责人访谈

> **Synthetic Teaching Case**：以下内容完全虚构，仅用于演示 Discovery 方法。

## Metadata
- Source ID: INT-005
- Stakeholder: 督办负责人 / Process Owner Candidate
- Evidence base level: E2

## Interview Excerpt

**研究者：** 什么样的事项会进入重点督办？

**督办负责人：** 不是所有工作都进来，主要是重要会议安排、领导明确交办、跨部门重点工作这几类。但实际还有临时专项，分类现在并不完全统一。

**研究者：** 谁可以认定一项工作进入督办？

**督办负责人：** 一般由办公室整理后确认，重大事项会根据领导要求调整。这个流程更多靠工作习惯，没有一份特别细的规则。

**研究者：** 临期和超期怎么判断？

**督办负责人：** 超期比较明确，超过要求完成时间还没完成就是超期。临期没有统一天数，不同事情周期差别很大。

**研究者：** 完成以后呢？

**督办负责人：** 部门说完成不一定就结束。有的需要确认成果，有的会议安排只要反馈结果就可以。我们现在表里写“完成”，但实际含义确实不完全一样。

## Analysis

### Strong Finding Candidate
当前“重点督办范围”“临期”“完成”均存在业务语义，但规则标准化程度不同。

### Business Rule Candidates
- BR-C005：重点督办候选来源包括重要会议安排、领导交办、跨部门重点工作、临时专项。
- BR-C006：超期与要求完成时间相关。
- BR-C007：临期不适合在 Discovery 阶段直接假定为固定 N 天。
- BR-C008：“部门反馈完成”可能不等于“流程正式结束”。

### Important Modeling Warning
后续 Requirements 不应直接建立：

```text
progress = 100% → status = completed → process closed
```

因为 INT-005 已提示 Progress、Completion Claim、Acceptance/Closure 可能是不同概念。

### Unknowns
- 不同来源是否需要不同流程？
- 谁拥有正式下达权？
- 哪些事项需要成果确认？
- 是否存在“申请办结 / 审核办结”？
- 超期后是否自动升级或仅作为状态？
