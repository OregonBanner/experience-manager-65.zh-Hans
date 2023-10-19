---
title: 更改外观(HBS)
description: 了解如何通过编辑HBS脚本来更改外观(HBS)。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 更改外观(HBS) {#alter-the-appearance-hbs}

现在，应用程序目录(/apps)中的自定义注释系统组件已准备就绪，resourceSuperType引用了默认注释系统，并且自定义模型/视图已注册，接下来您可以编辑实施。

对于简单的演示，将删除视觉功能，即发布评论的登录用户显示的头像。

>[!NOTE]
>
>要使用该扩展，要受影响的网站中的注释系统实例(/content)必须将其resourceType设置为自定义注释系统。

## 修改HBS脚本 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)：

* 打开 [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 注释掉标记，其中包含注释帖子的头像（~第21行）：

     ```
       <!--
        <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
        -->
     ```

* 打开 [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 注释掉标记，该标记包括下一个注释条目（~第44行）的头像：

     ```
       <!--
        <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
        -->
     ```

* 选择 **全部保存**

### 复制自定义应用程序 {#replicate-custom-app}

修改应用程序后，需要重新复制自定义组件。

这样做的一种方式是：

* 从主菜单

   * 选择 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复制]**.
   * 选择 **[!UICONTROL 激活树]**.
   * 设置 `Start Path` 到 `/apps/custom`.
   * 取消选择 **[!UICONTROL 仅已修改]**.
   * 选择 **[!UICONTROL 激活]** 按钮。

### 查看已发布示例页面上的修改评论 {#view-modified-comment-on-published-sample-page}

[继续体验](/help/communities/extend-sample-page.md#publish-sample-page) 在仍以同一用户身份登录的发布实例上，现在可以在发布环境中刷新页面以查看删除头像的修改：

![view-modified-content](assets/view-modified-content.png)

### 示例注释扩展包 {#sample-comment-extension-package}

附件是本教程中创建的自定义注释应用程序包。

[获取文件](assets/sample-comment-extension-6-1-fp3.zip)
