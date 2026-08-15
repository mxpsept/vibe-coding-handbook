# 01 — AI Refactoring：重构代码，不重构业务事实

AI 非常擅长大规模机械修改，也因此特别容易把“重构”扩大成行为变化。

## 1. Refactoring Contract

任何重构先定义：

```text
Behavior to preserve
Problem to improve
Boundary
Non-goals
Verification
Rollback
```

如果无法描述 Behavior to preserve，先补 Characterization Tests。

## 2. Trigger

好的 Trigger：
- duplicated stable logic；
- dependency boundary violation；
- change amplification；
- testability blocker；
- measured performance problem；
- obsolete abstraction after repeated evidence。

差的 Trigger：

```text
“AI 觉得这个写法不够优雅”
```

## 3. Refactoring Workflow

```text
Evidence
→ Characterize behavior
→ Define target shape
→ Small transformation
→ Verify
→ Repeat
```

不要一次同时做：目录迁移 + 框架升级 + API 修改 + 数据迁移。

## 4. Architecture Refactor

跨模块重构必须说明：
- 当前依赖问题；
- 目标依赖方向；
- ADR 是否需要更新；
- migration sequence；
- compatibility window。

## 5. AI Review Questions

- 是否改变 public contract？
- 是否改变 exception/error semantics？
- 是否改变 transaction boundary？
- 是否改变 permission behavior？
- 是否改变 serialization/data shape？
- 是否删除看似无用但具有兼容意义的代码？

## 6. Example

问题：三个模块各自计算 deadline attention。

不要直接创建 `CommonUtils.calculateStatus()`。

先确认这是同一业务语义，并确定 Owner。若 Attention module 是规则 Owner，则其他模块通过公开 contract 使用，而不是把 domain rule 降级成 global utility。

## 7. Done

Refactor 完成必须能证明：

```text
same required behavior
+ improved stated quality
+ no unintended scope
```
