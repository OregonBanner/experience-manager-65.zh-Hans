---
title: 配置资产分析以获得分析。
description: 在 [!DNL Adobe Experience Manager Assets]中配置资产分析。
contentOwner: AG
role: Architect, Administrator
feature: 资产分析，资产报表
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: c07467feb96c25a4bac1916f88f04fdb37979ee1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 6%

---

# 配置资产分析{#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 从中获取第三方网站使用的数字资产的使用数据 [!DNL Adobe Analytics]要使资产分析能够检索此数据并生成洞察，请首先配置该功能以与[!DNL Adobe Analytics]集成。 要使用此功能，请单独购买[!DNL Adobe Analytics]许可证。 [!DNL Managed Services]上的客户会收到与[!DNL Experience Manager]绑定的[!DNL Analytics]许可证。 请参阅[Managed Services产品说明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html)。

>[!NOTE]
>
>只支持并提供图像分析。

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]**。

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。
1. 在向导中，选择一个数据中心并提供您的凭据，包括您的单位名称、用户名和共享机密。

   ![在Adobe Analytics中配置资产分析](assets/insights_config2.png)

   *图：在中 [!DNL Adobe Analytics] 配置资产分 [!DNL Experience Manager]析*

1. 单击&#x200B;**[!UICONTROL Authenticate]**。
1. 在[!DNL Experience Manager]验证您的凭据后，从&#x200B;**[!UICONTROL 报表包]**&#x200B;列表中，选择[!DNL Adobe Analytics]报表包，您希望资产分析从中获取数据。 单击&#x200B;**[!UICONTROL 添加]**。
1. 在[!DNL Experience Manager]设置报表包后，单击&#x200B;**[!UICONTROL 完成]**。

## 页面跟踪器{#page-tracker}

配置[!DNL Adobe Analytics]帐户后，将为您生成页面跟踪器代码。 要使资产分析能够跟踪第三方网站中使用的[!DNL Experience Manager]资产，请在网站代码中包含页面跟踪器代码。 使用[!DNL Experience Manager Assets]中的[!UICONTROL 页面跟踪器]实用程序生成页面跟踪器代码。 有关如何在第三方网页中包含页面跟踪器代码的详细信息，请参阅[使用页面跟踪器并在网页中嵌入代码](/help/assets/use-page-tracker.md)。

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]**。

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 单击&#x200B;**[!UICONTROL 下载]**&#x200B;以下载页面跟踪器代码。
