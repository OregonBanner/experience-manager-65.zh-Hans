---
title: Tally Essentials
seo-title: Tally Essentials
description: 计数类概述
seo-description: 计数类概述
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Tally Essentials {#tally-essentials}

Tally是一个抽象类，它提供一种标准方法，用于收集成员对特定产品和服务的价值的反馈。 不支持匿名反馈。 网站访客必须注册并登录才能参加和登录以更改其反馈。 登录要求有助于协调，并通过阻止多个帖子来提高反馈的价值。

可通过扩展抽象计数类来创建自定义计数组件。

[](essentials-liking.md) Liking是一种简单的表达积极意见的方式。

[沃](essentials-voting.md) 廷格是一种简单的表达积极或消极意见的方法。

[Rating](rating-basics.md) 是一种运用星系系统表达各种观点的统计方法。

自AEM 6.1起，投票组件不再可用。

[查](reviews-basics.md) 看SCF组件，它是评论和评 [](essentials-comments.md) 级的 [混合](rating-basics.md)。

## 客户端{#essentials-for-client-side}的必备工具

* [客户端自定义](client-customize.md)

## 服务器端{#essentials-for-server-side}的必备工具

* [计数API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [计数端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已发布的计数(UGC){#accessing-posted-tallies-ugc}

UGC应使用一种标准的协调方法进行仲裁。
请参阅[协调用户生成的内容](moderate-ugc.md)。

自AEM 6.1社区起，对UGC使用[公用商店](working-with-srp.md)包括对UGC的程序化访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP实用程序方法和示例。
* [使用SRP编码准则](accessing-ugc-with-srp.md) 访问UGC。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。

