# Design Brief — Example

## Goal
让执行人员和管理人员在 5–10 秒内回答：

```text
现在最需要我关注什么？
为什么？
下一步可以做什么？
```

## Product Character
企业内部工具：可信、克制、信息密度适中。避免把“科技感”理解为大面积渐变、发光边框和装饰图表。

## Reference Research Questions
研究同类成熟产品时，不复制皮肤，重点记录：
- 导航如何组织；
- 列表怎样表达状态与优先级；
- 详情怎样安排事实、进度、操作；
- Dashboard 如何避免图表堆砌；
- Empty/Error/Permission 如何处理。

## Information Hierarchy

### Task List
1. 任务身份/标题；
2. attention reason；
3. owner / responsible scope；
4. due date / progress；
5. allowed action。

### Task Detail
1. 核心状态与风险；
2. 责任与时间；
3. 内容/要求；
4. progress timeline；
5. audit/attachments；
6. allowed actions。

## Visual Rules
- 一个页面最多一个主要 Primary Action；
- 红色只用于需要行动的风险，不作为大面积主题色；
- lifecycle 与 attention reason 视觉和语义分离；
- table/card density 根据任务而非审美口号决定；
- Design Token 优先于页面级随意 CSS。

## Required States

```text
Loading
Empty
Data
Partial/Degraded if applicable
Error
Permission denied
Action submitting
Action success/failure
```

## AI Usage

AI 可以：生成多个 Wireframe 方向、分析参考、检查信息层级、实现已批准 Page Spec、进行截图视觉 Review。

AI 不应该：根据“做得高级一点”独立决定整个产品视觉语言，并在编码时持续随机改变布局。

## Design Gate
进入实现前，至少确认 Critical Flow、chosen wireframe、component conventions、critical states 和 responsive expectation。
