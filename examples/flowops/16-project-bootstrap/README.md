# FlowOps Project Bootstrap — 从一句话到第一个 Agent-ready Slice

本案例完整模拟一个企业督办系统从“只有想法”到“可以安全交给 Coding Agent 开发”的过程。

## Raw Idea

> 做一套企业重点任务督办系统，让管理人员看到任务执行情况，责任人填报进度，系统能够识别临期和超期事项。

这句话足以开始 Discovery，但不足以开始 Production Coding。

## Bootstrap Sequence

```text
00 Raw Idea
↓
01 Discovery Log
↓
02 Glossary
↓
03 Critical Workflow
↓
04 Business Rules
↓
05 State & Permission
↓
06 UI Design Direction
↓
07 First Vertical Slice
↓
08 Agent Handoff
```

## What This Case Teaches

重点观察每一步如何减少 Agent 的自由猜测空间：

- Discovery 不把假设包装成事实；
- Glossary 解决同一个词多人理解不同；
- Workflow 先确定业务闭环，再列菜单；
- Rule / State / Permission 在写 CRUD 前明确；
- UI 先做信息层级和页面状态，再让前端 Agent 编码；
- Architecture 只为当前关键 Driver 做决定；
- 第一个 Slice 必须能端到端验证业务价值；
- Agent 收到的是批准后的 Artifact，而不是完整聊天记录。

## Recommended Reading

把本目录与 `starter-kits/enterprise-project/` 对照阅读：前者展示“填完是什么样”，后者提供“你自己的项目怎么开始”。
