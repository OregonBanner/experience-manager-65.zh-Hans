---
title: 處理已提交的Forms
seo-title: Handling Submitted Forms
description: 使用Forms服務來擷取在互動式表單中輸入的提交資料。 使用者可以提交XML、PDF和URL UTF-16格式的表單資料。
seo-description: Use the Forms service to retrieve the submitted data entered in an interactive form. The user can submit the form data in XML, PDF, and URL UTF-16 formats.
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2904'
ht-degree: 0%

---

# 處理已提交的Forms {#handling-submitted-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

讓使用者填寫互動式表單的網頁式應用程式需要將資料提交回伺服器。 使用Forms服務，您可以擷取使用者在互動式表單中輸入的資料。 擷取資料後，您可以處理資料以符合業務需求。 例如，您可以將資料儲存在資料庫中、將資料傳送至其他應用程式、將資料傳送至其他服務、將資料合併至表單設計、在網頁瀏覽器中顯示資料等等。

表單資料會以XML或PDF資料（在Designer中設定的選項）提交至Forms服務。 以XML形式提交的表單可讓您擷取個別欄位資料值。 也就是說，您可以擷取使用者在表單中輸入的每個表單欄位的值。 作為PDF資料提交的表單是二進位資料，而不是XML資料。 您可以將表單儲存為PDF檔案，或將表單傳送至其他服務。 如果您想要從以XML格式提交的表單中擷取資料，然後使用表單資料來建立PDF檔案，請叫用另一個AEM Forms作業。 (請參閱 [使用已提交的XML資料建立PDF檔案](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

下圖顯示提交至名為的Java Servlet的資料 `HandleData` 從網頁瀏覽器中顯示的互動式表單。

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

下表說明圖表中的步驟。

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>使用者填寫互動式表單，然後按一下表單的「提交」按鈕。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>資料已提交至 <code>HandleData</code> Java Servlet作為XML資料。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>此 <code>HandleData</code> Java Servlet包含用來擷取資料的應用程式邏輯。</p></td>
  </tr>
 </tbody>
</table>

## 處理提交的XML資料 {#handling-submitted-xml-data}

表單資料以XML提交時，您可以擷取代表已提交資料的XML資料。 所有表單欄位都會顯示為XML結構描述中的節點。 節點值對應至使用者填入的值。 考慮貸款表單，其中表單中的每個欄位都會顯示為XML資料中的節點。 每個節點的值與使用者填入的值相對應。 假設使用者填妥以下表格所示的資料。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

下圖顯示使用Forms服務使用者端API擷取的對應XML資料。

![hs_hs_loandata](assets/hs_hs_loandata.png)

貸款表單中的欄位。 這些值可以使用Java XML類別來擷取。

>[!NOTE]
>
>必須在Designer中正確設定表單設計，才能將資料作為XML資料提交。 若要正確設定表單設計以提交XML資料，請確保表單設計上的提交按鈕已設定為提交XML資料。 如需有關設定「提交」按鈕以提交XML資料的資訊，請參閱 [AEM Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

## 處理提交的PDF資料 {#handling-submitted-pdf-data}

假設有一個叫用Forms服務的Web應用程式。 Forms服務將互動式PDF表單轉譯給使用者端Web瀏覽器後，使用者會填入表單並將其提交回PDF資料。 Forms服務收到PDF資料時，可以將PDF資料傳送至其他服務或儲存為PDF檔案。 下圖顯示應用程式的邏輯流程。

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

下表說明此圖表中的步驟。

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>網頁內含的連結會存取叫用Forms服務的Java Servlet。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms服務會將互動式PDF表單轉譯給使用者端網頁瀏覽器。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者填寫互動式表單並按一下提交按鈕。 表單會以PDF資料的形式提交回Forms服務。 此選項是在Designer中設定。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms服務會將PDF資料儲存為PDF檔案。 </p></td>
  </tr>
 </tbody>
</table>

## 處理提交的URL UTF-16資料 {#handling-submitted-url-utf-16-data}

如果表單資料以URL UTF-16資料提交，使用者端電腦會需要Adobe Reader或Acrobat 8.1或更新版本。 此外，如果表單設計包含具有URL編碼資料(HTTP Post)的提交按鈕，且資料編碼選項為UTF-16，則表單設計必須在文字編輯器（例如記事本）中修改。 您可以將編碼選項設定為 `UTF-16LE` 或 `UTF-16BE` 針對「提交」按鈕。 Designer不提供此功能。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步驟摘要 {#summary-of-steps}

若要處理提交的表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 擷取表單資料。
1. 決定表單提交是否包含檔案附件。
1. 處理提交的資料。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API操作。 如果您使用Java API，請建立 `FormsServiceClient` 物件。 如果您使用Forms Web服務API，請建立 `FormsService` 物件。

**擷取表單資料**

若要擷取提交的表單資料，您需叫用 `FormsServiceClient` 物件的 `processFormSubmission` 方法。 叫用此方法時，您必須指定已提交表單的內容型別。 從使用者端Web瀏覽器將資料提交到Forms服務時，可以以XML或PDF資料形式提交資料。 若要擷取輸入表單欄位中的資料，資料可以提交為XML資料。

您也可以設定下列執行階段選項，從以PDF資料提交的表單中擷取表單欄位：

* 將下列值傳遞至 `processFormSubmission` 作為內容型別引數的方法： `CONTENT_TYPE=application/pdf`.
* 設定 `RenderOptionsSpec` 物件的 `PDFToXDP` 值至 `true`
* 設定 `RenderOptionsSpec` 物件的 `ExportDataFormat` 值至 `XMLData`

當您叫用時，請指定已提交表單的內容型別 `processFormSubmission` 方法。 下列清單會指定適用的內容型別值：

* **text/xml**：代表在PDF表單以XML形式提交表單資料時使用的內容型別。
* **application/x-www-form-urlencoded**：代表在HTML表單將資料提交為XML時所使用的內容型別。
* **application/pdf**：代表PDF表單將資料提交為PDF時使用的內容型別。

>[!NOTE]
>
>您會注意到，有三個與處理已提交的Forms區段相關的對應快速入門。 使用Java API快速入門處理以PDF形式提交的PDF forms會示範如何處理提交的PDF資料。 此快速入門中指定的內容型別為 `application/pdf`. 使用Java API快速入門處理以XML形式提交的PDF forms示範如何處理從PDF表單提交的提交XML資料。 此快速入門中指定的內容型別為 `text/xml`. 同樣地，使用Java API快速入門處理以XML格式提交的HTML表單會示範如何處理從HTML表單提交的提交XML資料。 此快速入門中指定的內容型別為application/x-www-form-urlencoded。

您可以擷取發佈至Forms服務的表單資料，並判斷其處理狀態。 也就是說，將資料提交至Forms服務時，不一定代表Forms服務已完成資料處理，資料已準備好處理。 例如，資料可提交至Forms服務，以便執行計算。 計算完成後，表單會呈現回使用者並顯示計算結果。 在處理提交的資料之前，建議您先判斷Forms服務是否已完成處理資料。

Forms服務會傳回下列值，指出是否已完成資料處理：

* **0 （提交）：** 已提交的資料已準備好進行處理。
* **1 （計算）：** Forms服務已對資料執行計算操作，且結果必須轉譯回使用者。
* **2 （驗證）：** Forms服務已驗證表單資料，且必須將結果轉譯回使用者。
* **3 （下一個）：** 目前頁面已變更，結果必須寫入使用者端應用程式。
* **4 (上一個**)：目前頁面已變更，且結果必須寫入使用者端應用程式。

>[!NOTE]
>
>計算與驗證必須呈現回使用者。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**決定表單提交是否包含檔案附件**

提交至Forms服務的Forms可包含檔案附件。 例如，使用Acrobat的內建附件窗格，使用者可以選擇要與表單一起提交的檔案附件。 此外，使用者也可以使用以HTML檔案呈現的HTML工具列來選取檔案附件。

確定表單是否包含檔案附件後，即可處理資料。 例如，您可以將檔案附件儲存至本機檔案系統。

>[!NOTE]
>
>必須以PDF資料提交表單，才能擷取檔案附件。 如果表單以XML資料形式提交，則不會提交檔案附件。

**處理提交的資料**

根據提交資料的內容型別，您可以從提交的XML資料中擷取個別表單欄位值，或將提交的PDF資料儲存為PDF檔案（或將其傳送至其他服務）。 若要擷取個別表單欄位，請將提交的XML資料轉換為XML資料來源，然後使用擷取XML資料來源值 `org.w3c.dom` 類別。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API處理提交的表單 {#handle-submitted-forms-using-the-java-api}

使用Forms API (Java)處理提交的表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取表單資料

   * 若要擷取發佈至Java Servlet的表單資料，請建立 `com.adobe.idp.Document` 物件，方法是使用其建構函式並叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getInputStream` 建構函式中的方法。
   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。 透過叫用 `RenderOptionsSpec` 物件的 `setLocale` 方法並傳遞字串值，以指定地區設定值。

   >[!NOTE]
   >
   >您可以透過叫用，指示Forms服務從提交的PDF內容建立XDP或XML資料 `RenderOptionsSpec` 物件的 `setPDF2XDP` 方法與傳遞 `true` 以及呼叫 `setXMLData` 和傳遞 `true`. 然後您可以叫用 `FormsResult` 物件的 `getOutputXML` 擷取與XDP/XML資料相對應的XML資料的方法。 (此 `FormsResult` 物件由傳回 `processFormSubmission` 方法，這會在下一個子步驟中說明。)

   * 叫用 `FormsServiceClient` 物件的 `processFormSubmission` 方法並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含表單資料的物件。
      * 字串值，指定包含所有相關HTTP標頭的環境變數。 指定要處理的內容型別。 若要處理XML資料，請為此引數指定下列字串值： `CONTENT_TYPE=text/xml`. 若要處理PDF資料，請為此引數指定下列字串值： `CONTENT_TYPE=application/pdf`.
      * 字串值，指定 `HTTP_USER_AGENT` 標頭值，例如。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 此引數值為選用。
      * A `RenderOptionsSpec` 儲存執行階段選項的物件。

      此 `processFormSubmission` 方法傳回 `FormsResult` 包含表單提交結果的物件。

   * 判斷Forms服務是否已透過叫用 `FormsResult` 物件的 `getAction` 方法。 如果此方法傳回值 `0`，資料已準備好處理。



1. 決定表單提交是否包含檔案附件

   * 叫用 `FormsResult` 物件的 `getAttachments` 方法。 此方法會傳回 `java.util.List` 包含透過表單提交的檔案的物件。
   * 循環瀏覽 `java.util.List` 物件，以判斷是否有檔案附件。 如果有檔案附件，則每個元素都是 `com.adobe.idp.Document` 執行個體。 您可以透過叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 方法和傳遞 `java.io.File` 物件。

   >[!NOTE]
   >
   >此步驟僅適用於表單以PDF提交時。

1. 處理提交的資料

   * 如果資料內容型別為 `application/vnd.adobe.xdp+xml` 或 `text/xml`，建立應用程式邏輯以擷取XML資料值。

      * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
      * 建立 `java.io.InputStream` 物件(透過叫用 `java.io.DataInputStream` 建構函式並傳遞 `com.adobe.idp.Document` 物件。
      * 建立 `org.w3c.dom.DocumentBuilderFactory` 物件（透過呼叫靜態） `org.w3c.dom.DocumentBuilderFactory` 物件的 `newInstance` 方法。
      * 建立 `org.w3c.dom.DocumentBuilder` 物件(透過叫用 `org.w3c.dom.DocumentBuilderFactory` 物件的 `newDocumentBuilder` 方法。
      * 建立 `org.w3c.dom.Document` 物件(透過叫用 `org.w3c.dom.DocumentBuilder` 物件的 `parse` 方法和傳遞 `java.io.InputStream` 物件。
      * 擷取XML檔案中每個節點的值。 完成此工作的一種方式是建立接受兩個引數的自訂方法： `org.w3c.dom.Document` 物件和您要擷取其值的節點名稱。 此方法會傳回代表節點值的字串值。 在此程式之後的程式碼範例中，會呼叫此自訂方法 `getNodeText`. 此時會顯示此方法的內文。
   * 如果資料內容型別為 `application/pdf`，建立應用程式邏輯，將提交的PDF資料儲存為PDF檔案。

      * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
      * 建立 `java.io.File` 物件（使用其公用建構函式）。 請務必指定PDF作為副檔名。
      * 叫用「 」填入PDF檔案 `com.adobe.idp.Document` 物件的 `copyToFile` 方法和傳遞 `java.io.File` 物件。


**另请参阅**

[快速入門（SOAP模式）：使用Java API處理以XML提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[快速入門（SOAP模式）：使用Java API處理以XML格式提交的HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[快速入門（SOAP模式）：使用Java API處理作為PDF提交的PDF forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API處理提交的PDF資料 {#handle-submitted-pdf-data-using-the-web-service-api}

使用Forms API （Web服務）處理提交的表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 擷取表單資料

   * 若要擷取發佈至Java Servlet的表單資料，請建立 `BLOB` 物件（使用其建構函式）。
   * 建立 `java.io.InputStream` 物件(透過叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getInputStream` 方法。
   * 建立 `java.io.ByteArrayOutputStream` 物件，使用它的建構函式傳遞 `java.io.InputStream` 物件。
   * 複製以下專案的內容： `java.io.InputStream` 物件放入 `java.io.ByteArrayOutputStream` 物件。
   * 透過叫用建立位元組陣列 `java.io.ByteArrayOutputStream` 物件的 `toByteArray` 方法。
   * 填入 `BLOB` 物件(透過叫用其 `setBinaryData` 方法，並將位元組陣列作為引數傳遞。
   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。 透過叫用 `RenderOptionsSpec` 物件的 `setLocale` 方法並傳遞字串值，以指定地區設定值。
   * 叫用 `FormsService` 物件的 `processFormSubmission` 方法並傳遞下列值：

      * 此 `BLOB` 包含表單資料的物件。
      * 字串值，指定包含所有相關HTTP標頭的環境變數。 指定要處理的內容型別。 若要處理XML資料，請為此引數指定下列字串值： `CONTENT_TYPE=text/xml`. 若要處理PDF資料，請為此引數指定下列字串值： `CONTENT_TYPE=application/pdf`.
      * 字串值，指定 `HTTP_USER_AGENT` 標頭值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 儲存執行階段選項的物件。
      * 空白 `BLOBHolder` 方法填入的物件。
      * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。
      * 空白 `BLOBHolder` 方法填入的物件。
      * 空白 `BLOBHolder` 方法填入的物件。
      * 空白 `javax.xml.rpc.holders.ShortHolder` 方法填入的物件。
      * 空白 `MyArrayOf_xsd_anyTypeHolder` 方法填入的物件。 此引數用於儲存與表單一起提交的檔案附件。
      * 空白 `FormsResultHolder` 使用已提交表單之方法填入的物件。

      此 `processFormSubmission` 方法填入 `FormsResultHolder` 引數以及表單提交的結果。

   * 判斷Forms服務是否已透過叫用 `FormsResult` 物件的 `getAction` 方法。 如果此方法傳回值 `0`，表單資料已準備好處理。 您可以取得 `FormsResult` 物件，方法是取得 `FormsResultHolder` 物件的 `value` 資料成員。


1. 決定表單提交是否包含檔案附件

   取得 `MyArrayOf_xsd_anyTypeHolder` 物件的 `value` 資料成員( `MyArrayOf_xsd_anyTypeHolder` 物件已傳遞至 `processFormSubmission` 方法)。 此資料成員傳回的陣列 `Objects`. 內的每個元素 `Object` 陣列是 `Object`與表單一起提交的檔案相對應。 您可以取得陣列中的每個元素，並將其轉型為 `BLOB` 物件。

1. 處理提交的資料

   * 如果資料內容型別為 `application/vnd.adobe.xdp+xml` 或 `text/xml`，建立應用程式邏輯以擷取XML資料值。

      * 建立 `BLOB` 物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
      * 透過叫用建立位元組陣列 `BLOB` 物件的 `getBinaryData` 方法。
      * 建立 `java.io.InputStream` 物件(透過叫用 `java.io.ByteArrayInputStream` 建構函式並傳遞位元組陣列。
      * 建立 `org.w3c.dom.DocumentBuilderFactory` 物件（透過呼叫靜態） `org.w3c.dom.DocumentBuilderFactory` 物件的 `newInstance` 方法。
      * 建立 `org.w3c.dom.DocumentBuilder` 物件(透過叫用 `org.w3c.dom.DocumentBuilderFactory` 物件的 `newDocumentBuilder` 方法。
      * 建立 `org.w3c.dom.Document` 物件(透過叫用 `org.w3c.dom.DocumentBuilder` 物件的 `parse` 方法和傳遞 `java.io.InputStream` 物件。
      * 擷取XML檔案中每個節點的值。 完成此工作的一種方式是建立接受兩個引數的自訂方法： `org.w3c.dom.Document` 物件和您要擷取其值的節點名稱。 此方法會傳回代表節點值的字串值。 在此程式之後的程式碼範例中，會呼叫此自訂方法 `getNodeText`. 此時會顯示此方法的內文。
   * 如果資料內容型別為 `application/pdf`，建立應用程式邏輯，將提交的PDF資料儲存為PDF檔案。

      * 建立 `BLOB` 物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
      * 透過叫用建立位元組陣列 `BLOB` 物件的 `getBinaryData` 方法。
      * 建立 `java.io.File` 物件（使用其公用建構函式）。 請務必指定PDF作為副檔名。
      * 建立 `java.io.FileOutputStream` 物件，使用它的建構函式並傳遞 `java.io.File` 物件。
      * 叫用「 」填入PDF檔案 `java.io.FileOutputStream` 物件的 `write` 方法並傳遞位元組陣列。


**另请参阅**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
