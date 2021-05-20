---
title: 评论要点
seo-title: 评论要点
description: 审阅和审阅摘要组件
seo-description: 审阅和审阅摘要组件
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 1%

---

# 评论要点{#reviews-essentials}

此功能包含两个可协同工作的组件：审阅和审阅摘要。

评论是基于[评论系统](essentials-comments.md)的组合组件，该系统包含一个或多个[评分](rating-basics.md)（计数）组件。

不支持匿名发布审阅。 网站访客必须注册并登录才能添加审阅。 已登录的访客（会员）可以随时更新其审阅。

## 客户端{#essentials-for-client-side}的要点

### 审核 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交/评论/组件/hbs/评论</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是 — 在<i>设计</i>模式下可编辑属性</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
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
   <td>请参阅<a href="reviews.md">使用Reviews</a></td>
  </tr>
 </tbody>
</table>

### 审核摘要 {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**可包含**](scf.md#add-or-include-a-communities-component) | 是 — 在*设计*模式下可编辑属性 |
| [**clientlibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **模板** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **属性** | 请参阅[使用Reviews](reviews.md) |

* [客户端自定义](client-customize.md)

## 服务器端{#essentials-for-server-side}的要点

* [审核API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [审阅端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已发布的审阅(UGC){#accessing-posted-reviews-ugc}

UGC应使用其中一种标准审核方法进行审核。
请参阅[审核用户生成的内容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用[用于UGC的公共存储](working-with-srp.md)包括对UGC的编程访问，而不考虑所选的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用工具方法映射到当前SRP实用工具方法。
