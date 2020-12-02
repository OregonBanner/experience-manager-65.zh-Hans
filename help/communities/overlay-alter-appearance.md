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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 更改外观{#alter-the-appearance}

## 修改脚本{#modify-the-script}

comment.hbs脚本负责为每个注释创建整体HTML。

不要在每个已发布的评论旁边显示头像：

1. 将`comment.hbs`从`libs`复制到`apps`

   1. 选择 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 选择&#x200B;**[!UICONTROL 复制]**
   1. 选择 `/apps/social/commons/components/hbs/comments/comment`
   1. 选择&#x200B;**[!UICONTROL 粘贴]**

1. 打开叠加的`comment.hbs`

   * 多次-单击`/apps/social/commons/components/hbs/comments/comment folder`中的节点`comment.hbs`

1. 查找以下行，并删除或注释它们：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

删除这些行，或用`<!--`和`-->`将它们包围起来，以注释掉它们。 此外，字符“xxx”正被添加为虚拟形象的位置的可视指示符。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 复制叠加{#replicate-the-overlay}

使用复制工具将叠加的注释组件推送到发布实例。

>[!NOTE]
>
>更可靠的复制形式是在包管理器中创建包，并[激活](/help/sites-administering/package-manager.md#replicating-packages)它。 可以导出和存档包。

在全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]**，然后单击&#x200B;**[!UICONTROL 激活树]**。

对于开始路径，输入`/apps/social/commons`并选择&#x200B;**[!UICONTROL 激活]**。

![verify-content-template](assets/verify-content-template.png)

### 视图结果{#view-results}

如果您以管理员(例如https://localhost:4503/crx/de以管理员／管理员身份登录)的身份登录发布实例，则可以验证叠加的组件是否在此处。

如果您注销并重新登录为`aaron.mcdonald@mailinator.com/password`并刷新页面，您将发现已发布的注释不再显示为头像，而是显示一个简单的“xxx”。

![create-template-component](assets/create-template-component.png)

