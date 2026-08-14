# FlowOps — Use Cases v0.1

> Synthetic Teaching Case。Use Case 用于描述跨角色完整业务交互，不替代 Business Rule 与 Acceptance Criteria。

## UC-001 — Issue Supervision Item

**Primary Actor:** Authorized Issuer  
**Goal:** 将准备完成的事项正式进入督办执行生命周期。  
**Preconditions:** Item is `DRAFT`。

### Main Flow
1. Actor 打开 Draft Item。
2. 系统展示当前来源、事项要求、Accountable Department、Effective Due Date。
3. Actor 执行 Issue。
4. 系统校验 BR-002、BR-003。
5. 系统将 Lifecycle 从 `DRAFT` 转换为 `ISSUED`。
6. 系统记录 Issue Actor / Timestamp / Audit Event。

### Alternatives
- A1: Accountable Department 缺失 → 拒绝 Issue。
- A2: Effective Due Date 缺失 → 拒绝 Issue。
- A3: Actor 无权限 → 拒绝操作且不得修改数据。

### SPEC_GAP
Authorized Issuer 的具体角色尚未定义。

---

## UC-002 — Submit Progress Update

**Primary Actor:** Authorized Responsible Participant  
**Goal:** 追加一次真实执行进展而不覆盖历史。  
**Preconditions:** Item is `IN_PROGRESS`。

### Main Flow
1. Actor 查看事项及历史进度。
2. Actor 输入本次 Progress Update。
3. 系统校验内容和权限。
4. 系统追加 Progress Record。
5. 系统刷新 Last Progress Update Time。
6. 系统记录 Audit Event。
7. 系统重新评估相关 Attention Flags。

### Alternatives
- A1: Item is terminal → reject。
- A2: Empty/invalid content → reject。
- A3: Unauthorized actor → deny。

### Invariant
不得修改已有 Progress Record 以模拟“新增进度”。

---

## UC-003 — Review Attention Items

**Primary Actor:** Supervision Specialist  
**Goal:** 在管理会议或日常督办前识别需要核验的事项。

### Main Flow
1. Actor 打开 Attention View。
2. 系统返回 Actor 数据权限范围内的事项。
3. 每个事项分别计算/展示适用 Attention Flags。
4. Actor 可按 `STALE_UPDATE`、`NEAR_DUE`、`OVERDUE` 等筛选。
5. Actor 打开事项查看 Progress History、期限和相关上下文。
6. Actor 决定是否进行人工核验或业务跟进。

### Important Rule
Attention View 不得把 `STALE_UPDATE` 自动描述成“任务延期”。

---

## UC-004 — Submit Completion Claim

**Primary Actor:** Authorized Accountable Party  
**Goal:** 声明执行工作已完成并进入正式 Closure Review。  
**Preconditions:** Item is `IN_PROGRESS`。

### Main Flow
1. Actor 打开事项。
2. Actor 填写 Completion Summary。
3. Actor 按适用规则提供 Completion Evidence（若要求）。
4. Actor 提交 Completion Claim。
5. 系统校验权限与必填信息。
6. 系统记录 Claim Actor / Timestamp。
7. Lifecycle 转换为 `PENDING_CLOSURE`。
8. 系统记录 Audit Event。

### Alternatives
- A1: Required evidence missing → reject。
- A2: Item not IN_PROGRESS → reject。
- A3: Duplicate normal claim while PENDING_CLOSURE → reject。

### Invariant
提交 Completion Claim 不得直接将 Item 置为 `CLOSED`。

---

## UC-005 — Approve Closure

**Primary Actor:** Closure Authority（具体角色 TBD）  
**Goal:** 对 Completion Claim 进行确认并正式结束督办。

### Main Flow
1. Actor 打开 `PENDING_CLOSURE` Item。
2. Actor 查看 Completion Summary / Evidence / History。
3. Actor 执行 Approve Closure。
4. 系统校验 Closure Authority。
5. Lifecycle 转换为 `CLOSED`。
6. 系统记录 Closure Actor / Timestamp / Audit Event。

### Alternative Candidate
Reject / Return Completion Claim 的业务规则尚未确认，因此暂不进入 Implementation-ready Scope。

### SPEC_GAP
- Closure Authority；
- 是否允许退回；
- 不同事项是否需要不同 Evidence。

---

## UC-006 — Management Intervention Review

**Primary Actor:** Manager  
**Goal:** 快速识别真正需要管理干预的事项。

### Main Flow
1. Actor 进入 Management View。
2. 系统仅展示 Actor 权限范围内信息。
3. 系统优先提供 Attention / Dependency / Blocking Context。
4. Actor 查看某事项为何需要关注。
5. Actor 决定是否协调资源或要求进一步说明。

### Product Design Boundary
Use Case 不规定必须使用：
- KPI 卡片；
- 饼图；
- 柱状图；
- 大屏。

UI 形式由 Product Design 阶段根据 Job 决定。
