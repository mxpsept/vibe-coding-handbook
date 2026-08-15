# vibe-workspace-kit v0.2 Product Design

本设计建立在 0.1.x 已有 polyrepo、snapshot、test fingerprint、review、single-repo commit/push 等能力之上。

## Product Goal

将 `vibe-workspace-kit` 从 **Polyrepo Workspace Orchestrator** 演进为 **AI Native Software Engineering Workspace Runtime**。

v0.2 不追求自动完成整个软件生命周期，而是把 Project Truth、Feature Context 和 Verification Gate 接入现有安全工作区。

## Non-goals

v0.2 不做：
- AI 聊天客户端；
- 自建模型网关；
- PRD 自动批准；
- Figma 替代品；
- GitHub/Jira 全功能项目管理；
- 自动 commit/push；
- 复杂 workflow engine。

## Capability 1 — `vibe bootstrap`

目的：初始化工程 Artifact，而不是重复 `vibe init` 的 workspace/repository 初始化。

```text
vibe init       → repositories + workspace safety
vibe bootstrap  → engineering context + artifact structure
```

示例：

```bash
vibe bootstrap
vibe bootstrap --minimal
```

建议生成：

```text
docs/product/product-context.md
docs/product/glossary.md
docs/product/business-rules.md
docs/design/design-context.md
docs/architecture/architecture-context.md
docs/features/.gitkeep
```

默认模板应简短并包含 `TODO`/`SPEC_GAP` guidance，不生成假业务内容。

## Capability 2 — `vibe feature`

### create

```bash
vibe feature create TASK-102 --title "Overdue Attention Workspace"
```

生成 Feature Workspace 和 metadata。

### start

```bash
vibe feature start TASK-102
```

执行建议流程：
1. validate feature artifacts；
2. validate repository names；
3. report unresolved critical gaps；
4. create/switch feature branch for selected repos；
5. snapshot selected repos；
6. set active feature in local `.vibe` state；
7. generate agent task context。

`start` 不应调用 AI，也不应修改业务代码。

### status

展示 artifact、repo、verification 和 snapshot 状态。

### close

只在 required gates 满足后关闭 Feature；默认不执行 Git push/merge。

## Capability 3 — `vibe context`

生成 canonical context bundle：

```bash
vibe context
vibe context TASK-102
vibe context TASK-102 --agent codex
```

Canonical bundle 来源：
- workspace config；
- product context；
- architecture/design context；
- feature spec；
- implementation packet；
- current repository/snapshot state。

Agent adapter 再把 bundle 投影为对应工具需要的 instruction/context 文件。

关键原则：Adapter 不拥有业务事实。

## Capability 4 — `vibe check`

执行 deterministic Engineering Contract checks。

第一阶段只检查可可靠判断的事实：
- configured artifact exists；
- front matter/schema valid；
- referenced repositories exist；
- feature status valid；
- unresolved SPEC_GAP markers；
- AC IDs unique；
- verification references valid AC IDs；
- required AC has evidence/result；
- snapshot/test fingerprint still valid；
- generated agent files stale or drifted。

不要在 v0.2 用 LLM 判断“PRD 是否写得好”。

## Proposed Command Surface

```text
vibe init
vibe clone
vibe doctor
vibe status

vibe bootstrap
vibe context [feature]

vibe feature create <id>
vibe feature start <id>
vibe feature status [id]
vibe feature close <id>

vibe branch
vibe snapshot
vibe review
vibe lint
vibe test
vibe build
vibe check [feature]

vibe commit
vibe push
```

## Backward Compatibility

0.1.x 用户即使不采用 Artifact Contract，也应继续正常使用原命令。

建议规则：
- 新 `artifacts` config optional；
- 没有 bootstrap 的 workspace，旧命令行为不变；
- `vibe check` 可以报告 `artifact system not initialized`，但不影响 `status/test/review`；
- 不修改现有 commit/push safety defaults。

## v0.2 Success Criteria

用一个真实 polyrepo Feature 验证：

```text
init existing workspace
→ bootstrap
→ feature create
→ approve spec
→ feature start
→ context
→ agent implementation
→ test/review
→ verification evidence
→ check
→ separate commits
```

整个过程无需依赖历史聊天才能被另一位开发者或 Agent 接手。