---
title: 更改外观(HBS)
seo-title: 更改外观
description: 修改HBS脚本
seo-description: 修改HBS脚本
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
source-wordcount: '278'
ht-degree: 0%

---

# 更改外观(HBS){#alter-the-appearance-hbs}

现在，应用程序目录(/apps)中自定义注释系统的组件就位，并且resourceSuperType引用默认注释系统并注册了自定义模型/视图，因此可以修改实施。

对于简单的演示，会删除视觉功能（发布评论的已登录用户显示的头像）。

>[!NOTE]
>
>要使用该扩展，要受影响的网站(/content)中评论系统的实例必须将其resourceType设置为自定义评论系统。

## 修改HBS脚本{#modify-the-hbs-scripts}

使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 打开[/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 注释掉包含评论帖子头像的标记（~第21行）：

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* 打开[/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 注释掉包含下一个评论条目的头像的标记（~第44行）：

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* 选择&#x200B;**Save All**

### 复制自定义应用程序{#replicate-custom-app}

修改应用程序后，需要重新复制自定义组件。

一种方法是：

* 从主菜单

   * 选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复制]**。
   * 选择&#x200B;**[!UICONTROL 激活树]**。
   * 将`Start Path`设置为`/apps/custom`。
   * 取消选择&#x200B;**[!UICONTROL 仅已修改]**。
   * 选择&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。

### 查看已发布示例页面{#view-modified-comment-on-published-sample-page}上的已修改注释

[继续发](/help/communities/extend-sample-page.md#publish-sample-page) 布实例上的体验（仍以同一用户身份登录），现在可以在发布环境中刷新页面以查看修改以删除头像：

![view-modified-content](assets/view-modified-content.png)

### 示例注释扩展包{#sample-comment-extension-package}

附加的是在本教程中创建的自定义注释应用程序包。

[获取文件](assets/sample-comment-extension-6-1-fp3.zip)
