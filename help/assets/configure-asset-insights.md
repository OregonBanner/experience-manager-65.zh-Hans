---
title: 配置资产分析以获取分析。
description: 在中配置资产分析 [!DNL Adobe Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c1362c2c1f32d02d36d2067e0e74d927ddbc1554
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 7%

---


# 配置资产分析 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 从第三方网站使用的数字资产中获取使用数据 [!DNL Adobe Analytics]。 要使资产分析能够检索此数据并生成洞察，请首先配置该功能以与Adobe Analytics集成。

>[!NOTE]
>
>只支持并提供图像洞察。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。
1. 在向导中，选择一个数据中心并提供您的凭据，包括您的组织名称、用户名和共享机密。

   ![配置Adobe AnalyticsExperience Manager的资产洞察](assets/insights_config2.png)

   *图：在中 [!DNL Adobe Analytics] 配置资产分 [!DNL Experience Manager]析。*

1. 单击“ **[!UICONTROL 身份验证]**”。
1. 验证 [!DNL Experience Manager] 您的凭据后，从报 **[!UICONTROL 表包列表中]** ，选择您希望 [!DNL Adobe Analytics] 资产分析从中获取数据的报表包。 单击&#x200B;**[!UICONTROL 添加]**。
1. 设置 [!DNL Experience Manager] 报表包后，单击“完 **[!UICONTROL 成”]**。

## 页面跟踪器 {#page-tracker}

配置帐户 [!DNL Adobe Analytics] 后，将为您生成页面跟踪器代码。 要使资产分析能够跟 [!DNL Experience Manager] 踪第三方网站中使用的资产，请在网站代码中包含页面跟踪器代码。 使用中 [!UICONTROL 的页面跟踪] 器实 [!DNL Experience Manager Assets] 用程序生成页面跟踪器代码。 有关如何在第三方网页中包含页面跟踪器代码的更多信息，请参 [阅使用页面跟踪器和在网页中嵌入代码](/help/assets/use-page-tracker.md)。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 单击 **[!UICONTROL “下载]** ”以下载页面跟踪器代码。
