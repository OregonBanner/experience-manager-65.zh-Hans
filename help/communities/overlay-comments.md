---
title: 叠加Communities组件
description: 了解如何叠加默认组件，以便针对组件的所有相对引用，全局更改组件的外观或行为。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 叠加Communities组件 {#overlay-communities-components}

意图 [覆盖](/help/communities/client-customize.md#overlays) 缺省组件是在全局范围内更改组件的外观或行为（对于组件的所有相对引用）。 它依赖于sling的性质，以在在/libs文件夹中进行搜索之前解析到/apps文件夹。 因此，组件的路径与默认组件的路径相同，不同之处在于它位于/apps文件夹中，而不是/libs文件夹中。

## 示例 {#example}

**叠加评论组件**

假设您想要修改评论功能，使其与您的网站设计相匹配，方法是更改评论标题，使其不再显示任何评论的头像。 用于隐藏头像的解决方案要么使用CSS，要么按照此处所述覆盖apps文件夹中的header.jsp，这样包含头像的HTML永远不会发送到客户端。

要叠加注释，您必须：

1. [“创建评论”页](/help/communities/overlay-create-comments-page.md)
1. [创建节点](/help/communities/overlay-create-nodes.md)
1. [更改外观](/help/communities/overlay-alter-appearance.md)

**覆盖通知电子邮件**

假设您要自定义电子邮件通知的消息，可以通过以下方式进行 [覆盖](/help/communities/client-customize.md#overlays) 模板位于 `/libs/settings/community/templates/email/html`.

例如，假设您要编辑提及电子邮件通知（针对创建UGC的特定社区组件）。 在这种情况下，请添加 **如果** 动词的条件 **提及** 在您为其启用的组件的模板中 **@mentions** 支持。

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

要修改博客评论中发@mention的电子邮件通知模板，请将现成模板放置在： `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
