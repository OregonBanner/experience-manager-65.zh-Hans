---
title: 根據片段轉譯Forms
seo-title: Rendering Forms Based on Fragments
description: 使用Forms服務來轉譯以使用Designer建立的片段為基礎的表單。
seo-description: Use the Forms service to render forms that are based on fragments created using Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 0%

---

# 根據片段轉譯Forms {#rendering-forms-based-on-fragments}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 根據片段轉譯Forms {#rendering-forms-based-on-fragments-inner}

Forms服務可以轉譯以您使用Designer建立的片段為基礎的表單。 A *片段* 是可重複使用的表單部分，並另存為可插入多個表單設計的個別XDP檔案。 例如，片段可以包含位址區塊或合法文字。

使用片段可簡化並加速大量表單的建立與維護。 建立新表單時，您會插入所需片段的參考，而片段會顯示在表單中。 片段參考包含指向實體XDP檔案的子表單。 如需有關根據片段建立表單設計的資訊，請參閱 [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn)

片段可以包含包在選擇子表單集中的多個子表單。 選擇子表單集根據資料連線的資料流程控制子表單的顯示。 您可以使用條件陳述式來決定集合中哪個子表單會出現在傳遞的表單中。 例如，集合中的每個子表單可以包含特定地理位置的資訊，而顯示的子表單可以根據使用者的位置來確定。

A *指令碼片段* 包含可重複使用的JavaScript函式或值，這些函式或值會與任何特定物件（例如日期剖析器或Web服務引動）分開儲存。 這些片段包含單一指令碼物件，會顯示為階層浮動視窗中變數的子項。 無法從作為其他物件屬性的指令碼（例如驗證、計算或初始化等事件指令碼）建立片段。

使用片段的優點如下：

* **內容重複使用**：您可以使用片段在多個表單設計中重複使用內容。 當您需要以多個表單使用某些相同內容時，使用片段比複製或重新建立內容更快更簡單。 使用片段也可確保表單設計中經常使用的部分在所有參考表單中都具有一致的內容和外觀。
* **全域更新**：您可以使用片段在一個檔案中僅對多個表單進行一次全域變更。 您可以變更片段中的內容、指令碼物件、資料繫結、版面或樣式，而所有參考片段的XDP表單都會反映變更。
* 例如，許多表單的共同元素可能是包含國家/地區下拉式清單物件的位址區塊。 如果您需要更新下拉式清單物件的值，則必須開啟許多表單才能進行變更。 如果您在片段中包含位址區塊，您只需要開啟一個片段檔案即可進行變更。
* 若要更新PDF表單中的片段，您必須在Designer中重新儲存表單。
* **共用表單建立**：您可以使用片段在數個資源之間共用表單的建立。 具備指令碼或Designer其他進階功能專業知識的表單開發人員可開發和共用利用指令碼和動態屬性的片段。 表單設計人員可以使用這些片段來配置表單設計，並確保表單的所有部分在多人設計的多個表單中都具有一致的外觀和功能。

### 組裝使用片段組裝的表單設計 {#assembling-a-form-design-assembled-using-fragments}

您可以組合表單設計，以根據多個片段傳遞至Forms服務。 若要組裝多個片段，請使用Assembler服務。 若要檢視使用Assemble服務建立其他Forms服務（Output服務）使用的表單設計的範例，請參閱 [使用片段建立PDF檔案](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). 您可以使用Forms服務執行相同的工作流程，而不使用輸出服務。

使用Assembler服務時，您傳遞的是使用片段組裝的表單設計。 已建立的表單設計未參考其他片段。 相較之下，本主題則討論將參照其他片段的表單設計傳遞至Forms服務。 不過，Assembler並未組裝表單設計。 它是在Designer中建立的。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關建立根據片段轉譯表單的網頁型應用程式的資訊，請參閱 [建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md).

### 步驟摘要 {#summary-of-steps}

若要根據片段呈現表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 指定URI值。
1. 演算表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API操作。

**指定URI值**

若要成功根據片段轉譯表單，您必須確保Forms服務能找到表單和表單設計參考的片段（XDP檔案）。 例如，假設表單名為PO.xdp，而此表單使用名為FooterUS.xdp和FooterCanada.xdp的兩個片段。 在此情況下，Forms服務必須能夠找到所有三個XDP檔案。

您可以將表單放在某個位置，將片段放在另一個位置，以組織表單及其片段，或將所有XDP檔案放在同一個位置。 就本節目的而言，假設所有XDP檔案都位於AEM Forms存放庫中。 如需有關將XDP檔案放入AEM Forms存放庫的資訊，請參閱 [寫入資源](/help/forms/developing/aem-forms-repository.md#writing-resources).

根據片段呈現表單時，您必須僅參考表單本身，而非片段。 例如，您必須參考PO.xdp，而不是FooterUS.xdp或FooterCanada.xdp。 請確定您將片段放置在Forms服務可找到它們的位置。

**演算表單**

基於片段的表單可以按與非片段表單相同的方式呈現。 也就是說，您可以將表單轉譯為PDF、HTML或表單參考線（已棄用）。 本節中的範例將以片段為基礎的表單轉譯為互動式PDF表單。 (請參閱 [呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，使用者可看見表單。

**另请参阅**

[使用Java API根據片段轉譯表單](#render-forms-based-on-fragments-using-the-java-api)

[使用Web服務API根據片段轉譯表單](#render-forms-based-on-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API根據片段轉譯表單 {#render-forms-based-on-fragments-using-the-java-api}

使用Forms API (Java)根據片段呈現表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 指定URI值

   * 建立 `URLSpec` 物件，使用其建構函式儲存URI值。
   * 叫用 `URLSpec` 物件的 `setApplicationWebRoot` 方法，並傳遞代表應用程式網頁根的字串值。
   * 叫用 `URLSpec` 物件的 `setContentRootURI` 方法並傳遞字串值，以指定內容根URI值。 確保表單設計和片段位於內容根URI中。 如果沒有，Forms服務會擲回例外狀況。 若要參照存放庫，請指定 `repository://`.
   * 叫用 `URLSpec` 物件的 `setTargetURL` 並傳遞字串值，該值會指定將表單資料發佈到的目標URL值。 如果您在表單設計中定義目標URL，您可以傳遞空字串。 您也可以指定傳送表單的URL，以執行計算。

1. 演算表單

   叫用 `FormsServiceClient` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。
   * A `URLSpec` 此物件包含Forms服務根據片段呈現表單所需的URI值。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得的內容型別 `com.adobe.idp.Document` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，叫用 `InputStream` 物件的 `read`方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[根據片段轉譯Forms](#rendering-forms-based-on-fragments)

[快速入門（SOAP模式）：使用Java API根據片段呈現表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API根據片段轉譯表單 {#render-forms-based-on-fragments-using-the-web-service-api}

使用Forms API （Web服務）根據片段呈現表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 指定URI值

   * 建立 `URLSpec` 使用其建構函式儲存URI值的物件。
   * 叫用 `URLSpec` 物件的 `setApplicationWebRoot` 方法，並傳遞代表應用程式網頁根的字串值。
   * 叫用 `URLSpec` 物件的 `setContentRootURI` 方法並傳遞字串值，以指定內容根URI值。 確認表單設計位於內容根URI中。 如果沒有，Forms服務會擲回例外狀況。 若要參照存放庫，請指定 `repository://`.
   * 叫用 `URLSpec` 物件的 `setTargetURL` 並傳遞字串值，該值會指定將表單資料發佈到的目標URL值。 如果您在表單設計中定義目標URL，您可以傳遞空字串。 您也可以指定傳送表單的URL，以執行計算。

1. 演算表單

   叫用 `FormsService` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞 `null`.
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。 請注意，如果輸入檔案是PDF檔案，則無法設定標籤的PDF選項。 如果輸入檔案是XDP檔案，則可以設定標籤的PDF選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 方法填入的物件。 此引數用於儲存演算後的表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 方法填入的物件。 此引數會儲存表單中的頁數。
   * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。 此引數將會儲存地區設定值。
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 將包含此作業結果的物件。

   此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 以表單資料流傳遞作為最後一個引數值的物件，必須寫入使用者端Web瀏覽器。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件的 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
   * 取得的內容型別 `BLOB` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立位元組陣列，並透過叫用 `BLOB` 物件的 `getBinaryData` 方法。 此任務指派 `FormsResult` 物件至位元組陣列。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[根據片段轉譯Forms](#rendering-forms-based-on-fragments)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
