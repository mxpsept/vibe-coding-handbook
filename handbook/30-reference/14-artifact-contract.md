# Vibe Engineering Artifact Contract v1

Artifact Contract 是 Handbook 与 Workspace Runtime 之间的稳定接口。它定义“哪些工程事实存在、由谁拥有、如何定位”，而不是要求所有团队写同样长度的文档。

## 1. Canonical Layout

```text
docs/
├── product/
│   ├── product-context.md
│   ├── glossary.md
│   └── business-rules.md
├── design/
│   └── design-context.md
├── architecture/
│   └── architecture-context.md
└── features/
    └── TASK-102/
        ├── feature-spec.md
        ├── implementation-packet.md
        └── verification.md
```

不是所有 Artifact 都必须在第一天创建。Contract 支持 maturity：`absent → draft → approved → verified`。

## 2. Ownership

| Fact | Canonical Owner |
| --- | --- |
| product goal / actors | product-context |
| business vocabulary | glossary |
| cross-feature domain rules | business-rules |
| visual/system conventions | design-context |
| module/dependency boundaries | architecture-context |
| feature behavior / AC | feature-spec |
| agent execution scope | implementation-packet |
| completion evidence | verification |
| repo paths/commands | vibe-workspace.yaml |

Agent rule files不得复制并重新定义这些事实。

## 3. Machine-readable Manifest

建议 v0.2 引入可选 manifest：

```yaml
version: 1

artifacts:
  product:
    context: docs/product/product-context.md
    glossary: docs/product/glossary.md
    businessRules: docs/product/business-rules.md
  design:
    context: docs/design/design-context.md
  architecture:
    context: docs/architecture/architecture-context.md
  features:
    root: docs/features
    spec: feature-spec.md
    implementationPacket: implementation-packet.md
    verification: verification.md
```

初期可以将其作为 `vibe-workspace.yaml` 的 `artifacts` section，避免过早增加第二份配置文件。只有 schema 生命周期明显独立后才考虑拆分。

## 4. Required Metadata

Feature Artifact 建议使用简单 Front Matter，使 CLI 能读取状态而不需要理解任意 Markdown：

```yaml
---
id: TASK-102
title: Overdue Attention Workspace
status: approved
risk: medium
repositories:
  - frontend
  - backend
---
```

不要把完整业务模型塞入 YAML。结构化 metadata 用于 routing/check；业务语义继续由可读 Markdown 表达。

## 5. SPEC_GAP Contract

未知事实必须可显式表示：

```text
SPEC_GAP: overdue comparison boundary has not been approved.
```

CLI 可以检测 `SPEC_GAP`，但不能自动替人做业务决定。

建议 gate：
- draft 阶段：允许存在；
- feature start：warning/error 取决于影响范围；
- commit/close：阻断与 Acceptance Criteria 相关的 unresolved SPEC_GAP。

## 6. Acceptance Criteria Identity

AC 必须具有稳定 ID：

```text
AC-01
AC-02
AC-03
```

Verification 使用相同 ID：

```text
AC-01 → test X → PASS
AC-02 → integration test Y → PASS
AC-03 → NOT RUN
```

这让 `vibe check` 能检查 coverage，而不需要 AI 猜测两段自然语言是否对应。

## 7. Compatibility

Contract v1 必须满足：
- Markdown-first；
- Git-friendly；
- Human-readable；
- Agent-readable；
- CLI 可做有限 deterministic validation；
- 不绑定 Codex/Claude/Cursor；
- 不要求 SaaS 或数据库。

## 8. What the Contract Does Not Do

它不定义：
- 具体业务答案；
- UI 风格；
- 技术栈；
- Agent 模型；
- 每个团队必须采用的审批流程。

Contract 的职责是建立可追踪的工程接口，而不是把软件研发变成填写表格。