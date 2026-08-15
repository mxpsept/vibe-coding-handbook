# FlowOps End-to-End Case — Overdue Escalation

这个案例演示一个 Feature 如何从一句业务想法一直走到 Production Evidence。

## 0. Raw Request

> 超期任务需要自动提醒相关责任人，超期严重时需要让管理人员关注。

直接交给 Coding Agent 会产生大量未定义问题：谁是相关责任人？何时算严重？提醒一次还是每天？已办结是否提醒？管理人员是谁？渠道是什么？

## 1. Discovery

访谈/现状 Evidence 发现：
- 执行人负责日常推进；
- 责任负责人需要知道自己负责事项的超期；
- 督办人员每天人工筛选严重超期事项；
- 高频无差别提醒会被忽略。

Unknown：通知渠道和“严重超期”阈值仍未批准。

## 2. Requirement

```text
R1 System identifies overdue active items.
R2 Authorized responsible actors can see overdue attention.
R3 Escalation severity is derived from an approved rule.
R4 Closed/cancelled items do not continue active escalation.
```

Non-goal：本 Feature 不决定短信/微信/邮件等外部通知渠道。

## 3. Business Rules

```text
OVERDUE when now > dueAt and lifecycle is active.
ESCALATION_LEVEL is separate from lifecycle.
Closed item != overdue attention item.
```

严重等级阈值未批准时创建 `SPEC_GAP: escalation threshold`，禁止 Agent 自行使用 3/7/15 天等“常见值”。

## 4. UX

Attention Workspace：
- lifecycle label 与 attention reason 分开；
- 显示超期时长；
- 支持按责任范围筛选；
- Empty / Loading / Error / Permission 状态均有 Page Spec。

不要把整个页面做成红色；红色只表达需要行动的风险信息。

## 5. Architecture

Owner：Attention module 负责派生 attention reason；Item module 负责 lifecycle/source facts。

```text
Item facts
→ Attention Policy
→ Attention Query Model
→ API
→ Workspace
```

不允许 UI 自己通过日期重复计算一套 OVERDUE 规则。

## 6. API Contract

Candidate：

```text
GET /attention/items?reason=OVERDUE
```

Response 包含稳定业务语义：item identity、lifecycle、attention reason、dueAt、overdue duration、allowed actions。

权限由服务端数据 scope 决定。

## 7. Implementation Packet

```text
Goal: implement overdue attention vertical slice
Read First: approved rules + page spec + module boundary + API contract
Scope: attention query + workspace rendering + tests
Non-goals: notification channel, lifecycle redesign
Stop: threshold/channel required; permission model conflict; new infra required
Verify: rule tests + permission integration + UI states + build
```

## 8. Agent Implementation

Coding Agent 先 Repository Reconnaissance：寻找已有 Item repository、Clock abstraction、permission policy、query convention、table component 和 tests。

发现可复用模式后再修改，禁止创建第二套 request client / date utility / permission system。

## 9. Verification

关键测试：

```text
before due → not OVERDUE
after due + active → OVERDUE
after due + closed → no active overdue attention
wrong data scope → not visible
boundary at dueAt → follows approved comparison semantics
```

时间测试使用 controllable Clock。

## 10. Review

Reviewer 重点找：
- UI 重复计算 rule；
- frontend-only authorization；
- timezone ambiguity；
- closed item still appears；
- query N+1；
- severity threshold invented by Agent；
- attention reason 被错误写入 lifecycle status。

## 11. Production Readiness

Evidence：
- query latency baseline；
- required index/query plan；
- auth scope test；
- observability for calculation/query failures；
- rollback/deploy plan。

## 12. Production Feedback

上线后关注：
- overdue item count trend；
- false positive/negative reports；
- query latency/error；
- 用户是否实际进入 Attention Workspace 处理事项。

如果业务要求增加“每天通知一次”，回到 Requirement/Integration Design，而不是让 Agent 在现有代码里随手加 scheduler。

## Traceability

```text
Raw Request
→ Discovery Evidence
→ Requirement
→ Business Rule / SPEC_GAP
→ Page Spec
→ Architecture
→ API Contract
→ Implementation Packet
→ Code
→ Tests
→ Review
→ Production Evidence
→ Next Requirement
```

这条链路就是本手册希望建立的企业 Vibe Coding 最小闭环。
