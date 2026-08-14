# Contributing to Vibe Coding Handbook

## 1. 目标

所有内容必须服务于一个目标：

> 帮助读者把 AI 从"代码生成器"升级为受规范约束、可验证的软件工程协作者。

本项目不是新闻合集、工具排行榜或 Prompt 大全。

## 2. 每章强制结构

原则上每章必须覆盖：

1.  **Why** --- 为什么需要这个能力；
2.  **Concepts** --- 核心概念；
3.  **When** --- 何时使用、何时不使用；
4.  **Workflow** --- 标准流程；
5.  **FlowOps Case** --- 贯穿案例；
6.  **Practice** --- 可执行练习；
7.  **Prompt** --- AI 协作模板；
8.  **Expected Artifact** --- 应产生什么项目资产；
9.  **Bad Practice** --- 常见错误；
10. **Review** --- 如何验证；
11. **Checklist** --- 进入下一阶段前的 Gate；
12. **Learning Resources** --- 延伸学习。

章节不要求机械使用相同标题，但内容必须完整。

## 3. Artifact First

重要结论不能只存在正文描述中。

如果一个结论会影响后续开发，应形成 Artifact，例如：

-   PRD；
-   Business Rule；
-   Design System；
-   ADR；
-   API Contract；
-   Feature Spec；
-   Test Plan；
-   Release Checklist。

正文负责解释，Template 负责复用，FlowOps Example 负责证明。

## 4. FlowOps 案例规则

FlowOps 是完全虚构案例。

禁止：

-   使用真实企业名称；
-   使用真实员工姓名；
-   使用真实内部系统截图；
-   使用真实业务数据；
-   引入某公司的内部流程作为 FlowOps 专有事实；
-   让案例在不同章节出现相互冲突的业务规则。

允许：

-   使用企业任务督办领域的通用业务模式；
-   使用虚构组织、人员、数据；
-   为教学目的制造需求变化、Bug、设计问题和架构冲突。

所有新增核心业务规则应先更新 `examples/flowops/CASE-SPEC.md` 或相应
Artifact。

## 5. 工具中立

方法论不得依赖单一工具。

推荐表达：

> Coding Agent 应先读取 Feature Spec 和相关 Architecture Context。

而不是：

> 必须点击某产品的某按钮。

具体工具可以作为实现示例，例如：

-   Codex；
-   Claude Code；
-   Cursor；
-   Gemini CLI；
-   GitHub Copilot。

但方法论必须在替换工具后仍然成立。

## 6. Prompt 编写规则

Prompt 不应该成为隐藏 Spec。

避免一个 5,000 字 Prompt 同时描述业务、UI、架构、测试和 Git 规则。

推荐：

``` text
Prompt
  +
Referenced Artifacts
  +
Current Task
  +
Acceptance Criteria
```

Prompt 应说明：

-   Role（必要时）；
-   Goal；
-   Context to read；
-   Scope；
-   Constraints；
-   Expected output；
-   Verification。

## 7. UI 内容规则

UI 章节不得只讨论"高级感""科技感"等主观词。

设计应尽可能落实为：

-   Information Hierarchy；
-   Layout；
-   Design Token；
-   Component；
-   State；
-   Interaction；
-   Responsive Rule；
-   Accessibility；
-   Visual Verification。

推荐工作流：

``` text
Reference → Wireframe → Design System → High Fidelity
→ Implementation → Screenshot → Visual Review
```

## 8. 代码内容规则

示例代码必须：

-   有明确上下文；
-   尽可能小；
-   不为了展示技术而引入不必要复杂度；
-   明确是 production pattern 还是 teaching simplification；
-   与 FlowOps 当前架构版本一致。

## 9. Verification 规则

任何"完成"都应该尽可能有证据。

例如：

-   编译结果；
-   Test Result；
-   API Response；
-   Screenshot；
-   Acceptance Criteria Mapping；
-   Review Result。

禁止把"AI 已确认完成"作为验证证据。

## 10. 外部资料等级

### Level A --- Primary Source

优先使用：

-   官方文档；
-   正式标准；
-   官方 GitHub Repository；
-   官方课程。

### Level B --- High Quality Community

包括：

-   成熟开源项目；
-   知名工程团队技术文章；
-   高质量会议；
-   大学课程；
-   有充分技术证据的实践文章。

### Level C --- Inspiration

包括：

-   UI 灵感；
-   社区讨论；
-   个人经验；
-   案例集合。

引用时应避免把 Inspiration 表述为行业标准。

## 11. 链接维护

外部链接必须：

-   尽量使用 canonical URL；
-   优先官方首页或长期稳定文档入口；
-   避免带营销跟踪参数；
-   不把临时搜索结果作为永久学习入口；
-   定期检查失效链接。

## 12. Decision Gate

每个 Stage 应明确是否需要 Gate。

Gate 必须回答：

-   当前 Artifact 是否完整？
-   是否存在阻断性未知项？
-   是否可以安全进入下一阶段？
-   谁拥有最终决策权？

AI 可以 Review Gate，但 Human 保留最终 Approval。

## 13. 写作风格

要求：

-   中文为主，关键行业术语保留英文；
-   第一次出现的重要英文术语给出中文解释；
-   少使用空泛口号；
-   优先流程、案例、Artifact 和对比；
-   不假设读者是 UI Designer 或 Product Manager；
-   不把"最佳实践"写成绝对真理；
-   明确 Trade-off。

## 14. Commit 建议

文档提交建议使用 Conventional Commit 风格：

``` text
docs: add product discovery chapter
docs: refine flowops business rules
templates: add feature spec template
prompts: add ui review prompt
examples: add flowops task lifecycle
resources: update design learning links
```

## 15. Definition of Done --- Chapter

一章进入 `done` 前至少确认：

-   [ ] 核心概念准确；
-   [ ] 有企业场景；
-   [ ] 有 FlowOps 案例；
-   [ ] 有实际操作；
-   [ ] 有 Artifact；
-   [ ] 有错误示例或风险；
-   [ ] 有验证方式；
-   [ ] 有 Checklist；
-   [ ] 有高质量延伸资源；
-   [ ] 不依赖单一 AI 工具；
-   [ ] 与已有章节和 CASE-SPEC 无冲突；
-   [ ] 关键外部事实有可靠来源。
