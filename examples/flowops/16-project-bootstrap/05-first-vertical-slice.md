# 05 — Selecting the First Vertical Slice

## Candidate Features

启动阶段可能想到：
- 登录/组织；
- 任务新增；
- 任务列表；
- 进度填报；
- 临期超期；
- 消息通知；
- Dashboard；
- 统计报表；
- 导入导出。

不要让 AI 按“后台系统常见模块”从基础 CRUD 横向铺开。

## Chosen Slice

**Create/Publish Item → Executor sees it → Executor submits Progress Update → Supervisor sees latest progress.**

为什么选它：
- 贯穿最核心角色；
- 验证 Item、assignment、permission、progress history；
- 有真实 UI/API/domain/data interaction；
- 不依赖复杂通知和统计；
- 后续 Attention/Closure 可以自然叠加。

## Slice Boundary

### Included
- minimal authenticated actor fixture/integration；
- create/publish Item；
- assigned executor list/detail；
- progress update；
- supervisor read latest/history；
- authorization；
- tests。

### Excluded
- external messaging；
- dashboard charts；
- completion/closure；
- escalation severity；
- bulk import/export；
- mobile native client。

## Acceptance Criteria

```text
AC1 authorized creator can publish a valid item with owner and dueAt.
AC2 assigned executor can see the active item.
AC3 unrelated executor cannot see it through executor scope.
AC4 assigned executor can append a progress update.
AC5 progress update is historical evidence; previous update is not overwritten.
AC6 authorized supervisor can see latest progress and history.
AC7 invalid state/scope/action returns stable business error semantics.
```

## Architecture Needed Now

只需要支持这个 Slice 的边界：

```text
Item
Progress
Authorization/Data Scope
API/Application
Persistence
Web UI
```

不因为“以后可能需要”提前引入 Kafka、Workflow Engine、Search Cluster 或复杂微服务拆分。

## Gate

当团队能清楚回答“这个 Slice 的 AC 如何被自动/人工 Evidence 证明”时，才进入 Agent Implementation Packet。
