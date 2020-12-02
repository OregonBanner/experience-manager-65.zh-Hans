---
title: 论坛基础
seo-title: 论坛基础
description: 论坛概述
seo-description: 论坛概述
uuid: 68849582-8742-40be-9e7e-0b574ae38815
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 059c5bbe-07eb-4873-8157-2196df887b27
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%

---


# Forum Essentials {#forum-essentials}

本页提供了使用论坛功能的基本信息。

## 客户端{#essentials-for-client-side}的必备工具

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>social/forum/components/hbs/forum<br /> social/forum/components/hbs/topic<br /> social/forum/components/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.porting<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>请参阅<a href="forum.md">论坛功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端{#essentials-for-server-side}的必备工具

* [论坛API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [论坛端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 论坛功能 {#forum-function}

包含[论坛功能](functions.md#forum-function)的社区站点结构包括已配置的`forum`组件，以及影响协调、标记和翻译的设置。

### 访问论坛帖子(UGC){#accessing-forum-posts-ugc}

UGC应使用一种标准的协调方法进行仲裁。
请参阅[协调用户生成的内容](moderate-ugc.md)。

自AEM 6.1社区起，对UGC使用[公用商店](working-with-srp.md)包括对UGC的程序化访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP实用程序方法和示例。
* [使用SRP编码准则](accessing-ugc-with-srp.md) 访问UGC。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。

