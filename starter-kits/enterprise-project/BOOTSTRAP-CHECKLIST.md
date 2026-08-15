# Enterprise Project Bootstrap Checklist

## Phase A — Intent
- [ ] 用一句话说清系统解决的问题
- [ ] 识别主要 Actor
- [ ] 定义 2–5 个可观察 Outcome
- [ ] 写出明确 Non-goals
- [ ] 记录合规、部署、网络、技术栈等硬约束

**Gate A:** 不知道“为谁解决什么问题”时，不进入页面和代码设计。

## Phase B — Discovery
- [ ] 收集现有流程/表单/系统/接口 Evidence
- [ ] 建立 Glossary
- [ ] 标注 Fact / Assumption / Unknown
- [ ] 找到 Critical Workflow
- [ ] 给 Blocking Unknown 指定 Owner

**Gate B:** Agent 不得把 Unknown 自动变成 Requirement。

## Phase C — Behavior
- [ ] Critical Workflow 有 Acceptance Criteria
- [ ] Business Rule 可追踪
- [ ] State/Lifecycle 有 Owner
- [ ] Permission/Data Scope 有定义
- [ ] Edge/Failure Case 被识别

**Gate C:** QA 能从 Artifact 推导关键测试。

## Phase D — UI/UX
- [ ] 做过 Reference Research，而非让 Coding Agent自由发挥
- [ ] User Flow 已确认
- [ ] 至少比较过两个 Wireframe/方向
- [ ] 基础 Design Tokens / Component convention 已选
- [ ] Critical Page 有 Loading/Empty/Error/Permission/Success 状态

**Gate D:** 前端实现不需要猜 Information Hierarchy。

## Phase E — Architecture
- [ ] Architecture Drivers 已识别
- [ ] Module/Domain ownership 清楚
- [ ] API/Data contracts 有基本策略
- [ ] Security/Observability/Integration 风险已识别
- [ ] 重要不可逆决策写 ADR

**Gate E:** 技术选择能解释“为什么”，而不是“AI 推荐”。

## Phase F — Agent Workspace
- [ ] `AGENTS.md` 只包含稳定仓库规则
- [ ] build/test/lint commands 可执行
- [ ] 第一 Feature 有 Implementation Packet
- [ ] Scope/Non-goals/Stop Conditions 明确
- [ ] Agent 权限和 Git Safety 明确

## Phase G — First Slice
- [ ] Slice 有真实业务价值
- [ ] 足够小，可独立 Review
- [ ] 穿过必要层级但不引入整个系统复杂度
- [ ] AC → Evidence 路径明确
- [ ] 可进行 Independent Review

**Bootstrap Ready:** Phase A–G 的关键 Gate 均通过后，才把 Coding Agent 从探索者升级为主要执行者。
