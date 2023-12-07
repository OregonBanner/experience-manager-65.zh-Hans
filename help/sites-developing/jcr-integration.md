---
title: JCR集成
description: 了解一些需要在JCR级别与Adobe Experience Manager集成时的提示。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# JCR集成{#jcr-integration}

## 与JCR API相比，首选Sling资源API {#prefer-the-sling-resource-api-to-jcr-api}

Sling API的工作级别比JCR API更高、更抽象。 这使您的代码可以更好地重用，并且独立于底层存储。 这样可根据需要通过ResourceProvider机制更容易包含外部虚拟数据。

## 尽可能避免查询 {#avoid-queries-wherever-possible}

在存储库中导航以检索数据总是比运行查询更快。 在某些情况下，查询是必需的，例如最终用户查询，或者需要从整个存储库中查找结构化内容，但在所有其他情况下，最好导航到必要的节点。 应始终避免在渲染逻辑中进行查询，如导航组件、“最近项目列表”、项目计数等。 在这些情况下，最好是遍历层级或预缓存结果，以便在渲染时可以直接使用。

## 限制JCR观察的范围 {#restrict-the-scope-of-jcr-observation}

在侦听存储库中的事件时，必须尽可能缩小范围。 例如，在以下位置监听事件会更好： `/etc/mycompany` 而不是去听 `/etc`. 永远不要监听存储库根目录中的事件。 此外，请确保在没有可执行的操作时，尽快执行回调方法。

## 消除JCR管理访问权限的使用 {#eliminate-use-of-jcr-admin-access}

自AEM 6起，登录管理功能已弃用，从ResourceResolverFactory获取管理会话的功能也已弃用。 而是应该为需要此类访问权限的后台操作创建服务帐户，并且可以使用ResourceResolverFactory为此帐户获取ResourceResolver。
