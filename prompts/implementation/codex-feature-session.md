# Codex Feature Session Prompt Pack

不要把以下 Prompt 当魔法咒语。真正重要的是它引用的 Artifact 和 Stop Condition。

## 1. Reconnaissance

```text
Read AGENTS.md and the Feature Implementation Packet first.
Do not edit code yet.

Explore the repository and report:
1. likely owning modules/files;
2. existing similar implementations;
3. architecture/conventions that constrain the change;
4. test/build commands;
5. reusable components/clients/utilities;
6. contradictions or SPEC_GAPs.

Do not propose a new abstraction until you have searched for an existing one.
```

## 2. Plan

```text
Using only approved requirements and repository evidence, produce a bounded implementation plan.
For each step include:
- files/modules likely affected;
- behavior added/changed;
- tests/evidence;
- risk.

Explicitly list Non-goals and Stop Conditions.
Do not implement yet.
```

## 3. Implement

```text
Implement the approved plan as the smallest coherent change.
Preserve unrelated behavior.
Do not expand scope for cleanup/refactoring unless required for correctness.
If a Stop Condition occurs, stop that part and report it instead of guessing.
```

## 4. Verify

```text
Verify the implementation against every Acceptance Criterion.
Run the repository's real relevant test/build/lint/typecheck commands.
Test negative, permission, state and boundary paths where applicable.
Return an AC → Evidence matrix.
Clearly separate PASSED, NOT RUN, FAILED and BLOCKED.
```

## 5. Review

Prefer a fresh context/agent when possible:

```text
Review this change as an independent senior engineer.
Do not assume the implementation is correct because another agent produced it.
Read the Feature Spec and diff.
Prioritize:
- business-rule mismatch;
- permission/security defects;
- state/time boundary bugs;
- architecture violations;
- missing negative tests;
- accidental scope expansion;
- performance/integration risks.

Report findings by severity with concrete file/behavior evidence.
```

## 6. Fix

```text
Address only validated review findings.
For each finding state the root cause and verification added/run.
Do not use the review as permission for unrelated refactoring.
```

## 7. Final Completion

```text
Return:
Summary
Files changed
AC → Evidence
Commands run
Known gaps
SPEC_GAP
Review focus

Do not say "complete" when required verification was not run.
```
