---
title: 在AEM中建立Adobe Campaign Forms
description: AEM可讓您建立並使用與您網站上的Adobe Campaign互動的表單。 特定欄位可以插入您的表單並對應至Adobe Campaign資料庫。
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# 在AEM中建立Adobe Campaign Forms{#creating-adobe-campaign-forms-in-aem}

AEM可讓您建立並使用與您網站上的Adobe Campaign互動的表單。 特定欄位可以插入您的表單並對應至Adobe Campaign資料庫。

您可以管理新的連絡人訂閱、取消訂閱和使用者設定檔資料，同時將其資料整合到您的Adobe Campaign資料庫中。

若要在AEM中使用Adobe Campaign表單，您必須依照本檔案所述的步驟操作：

1. 讓範本可供使用。
1. 建立表單。
1. 編輯表單內容。

預設提供三種特定於Adobe Campaign的表單型別：

* 儲存設定檔
* 訂閱服務
* 取消訂閱服務

這些表單會定義一個URL引數，該引數接受Adobe Campaign設定檔的加密主要金鑰。 表單會根據此URL引數更新相關Adobe Campaign設定檔的資料。

雖然您是獨立建立這些表單，但在典型的使用案例中，您會在電子報內容內產生表單頁面的個人化連結，讓收件者可以開啟連結，並調整其設定檔資料（無論是取消訂閱、訂閱或更新其設定檔）。

表單會根據使用者自動更新。 另請參閱 [編輯表單內容](#editing-form-content) 以取得詳細資訊。

## 讓範本可供使用 {#making-a-template-available}

您必須先在AEM應用程式中提供不同的範本，才能建立Adobe Campaign專用的表單。

若要這麼做，請參閱 [範本檔案](/help/sites-developing/page-templates-static.md#templateavailability).

首先，請檢查製作和發佈執行個體之間的連線，以及Adobe Campaign是否正常運作。 另請參閱 [與Adobe Campaign Standard整合](/help/sites-administering/campaignstandard.md) 或 [與Adobe Campaign 6.1整合](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>確定 **acMapping** 頁面上的屬性 **jcr：content** 節點已設為 **mapRecipient** 或 **設定檔** 分別使用Adobe Campaign 6.1.x或Adobe Campaign Standard時

### 建立表單 {#creating-a-form}

1. 在siteadmin中開始。
1. 捲動瀏覽樹狀結構，以抵達您要在所選網站中建立表單的位置。
1. 選取 **新增** > **新增頁面……**.
1. 選取 **Adobe Campaign設定檔(AC 6.1)** 或 **Adobe Campaign設定檔(ACS)** 範本並輸入頁面屬性。

   >[!NOTE]
   >
   >如果範本無法使用，請參閱 [讓範本可供使用](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) 區段。

1. 按一下 **建立** 以建立表單。

   ![chlimage_1-187](assets/chlimage_1-187.png)

   然後，您可以 [編輯和設定表單內容](#editing-form-content).

## 編輯表單內容 {#editing-form-content}

Adobe Campaign專用的Forms具有特定元件。 這些元件可讓您選擇將表單的每個欄位連結到Adobe Campaign資料庫中的欄位。

>[!NOTE]
>
>如果需要的範本無法使用，請參閱 [讓範本可供使用](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

本節僅詳細說明Adobe Campaign的特定連結。 如需如何在Adobe Experience Manager中使用表單的更多一般概覽資訊，請參閱 [Editmode元件](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. 導覽至您要編輯的表單。
1. 在工具箱中，選取 **頁面** > **頁面屬性……** 然後前往 **Cloud Services** 頁簽的快顯視窗。
1. 按一下「 」以新增Adobe Campaign服務 **新增服務**，然後在服務的下拉式清單中選取與您的Adobe Campaign執行個體對應的設定。 設定執行個體之間的連線時，會執行此設定。 如需詳細資訊，請參閱 [將AEM連線至Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >如有必要，請按一下掛鎖圖示以解除鎖定設定，進而新增Adobe Campaign服務。

1. 使用存取表單的一般引數 **編輯** 在表單開頭找到按鈕。 此 **表單** 索引標籤可讓您選取感謝頁面，在驗證表單後將使用者重新導向該頁面。

   此 **進階** 表單可讓您選取表單型別。 此 **張貼選項** 欄位可讓您選擇三種型別的Adobe Campaign表單：

   * **Adobe Campaign：儲存設定檔**：可讓您在Adobe Campaign （預設值）中建立或更新收件者。
   * **Adobe Campaign：訂閱服務**：可讓您在Adobe Campaign中管理收件者的訂閱。
   * **Adobe Campaign：取消訂閱服務**：可讓您在Adobe Campaign中取消收件者的訂閱。

   此 **動作設定** 欄位可讓您指定是否想要在Adobe Campaign資料庫中建立收件者設定檔（如果尚未存在）。 若要這麼做，請核取 **如果不存在，則建立使用者** 選項。

1. 將選取的元件從工具箱拖放至表單中，以新增這些元件。 如需可用Adobe Campaign特定元件的詳細資訊，請參閱 [Adobe表單元件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 按兩下新增的欄位以設定它們。 此 **Adobe Campaign** 索引標籤可讓您將欄位連結至Adobe Campaign收件者表格中的欄位。 您也可以指定欄位是否為調解金鑰的一部分，以允許辨識Adobe Campaign資料庫中已存在的收件者。

   >[!CAUTION]
   >
   >此 **元素名稱** 每個表單欄位必須不同。 如有需要，請加以變更。
   >
   >每個表單都必須包含 **加密的主要金鑰** 元件，以正確管理Adobe Campaign資料庫中的收件者。

1. 選取以啟動頁面 **頁面** > **啟動頁面** 在工具箱中。 頁面已在您的網站上啟動。 您可以前往AEM發佈執行個體來檢視它。 在驗證表單後，Adobe Campaign資料庫中的資料就會更新。

## 測試表單 {#testing-a-form}

建立表單並編輯表單內容後，您可能需要手動測試表單是否按預期運作。

>[!NOTE]
>
>您必須擁有 **加密的主要金鑰** 元件。 在「元件」中選取Adobe Campaign ，以便只顯示那些元件。
>
>雖然在此程式中，您需手動輸入設定檔號碼，但實際上，使用者會在電子報中取得此頁面的連結（無論是取消訂閱、訂閱或更新您的設定檔）。 會根據使用者自動更新epk。
>
>若要建立該連結，請使用變數 **主要資源識別碼**(Adobe Campaign Standard)或 **加密的識別碼** (Adobe Campaign 6.1) (例如，在 **文字與個人化（行銷活動）** 元件)，可連結至Adobe Campaign中的epk。

若要這麼做，您需要手動取得Adobe Campaign設定檔的EPK，然後將其附加至URL：

1. 若要取得Adobe Campaign設定檔的加密主要金鑰(EPK)：

   * 在Adobe Campaign Standard — 導覽至 **設定檔與對象** > **設定檔**，會列出現有的設定檔。 請確定表格顯示 **主要資源識別碼** 欄中的欄位（這可以按一下/點選來設定） **設定清單**)。 複製所需設定檔的主要資源識別碼。
   * 在Adobe Campaign 6.11中，前往 **設定檔與目標** >  **收件者**，會列出現有的設定檔。 請確定表格顯示 **加密的識別碼** 欄中的欄位(這可以透過在專案上按一下右鍵並選取 **設定清單……**)。 複製所需設定檔的加密識別碼。

1. 在AEM中，開啟發佈執行個體上的表單頁面，並從步驟1將EPK附加為URL引數：使用您先前在編寫表單時在EPK元件中定義的相同名稱(例如： `?epk=...`)
1. 此表單現在可用於修改與已連結Adobe Campaign設定檔相關聯的資料和訂閱。 修改部分欄位並提交表單後，您可以在Adobe Campaign中確認適當的資料已更新。

在驗證表單後，Adobe Campaign資料庫中的資料就會更新。
