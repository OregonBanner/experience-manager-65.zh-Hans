---
title: 將規則套用至最適化表單欄位
seo-title: Apply rules to adaptive form fields
description: 建立規則以將互動、商業邏輯和智慧驗證新增到最適化表單。
seo-description: Create rules to add interactivity, business logic, and smart validations to an adaptive form.
page-status-flag: de-activated
uuid: 60f142aa-81ca-4333-8614-85a01e23e917
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 982eddba-2350-40e7-8a42-db02d28cf133
exl-id: 0202ca65-21ef-4477-b704-7b52314a7d7b
source-git-commit: 63bc43bba88a42d62fb574bc8ce42470ac61d693
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---

# 教學課程：將規則套用至最適化表單欄位 {#tutorial-apply-rules-to-adaptive-form-fields}

![06-apply-rules-to-adaptive-form_main](assets/06-apply-rules-to-adaptive-form_main.png)

本教學課程是 [建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md) 數列。 Adobe建議依照時間順序觀看本系列，以瞭解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

您可以使用規則將互動、商業邏輯和智慧驗證新增至最適化表單。 調適型表單有內建規則編輯器。 規則編輯器提供拖放功能，類似於引導式導覽。 拖放方法是最快速且最簡單的規則建立方法。 規則編輯器還為有興趣測試其編碼技能或將規則提升到更高層級的使用者提供了一個代碼視窗。

如需規則編輯器的詳細資訊，請參閱 [最適化Forms規則編輯器](/help/forms/using/rule-editor.md).

在本教學課程結束時，您將瞭解如何建立規則來：

* 叫用表單資料模型服務以從資料庫擷取資料
* 叫用表單資料模型服務以將資料新增至資料庫
* 執行驗證檢查並顯示錯誤訊息

教學課程每個區段末尾的互動式GIF影像可協助您快速學習及驗證所建置表單的功能。

## 步驟1：從資料庫擷取客戶記錄 {#retrieve-customer-record}

您已遵循下列步驟建立表單資料模型 [建立表單資料模型](/help/forms/using/create-form-data-model.md) 文章。 現在，您可以使用規則編輯器來叫用Forms資料模型服務，以擷取資訊並新增至資料庫。

每個客戶都會獲派一個唯一的客戶ID號碼，這有助於識別資料庫中的相關客戶資料。 下列程式會使用客戶ID從資料庫擷取資訊：

1. 開啟最適化表單進行編輯。

   [http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)

1. 點選 **[!UICONTROL 客戶ID]** 欄位並點選 **[!UICONTROL 編輯規則]** 圖示。 「規則編輯器」視窗隨即開啟。
1. 點選 **[!UICONTROL +建立]** 圖示以新增規則。 它會開啟視覺化編輯器。

   在視覺化編輯器中， **[!UICONTROL 時間]** 陳述式預設為選取。 此外，表單物件(在此案例中， **[!UICONTROL 客戶ID]**)啟動規則編輯器的位置，會於 **[!UICONTROL 時間]** 陳述式。

1. 點選 **[!UICONTROL 選取狀態]** 下拉式清單並選取 **[!UICONTROL 已變更]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

1. 在 **[!UICONTROL 則]** 陳述式，選取 **[!UICONTROL 啟動服務]** 從 **[!UICONTROL 選取動作]** 下拉式清單。
1. 選取 **[!UICONTROL 擷取送貨地址]** 服務來自 **[!UICONTROL 選取]** 下拉式清單。
1. 拖放 **[!UICONTROL 客戶ID]** 欄位(從「表單物件」標籤到 **[!UICONTROL 拖放物件或在這裡選取]** 中的欄位 **[!UICONTROL 輸入]** 方塊。

   ![dropobjectstoinputfield-retrievedata](assets/dropobjectstoinputfield-retrievedata.png)

1. 拖放 **[!UICONTROL 客戶ID、名稱、送貨地址、州/省和郵遞區號]** 欄位(從「表單物件」標籤到 **[!UICONTROL 拖放物件或在這裡選取]** 中的欄位 **[!UICONTROL 輸出]** 方塊。

   ![dropobjectstooutputfield-retrievedata](assets/dropobjectstooutputfield-retrievedata.png)

   點選 **[!UICONTROL 完成]** 以儲存規則。 在規則編輯器視窗上，點選 **[!UICONTROL 關閉]**.

1. 預覽最適化表單。 在中輸入ID **[!UICONTROL 客戶ID]** 欄位。 表單現在可以從資料庫擷取客戶詳細資訊。

   ![retrieve-info](assets/retrieve-information.gif)

## 步驟2：將更新的客戶地址新增至資料庫 {#updated-customer-address}

從資料庫擷取客戶詳細資料後，您可以更新送貨地址、州別和郵遞區號。 下列程式會叫用「表單資料模型」服務，將客戶資訊更新至資料庫：

1. 選取 **[!UICONTROL 提交]** 欄位並點選 **[!UICONTROL 編輯規則]** 圖示。 「規則編輯器」視窗隨即開啟。
1. 選取 **[!UICONTROL 提交 — 按一下]** 規則，然後點選 **[!UICONTROL 編輯]** 圖示。 隨即顯示編輯「提交」規則的選項。

   ![submit-rule](assets/submit-rule.png)

   在WHEN選項中， **[!UICONTROL 提交]** 和 **[!UICONTROL 已點按]** 已選取選項。

   ![submit-is-clicked](assets/submit-is-clicked.png)

1. 在 **[!UICONTROL 則]** 選項，點選 **[!UICONTROL +新增陳述式]** 選項。 選取 **[!UICONTROL 啟動服務]** 從 **[!UICONTROL 選取動作]** 下拉式清單。
1. 選取 **[!UICONTROL 更新送貨地址]** 服務來自 **[!UICONTROL 選取]** 下拉式清單。

   ![update-shipping-address](assets/update-shipping-address.png)

   ![dropobjectstoinputfield-updatedata](assets/dropobjectstoinputfield-updatedata.png)

1. 拖放 **[!UICONTROL 送貨地址、州/省和郵遞區號]** 欄位來自 [!UICONTROL 表單物件] 定位字元至的相應tablename .property （例如customerdetails .shippingAddress）。 **[!UICONTROL 拖放物件或在這裡選取]** 中的欄位 **[!UICONTROL 輸入]** 方塊。 所有以tablename為前置詞的欄位（例如，此使用案例中的customerdetails）都會當作更新服務的輸入資料。 這些欄位中提供的所有內容都會在資料來源中更新。

   >[!NOTE]
   >
   >請勿拖放 **[!UICONTROL 名稱]** 和 **[!UICONTROL 客戶ID]** 至對應tablename.property的欄位（例如customerdetails.name）。 它有助於避免錯誤地更新客戶的名稱和ID。

1. 拖放 **[!UICONTROL 客戶ID]** 欄位來自 [!UICONTROL 表單物件] 標籤切換至中的id欄位 **[!UICONTROL 輸入]** 方塊。 沒有前置詞tablename的欄位（例如，此使用案例中的customerdetails）會作為更新服務的搜尋引數。 此 **[!UICONTROL id]** 此使用案例中的欄位可唯一識別中的記錄  **customerdetails**  表格。
1. 點選 **[!UICONTROL 完成]** 以儲存規則。 在規則編輯器視窗上，點選 **[!UICONTROL 關閉]**.
1. 預覽最適化表單。 擷取客戶的詳細資料、更新送貨地址並提交表單。 當您再次擷取相同客戶的詳細資料時，會顯示更新的送貨地址。

## 步驟3： （額外章節）使用程式碼編輯器執行驗證並顯示錯誤訊息 {#step-bonus-section-use-the-code-editor-to-run-validations-and-display-error-messages}

您應該對表單執行驗證，以確保在表單中輸入的資料正確無誤，並且在資料不正確的情況下會顯示錯誤訊息。 例如，如果在表單中輸入不存在的客戶ID，則會顯示錯誤訊息。

適用性表單提供數個內建驗證的元件，例如電子郵件和數值欄位，您可將其用於常見使用案例。 針對進階使用案例使用規則編輯器，例如在資料庫傳回零(0)記錄（無記錄）時顯示錯誤訊息。

下列程式說明如果表單中輸入的客戶ID不存在於資料庫中，如何建立規則以顯示錯誤訊息。 此規則也會將焦點導向並重設 **[!UICONTROL 客戶ID]** 欄位。 規則使用 [表單資料模型服務的dataIntegrationUtils API](/help/forms/using/invoke-form-data-model-services.md) 檢查客戶ID是否存在於資料庫中。

1. 點選 **[!UICONTROL 客戶ID]** 欄位並點選 `Edit Rules` 圖示。 此 [!UICONTROL 規則編輯器] 視窗隨即開啟。
1. 點選 **[!UICONTROL +建立]** 圖示以新增規則。 它會開啟視覺化編輯器。

   在視覺化編輯器中， **[!UICONTROL 時間]** 陳述式預設為選取。 此外，表單物件(在此案例中， **[!UICONTROL 客戶ID]**)啟動規則編輯器的位置，會於 **[!UICONTROL 時間]** 陳述式。

1. 點選 **[!UICONTROL 選取狀態]** 下拉式清單並選取 **[!UICONTROL 已變更]**.

   ![whencustomeridischanged](assets/whencustomeridischanged.png)

   在 **[!UICONTROL 則]** 陳述式，選取 **[!UICONTROL 啟動服務]** 從 **[!UICONTROL 選取動作]** 下拉式清單。

1. 切換來源 **[!UICONTROL 視覺化編輯器]** 至 **[!UICONTROL 代碼編輯器]**. 切換器控制項位於視窗的右側。 程式碼編輯器隨即開啟，顯示類似下列的程式碼：

   ![程式碼編輯器](assets/code-editor.png)

1. 以下列程式碼取代輸入變數區段：

   ```javascript
   var inputs = {
       "id" : this
   };
   ```

1. 取代 `guidelib.dataIntegrationUtils.executeOperation (operationInfo, inputs, outputs)` 區段，代碼如下：

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, function (result) {
     if (result) {
         result = JSON.parse(result);
       customer_Name.value = result.name;
       customer_Shipping_Address = result.shippingAddress;
     } else {
       if(window.confirm("Invalid Customer ID. Provide a valid customer ID")) {
             customer_Name.value = " ";
            guideBridge.setFocus(customer_ID);
       }
     }
   });
   ```

1. 預覽最適化表單。 輸入不正確的客戶ID。 出現錯誤訊息。

   ![display-validation-error](assets/display-validation-error.gif)
