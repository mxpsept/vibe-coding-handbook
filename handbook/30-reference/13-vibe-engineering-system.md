# Vibe Coding Engineering System

本章定义 `vibe-coding-handbook` 与 `vibe-workspace-kit` 的长期产品边界。目标不是制造更多 AI 工具，而是把方法、工程事实、执行环境和 Coding Agent 连接成一个可治理的软件工程系统。

## 1. Problem

Coding Agent 已经能够快速生成代码，但企业开发的主要风险逐渐从“代码写不出来”迁移到：

- Agent 不知道哪些信息是事实，哪些只是推断；
- PRD、设计、架构、代码和测试之间断裂；
- 多仓库上下文和提交边界混乱；
- 不同 Agent 各自维护一套 instructions，逐渐漂移；
- “代码生成完成”被错误等同于“Feature 完成”；
- 团队缺少机器可检查的 Engineering Contract。

因此下一阶段的核心不是更长的 Prompt，而是：

```text
Methodology
    ↓
Artifact Contract
    ↓
Workspace Runtime
    ↓
Agent Context
    ↓
Implementation
    ↓
Verification Evidence
```

## 2. Two Products, One System

### vibe-coding-handbook

定位：**AI Native Software Engineering Methodology**。

负责定义：
- Why / What / When；
- lifecycle；
- Artifact semantics；
- templates；
- playbooks；
- case studies；
- governance；
- quality expectations。

Handbook 告诉团队“应该怎样工作”。

### vibe-workspace-kit

定位：**AI Native Software Engineering Workspace Runtime**。

负责执行：
- workspace bootstrap；
- polyrepo coordination；
- repository safety；
- canonical project context；
- feature workspace；
- agent adapters；
- verification state；
- engineering gates。

Kit 让方法能够被执行和检查。

## 3. Layered Architecture

```text
┌──────────────────────────────────┐
│ Methodology                      │
│ vibe-coding-handbook             │
├──────────────────────────────────┤
│ Artifact Contract                │
│ product / design / architecture  │
│ feature / verification           │
├──────────────────────────────────┤
│ Workspace Runtime                │
│ vibe-workspace-kit               │
├──────────────────────────────────┤
│ Agent Adapters                   │
│ Codex / Claude / Cursor / ...    │
├──────────────────────────────────┤
│ Business Repositories            │
│ frontend / backend / contracts   │
└──────────────────────────────────┘
```

依赖方向必须向下。Handbook 不应成为 CLI 的 npm/runtime dependency。

## 4. One Fact, One Owner

系统最重要的设计原则：**Canonical Project Truth 只有一份。**

例如业务规则属于 Product/Feature Artifact；架构边界属于 Architecture Artifact；仓库命令属于 Workspace Config。`AGENTS.md`、`CLAUDE.md`、Cursor/Copilot rules 只是这些事实面向不同 Agent 的 Adapter，不成为新的事实源。

## 5. Capability Model

```text
Workspace
  init / clone / doctor / status

Project
  bootstrap / context

Feature
  feature create / start / status / close

Development
  branch / snapshot / run

Verification
  lint / test / build / review / check

Delivery
  commit / push
```

现有 0.1.x Workspace/Git Safety 能力应保持兼容。v0.2 的目标是向上增加 Project、Feature、Context 和 Engineering Gate，而不是重写已经稳定的 Git orchestration。

## 6. Definition of Success

当系统成熟后，一个新 Agent 进入项目，不需要依赖历史聊天，也应该能回答：

```text
What am I changing?
Why does it matter?
Which facts are approved?
Which repositories own the behavior?
What must not change?
When must I stop and ask?
How will completion be proven?
```

这才是 Vibe Coding 从个人技巧进入企业工程体系的关键。