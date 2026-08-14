# Gate 0 — Discovery Readiness Checklist

> 目标：判断一个项目想法是否已经具备进入 Product Discovery 的最低条件，而不是判断它是否已经可以进入开发。

## Problem

- [ ] 能用 3～5 句话描述业务问题。
- [ ] Problem Statement 没有退化成功能清单。
- [ ] 至少能够识别主要受影响人群。
- [ ] 有初步证据或合理理由相信问题真实存在。

## Context

- [ ] Known Facts 已单独记录。
- [ ] Assumptions 已单独记录。
- [ ] Unknowns 已单独记录。
- [ ] 没有让 AI 自行补齐核心业务规则。
- [ ] AI 建议没有未经确认直接升级为 Project Truth。

## Value

- [ ] 能说明为什么这个问题值得继续调查。
- [ ] 已定义至少一个初步 Expected Outcome。
- [ ] Expected Outcome 不是单纯“上线系统”或“完成数字化”。

## Scope Control

- [ ] 候选功能没有被误认为最终范围。
- [ ] 尚未因为 AI 能够 Coding 就提前进入 Build。
- [ ] 尚未过早冻结 UI 方案。
- [ ] 尚未过早冻结数据库模型。
- [ ] 尚未过早冻结 Architecture。
- [ ] 已知技术约束与技术方案选择被明确区分。

## Discovery Readiness

- [ ] 已形成需要进一步确认的 Discovery Questions。
- [ ] 知道下一阶段至少应该接触哪些 Stakeholder。
- [ ] 能指出当前最重要的 3～5 个 Unknown。
- [ ] `project-idea.md` 已由 Human Review。

## Gate Decision

选择一个结果：

- [ ] **PASS — Enter Discovery**
- [ ] **HOLD — Need more information**
- [ ] **STOP / PARK — 暂不继续投入**

### Blocking unknowns

- 

### Decision rationale

- 

### Human approval

- Decision owner:
- Review date:
- Result:
- Notes:

---

## Gate 原则

AI 可以帮助检查 Checklist、发现遗漏并提出风险，但最终 Gate Decision 属于 Human。

当 Checklist 无法通过时，优先执行：

```text
Collect Evidence
      ↓
Update project-idea.md
      ↓
Review
      ↓
Run Gate 0 Again
```

不要执行：

```text
Information Missing
      ↓
Let AI Guess
      ↓
Start Coding
```
