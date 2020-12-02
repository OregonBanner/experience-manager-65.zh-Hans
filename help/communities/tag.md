---
title: Tag Essentials
seo-title: Tag Essentials
description: 标记概述
seo-description: 标记概述
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# Tag Essentials {#tag-essentials}

当AEM Communities组件配置为启用标记时，社区成员能够标记他们在发布环境中发布的内容。

发布环境中应用的标记的基础结构与在创作环境中应用于内容的标记的基础结构相同，如页面和资产：

* 有关创建和管理标记的信息，请参阅[管理标记](../../help/sites-administering/tags.md)和[标记用户生成的内容](tag-ugc.md)(UGC)。

* 有关[标记框架](../../help/sites-developing/framework.md)以及在[自定义应用程序](../../help/sites-developing/building.md)中包括和扩展标记的信息，请参阅[开发人员标记](../../help/sites-developing/tags.md)。

* 有关作者如何向页面添加`social tag cloud`组件以在发布环境中突出显示应用于UGC的标记的信息，请参阅[使用社交标记云](tagcloud.md)。

* 有关为目录标记资源的信息，请参阅[标记Enablement Resources](tag-resources.md)。

在配置[社区站点](sites-console.md#tagging)或下列功能之一时，可以启用UGC标记：

* [博客](blog-feature.md)
* [日历](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md)
* [问题与解答](working-with-qna.md)

## 客户端{#essentials-for-client-side}的必备工具

### 社交标记云 {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>请参阅<a href="tagcloud.md">使用社交标记云</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端{#essentials-for-server-side}的必备工具

* [社交标记云API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交标签管理器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [服务器端自定义](server-customize.md)

## 标记搜索{#tag-searching}

从[功能包1](deploy-communities.md#latestfeaturepack)(FP1)开始，使用[标记标题](../../help/sites-developing/framework.md#tag-characteristics)执行标记搜索。

在FP1之前，使用[标记id](../../help/sites-developing/framework.md#tagid)执行搜索。
