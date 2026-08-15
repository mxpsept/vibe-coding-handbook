# 06 — First Slice Agent Handoff

到这里才进入 Coding Agent。

## Context Package

Agent 不需要读取整个项目讨论记录。提供：

```text
AGENTS.md
+ approved glossary/workflow/rules
+ architecture context
+ first vertical slice AC
+ relevant design/page spec
+ repository evidence
```

## First Session — Reconnaissance

```text
Read repository instructions and the approved first-slice artifacts.
Do not edit code yet.

Identify:
- existing application structure and conventions;
- owning modules/boundaries;
- auth/data-scope mechanism;
- persistence/API/UI patterns;
- test/build commands;
- contradictions or missing facts.

Return a proposed minimal implementation plan and SPEC_GAPs.
```

## Implementation Rule

如果仓库是空项目，Agent 可以提出 scaffold，但必须把：

```text
business decision
architecture decision
framework/setup choice
```

区分开。框架选择不能反向决定业务模型。

## Stop Conditions

- authentication/identity contract 无法确定；
- data scope 规则缺失；
- state transition 与 approved model 冲突；
- UI spec 不足以确定关键交互；
- Agent 认为必须增加重大 infrastructure；
- destructive migration；
- verification environment 不可用且无法证明核心 AC。

## Verification Matrix

| AC | Expected Evidence |
| --- | --- |
| AC1 publish | application/integration test |
| AC2 executor sees | permission/query integration |
| AC3 unrelated hidden | negative permission test |
| AC4 append progress | domain/application test |
| AC5 history preserved | persistence/integration test |
| AC6 supervisor reads | permission + API/UI evidence |
| AC7 stable errors | negative contract tests |

## Completion

Agent 必须返回：

```text
Summary
Files changed
AC → Evidence
Commands run
Not run / why
Known risks
SPEC_GAP
Suggested independent review focus
```

Human/Reviewer 接受 Evidence 后，第一 Slice 才算结束。
