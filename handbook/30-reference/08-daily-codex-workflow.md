# Daily Codex Workflow

这是一页可以放在开发者旁边每天看的执行版流程。

## New Feature

```text
Need
→ Feature Spec
→ Human approves critical behavior/UI
→ Implementation Packet
→ Codex Reconnaissance
→ Plan
→ Human/Rule Gate if high risk
→ Implement
→ Verify
→ Independent Review
→ Fix
→ Evidence
→ Commit/PR
```

## Small Bug

```text
Symptom
→ reproduce/evidence
→ hypothesis
→ locate owner
→ minimal fix
→ regression test
→ verify
```

不要直接：`这里报错了，帮我修复。`

## Brownfield Change

先建立 Change Contract：

```text
Preserve
Change
Non-goals
Characterization
Migration sequence
```

再让 Agent 编辑。

## UI Work

Coding Agent 不应该成为临时 UI Designer。

```text
Reference research
→ UI direction
→ user flow
→ wireframe
→ design tokens/components
→ page spec
→ implementation
→ visual review
```

当 UI 不满意时，先判断是 Design Artifact 缺失，还是代码实现偏离设计，而不是无限说“再美化一点”。

## Commit Boundary

一个 Commit/PR 应尽量对应一个可解释的 Intent。前后端可以同时开发，但必须能够分别说明：
- 为什么改；
- 哪个 contract 驱动；
- 如何验证。

## When Codex Must Stop

- business rule missing/contradictory；
- permission unclear；
- destructive migration；
- secret/production credential required；
- architecture boundary conflict；
- scope suddenly expands；
- required verification cannot run and completion depends on it。

## Five Questions Before Accepting AI Output

1. 它实现的是我批准的需求，还是它脑补的需求？
2. 它复用了仓库已有模式，还是创建了第二套体系？
3. 权限/状态/时间/失败路径验证了吗？
4. Evidence 能对应到 Acceptance Criteria 吗？
5. 换一个 Reviewer，它还能站得住吗？
