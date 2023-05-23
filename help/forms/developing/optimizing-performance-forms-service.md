---
title: 最佳化Forms服務的效能
seo-title: Optimizing the Performance of theForms Service
description: 在呈現表單時設定執行階段選項，並將XDP檔案儲存在存放庫中，以最佳化Forms服務的效能。
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# 最佳化Forms服務的效能 {#optimizing-the-performance-of-theforms-service}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 最佳化Forms服務的效能 {#optimizing-the-performance-of-the-forms-service}

轉譯表單時，您可以設定執行階段選項，以最佳化Forms服務的效能。 另一個您可以執行以改善Forms服務效能的任務是將XDP檔案儲存在存放庫中。 不過，本節並未說明如何執行此工作。 (請參閱 [使用Java使用者端程式庫叫用服務](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要在呈現表單時最佳化Forms服務的效能，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 設定效能執行階段選項。
1. 演算表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API操作。 如果您使用Java API，請建立 `FormsServiceClient` 物件。 如果您使用Forms Web服務API，請建立 `FormsService` 物件。

**設定效能執行階段選項**

您可以設定下列效能執行階段選項，以改善Forms服務的效能：

* **表單快取**：您可以快取在伺服器快取中呈現為PDF的表單。 每個表單在首次產生後都會進行快取。 在後續轉譯時，如果快取表單比表單設計的時間戳記新，則會從快取中擷取表單。 透過快取表單，您可以改善Forms服務的效能，因為它不需要從存放庫擷取表單設計。
* 表單參考線（已棄用）的轉譯時間可能比其他轉換型別長。 建議您快取表單參考線（已棄用）以提高效能。
* **獨立選項**：如果您不需要使用Forms服務來執行伺服器端計算，您可以將「獨立」選項設為 `true`，這會導致表單轉譯時沒有狀態資訊。 如果您想要將互動式表單轉譯給一般使用者，然後這些使用者在表單中輸入資訊，並將表單送回Forms服務，則需要狀態資訊。 Forms服務接著會執行計算操作，並將表單轉譯回使用者，結果會顯示在表單中。 如果將沒有狀態資訊的表單提交回Forms服務，則只有XML資料可用，並且不會執行伺服器端計算。
* **線性PDF**：線性PDF檔案經過整理，可在網路環境中實現有效的增量存取。 PDF檔案在所有方面都是有效的PDF，並與所有現有檢視器和其他PDF應用程式相容。 也就是說，線性PDF可在下載時檢視。
* 此選項無法改善在使用者端上呈現PDF表單時的效能。
* **GuideRSL選項**：啟用使用執行階段共用程式庫產生表單指南（已棄用）。 這表示第一個要求會下載較小的SWF檔案，加上儲存在瀏覽器快取中的較大共用程式庫。 如需詳細資訊，請參閱Flex檔案中的RSL 。
* 您也可以在使用者端上呈現表單，以改善Forms服務的效能。 (請參閱 [在使用者端轉譯Forms](/help/forms/developing/rendering-forms-client.md).)

**演算表單**

若要在設定效能選項後轉譯表單，您可以使用與轉譯沒有效能選項的表單相同的應用程式邏輯。

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯表單後，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，使用者可看見表單。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將Forms呈現為HTML](/help/forms/developing/rendering-forms-html.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API最佳化效能 {#optimize-the-performance-using-the-java-api}

使用Forms API (Java)呈現具有最佳化效能的表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定效能執行階段選項

   * 建立 `PDFFormRenderSpec` 物件（使用其建構函式）。
   * 透過叫用 `PDFFormRenderSpec` 物件的 `setCacheEnabled` 方法與傳遞 `true`.
   * 透過叫用 `PDFFormRenderSpec` 物件的 `setLinearizedPDF` 方法與傳遞 `true.`

1. 演算表單

   叫用 `FormsServiceClient` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 物件，用來儲存執行階段選項以改善效能。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流傳送至使用者端web瀏覽器的物件。
   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件的 `read`方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[快速入門（SOAP模式）：使用Java API最佳化效能](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API最佳化效能 {#optimize-the-performance-using-the-web-service-api}

使用Forms API （Web服務）呈現具有最佳化效能的表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 設定效能執行階段選項

   * 建立 `PDFFormRenderSpec` 物件（使用其建構函式）。
   * 透過叫用 `PDFFormRenderSpec` 物件的 `setCacheEnabled` 方法和傳遞true。
   * 透過叫用 `PDFFormRenderSpec` 物件的 `setStandAlone` 方法和傳遞true。
   * 透過叫用 `PDFFormRenderSpec` 物件的 `setLinearizedPDF` 方法和傳遞true。

1. 演算表單

   叫用 `FormsService` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * A `BLOB` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞 `null`.
   * A `PDFFormRenderSpecc` 儲存執行階段選項的物件。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 方法填入的物件。 這可用來儲存轉譯的PDF表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 方法填入的物件。 （此引數會儲存表單中的頁數）。
   * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。 （此引數會儲存地區設定值）。
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 將包含此作業結果的物件。

   此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 以表單資料流傳遞作為最後一個引數值的物件，必須寫入使用者端Web瀏覽器。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件的 `value` 資料成員。
   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流傳送至使用者端web瀏覽器的物件。
   * 建立 `BLOB` 包含表單資料的物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
   * 建立位元組陣列，並透過叫用 `BLOB` 物件的 `getBinaryData` 方法。 此任務指派 `FormsResult` 物件至位元組陣列。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
