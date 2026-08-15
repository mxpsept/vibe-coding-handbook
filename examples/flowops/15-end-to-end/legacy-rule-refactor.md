# FlowOps Brownfield Case — Legacy Deadline Rule Refactor

## Problem

随着系统演进，Deadline/Overdue 判断分别出现在：
- backend list query；
- detail service；
- frontend table formatter；
- scheduled report。

出现同一 Item 在不同页面显示不同状态的问题。

## Wrong AI Task

```text
帮我把所有日期判断代码重构一下，统一封装。
```

风险：Agent 可能把不同业务语义误认为重复代码，并创建 `DateUtils` 掩盖 Domain ownership。

## Refactoring Contract

### Preserve
已批准的 lifecycle、attention、reporting semantics。

### Improve
Deadline-derived rule 只有一个明确 Owner，其他模块通过稳定 contract 消费。

### Non-goals
- 改变阈值；
- 重做页面；
- 替换日期库；
- 改数据库 timezone strategy。

## Characterization

先收集现有测试和真实行为，建立 cases：

```text
before due
exactly due
one second after due
closed before due
closed after due
missing dueAt if allowed
timezone boundary
```

如果不同实现结果冲突，不选择“出现次数最多的行为”为正确答案；回到 Business Rule Source of Truth。

## Target Architecture

```text
Item facts + Clock
→ Attention/Deadline Policy (owner)
→ typed result
→ API/report/UI consumers
```

## Migration Sequence

1. 建立/强化 policy tests；
2. 引入 owner implementation；
3. 一个 consumer 一个 consumer 地迁移；
4. 每步运行 characterization/regression；
5. 删除确认无引用的 duplicate logic；
6. 更新 architecture/context artifact。

## Reviewer Checks

- transaction/query behavior 是否意外改变；
- DB-side filtering 与 in-memory rule 是否语义一致；
- timezone 是否改变；
- report historical semantics 是否与 live attention 真的是同一规则；
- frontend 是否仍保留第二套 fallback calculation。

## Done

不是“代码减少 200 行”，而是：

```text
approved behavior preserved
+ one explicit rule owner
+ consumers migrated
+ tests protect boundary semantics
+ no hidden duplicate rule remains
```
