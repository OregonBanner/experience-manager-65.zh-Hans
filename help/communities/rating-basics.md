---
title: 评级要点
seo-title: 评级要点
description: 评级组件概述
seo-description: 评级组件概述
uuid: 48ef61ad-be7a-4a6b-a284-23e5bb4f1671
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7dc3ef57-05c3-45d4-ace3-bb3ba6ea768b
exl-id: 49456944-ff0d-4507-b3b8-143c90067573
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# 评级要点{#rating-essentials}

评级组件[tally](tally.md)子类允许在社区成员中签名以对网站上的功能进行评级。

允许在同一页面上放置一个投票组件的多个实例；每个实例都必须使用唯一的`tally name`属性进行配置。

不支持匿名发布评级。 网站访客必须注册并登录才能仅参与一次评级。 已登录的访客（会员）可以随时更改其评级。

## 客户端{#essentials-for-client-side}的要点

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> 社交/计数/组件/hbs/评分</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是 — 在<i>设计</i>模式下可编辑属性</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td><p>请参阅<a href="rating.md">使用Rating</a></p> </td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端{#essentials-for-server-side}的要点

* [计数API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [计数端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已发布的评级(UGC){#accessing-posted-ratings-ugc}

UGC应使用其中一种标准审核方法进行审核。
请参阅[审核用户生成的内容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用[用于UGC的公共存储](working-with-srp.md)包括对UGC的编程访问，而不考虑所选的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法。
