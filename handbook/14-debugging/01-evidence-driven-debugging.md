# 01 — Evidence-driven Debugging with AI

AI Debug 最大风险不是不会提出原因，而是**太容易提出原因**。因此 Debug 流程必须让 Evidence 领先于 Fix。

## Workflow

```text
Observed
→ Reproduce
→ Scope
→ Evidence
→ Hypotheses
→ Discriminate
→ Root Cause
→ Minimal Fix
→ Regression Test
→ Verify
```

## 1. Problem Statement

必须区分：

```text
Observed behavior
Expected behavior
Environment
Frequency
First known occurrence
Recent relevant changes
```

不要只给一句“接口报错了”。

## 2. Reproduction

优先获得最小稳定复现。无法稳定复现时，明确记录概率和触发条件，不要假装确定。

## 3. Evidence Pack

根据问题收集最小必要 Evidence：
- request/response；
- logs + correlation id；
- stack trace；
- configuration；
- network trace；
- database state；
- browser console；
- failing test；
- relevant diff。

注意脱敏 secrets / PII。

## 4. Hypothesis Table

要求 Agent 输出：

| Hypothesis | Evidence For | Evidence Against | Cheapest Test |
| --- | --- | --- | --- |
| H1 | | | |
| H2 | | | |

这样避免从第一条错误信息直接跳到 Fix。

## 5. Discriminating Tests

优先执行能快速排除多个假设的检查，而不是随机修改配置。

例如 WebSocket 400：先确认 Upgrade headers、代理层、应用端握手日志，而不是先升级 Nginx。

## 6. Root Cause vs Symptom

```text
Restart fixes it
```

通常是 mitigation，不自动等于 root cause。

最终说明应包含：
- root cause；
- trigger；
- why existing safeguards missed it；
- fix；
- regression prevention。

## 7. Debug Change Rule

一次只做足以验证假设的最小改变。不要同时：升级依赖 + 改配置 + 重构代码，然后无法知道什么真正修复问题。

## 8. Regression

每个值得修复的 Bug 都应考虑最便宜的永久 Evidence：

```text
unit test
integration test
contract test
monitor/alert
runbook check
```

## Debug Prompt Skeleton

```text
Act as a debugging investigator.
Do not propose a fix before ranking hypotheses from evidence.

OBSERVED:
EXPECTED:
ENVIRONMENT:
REPRODUCTION:
EVIDENCE:
RECENT CHANGES:

Return:
1. scoped problem statement
2. ranked hypotheses
3. evidence for/against
4. minimal discriminating checks
5. only after evidence: root-cause fix
6. regression test/monitor
7. remaining uncertainty
```
