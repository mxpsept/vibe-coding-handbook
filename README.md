# Vibe Coding 实战：AI Native 企业级软件开发实践手册

> 从模糊业务想法到可验证、可部署、可持续演进的软件系统。

`vibe-coding-handbook` 面向已经或准备使用 Codex、Claude Code、Cursor、Gemini CLI 等 Coding Agent 的工程师与企业团队。重点不是“写更长的 Prompt”，而是建立一套让 AI **在明确业务事实、设计规范、架构边界和验证证据下工作**的软件工程方法。

## Start Here

第一次进入仓库，请先阅读 **[START-HERE.md](START-HERE.md)**。

你可以按真实问题进入，而不是强制顺序阅读：

| 场景 | 推荐入口 |
| --- | --- |
| 从零开发新系统 | `START-HERE.md` → Greenfield 路线 |
| 修改已有系统 | `handbook/13-brownfield/` |
| 排查 Bug | `handbook/14-debugging/` |
| 使用 Codex 开发 | `handbook/15-agent-governance/` + `templates/agent/` |
| 重构 / 升级 | `handbook/16-refactoring/` + `handbook/17-migration/` |
| 多 Agent 协作 | `handbook/18-multi-agent/` |
| AI Code Review | `handbook/19-code-review/` |
| 生产上线 | `handbook/21-security/` → `24-observability/` |
| 企业推广 | `handbook/27-metrics/` → `29-maturity/` |
| 查找模板/术语/完整流程 | `handbook/30-reference/` |

## 为什么需要这本手册

最危险的 Vibe Coding 流程是：

```text
Idea → Prompt → Code → “看起来能用”
```

本手册推荐：

```text
Intent
↓
Discovery / Evidence
↓
Requirements & Business Rules
↓
Product / UI Design
↓
Architecture & Contracts
↓
Bounded Agent Task
↓
Implementation
↓
Verification Evidence
↓
Independent Review
↓
Production Readiness
↓
Release / Observability
↓
Feedback → Next Specification
```

## 核心原则

1. **Human defines intent** — 人负责目标、价值判断、关键决策和最终责任。
2. **Artifacts define truth** — 重要业务、设计和架构事实不能只存在聊天记录。
3. **AI executes within constraints** — Agent 必须知道 Scope、Non-goals、Stop Conditions 和权限。
4. **Verification closes the loop** — “AI 说完成了”不是 Definition of Done。
5. **Production evidence feeds the next decision** — 软件上线不是工程闭环的终点。

## 贯穿案例：FlowOps

全书使用完全虚构的 **FlowOps — 企业任务督办与协同管理平台**。

它从一句模糊需求开始：

> 建设一套重点任务督办系统，统一管理重点工作，明确责任、跟踪进度、识别临期超期，并帮助管理者掌握整体执行情况。

FlowOps 会经历 Discovery、Requirement、业务建模、UI/UX、Architecture、Coding Agent、Testing、Brownfield Change、Release 与 Production Feedback。案例不使用任何真实企业名称、人员、数据、内部截图或专有业务资料。

## 仓库结构

```text
vibe-coding-handbook/
├── START-HERE.md       # 场景化入口
├── handbook/           # 方法论与完整教程
├── templates/          # 可复制工程 Artifact
├── prompts/            # 分阶段 AI Prompt
├── checklists/         # Quality / Release Gate
├── examples/           # FlowOps 等案例产物
├── resources/          # 学习路线和外部资源
└── assets/             # 图与示意资产
```

| 内容 | 回答的问题 |
| --- | --- |
| Handbook | 为什么以及应该怎样开发？ |
| Templates | 关键 Artifact 应该怎样写？ |
| Prompts | 怎样让 AI 协助产生/检查 Artifact？ |
| Checklists | 怎样判断真的完成？ |
| Examples | 企业案例怎样贯穿落地？ |

## Reference Center

当仓库内容越来越多时，优先使用：

- `handbook/30-reference/01-artifact-map.md` — 每种 Artifact 的职责与 Owner；
- `02-role-learning-paths.md` — Developer / Architect / Product / Design / QA / SRE / Manager 阅读路线；
- `03-glossary.md` — 全书术语；
- `04-project-playbook.md` — 从 Gate 0 到 Gate 10 的完整项目路线；
- `05-prompt-template-index.md` — Prompt / Template / Checklist 快速索引。

## Vibe Coding 成熟度

本手册使用 L0–L5 模型：

```text
L0 Ad-hoc Chat Coding
→ L1 Assisted Developer
→ L2 Artifact-driven Delivery
→ L3 Governed Agent Engineering
→ L4 Production Feedback Loop
→ L5 Adaptive AI Engineering System
```

详见 `handbook/29-maturity/01-vibe-coding-maturity-model.md`。

成熟度不由“用了哪个模型”决定，而由业务事实是否可追踪、Agent 是否受控、完成是否有 Evidence、生产反馈是否回流决定。

## 推荐第一次实践

不要直接拿一个完整大型系统试验。选择一个真实、有限的 Vertical Slice，用 1–2 周完整走一遍：

```text
Requirement
→ Page Spec
→ API / Domain
→ Implementation Packet
→ Codex
→ Tests
→ Review
→ Release
```

实践完成后，再把有效流程逐步固化为 Repository Instructions、Template、Checklist 和自动化 Gate。

## Handbook Status

当前已覆盖从需求发现到生产治理的完整主干，包括 Greenfield、Brownfield、Debugging、Refactoring、Migration、Multi-Agent、Security、Performance、Incident Response、Observability、Data、Integration、Metrics、Governance 与 Maturity。

项目仍会持续通过案例、交叉引用、模板和外部学习资源进行 Hardening，而不是无限增加概念章节。

---

> **Human defines intent. Artifacts define truth. AI executes within constraints. Verification closes the loop.**
