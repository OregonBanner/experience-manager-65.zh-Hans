---
title: Tag Essentials
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

# Tag Essentials {#tag-essentials}

在启用“标记”的情况下配置AEM Communities组件后，社区成员将能够标记他们在发布环境中发布的内容。

发布环境中应用的标记的基础基础架构与创作环境中应用于内容（如页面和资产）的标记的基础基础架构相同：

* 参见 [管理标记](../../help/sites-administering/tags.md) 和 [标记用户生成的内容](tag-ugc.md) (UGC)，以获取有关创建和管理标记的信息。

* 参见 [为开发人员添加标记](../../help/sites-developing/tags.md) 了解有关 [标记框架](../../help/sites-developing/framework.md) 以及在中包含和扩展标记 [自定义应用程序](../../help/sites-developing/building.md).

* 参见 [使用社交标签云](tagcloud.md) 供作者参考，了解如何添加 `social tag cloud` 页面中的组件，用于突出显示发布环境中应用于UGC的标记。

* 参见 [标记启用资源](tag-resources.md) 有关为目录标记资源的信息。

可以在配置 [社区站点](sites-console.md#tagging) 或以下功能之一：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md)
* [问题与解答](working-with-qna.md)

## 适用于客户端的Essentials {#essentials-for-client-side}

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
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
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
   <td>参见 <a href="tagcloud.md">使用社交标签云</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端Essentials {#essentials-for-server-side}

* [社交标记云API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交标签管理器](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [服务器端自定义](server-customize.md)

## 标记搜索 {#tag-searching}

截至 [功能包1](deploy-communities.md#latestfeaturepack) (FP1)，使用执行标签搜索 [标记标题](../../help/sites-developing/framework.md#tag-characteristics).

在FP1之前，搜索是使用 [标记id](../../help/sites-developing/framework.md#tagid).
