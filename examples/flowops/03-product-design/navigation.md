# FlowOps — Navigation Model v0.1

## 1. Navigation Goals

Navigation 应帮助用户回答：

```text
我现在应该去哪里？
我正在处理什么上下文？
下一步动作在哪里？
```

而不是展示系统拥有多少模块。

## 2. Proposed Desktop Navigation

```text
FlowOps
├── 工作台                 /workbench
├── 我的工作               /my-work
├── 督办事项
│   ├── 全部事项           /items
│   └── 重点关注           /attention
├── 管理视图               /management-review
└── 系统设置               /settings
```

Permission-based entry candidate:

```text
待办结审核               /closure-review
```

是否放入“督办事项”或“我的工作”需要在 Closure Authority 明确后验证。

## 3. Why this structure

### 工作台

不是“所有模块缩略图”，而是角色化入口。

### 我的工作

面向执行者的任务入口，降低从“全部事项”中过滤自己的成本。

### 督办事项

围绕核心业务对象组织，而不是按 CRUD 动作拆菜单。

### 重点关注

因为 Supervision Specialist 存在独立高频 Attention Job，所以提供工作入口；但 `OVERDUE`、`NEAR_DUE`、`STALE_UPDATE` 不分别成为菜单。

### 管理视图

服务 Manager 的独立决策场景，不等于统计中心。

## 4. Rejected Navigation

```text
首页
任务管理
任务新增
任务进度管理
临期管理
超期管理
办结管理
统计分析
日志管理
```

Rejected because:
- action-as-menu；
- state-as-menu；
- attention-as-module；
- object context fragmentation；
- role/job 不清晰。

## 5. Global Utilities

建议放在 Global Header / Utility Area：

```text
Global Search (future candidate)
Notification (future)
Help
User/Profile
```

不占一级业务导航。

## 6. Context Navigation — Item Detail

进入 Item Detail 后可采用页面内 Section Navigation：

```text
Overview
Progress
Supporting Information
Audit
```

但应优先测试单页渐进披露是否足够，不要为了“看起来完整”默认做多个 Tab。

## 7. Navigation Permission Principle

```text
Navigation visibility != Authorization
```

隐藏菜单只是 UX；真实权限仍由服务端执行。

## 8. Naming Rules

菜单名优先：
- 用户熟悉的业务语言；
- 名词/工作空间；
- 简短稳定。

避免：
- 技术术语；
- 数据表名；
- `xxx管理` 泛滥；
- 同义词混用。
