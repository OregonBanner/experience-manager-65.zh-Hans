---
title: Tag Essentials
description: 了解当社区组件配置为启用标记时，社区成员可以标记他们在发布环境中发布的内容。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 2%

---

# Tag Essentials {#tag-essentials}

在启用“标记”的情况下配置AEM Communities组件后，社区成员将能够标记他们在发布环境中发布的内容。

发布环境中应用的标记的基础基础结构与创作环境中应用于内容的标记的基础基础结构相同，例如页面和资产：

* 请参阅 [管理标记](../../help/sites-administering/tags.md) 和 [标记用户生成的内容](tag-ugc.md) (UGC)。

* 请参阅 [为开发人员添加标记](../../help/sites-developing/tags.md) 有关 [标记框架](../../help/sites-developing/framework.md) 并在中包含和扩展标记 [自定义应用程序](../../help/sites-developing/building.md).

* 请参阅 [使用社交标签云](tagcloud.md) 供作者参考，了解如何添加 `social tag cloud` 页面组件，用于突出显示发布环境中应用于UGC的标记。

配置 [社区站点](sites-console.md#tagging) 或以下功能之一：

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
   <td>请参阅 <a href="tagcloud.md">使用社交标签云</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [社交标记云API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交标签管理器](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [服务器端自定义](server-customize.md)

## 标记搜索 {#tag-searching}

截至 [功能包1](deploy-communities.md#latestfeaturepack) (FP1)，使用执行标签搜索 [标记标题](../../help/sites-developing/framework.md#tag-characteristics).

在FP1之前，使用执行搜索 [标记ID](../../help/sites-developing/framework.md#tagid).
