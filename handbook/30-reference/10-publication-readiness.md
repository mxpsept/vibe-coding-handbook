# Publication Readiness — 从内部手册到可公开维护的工程项目

当 Handbook 主干已经完整，下一步不是继续堆章节，而是确保陌生读者能够理解、导航、验证和贡献。

## 1. Repository Front Door

公开仓库至少让第一次访问者快速回答：

```text
这是什么？
适合谁？
我应该从哪里开始？
有没有完整案例？
如何贡献？
当前稳定程度如何？
```

对应入口：README、START-HERE、Case Index、CONTRIBUTING、Release Notes。

## 2. Navigation Quality

内部文档优先使用相对链接。检查：
- renamed/moved files；
- README / START-HERE 入口；
- chapter → template/example；
- example → source rule；
- reference index coverage。

目录存在不等于可导航；读者应该能从“我要解决的问题”到达正确 Artifact。

## 3. Content Quality

每个重要主题检查：

```text
Problem
Method
Boundary / Trade-off
Example
Reusable Artifact
Verification
Further Learning
```

不是每篇都必须机械使用相同标题，但不能只有观点没有落地方式。

## 4. Public Safety

发布前搜索：
- credentials/tokens/passwords；
- internal host/IP/domain；
- real employee/customer information；
- proprietary screenshots/documents；
- copied copyrighted material；
- company-specific confidential workflow。

FlowOps 必须保持虚构和行业通用。

## 5. External References

外部资源分级：

```text
A — Standard / Primary official source
B — Official product/maintainer documentation
C — High-quality engineering reference
D — Community inspiration
```

核心事实尽量使用 A/B；D 只能作为经验或灵感，不包装成行业标准。

## 6. Release Readiness

一次公开版本应说明：
- covered lifecycle；
- major examples/templates；
- known gaps；
- compatibility/tool-specific caveats；
- next direction。

版本号表达手册成熟度，不意味着方法永远不会变化。

## 7. Definition of Published

```text
A stranger can start.
A practitioner can apply.
A reviewer can verify.
A contributor can extend.
A maintainer can evolve it without losing Source of Truth.
```
