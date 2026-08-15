# 01 — Data Engineering：AI 修改代码容易，修改数据必须更谨慎

数据通常比应用实例寿命更长。AI-assisted change 必须把 Schema、Migration、Quality、Lineage 和 Recovery 当作一等公民。

## 1. Data Contract

重要数据集/接口明确：
- owner；
- semantic definition；
- schema；
- nullable/default；
- units/timezone；
- freshness；
- retention；
- sensitivity；
- consumers。

同名字段不保证同一语义。

## 2. Schema Change

优先 backward-compatible：

```text
add/expand
→ deploy compatible readers/writers
→ migrate/backfill
→ verify consumers
→ contract/remove
```

不要让 Agent 一次提交 `rename column + application switch + delete old`，除非停机/兼容条件明确允许。

## 3. Migration Evidence

必须记录：
- row/data volume；
- estimated duration；
- lock/IO impact；
- idempotency；
- checkpoint/resume；
- validation query；
- rollback/recovery。

## 4. Data Quality

除了 schema validation，还要验证业务 invariant，例如：

```text
closed_at must exist when lifecycle=CLOSED
completion_claim_at does not imply closed_at
```

## 5. Backfill

AI 生成 Backfill Script 前先定义：

```text
selection criteria
batch size
rate limit
restartability
dry-run
progress metric
error handling
validation
```

生产执行权限与写脚本权限分离。

## 6. Analytics / AI Use

生产业务数据进入分析或 AI 系统前确认：
- permitted purpose；
- minimization；
- masking/anonymization where required；
- retention；
- access scope。

## 7. Data Incident

发现错误写入时优先：

```text
stop further corruption
→ preserve evidence
→ quantify affected data
→ choose repair strategy
→ verify business invariants
```

不要先执行未经验证的大范围 UPDATE。
