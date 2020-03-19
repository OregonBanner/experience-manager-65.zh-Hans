---
title: Blog Essentials
seo-title: Blog Essentials
description: 博客概述
seo-description: 博客概述
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
translation-type: tm+mt
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# Blog Essentials {#blog-essentials}

自AEM 6.1 Communities起，博客是社区活动。 博客文章现在从发布环境发布，以前，博客文章只能在创作环境中创建并发布。

博客文章现在可由任何社区成员创建，除非仅限于特权成员。

本页提供了使用博客功能的基本信息。

>[!NOTE]
>
>博客功能的底层基础架构是日志功能。

## 客户端必备工具 {#essentials-for-client-side}

博客功能由两个主要组件组成，这两个组件可通过添加 [Blog功能](/help/communities/functions.md#blog-function) ，或通过在创作编辑模式下将组件添加到页面来使用。

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
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.partiting<br /> cq.social.hbs.journal</td>
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
   <td>查看 <a href="/help/communities/blog-feature.md">博客功能</a></td>
  </tr>
 </tbody>
</table>

### 博客侧栏 {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**可包含&#x200B;**](/help/communities/scf.md#add-or-include-a-communities-component) | 否 |
| [**clientlibs **](/help/communities/clientlibs.md) | cq.social.hbs.journal.sidebar |
| **模板** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **属性** | 查看 [博客功能](/help/communities/blog-feature.md) |

* [客户端自定义](/help/communities/client-customize.md)

## 服务器端必备工具 {#essentials-for-server-side}

* [博客API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [博客端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [服务器端自定义](/help/communities/server-customize.md)

### 博客功能 {#blog-function}

包含 [Blog功能的社区站点结](/help/communities/functions.md#blog-function) 构将配置 `Blog``Blog Sidebar` 和组件。 Blog函数支持标识特权 [成员用户组](/help/communities/users.md#privileged-members-group)。

### 访问博客条目(UGC) {#accessing-blog-entries-ugc}

UGC应使用一种标准的仲裁方法进行仲裁。
请参阅 [审核用户生成的内容](/help/communities/moderate-ugc.md)。

自AEM 6.1 Communities起，对 [UGC使用公用商店](/help/communities/working-with-srp.md) ，包括对UGC的程序化访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）如何。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](/help/communities/srp.md) -介绍和存储库使用概述
* [SRP和UGC Essentials](/help/communities/srp-and-ugc.md) - SRP实用程序方法和示例
* [使用SRP访问UGC](/help/communities/accessing-ugc-with-srp.md) —— 编码指南
* [SocialUtils重构](/help/communities/socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法

## 主发布者 {#primary-publisher}

当部署为发布场时，必须标识将轮询要发布的文章的主发布者。

有关更 [多详细信息](/help/communities/deploy-communities.md#primary-publisher) ，请参阅主发布者。

## 允许富媒体 {#allowing-rich-media}

AEM平台阻止来自其他网站的链接，以防止XSS攻击，如

* [防止跨站点脚本(XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

自AEM 6.2起，之前手动进行的修改将包括在默认的AntiSamy配置文件中。

通过选择图标，富媒体嵌入到博客文 `Embed Media from External Sites` 章中：

![chlimage_1-199](assets/chlimage_1-199.png)

