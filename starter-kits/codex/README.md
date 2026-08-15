# Codex Project Starter Kit

这是一套把 Handbook 方法真正放进日常仓库的最小 Starter Kit。

目标不是增加文档负担，而是让 Coding Agent 每次进入项目时都能快速回答：

```text
我在做什么？
什么事实不能猜？
代码边界在哪里？
什么情况下必须停？
怎样证明完成？
```

## 推荐复制结构

```text
project/
├── AGENTS.md
├── docs/
│   ├── product/
│   │   └── product-context.md
│   ├── architecture/
│   │   └── architecture-context.md
│   └── features/
│       └── FEAT-001/
│           ├── feature-spec.md
│           ├── implementation-packet.md
│           └── verification.md
└── ...source code
```

## Daily Loop

```text
1. Human/AI clarify Feature Spec
2. Human approves critical rules / UX / boundary
3. Create Implementation Packet
4. Codex performs repository reconnaissance
5. Codex proposes bounded plan
6. Implement smallest coherent slice
7. Run verification
8. Independent review
9. Record evidence / unresolved gaps
10. Commit intentionally
```

## Do Not Put Everything in AGENTS.md

`AGENTS.md` 是稳定仓库规则，不是 Feature PRD。

放入：build/test commands、architecture boundaries、conventions、forbidden actions、verification expectations。

不要放入：一次性需求、聊天历史、某个 Feature 的临时 AC、长篇产品背景。

## Minimum Adoption

如果团队第一次使用，只复制：
- `AGENTS.example.md`
- `implementation-packet.example.md`
- `verification-report.example.md`

跑完一个 Vertical Slice 后，再决定是否引入更多 Artifact。
