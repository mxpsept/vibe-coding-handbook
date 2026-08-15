# 01 — Enterprise AI Engineering Governance

治理的目标不是禁止 AI，而是让团队知道：什么可以自主做、什么需要 Evidence、什么需要审批。

## 1. Governance Layers

```text
Organization Policy
→ Project Policy
→ Repository Instructions
→ Task Autonomy
→ Automated Gates
→ Human Accountability
```

## 2. Organization Policy

至少明确：
- approved AI services/models；
- source code/data classification；
- secrets/PII rules；
- third-party licensing/IP policy；
- allowed integrations/tools；
- production access policy；
- audit/retention requirements。

## 3. Risk-based Controls

不要所有任务一个审批强度。

### Low
文档、测试草稿、局部低风险实现。

### Medium
普通业务 Feature、内部 API、依赖升级。

### High
权限、敏感数据、支付/资金、安全控制、不可逆数据迁移、生产基础设施。

风险越高，要求更多独立 Review、Evidence 和权限隔离。

## 4. Tool Permission

区分：

```text
Read repository
Write working tree
Commit
Push
Open PR
Merge
Deploy staging
Deploy production
Modify production data/infrastructure
```

不要把“允许 Codex 写代码”理解成以上权限全部开放。

## 5. Model Output Accountability

AI 是 contributor/tool，不是责任主体。合并者/发布者仍需对：
- correctness；
- security；
- compliance；
- operational risk
负责。

## 6. Evidence Retention

高风险变更保留适当 Evidence：
- approved spec/ADR；
- PR/review；
- automated test/security results；
- migration/release record；
- incident/change record。

不需要保存每一句聊天才能治理。

## 7. Governance Smells

### Ban everything
团队转向不可见 Shadow AI。

### Allow everything
速度快但风险不可解释。

### Prompt approval bureaucracy
审批 Prompt 文案，却不检查实际权限、数据和代码 Evidence。

更好的方向是 policy-as-code + risk-based gate + clear accountability。
