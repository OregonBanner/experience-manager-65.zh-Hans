---
title: 资产分析
description: 了解资产分析功能如何让您跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用情况统计数据。
contentOwner: AG
role: 业务从业者，管理员
feature: 资产分析，资产报表
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 8%

---


# 资产分析 {#asset-insights}

通过资产分析功能，您可以跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用统计信息。 它有助于获得有关其性能和受欢迎程度的洞察。

[!DNL Assets] Insights可捕获用户活动详细信息，例如对图像进行评级、点击和展示次数（图像在网站上加载的次数）。它根据这些统计信息为图像分配分数。 您可以使用分数和性能统计信息来选择热门图像，以将其纳入目录、营销活动等。 您甚至可以根据这些统计数据制定存档和许可证续订策略。

要从网站获取图像的使用情况统计信息，[!DNL Assets]必须在网站代码中包含图像的嵌入代码。

要让资产分析显示资产的使用情况统计信息，请首先配置该功能以从Adobe Analytics获取报告数据。 有关详细信息，请参阅[配置资产分析](/help/assets/configure-asset-insights.md)。

>[!NOTE]
>
>只支持并提供图像分析。

## 图像{#viewing-statistics-for-an-image}的视图统计

您可以从元数据页面视图资产分析分数。

1. 从[!DNL Assets]用户界面(UI)中，选择图像，然后从工具栏中单击&#x200B;**[!UICONTROL 属性]**。
1. 在“属性”页中，单击&#x200B;**[!UICONTROL Insights]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL Insights]**&#x200B;选项卡中查看资产的使用详细信息。 **[!UICONTROL Score]**&#x200B;部分描述资产的资产使用总数和性能存储。

   使用情况分数描述资产在各种解决方案中的使用次数。

   **[!UICONTROL 展示次数]**&#x200B;分数是资产在网站上加载的次数。 **[!UICONTROL 单击]**&#x200B;下显示的数字是单击资产的次数。

1. 查看&#x200B;**[!UICONTROL 使用统计信息]**&#x200B;部分，了解资产所属的实体以及最近使用的创意解决方案。 使用率越高，该资产在用户中受欢迎的可能性就越大。 使用数据显示在以下标题下：

   * **资产**:资产加入集合或复合资产的次数
   * **Web和移动**:资产加入网站和应用程序的次数
   * **社交**:资产在解决方案(如Adobe Social和Adobe Campaign)中的使用次数
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

1. 要获取包含在网站中的资产的嵌入代码以获取性能数据，请单击资产缩略图下方的&#x200B;**[!UICONTROL 获取嵌入代码]**。 有关如何在第三方网页中包含嵌入代码的详细信息，请参阅[使用页面跟踪器和在网页中嵌入代码](/help/assets/use-page-tracker.md)。

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 图像{#viewing-aggregate-statistics-for-images}的视图聚合统计信息

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在[!DNL Assets]用户界面中，导航到包含要视图分析的资产的文件夹。
1. 单击工具栏中的布局，然后选择&#x200B;**[!UICONTROL 分析视图]**。
1. 该页面显示资产的使用分数。 比较各个资产的评级并进行分析。

## 计划后台作业{#scheduling-background-job}

资产分析可定期从Adobe Analytics报表包获取资产的使用数据。 默认情况下，资产分析会在凌晨2点每24小时运行一个后台作业，以获取数据。 但是，您可以通过从Web控制台配置&#x200B;**[!UICONTROL Adobe CQ DAM资产性能报表同步作业]**&#x200B;服务来修改频率和时间。

1. 单击[!DNL Experience Manager]徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 打开&#x200B;**[!UICONTROL Adobe CQ DAM资产性能报表同步作业]**&#x200B;服务配置。

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 在属性调度程序中指定作业所需的开始频率和调度程序时间。 保存更改。
