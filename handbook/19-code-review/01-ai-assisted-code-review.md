# 01 — AI-assisted Code Review

AI Review 最有价值的地方是扩大检查面，但不能把 Review 变成“总结这个 PR”。

## Review Inputs

Reviewer 至少读取：

```text
PR goal
Acceptance Criteria
relevant Business Rules
ADR / architecture constraints
diff
new/changed tests
```

## Review Order

### P0 Correctness / Security
- data loss；
- authorization bypass；
- wrong state transition；
- concurrency/transaction defect；
- secret exposure；
- injection/input trust。

### P1 Business / Contract
- AC 未满足；
- API semantics 漂移；
- lifecycle/permission 错误；
- backward compatibility break。

### P2 Architecture / Maintainability
- boundary violation；
- duplicate abstraction；
- new dependency without justification；
- unrelated refactor。

### P3 UX / Quality
- missing state；
- accessibility；
- error recovery；
- weak tests。

### P4 Style
仅在影响一致性/可维护性时重点指出。

## Finding Format

每个 Finding：

```text
Severity
Location
Observed code/behavior
Why it is a problem
Evidence / violated contract
Concrete fix direction
```

不要输出几十条没有影响的偏好建议淹没真正 Bug。

## Reviewer Rules

- 不把“不同写法”自动当缺陷；
- 不要求无关重构；
- 不根据函数名猜行为，检查实际路径；
- 对不确定 Finding 明确置信度/需要的 Evidence；
- 优先发现可复现、可行动的问题。

## Review Prompt

```text
Act as a skeptical senior reviewer.
Review the diff against the supplied Source of Truth.
Prioritize correctness, security, business semantics and regressions over style.
Return only actionable findings, ordered by severity.
For each finding include location, impact, evidence and fix direction.
If no material findings exist, say so and list verification gaps separately.
```

## Review Is Not Testing

AI Review 不能替代运行：

```text
build
lint
tests
security checks
integration/e2e where needed
```

静态推理与运行 Evidence 是互补关系。
