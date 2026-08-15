# 01 — Observability：让 AI 交付的软件在生产中可解释

可观测性不是“多打日志”。目标是从外部 Evidence 推断系统内部发生了什么，并把生产反馈重新连接到研发 Artifact。

## 1. Three Questions

关键能力至少能回答：

```text
Is it working?
Who/what is affected?
Why is it failing or slow?
```

## 2. Signals

### Metrics
适合趋势、SLO、容量和告警。

### Logs
适合离散事件与上下文。使用结构化字段，避免把所有信息塞进 message。

### Traces
适合跨服务/组件请求路径和延迟分解。

三者通过 request/correlation/trace identity 关联。

## 3. Business Observability

技术健康不等于业务正确。

FlowOps candidate：
- completion claim submitted；
- closure rejected by rule；
- attention calculation failures；
- stale item count trend；
- privileged action audit events。

注意业务指标不应泄露不必要的敏感数据。

## 4. Instrument from Failure Modes

不要先问“我们要记录哪些日志”，先问：

```text
这个 Feature 最可能怎样失败？
发生后我们需要什么 Evidence 才能定位？
```

把 observability requirement 写进 Architecture / Implementation Packet。

## 5. Alert Quality

好的 Alert：
- actionable；
- owner known；
- user/business impact related；
- has runbook/context；
- threshold backed by baseline/SLO。

避免“CPU > 80% 就报警”式无上下文规则。

## 6. AI-assisted Operations

AI 可以：
- 聚合 logs/metrics/traces；
- 生成 incident timeline；
- 对照 deployment/change；
- 排序 hypotheses；
- 推荐 runbook。

但必须区分：

```text
Observed Fact
Inferred Hypothesis
Recommended Action
```

## 7. Telemetry Cost

Telemetry 也有成本。控制：
- cardinality；
- retention；
- sampling；
- sensitive fields；
- duplicate events。

## 8. Feedback Loop

```text
Production Evidence
→ Problem / Opportunity
→ Requirement / Debt / ADR
→ Change
→ New Evidence
```

真正成熟的 Vibe Coding 不是只让 AI 看源码，而是让它在受控条件下理解生产 Evidence。
