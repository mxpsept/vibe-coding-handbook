# FlowOps Production Example — Attention Workspace Release

## Scenario

Attention Workspace 已完成开发，准备首次生产发布。它用于集中展示 STALE_UPDATE / NEAR_DUE / OVERDUE，需要保证规则正确、权限正确，并能在规则计算异常时快速定位。

## 1. Release Evidence

上线前收集：
- approved Attention business rules；
- Page/API specs；
- architecture decision；
- test results；
- performance baseline；
- security/permission verification；
- migration/config changes；
- rollback plan。

## 2. Critical Rule Verification

至少覆盖：

```text
not due + recently updated → no attention
stale update → STALE_UPDATE
deadline approaching → NEAR_DUE
deadline passed → OVERDUE
closed item → excluded/handled per approved rule
```

时间测试使用 controllable Clock，避免依赖测试运行时真实日期。

## 3. Permission

验证：
- 普通执行人只能看到其允许范围；
- 管理视图按批准 scope 聚合；
- URL/API 直接访问不能绕过前端限制。

## 4. Performance

构造接近生产量级的数据，记录：

```text
query latency p95
DB query plan / index evidence
payload size
frontend render behavior
```

如果性能预算没有批准值，报告 GAP，不编造“必须 < 200ms”。

## 5. Observability

关键 Evidence：
- Attention query latency/error；
- rule calculation failure；
- downstream/database error；
- request correlation；
- deployment version。

不要记录不必要的敏感业务内容。

## 6. Release Sequence

```text
pre-check
→ deploy backend
→ health check
→ deploy frontend
→ technical smoke
→ business smoke
→ observe metrics/errors
→ release complete
```

如果存在 schema migration，则按兼容策略调整顺序。

## 7. Smoke Test

使用已知测试数据验证：
1. Attention list loads；
2. expected item appears with correct reason；
3. detail navigation works；
4. unauthorized scope cannot be queried；
5. lifecycle label 与 attention label 没有混淆。

## 8. Rollback Trigger

Candidate trigger：
- critical rule systematic misclassification；
- authorization/data-scope leakage；
- severe latency/error regression；
- migration/data integrity problem。

安全/数据泄露场景优先 containment，不机械等待普通 rollback 流程。

## 9. Feedback Loop

上线后一周复盘：
- false positive/negative Attention；
- user action rate；
- latency/error；
- support feedback；
- new rule evidence。

新的业务发现回到 Requirement/Business Rule，而不是直接在代码中调阈值。
