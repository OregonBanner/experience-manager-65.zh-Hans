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
role: Administrator
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 7%

---

# 报表控制台{#reports-console}

## 概述 {#overview}

对于AEM Communities，可以通过多种方式从创作环境访问各种报表。

通常，各种报告包括：

* [指定报表](#assignments-report)

   对于[启用社区](/help/communities/overview.md#enablement-community)，提供学习者在其分配中的进度概述，包括实施SCORM标准时的关联得分。

* [查看次数报表](#views-report)

   提供任何社区站点的社区成员和站点访客查看内容的图表。

* [发布报表](#posts-report)

   提供由社区成员到任何社区站点的各种类型帖子的图表。

启用[Adobe Analytics](/help/communities/sites-console.md#analytics)后，报表将包含一段时间内每个启用资源的查看次数、播放次数、评论次数和评级。

表格报表可以导出为.csv格式，以供后续处理。

## 报表控制台{#reporting-consoles}

### 社区站点{#reports-for-community-sites}的报表

* 从全局导航：**[!UICONTROL 导航]** > **[!UICONTROL Communities]** > **[!UICONTROL 报表]**

* 选择：

   * **[!UICONTROL 指定报表]**

      * 为选定的社区站点、用户或组以及分配生成报告。
   * **[!UICONTROL 发布报表]**

      * 为选定的社区站点、内容类型和时间段生成报表。
   * **[!UICONTROL 查看次数报表]**

      * 为选定的社区站点、内容类型和时间段生成报表。



![报告](assets/reports1.png)

### 有关启用资源和学习路径的报表{#reports-for-enablement-resources-and-learning-paths}

* 从全局导航：**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 资源]**

* 选择现有的启用社区网站：

   * 选择&#x200B;**报表**&#x200B;图标以生成涵盖所有启用资源的报表。
   * 选择启用学习路径。
   * 选择&#x200B;**报表**&#x200B;图标以生成以下报表：

      * 包含的支持资源。
      * 分配给学习路径的学习者。

* 这些报表提供：

   * 表格数据，可下载为CSV格式：

      * 识别学习者
      * 他们的状态
      * 通过目录分配或访问
      * 评论次数
      * 给定星级

有关更多详细信息，请参阅资源控制台的[报表部分](/help/communities/resources.md#report)。

## 指定报表 {#assignments-report}

“工作总揽”控制台允许按启用社区网站、用户或组以及工作总揽过滤报表。

报告提供了有关其进展情况以及提供的任何评论或评级的信息。

![赋值报告](assets/assignment-report.png)

为报表选择标准：

* **站点**

   选择一个支持社区网站。

* **用户或组**
   * 选择“用户”以为一个学员生成报告。
   * 选择“组”以为学习者组生成报告。

   隧道服务将从发布环境访问成员和成员组。

* **指定任务**

   从分配给选定学习者的支持资源中进行选择。

选择&#x200B;**生成**&#x200B;以创建报表：

![生成报告](assets/generate-assignment-report.png)

## 查看次数报表 {#views-report}

查看次数控制台允许在给定时间段内按社区功能在页面查看次数中生成报表。

![查看报表](assets/view-report.png)

为报表选择标准：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“所有内容”或选择网站上存在的功能之一。

* **[!UICONTROL 时间范围]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择&#x200B;**[!UICONTROL 生成]**&#x200B;以创建报表。

![生成视图](assets/generate-views.png)

## 发布报表 {#posts-report}

“帖子”控制台允许在给定时间段内生成有关社区功能的帖子数量的报表。

![帖子 — 报告](assets/posts-report.png)

为报表选择标准：

* **[!UICONTROL 站点]**

   选择社区站点。

* **[!UICONTROL 内容类型]**

   可以选择“所有内容”或选择网站上存在的功能之一。

* **[!UICONTROL 时间范围]**

   选择以下选项之一：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

选择&#x200B;**[!UICONTROL 生成]**&#x200B;以创建报表。

![生成报告](assets/generate-posts-report.png)

## 疑难解答 {#troubleshooting}

### 未列出{#no-community-sites-listed}社区站点

如果未列出社区站点，请确保已为站点启用Adobe Analytics。 如果选择分配报告，请确保分配功能在社区站点的结构中。

### 报表未显示在AEM创作实例{#reports-do-not-show-in-aem-author-instance}中

如果报表未在AEM创作实例中显示，请检查自定义设置，如发布实例上的URL映射。 如果URL映射仅在社区站点的AEM发布实例上完成，请确保已在&#x200B;**站点趋势报表社交组件工厂**&#x200B;配置的AEM创作实例中配置了该映射。

![AEM作者上的URL映射](assets/sitetrend.png)
