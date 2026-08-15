# 01 — AI 时代的 Technical Debt Management

AI 提高代码生成速度后，技术债不会消失；如果没有治理，它可能更快累积。

## Debt Is a Trade-off, Not an Insult

记录技术债时说明：

```text
Current compromise
Reason it was accepted
Cost / risk
Trigger to repay
Possible direction
```

不要只写“代码很烂，需要重构”。

## Debt Categories

- Architecture debt；
- Test debt；
- Dependency debt；
- Data/schema debt；
- UX consistency debt；
- Security debt；
- Operational debt；
- Documentation/context debt。

## Debt Register

| ID | Area | Evidence | Impact | Trigger | Priority | Owner |
| --- | --- | --- | --- | --- | --- | --- |

## AI-generated Debt Signals

特别关注：
- 第二套 request/state/error abstraction；
- `common/utils` 快速增长；
- duplicate domain rules；
- TODO without owner/trigger；
- tests only happy path；
- dependency added for tiny utility；
- generated docs no longer match code。

## Repayment Rule

不要固定“每 Sprint 20% 重构”作为唯一方法。优先结合 Trigger：

```text
change frequency × pain × risk
```

如果某债务长期不影响变化或风险，可能不是当前最值得处理的事情。

## Boy Scout Rule with AI

小范围清理可以做，但必须满足：
- 与当前代码直接相关；
- 行为可验证；
- 不扩大 review surface；
- 不改变 architecture contract。

否则创建独立 Debt Item。

## Context Debt

Vibe Coding 特有的重要债务：代码正确，但 Agent 无法理解为什么。

例如：
- hidden business rule；
- stale ADR；
- undocumented generated file；
- build command 只存在某人 shell history。

偿还 Context Debt 往往能直接提高后续 AI 开发质量。
