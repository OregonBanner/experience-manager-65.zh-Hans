---
title: 配置资产分析以获取分析。
description: 在中配置资产分析 [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 6%

---

# 配置资产分析 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 从以下位置获取有关第三方网站使用的数字资产的使用数据 [!DNL Adobe Analytics]. 要启用资产分析以检索此数据并生成分析，请首先配置要与集成的功能 [!DNL Adobe Analytics]. 要在内部部署安装中使用此功能，请购买 [!DNL Adobe Analytics] 单独许可。 客户位于 [!DNL Managed Services] 接收 [!DNL Analytics] 与捆绑在一起的许可证 [!DNL Experience Manager]. 参见 [Managed Services产品描述](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>仅支持并为图像提供见解。

1. In [!DNL Experience Manager]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。
1. 在向导中，选择一个数据中心并提供您的凭据，包括组织名称、用户名和共享密钥。

   ![在Experience Manager中配置Adobe Analytics以进行资产分析](assets/insights_config2.png)

   *图：配置 [!DNL Adobe Analytics] 中的资产分析 [!DNL Experience Manager].*

1. 单击 **[!UICONTROL 身份验证]**.
1. 晚于 [!DNL Experience Manager] 从验证您的凭据 **[!UICONTROL 报表包]** 列表，选择一个 [!DNL Adobe Analytics] 您希望资产分析从中获取数据的报表包。 单击&#x200B;**[!UICONTROL 添加]**。
1. 晚于 [!DNL Experience Manager] 设置报表包，单击 **[!UICONTROL 完成]**.

## 页面跟踪器 {#page-tracker}

配置之后 [!DNL Adobe Analytics] 帐户时，会为您生成页面跟踪器代码。 启用资产分析以进行跟踪 [!DNL Experience Manager] 第三方网站中使用的资产，在网站代码中包含页面跟踪器代码。 使用 [!UICONTROL 页面跟踪器] 中的实用程序 [!DNL Experience Manager Assets] 以生成页面跟踪器代码。 有关如何将页面跟踪器代码包含在第三方网页中的更多信息，请参阅 [在网页中使用页面跟踪器和嵌入代码](/help/assets/use-page-tracker.md).

1. In [!DNL Experience Manager]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 资产]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 单击 **[!UICONTROL 下载]** 以下载页面跟踪器代码。
