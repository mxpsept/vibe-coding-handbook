# Project Bootstrap Session Prompt

用于项目第一轮，不用于直接生成代码。

```text
Act as a product discovery + software engineering facilitator.
We are bootstrapping an enterprise software project.

Your goal is NOT to design the entire system or write code.
Your goal is to turn the raw idea into a reviewable Project Bootstrap Packet.

For every statement, distinguish:
- FACT: supported by user/evidence;
- ASSUMPTION: plausible but unconfirmed;
- UNKNOWN: must be resolved;
- DECISION: explicitly approved.

Work through:
1. Problem and actors
2. Desired outcomes
3. Non-goals
4. Existing workflow/evidence
5. Domain glossary
6. Critical workflows
7. Business/state/permission unknowns
8. UI/design questions
9. Architecture/integration constraints
10. Candidate first vertical slice

Do not invent organization rules, permissions, deadlines, thresholds or external-system behavior.

Output:
- Product Brief draft
- Discovery questions grouped by priority
- Fact/Assumption/Unknown table
- Candidate critical workflow
- Candidate first vertical slice
- Risks
- Artifacts that should be created next

Stop before implementation.
```

## 第二轮：收敛

```text
Using the approved answers from discovery, update the Bootstrap Packet.
Remove assumptions that have become decisions.
Keep unresolved UNKNOWNs explicit.
Recommend which unknowns block the first vertical slice and which can be deferred.
Do not expand scope.
```

## 第三轮：进入设计/架构

只有 Blocking Unknowns 足够收敛后，再分别进入 Product/UI Design 和 Architecture，不建议一个 Prompt 同时生成最终 UI、数据库、接口和全部代码。
