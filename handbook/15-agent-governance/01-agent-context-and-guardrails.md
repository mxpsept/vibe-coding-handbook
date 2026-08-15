# 01 — Coding Agent Context & Guardrails

## 1. Context Engineering > Prompt Tricks

Coding Agent 的结果取决于它能否在正确时间看到正确事实。

推荐 Context 分层：

```text
Organization policy
↓
Repository instructions
↓
Architecture / ADR
↓
Feature artifacts
↓
Task packet
↓
Current code + test evidence
```

越上层越稳定，越下层越任务相关。

## 2. What belongs in repository instructions

适合放稳定规则：
- build/test commands；
- directory ownership；
- architecture boundaries；
- dependency policy；
- code style/tooling；
- security rules；
- commit/PR expectations；
- known generated files / do-not-edit areas。

不要把某一个 Feature 的临时需求写成永久全局规则。

## 3. Context Budget

不是给 Agent 越多文件越好。

任务 Packet 应提供：

```text
Must Read
Useful if Needed
Do Not Need
```

减少无关上下文可以降低模型把旧 Pattern 错套到当前任务的概率。

## 4. Authority Order

出现冲突时必须有明确优先级，例如：

```text
approved business rule
> acceptance criteria
> accepted ADR
> page/API spec
> existing implementation
> task convenience
```

发现真正冲突时报告，而不是静默选择。

## 5. Agent Autonomy Levels

### L0 — Explain only
不改文件。

### L1 — Plan
允许仓库分析和方案，不写代码。

### L2 — Bounded implementation
在批准 Task Packet 内自主实现和测试。

### L3 — Broad refactor
允许跨模块修改，但需要明确目标/guardrail。

### L4 — Release/production action
必须受组织权限、审批和可回滚机制约束。

任务应明确所需 autonomy，而不是默认无限权限。

## 6. Stop Conditions as First-class Contract

Stop Conditions 不是 Prompt 尾部装饰。典型条件：
- business semantic unknown；
- architecture decision required；
- destructive migration；
- secret/credential required；
- production mutation outside authorization；
- unexpected unrelated failing baseline；
- scope expansion materially changes review surface。

## 7. Fresh Session Test

一个成熟项目应该能让一个全新的 Agent Session：
1. 读 repository instructions；
2. 读 task packet；
3. 找到正确模块；
4. 解释约束；
5. 在不依赖历史聊天记忆的情况下完成任务。

如果做不到，说明关键 Context 仍被困在聊天或个人经验里。

## 8. Context Drift Review

定期检查：
- README 是否过期；
- ADR 是否已 superseded；
- Prompt 是否引用不存在路径；
- build/test command 是否仍有效；
- Design System/Architecture 与代码是否漂移。

过期 Context 比没有 Context 更危险。
