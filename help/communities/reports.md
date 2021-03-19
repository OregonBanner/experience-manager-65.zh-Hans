---
title: 报表控制台
seo-title: 报表控制台
description: 了解如何访问报告
seo-description: 了解如何访问报告
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 7%

---


# 报表控制台{#reports-console}

## 概述 {#overview}

对于AEM Communities，有各种报表可以通过多种方式从作者环境访问。

一般而言，各种报告包括：

* [指定报表](#assignments-report)

   对于[启用社区](/help/communities/overview.md#enablement-community)，提供学员分配进度的概览，包括在实施SCORM标准时的相关得分。

* [查看次数报表](#views-report)

   提供按社区成员和任何社区站点的站点访客的视图图。

* [发布报表](#posts-report)

   提供社区成员向任何社区站点发布的各种类型帖子的图表。

启用[Adobe Analytics](/help/communities/sites-console.md#analytics)时，报告将包括一段时间内每个启用资源的视图、播放、评论和评级数。

表格报表可以以.csv格式导出，以便后续处理。

## 报告控制台{#reporting-consoles}

### 社区站点{#reports-for-community-sites}的报告

* 从全局导航：**[!UICONTROL 导航]** > **[!UICONTROL Communities]** > **[!UICONTROL 报告]**

* 选择：

   * **[!UICONTROL 指定报表]**

      * 为选定的社区站点、用户或组以及分配生成报告。
   * **[!UICONTROL 发布报表]**

      * 为所选社区站点、内容类型和时间段生成报告。
   * **[!UICONTROL 查看次数报表]**

      * 为所选社区站点、内容类型和时间段生成报告。



![报告](assets/reports1.png)

### Enablement Resources和学习路径报告{#reports-for-enablement-resources-and-learning-paths}

* 从全局导航：**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 资源]**

* 选择现有的教育社区站点：

   * 选择&#x200B;**报表**&#x200B;图标以生成涵盖所有启用资源的报表。
   * 选择支持学习路径。
   * 选择&#x200B;**报表**&#x200B;图标以生成以下报表：

      * 包含的支持资源。
      * 分配给学习路径的学员。

* 这些报告提供：

   * 表格数据，可下载为CSV:

      * 识别学员
      * 他们的地位
      * 是指派还是通过目录访问
      * 所作评论的数量
      * 给定星级

有关详细信息，请参阅“资源”控制台的[报告部分](/help/communities/resources.md#report)。

## 指定报表 {#assignments-report}

“任务”控制台允许按Enablement Community站点、用户或用户组以及任务分配筛选报表。

报告提供了有关其进展情况的信息以及提供的任何评论或评级。

![赋值报表](assets/assignment-report.png)

选择报表的条件：

* **站点**

   选择一个Enablement Community站点。

* **用户或组**
   * 选择“用户”为一个学员生成报告。
   * 选择“组”以为一组学员生成报表。

   隧道服务将从发布环境访问成员和成员组。

* **指定任务**

   从分配给选定学员的启用资源中进行选择。

选择&#x200B;**生成**&#x200B;以创建报表：

![generate-report](assets/generate-assignment-report.png)

## 查看次数报表 {#views-report}

“视图”控制台允许在指定时间段内按社区功能在页面视图上生成报表。

![视图报告](assets/view-report.png)

选择报表的条件：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“全部”内容或选择站点上存在的功能之一。

* **[!UICONTROL 时间范围]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择&#x200B;**[!UICONTROL 生成]**&#x200B;以创建报表。

![生成视图](assets/generate-views.png)

## 发布报表 {#posts-report}

帖子控制台允许在指定时间段内生成针对社区功能的帖子数的报告。

![帖子 — 报告](assets/posts-report.png)

选择报表的条件：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“全部”内容或选择站点上存在的功能之一。

* **[!UICONTROL 时间范围]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择&#x200B;**[!UICONTROL 生成]**&#x200B;以创建报表。

![generate-report](assets/generate-posts-report.png)

## 疑难解答 {#troubleshooting}

### 未列出社区站点{#no-community-sites-listed}

如果未列出社区站点，请确保已为站点启用Adobe Analytics。 如果选择分配报告，请确保分配功能位于社区站点的结构中。

### 报告不显示在AEM作者实例{#reports-do-not-show-in-aem-author-instance}中

如果报表未显示在AEM作者实例中，请检查自定义项，如发布实例上的URL映射。 如果仅对社区站点的AEM发布实例执行URL映射，请确保已在&#x200B;**站点趋势报表社交组件工厂**&#x200B;配置的AEM作者实例中配置了URL映射。

![AEM作者上的URL映射](assets/sitetrend.png)