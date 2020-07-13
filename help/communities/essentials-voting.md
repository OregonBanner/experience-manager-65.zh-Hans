---
title: Voting Essentials
seo-title: Voting Essentials
description: 投票组件概述
seo-description: 投票组件概述
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---


# Voting Essentials {#voting-essentials}

投票组件是一个计 [数子类](tally.md) ，是一个有用的工具，它允许成员通过选择向上或向下箭头来指示其意见来对特定内容进行评级。

允许在同一页面上放置一个投票组件的多个实例； 每个实例都必须配置唯一 `tally name` 属性。

不支持匿名发布投票。 网站访客必须注册并登录才能参加投票，已登录的访客（会员）可随时更改投票。

## 客户端必备工具 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/potting</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是——属性在设计模式下 <i>可编 </i>辑</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td><p>请参 <a href="voting.md">阅使用投票</a></p> </td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端必备工具 {#essentials-for-server-side}

* [计数API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [计数端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已过帐的投票(UGC) {#accessing-posted-voting-ugc}

UGC应使用一种标准的协调方法进行仲裁。
请参 [阅调节用户生成的内容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用UGC的 [公用商店](working-with-srp.md) ，包括以程序方式访问UGC，而不管选择的存储选项（如ASRP、MSRP或JSRP）如何。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md) —— 编码指南。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。

