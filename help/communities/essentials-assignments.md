---
title: Assignments Essentials
seo-title: Assignments Essentials
description: 支持社区的任务功能概述
seo-description: 支持社区的任务功能概述
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 11%

---


# Assignments Essentials {#assignments-essentials}

阅读以了解使用[启用社区](/help/communities/overview.md#enablement-community)站点的任务功能的基本信息。

分配功能是将支持资源和学习路径分配给支持社区的成员。

## 客户端{#essentials-for-client-side}的必备工具

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>请参阅<a href="/help/communities/assignments.md">任务功能</a></td>
  </tr>
 </tbody>
</table>

### 完成和成功状态{#completion-and-success-status}

“工作总揽”的报告和状态横幅中使用“完成”和“成功”状态。

完成状态:

* 未指定
* 未开始（新）
* 进行中
* 完成

成功状态:

* 未知
* Pass
* 失败

完成状态和成功状态的唯一可能组合是：

| **完成** | **成功** |
|---|---|
| 未启动 | 未知 |
| 进行中 | 未知 |
| 完成 | Pass |
| 完成 | 失败 |

## 服务器端{#essentials-for-server-side}的必备工具

### 指定任务功能 {#assignments-function}

包含[分配函数](/help/communities/functions.md#assignments-function)的社区站点结构包括已配置的` [assignments](/help/communities/assignments.md)`组件。

### 参考API {#reference-apis}

* [Enablement API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [报告API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [报告分析API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)

