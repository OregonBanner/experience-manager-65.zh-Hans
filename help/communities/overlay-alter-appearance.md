---
title: 更改外观
description: 修改脚本
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 更改外观 {#alter-the-appearance}

## 修改脚本 {#modify-the-script}

comment.hbs脚本负责为每个评论创建整体HTML。

不显示每个已发布评论旁的头像：

1. 复制 `comment.hbs`起始日期 `libs`到 `apps`

   1. 选择 `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. 选择 **[!UICONTROL 复制]**
   1. 选择 `/apps/social/commons/components/hbs/comments/comment`
   1. 选择 **[!UICONTROL 粘贴]**

1. 打开覆盖的 `comment.hbs`

   * 双击节点 `comment.hbs` 在 `/apps/social/commons/components/hbs/comments/comment folder`

1. 查找以下行，然后删除它们或将其注释掉：

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

删除这些行，或者用以下内容将它们围起来 `<!--` 和 `-->` 所以你别再说了。 此外，字符“xxx”将被添加为显示头像位置的可视指示器。

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### 复制叠加 {#replicate-the-overlay}

使用复制工具将覆盖的注释组件推送到发布实例。

>[!NOTE]
>
>更可靠的复制形式是在包管理器中创建包，并且 [激活](/help/sites-administering/package-manager.md#replicating-packages) 它。 可以导出和存档资源包。

在全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]** 并单击 **[!UICONTROL 激活树]**.

对于“起始路径”，输入 `/apps/social/commons` 并选择 **[!UICONTROL 激活]**.

![verify-content-template](assets/verify-content-template.png)

### 查看结果 {#view-results}

如果您以管理员身份(例如，以admin/admin身份登录https://localhost:4503/crx/de )登录到发布实例，则可以验证覆盖的组件是否存在。

如果您注销，然后以 `aaron.mcdonald@mailinator.com/password` 并刷新页面，您注意到某个头像未与发布的评论一起显示。 而是显示简单的“xxx”。

![create-template-component](assets/create-template-component.png)
