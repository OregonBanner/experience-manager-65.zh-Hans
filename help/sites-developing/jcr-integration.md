---
title: JCR集成
seo-title: JCR集成
description: 必须在JCR级别集成的提示
seo-description: 必须在JCR级别集成的提示
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# JCR集成{#jcr-integration}

## 比JCR API {#prefer-the-sling-resource-api-to-jcr-api}首选Sling资源API

Sling API的工作级别比JCR API更高、更抽象。 这样，您的代码就可以更加可重用，并且更独立于底层存储。 这样，在需要时便可以通过ResourceProvider机制包含外部虚拟数据。

## 尽量避免查询{#avoid-queries-wherever-possible}

与运行查询相比，浏览存储库以检索数据的速度总是更快。 在某些情况下，需要进行查询，例如最终用户查询，或需要从整个存储库中查找结构化内容，但是对于所有其他情况，最好导航到必要的节点。 在呈现逻辑中应始终避免出现查询，例如导航组件、“最近的项目列表”、项目计数等。 在这些情况下，最好浏览层次结构或预缓存结果，以便在渲染时直接使用。

## 限制JCR观测范围{#restrict-the-scope-of-jcr-observation}

在监听存储库中的事件时，务必尽可能缩小范围。 例如，在`/etc/mycompany`侦听事件比在`/etc`侦听事件好得多。 切勿监听存储库根目录中的事件。 此外，请确保当回调方法不可执行时，尽可能快地执行它们。

## 消除对JCR管理员访问{#eliminate-use-of-jcr-admin-access}的使用

自AEM 6起，已弃用登录管理，从ResourceResolverFactory获取管理会话也已弃用。 而是应该为需要此类访问权限的后台操作创建服务帐户，并且ResourceResolverFactory可用于获取此帐户的ResourceResolver。
