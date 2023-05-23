---
title: 資產分析
description: 瞭解Assets Insights功能如何讓您追蹤用於協力廠商網站、行銷活動和Adobe創意解決方案之影像的使用者評分和使用情況統計資料。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 7%

---

# 資產分析 {#asset-insights}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | 本文 |

Assets Insights功能可讓您追蹤用於協力廠商網站、行銷活動和Adobe創意解決方案之影像的使用者評等和使用情況統計資料。 這有助於獲得有關其效能和人氣的深入分析。

[!DNL Assets] Insights會擷取使用者活動詳細資訊，例如影像的評分、點按和曝光次數（影像載入網站的次數）。 系統會根據這些統計資料，將分數指派給影像。 您可以使用分數和效能統計資料來選取要包含在目錄、行銷活動等中的熱門影像。 您甚至可以根據這些統計資料制定封存和授權更新政策。

對象 [!DNL Assets] 深入分析若要從網站擷取影像的使用狀況統計資料，您必須在網站程式碼中包含影像的內嵌程式碼。

若要讓Assets Insights顯示資產的使用狀況統計資料，請先設定功能以從Adobe Analytics擷取報表資料。 如需詳細資訊，請參閱 [設定資產分析](/help/assets/configure-asset-insights.md). 若要在內部部署安裝中使用此功能，請購買 [!DNL Adobe Analytics] 另外授權。 客戶於 [!DNL Managed Services] 接收 [!DNL Analytics] 隨附的授權 [!DNL Experience Manager]. 另請參閱 [Managed Services產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>僅支援並為影像提供深入分析。

## 檢視影像的統計資料 {#viewing-statistics-for-an-image}

您可以從中繼資料頁面檢視Assets Insights分數。

1. 從 [!DNL Assets] 使用者介面(UI)，選取影像，然後按一下 **[!UICONTROL 屬性]** （從工具列）。
1. 在「屬性」頁面中，按一下 **[!UICONTROL 深入分析]** 標籤。
1. 在中檢閱資產的使用方式詳細資訊 **[!UICONTROL 深入分析]** 標籤。 此 **[!UICONTROL 分數]** 區段說明資產的資產使用總量和效能損失。

   使用分數說明資產在各種解決方案中的使用次數。

   此 **[!UICONTROL 曝光次數]** score是資產在網站上載入的次數。 以下顯示的數字： **[!UICONTROL 點按次數]** 是資產的點按次數。

1. 檢閱 **[!UICONTROL 使用狀況統計資料]** 區段，以瞭解資產所屬的實體，以及最近使用過資產的創意解決方案。 使用量越高，該資產在使用者中受歡迎的可能性就越大。 使用情況資料會顯示在下列標題下：

   * **資產**：資產成為集合或複合資產一部分的次數
   * **網頁與行動**：資產屬於網站和應用程式的次數
   * **社交**：資產在解決方案(例如Adobe Social和Adobe Campaign)中的使用次數
   * **電子郵件**：資產在電子郵件行銷活動中的使用次數

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >由於Assets Insights功能通常會定期從Adobe Analytics擷取解決方案資料，因此「解決方案」區段可能不會顯示最新資料。 資料顯示的時間長度取決於Assets Insights為擷取Analytics資料而執行的擷取作業排程。

1. 要以图形方式查看一段时间内资产的性能统计信息，请在&#x200B;**[!UICONTROL 性能统计信息]**&#x200B;部分中选择时间段。包括点击次数和印象在内的详细信息将显示为图形的趋势线。

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >與「解決方案」段落中的資料不同，「效能統計資料」段落會顯示最新的資料。

1. 若要取得您包含在網站中資產的內嵌程式碼，以取得效能資料，請按一下 **[!UICONTROL 取得內嵌程式碼]** 在資產縮圖下方。 如需如何在協力廠商網頁中包含內嵌程式碼的詳細資訊，請參閱 [在網頁中使用頁面追蹤器和內嵌程式碼](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## 檢視影像的彙總統計資料 {#viewing-aggregate-statistics-for-images}

您可以使用&#x200B;**[!UICONTROL 分析视图]**&#x200B;同时查看文件夹中所有资产的分数。

1. 在 [!DNL Assets] 在使用者介面中，導覽至包含您要檢視其見解的資產的資料夾。
1. 按一下工具列中的「配置」 ，然後選擇 **[!UICONTROL 深入分析檢視]**.
1. 頁面會顯示資產的使用情況分數。 比較各種資產的評等並得出深入見解。

## 排程背景工作 {#scheduling-background-job}

Assets Insights會定期從Adobe Analytics報表套裝擷取資產的使用情況資料。 根據預設，Assets Insights會在凌晨2:00每隔24小時執行背景工作以擷取資料。 不過，您可以透過設定 **[!UICONTROL Adobe CQ DAM資產效能報表同步工作]** Web控制檯的服務。

1. 按一下 [!DNL Experience Manager] 標誌，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.
1. 開啟 **[!UICONTROL Adobe CQ DAM資產效能報表同步工作]** 服務設定。

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. 在屬性排程器運算式中指定所需的排程器頻率和工作的開始時間。 保存更改。
