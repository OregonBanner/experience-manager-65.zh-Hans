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

---


# Tally Essentials {#tally-essentials}

Tally是一个抽象类，它提供了从成员那里收集反馈的标准方法，这些反馈是关于他们如何评价特定产品和服务。 不支持匿名反馈。 站点访客必须注册并登录才能参加和登录以更改其反馈。 登录要求有助于协调，并通过阻止多个帖子来提高反馈的价值。

可通过扩展抽象计数类来创建自定义计数组件。

[喜欢](essentials-liking.md) ，是一种简单的表达积极意见的方式，

[投票](essentials-voting.md) ，是一种简单的表达正面或负面意见的方式。

[评级](rating-basics.md) 是一种实施统计的方法，它使用星形系统来表达从正面到负面的各种意见。

自AEM 6.1起，投票组件不再可用。

[审阅](reviews-basics.md) 是一个SCF组件，它是评论和评级的 [混合](essentials-comments.md)[组件](rating-basics.md)。

## 客户端必备工具 {#essentials-for-client-side}

* [客户端自定义](client-customize.md)

## 服务器端必备工具 {#essentials-for-server-side}

* [Tally API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [计数端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已发布的计数(UGC) {#accessing-posted-tallies-ugc}

UGC应使用一种标准的仲裁方法进行仲裁。
请参阅 [审核用户生成的内容](moderate-ugc.md)。

自AEM 6.1 Communities起，对UGC使用公 [用商店](working-with-srp.md) ，包括以编程方式访问UGC，而不管选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP](accessing-ugc-with-srp.md) —— 编码准则访问UGC。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。

