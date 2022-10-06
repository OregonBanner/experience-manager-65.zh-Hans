---
title: 标记要点
seo-title: Tag Essentials
description: 标记概述
seo-description: Tag overview
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 3%

---

# 标记要点 {#tag-essentials}

在配置AEM Communities组件并启用标记后，社区成员便能够标记他们在发布环境中发布的内容。

发布环境中应用的标记的基础结构与在创作环境中应用于内容的标记（如页面和资产）的基础结构相同：

* 请参阅 [管理标记](../../help/sites-administering/tags.md) 和 [标记用户生成的内容](tag-ugc.md) (UGC)以了解有关创建和管理标记的信息。

* 请参阅 [面向开发人员的标记](../../help/sites-developing/tags.md) ，以了解有关 [标记框架](../../help/sites-developing/framework.md) 以及在 [自定义应用程序](../../help/sites-developing/building.md).

* 请参阅 [使用Social标签云](tagcloud.md) 有关如何添加 `social tag cloud` 组件，以突出显示在发布环境中应用于UGC的标记。

* 请参阅 [标记支持资源](tag-resources.md) 有关标记目录资源的信息。

在配置 [社区网站](sites-console.md#tagging) 或以下功能之一：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md)
* [问题与解答](working-with-qna.md)

## 客户端要点 {#essentials-for-client-side}

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
   <td>请参阅 <a href="tagcloud.md">使用Social标签云</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端要点 {#essentials-for-server-side}

* [Social标签云API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交标签管理器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [服务器端自定义](server-customize.md)

## 标记搜索 {#tag-searching}

截至 [功能包1](deploy-communities.md#latestfeaturepack) (FP1)，使用 [标记标题](../../help/sites-developing/framework.md#tag-characteristics).

在FP1之前，使用 [标记id](../../help/sites-developing/framework.md#tagid).
