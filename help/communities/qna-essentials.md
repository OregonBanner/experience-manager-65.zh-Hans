---
title: 问题与解答要点
description: 了解在Adobe Experience Manager社区中使用问题与解答(QnA)论坛功能的基础知识。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# 问题与解答要点 {#qna-essentials}

本页提供了有关使用问答(QnA)论坛功能的基本信息。

## 适用于客户端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">include</a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.qna</td>
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
   <td>请参阅 <a href="working-with-qna.md">问答论坛功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [问题与解答API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [问题与解答端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 问题与解答功能 {#qna-function}

社区站点结构包括 [问题与解答功能](functions.md#qna-function) 已配置 `QnA` 影响审核和标记的组件和设置。 QnA函数支持识别 [特权成员用户组](users.md#privileged-members-group).

### 访问问题与解答论坛帖子(UGC) {#accessing-qna-forum-posts-ugc}

UGC应使用标准审核方法之一进行审核。
请参阅 [审核用户生成的内容](moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用存储](working-with-srp.md) for UGC包括对UGC的编程访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）是什么。

**UGC在存储库中的位置和格式可能会发生更改，恕不发出警告**.

请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法。
