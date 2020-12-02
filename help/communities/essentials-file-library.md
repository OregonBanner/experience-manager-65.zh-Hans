---
title: File Library Essentials
seo-title: File Library Essentials
description: 使用文件库功能
seo-description: 使用文件库功能
uuid: 0630f13e-97b4-4f93-9dce-07f559287c29
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9019b967-fff8-4dda-bc5a-fd4a3e14a4ef
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 2%

---


# File Library Essentials {#file-library-essentials}

本页提供了使用文件库功能的基本信息。

## 客户端{#essentials-for-client-side}的必备工具

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>社交／文件库／组件/hbs/文件库</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.porting<br /> cq.social.hbs.filelibrary</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/filelibrary.hbs<br /> /libs/social/filelibrary/components/hbs/folder/folder.hbs<br /> /libs/social/filelibrary/components/hbs/folder/item.hbs<br /> /libs/social/filelibrary/components/hbs/document/document.hbs<br /> /libs/social/filelibrary/components/hbs/document/item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/clientlibs/filelibrary.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>请参阅<a href="file-library.md">文件库功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端{#essentials-for-server-side}的必备工具

* [文件库API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [文件库端点](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 文件库功能 {#file-library-function}

包含[文件库函数](functions.md#file-library-function)的社区站点结构包括已配置的`file library`组件。

### 访问针对文件库(UGC){#accessing-comments-posted-for-file-libraries-ugc}发布的注释

UGC应使用一种标准的协调方法进行仲裁。
请参阅[协调用户生成的内容](moderate-ugc.md)。

自AEM 6.1社区起，对UGC使用[公用商店](working-with-srp.md)包括对UGC的程序化访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）。

**UGC在存储库中的位置和格式可能会发生更改，但不会发出警告**。

请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP实用程序方法和示例。
* [使用SRP编码准则](accessing-ugc-with-srp.md) 访问UGC。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。

