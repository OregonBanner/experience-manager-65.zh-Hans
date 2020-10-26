---
title: 资产分析
description: 了解资产分析功能如何让您跟踪第三方网站、营销活动和Adobe的创意解决方案中使用的图像的用户评级和使用情况统计。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 8%

---


# 资产分析 {#asset-insights}

通过资产分析功能，您可以跟踪第三方网站、营销活动和Adobe的创意解决方案中使用的图像的用户评级和使用情况统计。 它有助于获得有关其性能和受欢迎程度的洞察。

[!DNL Assets] 洞察可捕获用户活动详细信息，如对图像进行评级、点击次数和展示次数（在网站上加载图像的次数）。 它根据这些统计信息为图像分配分数。 您可以使用分数和性能统计信息选择热门图像，以将其纳入目录、营销活动等。 您甚至可以根据这些统计信息制定存档和许可证续订策略。

要 [!DNL Assets] 获取网站中图像的使用情况统计信息，您必须在网站代码中包含图像的嵌入代码。

要让资产分析显示资产的使用情况统计信息，请首先配置该功能以从Adobe Analytics获取报告数据。 有关详细信息，请 [参阅配置资产分析](/help/assets/configure-asset-insights.md)。

>[!NOTE]
>
>只支持并提供图像洞察。

## 图像的视图统计 {#viewing-statistics-for-an-image}

您可以从元数据页面视图资产分析得分。

1. 从用 [!DNL Assets] 户界面(UI)中，选择图像，然后单击工 **[!UICONTROL 具栏]** 中的属性。
1. 在“属性”页面中，单击“ **[!UICONTROL 分析]** ”选项卡。
1. 在“洞察”选项卡中查看资产的使用 **[!UICONTROL 情况]** 详细信息。 分数 **[!UICONTROL 部分]** ，描述资产的资产使用总数和性能存储。

   使用情况分数描述资产在各种解决方案中的使用次数。

   展示 **[!UICONTROL 次数]** (Impessions)得分是资产在网站上加载的次数。 单击次数 **[!UICONTROL 下显]** 示的数量是单击资产的次数。

1. 查看“ **[!UICONTROL 使用统计]** ”部分，了解资产所属的实体以及最近使用的创意解决方案。 使用率越高，资产在用户中受欢迎的可能性就越大。 使用情况数据显示在以下标题下：

   * **资产**:资产加入集合或复合资产的次数
   * **Web和移动**:资产加入网站和应用程序的次数
   * **社交**:资产在解决方案中的使用次数，如Adobe Social和Adobe Campaign
   * **电子邮件**:资产在电子邮件活动中的使用次数

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由于资产分析功能通常会定期从Adobe Analytics获取解决方案数据，因此解决方案部分可能不会显示最新数据。 显示数据的时间段取决于资产分析运行以检索Analytics数据的提取操作的计划。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >与“解决方案”部分中的数据不同，“性能统计”部分显示最新数据。

1. 要获取包含在网站中的资产的嵌入代码以获取性能数据，请单击资产 **[!UICONTROL 缩略图下方的]** “获取嵌入代码”。 有关如何将嵌入代码包含在第三方网页中的更多信息，请参 [阅使用页面跟踪器和在网页中嵌入代码](/help/assets/use-page-tracker.md)。

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 视图聚合图像统计 {#viewing-aggregate-statistics-for-images}

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. In the [!DNL Assets] user interface, navigate to the folder containing the assets for which you want to view insights.
1. 单击工具栏中的布局，然后选择 **[!UICONTROL 分析视图]**。
1. 该页面显示资产的使用分数。 比较各个资产的评级并进行分析。

## 计划背景作业 {#scheduling-background-job}

资产分析可定期从Adobe Analytics报表包获取资产的使用数据。 默认情况下，资产分析每24小时在凌晨2点运行一次后台作业以获取数据。 但是，您可以通过从Web控制台配置 **[!UICONTROL Adobe CQDAM资产性能报表同步作业服务]** ，来修改频率和时间。

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. 打开 **[!UICONTROL Adobe CQDAM资产性能报表同步作业]** 服务配置。

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 在属性调度程序表达式中指定作业的所需开始频率和调度程序时间。 保存更改。
