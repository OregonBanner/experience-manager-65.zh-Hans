---
title: 将注释添加到示例页面
seo-title: 将注释添加到示例页面
description: 将自定义注释添加到页面
seo-description: 将自定义注释添加到页面
uuid: ab258960-6de2-4943-80a7-e72904c0fd8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a5040371-3bc2-43bc-a103-7175c4c6252d
docset: aem65
exl-id: d4295a77-b931-4bc8-b3b4-eec42fdcfc56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 将注释添加到示例页面{#add-comment-to-sample-page}

现在，自定义注释系统的组件已位于应用程序目录(/apps)中，因此可以使用扩展组件。 要受影响的网站中评论系统的实例必须将其resourceType设置为自定义评论系统，并包含所有必需的客户端库。

## 识别所需的Clientlib {#identify-required-clientlibs}

对于扩展注释，还需要默认注释的样式和功能所必需的客户端库。

[社区组件指南](/help/communities/components-guide.md)标识所需的客户端库。 浏览组件指南并查看注释组件，例如：

[https://localhost:4502/content/community-components/en/comments.html](https://localhost:4502/content/community-components/en/comments.html)

请注意注释正确呈现和运行所需的三个客户端库。 在引用扩展注释的位置以及[扩展注释的客户端库](/help/communities/extend-create-components.md#create-a-client-library-folder)(`apps.custom.comments`)时，需要包含这些内容。

![comments-component1](assets/comments-component1.png)

### 将自定义注释添加到页面{#add-custom-comments-to-a-page}

由于每页只能有一个注释系统，因此创建示例页面更简单，如简短的[创建示例页面](/help/communities/create-sample-page.md)教程中所述。

创建后，进入设计模式并使自定义组件组可用，以允许将`Alt Comments`组件添加到页面。

要使注释正常显示和运行，必须将注释的客户端库添加到页面的clientlibs列表中（请参阅[Clientlibs for Communities Components](/help/communities/clientlibs.md)）。

#### 示例页面{#comments-clientlibs-on-sample-page}上的注释Clientlibs

![comments-clientlibs-crxde](assets/comments-clientlibs-crxde.png)

#### 作者：示例页面{#author-alt-comment-on-sample-page}上的Alt注释

![alt-comment](assets/alt-comment.png)

#### 作者：示例页面注释节点{#author-sample-page-comments-node}

您可以通过查看示例页面`/content/sites/sample/en/jcr:content/content/primary/comments`中注释节点的属性来验证CRXDE中的resourceType。

![verify-comment-crxde](assets/verify-comment-crxde.png)

#### 发布示例页面{#publish-sample-page}

将自定义组件添加到页面后，还需要(re)[发布页面](/help/communities/sites-console.md#publishing-the-site)。

#### 发布：示例页面{#publish-alt-comment-on-sample-page}上的Alt注释

发布自定义应用程序和示例页面后，可以输入评论。 登录后，无论是使用[演示用户](/help/communities/tutorials.md#demo-users)还是管理员，都可以发布评论。

以下是aaron.mcdonald@mailinator.com发布评论：

![publish-alt-comment](assets/publish-alt-comment.png)

![publish-alt-comment1](assets/publish-alt-comment1.png)

现在，扩展组件在默认外观上工作正常，是时候修改外观了。
