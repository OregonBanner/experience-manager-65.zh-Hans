---
title: 注释要点
description: 注释组件概述
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---

# 注释要点 {#comments-essentials}

此页面提供了使用评论系统（评论组件）的要点，以及管理用户生成的内容(UGC)的选项，该内容在成员发布评论或回复时生成。

评论部件建立一个评论系统，使得每个单独的帖子由一个评论部件（单数）表示。 它是包含在页面上的评论系统。 注释系统在调用时创建单个注释。

## 适用于客户端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是 — 属性在中可编辑 <i>设计 </i>模式</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td> 参见 <a href="comments.md">使用注释</a></td>
  </tr>
 </tbody>
</table>

[客户端自定义](client-customize.md)

### 每页一个实例 {#one-instance-per-page}

分页以及将URL用于缓存和链接要求每个注释系统的URL必须是唯一的。 因此，每个页面只允许一个注释系统实例。

其他功能已经包括注释系统。 这四个关键原则分别是：

* [博客](blog-developer-basics.md)
* [日程表](calendar-basics-for-developers.md)
* [文件库](essentials-file-library.md)
* [论坛](essentials-forum.md)
* [问题与解答](qna-essentials.md)
* [审核](reviews-basics.md)

### 标记原因列表 {#flag-reason-list}

可以通过向应用程序添加flagreasonlist.hbs以覆盖中的内容来自定义标记原因列表

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

这适用于扩展注释系统的任何组件。

## 服务器端Essentials {#essentials-for-server-side}

* [注释API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [评论端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问发表的评论(UGC) {#accessing-posted-comments-ugc}

UGC应使用标准审核方法之一进行审核。
参见 [审核用户生成的内容](moderate-ugc.md).

自AEM 6.1社区起，使用 [公用存储](working-with-srp.md) for UGC包括对UGC的编程访问，而不考虑选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，恕不发出警告**.

请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前的SRP实用程序方法。
