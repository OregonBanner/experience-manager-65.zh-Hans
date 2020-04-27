---
title: 问题与解答基本功能
seo-title: 问题与解答基本功能
description: 问题与答案论坛功能
seo-description: 问题与答案论坛功能
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
translation-type: tm+mt
source-git-commit: ca15258a5dc7ca99b6c9d6ae85e42c77a3802c87

---


# 问题与解答基本功能 {#qna-essentials}

本页提供了有关使用问题与答案(QnA)论坛功能的基本信息。

## 客户端必备工具 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">可包含</a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientlibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.porting<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> 模板</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> 属性</td>
   <td>查看 <a href="working-with-qna.md">问题与答案论坛功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端必备工具 {#essentials-for-server-side}

* [问题与解答API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [问题与解答端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 问题与解答功能 {#qna-function}

包含 [QnA功能的社区站点结构将具有已配置的](functions.md#qna-function)`QnA` 组件，以及影响协调和标记的设置。 QnA函数支持标识特 [权成员用户组](users.md#privileged-members-group)。

### 访问问题与解答论坛帖子(UGC) {#accessing-qna-forum-posts-ugc}

UGC应使用一种标准的仲裁方法进行仲裁。
请参阅 [审核用户生成的内容](moderate-ugc.md)。

自AEM 6.1 Communities起，对UGC使用公 [用商店](working-with-srp.md) ，包括以编程方式访问UGC，而不管选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP](accessing-ugc-with-srp.md) —— 编码准则访问UGC。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。

