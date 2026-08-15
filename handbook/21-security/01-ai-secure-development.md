# 01 — AI Secure Development：把安全变成研发约束，而不是上线前扫描

AI 可以快速复制实现模式，也会快速复制不安全模式。安全必须进入 Source of Truth、Task Packet、Review 与 Verification。

## 1. Security Context

每个重要 Feature 至少识别：

```text
Assets
Actors
Trust boundaries
Sensitive data
Privileged actions
External inputs
Abuse cases
```

不是所有页面都需要完整 Threat Model，但权限、资金、敏感数据、上传、外部集成等功能必须提高审查等级。

## 2. Trust Rule

```text
Client input is untrusted
External system input is untrusted
AI-generated code is untrusted until verified
```

UI 隐藏、前端校验、Prompt 指令都不是安全边界。

## 3. Secure Feature Checklist

- authentication source 明确；
- authorization server-side；
- object/data scope 检查；
- input validation；
- output encoding where relevant；
- secrets 不进入代码/日志/Prompt；
- file upload type/size/storage policy；
- rate/abuse controls where exposed；
- audit evidence for privileged actions；
- dependency risk reviewed。

## 4. AI-specific Risks

### Secret leakage
不要把生产密码、Token、真实敏感数据复制给不允许接收这些数据的 AI 服务。

### Hallucinated security APIs
Agent 可能生成不存在或错误使用的安全配置。必须以当前框架/官方文档和测试验证。

### Security by convention
“项目其他地方都这么写”不能证明安全。高风险路径需要独立验证。

### Over-permissioned agents
Coding Agent 的 Git、Cloud、Production 权限应遵循最小权限；写代码不自动意味着可以部署生产。

## 5. Threat-driven Tests

对关键动作测试：

```text
unauthenticated
wrong role
wrong tenant/scope
object not owned/visible
invalid transition
malformed input
replay/duplicate where relevant
```

## 6. Security Review Gate

以下变化默认触发加强 Review：
- auth/authz；
- cryptography；
- secret handling；
- upload/download；
- external callback/webhook；
- SQL/query construction；
- deserialization；
- admin/privileged action；
- sensitive logging；
- new network exposure。

## 7. Security Finding

Finding 必须描述攻击/失败路径，而不是只写“可能不安全”。

```text
Actor
→ controllable input/action
→ missing control
→ impacted asset
→ concrete mitigation
```
