# OBS-001 — 周会材料汇总观察

> **Synthetic Teaching Observation**：完全虚构，用于展示 Observation 与 Interview 的区别。

## Source
- Source ID: OBS-001
- Type: Observation
- Evidence base level: E3
- Duration: 95 minutes observed segment
- Actor: 督办专员

## Observed Timeline

| Time | Observed behavior |
| --- | --- |
| 14:00 | 打开上周总表和 4 份部门反馈表 |
| 14:08 | 手工复制两个部门的“当前进展” |
| 14:17 | 发现一个部门修改了列顺序，重新对齐 |
| 14:25 | 在工作群搜索某事项关键词确认最新回复 |
| 14:34 | 私聊一名联系人询问 9 天未变化的事项 |
| 14:47 | 收到回复：“工作已完成，稍后补材料” |
| 14:55 | 暂未把该事项改为“完成”，等待结果材料 |
| 15:08 | 对照截止日期标记两个需要会上关注的事项 |
| 15:21 | 将备注中的跨部门阻塞复制到会议材料 |
| 15:35 | 观察结束，汇总仍未完全完成 |

## Findings

### F-004 — 信息汇总存在真实跨工具切换

督办专员在 Excel、群搜索、私聊和会议材料之间切换，而不是只维护一个 Excel。

Evidence: OBS-001 / E3。

### F-005 — “执行完成”与“督办结束”存在区别

观察中联系人表示工作已完成，但督办专员没有立即修改为完成，而是等待结果材料。

Evidence: OBS-001 / E3；与 INT-005 的 Statement 相互支持。

### F-006 — 未更新是调查信号，而不是业务结论

9 天未变化触发了人工询问，但询问后发现实际工作可能已经完成。

Evidence: OBS-001 / E3；与 INT-002 的观点相互支持。

## Why Observation Matters

如果只看 INT-001，我们可能把“自动识别未更新”直接做成功能。

Observation 让我们发现更准确的语义：

```text
Stale Update
   ↓
Needs Attention / Verification
   ≠
Task Is Delayed
```

这会显著影响后续 Risk Model 和 UI 状态表达。
