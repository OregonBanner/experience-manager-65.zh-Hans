---
title: 使用SRP访问UGC
seo-title: 使用SRP访问UGC
description: 将站点配置为使用ASRP或MSRP时，实际UGC不会存储在AEM的节点存储(JCR)中
seo-description: 将站点配置为使用ASRP或MSRP时，实际UGC不会存储在AEM的节点存储(JCR)中
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# 使用SRP访问UGC{#accessing-ugc-with-srp}

## 关于SRP {#about-srp}

所有AEM Communities组件和功能都构建在 [social组件框架(SCF)上](/help/communities/scf.md)，该框架调用SocialResourceProvider API以访问所有用户生成的内容(UGC)。

在创建社区站点之前，必 [须配置存储资源提供者(SRP)](/help/communities/working-with-srp.md) ，以选择与基础拓扑一致的 [实现](/help/communities/topologies.md)。 SRP实现基于三个存储选项：

1. [ASRP](/help/communities/asrp.md) - Adobe点播存储
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## 关于UGC存储 {#about-ugc-storage}

有关UGC存储的重要信息是，将站点配置为使用ASRP或MSRP时，实际UGC不会存储在AEM的节 [点存储](/help/sites-deploying/data-store-config.md) (JCR)中。

虽然JCR中可能存在使UGC阴影的节点以提供有用的元数据，但这些节点不应与实际UGC混淆。

请参 [阅存储资源提供者概述。](/help/communities/srp.md)

## 最佳实践 {#best-practice}

在开发自定义组件时，开发人员应当注意独立于当前选择的拓扑进行编码，从而保持将来转向新拓扑的灵活性。

### 假定JCR不可用 {#assume-jcr-not-available}

应避免特定于JCR的方法。

使用方法：

* Sling API(Sling Resource)

   * 不假定有JCR节点

* OSGi事件

   * 不要假设存在JCR事件

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

要避免的方法：

* 节点API
* JCR事件
* 工作流启动程序（使用JCR事件）

### 使用搜索集合 {#use-search-collections}

不同的SRP可以具有不同的本机查询语言。 建议使用com.adobe.cq.so [cial.ugc.api包中的方法来运行相应的查询语言](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 。

有关详细信息，请参 [阅Search Essentials](/help/communities/search-implementation.md)。

## 资源 {#resources}

* [社区内容存储](/help/communities/working-with-srp.md) -讨论UGC公用存储的可用SRP选项
* [存储资源提供者概述](/help/communities/srp.md) -介绍和存储库使用概述
* [SRP和UGC Essentials](/help/communities/srp-and-ugc.md) - SRP实用程序方法和示例
* [Search Essentials](/help/communities/search-implementation.md) —— 用于搜索UGC的基本信息
* [SocialUtils重构](/help/communities/socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法

