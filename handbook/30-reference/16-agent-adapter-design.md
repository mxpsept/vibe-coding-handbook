# Canonical Context & Agent Adapter Design

多 Agent 支持最容易产生的问题不是“少支持一个工具”，而是同一个项目事实在多个规则文件中发生漂移。

## Anti-pattern

```text
AGENTS.md          says rule A
CLAUDE.md          says rule A'
.cursor/rules      says rule B
copilot file       still says old A
```

长期结果是不同 Agent 在同一仓库执行不同工程规则。

## Canonical Context

先构建工具无关的 Context Model：

```text
Workspace Context
- repositories
- roles
- commands
- protected branches

Project Context
- product summary
- glossary
- approved business rules
- design conventions
- architecture boundaries

Feature Context
- goal
- approved facts
- acceptance criteria
- scope/non-goals
- repositories
- stop conditions

Runtime Context
- active branches
- dirty state
- snapshot
- tests/check status
```

## Projection

```text
Canonical Context
      │
      ├── Codex Adapter  → AGENTS.md / task context
      ├── Claude Adapter → CLAUDE.md
      ├── Cursor Adapter → .cursor/rules/...
      └── Copilot Adapter→ copilot instructions
```

Adapter 负责格式和工具特定 guidance，不重新定义 Product Truth。

## Generated vs Human-owned

生成文件必须明确：

```text
GENERATED — edit canonical artifacts/config instead.
```

如果目标文件已有人工内容，继续沿用现有 workspace-kit 的安全策略：默认不覆盖；提供 migration/force 的显式路径。

更长期可以支持：

```text
human-owned preamble
--- generated managed block ---
...projected context...
--- end managed block ---
```

但 v0.2 应优先保持实现简单。

## Context Budget

不是所有 Artifact 都应该完整塞给 Agent。

推荐三级：

```text
Always
- repo safety
- active feature goal/scope
- stop conditions

Relevant
- owning architecture section
- applicable business rules
- related design conventions

On demand
- historical cases
- unrelated modules
- long research notes
```

`vibe context` 的目标不是生成最大上下文，而是生成最小充分上下文。

## Drift Detection

`vibe check` 可通过生成 fingerprint 检测：
- canonical source 已变化；
- generated agent rules 未刷新；
- managed output 被直接编辑。

CLI 应提示 `vibe generate/context`，而不是静默覆盖用户文件。

## Security Boundary

Context generation 必须避免：
- 读取并复制 `.env`；
- 输出 credentials；
- 将 local-only config 写入可提交 Agent files；
- 将 `.vibe` 中敏感 runtime evidence 默认提交。

Project Truth 与 Secret 是两类完全不同的信息。