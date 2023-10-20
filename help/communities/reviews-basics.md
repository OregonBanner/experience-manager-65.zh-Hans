---
title: 审核要点
description: 了解AEM Communities中的审阅如何是一个基于注释系统的复合组件，其中包含一个或多个评级（记帐）组件。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# 审核要点 {#reviews-essentials}

此功能包含两个可协同工作的组件：审阅和审阅摘要。

审阅是一个基于的复合组件 [评论系统](essentials-comments.md) 包含一或多个 [评级](rating-basics.md) （按）组件。

不支持评论的匿名发布。 网站访客必须注册并登录才能添加审核。 已登录的访客（成员）可随时更新其审核。

## 适用于客户端的Essentials {#essentials-for-client-side}

### 审核 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是 — 属性可在以下位置编辑： <i>设计 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>请参阅 <a href="reviews.md">使用审阅</a></td>
  </tr>
 </tbody>
</table>

### 审核摘要 {#review-summary}

| **resourceType** | social/review/components/hbs/summary |
|---|---|
| [**可包含**](scf.md#add-or-include-a-communities-component) | 是 — 可在*设计*模式下编辑属性 |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **模板** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **属性** | 请参阅 [使用审阅](reviews.md) |

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [审核API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [审核端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已发布的审核(UGC) {#accessing-posted-reviews-ugc}

UGC应使用标准审核方法之一进行审核。
请参阅 [审核用户生成的内容](moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用存储](working-with-srp.md) for UGC包括对UGC的编程访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）是什么。

**UGC在存储库中的位置和格式可能会发生更改，恕不发出警告**.

请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法。
