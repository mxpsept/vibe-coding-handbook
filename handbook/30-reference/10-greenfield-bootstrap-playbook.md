# Greenfield Bootstrap Playbook

当你只有一个系统想法，尤其是“我知道业务，但不知道 UI 怎么设计，也不知道该先让 Codex 做什么”时，从这里开始。

## Day 0 — 不写代码

写 Raw Idea，收集已有表格、流程、角色、痛点、现有系统和接口。让 AI 帮你提出问题，而不是直接生成数据库和页面。

Output：Product Brief + Fact/Assumption/Unknown。

## Day 1 — 找 Critical Workflow

不要列 80 个菜单。画出 1–3 条核心业务流。

```text
Actor
→ Trigger
→ Business Action
→ State/Result
→ Next Actor
```

Output：Workflow、Glossary、Business Rule candidates。

## Day 2 — 先做信息架构，再做“漂亮 UI”

研究 3–5 个成熟同类产品/设计系统，提取 Pattern：navigation、list/detail、filter、status、action、feedback。

让 AI 生成 2–3 个 Wireframe alternatives，解释 trade-off。选方向后建立 Design Context/Page Spec。

> UI 美观度问题通常不应在 Coding 阶段用“再优化一下”解决，而应提前形成视觉方向、层级、组件和状态约束。

## Day 3 — Architecture Skeleton

根据真实 Drivers 决定模块 Owner、dependency、API/data/security/integration strategy。不要因为技术流行就引入微服务、MQ、搜索引擎。

Output：Architecture Context + 必要 ADR。

## Day 4 — 选第一 Vertical Slice

好的第一 Slice：有真实价值、端到端、规则有限、能独立验证。

坏的第一 Slice：完整权限平台、整个 Dashboard、所有基础字典、一次做完全部 CRUD。

Output：Feature Spec + Implementation Packet。

## Day 5+ — Codex Execution Loop

```text
Reconnaissance
→ Plan
→ Implement
→ Verify
→ Independent Review
→ Fix
→ Evidence
```

OpenAI 当前官方 Codex 用例也明确覆盖理解大型代码库、从 idea 到 proof of concept、重构、迁移、质量验证等不同任务形态；因此工程流程应根据任务类型给 Agent 不同边界，而不是只使用一个万能 Prompt。

## UI Feedback Loop

实现页面后：

```text
real screenshot
→ compare with Page Spec/reference
→ identify hierarchy/spacing/component/state deviation
→ bounded visual fix
→ screenshot again
```

不要只用主观反馈：`不够高级，再优化。`

## Bootstrap Exit

当第一 Slice 已有：approved behavior、approved UI direction、architecture owner、bounded packet、executable verification 时，项目正式从探索期进入 Agent-assisted Delivery。
