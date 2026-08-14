# FlowOps Case Specification v1.0

## 1. 项目定义

**名称：** FlowOps

**定位：** 企业任务督办与协同管理平台。

**性质：** 完全虚构的教学案例。

FlowOps 用于演示如何从模糊企业需求出发，利用 AI
完成需求发现、产品设计、UI/UX、架构、开发、验证、部署和持续演进。

## 2. 初始业务描述

案例开始时，团队只知道：

> 某中大型企业长期通过
> Excel、即时通讯、邮件和会议跟踪重点任务。随着任务数量增加，逐渐出现信息分散、责任不清、进度更新不及时、临期超期发现困难、管理者缺少整体执行视图等问题。企业希望建设一套重点任务督办系统。

此时不得假设最终功能。

Discovery 的目的就是发现真实需求。

## 3. 虚构企业背景

为了便于教学，定义一个虚构组织：

**企业：** Northstar Group（北辰集团，虚构）

**规模：** 约 3,000 名员工。

**组织特点：**

-   总部 + 多个业务部门；
-   存在跨部门重点工作；
-   管理层定期召开经营和专项会议；
-   部分重点任务需要持续数周或数月；
-   当前大量使用 Excel、邮件和即时通讯协作。

Northstar Group 与任何现实企业无对应关系。

## 4. 初始角色假设

这些角色属于 Discovery 初始假设，允许后续修订。

### 4.1 管理者

关注：

-   重点任务整体完成情况；
-   哪些事项存在风险；
-   哪些部门长期延期；
-   本周 / 本月有哪些重点事项。

### 4.2 督办人员

负责：

-   创建和下达督办事项；
-   跟踪办理情况；
-   催办；
-   检查临期和超期事项；
-   汇总督办情况。

### 4.3 部门负责人

负责：

-   接收部门任务；
-   分配或确认责任人；
-   查看部门任务进度；
-   协调资源。

### 4.4 执行人员

负责：

-   查看自己的任务；
-   填报进展；
-   上传附件；
-   反馈问题；
-   申请办结。

### 4.5 系统管理员

负责：

-   组织；
-   用户；
-   角色；
-   权限；
-   基础配置。

## 5. 初始业务问题

已知问题：

1.  任务来源分散；
2.  Excel 版本难统一；
3.  责任人和协办关系不清晰；
4.  进度需要人工询问；
5.  临期事项发现太晚；
6.  超期后缺乏统一催办记录；
7.  管理层无法快速看到整体执行情况；
8.  历史过程难追溯。

未知问题必须通过 Discovery 发现，而不是由 AI 自行补齐。

## 6. 预期领域概念（非最终模型）

随着 Discovery 推进，可能出现：

``` text
Task
TaskSource
Department
Assignee
Collaborator
ProgressUpdate
Reminder
Urge
Extension
Completion
Attachment
Comment
Notification
AuditLog
```

这些概念在 Domain Modeling 前均视为候选，不视为最终数据库实体。

## 7. 候选任务生命周期

初始假设：

``` text
Draft
  ↓
Issued
  ↓
Accepted
  ↓
In Progress
  ↓
Completion Requested
  ↓
Completed
```

可能存在：

``` text
Returned
Cancelled
Overdue
Extended
```

具体状态及转换规则必须在 Requirements 阶段确认。

## 8. 候选任务来源

可能包括：

-   管理会议；
-   年度重点工作；
-   专项工作；
-   管理层安排；
-   部门重点事项；
-   其他人工创建来源。

是否全部进入 MVP，由 Product Discovery 和 Prioritization 决定。

## 9. MVP 假设

为了控制案例规模，初步候选 MVP：

-   工作台；
-   督办事项管理；
-   任务下达；
-   我的任务；
-   进度填报；
-   临期 / 超期识别；
-   催办；
-   任务办结；
-   基础统计；
-   组织、用户、角色和权限。

MVP 在 PRD 完成前不是最终承诺。

## 10. 后续演进候选

用于书籍后续章节：

### Collaboration

-   评论；
-   @成员；
-   附件；
-   子任务；
-   协办；
-   活动时间线。

### Governance

-   延期申请；
-   任务变更；
-   取消；
-   核销；
-   审计日志；
-   数据权限。

### Analytics

-   管理驾驶舱；
-   部门执行分析；
-   超期趋势；
-   更新频率；
-   完成周期。

### Integration

-   Email；
-   企业即时通讯；
-   Calendar；
-   Open API；
-   Webhook。

### AI

-   AI 每日督办简报；
-   AI 周报；
-   AI 风险事项识别；
-   AI 自然语言查询；
-   AI 创建任务助手；
-   AI 总结任务历史。

## 11. 非目标

FlowOps 教学案例不追求：

-   覆盖所有项目管理能力；
-   成为 Jira / Asana / Linear 的复制品；
-   演示某个特定行业专有流程；
-   模拟真实公司的组织架构；
-   使用真实企业数据。

## 12. 技术栈候选

为了贴近典型企业项目，案例默认候选：

### Frontend

-   Vue 3
-   TypeScript
-   Vite
-   Element Plus
-   Pinia
-   Vue Router
-   ECharts

### Backend

-   Java
-   Spring Boot
-   Spring Security
-   ORM / SQL Access Layer

### Infrastructure

-   PostgreSQL
-   Redis
-   Object Storage
-   Nginx
-   Docker

搜索、消息队列、Elasticsearch 等组件只有在需求和架构证明需要时才加入。

原则：

> 不为了展示技术而增加技术。

## 13. 教学中的故意失败

FlowOps 将故意制造典型 AI Coding 问题，例如：

-   Dashboard 功能正确但 UI 很差；
-   AI 在没有 Spec 时误解业务；
-   Vue 页面变成超大单文件；
-   前后端 API 理解不一致；
-   AI 修改 Feature A 时破坏 Feature B；
-   测试缺失但 Agent 声称完成；
-   Design System 缺失导致页面风格漂移；
-   Context 过载导致 Agent 输出质量下降；
-   Requirement Change 没有同步 Spec。

每个失败都用于引出对应工程方法。

## 14. 案例演进原则

每次新增 FlowOps 规则时：

``` text
Discovery / Feedback
        ↓
Decision
        ↓
Update Artifact
        ↓
Review
        ↓
Commit
        ↓
Project Truth
```

不得直接因为某一章需要示例而临时创造与已有 Spec 冲突的业务事实。

## 15. 隐私与公开规则

FlowOps 必须保持完全虚构：

-   不引用真实公司内部项目；
-   不使用真实人员；
-   不使用内部 IP、域名、账号；
-   不使用真实业务截图；
-   不使用保密文档；
-   示例数据必须人工构造。

这使 FlowOps 可以安全地作为公开 Handbook 的 Reference Application。
