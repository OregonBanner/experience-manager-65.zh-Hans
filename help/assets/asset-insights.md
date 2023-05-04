---
title: 资产分析
description: 了解资产分析功能如何让您跟踪用户评级和第三方网站、营销活动和Adobe创意解决方案中使用的图像的使用情况统计信息。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 7%

---

# 资产分析 {#asset-insights}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | 本文 |

通过Adobe分析功能，您可以跟踪在第三方网站、营销活动和资产创意解决方案中使用的图像的用户评级和使用情况统计信息。 这有助于深入了解其性能和受欢迎程度。

[!DNL Assets] 分析可捕获用户活动详细信息，如图像的评级、点击次数和展示次数（图像在网站上加载的次数）。 它根据这些统计数据为图像分配分数。 您可以使用得分和效果统计信息来选择要包含在目录、营销活动等中的热门图像。 您甚至可以根据这些统计数据制定存档和许可证续订策略。

对于 [!DNL Assets] 分析以从网站捕获图像的使用情况统计信息，您必须在网站代码中包含图像的嵌入代码。

要让资产分析显示资产的使用情况统计信息，请首先配置功能以从Adobe Analytics获取报表数据。 有关详细信息，请参阅 [配置资产分析](/help/assets/configure-asset-insights.md). 要在内部部署安装中使用此功能，请购买 [!DNL Adobe Analytics] 单独许可。 客户 [!DNL Managed Services] 接收 [!DNL Analytics] 与 [!DNL Experience Manager]. 请参阅 [Managed Services产品说明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>仅支持并提供图像分析。

## 查看图像的统计信息 {#viewing-statistics-for-an-image}

您可以从元数据页面查看资产分析得分。

1. 从 [!DNL Assets] 用户界面(UI)，选择图像，然后单击 **[!UICONTROL 属性]** 中。
1. 在属性页面中，单击 **[!UICONTROL 分析]** 选项卡。
1. 在 **[!UICONTROL 分析]** 选项卡。 的 **[!UICONTROL 得分]** 部分介绍资产的资产使用总数和性能存储。

   使用情况分数描述了资产在各种解决方案中使用的次数。

   的 **[!UICONTROL 展示次数]** score是资产在网站上加载的次数。 显示在 **[!UICONTROL 点击次数]** 是点击资产的次数。

1. 查看 **[!UICONTROL 使用情况统计信息]** 部分以了解资产所属的实体以及最近使用过的创意解决方案。 使用率越高，资产在用户中受欢迎的可能性就越大。 使用情况数据显示在以下标题下：

   * **资产**:资产属于收藏集或复合资产的次数
   * **Web和移动设备**:资产成为网站和应用程序一部分的次数
   * **社交**:资产在解决方案(如Adobe Social和Adobe Campaign)中使用的次数
   * **电子邮件**:资产在电子邮件促销活动中使用的次数

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由于资产分析功能通常会定期从Adobe Analytics中获取解决方案数据，因此解决方案部分可能不会显示最新数据。 显示数据的时间段取决于资产分析为检索Analytics数据而运行的获取操作的计划。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >与“解决方案”部分中的数据不同，“性能统计”部分显示最新的数据。

1. 要获取您包含在网站中的资产的嵌入代码以获取性能数据，请单击 **[!UICONTROL 获取嵌入代码]** 资产缩略图下方。 有关如何将嵌入代码包含在第三方网页中的更多信息，请参阅 [在网页中使用页面跟踪器和嵌入代码](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 查看图像的聚合统计信息 {#viewing-aggregate-statistics-for-images}

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在 [!DNL Assets] 用户界面中，导航到包含要查看其分析的资产的文件夹。
1. 单击工具栏中的布局，然后选择 **[!UICONTROL 分析视图]**.
1. 页面会显示资产的使用情况分数。 比较各个资产的评级并进行分析。

## 计划后台作业 {#scheduling-background-job}

资产分析会定期从Adobe Analytics报表包中获取资产的使用情况数据。 默认情况下，资产分析会在凌晨2点运行一个后台作业，以获取数据。 但是，您可以通过配置 **[!UICONTROL Adobe CQ DAM资产性能报表同步作业]** 服务。

1. 单击 [!DNL Experience Manager] 徽标，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 打开 **[!UICONTROL Adobe CQ DAM资产性能报表同步作业]** 服务配置。

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 在属性调度程序表达式中指定所需的调度程序频率和作业的开始时间。 保存更改。
