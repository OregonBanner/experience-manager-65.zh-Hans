---
title: 設定Assets Insights以取得分析。
description: 在中設定資產分析 [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 5%

---

# 設定資產分析 {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] 從擷取有關協力廠商網站使用的數位資產的使用資料 [!DNL Adobe Analytics]. 若要啟用Assets Insights以擷取此資料並產生深入分析，請先設定要與整合的功能 [!DNL Adobe Analytics]. 若要在內部部署安裝中使用此功能，請購買 [!DNL Adobe Analytics] 另外授權。 客戶於 [!DNL Managed Services] 接收 [!DNL Analytics] 隨附的授權 [!DNL Experience Manager]. 另請參閱 [Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>僅支援並為影像提供深入分析。

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. 单击&#x200B;**[!UICONTROL 分析配置]**&#x200B;卡。
1. 在精靈中，選取資料中心並提供您的認證，包括您的組織名稱、使用者名稱和共用機密。

   ![設定Adobe Analytics以在Experience Manager中分析資產](assets/insights_config2.png)

   *圖：設定 [!DNL Adobe Analytics] 中的「資產分析」 [!DNL Experience Manager].*

1. 按一下 **[!UICONTROL 驗證]**.
1. 晚於 [!DNL Experience Manager] 驗證您的認證，從 **[!UICONTROL 報表套裝]** 清單，選擇 [!DNL Adobe Analytics] 您希望Assets Insights從中擷取資料的報表套裝。 按一下 **[!UICONTROL 新增]**.
1. 晚於 [!DNL Experience Manager] 設定您的報表套裝，按一下 **[!UICONTROL 完成]**.

## 頁面追蹤器 {#page-tracker}

在您設定您的 [!DNL Adobe Analytics] 帳戶時，系統就會為您產生「頁面追蹤器」代碼。 啟用「資產分析」以進行追蹤的方式 [!DNL Experience Manager] 用於第三方網站的資產，請在網站程式碼中包含頁面追蹤器程式碼。 使用 [!UICONTROL 頁面追蹤器] 中的公用程式 [!DNL Experience Manager Assets] 以產生頁面追蹤器程式碼。 如需如何在協力廠商網頁中加入頁面追蹤器程式碼的詳細資訊，請參閱 [在網頁中使用頁面追蹤器和內嵌程式碼](/help/assets/use-page-tracker.md).

1. 在 [!DNL Experience Manager]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. 从&#x200B;**[!UICONTROL 导航]**&#x200B;页面中，单击&#x200B;**[!UICONTROL 分析页面跟踪器]**&#x200B;卡。
1. 按一下 **[!UICONTROL 下載]** 以下載頁面追蹤器程式碼。
