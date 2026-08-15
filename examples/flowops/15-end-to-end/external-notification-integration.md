# FlowOps End-to-End Case — External Notification Integration

这个案例演示企业项目常见的“功能不难，集成很难”。

## Request

> 临期和超期事项希望通过企业现有消息平台提醒责任人。

## Discovery Questions

- provider 是否有正式 API？
- 用户身份如何映射？
- provider 是否支持模板消息？
- rate limit？
- 是否异步？
- 成功响应代表“已接收”还是“已送达”？
- 重复请求会不会重复通知？
- provider outage 如何处理？

没有文档 Evidence 的行为不允许 Agent 猜测。

## Requirement Boundary

本 Feature 负责：

```text
approved reminder event
→ resolve recipients
→ create notification delivery request
→ provider adapter
→ delivery status/evidence
```

不负责重新定义 Attention rule。

## Architecture

```text
Attention / Reminder domain event
        ↓
Notification Application
        ↓
Notification Port
        ↓
Provider Adapter
        ↓
External Platform
```

Provider DTO 不进入 Domain。

## Reliability Contract

必须定义：
- timeout；
- retryable errors；
- max attempts/backoff；
- idempotency key；
- duplicate handling；
- dead-letter/manual replay；
- provider correlation id。

## Security

Credential：secret manager/environment injection，不进入 repository、test fixture 或 Prompt。

Callback（若存在）：signature/auth、replay、duplicate、fast ack、async processing。

## Testing

### Unit
Provider error → internal error mapping。

### Contract
Request schema/header/signature。

### Integration
Provider sandbox/staging 成功和已知错误。

### Failure
Timeout、429、5xx、duplicate、invalid recipient。

Mock 成功不等于 Integration 完成。

## Operations

Runbook 应回答：
- 某条通知是否生成？
- 是否进入发送队列？
- provider 是否接收？
- retry 到第几次？
- 是否可以安全 replay？
- provider outage 时业务是否仍可在系统内查看 Attention？

## AI Review Traps

- 无限 timeout；
- 对所有异常无脑 retry；
- hard-coded token；
- provider response 直接返回前端；
- 同步调用阻塞主业务 transaction；
- 没有 idempotency；
- 日志输出完整消息/凭证；
- Agent 声称“接口调用成功就一定送达”。

## Trace

```text
Business Requirement
→ Integration Contract
→ Architecture Port
→ Adapter
→ Reliability/Security Rules
→ Tests
→ Runbook/Observability
```
