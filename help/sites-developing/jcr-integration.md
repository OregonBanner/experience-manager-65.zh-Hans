---
title: JCR集成
seo-title: JCR Integration
description: 关于何时必须在JCR级别集成的提示
seo-description: Tips for when you must integrate at the JCR level
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# JCR集成{#jcr-integration}

## 与JCR API相比，首选Sling资源API {#prefer-the-sling-resource-api-to-jcr-api}

Sling API的工作级别比JCR API更高、更抽象。 这使您的代码可重用性更高，并且独立于底层存储。 这样可以更轻松地根据需要通过ResourceProvider机制包含外部虚拟数据。

## 尽可能避免查询 {#avoid-queries-wherever-possible}

在存储库中导航以检索数据总是比运行查询更快。 在某些情况下，查询是必要的，例如最终用户查询，或者需要从整个存储库中查找结构化内容，但对于所有其他情况，最好导航到必要的节点。 应始终避免在渲染逻辑中进行查询，例如导航组件、“最近项目列表”、项目计数等。 在这些情况下，最好是遍历层级或预缓存结果，以便在渲染时可以直接使用它。

## 限制JCR观察的范围 {#restrict-the-scope-of-jcr-observation}

在监听存储库中的事件时，必须尽可能缩小范围。 例如，在以下位置监听事件要好得多： `/etc/mycompany` 而不是去聆听 `/etc`. 绝不监听存储库根目录中的事件。 此外，请确保回调方法在没有可执行的操作时尽快执行。

## 消除JCR管理访问权限的使用 {#eliminate-use-of-jcr-admin-access}

自AEM 6起，登录管理已弃用，从ResourceResolverFactory获取管理会话的方式也是如此。 而是应该为需要此类访问权限的后台操作创建服务帐户，并且可以使用ResourceResolverFactory获取此帐户的ResourceResolver。
