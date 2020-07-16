---
title: 向示例页面添加注释
seo-title: 向示例页面添加注释
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
source-git-commit: 230c700d87d82d248b7d0bbc45c69c5c2b0e3ff8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# 向示例页面添加注释  {#add-comment-to-sample-page}

现在，自定义注释系统的组件在应用程序目录(/apps)中就位，可以使用扩展组件。 受影响网站中注释系统的实例必须将其resourceType设置为自定义注释系统并包含所有必需的客户端库。

## 识别所需的客户端库 {#identify-required-clientlibs}

扩展注释还需要默认注释的样式和功能所必需的客户端库。

《社 [区组件指南](/help/communities/components-guide.md) 》可标识所需的客户端库。 浏览到组件指南并视图注释组件，例如：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

请注意注释需要的三个客户端库才能正常呈现和运行。 扩展注释和扩展注释的客户端库() [中需要包含这些注释](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`)。

![chlimage_1-47](assets/chlimage_1-47.png)

### 向页面添加自定义注释 {#add-custom-comments-to-a-page}

由于每页只能有一个注释系统，因此创建示例页面更简单，如简短的创建示例 [页面教程中所述](/help/communities/create-sample-page.md) 。

创建后，进入设计模式并使自定义组件组可用，以允 `Alt Comments` 许将组件添加到页面。

为了使“注释”正确显示和运行，必须将“注释”的客户端库添加到该页的clientlibslist中(请参 [阅Clientlibs for Communities](/help/communities/clientlibs.md))。

#### 示例页面上的注释客户端库 {#comments-clientlibs-on-sample-page}

![chlimage_1-48](assets/chlimage_1-48.png)

#### 作者： 示例页面上的替代注释 {#author-alt-comment-on-sample-page}

![chlimage_1-49](assets/chlimage_1-49.png)

#### 作者： 示例页面注释节点 {#author-sample-page-comments-node}

可以通过查看示例页面的注释节点的属性来验证CRXDE中的resourceType `/content/sites/sample/en/jcr:content/content/primary/comments`。

![chlimage_1-50](assets/chlimage_1-50.png)

#### 发布示例页面 {#publish-sample-page}

将自定义组件添加到页面后，还需要（重新）发 [布页面](/help/communities/sites-console.md#publishing-the-site)。

#### 发布： 示例页面上的替代注释 {#publish-alt-comment-on-sample-page}

发布自定义应用程序和示例页面后，可以输入评论。 登录后，无论是与演示用 [户](/help/communities/tutorials.md#demo-users) 还是管理员登录，都可以发布评论。

以下是aaron.mcdonald@mailinator.com发布评论：

![chlimage_1-51](assets/chlimage_1-51.png)

![chlimage_1-52](assets/chlimage_1-52.png)

现在，扩展组件在默认外观上工作正常，是时候修改外观了。