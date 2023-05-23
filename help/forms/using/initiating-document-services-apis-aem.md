---
title: 從AEM工作流程啟動Document Services API
seo-title: Initiate Document Services APIs from AEM Workflow
description: 瞭解如何在DDX或提供的輸入上叫用AEM檔案服務。 另請參閱如何將PDF轉換為PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---

# 從AEM工作流程啟動Document Services API  {#initiate-document-services-apis-from-aem-workflow}

## 組合器 {#assembler}

AEM Forms提供自訂工作流程，以叫用下列Assembler服務API：

* **叫用**：對提供的輸入叫用輸入DDX中指定的操作。
* **toPDFA**：將輸入PDF檔案轉換為PDF/A檔案。

### 叫用DDX工作流程 {#invoke-ddx-workflow}

此 **啟動DDX** 工作流程會叫用 `Invoke` 組合器服務API，可用於組合或分解檔案、為PDF新增浮水印等。

1. 拖曳 **[!UICONTROL 啟動DDX]** Sidekick中「Forms Workflow」標籤下的工作流程步驟。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話方塊中，設定輸入檔案、環境選項和輸出檔案，然後按一下 **[!UICONTROL 確定]**.

#### 輸入檔案 {#input-documents}

叫用DDX工作流程需要下列輸入檔案：

* **DDX**：此為呼叫DDX工作流程步驟的必要輸入，可透過從DDX輸入下拉式清單中選取下列選項之一來指定。

   * *相對於裝載*： DDX輸入檔案是相對於工作流程專案的裝載資料夾。
   * *使用裝載*：工作流程專案的裝載會用作輸入DDX檔案。
   * *絕對路徑*：CRX存放庫中DDX檔案的絕對路徑。

* **從付款載入建立地圖**：選取後，裝載資料夾下的所有檔案都會新增到的Input Document地圖中 `invoke` 組合器中的API。 每個檔案的節點名稱都會當做對應中的索引鍵。

* **輸入檔案的地圖**：指定輸入檔案的對應。 您可以新增任意數量的專案，每個專案都會指定對應中的檔案索引鍵和檔案來源。

#### 環境選項 {#environment-options}

「環境選項」索引標籤可讓您為叫用API設定各種處理選項。

* *工作記錄層級*：指定處理記錄的記錄層級。
* *僅驗證*：檢查輸入DDX的有效性。

* *因錯誤而失敗*：指定發生錯誤時，對Assembler服務的呼叫是否應失敗。 預設值為False。

#### 輸出檔案 {#output-documents}

根據輸入DDX，叫用API可以產生多個輸出檔案。 「輸出檔案」標籤可讓您選取將儲存輸出檔案的位置。

1. *將輸出儲存在承載中*：將輸出檔案儲存在承載資料夾下，或如果承載是檔案則覆寫承載。
1. *輸出檔案的地圖*：允許為每個輸出檔案新增一個專案，以明確指定儲存每個輸出檔案的位置。 每個專案都會指定檔案以及儲存檔案的位置。 輸出檔案可能會覆寫承載或儲存在承載資料夾下。 有多個輸出檔案時，此功能會很有用。

1. *工作記錄*：指定工作記錄檔案的儲存位置，這有助於疑難排解失敗。

### 轉換為PDF/工作流程 {#convert-to-pdf-a-workflow}

轉換成PDF/工作流程步驟會叫用 `toPDFA` 組合器服務API。 它用於將PDF檔案轉換為PDF/A相容檔案。

1. 拖曳 **[!UICONTROL ConvertToPDFA]** Sidekick中「Forms Workflow」標籤下的工作流程步驟。

1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話方塊中，設定輸入檔案、轉換選項和輸出檔案，然後按一下 **[!UICONTROL 確定]**.

#### 輸入檔案 {#input-documents-1}

以下列其中一種方式指定要轉換為PDF/A相容檔案的檔案來源。

* *相對於裝載*：輸入檔案是相對於工作流程專案的裝載資料夾。
* *使用裝載*：工作流程專案的裝載會用作輸入檔案。
* *絕對路徑*：CRX存放庫中輸入檔案的絕對路徑。

#### 轉換選項 {#conversion-options}

「轉換選項」可讓您指定變更PDF/A轉換程式的選項。

* *合規性* ：指定輸出PDF/A必須符合的PDF/A標準。
* *結果層級* ：指定用於PDF/A轉換記錄的記錄層級。
* *簽章* ：指定轉換期間必須如何處理輸入檔案中的簽章。
* *色域* ：指定要用於輸出PDF/A檔案的預先定義色域。
* *驗證* 轉換：指定轉換後的PDF/A檔案在轉換後是否應驗證PDF/A相容性。
* *工作記錄層級* ：指定用於處理記錄的記錄層級。

* *中繼資料延伸結構描述* ：指定PDF檔案中繼資料中用於XMP屬性的中繼資料延伸結構描述的路徑。

#### 輸出檔案 {#output-documents-1}

「輸出檔案」標籤可讓您指定輸出檔案的目的地

* *PDFA檔案*：指定轉換PDF/A檔案的儲存位置。 它可以覆寫裝載檔案或儲存在裝載資料夾下。
* *轉換記錄*：指定儲存轉換記錄的位置。 它可以覆寫裝載檔案，或儲存在裝載資料夾下。

## Forms {#forms}

呈現PDF表單工作流程是周圍的包裝函式 `renderPDFForm` Forms服務API可使用XDP範本和資料xml建立PDF表單。

### 呈現PDF表單工作流程 {#render-pdf-form-workflow}

1. 將「呈現PDF表單」工作流程步驟拖曳至Sidekick中「Forms Workflow」標籤下方。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話方塊中，設定輸入檔案、輸出檔案和其他引數，然後按一下 **[!UICONTROL 確定]**.

#### 輸入檔案 {#input-documents-2}

* *範本檔案*：指定XDP範本的位置。 它是必填欄位。

* *資料檔案*：指定需要與範本合併的資料xml的位置。

#### 輸出檔案 {#output-documents-2}

* *輸出檔案*： — 指定所產生PDF表單的名稱。

#### 其他引數 {#additional-parameters}

* *內容根目錄*：指定存放庫中儲存輸入XDP範本中使用的片段或影像的資料夾路徑。
* *提交Url*：指定所產生PDF表單的預設提交URL。
* *地區設定*：指定所產生PDF表單的預設地區設定。
* *Acrobat版本*：指定所產生PDF表單的目標Acrobat版本。
* *標籤PDF*：指定是否允許存取產生的PDF。
* *XCI檔案*：指定XCI檔案的路徑。

## 输出 {#output}

「產生非互動式PDF」工作流程是周圍的包裝函式 `generatePDFOutput` 輸出服務API。 它用於從XDP範本和資料xml產生非互動式PDF檔案。

### 產生非互動式PDF輸出工作流程   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. 將「產生非互動式PDF輸出」工作流程拖曳至Sidekick中「Forms Workflow」標籤下方。
1. 連按兩下新增的工作流程步驟以編輯元件。
1. 在「編輯元件」對話方塊中，設定輸入檔案、輸出檔案和其他引數，然後按一下 **[!UICONTROL 確定]**.

#### 輸入檔案 {#input-documents-3}

* *範本檔案*：指定XDP範本的位置。 它是必填欄位。

* *資料檔案*：指定需要與範本合併的資料xml的位置。

#### 輸出檔案 {#output-document}

*輸出檔案*：指定所產生PDF表單的名稱。

#### 其他引數 {#additional-parameters-1}

* *內容根目錄*：指定存放庫中儲存輸入XDP範本中使用的片段或影像的資料夾路徑。
* *地區設定*：指定所產生PDF表單的預設地區設定。
* *Acrobat版本*：指定所產生PDF表單的目標Acrobat版本。
* 線性PDF：指定是否要最佳化產生的PDF以供網頁檢視。
* *標籤PDF*：指定是否允許存取產生的PDF。
* *XCI檔案*：指定XCI檔案的路徑。
