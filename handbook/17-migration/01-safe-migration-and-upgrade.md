# 01 — Migration & Upgrade：让 AI 帮你迁移，而不是豪赌一次切换

迁移任务的核心不是“新版本代码能运行”，而是兼容、数据、回滚和切换过程可控。

## Migration Packet

```text
Current State
Target State
Reason / Driver
Compatibility constraints
Inventory
Migration steps
Data migration
Dual-run/compatibility window
Cutover
Rollback
Observability
Verification
```

## 1. Inventory First

升级框架、数据库、API 或基础设施前，让 Agent 先列出：
- direct dependencies；
- deprecated APIs；
- configuration；
- plugins/drivers；
- build pipeline；
- runtime assumptions；
- data/schema compatibility；
- integration consumers。

## 2. Incremental Path

优先：

```text
Current
→ supported intermediate
→ target
```

而不是为了省步骤跨越多个不兼容大版本。

## 3. Expand / Migrate / Contract

数据库/API 常用模式：

```text
Expand: 新旧都能工作
Migrate: 数据/调用逐步迁移
Contract: 确认无旧消费者后删除旧结构
```

AI 很适合机械迁移，但“什么时候可以 Contract”必须基于 Evidence。

## 4. Data Safety

必须明确：
- backup/restore tested？
- migration idempotent？
- large table lock/time impact？
- partial failure behavior？
- validation counts/checksum/business invariants？

## 5. Cutover

上线计划至少包含：

```text
pre-check
change window
owner
commands/actions
health checks
business smoke test
rollback trigger
rollback action
post-check
```

## 6. AI Stop Conditions

- 官方兼容路径不明确；
- irreversible data operation 无 backup/rollback；
- consumer inventory 不完整；
- production config 与测试环境存在未知差异；
- migration duration 超出窗口但没有 rehearsal。

## 7. Verification

不要只验证启动成功。验证：
- critical business flows；
- data invariants；
- integrations；
- performance regression；
- logs/metrics/errors；
- rollback rehearsal where risk justifies it。
