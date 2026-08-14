# End-to-End Vibe Coding Playbook

`Idea → Discovery → Requirements → Product Design → Architecture → Implementation → Testing → Delivery → Operations → Evolution`.

At each stage: `Source of Truth → AI Draft/Implementation → Specialist Review → Human Decision for material ambiguity → Gate → Next Stage`.

## Golden Rules
1. AI autonomy belongs inside explicit boundaries.
2. UI cannot invent business rules.
3. Code is not the only specification.
4. Prefer small vertical slices/reviewable diffs.
5. Architecture decisions need Drivers/ADRs.
6. Server is security source of truth.
7. Tests prove contracts, not just code paths.
8. Production evidence feeds Requirements/Architecture back.
9. Stop conditions are a feature.
10. Repository context must be readable by a fresh human or agent.

Success is not “AI wrote most lines”; it is shipping correct software faster while retaining understandable decisions, coherent architecture, test evidence and operational control.