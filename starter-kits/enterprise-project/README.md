# Enterprise Project Bootstrap Kit

这套 Starter Kit 用于把一个新的企业软件想法初始化成 **AI-ready Engineering Workspace**。

它不是代码脚手架，而是代码脚手架之前的“决策与上下文脚手架”。

## 从一句想法开始

```text
Idea
→ 00-product-brief
→ 01-discovery
→ 02-requirements
→ 03-design
→ 04-architecture
→ 05-feature-slices
→ AGENTS.md
→ Coding Agent
→ Verification
```

## 推荐目录

```text
project/
├── AGENTS.md
├── docs/
│   ├── 00-product/
│   │   ├── product-brief.md
│   │   └── glossary.md
│   ├── 01-discovery/
│   │   └── discovery-log.md
│   ├── 02-requirements/
│   │   ├── business-rules.md
│   │   ├── state-model.md
│   │   └── permission-model.md
│   ├── 03-design/
│   │   ├── design-context.md
│   │   └── page-specs/
│   ├── 04-architecture/
│   │   ├── architecture-context.md
│   │   └── decisions/
│   └── 05-features/
│       └── FEAT-001/
│           ├── feature-spec.md
│           ├── implementation-packet.md
│           └── verification.md
└── source...
```

## Bootstrap Principle

不要第一天就把所有文档写满。按 Risk Progressive Disclosure：

- 产品事实成熟时写 Product/Requirement；
- UI 决策会影响实现时写 Page Spec；
- 技术选择有长期成本时写 ADR；
- Feature 要交给 Agent 时写 Implementation Packet；
- 准备接受结果时记录 Verification Evidence。

## First Vertical Slice

第一次不要选“完整用户权限体系”或“整个工作台”。选择一个端到端、有限且有真实业务价值的 Slice，例如：

```text
任务列表
→ 查看详情
→ 一个受权限约束的业务动作
→ 状态变化
→ 可验证结果
```

它应穿过 UI、API、Domain、Persistence 和 Test，但保持规则数量有限。

## Bootstrap Done

项目不是“目录建好了”就完成 Bootstrap。至少满足：

```text
problem understood
critical vocabulary aligned
first workflow specified
UI direction chosen
architecture boundary known
first slice agent-ready
verification path executable
```
