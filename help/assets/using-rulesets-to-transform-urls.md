---
title: 使用规则集转换 URL
description: 您可以在Dynamic Media中部署規則集來轉換URL。 規則集是以指令碼語言（例如JavaScript）撰寫的指令集，可評估XML資料，並在資料符合特定條件時採取特定動作。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# 使用規則集轉換URL {#using-rulesets-to-transform-urls}

您可以在Dynamic Media中部署規則集來轉換URL。 規則集是以指令碼語言（例如JavaScript）撰寫的指令集，可評估XML資料，並在資料符合特定條件時採取特定動作。 每個規則都包含至少一個條件和至少一個動作。 規則會根據條件評估XML資料，如果符合條件，則會採取適當的動作。 規則集的範例包括：

* 新增MIME型別字尾。 許多服務和網站都需要影像尾碼，例如 `.jpg` 至URL。
* 為SEO （搜尋引擎最佳化）目的建立URL的資料夾路徑。

   另請參閱 [Adobe Dynamic Media Classic如何支援SEO](/help/assets/assets/s7_seo.pdf).

* 將中繼資料新增至URL以進行SEO （搜尋引擎最佳化）。

   另請參閱 [Adobe Dynamic Media Classic如何支援SEO](/help/assets/assets/s7_seo.pdf).

* 設定內容處置以觸發下載。
* 簡化個人化的影像伺服範本URL。 例如，翻轉 `rgb{XX,YY,ZZ}` 進入RTF-ready `\redXX\greenYY\blueZZ`

* 要求編碼特定字元，例如 `$`， `{`、和 `}`和某些要解碼為ImageServer的字元。 例如，Facebook無法順利處理包含特殊字元的URL。

   另請參閱 [從URL中移除特殊字元](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

在Dynamic Media環境中，使用XML系統管理資產資訊的網站可將XML檔案上傳至Dynamic Media。 您可以將其中一個檔案指定為預先處理規則集檔案，以提供Dynamic Media資產。 此檔案會重新建構標準URL通訊協定格式，以符合與Dynamic Media整合之系統的商業邏輯。 您可以指定XML檔案做為規則集定義檔案路徑。

>[!CAUTION]
>
>使用規則集時請務必小心，因為規則集可能會導致Dynamic Media內容無法在您的網站上顯示。

有些範例規則集可協助您建立自己的規則集。
另請參閱 [規則集參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

與建立所有規則集時一樣，使用xmlvalid之類的XML驗證器程式，在上傳XML檔案之前，請確保XML檔案有效。
另請參閱 [規則集疑難排解](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

此外，請務必先在中繼環境中測試規則集，以免影響您的即時生產環境。
生產環境和測試環境通常需要不同的登入。

請參閱 [登入資訊的Adobe Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

另請參閱 [在規則集中使用「asset」而不是「is」影像](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**若要建置XML規則集，請執行下列動作：**

1. 登入您的 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Adobe在布建時已提供您的認證和登入詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 執行下列操作上傳規則集檔案：

   * 在全域導覽列上，選取 **[!UICONTROL 上傳]**.
   * 於 **[!UICONTROL 上傳]** 頁面，左上角附近，選取 **[!UICONTROL 瀏覽]**.
   * 在 **[!UICONTROL 開啟]** 對話方塊中，瀏覽至規則集檔案(XML)。
   * 選取檔案，然後選取 **[!UICONTROL 開啟]**.
   * 在右側 **[!UICONTROL 上傳]** 頁面，選取規則集檔案的目標資料夾。
   * 在頁面底部附近，確認 **[!UICONTROL 上傳後發佈]** 已勾選。
   * 在頁面的右下角，選取 **[!UICONTROL 提交上傳]**.
   * 在全域導覽列上，選取 **[!UICONTROL 工作]** 以檢查上傳工作的狀態。 當 **[!UICONTROL 狀態]** 上的欄 **[!UICONTROL 工作]** 頁面顯示上傳完成，繼續後續步驟。

1. 在靠近頁面頂端的導覽列上，選取 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 影像伺服器]**.
1. 於 **[!UICONTROL 影像伺服器發佈]** 頁面，在 **[!UICONTROL 目錄管理]** 群組，找出 **[!UICONTROL 規則集定義檔案路徑]**，然後選取 **[!UICONTROL 選取]**.
1. 於 **[!UICONTROL 選取規則集定義檔案(XML)]** 頁面，瀏覽至規則集檔案，然後在頁面的右下角選取「 」 **[!UICONTROL 選取]**.
1. 在「設定」頁面的右下角，選取 **[!UICONTROL 關閉]**.
1. 執行影像伺服器發佈工作。

   規則集條件會套用至即時Dynamic Media影像伺服器的請求。

   如果您變更規則集檔案，當您重新上傳並重新發佈更新的規則集檔案時，會立即套用變更。
