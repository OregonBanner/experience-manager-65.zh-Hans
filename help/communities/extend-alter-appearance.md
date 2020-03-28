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
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# 更改外观(HBS) {#alter-the-appearance-hbs}

现在，应用程序目录(/apps)中的自定义注释系统的组件就位，并且resourceSuperType引用默认注释系统和已注册的自定义模型/视图，因此可以修改实现。

对于简单的演示，删除了可视功能（发布评论的登录用户显示的头像）。

>[!NOTE]
>
>要使用扩展，要受影响的网站(/content)中的评论系统实例必须将其resourceType设置为自定义评论系统。

## 修改HBS脚本 {#modify-the-hbs-scripts}

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 打 [开/apps/custom/components/comments/comment/**comment.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * 注释掉标记，该标记包含评论帖子的头像（~行21）:

      ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
      ```

* Open [/apps/custom/components/comments/**comments.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * 注释掉标记，该标记包括下一个注释条目的头像（~行44）:

      ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
      ```

* 选择 **全部保存**

### 复制自定义应用程序 {#replicate-custom-app}

修改应用程序后，必须重新复制自定义组件。

这样做的一个方法是

* 从主菜单

   * 选择“ **工具”>“操作”>“复制”**
   * select `Activate Tree`
   * 设置 `Start Path`:to `/apps/custom`
   * deselect `Only Modified`
   * 选择按 `Activate`钮

### 视图在已发布的示例页面上修改的注释 {#view-modified-comment-on-published-sample-page}

[继续发布实例](/help/communities/extend-sample-page.md#publish-sample-page) （仍以同一用户身份登录）的体验，现在可以刷新发布环境中的页面以视图修改以删除头像：

![chlimage_1-136](assets/chlimage_1-136.png)

### 示例注释扩展包 {#sample-comment-extension-package}

附加的是本教程中创建的自定义注释应用程序的包。

[获取文件](assets/sample-comment-extension-6-1-fp3.zip)
