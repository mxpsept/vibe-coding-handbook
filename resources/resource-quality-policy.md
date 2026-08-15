# External Resource Quality Policy

Handbook 中的外部链接不是“收藏夹”，每个链接都应帮助读者解决明确问题。

## Level A — Standards / Primary Sources

例如正式规范、标准组织、语言/协议官方规范。

适合支撑：
- normative behavior；
- protocol/security/accessibility requirements；
- stable technical definitions。

## Level B — Official Product / Maintainer Docs

例如工具、框架、平台官方文档和官方维护仓库。

适合支撑：
- current configuration；
- commands/APIs；
- supported capabilities；
- product-specific workflows。

工具变化快，因此需要定期复查。

## Level C — Engineering References

成熟工程团队文章、经典工程资料、大学课程、可信技术会议等。

适合：
- trade-off；
- architecture/design thinking；
- case-based learning。

不能仅凭作者知名度把观点当标准。

## Level D — Community / Inspiration

社区讨论、个人博客、UI gallery、经验分享。

适合：
- discovery；
- alternative ideas；
- visual inspiration；
- practitioner sentiment。

不适合单独支撑安全、协议、合规或产品当前能力等关键事实。

## Link Entry

推荐记录：

```text
Title
URL
Level
Why it is useful
Handbook topics
Last checked (optional for volatile resources)
```

## Hygiene

- canonical URL；
- 去除无必要 tracking parameters；
- repository internal links 使用 relative path；
- 避免复制大量外部原文；
- 链接失效时优先寻找同一 Primary Source 的新 canonical page；
- 工具当前行为变化时更新 Handbook，而不是只替换 URL。
