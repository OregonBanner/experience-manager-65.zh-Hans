---
title: 設定提交動作
seo-title: Configuring the Submit action
description: Forms可讓您設定提交動作，以定義提交後處理最適化表單的方式。 您可以使用內建提交動作，或從頭開始編寫自己的提交動作。
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: Adaptive Forms
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 0%

---

# 設定提交動作{#configuring-the-submit-action}

## 提交動作簡介 {#introduction-to-submit-actions}

當使用者按一下最適化表單上的提交按鈕時，就會觸發提交動作。 您可以在最適化表單上設定提交動作。 調適型表單提供一些現成的提交動作。 您可以複製並擴充預設提交動作，以建立您自己的提交動作。 不過，您可以根據自己的需求，編寫並註冊自己的提交動作，以處理提交表單中的資料。 提交動作可使用 [同步或非同步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md).

您可以在以下位置設定提交動作： **提交** 側邊欄中適用性表單容器屬性的區段。

![設定提交動作](assets/thank-you-setting.png)

設定提交動作

最適化表單可用的預設提交動作如下：

* 提交至REST端點
* 发送电子邮件
* 透過電子郵件傳送PDF
* 叫用Forms Workflow
* 使用表单数据模型提交
* Forms入口網站提交動作
* 叫用AEM工作流程

>[!NOTE]
>
>透過電子郵件傳送PDF提交動作僅適用於使用XFA範本作為表單模型的最適化表單。

>[!NOTE]
>
>確保 [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM資料夾
>存在. 需要目錄來暫時儲存附件。 如果目錄不存在，請建立目錄。

>[!CAUTION]
>
>若您 [預填](../../forms/using/prepopulate-adaptive-form-fields.md) 表單範本、表單資料模型或結構描述型最適化表單，針對不含資料的結構描述（XML結構描述、JSON結構描述、表單範本或表單資料模型）提出XML或JSON資料投訴 &lt;afdata>， &lt;afbounddata>、和 &lt;/afunbounddata> 標籤，則為無限制欄位的資料(無限制欄位為不適用的最適化表單欄位 [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) 屬性)。

您可以撰寫最適化表單的自訂提交動作，以符合您的使用案例。 如需詳細資訊，請參閱 [為最適化表單編寫自訂提交動作](../../forms/using/custom-submit-action-form.md).

## 提交至REST端點 {#submit-to-rest-endpoint}

此 **提交至REST端點** 提交選項會將表單中填入的資料傳遞至已設定的確認頁面，作為HTTPGET請求的一部分。 您可以新增要請求的欄位名稱。 請求的格式為：

`{fieldName}={request parameter name}`

如下圖所示， `param1` 和 `param2` 會以引數形式傳遞，其值複製自 **文字方塊** 和 **數值方塊** 下一個動作的欄位。

您也可以 **啟用POST請求** 並提供一個URL以張貼請求。 若要將資料提交至託管表單的Experience Manager伺服器，請使用與Experience Manager伺服器根路徑對應的相對路徑。 例如，/content/forms/af/SampleForm.html。 若要將資料提交至任何其他伺服器，請使用絕對路徑。

![設定Rest端點提交動作](assets/action-config.png)

設定Rest端點提交動作

>[!NOTE]
若要在REST URL中將欄位作為引數傳遞，所有欄位都必須有不同的元素名稱，即使欄位位於不同的面板上也是如此。

### 將提交的資料發佈到資源或外部Rest端點  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用 **提交至REST端點** 將已提交的資料發佈至rest URL的動作。 URL可以是內部（呈現表單的伺服器）或外部伺服器。

若要將資料發佈到內部伺服器，請提供資源的路徑。 資料會張貼在資源的路徑中。 例如，/content/restEndPoint。 對於此類貼文請求，會使用提交請求的驗證資訊。

若要將資料發佈至外部伺服器，請提供URL。 URL的格式為https://host:port/path_to_rest_end_point。 請確定您設定匿名處理POST請求的路徑。

![以「感謝您」頁面引數傳遞的欄位值對應](assets/post-enabled-actionconfig.png)

在上述範例中，使用者輸入資訊於 `textbox` 是使用引數擷取 `param1`. 張貼使用擷取之資料的語法 `param1` 為：

`String data=request.getParameter("param1");`

同樣地，您用於公佈XML資料和附件的引數為 `dataXml` 和 `attachments`.

例如，您可以在指令碼中使用這兩個引數，將資料剖析至其餘端點。 您使用下列語法來儲存及剖析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此範例中， `data` 儲存XML資料，以及 `att` 儲存附件資料。

## 发送电子邮件 {#send-email}

此 **傳送電子郵件** 提交動作會在成功提交表單時傳送電子郵件給一或多位收件者。 產生的電子郵件可以包含預先定義的格式表單資料。

>[!NOTE]
所有表單欄位都必須有不同的元素名稱（即使它們放在不同的面板上），才能在電子郵件中包含表單資料。

## 透過電子郵件傳送PDF {#send-pdf-via-email}

此 **透過電子郵件傳送PDF** 提交動作會在成功提交表單時，傳送內含表單資料PDF的電子郵件給一或多個收件者。

>[!NOTE]
此提交動作適用於具有記錄檔案範本的XFA型最適化表單和XSD型最適化表單。

## 叫用Forms Workflow {#invoke-a-forms-workflow}

此 **提交至Forms Workflow** 提交選項會將資料xml和檔案附件（若有）傳送至現有的AdobeLiveCycle或JEE程式上的AEM Forms。

如需有關如何設定「提交至Forms Workflow」提交動作的資訊，請參閱 [使用表單工作流程提交和處理您的表單資料](../../forms/using/submit-form-data-livecycle-process.md).

## 使用表单数据模型提交 {#submit-using-form-data-model}

此 **使用表單資料模型提交** 提交動作會將表單資料模型中指定資料模型物件的已提交最適化表單資料寫入其資料來源。 在設定提交動作時，您可以選擇要將其提交資料寫入其資料來源的資料模型物件。

此外，您可以使用表單資料模型和記錄檔案(DoR)將表單附件提交至資料來源。

如需表單資料模型的相關資訊，請參閱 [AEM Forms資料整合](../../forms/using/data-integration.md).

## Forms入口網站提交動作 {#forms-portal-submit-action}

此 **Forms入口網站提交動作** 選項可透過AEM Forms入口網站提供表單資料。

如需Forms入口網站與提交動作的詳細資訊，請參閱 [草稿和提交元件](../../forms/using/draft-submission-component.md).

## 叫用AEM工作流程 {#invoke-an-aem-workflow}

此 **[!UICONTROL 叫用AEM工作流程]** 提交動作會將最適化表單與以下專案建立關聯： [AEM工作流程](/help/sites-developing/workflows-models.md). 提交表單時，相關工作流程會在作者執行個體上自動啟動。 您可以將資料檔案、附件和記錄檔案儲存至相對資料夾，或工作流程裝載下的資料夾，或儲存至變數。 如果工作流程標籤為外部資料儲存，則變數選項可用，而不是裝載選項。 您可以從工作流程模型可用的變數清單中選取。 如果工作流程在稍後階段而非建立工作流程時標籤為外部資料儲存，則請確保必要的變數設定已準備就緒。

使用之前 **叫用AEM工作流程** 提交動作， [設定Experience ManagerDS設定](../../forms/using/configuring-the-processing-server-url-.md). 如需建立AEM Workflow的相關資訊，請參閱 [OSGi上以表單為中心的工作流程](../../forms/using/aem-forms-workflow.md).

提交動作會將下列專案置於工作流程的裝載位置。 但請注意，如果工作流程模型標示為用於外部資料儲存，則只會顯示「變數」選項，而不會顯示「裝載」選項。

* **資料檔案**：此變數包含提交至最適化表單的資料。 您可以使用 **[!UICONTROL 資料檔案路徑]** 選項來指定檔案的名稱及相對於承載的檔案路徑。 例如， `/addresschange/data.xml` path會建立名為的資料夾 `addresschange` 並將其相對於承載放置。 您也可僅指定 `data.xml` 只傳送已提交的資料，而不建立資料夾階層。 使用變數選項，並從工作流程模型可用的變數清單中選取變數。

>[!NOTE]
無論工作流程模型是否標示為外部資料儲存，都可以使用變數。

* **附件**：您可以使用 **[!UICONTROL 附件路徑]** 用於指定資料夾名稱以儲存已上傳至最適化表單的附件。 資料夾會相對於承載建立。 如果工作流程已標籤為外部資料儲存，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

* **記錄檔案**：它包含為最適化表單產生的記錄檔案。 您可以使用 **[!UICONTROL 記錄檔案路徑]** 選項以指定記錄檔案檔案的名稱以及相對於承載的檔案路徑。 例如， `/addresschange/DoR.pdf` path會建立名為的資料夾 `addresschange` 相對於裝載，並放置 `DoR.pdf` 相對於裝載。 您也可僅指定 `DoR.pdf` 只儲存記錄檔案，而不建立資料夾階層。 如果工作流程已標籤為外部資料儲存，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

## Adaptive Form中的伺服器端重新驗證 {#server-side-revalidation-in-adaptive-form}

在任何線上資料擷取系統中，開發人員通常會在使用者端放置一些JavaScript驗證，以強制執行一些商業規則。 但在現代瀏覽器中，一般使用者可以略過這些驗證，並使用各種技術手動提交內容，例如網頁瀏覽器DevTools主控台。 這些技巧對於最適化表單也是有效的。 表單開發人員可以建立各種驗證邏輯，但技術上來說，一般使用者可以略過這些驗證邏輯，並將無效資料提交至伺服器。 無效資料會破壞表單作者已強制執行的商業規則。

伺服器端重新驗證功能也讓您能夠執行最適化表單作者在伺服器上設計最適化表單時所提供的驗證。 它可防止表單驗證中顯示的資料提交和業務規則違規的任何可能危害。

### 要在伺服器上驗證什麼？ {#what-to-validate-on-server-br}

在伺服器上重新執行的最適化表單的所有開箱即用(OOTB)欄位驗證包括：

* 必填
* 驗證圖片子句
* 驗證運算式

### 啟用伺服器端驗證 {#enabling-server-side-validation-br}

使用 **在伺服器上重新驗證** 在側欄的「調適型表單容器」下，啟用或停用目前表單的伺服器端驗證。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果一般使用者略過這些驗證並提交表單，伺服器會再次執行驗證。 如果驗證在伺服器端失敗，則送出交易會停止。 使用者會再次看到原始表單。 擷取的資料和提交的資料會向使用者呈現為錯誤。

>[!NOTE]
伺服器端驗證會驗證表單模型。 建議建立個別的使用者端程式庫進行驗證，不要將其與其他專案(例如HTML樣式和DOM操作)混合在同一個使用者端程式庫中。

### 在驗證運算式中支援自訂函式 {#supporting-custom-functions-in-validation-expressions-br}

有時，如果有複雜的驗證規則，確切的驗證指令碼會位於自訂函式中，而作者會從欄位驗證運算式呼叫這些自訂函式。 AEM若要在執行伺服器端驗證時讓此自訂函式館為已知且可用，表單作者可在 **基本** 最適化表單容器屬性的索引標籤，如下所示。

![在驗證運算式中支援自訂函式](assets/clientlib-cat.png)

在驗證運算式中支援自訂函式

作者可以根據每個最適化表單設定customJavaScript程式庫。 在程式庫中，僅保留可重複使用的函式，這些函式依賴於jquery和underscore.js第三方程式庫。

## 提交動作的錯誤處理 {#error-handling-on-submit-action}

在Experience Manager安全性和強化准則中，請設定自訂錯誤頁面，例如404.jsp和500.jsp。 提交表單時出現404或500錯誤時，會呼叫這些處理常式。 在Publish節點上觸發這些錯誤碼時，也會呼叫處理常式。

如需詳細資訊，請參閱 [自訂錯誤處理常式顯示的頁面](/help/sites-developing/customizing-errorhandler-pages.md).
