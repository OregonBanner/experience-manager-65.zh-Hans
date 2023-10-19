---
title: 向示例页面添加注释
description: 了解网站评论系统的实例如何必须将其resourceType设置为自定义评论系统并包括所有必要的客户端库。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 向示例页面添加注释  {#add-comment-to-sample-page}

现在，自定义注释系统的组件已放置在application目录(/apps)中，可以使用扩展组件。 要受影响的网站中评论系统的实例必须将其resourceType设置为自定义评论系统，并包括所有必要的客户端库。

## 确定所需的Clientlibs {#identify-required-clientlibs}

对于扩展注释而言，缺省注释的样式和功能所必需的客户端库也是必需的。

此 [社区组件指南](/help/communities/components-guide.md) 标识所需的客户端库。 浏览到“组件指南”并查看“注释”组件，例如：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

请注意呈现评论和使其正常运行所需的三个客户端库。 引用扩展注释时必须包含这些注释，并且 [扩展注释的客户端库](/help/communities/extend-create-components.md#create-a-client-library-folder) ( `apps.custom.comments`)。

![comments-component1](assets/comments-component1.png)

### 向页面添加自定义评论 {#add-custom-comments-to-a-page}

由于每页只能有一个注释系统，因此创建示例页面会更简单，如简介中所述 [创建示例页面](/help/communities/create-sample-page.md) 教程。

创建后，进入设计模式并提供自定义组件组，以允许 `Alt Comments` 要添加到页面中的组件。

要使注释正确显示和运行，必须将注释的客户端库添加到页面的clientlibslist中(请参阅 [适用于社区组件的Clientlibs](/help/communities/clientlibs.md))。

#### 示例页面上的注释Clientlibs {#comments-clientlibs-on-sample-page}

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 作者：示例页面上的替代评论 {#author-alt-comment-on-sample-page}

![alt-comment](assets/alt-comment.png)

#### 作者：示例页面评论节点 {#author-sample-page-comments-node}

在CRXDE中可通过查看示例页面的comments节点的属性来验证resourceType `/content/sites/sample/en/jcr:content/content/primary/comments`.

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### 发布示例页面 {#publish-sample-page}

将自定义组件添加到页面后，还需要（重新） [发布页面](/help/communities/sites-console.md#publishing-the-site).

#### 发布：示例页面上的Alt注释 {#publish-alt-comment-on-sample-page}

在发布自定义应用程序和示例页面后，可以输入注释。 登录时，使用 [演示用户](/help/communities/tutorials.md#demo-users) 或管理员，可以发布评论。

以下是aaron.mcdonald@mailinator.com发表评论：

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

现在，扩展组件在默认外观下运行正常，是时候修改外观了。
