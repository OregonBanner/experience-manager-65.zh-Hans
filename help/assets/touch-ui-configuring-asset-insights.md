---
title: 配置资产分析
description: 在AEM资产中配置资产分析。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6d4f79c126a3c44666e2a42b2246c964813d24ab

---


# 配置资产分析 {#configure-asset-insights}

Adobe Experience Manager(AEM)资产可从Adobe Analytics获取第三方网站使用的有关AEM资产的使用数据。 要使资产分析能够检索此数据并生成洞察，请首先配置该功能以与Adobe Analytics集成。

>[!NOTE]
>
>仅支持和提供图像洞察。

1. 在AEM中，单击工 **[!UICONTROL 具]** >资 **[!UICONTROL 产]**。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 单击“ **[!UICONTROL Insights Configuration]** ”卡。
1. 在向导中，选择一个数据中心并提供您的凭据，包括您的单位名称、用户名和共享机密。

   ![在AEM中为资产分析配置Adobe Analytics](assets/insights_config2.png)


   *图：在AEM中为资产分析配置Adobe Analytics*

1. 单击／点按 **[!UICONTROL 身份验证]**。
1. 在AEM验证您的凭据后，从报 **[!UICONTROL 表包列表中]** ，选择Adobe Analytics报表包，您希望从中获取数据。 单击&#x200B;**[!UICONTROL 添加]**。
1. 在AEM设置您的报表包后，单击／点按完 **[!UICONTROL 成]**。

## 页面跟踪器 {#page-tracker}

配置Adobe Analytics帐户后，将为您生成页面跟踪器代码。 要使资产分析能够跟踪第三方网站中使用的AEM资产，请在网站代码中包含页面跟踪器代码。 在AEM资产中使用页面跟踪器实用程序生成页面跟踪器代码。 有关如何在第三方网页中包含页面跟踪器代码的详细信息，请参阅 [使用页面跟踪器和在网页中嵌入代码](/help/assets/touch-ui-using-page-tracker.md)。

1. 在AEM中，单击工 **[!UICONTROL 具]** >资 **[!UICONTROL 产]**。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 在导航页 **[!UICONTROL 面中]** ，单击“ **[!UICONTROL 分析页面跟踪器]** ”卡。
1. 单击 **[!UICONTROL 下载]** ，下载页面跟踪器代码。
