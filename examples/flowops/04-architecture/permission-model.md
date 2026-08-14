# FlowOps — Permission Model v0.1

Authorization = `Actor + Capability + Resource Scope + Current Business State`.

Candidate capabilities: `ITEM_READ`, `ITEM_CREATE`, `ITEM_EDIT`, `PROGRESS_UPDATE`, `COMPLETION_CLAIM`, `ITEM_CLOSE`, `ATTENTION_REVIEW`, `MANAGEMENT_REVIEW`, `AUDIT_READ`.

Scope may include own assigned items, department items, or organization supervision scope. Queries enforce scope before returning protected data.

A capability does not bypass lifecycle rules. Frontend capability checks are UX; backend repeats the authoritative decision.

Maintain a permission test matrix covering actor × scope × lifecycle × action, including negative cases.