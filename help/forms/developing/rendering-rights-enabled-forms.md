---
title: 轉譯啟用許可權的Forms
seo-title: Rendering Rights-Enabled Forms
description: 使用Forms服務來轉譯已套用使用許可權的表單。 您可以使用Java API和Web服務API來轉譯啟用許可權的表單。
seo-description: Use the Forms service to render forms that have usage rights applied to them. You can render rights-enabled forms using the Java API and Web Service API.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---

# 轉譯啟用許可權的Forms {#rendering-rights-enabled-forms}

Forms服務可轉譯具有套用使用許可權的表單。 使用許可權與Acrobat中預設提供但Adobe Reader中預設不提供的功能相關，例如新增註解至表單或填寫表單欄位及儲存表單的功能。 已套用使用許可權的Forms稱為許可權啟用表單。 在Adobe Reader中開啟許可權啟用表單的使用者，可以執行為該表單啟用的操作。

若要將使用許可權套用至表單，Acrobat Reader DC擴充功能服務必須是AEM表單安裝的一部分。 此外，您必須具備有效的認證，才能將使用許可權套用至PDF檔案。 也就是說，您必須先正確設定Acrobat Reader DC擴充功能服務，才能轉譯啟用許可權的表單。 (請參閱 [關於Acrobat Reader DC擴充功能服務](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>若要轉譯包含使用許可權的表單，您必須使用XDP檔案作為輸入，而不是PDF檔案。 如果您使用PDF檔案作為輸入，表單仍會呈現；但是，它不會是啟用許可權的表單。

>[!NOTE]
>
>指定下列使用許可權時，您無法預先填入XML資料的表單： `enableComments`， `enableCommentsOnline`， `enableEmbeddedFiles`，或 `enableDigitalSignatures`. (請參閱 [使用可流動版面預先填入Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步驟摘要 {#summary-of-steps}

若要轉譯啟用許可權的表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 設定使用許可權執行階段選項。
1. 轉譯啟用許可權的表單。
1. 將啟用許可權的表單寫入使用者端Web瀏覽器。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API操作。

**設定使用許可權執行階段選項**

您必須設定使用許可權執行階段選項，才能轉譯啟用許可權的表單。 您也必須指定用來套用使用許可權至表單的認證別名。 指定別名值後，您即可指定套用至表單的每個使用許可權。

**轉譯啟用許可權的表單**

若要轉譯啟用許可權的表單，您使用與轉譯沒有使用許可權的表單相同的應用程式邏輯。 唯一的區別是，您必須確保使用許可權執行階段選項包含在應用程式邏輯中。

>[!NOTE]
>
>使用Forms Web服務API轉譯啟用許可權的表單時，您無法將檔案附加至表單。

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯啟用許可權的表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 將表單寫入使用者端網頁瀏覽器後，使用者即可看到表單。 檢視Adobe Reader中啟用許可權之表單的使用者可執行針對該表單啟用的操作。

**另请参阅**

[使用Java API轉譯啟用許可權的表單](#render-rights-enabled-forms-using-the-java-api)

[使用Web服務API轉譯啟用許可權的表單](#render-rights-enabled-forms-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API轉譯啟用許可權的表單 {#render-rights-enabled-forms-using-the-java-api}

使用Forms API (Java)轉譯啟用許可權的表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定使用許可權執行階段選項

   * 建立 `ReaderExtensionSpec` 物件（使用其建構函式）。
   * 透過叫用 `ReaderExtensionSpec` 物件的 `setReCredentialAlias` 方法並指定代表別名值的字串值。
   * 透過叫用屬於 `ReaderExtensionSpec` 物件。 不過，您只能在您參照的認證允許您這樣做時，設定使用許可權。 也就是說，如果認證不允許您設定使用權，則您無法設定使用權。 例如。 若要設定使用許可權，讓使用者能夠填寫表單欄位並儲存表單，請叫用 `ReaderExtensionSpec` 物件的 `setReFillIn` 方法與傳遞 `true`.

   >[!NOTE]
   >
   >不需要叫用 `ReaderExtensionSpec` 物件的 `setReCredentialPassword` 方法。 Forms服務未使用此方法。

1. 轉譯啟用許可權的表單

   叫用 `FormsServiceClient` 物件的 `renderPDFFormWithUsageRights` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。
   * A `ReaderExtensionSpec` 物件，用來儲存使用許可權執行階段選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。

   此 `renderPDFFormWithUsageRights` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得的內容型別 `com.adobe.idp.Document` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，叫用 `InputStream` 物件的 `read` 方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[快速入門（SOAP模式）：使用Java API轉譯已啟用許可權的表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API轉譯啟用許可權的表單 {#render-rights-enabled-forms-using-the-web-service-api}

使用Forms API （Web服務）演算啟用許可權的表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 設定使用許可權執行階段選項

   * 建立 `ReaderExtensionSpec` 物件（使用其建構函式）。
   * 透過叫用 `ReaderExtensionSpec` 物件的 `setReCredentialAlias` 方法並指定代表別名值的字串值。
   * 透過叫用屬於 `ReaderExtensionSpec` 物件。 不過，您只能在您參照的認證允許您這樣做時，設定使用許可權。 也就是說，如果認證不允許您設定使用權，則您無法設定使用權。 若要設定使用許可權，讓使用者能夠填寫表單欄位並儲存表單，請叫用 `ReaderExtensionSpec` 物件的 `setReFillIn` 方法與傳遞 `true`.

1. 轉譯啟用許可權的表單

   叫用 `FormsService` 物件的 `renderPDFFormWithUsageRights` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要與表單合併之資料的物件。 如果您不想將資料與表單合併，則必須傳遞 `BLOB` 以空白XML資料來源為基礎的物件。 您無法傳遞 `BLOB` 為null的物件；否則會擲回例外狀況。
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。
   * A `ReaderExtensionSpec` 物件，用來儲存使用許可權執行階段選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。

   此 `renderPDFFormWithUsageRights` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `BLOB` 包含表單資料的物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
   * 取得的內容型別 `BLOB` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立位元組陣列，並透過叫用 `BLOB` 物件的 `getBinaryData` 方法。 此任務指派 `FormsResult` 物件至位元組陣列。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[轉譯啟用許可權的Forms](#rendering-rights-enabled-forms)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
