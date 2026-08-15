# 01 — Vibe Coding Maturity Model

成熟度不是“用了哪个模型”，而是团队能否持续把 AI 能力转化成可信交付。

## Level 0 — Ad-hoc Chat Coding

```text
Idea → Chat → Code
```

特征：依赖个人 Prompt；Context 在聊天；验证随意。

## Level 1 — Assisted Developer

有 Coding Agent、基本测试和人工 Review，但需求/设计/架构仍大量隐式存在。

目标：建立 Repository Instructions 与 Task Packet。

## Level 2 — Artifact-driven Delivery

```text
Requirement
→ Design/Architecture Artifact
→ Implementation Packet
→ Agent
→ Verification
```

关键业务事实版本化。

## Level 3 — Governed Agent Engineering

具备：
- bounded autonomy；
- stop conditions；
- architecture/security gates；
- independent AI/human review；
- brownfield/refactor/migration discipline。

## Level 4 — Production Feedback Loop

生产 Evidence 能回流：

```text
Observability / Incident / User Feedback
→ Requirement / Debt / ADR
→ Change
```

团队衡量 outcome，而不是 AI LOC。

## Level 5 — Adaptive AI Engineering System

组织能够：
- 对 Agent workflow 做实验；
- policy-as-code；
- 自动生成/验证部分 Artifact；
- 根据风险动态调整 autonomy/gates；
- 多项目复用成熟模式；
- 持续校验 Context 是否漂移。

Level 5 不是“无人开发”。人类从大量机械执行转向产品判断、架构权衡、风险和责任。

## Assessment Dimensions

| Dimension | Question |
| --- | --- |
| Product Truth | 关键业务事实是否可追踪？ |
| Context | 新 Agent 能否独立接手？ |
| Architecture | 边界是否明确且可检查？ |
| Verification | 完成是否有 Evidence？ |
| Security | 是否风险分级并最小权限？ |
| Operations | 是否可观察、可恢复？ |
| Governance | autonomy/approval 是否明确？ |
| Metrics | 是否衡量 outcome 与返工？ |

## Adoption Advice

不要追求一次从 L0 到 L5。优先解决当前最痛的约束。例如 UI 漂移严重，先强化 Design System/Page Spec；Bug 多，先强化 Acceptance/Test/Review；Agent 经常乱改架构，先强化 Repository Instructions/ADR/Stop Conditions。
