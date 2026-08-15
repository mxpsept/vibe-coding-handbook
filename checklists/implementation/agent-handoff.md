# Agent Handoff Checklist

在把任务交给新的 Coding Agent / 新会话前检查：

## Truth
- [ ] Goal 明确
- [ ] Acceptance Criteria 明确
- [ ] Source of Truth 路径明确
- [ ] Artifact 冲突优先级明确

## Repository
- [ ] Owning module 已知
- [ ] 相关 existing pattern 已定位
- [ ] build/test commands 可执行
- [ ] generated / do-not-edit 文件已说明

## Boundaries
- [ ] Scope / Non-goals 明确
- [ ] Architecture constraints 明确
- [ ] Dependency policy 明确
- [ ] Security/permission semantics 明确

## Autonomy
- [ ] Agent autonomy level 合适
- [ ] Stop Conditions 明确
- [ ] 是否允许 commit/push/release 已明确

## Verification
- [ ] Normal path
- [ ] Failure/edge state
- [ ] Regression scope
- [ ] Required automated checks

## Fresh Session Test

如果新 Agent 必须依赖“你应该记得我们之前聊过”才能完成任务，则 Handoff 未准备好。
