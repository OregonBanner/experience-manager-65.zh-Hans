---
title: 报表控制台
seo-title: Reports Console
description: 了解如何访问报告
seo-description: Learn how to access reports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 7%

---

# 报表控制台 {#reports-console}

## 概述 {#overview}

对于AEM Communities，可以通过多种方式从创作环境访问各种报表。

通常，各种报告包括：

* [指定报表](#assignments-report)

   对于 [启用社区](/help/communities/overview.md#enablement-community)，提供学习者在其任务中的进度概述，包括实施SCORM标准时的关联分数。

* [查看次数报表](#views-report)

   按社区成员和站点访客提供任意社区站点的内容视图图表。

* [发布报表](#posts-report)

   提供社区成员在任何社区站点上发表的各种类型的帖子的图表。

时间 [Adobe Analytics已启用](/help/communities/sites-console.md#analytics)，报告将包括一段时间内每个支持资源的查看次数、播放次数、评论次数和评级。

表格报表可以导出为.csv格式，以供后续处理。

## 报表控制台 {#reporting-consoles}

### 社区站点报表 {#reports-for-community-sites}

* 从全局导航： **[!UICONTROL 导航]** > **[!UICONTROL Communities]** >  **[!UICONTROL 报告]**

* 选择自：

   * **[!UICONTROL 指定报表]**

      * 为选定的社区站点、用户或组以及分配生成报告。
   * **[!UICONTROL 发布报表]**

      * 为选定的社区站点、内容类型和时间段生成报告。
   * **[!UICONTROL 查看次数报表]**

      * 为选定的社区站点、内容类型和时间段生成报告。



![报告](assets/reports1.png)

### 启用资源和学习路径报表 {#reports-for-enablement-resources-and-learning-paths}

* 从全局导航： **[!UICONTROL 导航]** > **[!UICONTROL Communities]** >  **[!UICONTROL 资源]**

* 选择现有的启用社区站点：

   * 选择 **报告** 图标以生成涵盖所有启用资源的报表。
   * 选择启用学习路径。
   * 选择 **报告** 图标以生成以下项目的报告：

      * 包含的启用资源。
      * 分配给学习路径的学习者。

* 这些报告提供：

   * 可下载为CSV的表数据：

      * 识别学习者
      * 他们的状态
      * 是否通过目录分配或访问
      * 评论的数量
      * 给予的星级

有关更多详细信息，请参阅 [“报表”部分](/help/communities/resources.md#report) 资源控制台的。

## 指定报表 {#assignments-report}

“工作总揽”控制台允许按启用社区站点、用户或组以及分配筛选报告。

报告提供有关其进展的信息以及任何评论或评级。

![任务报告](assets/assignment-report.png)

选择报告的标准：

* **站点**

   选择启用社区站点。

* **用户或组**
   * 选择用户为一个学习者生成报告。
   * 选择“群组”可生成一组学习者的报告。

   通道服务将从发布环境访问成员和成员组。

* **指定任务**

   从分配给选定学习者的启用资源中进行选择。

选择 **生成** 要创建报告，请执行以下操作：

![generate-report](assets/generate-assignment-report.png)

## 查看次数报表 {#views-report}

通过“查看次数”控制台，可按社区功能生成给定时间段内的页面查看次数报表。

![view-report](assets/view-report.png)

选择报告的标准：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“所有内容”或选择网站上存在的功能之一。

* **[!UICONTROL 期限]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择 **[!UICONTROL 生成]** 以创建报告。

![generate-view](assets/generate-views.png)

## 发布报表 {#posts-report}

通过“帖子”控制台，可生成给定时间段内社区功能的帖子数量报告。

![帖子报表](assets/posts-report.png)

选择报告的标准：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“所有内容”或选择网站上存在的功能之一。

* **[!UICONTROL 期限]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择 **[!UICONTROL 生成]** 以创建报告。

![generate-report](assets/generate-posts-report.png)

## 疑难解答 {#troubleshooting}

### 未列出社区站点 {#no-community-sites-listed}

如果未列出任何社区站点，请确保已为站点启用Adobe Analytics。 如果选择分配报表，请确保分配功能在社区站点的结构中。

### 报告未显示在AEM创作实例中 {#reports-do-not-show-in-aem-author-instance}

如果报表未显示在AEM创作实例中，请检查自定义设置，例如发布实例上的URL映射。 如果仅在Communities站点的AEM发布实例上完成URL映射，请确保已在的AEM创作实例中配置相同的URL映射 **网站趋势报表社交组件工厂** 配置。

![AEM作者上的URL映射](assets/sitetrend.png)
