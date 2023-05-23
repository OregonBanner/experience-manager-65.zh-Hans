---
title: 使用SubmittedXML資料建立PDF檔案
seo-title: Creating PDF Documents with SubmittedXML Data
description: 使用Forms服務來擷取使用者在互動式表單中輸入的表單資料。 將表單資料傳遞至另一個AEM Forms服務操作，然後使用該資料建立PDF檔案。
seo-description: Use the Forms service to retrieve the form data that the user entered into an interactive form. Pass the form data to another AEM Forms service operation and create a PDF document using the data.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 0%

---

# 使用已提交的XML資料建立PDF檔案 {#creating-pdf-documents-with-submittedxml-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 使用已提交的XML資料建立PDF檔案 {#creating-pdf-documents-with-submitted-xml-data}

讓使用者填寫互動式表單的網頁式應用程式需要將資料提交回伺服器。 使用Forms服務，您可以擷取使用者在互動式表單中輸入的表單資料。 然後，您可以將表單資料傳遞至另一個AEM Forms服務操作，並使用資料建立PDF檔案。

>[!NOTE]
>
>在閱讀本內容之前，建議您先對處理已提交表單有一定的瞭解。 處理提交的Forms中涵蓋了表單設計和提交的XML資料之間的關係等概念。

請考量下列涉及三項AEM Forms服務的工作流程：

* 使用者從網頁型應用程式將XML資料提交至Forms服務。
* Forms服務用於處理提交的表單並擷取表單欄位。 可以處理表單資料。 例如，資料可以提交至企業資料庫。
* 表單資料會傳送至Output服務以建立非互動式PDF檔案。
* 非互動式PDF檔案會儲存在Content Services中（已棄用）。

下圖提供此工作流程的視覺化呈現。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

使用者從使用者端Web瀏覽器提交表單後，非互動式PDF檔案會儲存在Content Services中（已棄用）。 下圖顯示儲存在Content Services （已棄用）中的PDF檔案。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步驟摘要 {#summary-of-steps}

若要使用提交的XML資料建立非互動式PDF檔案，並將其儲存在Content Services的PDF檔案中（已棄用），請執行下列工作：

1. 包含專案檔案。
1. 建立Forms、輸出和檔案管理物件。
1. 使用Forms服務擷取表單資料。
1. 使用Output服務建立非互動式PDF檔案。
1. 使用Document Management服務將PDF表單儲存在Content Services （已棄用）。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms、Output和Document Management物件**

以程式設計方式執行Forms服務API作業之前，請先建立Forms使用者端API物件。 同樣地，由於此工作流程會叫用Output和Document Management服務，因此請建立Output Client API物件和Document Management Client API物件。

**使用Forms服務擷取表單資料**

擷取已提交至Forms服務的表單資料。 您可以處理提交的資料，以符合您的業務需求。 例如，您可以將表單資料儲存在企業資料庫中。 不過，若要建立非互動式PDF檔案，會將表單資料傳遞至Output服務。

**使用Output服務建立非互動式PDF檔案。**

使用Output服務建立以表單設計和XML表單資料為基礎的非互動式PDF檔案。 在工作流程中，會從Forms服務擷取表單資料。

**使用檔案管理服務將PDF表單儲存在內容服務（已棄用）中**

使用檔案管理服務API將PDF檔案儲存在內容服務（已棄用）中。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API建立包含已提交XML資料的PDF檔案 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

使用Forms、Output和Document Management API (Java)建立包含已提交XML資料的PDF檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立Forms、Output和Document Management物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。
   * 建立 `DocumentManagementServiceClientImpl` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 使用Forms服務擷取表單資料

   * 叫用 `FormsServiceClient` 物件的 `processFormSubmission` 方法並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含表單資料的物件。
      * 字串值，指定環境變數，包括所有相關的HTTP標頭。 指定要處理的內容型別，方法為指定一個或多個 `CONTENT_TYPE` 環境變數。 例如，若要處理XML資料，請為此引數指定下列字串值： `CONTENT_TYPE=text/xml`.
      * 字串值，指定 `HTTP_USER_AGENT` 標頭值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 儲存執行階段選項的物件。

      此 `processFormSubmission` 方法傳回 `FormsResult` 包含表單提交結果的物件。

   * 判斷Forms服務是否已透過叫用 `FormsResult` 物件的 `getAction` 方法。 如果此方法傳回值 `0`，資料已準備好處理。
   * 透過建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。 （此物件包含可傳送至Output服務的表單資料。）
   * 建立 `java.io.InputStream` 物件(透過叫用 `java.io.DataInputStream` 建構函式並傳遞 `com.adobe.idp.Document` 物件。
   * 建立 `org.w3c.dom.DocumentBuilderFactory` 物件（透過呼叫靜態） `org.w3c.dom.DocumentBuilderFactory` 物件的 `newInstance` 方法。
   * 建立 `org.w3c.dom.DocumentBuilder` 物件(透過叫用 `org.w3c.dom.DocumentBuilderFactory` 物件的 `newDocumentBuilder` 方法。
   * 建立 `org.w3c.dom.Document` 物件(透過叫用 `org.w3c.dom.DocumentBuilder` 物件的 `parse` 方法和傳遞 `java.io.InputStream` 物件。
   * 擷取XML檔案中每個節點的值。 完成此工作的一種方式是建立接受兩個引數的自訂方法： `org.w3c.dom.Document` 物件和您要擷取其值的節點名稱。 此方法會傳回代表節點值的字串值。 在此程式之後的程式碼範例中，會呼叫此自訂方法 `getNodeText`. 此時會顯示此方法的內文。


1. 使用Output服務建立非互動式PDF檔案。

   透過叫用建立PDF檔案 `OutputClient` 物件的 `generatePDFOutput` 並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定表單設計的名稱。 確保表單設計與從Forms服務擷取的表單資料相容。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `com.adobe.idp.Document` 包含要與表單設計合併之資料之XML資料來源的物件。 確定此物件是由 `FormsResult` 物件的 `getOutputContent` 方法。
   * 此 `generatePDFOutput` 方法傳回 `OutputResult` 包含作業結果的物件。
   * 透過叫用非互動式PDF檔案來擷取 `OutputResult` 物件的 `getGeneratedDoc` 方法。 此方法會傳回 `com.adobe.idp.Document` 代表非互動式PDF檔案的例項。

1. 使用Document Management服務將PDF表單儲存在內容服務（已棄用）中

   透過叫用 `DocumentManagementServiceClientImpl` 物件的 `storeContent` 並傳遞下列值：

   * 字串值，指定新增內容的存放區。 預設存放區為 `SpacesStore`. 此值為必要引數。
   * 字串值，指定新增內容的空間完整路徑(例如， `/Company Home/Test Directory`)。 此值為必要引數。
   * 代表新內容的節點名稱(例如， `MortgageForm.pdf`)。 此值為必要引數。
   * 字串值，指定節點型別。 若要新增內容(例如PDF檔案)，請指定 `{https://www.alfresco.org/model/content/1.0}content`. 此值為必要引數。
   * A `com.adobe.idp.Document` 代表內容的物件。 此值為必要引數。
   * 字串值，指定編碼值(例如， `UTF-8`)。 此值為必要引數。
   * 一個 `UpdateVersionType` 指定如何處理版本資訊的列舉值(例如， `UpdateVersionType.INCREMENT_MAJOR_VERSION` 增加內容版本。 )此值是必要引數。
   * A `java.util.List` 指定與內容相關之方面的例項。 此值是選用引數，您可以指定 `null`.
   * A `java.util.Map` 儲存內容屬性的物件。

   此 `storeContent` 方法傳回 `CRCResult` 說明內容的物件。 使用 `CRCResult` 物件，例如，您可以取得內容的唯一識別碼值。 若要執行此工作，請叫用 `CRCResult` 物件的 `getNodeUuid` 方法。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
