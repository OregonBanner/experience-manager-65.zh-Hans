---
title: 工作总揽
seo-title: 工作总揽
description: 启用社区的工作总揽功能概述
seo-description: 启用社区的工作总揽功能概述
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
exl-id: 75cef5da-4f93-4721-99c0-ad44c8ab76d4
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 11%

---

# 工作总揽 {#assignments-essentials}

阅读并了解有关使用[启用社区](/help/communities/overview.md#enablement-community)站点的分配功能的基本信息。

分配功能是将支持资源和学习路径分配给支持社区的成员的功能。

## 客户端要点 {#essentials-for-client-side}

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
   <td>请参阅<a href="/help/communities/assignments.md">工作总揽功能</a></td>
  </tr>
 </tbody>
</table>

### 完成和成功状态 {#completion-and-success-status}

“工作总揽”上的报表和状态横幅中使用“完成”和“成功”状态。

完成状态:

* 未指定
* 未开始（新）
* 进行中
* 完成

成功状态:

* 未知
* 通过
* 失败

完成状态和成功状态的唯一可能组合包括：

| **完成** | **成功** |
|---|---|
| 未启动 | 未知 |
| 进行中 | 未知 |
| 完成 | 通过 |
| 完成 | 失败 |

## 服务器端要点 {#essentials-for-server-side}

### 指定任务功能 {#assignments-function}

包括[分配函数](/help/communities/functions.md#assignments-function)的社区站点结构包括配置的` [assignments](/help/communities/assignments.md)`组件。

### 参考API {#reference-apis}

* [启用API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [报表API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [报表分析API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
