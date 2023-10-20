---
title: 标签要点
description: 了解Tally如何作为一个抽象类，提供从成员那里收集关于他们如何评价特定产品和服务的反馈的标准方法。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 标签要点 {#tally-essentials}

Tally是一个抽象类，它提供了一种标准方法，用于收集成员关于他们如何评价特定产品和服务的反馈。 不支持匿名反馈。 网站访客必须注册并登录才能参与并登录以更改其反馈。 登录要求通过阻止多个帖子来促进审核并提高反馈的价值。

通过扩展抽象tally类，可创建自定义的tally组件。

[点赞](essentials-liking.md) 是一种简单的计数的实现方式，表达积极的观点。

[投票](essentials-voting.md) 是一种简单形式的计数的实现，用于表达积极或消极的观点。

[评级](rating-basics.md) 是一种使用星形系统表示从正面到负面的一系列意见的计数的实现。

自AEM 6.1起，轮询组件不再可用。

[审核](reviews-basics.md) 是一个SCF组件，它是 [评论](essentials-comments.md) 和 [评级](rating-basics.md).

## 适用于客户端的Essentials {#essentials-for-client-side}

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [标签API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [标签端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已过帐的表(UGC) {#accessing-posted-tallies-ugc}

UGC应使用标准审核方法之一进行审核。
请参阅 [审核用户生成的内容](moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用存储](working-with-srp.md) for UGC包括对UGC的编程访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）是什么。

**UGC在存储库中的位置和格式可能会发生更改，恕不发出警告**.

请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法。
