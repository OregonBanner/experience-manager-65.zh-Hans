---
title: 更改外观
seo-title: 更改外观
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
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# 更改外观 {#alter-the-appearance}

## 修改脚本 {#modify-the-script}

comment.hbs脚本负责为每个注释创建整体HTML。

不要在每个已发布评论旁边显示头像：

1. 从复 `comment.hbs`制 `libs`到 `apps`

   1. 选择 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 选择复 **制**
   1. 选择 `/apps/social/commons/components/hbs/comments/comment`
   1. 选择粘 **贴**

1. 打开叠加 `comment.hbs`

   * 多次-单击中的节点 `comment.hbs``/apps/social/commons/components/hbs/comments/comment folder`

1. 查找以下行，然后删除或注释这些行：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

删除这些行，或将其包围 `<!--` 并 `-->` 注释掉它们。 此外，字符“xxx”正被添加为头像所在位置的可视指示符。

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
>更可靠的复制形式是在包管理器中创建包并 [激活](/help/sites-administering/package-manager.md#replicating-packages) 。 可以导出和存档包。


在全局导航中，选择 **[!UICONTROL 工具]** >部 **[!UICONTROL 署]** >复 **[!UICONTROL 制]** ，然后单击 ****&#x200B;激活树导航。

对于开始路径，请输入并 `/apps/social/commons` 选择“ **[!UICONTROL 激活”]**。

![chlimage_1-77](assets/chlimage_1-77.png)

### 视图结果 {#view-results}

如果您以管理员(例如，以管理员／管理员身份https://localhost:4503/crx/de)的身份登录到发布实例，则可以验证覆盖的组件是否在此处。

如果您注销并重新登录为 `aaron.mcdonald@mailinator.com/password` 页面并刷新该页面，您会发现已发布的评论不再显示为头像，而是显示一个简单的“xxx”。

![chlimage_1-78](assets/chlimage_1-78.png)

