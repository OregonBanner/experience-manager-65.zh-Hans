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
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# 报表控制台 {#reports-console}

## 概述 {#overview}

对于AEM Communities，可以通过多种方式从创作环境访问各种报表。

通常，各种报告包括：

* [查看次数报表](#views-report)

   提供任何社区站点的社区成员和站点访客查看内容的图表。

* [发布报表](#posts-report)

   提供由社区成员到任何社区站点的各种类型帖子的图表。

表格报表可以导出为.csv格式，以供后续处理。

## 报表控制台 {#reporting-consoles}

### 社区站点报告 {#reports-for-community-sites}

* 从全局导航： **[!UICONTROL 导航]** > **[!UICONTROL 社区]** >  **[!UICONTROL 报表]**

* 选择：

   * **[!UICONTROL 指定报表]**

      * 为选定的社区站点、用户或组以及分配生成报告。
   * **[!UICONTROL 发布报表]**

      * 为选定的社区站点、内容类型和时间段生成报表。
   * **[!UICONTROL 查看次数报表]**

      * 为选定的社区站点、内容类型和时间段生成报表。



![报告](assets/reports1.png)

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

选择 **[!UICONTROL 生成]** 以创建报表。

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

选择 **[!UICONTROL 生成]** 以创建报表。

![生成报告](assets/generate-posts-report.png)

## 疑难解答 {#troubleshooting}

### 未列出社区站点 {#no-community-sites-listed}

如果未列出社区站点，请确保已为站点启用Adobe Analytics。 如果选择分配报告，请确保分配功能在社区站点的结构中。

### 报表未在AEM创作实例中显示 {#reports-do-not-show-in-aem-author-instance}

如果报表未在AEM创作实例中显示，请检查自定义设置，如发布实例上的URL映射。 如果URL映射仅在社区站点的AEM发布实例上完成，请确保已在的AEM创作实例中配置了该URL映射 **网站趋势报表社交组件工厂** 配置。

![AEM作者上的URL映射](assets/sitetrend.png)
