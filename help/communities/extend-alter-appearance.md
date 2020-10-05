---
title: 更改外观(HBS)
seo-title: 改变外观
description: 修改HBS脚本
seo-description: 修改HBS脚本
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: 570c970c328ded828680baeb1b04ab4361a36226
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# 更改外观(HBS) {#alter-the-appearance-hbs}

现在，应用程序目录(/apps)中的自定义注释系统的组件就位，并且resourceSuperType引用默认注释系统和注册的自定义模型/视图，因此可以修改实现。

对于简单的演示，将删除可视功能（发布评论的已登录用户显示的头像）。

>[!NOTE]
>
>要使用扩展，要受影响的网站(/content)中的评论系统实例必须将其resourceType设置为自定义评论系统。


## 修改HBS脚本 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 打开 [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 注释掉包含评论帖子的头像的标记（~行21）:

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Open [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 注释掉包含下一个注释条目的头像的标记（~行44）:

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* 选择 **全部保存**

### 复制自定义应用程序 {#replicate-custom-app}

修改应用程序后，必须重新复制自定义组件。

一种方法是：

* 从主菜单

   * 选择 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复]**&#x200B;制。
   * 选择 **[!UICONTROL 激活树]**。
   * 设 `Start Path` 置为 `/apps/custom`。
   * 取消选 **[!UICONTROL 择“仅修改]**”。
   * 选择 **[!UICONTROL 激活]** 按钮。

### 视图在已发布的示例页面上修改的注释 {#view-modified-comment-on-published-sample-page}

[继续在发布实例](/help/communities/extend-sample-page.md#publish-sample-page) （仍以同一用户身份登录）上体验，现在可以刷新发布环境中的页面，以视图修改以删除头像：

![视图修改内容](assets/view-modified-content.png)

### 注释扩展包示例 {#sample-comment-extension-package}

附加是本教程中创建的自定义注释应用程序的包。

[获取文件](assets/sample-comment-extension-6-1-fp3.zip)
