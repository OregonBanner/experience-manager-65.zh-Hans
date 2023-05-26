---
title: 使用SRP访问UGC
seo-title: Accessing UGC with SRP
description: 当站点配置为使用ASRP或MSRP时，实际的UGC不会存储在AEM节点存储(JCR)中
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 使用SRP访问UGC {#accessing-ugc-with-srp}

## 关于SRP {#about-srp}

所有AEM Communities组件和功能都基于 [社交组件框架(SCF)](/help/communities/scf.md)，用于调用SocialResourceProvider API以访问所有用户生成的内容(UGC)。

在创建社区站点之前， [存储资源提供程序(SRP)](/help/communities/working-with-srp.md) 必须配置为选择与基础实施一致的实施 [拓扑](/help/communities/topologies.md). SRP实施基于三个存储选项：

1. [ASRP](/help/communities/asrp.md)  — 按需Adobe存储
1. [MSRP](/help/communities/msrp.md) - MongoDb
1. [JSRP](/help/communities/jsrp.md) - JCR

## 关于UGC存储 {#about-ugc-storage}

对于UGC的存储，务必要了解的是，当站点配置为使用ASRP或MSRP时，实际的UGC不会存储在AEM中 [节点存储](/help/sites-deploying/data-store-config.md) (JCR)。

虽然JCR中可能有一些节点遮蔽UGC以提供有用的元数据，但不要将这些节点与实际的UGC混淆。

参见 [存储资源提供程序概述。](/help/communities/srp.md)

## 最佳实践 {#best-practice}

在开发自定义组件时，开发人员应小心独立于当前选择的拓扑进行编码，从而保留将来迁移到新拓扑的灵活性。

### 假设JCR不可用 {#assume-jcr-not-available}

应避免特定于JCR的方法。

使用的方法：

* Sling API（Sling资源）

   * 不要假定存在JCR节点

* OSGi事件

   * 不要假定存在JCR事件

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

避免的方法：

* 节点API
* JCR事件
* 工作流启动器（使用JCR事件）

### 使用搜索收藏集 {#use-search-collections}

不同的SRP可以有不同的本地查询语言。 建议使用来自以下项的方法： [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 包以运行适当的查询语言。

有关更多信息，请参阅 [Search Essentials](/help/communities/search-implementation.md).

## 资源 {#resources}

* [社区内容存储](/help/communities/working-with-srp.md)  — 讨论UGC公用存储的可用SRP选择
* [存储资源提供程序概述](/help/communities/srp.md)  — 简介和存储库使用情况概述
* [SRP和UGC Essentials](/help/communities/srp-and-ugc.md) - SRP实用程序方法和示例
* [Search Essentials](/help/communities/search-implementation.md)  — 搜索UGC的基本信息
* [SocialUtils重构](/help/communities/socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法
