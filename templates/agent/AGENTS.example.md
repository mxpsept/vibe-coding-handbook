# AGENTS.md — Repository Instructions Example

> Copy and adapt. Keep this file short enough that agents actually use it; link to deeper artifacts instead of duplicating them.

## Mission
Build and maintain this repository without silently redefining product behavior or architecture.

## Source of Truth
Read in this order when relevant:
1. approved requirements/business rules;
2. accepted ADRs/architecture docs;
3. approved design/API specs;
4. task packet;
5. existing code/tests as implementation evidence.

If these conflict, stop and report the conflict.

## Repository Map
```text
<frontend path>  — ...
<backend path>   — ...
<docs path>      — ...
```

## Commands
```bash
# install
...
# lint/typecheck
...
# test
...
# build
...
```

Do not claim verification you did not run.

## Architecture Guardrails
- Respect module ownership and dependency direction.
- Do not import another module's internal persistence implementation.
- Do not create a new global abstraction to solve a local problem without evidence.
- New framework/library categories require architecture review.
- Prefer existing project conventions over agent preference.

## Product Guardrails
- Do not invent missing business semantics.
- Backend authorization is source of truth.
- Preserve approved lifecycle/state semantics.
- UI must use approved design tokens/patterns.

## Change Discipline
Before coding:
1. inspect relevant existing implementation;
2. identify owning module;
3. state plan and reuse points;
4. identify blocking gaps.

During coding:
- keep changes task-scoped;
- avoid unrelated refactors;
- add/update tests with behavior changes.

## Stop Conditions
Stop and report when:
- requirement/architecture conflict exists;
- destructive migration appears unexpectedly;
- public API must change outside scope;
- new infrastructure/framework is required;
- permission/security semantics are unknown;
- baseline has unrelated failures that prevent trustworthy verification.

## Final Report
Return:
1. summary;
2. files changed;
3. trace to requirement/spec;
4. verification commands + results;
5. assumptions/gaps;
6. intentionally deferred debt.

## Git
Do not commit, push, merge, release, or mutate production unless the task explicitly grants that action.
