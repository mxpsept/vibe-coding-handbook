# AGENTS.md — Example

## Mission

This repository contains an enterprise application. Preserve approved business behavior and existing architecture unless the task explicitly changes them.

## Read Before Editing

1. Feature-specific spec/implementation packet named in the task.
2. `docs/architecture/architecture-context.md`.
3. Relevant existing module and tests.

## Repository Reconnaissance

Before implementation:
- locate the owning module;
- find similar existing features;
- identify test/build commands;
- identify shared clients/components/utilities;
- report contradictions between task and repository evidence.

Do not create a parallel pattern before checking for an existing one.

## Business Rules

Never invent:
- state transitions;
- permission scope;
- thresholds/deadlines;
- money/time rounding;
- notification recipients;
- external-provider behavior.

If required information is absent, report `SPEC_GAP` and stop the affected part.

## Architecture

- Respect module ownership and dependency direction.
- UI must not become the source of truth for authorization or domain rules.
- Provider-specific DTOs stay inside adapters/integration boundaries.
- Avoid new infrastructure/dependencies unless explicitly approved.

## Scope

Make the smallest coherent change that satisfies the approved Feature Spec.

Do not opportunistically refactor unrelated code.

## Verification

Before claiming completion:
- run relevant tests;
- run build/typecheck/lint required by this repository;
- verify negative and permission paths when applicable;
- map evidence to Acceptance Criteria;
- report tests not run and why.

## Git Safety

Do not:
- force push;
- rewrite shared history;
- delete unrelated files;
- commit secrets;
- include unrelated working-tree changes.

## Completion Report

Return:

```text
Summary
Files changed
Behavior implemented
Verification performed
Known gaps / risks
SPEC_GAP (if any)
Suggested review focus
```
