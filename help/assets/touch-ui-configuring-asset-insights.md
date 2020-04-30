---
title: 配置资产分析以获取数字资产使用情况分析。
description: 在[!DNL Adobe Experience Manager Assets]中配置资产分析。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 配置资产分析 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 第三方网站使用的数字资产的使用数据会从中获取 [!DNL Adobe Analytics]。 要使资产分析能够检索此数据并生成洞察，请首先配置该功能以与Adobe Analytics集成。

>[!NOTE]
>
>仅支持和提供图像洞察。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。
1. 在向导中，选择一个数据中心并提供您的凭据，包括您的单位名称、用户名和共享机密。

   ![在Experience Manager中配置Adobe Analytics以分析资产](assets/insights_config2.png)

   *图：在中[!DNL Adobe Analytics]为资产分析配置[!DNL Experience Manager]。*

1. 单击“ **[!UICONTROL 身份验证]**”。
1. 验 [!DNL Experience Manager] 证凭据后，从报表包 **[!UICONTROL 列表中]** ，选择要从中获取数据的 [!DNL Adobe Analytics] 资产分析报表包。 单击&#x200B;**[!UICONTROL 添加]**。
1. 设置 [!DNL Experience Manager] 报表包后，单击“完 **[!UICONTROL 成”]**。

## 页面跟踪器 {#page-tracker}

配置帐户后， [!DNL Adobe Analytics] 将为您生成页面跟踪器代码。 要使“资产分析”能够跟 [!DNL Experience Manager] 踪第三方网站中使用的资产，请在网站代码中包含页面跟踪器代码。 使用中 [!UICONTROL 的页面跟踪器] ，以 [!DNL Experience Manager Assets] 生成页面跟踪器代码。 有关如何在第三方网页中包含页面跟踪器代码的详细信息，请参阅 [使用页面跟踪器和在网页中嵌入代码](/help/assets/touch-ui-using-page-tracker.md)。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 单击 **[!UICONTROL 下载]** ，下载页面跟踪器代码。
