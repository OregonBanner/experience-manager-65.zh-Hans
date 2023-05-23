---
title: 判斷檔案是否符合PDF/A規範
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: 使用Java API和Web服務API，使用Assembler服務來判斷PDF檔案是否符合PDF/A標準。
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 2%

---

# 判斷檔案是否符合PDF/A規範 {#determining-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服務來判斷PDF檔案是否符合PDF/A標準。 PDF/檔案是用來長期儲存檔案內容的封存格式。 字体将嵌入到文档中，并且文件是未压缩的。因此，PDF/A 文档通常比标准 PDF 文档大。此外，PDF/A 文档不包含音频和视频内容。

PDF/A-1規格包含兩個一致性層級，即A和B。兩個層級之間的主要差異在於邏輯結構（協助工具）支援，這是符合性層級B所不需要。無論符合性層級為何，PDF/A-1會指定所有字型都內嵌在產生的PDF/A檔案中。 目前，驗證（和轉換）僅支援PDF/A-1b。

為了進行此討論，假設使用下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

在此DDX檔案中， `DocumentInformation` 元素會指示Assembler服務傳回有關輸入PDF檔案的資訊。 在內 `DocumentInformation` 元素， `PDFAValidation` element指示Assembler服務指出輸入PDF檔案是否符合PDF/A。

Assembler服務會傳回指定輸入PDF檔案在包含的XML檔案中是否符合PDF/A的資訊。 `PDFAConformance` 元素。 如果輸入PDF檔案符合PDF/A標準，則值 `PDFAConformance` 元素的 `isCompliant` 屬性為 `true`. 如果PDF檔案不符合PDF/A標準，則其值 `PDFAConformance` 元素的 `isCompliant` 屬性為 `false`.

>[!NOTE]
>
>因為在此區段中指定的DDX檔案包含 `DocumentInformation` 元素，則Assembler服務會傳回XML資料，而非PDF檔案。 也就是說，Assembler服務不會組裝或拆解PDF檔案；它會傳回XML檔案中有關輸入PDF檔案的資訊。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

若要判斷PDF檔案是否符合PDF/A標準，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考用於判斷PDF/A合規性的PDF檔案。
1. 設定執行階段選項。
1. 擷取PDF檔案的相關資訊。
1. 儲存傳回的XML檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果AEM Forms部署在支援的J2EE應用程式伺服器上，而不是JBoss，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立PDF組合器使用者端**

您必須先建立Assembler服務使用者端，才能以程式設計方式執行Assembler作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能執行組合器服務作業。 若要判斷輸入PDF檔案是否符合PDF/A標準，請確定DDX檔案包含 `PDFAValidation` 內的元素 `DocumentInformation` 元素。 此 `PDFAValidation` element會指示Assembler服務傳回XML檔案，以指定輸入PDF檔案是否符合PDF/A規範。

**參考用於判斷PDF/A合規性的PDF檔案**

必須參考PDF檔案並將其傳遞到Assembler服務，以確定PDF檔案是否符合PDF/A規範。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。 如需您可以設定的執行階段選項的相關資訊，請參閱 `AssemblerOptionSpec` 中的類別參考 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**擷取PDF檔案的相關資訊**

建立Assembler服務使用者端、參照DDX檔案、參照互動式PDF檔案，以及設定執行階段選項之後，您可以叫用 `invokeDDX` 作業。 因為DDX檔案包含 `DocumentInformation` 元素，則Assembler服務會傳回XML資料，而非PDF檔案。

**儲存傳回的XML檔案**

Assembler服務傳回的XML檔案會指定輸入PDF檔案是否符合PDF/A。 例如，如果輸入PDF檔案不符合PDF/A標準，Assembler服務會傳回包含以下元素的XML檔案：

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

將XML檔案儲存為XML檔案，以便您可以開啟檔案並檢視結果。

**另请参阅**

[使用Java API判斷檔案是否符合PDF/A規範](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[使用Web服務API判斷檔案是否符合PDF/A標準](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組裝PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API判斷檔案是否符合PDF/A規範 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

使用Assembler Service API (Java)判斷PDF檔案是否符合PDF/A規範：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值（指定DDX檔案的位置）來代表DDX檔案。 若要確定PDF檔案是否符合PDF/A標準，請確定DDX檔案包含 `PDFAValidation` 包含在中的元素 `DocumentInformation` 元素。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 參考用於判斷PDF/A合規性的PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用物件的建構函式，並傳遞用來判斷PDF/A相容性的PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 包含PDF檔案的物件。
   * 建立 `java.util.Map` 透過使用儲存輸入PDF檔案的物件 `HashMap` 建構函式。
   * 將專案新增至 `java.util.Map` 物件(透過叫用其 `put` 方法並傳遞下列引數：

      * 代表機碼名稱的字串值。 此值必須與DDX檔案中指定的來源元素的值相符。 例如，本節介紹的DDX檔案中來源元素的值為Loan.pdf。
      * A `com.adobe.idp.Document` 包含輸入PDF檔案的物件。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 透過叫用屬於以下專案的方法，設定執行階段選項以滿足您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用 `AssemblerOptionSpec` 物件的 `setFailOnError` 方法與傳遞 `false`.

1. 擷取PDF檔案的相關資訊。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列必要值：

   * A `com.adobe.idp.Document` 代表要使用的DDX檔案的物件
   * A `java.util.Map` 包含用於判斷PDF/A相容性之輸入PDF檔案的物件
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項的物件

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含指定輸入PDF檔案是否符合PDF/A規範之XML資料的物件。

1. 儲存傳回的XML檔案。

   若要取得指定輸入PDF檔案是否為PDF/A檔案的XML資料，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的 `getDocuments` 方法。 這會傳回 `java.util.Map` 物件。
   * 循環瀏覽 `java.util.Map` 物件，直到您找到結果為止 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 用於擷取XML檔案的方法。 請確定您將XML資料儲存為XML檔案。

**另请参阅**

[快速入門（SOAP模式）：使用Java API判斷檔案是否符合PDF/A標準](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAP模式）

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API判斷檔案是否符合PDF/A標準 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

使用Assembler服務API （Web服務）來判斷PDF檔案是否符合PDF/A規範：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立PDF組合器使用者端。

   * 建立 `AssemblerServiceClient` 物件（使用其預設建構函式）。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `AssemblerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參考現有的DDX檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存DDX檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表DDX檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 參考用於判斷PDF/A合規性的PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此集合物件用於儲存PDF檔案。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `key` 欄位。 此值必須與DDX檔案中指定的PDF來源元素的值相符。
   * 指派 `BLOB` 將PDF檔案儲存至的物件 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `value` 欄位。
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件至 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` object` `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將值指派給屬於下列專案的資料成員，以設定執行階段選項，符合您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請指派 `false` 至 `AssemblerOptionSpec` 物件的 `failOnError` 資料成員。

1. 擷取PDF檔案的相關資訊。

   叫用 `AssemblerServiceService` 物件的 `invoke` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件。
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含輸入PDF檔案的物件。 其索引鍵必須與PDF來源檔案的名稱相符，其值必須是 `BLOB` 對應至輸入PDF檔案的物件。
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件。

   此 `invoke` 方法傳回 `AssemblerResult` 包含指定輸入PDF檔案是否為PDF/A檔案的XML資料的物件。

1. 儲存傳回的XML檔案。

   若要取得指定輸入PDF檔案是否為PDF/A檔案的XML資料，請執行下列動作：

   * 存取 `AssemblerResult` 物件的 `documents` 欄位，即 `Map` 包含指定輸入PDF檔案是否為PDF/A檔案的XML資料的物件。
   * 循環瀏覽 `Map` 物件以取得每個產生的檔案。 然後，將該陣列成員的值轉換為 `BLOB`.
   * 存取代表XML資料的二進位資料，以擷取其 `BLOB` 物件的 `MTOM` 欄位。 此欄位儲存您可以寫出為XML檔案的位元組陣列。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
