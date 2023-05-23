---
title: '"[!DNL Assets] 首頁體驗」'
description: 個人化 [!DNL Experience Manager Assets] 首頁提供豐富的歡迎畫面體驗，包括資產相關近期活動的快照。
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] 首頁體驗 {#aem-assets-home-page-experience}

個人化 [!DNL Adobe Experience Manager Assets] 首頁，提供豐富的歡迎畫面體驗，包括資產相關近期活動的快照。

[!DNL Assets] 首頁提供豐富且個人化的歡迎畫面體驗，包括最近活動的快照，例如最近檢視或上傳的資產。

此 [!DNL Assets] 首頁預設為停用。 若要啟用此功能，請執行下列步驟：

1. 開啟 [!DNL Experience Manager] 設定管理員 `https://[aem_server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL Day CQ DAM事件記錄器]** 服務。
1. 選取 **[!UICONTROL 啟用此服務]** 以啟用活動記錄。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 從 **[!UICONTROL 事件型別]** 清單中，選取要記錄的事件，並儲存變更。

   >[!CAUTION]
   >
   >啟用「已檢視資產」、「已檢視專案」和「已檢視集合」選項，會大幅增加已記錄事件的數量。

1. 開啟 **[!UICONTROL dam資產首頁功能標幟]** 來自Configuration Manager的服務 `https://[aem_server]:[port]/system/console/configMgr`.
1. 選取 `isEnabled.name` 可啟用「 」的選項 [!DNL Assets] 首頁功能。 保存更改。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 開啟 **[!UICONTROL 使用者偏好設定]** 對話方塊，並選取 **[!UICONTROL 啟用資產首頁]**. 保存更改。

   ![在使用者偏好設定對話方塊上啟用資產首頁](assets/Annotation-color.png)

啟用 [!DNL Assets] 首頁，導覽至 [!DNL Assets] 使用者介面可從導覽頁面或直接從URL存取 `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![在Assets使用者介面上設定體驗連結](assets/config-experience-link.png)

按一下 **[!UICONTROL 按一下這裡以設定您的體驗連結]** 以新增您的使用者名稱、背景影像和設定檔影像。

此 [!DNL Assets] 首頁包含下列段落：

* 歡迎區段
* Widget區段

**歡迎區段**

如果您的設定檔存在，「歡迎」區段會顯示寄給您的歡迎訊息。 此外，它會顯示您的個人資料圖片和歡迎影像（如果已設定）。

如果您的設定檔不完整，「歡迎」區段會顯示一般歡迎訊息和設定檔圖片的預留位置。

**Widget區段**

此區段會顯示在「歡迎」區段下方，並在下列區段下顯示現成的Widget：

* 活动
* 最近
* 发现

**活動**：在本節底下， **[!UICONTROL 我的活動]** widget會顯示登入使用者使用資產（包括沒有轉譯的資產）執行的最近活動，例如資產上傳、下載、資產建立、編輯、註解、註解及共用。

**最近**：此 **[!UICONTROL 最近檢視的專案]** 此區段下的Widget會顯示登入使用者最近存取的實體，包括資料夾、集合和專案。

**探索**：此 **[!UICONTROL 新增]** 此區段下的Widget會顯示最近上傳至的資產和轉譯 [!DNL Assets] 部署。

若要啟用清除使用者活動資料，請啟用 **[!UICONTROL DAM事件清除服務]** 從Configuration Manager。 啟用此服務後，系統會刪除登入使用者超過指定數目的活動。

「歡迎」畫面提供簡單的導覽協助，例如工具列上的圖示以存取資料夾、集合和目錄。

>[!NOTE]
>
>啟用 [!UICONTROL Day CQ DAM事件記錄器] 和 [!UICONTROL DAM事件清除] 服務會增加對JCR的寫入作業和搜尋索引，大幅增加 [!DNL Experience Manager] 伺服器。 上的額外負載 [!DNL Experience Manager] 伺服器可能會影響其效能。

>[!CAUTION]
>
>擷取、篩選及永久刪除使用者活動所需 [!DNL Assets] 首頁會對效能造成額外負擔。 因此，管理員應該為目標使用者有效地設定首頁。
>
>Adobe建議執行大量作業的管理員和使用者避免使用資產首頁功能，以防止使用者活動增加。 此外，管理員可以透過設定來排除特定使用者的錄製活動 [!UICONTROL Day CQ DAM事件記錄器] 從 [!UICONTROL 設定管理員].
>
>如果您使用此功能，Adobe建議您根據伺服器負載排定清除頻率。
