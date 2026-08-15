# 01 — AI Engineering Metrics：衡量交付系统，而不是统计 AI 写了多少行

## 1. Wrong North Star

不建议把这些作为核心成功指标：

```text
AI-generated LOC
prompts per developer
tokens consumed
percentage of code written by AI
```

它们可以用于成本/使用分析，但不代表软件价值或质量。

## 2. Outcome Dimensions

### Flow
- lead time for change；
- cycle time；
- PR review time；
- deployment frequency。

### Quality
- escaped defects；
- change failure rate；
- rollback/hotfix；
- regression findings。

### Rework
- requirement clarification after implementation started；
- review rework；
- architecture drift correction；
- abandoned AI changes。

### Reliability
- SLO attainment；
- MTTR；
- incident frequency/severity。

### Context Health
- stale ADR/instructions findings；
- tasks blocked by missing Source of Truth；
- fresh-session handoff success。

## 3. Compare Carefully

AI adoption 前后比较必须考虑：
- project complexity；
- team composition；
- change size；
- release policy；
- measurement period。

不要因为一个 Sprint 更快就宣称生产力提升 300%。

## 4. Balanced Scorecard

推荐同时看：

```text
Speed
Quality
Reliability
Developer/Reviewer Load
Business Outcome
```

速度提升但返工和事故上升，不是成功。

## 5. Experiment

新 Agent Workflow 可以用有限范围试验：

```text
Hypothesis
Baseline
Intervention
Observation window
Metrics
Qualitative feedback
Decision
```

把 AI 工程实践本身也当作需要 Evidence 的产品。
