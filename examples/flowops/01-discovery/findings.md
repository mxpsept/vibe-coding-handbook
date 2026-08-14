# FlowOps — Discovery Findings v0.1

> 所有 Evidence 均为 **Synthetic Teaching Case**。本文件演示 Cross-source Synthesis，不代表真实用户研究。

## 1. Evidence Index

| Source | Type | Level | Main perspective |
| --- | --- | --- | --- |
| INT-001 | Interview | E2 | 督办专员 |
| INT-002 | Interview | E2 | 执行人员 |
| INT-003 | Interview | E2 | 管理者 |
| INT-004 | Interview | E2 | 部门负责人 |
| INT-005 | Interview | E2 | 督办负责人 |
| ART-001 | Existing Artifact | E3 | 当前 Excel 结构 |
| OBS-001 | Observation | E3 | 周会前实际汇总行为 |

## 2. Consolidated Findings

### F-001 — 信息分散不是单纯“Excel 不好用”

重点事项信息实际跨 Excel、即时通讯、人工询问和会议材料流动。问题是多个来源之间缺少稳定的一致性与追踪关系，而不是单纯需要“把 Excel 搬到网页”。

Evidence: INT-001, INT-002, OBS-001。Confidence: High within teaching case。

### F-002 — 责任存在多个层级

当前至少出现：

```text
责任部门
部门内部执行人
督办联系人
跨部门依赖方
```

它们不能未经验证直接压缩成一个 `assignee_id`。

Evidence: INT-002, INT-004, ART-001。

### F-003 — Progress、Update、Status、Risk 不是同一个概念

```text
工作正在推进
  ≠ 最近有进度填报
  ≠ Excel 状态已更新
  ≠ 当前没有风险
```

Evidence: INT-001, INT-002, ART-001, OBS-001。

### F-004 — “未更新”适合作为 Attention Signal，而非自动异常结论

未更新可能代表信息滞后，也可能只是工作没有阶段性成果或重复填报成本过高。

Evidence: INT-001, INT-002, OBS-001。

### F-005 — 管理者需要的是 Intervention View，而非“更多图表”

管理者的核心 Job 是识别需要管理干预的事项、原因以及协调需求。

Evidence: INT-003。

需要更多管理角色 Evidence 才能升级可信度。

### F-006 — Completion Claim 与 Process Closure 可能不同

部门/执行人员说“完成”后，部分事项可能仍需要成果确认。

Evidence: INT-005 + OBS-001。

这意味着后续必须明确 Completion / Acceptance / Closure 语义。

### F-007 — 跨部门依赖是风险信息的重要来源

当前依赖可能只存在于备注、群聊或口头说明中，无法稳定用于风险识别。

Evidence: INT-003, INT-004, ART-001, OBS-001。

### F-008 — 重点事项来源存在分类，但尚未标准化

候选包括会议安排、领导交办、跨部门重点工作和临时专项。

Evidence: INT-005 + ART-001（证明“任务来源”字段存在）。

## 3. Jobs

### J-001 督办专员
在管理会议前快速获得可信的风险事项清单，并知道需要继续确认什么。

### J-002 执行人员
清楚知道自己承担什么以及何时需要反馈，用较低重复成本同步真实进展和阻塞。

### J-003 管理者
在有限时间内识别需要管理层干预的事项，并理解原因与协调需求。

### J-004 部门负责人
管理部门责任、内部执行和外部依赖，并能够解释影响交付的因素。

## 4. Business Rule Candidates

| ID | Candidate | Evidence | Status |
| --- | --- | --- | --- |
| BR-C001 | 管理层介入与跨部门协调、重要节点延误、责任不明确有关 | INT-003 | Validate |
| BR-C002 | 责任部门与个人执行责任可能分层 | INT-004, ART-001 | Validate |
| BR-C003 | 部分事项存在协作/依赖方 | INT-004, ART-001 | Validate |
| BR-C004 | 延期规则可能因事项类型而不同 | INT-004 | Validate |
| BR-C005 | 督办事项存在多个来源类别 | INT-005, ART-001 | Validate |
| BR-C006 | 超期与要求完成时间相关 | INT-005, ART-001 | Validate |
| BR-C007 | 临期不一定适合统一固定天数 | INT-001, INT-005 | Validate |
| BR-C008 | Completion Claim 可能需要进一步确认后才能 Closure | INT-005, OBS-001 | Validate |

## 5. Feature Requests — Still Not Requirements

| Request | Source | Underlying Job / Problem |
| --- | --- | --- |
| 自动提醒未更新 | INT-001 | 减少人工筛选并及时发现信息缺口 |
| 自动提醒快超期 | INT-001 | 提前发现交付风险 |
| 我的任务列表 | INT-002 implied | 清楚知道个人需要处理什么 |
| 管理驾驶舱 | Project hypothesis | 快速识别需要管理干预的事项 |

任何一项都尚未因为“听起来合理”而直接批准。

## 6. Contradictions / Tensions

### C-001：未更新 = 风险？

督办视角倾向将未更新作为风险；执行视角说明未更新不等于未推进。

Resolution direction: 区分 `information freshness` 与 `delivery risk`。

### C-002：是否必须维护个人责任人？

执行侧需要知道个人任务，但部门负责人认为正式督办责任可能只到部门。

Resolution direction: Requirements 阶段定义 Accountability 与 Assignment 两个层级是否必要。

### C-003：完成意味着结束？

部分角色会说“完成”，但督办流程可能仍需成果确认。

Resolution direction: 定义 Completion Claim / Acceptance / Closure。

## 7. Highest-priority Unknowns

1. 重点事项正式进入督办的规则与权力边界；
2. 下达与签收是否存在正式流程；
3. 主责、协办、个人执行责任的正式语义；
4. Progress 百分比是否有业务价值和统一标准；
5. 临期规则应固定、按任务配置还是按类型配置；
6. 延期是否正式审批；
7. 办结是否需要申请与确认；
8. 数据权限边界；
9. 不同任务来源是否需要不同流程；
10. Outcome Metrics 的真实基线。

## 8. Discovery Decision

当前 Evidence 足以证明问题值得继续，并能够开始 Requirements 的部分定义；但 Business Rules 仍存在明显 Unknown。

建议 Gate 1：**PASS WITH OPEN ITEMS**。

进入 Requirements 时必须保留 Traceability，不得把所有 Candidate 自动升级为 Must-have。
