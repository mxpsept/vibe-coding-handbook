# FlowOps — Non-functional Requirements v0.1

> 原则：不使用没有 Evidence 的“专业数字”。不知道的指标明确标记 TBD，并定义验证方式。

## 1. Security

### NFR-SEC-001 — Authentication
系统业务能力必须仅向已认证用户开放，除明确公开资源外。

### NFR-SEC-002 — Authorization
每次读取和写入必须同时满足功能权限与数据范围权限。前端隐藏按钮不能作为权限控制。

### NFR-SEC-003 — Least Privilege
角色默认只获得完成职责所需权限。高风险操作如 Closure、Cancellation、Accountability Change 必须独立授权。

### NFR-SEC-004 — Server-side Enforcement
所有 Business Rule 与 Authorization 必须在可信服务端强制执行，不能只依赖 UI 校验。

## 2. Auditability

### NFR-AUD-001
关键生命周期与责任变更必须记录 Actor、Timestamp、Action、关键 Before/After Value。

### NFR-AUD-002
普通业务用户不得直接修改历史 Audit Record。

### NFR-AUD-003
Progress History 与 Audit History 语义分离：前者是业务过程记录，后者是系统行为追踪。

## 3. Data Integrity

### NFR-DATA-001
生命周期转换必须满足 state-model.md 定义，不允许通过普通 CRUD 更新绕过 Transition Rule。

### NFR-DATA-002
Progress Update 采用 append-only 业务语义；纠错机制在规则批准前不得静默覆盖历史。

### NFR-DATA-003
Attention Flag 的计算不得改变 Lifecycle State，除非未来有明确 Business Rule。

## 4. Performance

### NFR-PERF-001 — Interactive Query
典型列表与详情查询需要满足企业 Web 交互可接受体验。

**Numeric target:** TBD。

在 Architecture / Test Planning 前必须根据以下数据确定：
- expected item count；
- active item count；
- concurrent users；
- query filters；
- reporting period；
- infrastructure constraints。

禁止 Agent 自行填入 `200ms`、`1000 QPS` 等目标。

### NFR-PERF-002 — Attention Evaluation
Near-due / Overdue / Stale evaluation 应在业务可接受时间内反映规则变化。

Evaluation freshness target: TBD。

## 5. Availability & Reliability

### NFR-REL-001
系统不得因为通知渠道故障而丢失核心督办业务数据。

### NFR-REL-002
如果未来引入异步通知，通知失败与业务事务成功必须具有明确语义，禁止因为微信/邮件发送失败导致已提交 Progress 回滚，除非 Business Rule 明确要求。

### NFR-REL-003
Availability SLA: TBD，根据部署环境和企业运维要求确定。

## 6. Observability

### NFR-OBS-001
关键业务操作失败应产生可定位日志，并携带可关联 Request/Trace Identifier。

### NFR-OBS-002
不得在日志中输出密码、Token、Secret 等敏感凭据。

### NFR-OBS-003
Attention Evaluation、scheduled jobs、notification jobs 等后台任务如果存在，应具备成功/失败可观测性。

## 7. Usability

### NFR-UX-001
高频角色的核心任务应优先减少跨页面跳转与重复输入。

### NFR-UX-002
Lifecycle State、Attention Flag、Progress 等不同业务维度在 UI 中必须具有可区分表达，不能全部压缩成一个颜色标签。

具体视觉表达由 Product Design 定义。

## 8. Accessibility / Responsive

企业 Web MVP 应支持主流桌面浏览器。移动 Web / App 支持范围：TBD。

如果 Product Scope 后续确认移动端，则重新定义 Responsive Acceptance。

## 9. Backup / Recovery

RPO / RTO：TBD，需要结合部署环境、数据库方案和企业运维要求在 Architecture 阶段确认。

禁止为了文档完整度虚构 RPO/RTO。

## 10. NFR Gap Register

| Gap | Validation Method | Owner |
| --- | --- | --- |
| Performance target | workload + prototype/load test | Architect/Product |
| Concurrent users | usage analysis | Product/Business |
| Availability SLA | operations requirement | Ops/Business |
| RPO/RTO | infrastructure & business impact analysis | Ops/Architect |
| Browser/mobile support | user environment analysis | Product |
| Attention freshness | business workshop | Business/Product |

## Teaching Point

好的 NFR 文档不是数字越多越专业，而是：

```text
Known constraint → explicit requirement
Unknown target → explicit TBD + validation plan
Unsupported precision → reject
```
