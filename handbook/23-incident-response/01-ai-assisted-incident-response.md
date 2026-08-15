# 01 — AI-assisted Incident Response：恢复优先，分析其次，变更受控

生产事故中 AI 可以帮助聚合 Evidence、形成假设、查询 Runbook、生成检查命令，但事故现场不适合让 Agent 无限自主试错。

## 1. Priority

```text
Protect people/data
→ contain impact
→ restore service
→ preserve evidence
→ root cause
→ prevention
```

## 2. Incident Context Pack

```text
Incident ID
Start time
Impact
Affected services/users
Recent changes
Dashboards/alerts
Logs/traces
Known mitigations
Owners
Communication channel
```

AI 生成的推断必须与观测事实分开。

## 3. Roles

典型职责：
- Incident Commander；
- Operations/technical responders；
- Communications；
- Scribe/timeline。

AI 可以辅助 Scribe 和 Evidence synthesis，但不替代 Incident Commander 的风险决策。

## 4. Change Discipline

事故中每个生产变更记录：

```text
what
why
owner
expected effect
rollback
observed result
```

避免多个 Agent/工程师同时修改同一系统而没有协调。

## 5. AI Guardrails

默认不允许 Agent 自主：
- 删除生产数据；
- rotate/revoke credentials without approval；
- 执行不可逆 migration；
- 大范围 restart/scale-down；
- 修改 firewall/IAM；
- 关闭安全控制以“先恢复”。

## 6. Hypothesis Board

| Hypothesis | Evidence | Test | Result | Status |
| --- | --- | --- | --- | --- |

持续更新，防止团队重复排查或把猜测当事实。

## 7. After Restore

不要立即把临时 mitigation 当永久 Fix。创建：
- Root Cause Analysis；
- corrective actions；
- test/monitor improvement；
- runbook update；
- architecture/product follow-up。

## 8. Postmortem Principle

目标是改进系统，不是寻找“谁写了这段 AI 代码”。真正要回答：为什么现有 Requirement、Review、Test、Release、Observability 没有阻止或快速发现它？
