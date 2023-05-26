---
title: 更改外观(HBS)
seo-title: Alter the Appearance
description: 修改HBS脚本
seo-description: Modify the HBS scripts
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 更改外观(HBS) {#alter-the-appearance-hbs}

现在，应用程序目录(/apps)中的自定义注释系统组件已准备就绪，并且resourceSuperType引用了默认注释系统和注册的自定义模型/视图，因此可以修改实施。

对于简单的演示，将删除视觉功能，即发布评论的登录用户的头像。

>[!NOTE]
>
>要使用扩展，要受影响的网站中的注释系统实例(/content)必须将其resourceType设置为自定义注释系统。

## 修改HBS脚本 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)：

* 打开 [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 注释掉包含注释帖子头像的标记（~第21行）：

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* 打开 [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 注释掉包含下一个注释条目（~第44行）的头像的标记：

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* 选择 **全部保存**

### 复制自定义应用程序 {#replicate-custom-app}

修改应用程序后，需要重新复制自定义组件。

实现目标的一种方法是：

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
