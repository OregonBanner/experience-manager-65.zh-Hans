---
title: 报告控制台
seo-title: 报告控制台
description: 了解如何访问报告
seo-description: 了解如何访问报告
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 7%

---


# 报告控制台{#reports-console}

## 概述 {#overview}

对于AEM Communities，有各种报告可从作者环境以多种方式访问。

总的来说，各种报告有：

* [指定报表](#assignments-report)

   对于[启用社区](/help/communities/overview.md#enablement-community)，提供学员分配进度的概览，包括在实施SCORM标准时的关联得分。

* [查看次数报表](#views-report)

   提供按社区成员和任何社区站点的站点视图的内容图表。

* [发布报表](#posts-report)

   按社区成员向任何社区站点提供各种类型的帖子图表。

启用[Adobe Analytics](/help/communities/sites-console.md#analytics)时，报告将包括一段时间内每个启用资源的视图、播放、评论和评级数。

表格报表可以以。csv格式导出，供后续处理。

## 报告控制台{#reporting-consoles}

### 社区站点报告{#reports-for-community-sites}

* 从全局导航：**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 报告]**

* 从以下选项中进行选择：

   * **[!UICONTROL 指定报表]**

      * 为所选社区站点、用户或组和分配生成报告。
   * **[!UICONTROL 发布报表]**

      * 为所选社区站点、内容类型和时间段生成报告。
   * **[!UICONTROL 查看次数报表]**

      * 为所选社区站点、内容类型和时间段生成报告。



![报告](assets/reports1.png)

### Enablement Resources和Learning Paths报告{#reports-for-enablement-resources-and-learning-paths}

* 从全局导航：**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 资源]**

* 选择现有的支持社区站点：

   * 选择&#x200B;**报告**&#x200B;图标以生成涵盖所有启用资源的报告。
   * 选择支持学习路径。
   * 选择&#x200B;**报表**&#x200B;图标以生成以下报表：

      * 包含的支持资源。
      * 分配给学习路径的学员数。

* 这些报告提供：

   * 表数据，可下载为CSV:

      * 识别学员
      * 他们的状态
      * 是分配还是通过目录访问
      * 评论数
      * 给定星级

有关详细信息，请参阅“资源”控制台的[报告部分](/help/communities/resources.md#report)。

## 指定报表 {#assignments-report}

分配控制台允许按启用社区站点、用户或用户组以及分配筛选报告。

该报告提供了有关其进度的信息以及提供的任何评论或评级。

![赋值报表](assets/assignment-report.png)

选择报表的条件：

* **站点**

   选择一个支持社区站点。

* **用户或组**
   * 选择“用户”，为一个学员生成报告。
   * 选择“组”以为一组学员生成报告。

   隧道服务将从发布环境访问成员和成员组。

* **指定任务**

   从分配给选定学员的启用资源中进行选择。

选择&#x200B;**生成**&#x200B;以创建报告：

![生成报表](assets/generate-assignment-report.png)

## 查看次数报表 {#views-report}

视图控制台允许在指定时间段内按社区功能在页面视图上生成报告。

![视图报告](assets/view-report.png)

选择报表的条件：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“所有内容”或选择站点上提供的某个功能。

* **[!UICONTROL 时间范围]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择&#x200B;**[!UICONTROL 生成]**&#x200B;以创建报告。

![生成视图](assets/generate-views.png)

## 发布报表 {#posts-report}

“帖子”控制台允许在特定时间段内生成有关社区功能的帖子数的报告。

![帖子报告](assets/posts-report.png)

选择报表的条件：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“所有内容”或选择站点上提供的某个功能。

* **[!UICONTROL 时间范围]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择&#x200B;**[!UICONTROL 生成]**&#x200B;以创建报告。

![生成报表](assets/generate-posts-report.png)

## 疑难解答 {#troubleshooting}

### 未列出社区站点{#no-community-sites-listed}

如果未列出社区站点，请确保已为站点启用Adobe Analytics。 如果选择分配报告，请确保分配功能在社区站点的结构中。

### AEM作者实例{#reports-do-not-show-in-aem-author-instance}中不显示报告

如果报告未显示在AEM作者实例中，请检查自定义，如发布实例上的URL映射。 如果URL映射仅在社区站点的AEM发布实例上完成，请确保已在&#x200B;**站点趋势报告社交组件工厂**&#x200B;配置的AEM作者实例中配置了该映射。

![AEM作者上的URL映射](assets/sitetrend.png)