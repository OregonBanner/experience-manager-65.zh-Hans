---
title: 在最適化表單中使用Adobe Sign
seo-title: Using Adobe Sign in an adaptive form
description: 啟用最適化表單的電子簽章(Adobe Sign)工作流程，以自動化簽署工作流程、簡化單一和多重簽名流程，並以電子方式簽署行動裝置的表單。
seo-description: Enable e-signature (Adobe Sign) workflows for an adaptive form to automate signing workflows, simplify single and multi-signature processes, and to electronically sign forms from mobile devices.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: 4714554609a10e58b1c7141696d694fac46887a6
workflow-type: tm+mt
source-wordcount: '3826'
ht-degree: 0%

---

# 使用 [!DNL Adobe Sign] 在最適化表單中{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] 啟用最適化表單的電子簽章工作流程。 電子簽章可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在一般情況下 [!DNL Adobe Sign] 在最適化表單情境下，使用者需填寫最適化表單來申請服務。 例如，抵押貸款與信用卡申請需要所有借方與共同應徵者的合法簽名。 若要針對類似案例啟用電子簽章工作流程，您可以整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms]. 還有幾個範例是，您可以使用 [!DNL Adobe Sign] 至：

* 透過完全自動化的提案、報價和合約程式，完成任何裝置的交易。
* 更快完成人力資源流程，為員工提供數位體驗。
* 縮短合約週期時間，讓您的廠商更快上線。
* 建立自動化常見流程的數位工作流程。

[!DNL Adobe Sign] 與AEM整合 [!DNL Forms] 支援：

* 單一和多使用者簽署工作流程
* 循序和同步簽署工作流程
* 表單內和表單外簽署體驗
* 以匿名或登入使用者身分簽署表單
* 動態簽署程式(與AEM整合) [!DNL Forms] 工作流程)
* 透過知識庫、電話和社交設定檔進行驗證

瞭解 [搭配最適化表單使用Adobe Sign的最佳做法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) 以建立更好的簽署體驗。

## 前提条件 {#prerequisites}

使用前 [!DNL Adobe Sign] 在最適化表單中：

* 確定AEM [!DNL Forms] 雲端服務已設定為使用 [!DNL Adobe Sign]. 如需詳細資訊，請參閱 [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* 保持簽名者清單準備就緒。 您至少需要每個簽署者的電子郵件地址。

## 設定 [!DNL Adobe Sign] 最適化表單 {#configure-adobe-sign-for-an-adaptive-form}

執行以下步驟來設定 [!DNL Adobe Sign] 最適化表單：

1. [編輯Adobe符號的最適化表單屬性](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [將Adobe Sign欄位新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [為最適化表單啟用Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [為最適化表單選取Adobe Sign Cloud Service](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [將Adobe Sign簽署者新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [為最適化表單選取提交動作](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![签名者详细信息](assets/signer_details_new.png)

### 編輯最適化表單屬性 [!DNL Adobe Sign] {#enableadobesign}

設定最適化表單屬性 [!DNL Adobe Sign] 適用於現有或新的最適化表單。

[為Adobe Sign建立最適化表單](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 說明建立基本最適化表單的步驟。 另請參閱 [建立最適化表單](../../forms/using/creating-adaptive-form.md) 以取得建立最適化表單時可用的其他選項。

#### 建立最適化表單 [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

執行以下步驟，建立可啟用簽名的最適化表單：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **[!UICONTROL 建立]** 並選取 **[!UICONTROL 最適化表單]**. 範本清單隨即顯示。 選取範本並點選 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 基本]** 標籤：

   1. 指定 **[!UICONTROL 名稱]** 和 **[!UICONTROL 標題]** 最適化表單的預設值。

   1. 選取 [設定容器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 在設定時建立 [!DNL Adobe Sign] 使用AEM [!DNL Forms].

      >[!NOTE]
      >
      >此 **[!UICONTROL Adobe Sign Cloud Service]** 下拉式清單會顯示在此欄位中選取的設定容器中設定的雲端服務。 此 **[!UICONTROL Adobe Sign Cloud Service]** 下拉式清單位於 **[!UICONTROL 電子簽章]** 最適化表單屬性的區段 **[!UICONTROL 啟用Adobe Sign]** 選項。

1. 在 **[!UICONTROL 表單模型]** 索引標籤中，選取下列其中一個選項：

   * 選取 **[!UICONTROL 建立表單範本為記錄檔案範本的關聯]** 選項並選取記錄檔案範本。 如果您使用以表單範本為基礎的最適化表單，則傳送以供簽署的檔案只會顯示以相關表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   * 選取 **[!UICONTROL 產生記錄檔案]** 選項。 如果您使用已啟用最適化表單的記錄檔案選項，則傳送以供簽署的檔案會顯示最適化表單的所有欄位。

1. 點選 **[!UICONTROL 建立。]** 建立可啟用簽名的最適化表單，該表單可用於新增 [!DNL Adobe Sign] 欄位。

#### 編輯最適化表單 [!DNL Adobe Sign] {#editafsign}

執行以下步驟以使用 [!DNL Adobe Sign] 在現有的最適化表單中：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取最適化表單並點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 基本]** 索引標籤中，選取 [設定容器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 在設定時建立 [!DNL Adobe Sign] 使用AEM [!DNL Forms].
1. 在 **[!UICONTROL 表單模型]** 索引標籤中，選取下列其中一個選項：

   * 選取 **[!UICONTROL 建立表單範本為記錄檔案範本的關聯]** 選項並選取記錄檔案範本。 如果您使用以表單範本為基礎的最適化表單，則傳送以供簽署的檔案只會顯示以相關表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   * 選取 **[!UICONTROL 產生記錄檔案]** 選項。 如果您使用已啟用最適化表單的記錄檔案選項，則傳送以供簽署的檔案會顯示最適化表單的所有欄位。

1. 點選 **[!UICONTROL 儲存並關閉]**. 已針對以下專案啟用最適化表單 [!DNL Adobe Sign].

### 將Adobe Sign欄位新增至最適化表單 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 有多種欄位可放置在調適型表單上。 這些欄位接受各種型別的資料，例如簽名、縮寫、公司或標題，並協助在簽名期間收集額外的資訊以及簽名。 您可以使用 [!DNL Adobe Sign] 要置入的區塊元件 [!DNL Adobe Sign] 最適化表單中不同位置的欄位。

執行以下步驟，將欄位新增至最適化表單，並自訂與這些欄位相關的各種選項：

1. 拖放 **[!UICONTROL Adobe Sign區塊]** 元件從元件瀏覽器變更為最適化表單。 此 [!DNL Adobe Sign] 區塊元件具有所有支援的 [!DNL Adobe Sign] 欄位。 依預設，它會新增 **簽章** 最適化表單的欄位。

   ![簽署區塊](assets/sign_block_new.png)

   根據預設， [!DNL Adobe Sign] 封鎖在已發佈的最適化表單中不可見。 它只會顯示在簽署檔案中。 您可以變更下列專案的可見度 [!DNL Adobe Sign] 從的屬性封鎖 [!DNL Adobe Sign] 區塊元件。

   >[!NOTE]
   >
   >    * 使用 [!DNL Adobe Sign] 區塊並非強制使用 [!DNL Adobe Sign] 在最適化表單中。 如果您不使用 [!DNL Adobe Sign] 封鎖並新增簽署者的欄位，則預設簽名欄位會顯示在簽署檔案的底部。
   >    * 使用 [!DNL Adobe Sign] 僅封鎖那些自動產生記錄檔案的最適化表單。 如果您使用自訂XDP來產生記錄檔案或表單範本式的最適化表單， [!DNL Adobe Sign] 不支援此區塊。


1. 選取 **[!UICONTROL Adobe Sign區塊]** 元件並點選 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 圖示。 它會顯示新增欄位和格式化欄位外觀的選項。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **答：** 選取並新增 [!DNL Adobe Sign] 欄位。 **B.** 展開 [!DNL Adobe Sign] 封鎖至全熒幕檢視

1. 點選 **[!UICONTROL Adobe Sign] 欄位** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 圖示。 它會顯示選取和新增的選項 [!DNL Adobe Sign] 欄位。

   展開 **[!UICONTROL 型別]** 下拉式欄位以選取 [!DNL Adobe Sign] 欄位並點選「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以將選取的欄位新增至 [!DNL Adobe Sign] 區塊。 此 **[!UICONTROL 型別]** 下拉式欄位包含簽名、簽署者資訊和資料欄位型別。 [!DNL Adobe Sign] 與AEM整合 [!DNL Forms] 中列出的支援欄位 [!UICONTROL 型別] 下拉式方塊。 如需關於以下專案的詳細資訊： [!DNL Adobe Sign] 欄位，請參閱 [Adobe Sign檔案](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   必須為欄位提供唯一名稱。 您也可以選取必要選項，將欄位標示為必要欄位。 除了 **[!UICONTROL 名稱]** 和 **[!UICONTROL 必填]** 選項，部分 [!DNL Adobe Sign] 欄位有更多選項。 例如，遮色片和多行。 此外，請為每一個檔案指定唯一的名稱 [!DNL Adobe Sign] 欄位是位於相同還是不同的欄位 [!DNL Adobe Sign] 個區塊。

   如果您選取 **[!UICONTROL 數位簽名]** 從下拉式清單中，您可以將數位簽名套用至最適化表單：

   * 使用雲端簽名透過進行線上簽署 [數位ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供者代管。
   * 透過Adobe Acrobat下載檔案，或使用智慧卡、USB代號或檔案式數位IDReader在本機。

### 啟用 [!DNL Adobe Sign] 最適化表單 {#enableadobsignforanadaptiveform}

開箱即用 [!DNL Adobe Sign] 未針對最適化表單啟用。 執行以下步驟來啟用它：

1. 在「內容」瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/configure.png) 圖示。 它會開啟屬性瀏覽器並顯示最適化表單容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽章]** 摺疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 最適化表單。

### 選取 [!DNL Adobe Sign] Cloud Service和簽署順序 {#selectadobesigncloudserviceforanadaptiveform}

您可以設定多個 [!DNL Adobe Sign] AEM執行個體的服務 [!DNL Forms]. 建議您為每個功能（人力資源、財務等）分別設定一組服務。 它可讓您更輕鬆追蹤及報告已簽署的檔案。 例如，一家銀行擁有多個部門。 您可以為每個部門設定個別的設定，以便更妥善地追蹤檔案。

一個檔案也可以有多個簽署者。 例如，信用卡申請可以有多個應徵者。 在開始處理申請之前，銀行需要所有申請者的簽名。 對於多簽署者情況，您可以選取以循序或同時順序簽署檔案。

執行以下步驟來選取雲端服務和簽署順序：

![雲端服務](assets/cloud-service.png)

1. 在「內容」瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/configure.png) 圖示。 它會開啟屬性瀏覽器並顯示最適化表單容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽章]** 摺疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 最適化表單。
1. 從已設定的清單中選取雲端服務 [!DNL Adobe Sign] Cloud Services。

   如果 **[!UICONTROL Adobe Sign Cloud Service]** 清單是空的，請遵循 [使用AEM Forms設定Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) 設定服務的文章。

   下拉式清單會列出以下專案中存在的雲端服務： `global` 「工具>中的資料夾」 **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 此外，下拉式清單也會列出您在中選擇的資料夾中存在的雲端服務 **[!UICONTROL 設定容器]** 欄位建立最適化表單時。

1. 從中選擇簽署順序 **[!UICONTROL 簽署者可以簽署]** 對話方塊。 [!DNL Adobe Sign] 歌手可以簽署最適化表單 **[!UICONTROL 循序]**  — 一個接著一個的簽署者，或 **[!UICONTROL 同時]**  — 以任何順序。

   依序由一位簽署者一次收到需要簽署的表單。 簽名者完成檔案簽名後，表單會傳送給下一個簽名者，依此類推。

   以同時順序，多位簽署者可以一次簽署表單。

1. [將簽署者新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) 然後點選「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存變更。


### 將簽署者新增至最適化表單 {#addsignerstoanadaptiveform}

一個最適化表單只能有一個或多個簽署者。 新增簽署者時，您也可以為簽署者設定驗證詳細資訊。 您也可以選擇表單填寫者和歌手是否為同一個人。 執行以下步驟，新增並提供簽署者的各種詳細資訊：

1. 在「內容」瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/configure.png) 圖示。 它會開啟具有最適化表單容器屬性的屬性瀏覽器。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽章]** 摺疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 最適化表單。
1. 點選 **[!UICONTROL 新增簽署者]** 在 **[!UICONTROL 簽署者設定]**. 它會新增簽名者至最適化表單。 您可以新增多個 [!DNL Adobe Sign] 最適化表單的簽署者。
   ![phone-details](assets/phone-details.png)

1. 按一下 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 圖示來指定下列有關簽署者的資訊：

   * **[!UICONTROL 標題]：** 指定標題以唯一識別簽署者。

   * **[!UICONTROL 签名者与填写表单的人员是否为同一人？]：** 選取 **是**，如果表單填寫者與第一個簽署者是同一個人。 如果選項設為 **否，** 則請勿在最適化表單中使用簽名步驟元件。 如果表單包含「簽名步驟」元件，則欄位會自動設定為「是」。

   * **[!UICONTROL 簽署者電子郵件地址]：** 指定簽署者的電子郵件地址。 簽署者在指定的電子郵件地址上接收要簽署的檔案/表單。 您可以選擇使用表單欄位、登入使用者的AEM使用者設定檔中提供的電子郵件地址，或手動輸入電子郵件地址。 此為必要步驟。 確保第一個簽名者或唯一簽名者的電子郵件地址（如果是單一簽名者）與 [!DNL Adobe Sign] 用於設定AEM雲端服務的帳戶。

   * **[!UICONTROL 簽署者驗證方法]：** 指定在開啟表單進行簽署之前驗證使用者的方法。 您可以在電話、知識庫及以社交身分為基礎的驗證之間進行選擇。
   >[!NOTE]
   >
   >    * 依預設，社交身分型驗證會提供使用Facebook、Google和LinkedIn驗證的選項。 您可以聯絡 [!DNL Adobe Sign] 支援啟用其他社交驗證服務提供者。


   * **[!DNL Adobe Sign]要填寫或簽署的欄位：** 選取 [!DNL Adobe Sign] 簽署者的欄位。 最適化表單可以有多個 [!DNL Adobe Sign] 欄位。 您可以選擇為簽署者啟用特定欄位。 欄位會顯示所有可用的 [!DNL Adobe Sign] 個區塊。 當您選取區塊時，會選取區塊的所有欄位。 您可以使用X圖示來取消選取欄位。

   ![簽署者詳細資訊](assets/signer-details.png)

   上圖有兩個範例 [!DNL Adobe Sign] 區塊：個人資訊和辦公室詳細資訊

   點選「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示。 簽署者已新增並設定。

### 為最適化表單選取提交動作 {#selectsubmitactionforanadaptiveform}

在您之後，新增 [!DNL Adobe Sign] 最適化表單的欄位，啟用 [!DNL Adobe Sign] 在表單容器中，選取 [!DNL Adobe Sign] Cloud Service並新增 [!DNL Adobe Sign] 簽署者，請為最適化表單選取適當的提交動作。 如需最適化表單提交動作的詳細資訊，請參閱 [設定提交動作](../../forms/using/configuring-submit-actions.md).

此外， [!DNL Adobe Sign] 啟用的最適化表單只會在所有簽署者簽署表單後提交。 您可以在Forms Portal的「等待簽署」區段中找到部分簽署的表單。 [!DNL Adobe Sign] 設定服務持續輪詢 [!DNL Adobe Sign] 伺服器位置 [規則間隔](../../forms/using/adobe-sign-integration-adaptive-forms.md) 驗證簽名狀態。 如果所有簽署者完成表單簽署，則會啟動提交動作服務並提交表單。 如果您使用自訂提交動作，而表單會使用 [!DNL Adobe Sign]，請更新您的自訂提交動作以使用提交動作服務。

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

您的表單簽署體驗已就緒。 您可以預覽表單以驗證簽署體驗。 在已發佈的表單上， [!DNL Adobe Sign] 當簽署者收到透過電子郵件簽署的表單時，會顯示封鎖欄位。 此體驗也稱為表單外簽名體驗。 您也可以為第一個簽署者設定表單內簽署體驗，如需詳細步驟，請參閱 [建立表單內簽名體驗](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## 設定最適化表單的雲端簽名 {#configure-cloud-signatures-for-an-adaptive-form}

雲端數位簽名或遠端簽名是新一代數位簽名，可在案頭、行動裝置和Web上運作，並符合簽名者驗證的最高規範與保證。 您可以使用雲端數位簽名來簽署調適型表單。

晚於 [編輯Adobe簽署的適用性表單屬性](../../forms/using/working-with-adobe-sign.md#enableadobesign)，執行以下步驟以將雲端簽名欄位新增至最適化表單：

1. 拖放 **[!UICONTROL Adobe Sign區塊]** 元件從元件瀏覽器變更為最適化表單。 此 [!UICONTROL Adobe Sign區塊] 元件具有所有支援的 [!DNL Adobe Sign] 欄位。 依預設，它會新增 **[!UICONTROL 簽章]** 最適化表單的欄位。

   ![簽署區塊](assets/sign-block-new.png)

1. 選取 **[!UICONTROL Adobe Sign區塊]** 元件並點選 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 圖示。 它會顯示新增欄位和格式化欄位外觀的選項。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **答：** 選取並新增 [!DNL Adobe Sign] 欄位。 **B.** 展開 [!DNL Adobe Sign] 封鎖至全熒幕檢視

1. 點選 **[!UICONTROL Adobe Sign欄位]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 圖示。 它會顯示選取和新增的選項 [!DNL Adobe Sign] 欄位。

   展開 **[!UICONTROL 型別]** 要選取的下拉式欄位 **[!UICONTROL 數位簽名]** 然後點選 **完成** 圖示以將選取的欄位新增至 [!DNL Adobe Sign] 區塊。

   ![數位簽名](assets/digital_signatures_new.png)

   必須為欄位提供唯一名稱。

   使用以下方法將數位簽名套用至最適化表單：

   * 雲端簽名：使用 [數位ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供者代管。
   * Adobe Acrobat或Reader：使用Adobe Acrobat或Reader下載並開啟檔案，以使用智慧卡、USB權杖或檔案式數位ID簽名。

   將雲端簽名欄位新增至最適化表單後，執行以下步驟以完成設定程式：

   * [為最適化表單啟用Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [為最適化表單選取Adobe Sign Cloud Service](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [將Adobe Sign簽署者新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [為最適化表單選取提交動作](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## 建立表單內簽名體驗 {#create-in-form-signing-experience}

使用者也可以在填寫表單時簽署最適化表單。 此體驗也稱為表單內簽名體驗。 表單內簽名體驗僅適用於多位簽名者環境中的第一位歌手。 執行以下步驟，為最適化表單建立表單內簽名體驗：

1. [新增並設定簽名步驟元件](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [新增摘要步驟元件](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![表單內簽名體驗](assets/in_form_signing_experience_new.png)

### 新增並設定簽名步驟元件 {#add-and-configure-the-signature-step-component}

使用「簽名步驟」元件提供一個區域，以電子方式簽署填寫的表單。 呈現包含「簽名步驟」元件的區段時，會顯示填寫表單的可簽署PDF版本。 簽章步驟元件會佔據可用於表單的完整寬度。 建議在包含簽名步驟元件的區段上不要有任何其他元件。

執行以下步驟來設定「簽名步驟」元件：

1. 拖放 **[!UICONTROL 簽章步驟]** 元件從「元件」瀏覽器移至表單。
1. 選取新新增的簽名步驟元件，然後點選 **設定** ![設定](assets/configure.png) 圖示。 它會開啟屬性瀏覽器並顯示簽名步驟屬性。 設定下列屬性：

   * **[!UICONTROL 名稱]**：指定元件的名稱。

   * **[!UICONTROL 標題]：** 指定元件的唯一標題。
   * **[!UICONTROL 範本訊息]：** 指定在載入簽名PDF時要顯示的訊息。 [!DNL Adobe Sign] 服務需要一些時間來準備和載入簽名PDF。
   * **[!UICONTROL 簽署服務]：** 選取 **[!DNL Adobe Sign]** 選項。

   * **[!UICONTROL 使用舊版E-sign元件]**：如果您在中使用個別的最適化表單 [AEM Forms工作區](../../forms/using/introduction-html-workspace.md)， AEM [!DNL Forms] 應用程式，或基礎的最適化表單具有舊版電子簽章元件，請選取 **使用舊版E-sign元件** 選項。

   * **[!UICONTROL 設定]**：選取設定([!DNL Adobe Sign] Cloud Service)。 下拉式方塊僅適用於 **使用舊版E-sign元件** 選項已啟用。

   * **[!UICONTROL CSS類別]**：指定元件的CSS類別。

   點選「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存變更。

   ![簽章步驟](assets/signature_step_new.png)

   >[!NOTE]
   >
   >* 當您拖放 **[!UICONTROL 簽章步驟]** 表單的元件， **[!UICONTROL 簽署者和填表人是否相同？]** 選項會自動設定為 **是**. 需要保持表單正常運作。
   >* 在簽名步驟元件後使用摘要步驟元件以獲得最佳體驗。 在簽名步驟元件中完成表單簽名後，「摘要」步驟會自動並立即提交表單。 如果您不使用摘要步驟，則只有在使用設定的間隔後，才會觸發自動提交。 [Adobe Sign設定服務](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).

   >
   >一些最佳實務如下：
   >
   >* 包含簽名步驟的最適化表單面板一律在最適化表單的最後一個或第二個面板中。 只有在最後一個面板包含「摘要」步驟時，它才能成為第二個最後一個面板。
   >* 包含簽名或摘要步驟元件的面板不能包含任何其他元件。
   >* 包含簽名步驟的最適化表單不能有提交按鈕。
   >* 包含簽名步驟的最適化表單的提交透過背景服務或摘要步驟處理。 如果有一個已設定的簽署者也在填寫表單，則使用「摘要」步驟處理最適化表單提交的優點是會立即評估簽署者是否已簽署表單並叫用提交動作。 背景服務需要更多時間來評估是否所有已設定的簽署者都已簽署表單，並延遲提交最適化表單。
   >* 將表單設計為不允許使用者從包含簽名或摘要步驟的面板導覽回來。



### 設定感謝頁面或摘要步驟元件 {#configure-the-thank-you-page-or-summary-step-component}

此 **摘要步驟** 元件會自動提交表單、填入自訂摘要頁面內的資訊，並顯示已提交表單的摘要。 它也會取得傳回對應中的必要資訊。 摘要步驟元件會佔據表單可用的完整寬度。 建議在包含摘要步驟元件的區段上不要有任何其他元件。

現在，表單中的簽名體驗已準備就緒。 您可以預覽表單以驗證簽署體驗。

## 常见问题 {#frequently-asked-questions}

**問：** 您可以將最適化表單內嵌在其他最適化表單中。 內嵌的最適化表單可以是 [!DNL Adobe Sign] 已啟用？
**ans：** 否， AEM [!DNL Forms] 不支援使用內嵌 [!DNL Adobe Sign] 啟用最適化表單以供簽署

**問：** 當我使用進階範本建立最適化表單並開啟它進行編輯時，出現錯誤訊息「電子簽章或簽署者設定不正確」。 出現。 如何解決錯誤訊息？
**ans：** 使用進階範本建立的最適化表單已設定為使用 [!DNL Adobe Sign]. 若要解決錯誤，請建立並選取 [!DNL Adobe Sign] 雲端設定和設定 [!DNL Adobe Sign] 最適化表單的簽署者。

**問：** 我可以使用 [!DNL Adobe Sign] 最適化表單的靜態文字元件中的文字標籤？
**ans：** 可以，您可以在文字元件中使用文字標籤來新增 [!DNL Adobe Sign] 欄位至 [記錄檔案](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) （僅限自動產生的記錄檔案選項）啟用的最適化表單。 若要瞭解建立文字標籤的程式和規則，請參閱 [Adobe Sign檔案](https://helpx.adobe.com/sign/using/text-tag.html). 另請注意，調適型表單對文字標籤的支援有限。 您只能使用文字標籤來建立符合以下條件的欄位： [Adobe Sign區塊](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) 支援。

**問：** AEM [!DNL Forms] 提供兩者 [!UICONTROL Adobe Sign區塊] 和簽名步驟元件。 這些可否在最適化表單中同時使用？
**ans：** 您可以在表單中同時使用這兩個元件。 以下是一些使用這些元件的建議：

**Adobe Sign區塊：** 您可以使用 [!UICONTROL Adobe Sign區塊] 新增 [!UICONTROL Adobe Sign] 最適化表單上的任何欄位。 它還有助於將特定欄位指派給簽署者。 預覽或發佈最適化表單時 [!UICONTROL Adobe Sign] 預設不會顯示區塊。 這些區塊僅在簽署檔案中啟用。 在簽署檔案中，只會啟用指派給簽署者的欄位。 [!UICONTROL Adobe Sign] 區塊可搭配第一和後續簽署者使用。

**簽章步驟元件：** 您可以使用簽名步驟元件來建立表單內簽名體驗。 它只允許第一個簽署者在填寫表單時簽署。 呈現包含簽名步驟元件的區段時，會顯示表單的可簽署PDF版本。 它通常是最後一個或倒數第二部分，後面接著表單的摘要元件。

## 疑难解答 {#troubleshoot}

### [!DNL Adobe Sign] 合約失敗 {#adobe-sign-agreement-failures}

**問題**
時間 [!DNL Adobe Sign] 已針對最適化表單設定服務，該服務無法建立 [!DNL Adobe Sign] 最適化表單的合約。

**解决方法**

* 檢查 [Adobe Sign雲端服務的設定](../../forms/using/adobe-sign-integration-adaptive-forms.md) 用於最適化表單中。
* 確定API應用程式位於 [!DNL Adobe Sign] 用於設定的伺服器 [!DNL Adobe Sign] Cloud Service有必要的許可權。
* 如果您使用多個 [!DNL Adobe Sign] 雲端服務，指向 **[!UICONTROL oAuth URL]** 所有服務中的相同專案 **[!UICONTROL Adobe Sign Shard]**.

* 使用個別的電子郵件地址進行設定 [!DNL Adobe Sign] 帳戶，以及第一個簽署者和單一簽署者。 第一個簽署者或唯一簽署者的電子郵件地址（若為單一簽署者）不可與 [!DNL Adobe Sign] 用於設定AEM雲端服務的帳戶。

### AEM [!DNL Forms] 為設定的工作流程 [!DNL Adobe Sign] 啟用的最適化表單未開始 {#adobe-sign-aem-form-workflow-failures}

**問題**
時間 [!DNL Adobe Sign] 針對最適化表單而設定，工作流程則使用叫用來設定 [!DNL Forms] 工作流程選項未啟動。

**解决方法**

* 當您使用 [!DNL Adobe Sign] 若無簽章步驟，或表單需要多人簽章，AEM [!DNL Forms] 伺服器會等待排程器確認所有人員已簽署表單。 排程器只會在所有人員完成簽署後提交調適型表單，而工作流程只會在成功提交調適型表單後開始。 您可以縮短 [排程器](adobe-sign-integration-adaptive-forms.md) 以快速檢查表單簽署狀態並加快表單提交。


## 相关文章 {#related-articles}

* [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [搭配最適化表單使用Adobe Sign的最佳做法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [將Adobe Sign與AEM Forms搭配使用（影片）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
