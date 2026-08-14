# Codex Frontend Implementation Prompt

```text
You are implementing an approved enterprise UI specification.
Your task is implementation, not product redesign.

GOAL
Implement: <Page / Feature>

READ FIRST — source of truth
1. <business-rules.md>
2. <state-model.md>
3. <acceptance-criteria.md>
4. <page-spec.md>
5. <design-system.md>
6. <ui-state-matrix.md>
7. relevant existing frontend architecture/components

BEFORE CODING
- inspect the repository and identify existing layout, tokens, shared components, API patterns and tests;
- summarize the intended implementation plan;
- report any contradiction or missing blocking contract;
- do not start by replacing existing architecture with a new framework/pattern.

IMPLEMENT
- approved layout and hierarchy;
- approved interactions;
- lifecycle and attention semantics;
- applicable loading/empty/error/read-only/pending states;
- responsive behavior;
- accessibility basics;
- reusable semantic components where repetition is stable.

REUSE
Prefer existing:
- design tokens;
- PageHeader / FilterBar / EmptyState patterns;
- LifecycleBadge / AttentionIndicator;
- form and validation infrastructure;
- API/query/state conventions.

DO NOT
- invent business actions;
- invent metrics or risk scores;
- merge Lifecycle and Attention;
- auto-close a Completion Claim;
- add arbitrary colors/spacing/radius/shadows;
- create a page-local design system;
- hide backend authorization gaps with frontend-only checks;
- refactor unrelated code;
- change API semantics merely to simplify the UI.

STOP CONDITIONS
Stop and report before implementation if:
- Page Spec conflicts with Business Rules / AC;
- required permission semantics are unknown;
- API cannot represent an approved state;
- a blocking DESIGN_SPEC_GAP exists;
- implementing the UI would require inventing domain behavior.

VERIFY
Run the repository's relevant:
- lint/typecheck;
- unit/component tests;
- build;
- targeted UI tests if available.

Then manually reason through:
- normal data;
- no data/no result where applicable;
- API error;
- long title/content;
- multiple attention flags;
- read-only/forbidden actions;
- pending submission;
- terminal lifecycle;
- narrow viewport where supported.

FINAL RESPONSE
1. What changed
2. Files changed
3. Requirement/Page Spec trace
4. Verification performed + results
5. UI states covered
6. Remaining gaps / assumptions
7. Screenshots or visual QA notes if tooling supports them

Do not commit unless explicitly requested.
```

## Why this prompt exists

Codex should have freedom in implementation details, but not freedom to silently redefine the product.
