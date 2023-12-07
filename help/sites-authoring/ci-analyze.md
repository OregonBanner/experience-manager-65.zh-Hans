---
title: 分析页面性能
description: 使用“内容分析”页可以分析所创作页面的性能
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# 分析页面性能{#analyzing-page-performance}

打开 [内容分析](/help/sites-authoring/content-insights.md) 页面，用于分析所创作页面的性能。 配置报告时段以集中进行分析。

## 为页面打开Analytics和Recommendations {#opening-analytics-and-recommendations-for-a-page}

使用以下过程可查看页面的Analytics和Recommendations：

1. 导航到要分析的页面。
1. 在工具栏中，单击 **Analytics和Recommendations**.

   >[!NOTE]
   >
   >仅当您将AEM配置为时，才会显示页面的Analytics和Recommendations [与Adobe Analytics集成](/help/sites-administering/adobeanalytics-connect.md).

   ![screen-shot_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### 更改报告周期 {#changing-the-reporting-period}

更改分析报表的以下与时间相关的方面：

* 要报告的时段。
* 数据的粒度。

用于更改报表中与时间相关的方面的工具显示在内容分析页面的顶部。 ![chlimage_1-126](assets/chlimage_1-126.png)

#### 更改报告周期 {#changing-the-reporting-period-1}

更改内容分析页面的报告时段，将您对页面活动的分析集中到特定时段。 在更改报告时段时，报表会自动刷新。 时间框架上的阴影区域表示报告时段。 时间框架上的日期从左到右增加。

![chlimage_1-127](assets/chlimage_1-127.png)

要更改内容分析页面的报告时段，请执行以下操作：

1. 如果时间范围未出现在页面顶部，请单击切换时间范围图标。

   ![切换时间范围](do-not-localize/chlimage_1-22.png)

1. 要更改报告时段的开始日期，请将阴影区域左侧的圆拖动到所需的开始日期。

   如果看不到着色区域的左侧，请使用滚动条将其带入视图。

1. 要更改报告时段的结束日期，请将阴影区域右侧的圆拖动到所需的结束日期。

#### 更改报告时段的粒度 {#changing-the-granularity-of-the-reporting-period}

更改每个数据点在报表中跨越的时间。 例如，当选择“周”粒度时，“视图”报表上的每个数据点表示一周的视图数。

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

粒度会影响按时间绘制数据的报表，例如“查看次数”和“页面平均参与分钟数”报表。 粒度还影响时间范围的范围。

1. 如果未显示粒度控件，请单击切换粒度图标。

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. 单击所需的粒度。 选择后，报表将自动更新以反映粒度。

### 为SEO Recommendations分配任务 {#assigning-tasks-for-seo-recommendations}

使用SEO Recommendations报表可创建用于提高搜索引擎页面可见性的任务。 对于报表中没有复选标记的每个推荐，您可以创建分配给用户的任务以执行所需工作。

![chlimage_1-129](assets/chlimage_1-129.png)

SEO推荐的状态表示任务已创建但尚未完成。

![chlimage_1-130](assets/chlimage_1-130.png)

创建任务后，该任务将显示在用户的“任务”列表中。 有关任务的信息，请参阅 [使用任务](/help/sites-authoring/task-content.md).

使用以下过程可为SEO建议创建任务。

1. 单击SEO推荐的信息图标。

   ![“信息”图标](do-not-localize/chlimage_1-23.png)

1. 单击信息图标旁边显示的环绕三角形图标。

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. 填写显示的表单字段，然后选择“创建”：

   * 项目：选择要创建任务的项目。
   * 名称：标识任务的名称。 默认名称是SEO推荐的标题。
   * 分配给：选择要为其分配任务的用户。 开始键入用户名以筛选列表。
   * 说明：完成任务所需的活动说明。 默认描述是SEO推荐随附的信息。
   * 任务优先级：任务的优先级。
   * 截止日期：任务应完成的截止日期。

   **注意：** 创建的任务还包括应用SEO推荐的页面的路径。

1. 单击完成以关闭“创建的任务”消息。
