# Gate 3 — Product Design → Frontend Readiness

## Product Intent
- [ ] 每个核心页面有 Primary Actor
- [ ] 每个核心页面有一个明确 Primary Job
- [ ] 页面不是为了“功能完整”堆模块

## IA / Navigation
- [ ] Navigation 围绕业务对象与用户任务
- [ ] 没有数据库表直接泄漏成菜单
- [ ] 没有每个状态/动作一个菜单
- [ ] Item Detail 等上下文页面位置合理

## User Flow
- [ ] Critical Flow 已定义
- [ ] 高频任务无重复寻找对象
- [ ] 无意义页面跳转已消除
- [ ] Failure / cancel / permission path 已考虑

## Page Specification
- [ ] Information Priority 明确
- [ ] Layout Contract 明确
- [ ] Component hierarchy 明确
- [ ] Actions 有 Actor + Preconditions
- [ ] Permission source 明确

## Business Integrity
- [ ] Lifecycle 与 Attention 未混合
- [ ] Completion Claim 与 Closure 未混合
- [ ] UI 未发明 Business Rule
- [ ] DESIGN_SPEC_GAP 已返回 Product/Requirements

## Design System
- [ ] Visual Direction 已批准
- [ ] Semantic Tokens 可用
- [ ] Typography / spacing / radius 受约束
- [ ] Status / Attention Pattern 一致
- [ ] 没有 Page-local Design System

## UI States
- [ ] Loading
- [ ] Empty / No Result
- [ ] Error
- [ ] Unauthorized / Read-only
- [ ] Pending / Success
- [ ] Conflict where relevant
- [ ] Long Content
- [ ] Large Data
- [ ] Terminal lifecycle

## Responsive / Accessibility
- [ ] Responsive 基于 Job，而非只缩放
- [ ] 不只靠颜色表达状态
- [ ] Focus / keyboard considerations captured
- [ ] Key information not tooltip-only

## Frontend Handoff
- [ ] Requirement / Rule / AC 可追踪
- [ ] Coding Agent read-list 已定义
- [ ] Forbidden assumptions 已定义
- [ ] Stop conditions 已定义
- [ ] Blocking gaps = 0

## Decision
- [ ] PASS — Ready for Frontend Architecture / Implementation
- [ ] PASS WITH GAPS — only non-blocking gaps
- [ ] HOLD
- [ ] RETURN TO REQUIREMENTS

### Blocking gaps
- 

### Non-blocking gaps
- 

### Human reviewers
- Product:
- UX:
- Engineering:
- Business when semantics changed:

### Decision note
- 
