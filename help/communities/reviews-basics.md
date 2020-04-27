---
title: Reviews Essentials
seo-title: Reviews Essentials
description: 审阅和审阅摘要组件
seo-description: 审阅和审阅摘要组件
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Reviews Essentials {#reviews-essentials}

此功能由两个可协同工作的组件组成：审阅和审阅摘要。

审阅是基于包含一个或多个评 [级(计数](essentials-comments.md) )组件的注释系 [统的](rating-basics.md) 复合组件。

不支持匿名发布审阅。 站点访客必须注册并登录才能添加审阅。 已签署的访客（会员）可随时更新其审阅。

## 客户端必备工具 {#essentials-for-client-side}

### 审核 {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/reviews/components/hbs/reviews</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是——在设计模式下可编辑 <i>属 </i>性</td>
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
   <td>请参阅 <a href="reviews.md">使用审阅</a></td>
  </tr>
 </tbody>
</table>

### 审核摘要 {#review-summary}

| **resourceType** | social/reviews/components/hbs/summary |
|---|---|
| [**可包含&#x200B;**](scf.md#add-or-include-a-communities-component) | 是——属性可在*design *mode中编辑 |
| [**clientlibs **](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **模板** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **属性** | 请参阅 [使用审阅](reviews.md) |

* [客户端自定义](client-customize.md)

## 服务器端必备工具 {#essentials-for-server-side}

* [审阅API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [审阅端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已发布的审阅(UGC) {#accessing-posted-reviews-ugc}

UGC应使用一种标准的仲裁方法进行仲裁。
请参阅 [审核用户生成的内容](moderate-ugc.md)。

自AEM 6.1 Communities起，对UGC使用公 [用商店](working-with-srp.md) ，包括以编程方式访问UGC，而不管选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP](accessing-ugc-with-srp.md) —— 编码准则访问UGC。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。

