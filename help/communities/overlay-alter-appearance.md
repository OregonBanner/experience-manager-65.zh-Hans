---
title: 改变外观
seo-title: 改变外观
description: 修改脚本
seo-description: 修改脚本
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: 9d6ec05fdc98e33a11303d189414c2c45c5e8b3c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 改变外观 {#alter-the-appearance}

## 修改脚本 {#modify-the-script}

comment.hbs脚本负责为每个注释创建整体HTML。

不要在每个已发布的评论旁边显示头像：

1. 复制 `comment.hbs`自 `libs`到 `apps`

   1. 选择 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 选择复 **[!UICONTROL 制]**
   1. 选择 `/apps/social/commons/components/hbs/comments/comment`
   1. 选择粘 **[!UICONTROL 贴]**

1. 打开叠加 `comment.hbs`

   * 多次-单击中的节 `comment.hbs` 点 `/apps/social/commons/components/hbs/comments/comment folder`

1. 查找以下行，并删除或注释它们：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

删除这些行，或将其周围 `<!--` 放置 `-->` 并注释掉它们。 此外，字符“xxx”正被添加为虚拟形象的位置的可视指示符。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 复制叠加 {#replicate-the-overlay}

使用复制工具将叠加的注释组件推送到发布实例。

>[!NOTE]
>
>更可靠的复制形式是在包管理器中创建包并 [激活](/help/sites-administering/package-manager.md#replicating-packages) 它。 可以导出和存档包。


在全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复]** 制 **[!UICONTROL ，然后单]**&#x200B;击激活树。

对于开始路径，请输 `/apps/social/commons` 入并选 **[!UICONTROL 择激活]**。

![verify-content-template](assets/verify-content-template.png)

### 视图结果 {#view-results}

如果您以管理员(例如https://localhost:4503/crx/de以管理员／管理员身份登录)的身份登录发布实例，则可以验证叠加的组件是否在此处。

如果注销并重新登录为 `aaron.mcdonald@mailinator.com/password` 页面并刷新页面，您将发现已发布的注释不再显示为头像，而是显示一个简单的“xxx”。

![create-template-component](assets/create-template-component.png)

