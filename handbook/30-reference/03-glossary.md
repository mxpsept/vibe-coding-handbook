# Glossary

## Acceptance Criteria (AC)
可验证的完成条件。不是实现步骤。

## ADR — Architecture Decision Record
记录重要架构决策的 Context、Decision、Alternatives、Consequences 和 Revisit Trigger。

## Agent
能读取上下文、使用工具并执行多步骤任务的 AI 系统。Coding Agent 是其软件开发子类。

## Artifact
版本化的工程事实/决定载体，如 Requirement、ADR、Page Spec、API Contract、Runbook。

## Brownfield
在已有系统/仓库/约束中开发，与从零开始的 Greenfield 相对。

## Business Rule
必须成立的业务约束或计算/决策语义。

## Characterization Test
用于捕获和保护遗留系统当前行为的测试，常用于安全重构前。

## Context Engineering
设计 Agent 在正确时间获得正确 Source of Truth、代码、工具和约束的工程实践。

## Context Debt
关键工程知识隐藏、过期或不可被新成员/Agent可靠获取造成的技术债。

## Contract
系统或角色边界上的稳定约定，例如 API、Data、Permission Contract。

## Definition of Done
任务被视为完成所需的整体条件，包括 Verification，而不仅是代码完成。

## Driver
促使设计/架构选择的真实需求或约束，而非个人偏好。

## Evidence
支持判断的可检查事实：用户研究、代码、测试结果、日志、指标、benchmark 等。

## Greenfield
从零建立的新项目/系统。

## Implementation Packet
把批准 Artifact 转换成一个边界明确、可交给 Coding Agent 的执行任务。

## Non-goal
明确本次工作不解决什么，用于控制 Scope。

## Page Spec
页面结构、行为、状态、权限、错误和响应式等实现契约。

## Repository Reconnaissance
在修改存量代码前系统定位入口、Owner、Convention、Tests 和相关约束。

## Source of Truth
某类事实的权威来源。其他 Artifact 应引用而非复制并独立演化。

## SPEC_GAP / ARCH_GAP / DESIGN_SPEC_GAP
发现缺失且无法安全推断的业务、架构或设计信息时使用的显式阻塞信号。

## Stop Condition
Agent 必须停止自主执行并请求决策/报告风险的条件。

## Vertical Slice
贯穿 UI/API/Domain/Data/Test 的可交付业务切片，而不是先横向完成所有“基础层”。

## Vibe Coding
本手册中指以自然语言和 AI Coding Agent 为重要执行界面的软件开发方式；成熟实践强调 Artifact、边界和 Verification，而不是只依赖即时 Prompt。
