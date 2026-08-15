# Handbook Quality Scorecard

用于定期判断手册是否真的在变好，而不是只统计 Markdown 文件数量。

每项 0–3 分：

```text
0 absent
1 partial / inconsistent
2 usable
3 strong / repeatable
```

## Dimensions

| Dimension | Question |
| --- | --- |
| Discoverability | 新读者能否在几分钟内找到正确入口？ |
| Traceability | 方法能否追踪到 Artifact / Example / Evidence？ |
| Applicability | 读者是否能照着完成真实工程任务？ |
| Case Coverage | 是否覆盖 Greenfield、Brownfield、Integration、Refactor、Production？ |
| Reusability | Template / Checklist / Prompt 是否可直接适配？ |
| Consistency | Glossary、FlowOps Rules、章节之间是否一致？ |
| Evidence Quality | 外部事实和工程结论是否有适当来源/验证？ |
| Tool Neutrality | 核心方法是否不依赖某个产品 UI？ |
| Maintainability | 是否避免重复 Source of Truth 和过期路径？ |
| Public Safety | 是否避免敏感信息、秘密和未经授权资产？ |

## Interpretation

```text
0–10   Fragmented notes
11–18  Useful draft
19–24  Practical handbook
25–28  Team-ready operating manual
29–30  Strong publication baseline
```

分数不是 KPI，也不应该为了满分制造文档。它用于暴露最弱环节。

## Review Questions

每个 Release 前额外问：

1. 哪一章最可能让读者误解？
2. 哪个流程仍需要作者口头解释才能使用？
3. 哪个案例缺少失败路径？
4. 哪个外部链接最容易过期？
5. 哪个 Artifact 被多个文件重复定义？
6. 哪个 Agent workflow 缺少 Stop Condition？

优先修复这些问题，再新增主题。
