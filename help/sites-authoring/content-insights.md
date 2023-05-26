---
title: 内容分析
seo-title: Content Insight
description: 内容分析通过Web分析和SEO推荐提供有关页面性能的信息
seo-description: Content Insight provides information about page performance using web analytics and SEO recommendation
uuid: 32f5b37c-2a82-462a-9f0a-c19bed46e198
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 60f980fd-049e-43c1-8b5d-60a8279b357a
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 内容分析{#content-insight}

内容分析提供了有关使用Web分析和SEO推荐的页面性能的信息。 使用内容分析可做出有关如何修改页面的决策，或了解以前的更改如何更改性能。 对于您创建的每个页面，都可以打开“内容分析”来分析该页面。

![chlimage_1-311](assets/chlimage_1-311.png)

“内容分析”页面的布局会发生更改，以适合您正在使用的设备的屏幕维度和方向。

## 报表数据

“内容分析”页面包含使用Adobe SiteCatalyst、Adobe Target、Adobe Social和BrightEdge数据的报表：

* SiteCatalyst：提供了以下量度的报表：

   * 页面查看次数
   * 页面平均逗留时间
   * 源

* Target：页面包含选件的促销活动报表。
* BrightEdge：报告提高页面对搜索引擎可见性的页面功能，并推荐应实施的功能。

参见 [为页面打开Analytics和Recommendations](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## 报告期

报表显示您所控制的一段时间的数据。 在调整报告时段时，报表将自动刷新以显示该时段的数据。 视觉提示指示页面版本发生更改的时间，以便您可以比较每个版本的性能。

您还可以指定报告数据的粒度，例如，您可以查看每日、每周、每月或每年数据。

参见 [更改报告周期](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>内容分析报表要求您的管理员已将AEM与SiteCatalyst、Target和BrightEdge集成。 参见 [与SightCatalyst集成](/help/sites-administering/adobeanalytics.md)， [与Adobe Target集成](/help/sites-administering/target.md)、和 [与BrightEdge集成](/help/sites-administering/brightedge.md).

## 查看次数报表 {#the-views-report}

“查看次数”报表包括以下用于评估页面流量的功能：

* 报告期内页面查看的总数。
* 报告期内查看次数的图表：

   * 查看次数总计。
   * 独特访客。

![chlimage_1-312](assets/chlimage_1-312.png)

## 页面平均参与次数报表 {#the-page-average-engaged-report}

“页面平均参与次数”报表包括以下用于评估页面有效性的功能：

* 页面在整个报告期内保持打开状态的平均时间。
* 整个报告期间的页面查看平均长度的图表。

![chlimage_1-313](assets/chlimage_1-313.png)

## 源报表 {#the-sources-report}

“源”报表指示用户如何导航到页面，例如从搜索引擎结果或使用已知URL。

![chlimage_1-314](assets/chlimage_1-314.png)

## “跳出”报表 {#the-bounces-report}

“跳出次数”报表包含一个图表，该图表显示在选定的报告时段内某个页面发生的跳出次数。

![chlimage_1-315](assets/chlimage_1-315.png)

## 促销活动报表 {#the-campaign-activity-report}

对于页面处于活动状态的每个营销活动，都会显示一个名为的报告 *营销活动名称* 活动。 报表会显示提供选件的每个区段的页面展示次数和转化次数。

![chlimage_1-316](assets/chlimage_1-316.png)

## SEO Recommendations报表 {#the-seo-recommendations-report}

SEO Recommendations报表包含对页面进行BrightEdge分析的结果。 该报告是页面功能的核对清单，指示页面包含和不包含哪些功能，以便使用搜索引擎最大程度地提高查找能力。

利用报告，可创建任务以改进页面查找能力。 Recommendations表示已创建用于实施推荐的任务。 参见 [为SEO Recommendations分配任务](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)
