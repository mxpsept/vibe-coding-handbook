# START HERE — 如何使用这本 Vibe Coding Handbook

这不是一本要求从第一页顺序读到最后一页的理论书。它更像企业 AI 软件工程的 **操作系统 + Playbook + Artifact Library**。

## 你现在属于哪种场景？

### A. 我要从零开发一个新系统

```text
Foundation
→ Discovery
→ Requirements
→ Product/UI Design
→ Architecture
→ Vertical Slice Implementation
→ Testing
→ Release
→ Operations
```

第一步不要打开 Codex 写代码。先完成 `handbook/12-reference/01-project-start-checklist.md`。

### B. 我要修改一个已有项目

从：

```text
handbook/13-brownfield/01-existing-project-workflow.md
```

开始，并使用 `templates/implementation/brownfield-change-packet.template.md`。

### C. 我遇到 Bug

不要先问 AI“怎么修”。进入：

```text
handbook/14-debugging/01-evidence-driven-debugging.md
```

### D. 我要让 Codex 更稳定地开发

重点：

```text
handbook/15-agent-governance/
handbook/18-multi-agent/
templates/agent/AGENTS.example.md
checklists/implementation/agent-handoff.md
```

### E. 我要做架构/重构/升级

```text
04 Architecture
16 Refactoring
17 Migration
```

### F. 我要准备上线

```text
06 Testing
07 Delivery
08 Operations
21 Security
22 Performance
23 Incident Response
24 Observability
```

### G. 我要在企业团队推广

```text
11 Team Adoption
27 Metrics
28 Governance
29 Maturity
```

## 核心工作流

无论使用 Codex、Claude Code、Cursor 或未来 Agent，核心不变：

```text
Intent
↓
Evidence / Discovery
↓
Approved Artifact
↓
Bounded Agent Task
↓
Implementation
↓
Verification Evidence
↓
Independent Review
↓
Release / Operations
↓
Production Feedback
```

## 三条最重要原则

### 1. Chat is not Source of Truth
确认后的业务规则、设计、架构和接口进入版本化 Artifact。

### 2. AI autonomy must be bounded
Agent 应知道 Scope、Non-goals、Stop Conditions、Verification 和它拥有的 Git/生产权限。

### 3. Done requires Evidence
“AI 说完成了”“代码能编译”“页面看起来正常”都不是完整 Definition of Done。

## 推荐第一次实践

不要拿整个大型系统试验。选择一个真实但有限的 Vertical Slice，用 1–2 周完整走一次：

```text
Requirement
→ UI/Page Spec
→ API/Domain
→ Implementation Packet
→ Codex
→ Tests
→ Review
→ Release
```

然后再决定哪些流程值得自动化和标准化。
