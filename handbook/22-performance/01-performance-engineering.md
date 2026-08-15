# 01 — Performance Engineering：先建立预算，再让 AI 优化

“优化性能”不是一个可验证任务。性能工作必须从用户体验/系统目标转化成指标和 Evidence。

## 1. Performance Budget

示例维度：

```text
API p50 / p95 / p99 latency
throughput
error rate
DB query count/time
frontend LCP/interaction
memory/CPU
queue lag
batch duration
```

预算应来自真实业务目标和环境，不要让 Agent 随机定义“200ms 最佳实践”。

## 2. Workflow

```text
Define workload
→ Baseline
→ Profile/Measure
→ Identify bottleneck
→ Hypothesis
→ Minimal optimization
→ Re-measure
→ Regression guard
```

## 3. No Benchmark, No Claim

AI 可以提出优化候选，但不能因为：

```text
for-loop → stream
cache added
async added
SQL rewritten
```

就声称“性能提升”。必须比较相同 workload 下的 Evidence。

## 4. Common Enterprise Traps

- N+1 query；
- unbounded list/export；
- missing index / wrong index；
- large payload；
- repeated remote calls；
- cache without invalidation design；
- thread pool exhaustion；
- connection pool mismatch；
- frontend repeated requests；
- expensive render/table operations。

## 5. Cache Rule

加 Cache 前回答：
- correctness tolerance？
- key？
- TTL？
- invalidation？
- stampede？
- memory bound？
- stale data UX？

Cache 是数据一致性设计，不只是性能开关。

## 6. Load Test

至少记录：

```text
environment
build/version
scenario
concurrency/arrival rate
duration
data volume
warm-up
results
bottleneck evidence
```

否则不同 Agent/人生成的压测数字不可比较。

## 7. Performance Done

```text
measured baseline
+ measured improvement or budget compliance
+ correctness preserved
+ regression guard where valuable
```
