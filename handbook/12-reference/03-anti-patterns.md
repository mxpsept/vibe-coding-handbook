# Vibe Coding Anti-pattern Catalog

## AP-01 — Idea → Prompt → Code

症状：业务想法刚出现就要求 AI 开发完整功能。

后果：需求、UI、架构和代码同时被模型隐式决定。

替代：Idea → Discovery → Spec → Design → Architecture → Implementation。

## AP-02 — Chat as Source of Truth

症状：“我们上次聊天已经说过了。”

后果：新会话、新 Agent、团队成员无法稳定获得已确认事实。

替代：批准的决定进入版本化 Artifact。

## AP-03 — Screenshot-driven Development

症状：只给 UI 图要求 1:1 实现。

缺失：权限、状态、错误、长数据、响应式、业务语义。

替代：Screenshot + Page Spec + Design System + State Matrix。

## AP-04 — AI Default Dashboard

症状：四张 KPI 卡 + 两张图 + 排名 + 表格。

原因：没有明确 Primary Job。

替代：先定义用户要做的决定/动作，再选择信息结构。

## AP-05 — CRUD = Domain

症状：所有业务都变成增删改查和 `status` 字段修改。

替代：显式 Domain Actions、State Model、Business Rules。

## AP-06 — Common/Utils Black Hole

症状：遇到依赖问题就移动到 `common`。

后果：所有模块最终依赖所有东西。

替代：明确 Owner；真正技术通用能力才共享。

## AP-07 — Framework of the Week

症状：每个 Agent 都引入自己熟悉的新库。

替代：Architecture Decision + New Dependency Rule。

## AP-08 — Frontend Permission = Security

症状：隐藏按钮后认为用户没有权限。

替代：Backend Authorization Source of Truth。

## AP-09 — Compile = Done

症状：AI 回复“build successful”，任务即结束。

替代：Acceptance Criteria + tests + state verification + review。

## AP-10 — AI Reviews AI and Automatically Passes

症状：生成代码的 Agent 自己简单检查后直接合并。

替代：独立 Reviewer Context + automated gates + human ownership。

## AP-11 — Mega Prompt

症状：一个 Prompt 同时要求研究、设计、架构、开发、测试、部署。

替代：按 Artifact Stage 拆分，并把阶段输出作为下一阶段输入。

## AP-12 — Over-specification

症状：为了控制 AI，把每一行实现都提前规定。

后果：人承担了实现成本，AI 失去合理自主空间。

替代：固定 Intent/Contract/Constraints，把实现细节留给 Agent。

## AP-13 — No Stop Conditions

症状：缺信息时 AI 继续猜。

替代：明确 `SPEC_GAP / ARCH_GAP / DESIGN_SPEC_GAP` 与 Stop Conditions。

## AP-14 — Premature Microservices

症状：因为“企业级”直接引入大量分布式组件。

替代：Architecture Drivers → simplest sufficient architecture → revisit triggers。

## AP-15 — Demo-data UI

症状：页面只有 3 条短标题数据时非常漂亮。

替代：测试 empty / error / long / large / multiple-state / narrow viewport。

## AP-16 — Refactor While Feature Building

症状：实现一个按钮顺便重写请求层、目录和状态管理。

替代：Feature Scope 与 Architecture Refactor 分离；必要时单独 ADR/PR。

## AP-17 — No Production Feedback Loop

症状：上线后只继续堆需求。

替代：Observability → feedback → new evidence → next specification。

## Self-check

当 AI 提议一个“更优雅”的方案时，先问：

```text
它解决了哪个已知问题？
它改变了哪个已批准 Contract？
它增加了什么长期成本？
我们如何验证它更好？
```
