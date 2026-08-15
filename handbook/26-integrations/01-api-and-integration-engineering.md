# 01 — API & Integration Engineering：把外部系统当成不可靠边界

企业软件经常不是算法复杂，而是集成复杂。第三方 API、Webhook、消息、文件交换都必须明确 Contract 与 Failure Model。

## 1. Integration Contract

记录：

```text
owner/provider
protocol/auth
request/response schema
version
rate limit
timeout
retry semantics
idempotency
error mapping
SLA/SLO if known
sandbox/test method
```

## 2. Timeout First

任何远程调用都应有明确 timeout。无限等待不是可靠性策略。

## 3. Retry

只有当操作语义允许时重试。考虑：
- transient vs permanent error；
- exponential backoff/jitter；
- max attempts；
- idempotency；
- retry storm。

`POST` 并不自动不可重试，关键是业务语义和幂等设计。

## 4. Webhook

接收端考虑：
- authentication/signature；
- replay；
- duplicate delivery；
- ordering assumptions；
- fast acknowledgement；
- asynchronous processing；
- dead letter/recovery；
- audit。

不要假设“回调只会发送一次”。

## 5. Error Translation

外部系统错误不要直接泄漏为内部 Domain Error。Adapter 负责把 provider-specific failure 转换成稳定内部语义，并保留可诊断 Evidence。

## 6. Contract Tests

适合验证：
- schema；
- required headers；
- auth/signature；
- provider error mapping；
- compatibility。

Mock 只能证明我们对 provider 的想象一致；关键集成还需要 sandbox/staging Evidence。

## 7. AI Rules

Agent 不得：
- 猜测 undocumented provider behavior；
- 在测试代码硬编码真实 secret；
- 因一次成功调用认定 retry/idempotency 无需设计；
- 把 provider DTO 扩散到 Domain；
- 在没有证据时声称某 API “永久有效”或“不会限流”。

## 8. Integration Runbook

生产支持至少知道：
- 如何确认本方请求是否发出；
- provider response/correlation id；
- queue/retry 状态；
- 如何安全 replay；
- provider outage 时降级策略。
