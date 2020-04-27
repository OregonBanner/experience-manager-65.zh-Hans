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
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# 报告控制台 {#reports-console}

## 概述 {#overview}

对于AEM Communities，可以通过多种方式从创作环境访问各种报告。

一般而言，各种报告包括：

* [指定报表](#assignments-report)

   对于支 [持社区](/help/communities/overview.md#enablement-community)，提供学员分配进度的概述，包括在实施SCORM标准时的关联得分。

* [查看次数报表](#views-report)

   提供按社区成员和任何社区站点的站点视图的内容访客图表。

* [发布报表](#posts-report)

   按社区成员向任何社区站点提供各种类型的帖子图表。

启用 [Adobe Analytics后](/help/communities/sites-console.md#analytics)，报告将包括一段时间内每个支持资源的视图数、播放数、评论数和评级数。

表格式报告可以以。csv格式导出，以便后续处理。

## 报告控制台 {#reporting-consoles}

### 社区站点报告 {#reports-for-community-sites}

* 从全局导航：导 **[!UICONTROL 航]** >社 **[!UICONTROL 区]** >报 **[!UICONTROL 告]**

* 从以下选项中进行选择：

   * **[!UICONTROL 指定报表]**

      * 为选定的社区站点、用户或用户组以及分配生成报告。
   * **[!UICONTROL 发布报表]**

      * 为选定的社区站点、内容类型和时间段生成报告。
   * **[!UICONTROL 查看次数报表]**

      * 为选定的社区站点、内容类型和时间段生成报告。



![chlimage_1-236](assets/chlimage_1-236.png)

### Enablement Resources和学习路径报告 {#reports-for-enablement-resources-and-learning-paths}

* 从全局导航：“导 **[!UICONTROL 航]** ”>“社 **[!UICONTROL 区”]** >“资 **[!UICONTROL 源”]**

* 选择现有的支持社区站点：

   * 选择 **报告图标** ，以生成涵盖所有启用资源的报告。
   * 选择一个启用学习路径。
   * 选择“ **报告** ”图标以生成以下报表：

      * 包含的支持资源。
      * 分配给学习路径的学员数。

* 这些报告提供：

   * 可下载的表数据：

      * 识别学员
      * 他们的状态
      * 是分配还是通过目录访问
      * 评论数
      * 给定星级

有关详细信息，请参 [阅资源控制台](/help/communities/resources.md#report) 的“报告”部分。

## 指定报表 {#assignments-report}

“任务”控制台允许按启用社区站点、用户或用户组以及任务分配筛选报告。

该报告提供了有关其进度的信息以及提供的任何评论或评级。

![chlimage_1-237](assets/chlimage_1-237.png)

选择报表的条件：

* **站点**

   选择一个支持社区站点。

* **用户或组**
   * 选择“用户”，为一个学员生成报告。
   * 选择“组”以为学员组生成报告。
   通道服务将从发布环境访问成员和成员组。

* **指定任务**

   从分配给选定学员的启用资源中进行选择。

选择 **生成** ，以创建报表：

![chlimage_1-238](assets/chlimage_1-238.png)

## 查看次数报表 {#views-report}

视图控制台允许在指定时间段内按社区功能在页面视图中生成报告。

![chlimage_1-239](assets/chlimage_1-239.png)

选择报表的条件：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“所有内容”或选择站点上提供的功能之一。

* **[!UICONTROL 时间范围]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择 **[!UICONTROL 生成]** ，以创建报表。

![chlimage_1-240](assets/chlimage_1-240.png)

## 发布报表 {#posts-report}

“帖子”控制台允许在指定时间段内生成有关社区功能的帖子数的报告。

![chlimage_1-241](assets/chlimage_1-241.png)

选择报表的条件：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“所有内容”或选择站点上提供的功能之一。

* **[!UICONTROL 时间范围]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择 **[!UICONTROL 生成]** ，以创建报表。

![chlimage_1-242](assets/chlimage_1-242.png)

## 疑难解答 {#troubleshooting}

### 未列出社区站点 {#no-community-sites-listed}

如果未列出社区站点，请确保已为站点启用Adobe Analytics。 如果选择任务报告，请确保任务功能位于社区站点的结构中。

### 报告不显示在AEM作者实例中 {#reports-do-not-show-in-aem-author-instance}

如果报告未显示在AEM作者实例中，请检查自定义，如发布实例上的URL映射。 如果仅对社区站点的AEM发布实例执行URL映射，请确保在“站点趋势报告社交组件工厂”配置的AEM作者实例中已配置 **URL映射** 。

![AEM作者上的URL映射](assets/sitetrend.png)