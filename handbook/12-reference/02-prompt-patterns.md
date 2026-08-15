# Prompt Patterns — 不依赖某个模型的 AI 软件工程任务结构

> Prompt 是执行接口，不是 Project Truth。真正稳定的信息应存在 Artifact 中。

## Pattern 1 — Research

```text
ROLE
GOAL
KNOWN CONTEXT
QUESTIONS TO ANSWER
SOURCES / ARTIFACTS
DO NOT ASSUME
OUTPUT FORMAT
GAPS TO REPORT
```

适用：Discovery、技术调研、Design Research。

## Pattern 2 — Generate Alternatives

```text
GOAL
CONSTRAINTS
SOURCE OF TRUTH
GENERATE 3 MEANINGFULLY DIFFERENT OPTIONS
FOR EACH: rationale / strengths / weaknesses / risks
COMPARE
RECOMMEND
WAIT FOR HUMAN DECISION when decision is material
```

适用：UX、Architecture、技术方案。

## Pattern 3 — Specification

```text
INPUT ARTIFACTS
CONVERT TO <SPEC TYPE>
TRACE EVERY IMPORTANT RULE
DO NOT INVENT MISSING SEMANTICS
OUTPUT GAPS
READINESS STATUS
```

适用：Page Spec、API Spec、Implementation Packet。

## Pattern 4 — Implementation

```text
GOAL
READ FIRST
INSPECT REPOSITORY
PLAN
IMPLEMENT
REUSE
DO NOT
STOP CONDITIONS
VERIFY
FINAL REPORT
```

适用：Codex/Claude Code/Cursor Agent。

## Pattern 5 — Reviewer

```text
ROLE: skeptical reviewer
SOURCE OF TRUTH
REVIEW DIMENSIONS
FINDINGS WITH SEVERITY
NO SILENT FIXING OF UNKNOWN REQUIREMENTS
FINAL: PASS / PASS_WITH_GAPS / HOLD / RETURN
```

Reviewer 与 Generator 的职责应分离。

## Pattern 6 — Debug

```text
OBSERVED BEHAVIOR
EXPECTED BEHAVIOR
REPRODUCTION
ENVIRONMENT
RECENT CHANGES
EVIDENCE / LOGS
FORM HYPOTHESES
RANK BY EVIDENCE
RUN MINIMAL DIAGNOSTICS
FIX ROOT CAUSE
ADD REGRESSION TEST
```

禁止从错误信息直接跳到大规模重构。

## Pattern 7 — Refactor

```text
BEHAVIOR TO PRESERVE
PROBLEM TO IMPROVE
BOUNDARY
NON-GOALS
CHARACTERIZATION TESTS
SMALL STEPS
VERIFY AFTER EACH LOGICAL CHANGE
```

AI Refactor 最危险的问题是顺手改变业务行为，因此“Behavior to preserve”必须显式存在。

## Pattern 8 — Migration

```text
CURRENT STATE
TARGET STATE
COMPATIBILITY WINDOW
DATA MIGRATION
ROLLBACK
OBSERVABILITY
CUTOVER
VERIFICATION
```

适用数据库、API、框架、基础设施升级。

## Prompt Smells

```text
“帮我优化一下”
“按照最佳实践重构”
“做得高级一点”
“把这个系统完善一下”
“你看着办”
```

这些不是不能使用，而是它们必须有足够 Artifact Context 才安全。

## Model Independence

不要让工程体系绑定某个模型专有措辞。理想情况下，同一个 Implementation Packet 可以被不同 Coding Agent 消费，并产生语义一致的结果。
