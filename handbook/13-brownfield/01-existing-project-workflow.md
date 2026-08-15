# 01 — 存量项目中的 Vibe Coding：先理解，再修改

新项目可以建立理想 Artifact；现实中更多任务发生在已有系统中。Brownfield AI Coding 的第一原则是：**Repository 本身也是 Evidence。**

## 1. 为什么存量项目风险更高

Coding Agent 很容易看到局部问题后提出“更现代”的全局方案：重构目录、更换请求层、引入状态库、统一 DTO、升级框架。局部看合理，但它可能破坏隐藏约束。

因此默认流程应是：

```text
Task
→ Repository Reconnaissance
→ Existing Behavior
→ Change Boundary
→ Characterization
→ Minimal Design
→ Implementation
→ Regression Verification
```

## 2. Repository Reconnaissance

编码前回答：
- 功能入口在哪里？
- 同类 Feature 如何实现？
- API / persistence / state / error convention 是什么？
- 哪些测试保护当前行为？
- 是否存在 ADR / README / agent instructions？
- 最近相关修改是什么？

输出一个简短 Repository Map，而不是立刻改代码。

## 3. Preserve before Improve

如果任务是 Bug Fix 或小 Feature，先记录：

```text
Behavior to preserve
Behavior to change
Explicit non-goals
```

对缺少测试的遗留逻辑，必要时先补 Characterization Test。

## 4. Local Convention Wins

除非当前 Convention 明显导致任务无法正确实现，否则：

```text
existing project convention
>
agent's favorite pattern
```

“我通常建议”不是重构理由。

## 5. Change Budget

每个任务设定 Change Budget：

```text
Required change
Allowed supporting change
Out-of-scope cleanup
```

发现值得重构的问题，记录 Technical Debt / follow-up，而不是顺手扩大 PR。

## 6. Brownfield Stop Conditions

Agent 应停止并报告：
- 现有行为与需求冲突但没有产品决定；
- 修改需要改变公共 API；
- 数据迁移不可避免；
- 需要升级框架/核心依赖；
- 找不到关键行为的 Source of Truth；
- 修改跨越多个高耦合模块且回归面未知。

## 7. Example

需求：在已有任务详情页增加“完成声明”。

错误：为了新按钮把整个详情页迁移到新状态管理库。

正确：
1. 找到现有详情页和 API convention；
2. 确认 Completion Claim 业务语义；
3. 找同类 action/modal 实现；
4. 增加最小 API + UI + tests；
5. 保持已有状态管理；
6. 单独记录未来重构建议。

## 8. Brownfield Definition of Done

不仅是新功能工作，还要证明：
- 原行为未意外改变；
- migration/compatibility 已考虑；
- 新代码遵守现有边界；
- 相关回归测试通过；
- 没有无关 architecture churn。
