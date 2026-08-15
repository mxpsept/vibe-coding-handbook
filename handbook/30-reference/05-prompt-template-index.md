# Prompt / Template / Checklist Index

当你知道“我要做什么”，但不知道该用哪个资产时，从这里找。

## Discovery / Requirements

用途：从模糊想法形成 Evidence、Requirement、Rule、AC。

查找：
```text
prompts/discovery/
prompts/requirements/
templates/requirements/
checklists/requirements/
```

## Product / UI

用途：研究参考、生成 Wireframe alternatives、建立 Design System、Page Spec、UX Review。

查找：
```text
prompts/product-design/
templates/design/
checklists/design/
```

## Architecture

用途：Architecture Drivers、模块边界、ADR、API/Data/Permission/Error。

查找：
```text
prompts/architecture/
templates/architecture/
checklists/architecture/
```

## Coding Agent Implementation

用途：把 Feature 交给 Codex/其他 Coding Agent。

查找：
```text
prompts/implementation/
templates/implementation/implementation-packet.template.md
checklists/implementation/feature-done.md
```

存量修改：
```text
templates/implementation/brownfield-change-packet.template.md
checklists/implementation/agent-handoff.md
```

仓库级规则：
```text
templates/agent/AGENTS.example.md
```

## Testing / Review

```text
prompts/testing/
checklists/testing/
handbook/19-code-review/
```

## Release / Operations

```text
checklists/release/production-readiness.md
templates/operations/runbook.template.md
templates/operations/incident-context.template.md
```

## Governance

```text
templates/governance/ai-project-policy.template.md
handbook/28-governance/
handbook/29-maturity/
```

## Selection Rule

不要为了“使用模板”填满所有模板。选择 Artifact 的标准是：

> 如果这个决定丢失、漂移或被 Agent 猜错，会不会造成明显返工或风险？

如果答案是会，就值得显式化。
