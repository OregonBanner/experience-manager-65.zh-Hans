---
title: JCR集成
seo-title: JCR集成
description: 何时必须在JCR级别集成的提示
seo-description: 何时必须在JCR级别集成的提示
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# JCR集成{#jcr-integration}

## 比起JCR API {#prefer-the-sling-resource-api-to-jcr-api}，首选Sling Resource API

Sling API的工作级别比JCR API更高、更抽象。 这使您的代码能够更加可重用，并且更独立于基础存储。 这使得在需要时通过ResourceProvider机制包含外部虚拟数据更加容易。

## 尽可能避免查询{#avoid-queries-wherever-possible}

导航存储库以检索数据的速度始终快于运行查询。 有时需要查询，例如最终用户查询，或需要从整个存储库中查找结构化内容，但对于所有其他情况，则最好导航到必要的节点。 在呈现逻辑(如导航组件、“最近使用的项目列表”、项目计数等)中，应始终避免查询。 在这些情况下，最好遍历层次结构或预缓存结果，以便在渲染后直接使用。

## 限制JCR观察范围{#restrict-the-scope-of-jcr-observation}

在存储库中监听事件时，必须尽可能缩小范围。 例如，在`/etc/mycompany`监听事件比在`/etc`监听要好得多。 切勿在存储库根中侦听事件。 此外，请确保回调方法在无法执行时尽可能快地执行。

## 消除JCR管理员访问{#eliminate-use-of-jcr-admin-access}的使用

自AEM 6起，登录管理已弃用，从ResourceResolverFactory获取管理会话也已弃用。 相反，应为需要此类型访问的后台操作创建服务帐户，并且ResourceResolverFactory可用于为此帐户获取ResourceResolver。
