---
title: 在使用者端轉譯Forms
seo-title: Rendering Forms at the Client
description: 最佳化PDF內容的傳送，並使用Acrobat或Adobe Reader的使用者端轉譯功能，改善Forms服務處理網路負載的能力
seo-description: Optimize the delivery of PDF content and improve the Forms service’s ability to handle network load by using the client-side rendering capability of Acrobat or Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# 在使用者端轉譯Forms {#rendering-forms-at-the-client}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 在使用者端轉譯Forms {#rendering-forms-at-the-client-inner}

您可以使用Acrobat或Adobe Reader的使用者端轉譯功能，最佳化PDF內容的傳送，並改善Forms服務處理網路負載的能力。 此程式稱為在使用者端轉譯表單。 若要在使用者端轉譯表單，使用者端裝置（通常是網頁瀏覽器）必須使用Acrobat 7.0或Adobe Reader 7.0或更新版本。

伺服器端指令碼執行導致的表單變更，不會反映在使用者端轉譯的表單中，除非root子表單包含 `restoreState` 屬性已設定為 `auto`. 如需有關此屬性的詳細資訊，請參閱 [Forms Designer。](https://www.adobe.com/go/learn_aemforms_designer_63_cn)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要在使用者端轉譯表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 設定使用者端演算執行階段選項。
1. 在使用者端轉譯表單。
1. 將表單寫入使用者端網頁瀏覽器。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API操作。 如果您使用Java API，請建立 `FormsServiceClient` 物件。 如果您使用Forms Web服務API，請建立 `FormsService` 物件。

**設定使用者端演算執行階段選項**

您必須設定使用者端轉譯執行階段選項，以在使用者端轉譯表單，方法是設定 `RenderAtClient` 執行階段選項 `true`. 這會導致表單傳送至產生表單的使用者端裝置。 若 `RenderAtClient` 是 `auto` （預設值），表單設計會決定是否在使用者端轉譯表單。 表單設計必須是具有可流動配置的表單設計。

您可以設定的選擇性執行階段選項是 `SeedPDF` 選項。 此 `SeedPDF` 選項會將PDF容器(種子PDF檔案)與表單設計和XML資料相結合。 表單設計和XML資料都會傳送到Acrobat或Adobe Reader，表單會在這裡呈現。 此 `SeedPDF` 當使用者端電腦沒有表單中使用的字型時（例如，當一般使用者未授權使用表單擁有者授權使用的字型時），可以使用選項。

您可以使用Designer建立簡單的動態PDF檔案，以作為種子PDF檔案。 若要執行此工作，必須執行下列步驟：

1. 決定是否需要在種子PDF檔案中嵌入任何字型。 種子PDF檔案將需要包含呈現的表單所需的其他字型。 將字型內嵌到種子PDF檔案中時，請確定您沒有違反任何字型授權合約。 在Designer中，您可以決定您是否可合法嵌入字型。 儲存後，如果表單中有無法嵌入的字型，Designer會顯示一則訊息，列出無法嵌入的字型。 靜態PDF檔案的Designer中未顯示此訊息。
1. 如果您是在Designer中建立種子PDF檔案，建議您至少新增包含訊息的文字欄位。 此訊息應導向至舊版Adobe Reader的使用者，告知他們需要Acrobat 7.0或更新版本，或Adobe Reader 7.0或更新版本才能檢視檔案。
1. 將種子PDF檔案儲存為動態PDF檔案，並以PDF檔案副檔名命名。

>[!NOTE]
>
>您不需要定義種子PDF執行階段選項就能在使用者端上轉譯表單。 如果您未指定種子PDF，Forms服務會建立殼層pdf，其中不會包含COS物件，但會包含內嵌實際XDP內容的PDF包裝函式。 本節中的步驟不會設定種子PDF執行階段選項。 如需COS物件的相關資訊，請參閱《Adobe PDF參考指南》。

**在使用者端轉譯表單**

若要在使用者端轉譯表單，您必須確保使用者端轉譯執行階段選項包含在要轉譯表單的應用程式邏輯中。

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務會建立您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，表單會由Acrobat 7.0或Adobe Reader 7.0或更新版本轉譯，且使用者看得見。

**另请参阅**

[使用Java API在使用者端轉譯表單](#render-a-form-at-the-client-using-the-java-api)

[使用Web服務API在使用者端轉譯表單](#render-a-form-at-the-client-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API在使用者端轉譯表單 {#render-a-form-at-the-client-using-the-java-api}

使用Forms API (Java)在使用者端轉譯表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定使用者端演算執行階段選項

   * 建立 `PDFFormRenderSpec` 物件（使用其建構函式）。
   * 設定 `RenderAtClient` 執行階段選項，方法是叫用 `PDFFormRenderSpec` 物件的 `setRenderAtClient` 方法和傳遞列舉值 `RenderAtClient.Yes`.

1. 在使用者端轉譯表單

   叫用 `FormsServiceClient` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於AEM Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 物件，儲存在使用者端轉譯表單所需的執行階段選項。
   * A `URLSpec` 包含Forms服務轉譯表單所需的URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得的內容型別 `com.adobe.idp.Document` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件的 `read` 方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[快速入門（SOAP模式）：使用Java API在使用者端轉譯表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API在使用者端轉譯表單 {#render-a-form-at-the-client-using-the-web-service-api}

使用Forms API （Web服務）在使用者端轉譯表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 設定使用者端演算執行階段選項

   * 建立 `PDFFormRenderSpec` 物件（使用其建構函式）。
   * 設定 `RenderAtClient` 執行階段選項，方法是叫用 `PDFFormRenderSpec` 物件的 `setRenderAtClient` 方法和傳遞字串值 `RenderAtClient.Yes`.

1. 在使用者端轉譯表單

   叫用 `FormsService` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞 `null`. (請參閱 [使用可流動版面預先填入Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` 物件，儲存在使用者端轉譯表單所需的執行階段選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 方法填入的物件。 此引數用於儲存轉譯的PDF表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 方法填入的物件。 （此引數會儲存表單中的頁數）。
   * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。 （此引數會儲存地區設定值）。
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

[在使用者端轉譯Forms](#rendering-forms-at-the-client)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
