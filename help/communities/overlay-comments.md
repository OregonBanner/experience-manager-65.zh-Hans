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
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 覆盖社区组件{#overlay-communities-components}

[覆盖](/help/communities/client-customize.md#overlays)默认组件的意图是全局更改组件的外观或行为，以便对组件进行所有相对引用。 在/libs文件夹中搜索之前，它依赖于sling的性质来解析到/apps文件夹。 因此，组件的路径与默认组件的路径相同，不同之处在/apps文件夹中，而不是/libs文件夹中。

## 示例 {#example}

**叠加注释组件**

假定您想要修改评论功能，使其与您网站的设计相匹配，方法是更改评论标题，以便不再显示任何评论的头像。 用于隐藏头像的解决方案是使用CSS，或者，如此处所述，在apps文件夹中叠加header.jsp，以便包含头像的HTML永远不会发送到客户端。

要叠加评论，您需要：

1. [“评论”页面](/help/communities/overlay-create-comments-page.md)
1. [创建节点](/help/communities/overlay-create-nodes.md)
1. [更改外观](/help/communities/overlay-alter-appearance.md)

**叠加通知电子邮件**

假定要自定义电子邮件通知的消息，可以通过[覆盖](/help/communities/client-customize.md#overlays)**/libs/settings/community/templates/email/html**&#x200B;中的模板来执行此操作。

例如，要修改提及次数电子邮件通知（针对创建ugc的特定社区组件），请在为其启用&#x200B;**@mentions**&#x200B;支持的组件模板中，为动词&#x200B;**提及**&#x200B;添加&#x200B;**条件。**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

要修改博客评论中@mention的电子邮件通知模板，请将开箱即用模板放置：`/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
