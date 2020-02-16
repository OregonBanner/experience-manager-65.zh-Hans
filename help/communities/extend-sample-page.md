---
title: 向示例页面添加评论
seo-title: 向示例页面添加评论
description: 向页面添加自定义注释
seo-description: 向页面添加自定义注释
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 向示例页面添加评论 {#add-comment-to-sample-page}

现在，自定义注释系统的组件就位于应用程序目录(/apps)中，可以使用扩展组件。 要受影响的网站中的评论系统实例必须将其resourceType设置为自定义评论系统并包含所有必需的客户端库。

## 识别所需的客户端库 {#identify-required-clientlibs}

扩展注释还需要默认注释的样式和功能所必需的客户端库。

《社 [区组件指南](/help/communities/components-guide.md) 》可标识所需的客户端库。 浏览到“组件指南”并查看“注释”组件，例如：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

请注意注释所需的三个客户端库以正确呈现和运行。 扩展注释和扩展注释的客户端库( [](/help/communities/extend-create-components.md#create-a-client-library-folder)`apps.custom.comments`)需要包含这些注释。

![chlimage_1-79](assets/chlimage_1-79.png)

### 向页面添加自定义注释 {#add-custom-comments-to-a-page}

由于每页只能有一个注释系统，因此创建示例页面更简单，如简短的创建示例页 [面教程中所述](/help/communities/create-sample-page.md) 。

创建后，进入设计模式并使自定义组件组可用，以允 `Alt Comments` 许将组件添加到页面。

为了使“注释”正确显示和运行，必须将“注释”的客户端库添加到页面的clientlibslist中(请参阅 [Clientlibs for Communities组件](/help/communities/clientlibs.md))。

#### 示例页面上的注释客户端库 {#comments-clientlibs-on-sample-page}

![示例页面上的注释客户端库](assets/chlimage_1-80.png)

#### 作者：示例页面上的替代注释 {#author-alt-comment-on-sample-page}

![示例页面上的替代注释](assets/chlimage_1-81.png)

#### 作者：示例页面注释节点 {#author-sample-page-comments-node}

可以通过查看示例页面的注释节点的属性来验证CRXDE中的resourceType `/content/sites/sample/en/jcr:content/content/primary/comments`。

![chlimage_1-82](assets/chlimage_1-82.png)

#### 发布示例页面 {#publish-sample-page}

将自定义组件添加到页面后，还必须（重新）发 [布页面](/help/communities/sites-console.md#publishing-the-site)。

#### 发布：示例页面上的替代注释 {#publish-alt-comment-on-sample-page}

发布自定义应用程序和示例页面后，可以输入评论。 登录后，无论是与演示用户 [还是管理员](/help/communities/tutorials.md#demo-users) ，都可以发布评论。

以下是aaron.mcdonald@mailinator.com发布评论：

![chlimage_1-83](assets/chlimage_1-83.png) ![chlimage_1-84](assets/chlimage_1-84.png)

现在，扩展组件看起来可以正确使用默认外观，是时候修改外观了。