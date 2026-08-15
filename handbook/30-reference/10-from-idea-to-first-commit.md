# From Idea to First Commit — Quick Guide

当你下次只有一个系统想法时，先不要问 Coding Agent：

> 帮我用 Spring Boot + Vue 开发这个系统。

按下面顺序走。

## Hour 0–1: Frame the Problem

写 1 页 Product Brief：Problem、Actors、Outcome、Non-goals、Constraints。

AI 可以提问和整理，但 Unknown 保持 Unknown。

## Hour 1–3: Discover Critical Behavior

只研究 1–3 条核心 Workflow，建立 Glossary、Business Rules、State、Permission。

这一步比先列 30 个菜单重要。

## Hour 3–6: Design the First Experience

研究同类交互模式 → 画 2–3 个 Wireframe Direction → 选一个 → 明确 Page States / Component Convention。

UI 不满意通常应回到这里，而不是在 CSS 完成后无限“再美化”。

## Hour 6–8: Define Architecture Context

只决定当前 Driver 需要的：module ownership、data/API boundary、auth/error/observability basics、important ADR。

不要把架构设计变成技术清单。

## Day 2: Select First Vertical Slice

选择贯穿真实用户价值、可以端到端验证、范围足够小的 Slice。

写 AC + Scope + Non-goals + Stop Conditions + Verification。

## Day 2+: Start Codex

```text
Reconnaissance
→ Plan
→ Implement
→ Verify
→ Independent Review
→ Fix
→ AC/Evidence
→ Commit
```

## First Commit Gate

第一次 Feature Commit 前问：
- 我们实现的是批准事实还是 AI 假设？
- UI 是否已有设计方向？
- Rule/Permission 是否有明确 Owner？
- Agent 是否理解仓库边界？
- 每个关键 AC 是否有 Evidence？

如果答案大多是否定的，提交得更快通常只是在更快积累返工。

完整演示见：`examples/flowops/16-project-bootstrap/`。
