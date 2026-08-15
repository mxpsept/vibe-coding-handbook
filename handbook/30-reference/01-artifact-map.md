# Artifact Map — 每一种文档到底解决什么问题

Artifact 的目的不是增加文档，而是把关键决定从聊天和个人记忆中提取出来。

| Artifact | Core Question | Primary Owner | Consumed By |
| --- | --- | --- | --- |
| Product Brief | 为什么做？为谁做？ | Product | all roles |
| Discovery Notes | 我们知道什么 Evidence？ | Product/Research | Requirement |
| Glossary | 术语到底是什么意思？ | Product/Domain | humans + agents |
| User Story / Job | 用户要完成什么？ | Product | Design/Dev/Test |
| Acceptance Criteria | 怎样算完成？ | Product/QA | Dev/Test/Review |
| Business Rules | 哪些业务约束必须成立？ | Domain/Product | Architecture/Dev/Test |
| State Model | 生命周期如何变化？ | Product/Architecture | UI/API/Domain/Test |
| Permission Model | 谁能看/做什么？ | Product/Security | UI/API/Test |
| User Flow | 用户如何完成任务？ | Design/Product | UI/Dev/Test |
| Wireframe | 信息与交互结构？ | Design | Product/UI |
| Design System | 视觉语言如何保持一致？ | Design | UI/Agent |
| Page Spec | 页面各种状态如何工作？ | Design/Product | Frontend/Test |
| Quality Attributes | 系统必须多可靠/快/安全？ | Architecture | Design/Dev/Ops |
| ADR | 为什么选择这个重要技术决策？ | Architecture | Agents/Review |
| Module Boundary | 代码责任在哪里？ | Architecture | Dev/Agent |
| API Contract | 系统边界如何通信？ | Architecture/Dev | FE/BE/Test/Integration |
| Data Contract | 数据语义与兼容规则？ | Data/Domain | Dev/Analytics/Ops |
| Implementation Packet | 这次 Agent 具体做什么？ | Engineer/Lead | Coding Agent |
| Test Plan | 如何证明行为？ | QA/Engineer | Agent/CI |
| Runbook | 生产异常如何安全处理？ | Ops/Engineering | Incident responders |
| Incident Context | 事故事实/动作是什么？ | Incident team | responders/postmortem |
| Debt Register | 接受了哪些妥协？何时偿还？ | Tech Lead | planning |
| AI Project Policy | Agent 可以访问/执行什么？ | Org/Project | all AI workflows |

## Artifact Dependency

```text
Discovery
↓
Requirements + Rules + Glossary
↓
UX / State / Permission
↓
Architecture / ADR / Contracts
↓
Implementation Packet
↓
Code + Tests
↓
Release Evidence / Runbook
↓
Production Evidence
```

## Rule

如果两个 Artifact 重复维护同一事实，指定一个 Owner/Source of Truth，其他文档链接引用，而不是复制后独立演化。
