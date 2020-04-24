---
title: 叠加社区组件
seo-title: 叠加社区组件
description: 叠加社区组件
seo-description: 叠加社区组件
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# 叠加社区组件 {#overlay-communities-components}

覆盖默认 [组件](/help/communities/client-customize.md#overlays) ，目的是全局更改组件的外观或行为，以便对组件的所有相对引用进行更改。 在/libs文件夹中搜索之前，它依赖sling的性质解析到/apps文件夹。 因此，组件的路径与默认组件的路径相同，只是它位于/apps文件夹中，而不是/libs文件夹中。

## 示例 {#example}

**叠加注释组件**

假定您要修改注释功能，以便它与您网站的设计相匹配，方法是更改注释标题，以便不再显示任何注释的头像。 隐藏头像的解决方案是使用CSS，或者如此处所述，在apps文件夹中覆盖header.jsp，这样包含头像的HTML就不会发送到客户端。

要叠加注释，您需要：

1. [评论页面](/help/communities/overlay-create-comments-page.md)
1. [创建节点](/help/communities/overlay-create-nodes.md)
1. [更改外观](/help/communities/overlay-alter-appearance.md)

**叠加通知电子邮件**

假定要自定义电子邮件通知的消息，可以通过在 [/libs](/help/communities/client-customize.md#overlays) /settings/community/templates/email/html中覆盖 **模板来实现**。

例如，要修改提及电子邮件通知（针对创建ugc的特定社区组件），请在启用了 **@mentions** 支持的组件的模板中为动词提及添加 **if****** 条件。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

要修改博客评论中@tuntice的电子邮件通知模板，请将开箱即用模板放在： `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
