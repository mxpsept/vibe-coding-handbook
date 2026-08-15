# Agent Context Budget

AI Coding 不是“给越多上下文越好”。上下文也有成本：噪声、冲突、过期事实会降低 Agent 判断质量。

## Context Layers

### L1 Repository Stable Context
`AGENTS.md`、build/test、architecture boundaries、conventions。

### L2 Domain Context
当前模块 glossary、state/rule、API/data contract。

### L3 Task Context
Feature Spec、Implementation Packet、AC、Non-goals。

### L4 Runtime Evidence
错误日志、diff、test output、screenshots、query plan。

### L5 Conversation
临时讨论和探索。

优先级：Artifact/Evidence > chat recollection。

## Load What the Task Needs

一个前端小修复通常不需要把完整企业 PRD、所有 ADR、数据库 schema 全部塞入 context。

推荐：

```text
stable instructions
+ task packet
+ owning module
+ directly relevant contracts/tests
+ evidence
```

## Context Smells

- 同一规则在 Prompt、PRD、README、代码注释中有四个版本；
- 每次都复制几千行聊天历史；
- Agent 读了整个 monorepo 却不知道 owning module；
- 使用已经过期的截图/接口文档；
- Prompt 里重复十次“不要犯错”，却没有 Acceptance Criteria。

## Compression Rule

长期上下文应该压缩成 Artifact：

```text
Conversation → Decision → concise Artifact → Git
```

不要把 Conversation 本身当长期记忆系统。

## Session Reset

以下情况考虑开新 Agent/session：
- 从 implementation 转 independent review；
- 任务目标发生明显变化；
- context 被大量失败尝试污染；
- Agent 开始持续引用已否决方案；
- 需要重新从 Evidence 独立判断。

## Practical Target

最好的 Context 不是最大 Context，而是：

> 足够让 Agent 正确理解任务，又足够小到能明确区分事实、约束、证据和未知项。
