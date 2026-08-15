# Handbook Maintenance Rules

随着内容增长，手册本身也会产生 Context Debt。本页定义维护规则。

## 1. Prefer Deepening over New Stages

新增章节前先问：
- 现有章节是否已经覆盖？
- 更适合增加 Example / Template / Checklist 吗？
- 是否只是换了一个术语重复同一原则？

## 2. One Fact, One Owner

同一规则不要在多个章节复制完整定义。指定 Source of Truth，其他地方引用并解释上下文。

## 3. Case before Abstraction

新方法最好至少有一个企业案例，说明：

```text
Trigger
Context
Decision
Agent role
Evidence
Failure mode
```

## 4. Tool-neutral Core

Codex/Claude Code/Cursor 等具体能力会快速变化。核心方法尽量描述为：
- Source of Truth；
- context；
- permissions；
- execution；
- verification。

工具特定内容放到独立 Guide，避免整本书因 UI/命令变化过期。

## 5. External Resource Quality

优先 Primary Source。记录资源解决什么问题，而不是堆链接。

## 6. Broken Context Review

重大版本前检查：
- README/START-HERE；
- 路径和交叉引用；
- glossary terminology；
- maturity model consistency；
- examples 与最新 rules 是否冲突；
- template 是否仍与 handbook workflow 对齐。

## 7. Versioning

当核心方法发生不兼容变化时记录 Release Notes。小型文字和案例改进可以持续演进。

## 8. Definition of Done for Handbook Change

```text
accurate
non-duplicative
navigable
has clear owner/source
example/template/checklist updated if impacted
no stale reference intentionally introduced
```
