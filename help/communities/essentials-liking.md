---
title: 点赞Essentials
description: 了解如何使用赞组件，该组件是一个有用的工具，允许成员通过选择中心图标来表达对某些内容的积极看法。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
pagetitle: Liking Essentials
exl-id: ef314385-cd5c-411c-91df-83691a81c1bc
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 点赞Essentials {#liking-essentials}

点赞组件， [总计](tally.md) 子类是一种非常有用的工具，它允许成员通过简单地选择心形图标来表达对特定内容的积极看法。

允许将链接组件的多个实例放在同一页面上；必须为每个实例配置一个唯一的 `tally name` 属性。

不支持类似内容的匿名发布。 网站访客必须注册并登录才能参与点击。 已登录的访客（成员）可随时进行打开和关闭之类的切换。

## 适用于客户端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/liking</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是 — 属性可在以下位置编辑： <i>设计 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.liking</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td><p> /libs/social/tally/components/hbs/liking/liking.hbs<br /> /libs/social/tally/components/hbs/liking/activity-icon.hbs<br /> /libs/social/tally/components/hbs/liking/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/liking/clientlibs/likingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td><p>请参阅 <a href="liking.md">使用点赞</a></p> </td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [标签API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [标签端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已过帐投票(UGC) {#accessing-posted-voting-ugc}

UGC应使用标准审核方法之一进行审核。
请参阅 [审核用户生成的内容](moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用存储](working-with-srp.md) for UGC包括对UGC的编程访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）是什么。

**UGC在存储库中的位置和格式可能会发生更改，恕不发出警告**.

请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法。
