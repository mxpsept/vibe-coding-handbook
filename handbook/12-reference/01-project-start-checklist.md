# 新项目启动 Checklist — 从 Idea 到第一个 Codex Task

当你准备开发一个新系统但还不知道从哪里开始时，按此清单执行。

## Phase A — Intent
- [ ] 用一句话描述系统解决的问题
- [ ] 明确目标用户/Actor
- [ ] 写出成功意味着什么
- [ ] 列出明确不做什么
- [ ] 记录业务术语而不是先设计数据库表

## Phase B — Discovery
- [ ] Stakeholder / Actor Map
- [ ] Current workflow
- [ ] Pain points
- [ ] Constraints
- [ ] Unknowns
- [ ] Assumption register
- [ ] Evidence / source links

## Phase C — Requirements
- [ ] User Stories / Jobs
- [ ] Acceptance Criteria
- [ ] Business Rules
- [ ] State Model
- [ ] Permission semantics
- [ ] Edge cases
- [ ] Open SPEC_GAP

## Phase D — Product Design
- [ ] Page inventory
- [ ] Critical user flows
- [ ] Design reference research
- [ ] 2–3 wireframe alternatives for critical pages
- [ ] Human design decision
- [ ] Visual direction
- [ ] Design System
- [ ] UI State Matrix
- [ ] Page Specs
- [ ] UX review

## Phase E — Architecture
- [ ] Quality attributes
- [ ] System context
- [ ] Module boundaries
- [ ] Domain model
- [ ] Data model
- [ ] API contract
- [ ] Permission model
- [ ] Error model
- [ ] Security / observability / deployment
- [ ] ADRs for important choices
- [ ] Architecture review

## Phase F — First Implementation Packet

选择一个 Vertical Slice，而不是“先把所有基础代码搭完”。

推荐 Slice 应能贯穿：

```text
UI
→ API
→ Application
→ Domain
→ Persistence
→ Test
```

Packet 必须包含：
- Goal；
- Read First；
- Scope；
- Acceptance Criteria；
- Architecture constraints；
- UI states；
- Do Not；
- Stop Conditions；
- Verification commands。

## Phase G — Codex

Codex 开始前必须：
- [ ] inspect repository
- [ ] read Source of Truth
- [ ] explain implementation plan
- [ ] identify reuse points
- [ ] report contradictions

Codex 完成前必须：
- [ ] lint/typecheck
- [ ] tests
- [ ] build
- [ ] critical rule verification
- [ ] summarize changed files
- [ ] list remaining assumptions/gaps

## Golden Rule

```text
If you cannot explain what “done” means,
do not ask AI to implement it yet.
```
