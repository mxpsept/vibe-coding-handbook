# Versioning & Releases

Handbook 是持续演进的工程知识库，但公开使用需要稳定的版本语义。

## Recommended Scheme

使用 Semantic-like Versioning：

```text
MAJOR.MINOR.PATCH
```

### PATCH
- typo/link fix；
- wording clarification；
- example correction；
- 不改变核心 workflow。

### MINOR
- 新案例；
- 新 Template/Checklist；
- 新章节；
- 向后兼容的方法深化。

### MAJOR
核心方法发生明显不兼容变化，例如：
- Artifact ownership 被重新定义；
- Project Playbook Gate 模型大幅改变；
- maturity model 被替换；
- 推荐工程生命周期发生结构性调整。

## Release Notes

每个重要 Release 建议记录：

```text
Highlights
New / Improved
Breaking methodology changes
Deprecated guidance
Known gaps
Suggested reading path
```

## Stable vs Current

`main/default branch` 可以持续演进；对公开培训或团队制度引用，推荐引用 Release/Tag，而不是假设分支内容永远不变。

## Deprecation

不要静默删除已经被广泛引用的方法：

```text
mark deprecated
→ explain why
→ link replacement
→ remove in later major release if needed
```

## Tool-specific Content

Codex、Claude Code、Cursor 等产品变化不必推动 Handbook MAJOR。工具特定指南可以独立更新，只要核心工程 contract 未改变。

## Release Ownership

Release Maintainer 负责确认：
- Public Release Gate；
- Quality Scorecard review；
- changelog/release notes；
- tag/version；
- known gaps。

AI 可以协助生成差异摘要，但版本语义和发布责任由 Maintainer 决定。
