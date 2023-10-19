---
title: 博客要点
description: 了解如何将博客功能添加到页面，以便登录社区成员可以发布博客文章。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 2%

---

# 博客要点 {#blog-essentials}

截至AEM 6.1 Communities，博客是一种社区活动。 博客文章现在从发布环境发布，以前，只能在创作环境中创建并发布博客文章。

博客文章现在可由任何社区成员创建，除非限制为拥有权限的成员。

本页提供了使用博客功能的基本信息。

>[!NOTE]
>
>博客功能的基础架构是日志功能。

## 适用于客户端的Essentials {#essentials-for-client-side}

博客功能由两个主要组件组成，可以通过添加 [博客功能](/help/communities/functions.md#blog-function) 或者以创作编辑模式将组件添加到页面。

### 博客 {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>请参阅 <a href="/help/communities/blog-feature.md">博客功能</a></td>
  </tr>
 </tbody>
</table>

### 博客侧栏 {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**可包含**](/help/communities/scf.md#add-or-include-a-communities-component) | 否 |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **模板** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **属性** | 请参阅 [博客功能](/help/communities/blog-feature.md) |

* [客户端自定义](/help/communities/client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [博客API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [博客端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [服务器端自定义](/help/communities/server-customize.md)

### 博客功能 {#blog-function}

社区站点结构包括 [博客功能](/help/communities/functions.md#blog-function) 具有 `Blog` 和 `Blog Sidebar` 组件已配置。 “博客”功能支持识别 [特权成员用户组](/help/communities/users.md#privileged-members-group).

### 访问博客条目(UGC) {#accessing-blog-entries-ugc}

UGC应使用标准审核方法之一进行审核。
请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md).

自AEM 6.1 Communities起，使用 [公用存储](/help/communities/working-with-srp.md) for UGC包括对UGC的编程访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）是什么。

**UGC在存储库中的位置和格式可能会发生更改，恕不发出警告**.

请参阅：

* [存储资源提供程序概述](/help/communities/srp.md)  — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](/help/communities/srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](/help/communities/accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](/help/communities/socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法。

## 主要发布者 {#primary-publisher}

如果部署是发布场，则必须确定轮询计划发布的文章的主要发布者。

请参阅 [主要发布者](/help/communities/deploy-communities.md#primary-publisher) 以了解更多详细信息。

## 允许富媒体 {#allowing-rich-media}

AEM平台会阻止其他网站的链接，以防止XSS攻击，如中所述

* [Protect抵御跨站点脚本(XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

从AEM 6.2开始，以前需要手动进行的修改包含在默认的AntiSamy配置文件中。

通过选择 `Embed Media from External Sites` 图标：

![媒体](assets/media-icon.png)
