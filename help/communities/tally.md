---
title: 计数要点
seo-title: Tally Essentials
description: 计数类概述
seo-description: Tally class overview
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 计数要点 {#tally-essentials}

Tally是一个抽象类，它提供了一种从成员那里收集反馈的标准方法，来了解他们如何评价特定的产品和服务。 不支持匿名反馈。 网站访客必须注册并登录才能参与并登录才能更改其反馈。 登录要求有助于审核，并通过阻止多个帖子来提高反馈的价值。

可通过扩展抽象计数类来创建自定义计数组件。

[称赞](essentials-liking.md) 是一种简单的表达积极意见的方式。

[投票](essentials-voting.md) 是一种简单的表达正面或负面意见的理解。

[评级](rating-basics.md) 是使用星形系统表达从正面到负面的一系列观点的计数实施。

自AEM 6.1起，投票组件不再可用。

[评论](reviews-basics.md) 是SCF组件，它是 [评论](essentials-comments.md) 和 [评级](rating-basics.md).

## 客户端要点 {#essentials-for-client-side}

* [客户端自定义](client-customize.md)

## 服务器端要点 {#essentials-for-server-side}

* [计数API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [计数端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已发布的计数(UGC) {#accessing-posted-tallies-ugc}

UGC应使用其中一种标准审核方法进行审核。
请参阅 [审核用户生成的内容](moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用商店](working-with-srp.md) 对于UGC，包括以编程方式访问UGC，而不考虑选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**.

请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用概述。
* [SRP和UGC要点](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法。
