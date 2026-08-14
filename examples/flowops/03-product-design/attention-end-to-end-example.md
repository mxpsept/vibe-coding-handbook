# FlowOps — Attention 页面端到端 AI Design Workflow

> 本案例演示如何把 Stage 02 的 Requirement 一路转换成可以交给 Codex 的前端实现任务。

## Step 1 — Requirement Input

已知业务语义：

```text
Supervision Specialist 需要识别并核验需要关注的事项。
Attention 可能包含 STALE_UPDATE / NEAR_DUE / OVERDUE。
Attention != Lifecycle。
一个事项可同时拥有多个 Attention Flags。
STALE_UPDATE 只证明长时间没有新的进展信息，不证明执行停滞。
```

此时不要生成页面。

---

## Step 2 — Run Design Research

使用：

```text
prompts/product-design/design-research.prompt.md
```

输入：

```text
Actor: Supervision Specialist
Primary Job: 快速核验需要关注的事项并理解原因
Device: desktop enterprise web
```

### Expected research directions

```text
issue triage
review queue
master-detail / split view
work inbox
enterprise filtering
activity context
```

### Reference finding example

| Pattern | Observation | Fit |
| --- | --- | --- |
| dense table | scans many rows efficiently | Medium |
| split view | queue remains visible while context changes | High |
| kanban | good for mutually exclusive workflow stages | Low |

这里已经能发现：Kanban 与“多 Attention 并存”存在模型冲突。

---

## Step 3 — Generate 3 Wireframes

使用：

```text
prompts/product-design/wireframe-generator.prompt.md
```

得到：

```text
A Filtered Table
B Attention Split View
C Kanban by Attention Type
```

### Human Decision

选择 B，因为：

```text
Job Fit: High
Context preservation: High
Navigation cost: Low
Multi-attention integrity: High
```

拒绝 C，因为一个 Item 可能同时 `STALE_UPDATE + NEAR_DUE`。

记录决定，而不是让下一轮 AI 重新选择。

---

## Step 4 — Choose Visual Direction

使用：

```text
prompts/product-design/visual-direction.prompt.md
```

候选：

```text
Enterprise Neutral
Modern Operational
Executive Minimal
```

### Human Decision

Attention 选择 `Modern Operational`：

```text
moderate density
strong hierarchy
restrained surfaces
attention-aware semantic color
minimal decoration
```

但 All Items 可以使用同一 Design System 下更 Compact 的 composition。

---

## Step 5 — Apply Design System

读取：

```text
examples/flowops/03-product-design/design-system.md
```

关键 Contract：

```text
LifecycleBadge
!=
AttentionIndicator
```

示例：

```text
[办理中]
已超过有效截止日期 3 天
8 天未收到新的进展信息
```

而不是：

```text
[异常]
```

---

## Step 6 — Expand UI State Space

读取：

```text
ui-state-matrix.md
```

Attention 至少覆盖：

```text
Loading
Empty
Filter No Result
Error
Unauthorized
Selected Item Error
Multiple Attention
Long Content
Many Items
```

### Example

Empty：

```text
当前没有需要核验的事项。
```

Filter No Result：

```text
当前筛选条件下没有关注事项。
[清除筛选]
```

两者业务含义不同。

---

## Step 7 — Generate Page Spec

使用：

```text
prompts/product-design/page-spec-generator.prompt.md
```

产物：

```text
page-specs/attention.md
```

此时实现边界已经明确：

```text
Queue
Selected Context
Attention Explanation
Latest Progress
Open Full Detail
```

同时明确：

```text
催办
升级
忽略
标记已核验
```

如果 Requirements 没有定义，就不能因为“这类系统通常有”而加入。

---

## Step 8 — Run UX Reviewer

使用：

```text
prompts/product-design/ux-reviewer.prompt.md
```

### Example finding

```text
HIGH
Location: Selected Item Header
Problem: UI displays “任务停滞 8 天” for STALE_UPDATE.
Why: Evidence only proves no new progress update.
Affected rule: Attention semantics.
Fix: “8 天未收到新的进展信息”.
Owner: UX/Product.
```

这类问题不是 CSS Bug，而是 Semantic Defect。

---

## Step 9 — Prepare Codex Implementation Packet

使用：

```text
prompts/product-design/frontend-implementation.prompt.md
```

实例化：

```text
GOAL
Implement FlowOps Attention Workspace.

READ FIRST
- examples/flowops/02-requirements/business-rules.md
- examples/flowops/02-requirements/state-model.md
- examples/flowops/03-product-design/page-specs/attention.md
- examples/flowops/03-product-design/design-system.md
- examples/flowops/03-product-design/ui-state-matrix.md

IMPLEMENT
- desktop split view
- attention filters
- queue
- selected context
- lifecycle badge
- multiple attention indicators
- loading/empty/no-result/error states

DO NOT
- implement Kanban
- create risk score
- add reminder/escalation action
- merge lifecycle and attention
- invent local colors

STOP IF
- backend does not expose attention reasons/data needed by approved Page Spec
- permission semantics are missing
```

---

## Step 10 — Codex Repository Inspection

Codex 应先查看：

```text
existing routes
layout
component library
state/query approach
design tokens
API client
existing tests
```

然后给出 Plan。

不要一收到 Prompt 就创建：

```text
src/components/NewDesignSystem/
```

---

## Step 11 — Implementation Review

Review 分三层。

### Functional

```text
data correct?
actions correct?
filters correct?
```

### Semantic

```text
Lifecycle != Attention?
Multiple flags supported?
STALE copy accurate?
```

### Visual / UX

```text
queue scanable?
selected context clear?
density appropriate?
long content works?
empty/error states designed?
tokens reused?
```

---

## Step 12 — Trace the Result

最终链路：

```text
Discovery Finding
↓
Requirement
↓
Business Rule / Attention semantics
↓
User Flow UF-002
↓
Wireframe Direction B
↓
Page Spec P-004
↓
Frontend Components
↓
Code
↓
Tests / Visual QA
```

如果以后用户反馈：

```text
“为什么这里把未更新写成任务停滞？”
```

团队可以定位这是：

```text
Semantic presentation defect
```

而不是模糊地说：

```text
前端文案改一下。
```

---

# Reusable Lesson

整个案例最重要的不是 Split View 本身。

而是：

```text
AI Research
→ AI Alternatives
→ Human Decision
→ AI Specification
→ AI Review
→ Codex Implementation
→ Human/Automated Verification
```

AI 在每个阶段承担不同角色，人类保留业务和产品决策权。
