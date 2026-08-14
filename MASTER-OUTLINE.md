# Vibe Coding Handbook --- Master Outline v1.0

## 0. 使用说明

这不是一本按工具菜单编写的 Codex 教程，而是一套企业级 AI Native Software
Engineering 生命周期。

每一章默认包含：

1.  Why
2.  Concepts
3.  When to use
4.  Workflow
5.  FlowOps Case
6.  Practice
7.  Prompt
8.  Expected Artifact
9.  Bad Practice
10. Review
11. Checklist
12. Learning Resources

------------------------------------------------------------------------

# Stage 00 --- Foundations

## 第 0 章：从 Vibe Coding 到 AI Native Software Engineering

### 0.1 Vibe Coding 带来了什么

### 0.2 为什么原型成功不代表企业项目成功

### 0.3 AI Coding 的优势、边界和典型失效模式

### 0.4 为什么"一句话开发整个系统"会失控

### 0.5 Human 与 AI 的职责边界

### 0.6 AI Native Software Engineering 的定义

### 0.7 从 Prompt-Driven 到 Spec-Driven

### 0.8 从 Chat-Driven 到 Artifact-Driven

### 0.9 从"生成代码"到 Verification Loop

### 0.10 企业采用 AI Coding 的成熟度模型

**FlowOps 节点：** 只有一句业务想法，不允许 Coding Agent 写代码。

**实践：** 将自己的项目描述限制为 3～5 句话，识别未知项。

**Artifact：** `project-idea.md`

**Gate 0：** 是否值得进入 Discovery？

------------------------------------------------------------------------

# Stage 01 --- Discovery

## 第 1 章：从模糊想法发现真正的问题

### 1.1 Solution 与 Problem 的区别

### 1.2 Stakeholder Mapping

### 1.3 用户角色与 Persona

### 1.4 Pain Point

### 1.5 Jobs To Be Done

### 1.6 当前业务流程 As-Is

### 1.7 目标业务流程 To-Be

### 1.8 AI 如何辅助需求访谈

### 1.9 如何避免 AI 替用户猜需求

### 1.10 Discovery Interview Prompt

**FlowOps：**
从"做一个督办系统"发现任务来源、下达、签收、办理、催办、延期、办结等真实流程。

**Artifact：** - `vision.md` - `stakeholders.md` -
`discovery-notes.md` - `as-is-process.md` - `to-be-hypothesis.md`

**Gate 1：** 问题是否真实、重要且值得解决？

------------------------------------------------------------------------

# Stage 02 --- Requirements

## 第 2 章：把发现转化为可执行需求

### 2.1 Functional / Non-functional Requirements

### 2.2 User Story

### 2.3 Use Case

### 2.4 Business Rule

### 2.5 Acceptance Criteria

### 2.6 Scope / Out of Scope

### 2.7 MVP

### 2.8 Requirement Priority

### 2.9 Requirement Traceability

### 2.10 PRD

### 2.11 AI Requirement Review

### 2.12 Requirement Ambiguity Checklist

**FlowOps：** 形成 MVP PRD。

**Artifact：** - `prd.md` - `business-rules.md` - `user-stories.md` -
`acceptance-criteria.md` - `glossary.md`

**Gate 2：** 需求是否足以进入产品设计？

------------------------------------------------------------------------

# Stage 03 --- Product Design

## 第 3 章：从需求到产品结构

### 3.1 Domain 与 Feature

### 3.2 Information Architecture

### 3.3 Navigation Design

### 3.4 User Journey

### 3.5 User Flow

### 3.6 Page Inventory

### 3.7 Page Goal

### 3.8 Information Hierarchy

### 3.9 Empty / Loading / Error / Permission States

### 3.10 Desktop / Mobile 场景差异

**FlowOps：** - 工作台 - 督办事项 - 我的任务 - 过程管理 - 统计分析 -
系统管理

**Artifact：** - `domain-map.md` - `information-architecture.md` -
`user-flows.md` - `page-inventory.md`

**Gate 3：** 业务流程、页面结构和角色路径是否成立？

------------------------------------------------------------------------

# Stage 04 --- UI / UX

## 第 4 章：没有 UI 思路时，应该怎样开始

### 4.1 为什么不要从颜色开始

### 4.2 UI Reference Research

### 4.3 如何学习而不是复制优秀产品

### 4.4 Moodboard

### 4.5 Wireframe

### 4.6 Visual Direction

### 4.7 High Fidelity

### 4.8 UI Review

## 第 5 章：建立 Design System

### 5.1 Design Token

### 5.2 Color

### 5.3 Typography

### 5.4 Spacing

### 5.5 Radius / Shadow / Elevation

### 5.6 Icon

### 5.7 Component

### 5.8 Pattern

### 5.9 Layout

### 5.10 Status Semantic

### 5.11 Responsive

### 5.12 Design System 与前端组件库的关系

## 第 6 章：AI UI Workflow

核心流程：

``` text
Reference
  ↓
Wireframe
  ↓
Design System
  ↓
High Fidelity
  ↓
Implementation
  ↓
Screenshot
  ↓
Visual Verification
```

### 6.1 Design Agent

### 6.2 UI Implementation Agent

### 6.3 Visual Reviewer

### 6.4 Screenshot Comparison

### 6.5 如何避免 AI "越改越丑"

### 6.6 如何控制页面间视觉漂移

**FlowOps：** 完成工作台、督办列表、详情、新建任务和领导驾驶舱设计。

**Artifact：** - `wireframes/` - `design-direction.md` -
`design-system.md` - `ui-spec.md`

**Gate 4：** 设计是否达到 Development Ready？

------------------------------------------------------------------------

# Stage 05 --- Context Engineering

## 第 7 章：Prompt Engineering 之后是什么

### 7.1 Prompt 与 Context 的区别

### 7.2 Context Window ≠ Context Engineering

### 7.3 Project Context

### 7.4 Business Context

### 7.5 Product Context

### 7.6 Design Context

### 7.7 Architecture Context

### 7.8 Development Context

### 7.9 Task Context

### 7.10 Context Selection

### 7.11 Context Freshness

### 7.12 Context Conflict

## 第 8 章：建立 Project Truth

### 8.1 Chat 不是 Project Truth

### 8.2 Artifact Lifecycle

### 8.3 Source of Truth

### 8.4 Artifact Priority

### 8.5 Spec Versioning

### 8.6 Decision Log

### 8.7 AGENTS.md

### 8.8 Repository-level 与 Module-level Agent Instructions

**FlowOps：** 建立 AI 可读取的项目上下文体系。

**Artifact：** - `AGENTS.md` - `docs/context-map.md` -
`docs/decision-log.md`

------------------------------------------------------------------------

# Stage 06 --- Architecture

## 第 9 章：AI 时代的架构设计

### 9.1 Architecture Before Code

### 9.2 Quality Attributes

### 9.3 C4 Model

### 9.4 System Context

### 9.5 Container

### 9.6 Component

### 9.7 Deployment View

## 第 10 章：领域与数据设计

### 10.1 Domain Model

### 10.2 Aggregate / Entity / Value Object

### 10.3 ER Model

### 10.4 Schema

### 10.5 Migration

### 10.6 Audit Data

## 第 11 章：API Contract

### 11.1 Contract First

### 11.2 REST

### 11.3 OpenAPI

### 11.4 Error Model

### 11.5 Pagination

### 11.6 Idempotency

### 11.7 API Versioning

## 第 12 章：企业基础能力

### 12.1 Authentication

### 12.2 RBAC

### 12.3 Data Permission

### 12.4 Logging

### 12.5 Audit

### 12.6 Cache

### 12.7 File Storage

### 12.8 Search

### 12.9 Notification

### 12.10 Security

## 第 13 章：ADR

### 13.1 什么需要 ADR

### 13.2 Context / Decision / Consequence

### 13.3 AI 生成 ADR 的风险

### 13.4 Architecture Review

**FlowOps：** 建立完整技术架构。

**Gate 5：** 技术方案是否足以进入实施规划？

------------------------------------------------------------------------

# Stage 07 --- Planning

## 第 14 章：把项目拆成 AI 可以完成的工作

### 14.1 Roadmap

### 14.2 Epic

### 14.3 Feature

### 14.4 Story

### 14.5 Task

### 14.6 Subtask

### 14.7 Feature Spec

### 14.8 Task Spec

### 14.9 Dependency

### 14.10 Parallelization

### 14.11 Frontend / Backend Contract Coordination

### 14.12 Git Branch / Commit Strategy

**核心：**

``` text
Roadmap
 ↓
Epic
 ↓
Feature
 ↓
Story
 ↓
Task
 ↓
AI Session
 ↓
Commit
```

**FlowOps：** 拆解第一个可交付 Feature Slice。

**Artifact：** - `roadmap.md` - `features/*/spec.md` -
`features/*/tasks.md`

------------------------------------------------------------------------

# Stage 08 --- AI Coding

## 第 15 章：Coding Agent 标准工作循环

``` text
Explore → Plan → Implement → Test → Review → Fix → Verify
```

### 15.1 先读代码还是先写代码

### 15.2 Repository Exploration

### 15.3 Implementation Plan

### 15.4 Small Diff

### 15.5 Scope Control

### 15.6 Incremental Implementation

### 15.7 Self Test

### 15.8 Commit

## 第 16 章：前后端协同开发

### 16.1 API Contract

### 16.2 Mock

### 16.3 Parallel Development

### 16.4 Multi-repo

### 16.5 Workspace

### 16.6 Commit Isolation

## 第 17 章：AI Debugging

### 17.1 Evidence First

### 17.2 Reproduce

### 17.3 Hypothesis

### 17.4 Minimal Fix

### 17.5 Regression Test

### 17.6 Root Cause

## 第 18 章：Refactoring 与 Brownfield

### 18.1 Legacy Context

### 18.2 Behavior Preservation

### 18.3 Characterization Test

### 18.4 Incremental Refactor

### 18.5 Migration

**FlowOps：** 完成首批生产级功能。

------------------------------------------------------------------------

# Stage 09 --- Testing & Review

## 第 19 章：Verification Engineering

### 19.1 AI "完成"为什么不可信

### 19.2 Definition of Done

### 19.3 Verification Evidence

### 19.4 Build

### 19.5 Static Analysis

### 19.6 Unit Test

### 19.7 Integration Test

### 19.8 API Test

### 19.9 E2E

### 19.10 Visual Test

### 19.11 Security Test

### 19.12 Performance Test

## 第 20 章：Reviewer Agent

### 20.1 Builder 与 Reviewer 分离

### 20.2 Code Review

### 20.3 UI Review

### 20.4 Architecture Review

### 20.5 Requirement Review

### 20.6 Test Review

### 20.7 Review Severity

**Gate 6：** Feature 是否达到 Definition of Done？

------------------------------------------------------------------------

# Stage 10 --- DevOps

## 第 21 章：从代码到 Production

### 21.1 CI

### 21.2 Build

### 21.3 Test Gate

### 21.4 Container

### 21.5 Deployment

### 21.6 Database Migration

### 21.7 Configuration

### 21.8 Secrets

### 21.9 Observability

### 21.10 Rollback

### 21.11 Release Checklist

**FlowOps：** 发布 v1.0。

**Gate 7：** 是否允许 Production Release？

------------------------------------------------------------------------

# Stage 11 --- AI Features

## 第 22 章：从 AI Coding 到 AI Application

### 22.1 AI Feature Discovery

### 22.2 LLM API

### 22.3 Structured Output

### 22.4 RAG

### 22.5 Tool Calling

### 22.6 MCP

### 22.7 Agent

### 22.8 Human-in-the-loop

### 22.9 AI Permission

### 22.10 Evaluation

### 22.11 Cost / Latency / Safety

**FlowOps AI：** - AI 督办简报 - AI 周报 - AI 风险事项分析 - AI
自然语言查询 - AI 任务创建助手

------------------------------------------------------------------------

# Stage 12 --- Evolution

## 第 23 章：软件上线以后，Spec 如何继续活着

### 23.1 Feedback

### 23.2 Analytics

### 23.3 Bug

### 23.4 Requirement Change

### 23.5 Spec Update

### 23.6 Design Update

### 23.7 Architecture Evolution

### 23.8 Technical Debt

### 23.9 AI-assisted Maintenance

## 第 24 章：企业 AI Engineering Operating Model

### 24.1 Team Roles

### 24.2 Multi-Agent Workflow

### 24.3 Governance

### 24.4 Security Boundary

### 24.5 Model / Tool Independence

### 24.6 Metrics

### 24.7 Enterprise Adoption Roadmap

------------------------------------------------------------------------

# Appendices

## A. Prompt Library

## B. Template Library

## C. Checklist Library

## D. FlowOps Artifact Index

## E. Learning Hub

## F. Terminology

## G. Recommended Tools

## H. AI Coding Anti-patterns

## I. Project Starter Workspace

------------------------------------------------------------------------

# 全书最终验证标准

读者完成全书后，应该能够：

-   从模糊 Idea 开始进行 AI-assisted Discovery；
-   建立 PRD、业务规则和 Acceptance Criteria；
-   在没有 UI 灵感时系统地完成 Reference → Wireframe → Design System →
    UI；
-   建立可被 Coding Agent 消费的 Project Context；
-   使用架构、ADR、API Contract 和 Feature Spec 控制实现；
-   将 Feature 拆解为 AI 可安全执行的任务；
-   使用 Coding Agent 实现而不是让其自由发挥；
-   建立自动化 Verification Loop；
-   完成企业应用部署；
-   在已有系统中持续迭代 Spec；
-   将方法迁移到不同 AI Coding Agent，而不绑定单一厂商。
