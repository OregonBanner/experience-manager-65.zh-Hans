---
title: 依值呈現Forms
seo-title: Rendering Forms By Value
description: 使用Forms API (Java)透過Java API和Web服務API依值轉譯表單。
seo-description: Use the Forms API (Java) to render a form by value using the Java API and Web Service API.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 0%

---

# 依值呈現Forms {#rendering-forms-by-value}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

通常，在Designer中建立的表單設計會參考Forms服務來傳遞。 表單設計可能較大，因此參考傳遞它們會更有效率，以避免必須依值封送表單設計位元組。 Forms服務也可以快取表單設計，以便在快取時不需要持續讀取表單設計。

如果表單設計包含UUID屬性，則會快取該屬性。 UUID值對於所有表單設計都是唯一的，且可用來唯一識別表單。 依值呈現表單時，應僅在重複使用表單時快取表單。 不過，如果表單未重複使用且必須是唯一的，您可以避免使用使用AEM Forms API設定的快取選項來快取表單。

Forms服務也可以解析表單設計內連結內容的位置。 例如，從表單設計內參照的連結影像是相對URL。 連結的內容一律假定為相對於表單設計位置。 因此，解析連結內容時，只需將相對路徑套用至絕對表單設計位置來決定其位置。

您可以按值傳遞表單設計，而不是以參考傳遞表單設計。 在動態建立表單設計時，即當使用者端應用程式在執行階段產生建立表單設計的XML時，按值傳遞表單設計會很有效率。 在此情況下，表單設計不會儲存在實體存放庫中，因為它儲存在記憶體中。 在執行階段動態建立表單設計並按值傳遞時，您可以快取表單並改善Forms服務的效能。

**依值傳遞表單的限制**

當表單設計透過值傳遞時，以下限制適用：

* 表單設計內不能有相對連結的內容。 所有影像和片段都必須嵌入表單設計內，或絕對參照。
* 轉譯表單後無法執行伺服器端計算。 如果將表單提交回Forms服務，則會擷取並傳回資料，而不會進行任何伺服器端計算。
* 由於HTML只能在執行階段使用連結的影像，因此無法產生包含內嵌影像的HTML。 這是因為Forms服務可透過從參照的表單設計擷取影像，支援包含HTML的內嵌影像。 由於以值傳遞的表單設計沒有參考位置，因此在顯示HTML頁面時無法擷取內嵌影像。 因此，影像參照必須是絕對路徑，才能以HTML呈現。

>[!NOTE]
>
>雖然您可以依值呈現不同型別的表單(例如，HTML表單或包含使用許可權的表單)，本節將討論呈現互動式PDF forms。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步驟摘要 {#summary-of-steps}

若要依值呈現表單，請執行下列步驟：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 參考表單設計。
1. 依值演算表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立資料整合服務使用者端，才能以程式設計方式將資料從使用者端API匯入PDF。 建立服務使用者端時，您可以定義呼叫服務所需的連線設定。

**參考表單設計**

依值呈現表單時，您必須建立 `com.adobe.idp.Document` 包含要呈現之表單設計的物件。 您可以參照現有的XDP檔案，也可以在執行階段動態建立表單設計並填入 `com.adobe.idp.Document` 使用該資料。

>[!NOTE]
>
>此區段和對應的快速入門會參考現有的XDP檔案。

**依值演算表單**

若要依值演算表單，請傳遞 `com.adobe.idp.Document` 包含表單設計到演算方法的例項 `inDataDoc` 引數(可以是任何 `FormsServiceClient` 物件的演算方法，例如 `renderPDFForm`， `(Deprecated) renderHTMLForm`、等等)。 此引數值通常保留給與表單合併的資料。 同樣地，將空字串值傳遞至 `formQuery` 引數。 通常，此引數需要字串值，用以指定表單設計的名稱。

>[!NOTE]
>
>如果您想要在表單中顯示資料，資料必須在 `xfa:datasets` 元素。 如需XFA架構的相關資訊，請前往 [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務依值轉譯表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，使用者可看見表單。

**另请参阅**

[使用Java API依值轉譯表單](#render-a-form-by-value-using-the-java-api)

[使用Web服務API依值轉譯表單](#render-a-form-by-value-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API依值轉譯表單 {#render-a-form-by-value-using-the-java-api}

使用Forms API (Java)依值轉譯表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考表單設計

   * 建立 `java.io.FileInputStream` 物件，代表使用建構函式並傳遞字串值（指定XDP檔案的位置）來呈現的表單設計。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 依值演算表單

   叫用 `FormsServiceClient` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 空字串值。 （此引數通常需要字串值，用以指定表單設計的名稱。）
   * A `com.adobe.idp.Document` 包含表單設計的物件。 通常此引數值會保留給與表單合併的資料。
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。 此為選用引數，您可以指定 `null` 如果您不想指定執行階段選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含可寫入使用者端網頁瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得的內容型別 `com.adobe.idp.Document` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列並配置的大小 `InputStream` 物件。 叫用 `InputStream` 物件的 `available` 取得「 」大小的方法 `InputStream` 物件。
   * 透過叫用 `InputStream` 物件的 `read`方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[依值呈現Forms](/help/forms/developing/rendering-forms.md)

[快速入門（SOAP模式）：使用Java API依值轉譯](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API依值轉譯表單 {#render-a-form-by-value-using-the-web-service-api}

使用Forms API （Web服務）依值轉譯表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 參考表單設計

   * 建立 `java.io.FileInputStream` 物件（使用其建構函式）。 傳遞字串值，指定XDP檔案的位置。
   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存已使用密碼加密的PDF檔案。
   * 建立位元組陣列，儲存 `java.io.FileInputStream` 物件。 您可以取得 `java.io.FileInputStream` 物件大小(使用其 `available` 方法。
   * 叫用 `java.io.FileInputStream` 物件的 `read` 方法並傳遞位元組陣列。
   * 填入 `BLOB` 物件(透過叫用其 `setBinaryData` 方法並傳遞位元組陣列。

1. 依值演算表單

   叫用 `FormsService` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 空字串值。 （此引數通常需要字串值，用以指定表單設計的名稱。）
   * A `BLOB` 包含表單設計的物件。 通常此引數值會保留給與表單合併的資料。
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。 此為選用引數，您可以指定 `null` 如果您不想指定執行階段選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 方法填入的物件。 這可用來儲存轉譯的PDF表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 方法填入的物件。 （此引數會以表單儲存頁數。）
   * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。 （此引數會儲存地區設定值。）
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

[依值呈現Forms](#rendering-forms-by-value)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
