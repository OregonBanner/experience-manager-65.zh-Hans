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

---


# Tag Essentials {#tag-essentials}

在配置AEM Communities组件并启用标记后，社区成员可以标记他们在发布环境中发布的内容。

发布环境中应用的标记的基础结构与创作环境中应用于内容的标记（如页面和资产）的基础结构相同：

* 有关创 [建和管理标记](../../help/sites-administering/tags.md) ，请参 [阅管理标记和标记用户生成的内容](tag-ugc.md) (UGC)。

* See [Tagging for Developers](../../help/sites-developing/tags.md) for information about the [tagging framework](../../help/sites-developing/framework.md) as well as including and extending tags in [custom applications](../../help/sites-developing/building.md).

* 有关如 [何向页面添加组件以突出显示在发布环境中应用于UGC的标记的信息，请参阅使](tagcloud.md)`social tag cloud` 用社交标记云。

* 有关目 [录的标记资源](tag-resources.md) ，请参阅标记启用资源。

在配置社区站点或以下功能之一时 [可启用](sites-console.md#tagging) UGC标记：

* [博客](blog-feature.md)
* [日历](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md)
* [问题与解答](working-with-qna.md)

## 客户端必备工具 {#essentials-for-client-side}

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
   <td>请参 <a href="tagcloud.md">阅使用社交标记云</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端必备工具 {#essentials-for-server-side}

* [Social Tag Cloud API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交标签管理器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [服务器端自定义](server-customize.md)

## 标记搜索 {#tag-searching}

从功 [能包1](deploy-communities.md#latestfeaturepack) (FP1)开始，使用标签标题执行标 [签搜索](../../help/sites-developing/framework.md#tag-characteristics)。

在FP1之前，使用标签id执行 [搜索](../../help/sites-developing/framework.md#tagid)。
