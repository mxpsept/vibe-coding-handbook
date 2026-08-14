# Idea Analysis Prompt

## Purpose

用于项目 Stage 00。在任何 Coding、UI、数据库或架构设计之前，帮助团队把模糊项目想法整理为可 Review 的 `project-idea.md`。

## Prompt

```text
你是我的 Product Discovery 协作者。

我们目前处于 Idea 阶段，不是 Implementation 阶段。

【项目想法】
<用 3～5 句话描述业务背景、当前问题和期望结果>

你的目标不是帮我立即设计完整系统，而是帮助我判断这个想法是否值得进入 Discovery。

请严格遵守：
1. 不编写代码；
2. 不设计数据库；
3. 不自行确定技术栈；
4. 不设计高保真 UI；
5. 不把常见行业做法直接当作我们的需求；
6. 不把你的推测写成事实；
7. 明确区分 Fact / Assumption / Unknown；
8. 如果信息不足，保留 Unknown，而不是补齐答案。

请输出：

A. Problem Statement
B. Target Users / Stakeholders（当前假设）
C. Known Facts
D. Assumptions
E. Unknowns
F. Expected Outcomes
G. Constraints
H. Major Risks
I. Discovery Questions
J. 是否建议进入 Discovery，以及原因
K. project-idea.md 草案

最后执行 Self Review：
- 是否偷偷发明了业务规则？
- 是否过早定义了解决方案？
- 是否把 Feature 当成 Problem？
- 是否把 Assumption 写成 Fact？
- 是否存在必须由 Human 确认的关键假设？
- 是否提出了当前阶段没有必要讨论的技术实现？

如果发现以上问题，请先修正再输出最终结果。
```

## Expected input

最理想的输入不是功能清单，而是：

```text
谁正在遇到问题？
现在如何工作？
主要痛点是什么？
为什么现在值得解决？
希望改善什么业务结果？
```

## Expected output

输出应能够直接用于完善：

`templates/project/project-idea.template.md`

AI 输出仍然只是 Draft。Fact、Assumption、Decision 和 Gate Result 必须由 Human Review。
