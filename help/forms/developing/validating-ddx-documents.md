---
title: 驗證DDX檔案
seo-title: Validating DDX Documents
description: 使用Java API和Web服務API以程式設計方式驗證DDX檔案。
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 0%

---

# 驗證DDX檔案 {#validating-ddx-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

您可以以程式設計方式驗證Assembler服務所使用的DDX檔案。 也就是說，您可以使用Assembler服務API來判斷DDX檔案是否有效。 例如，如果您從先前的AEM Forms版本升級，並且想要確保DDX檔案有效，則可以使用組合器服務API來驗證它。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

若要驗證DDX檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立組合器使用者端。
1. 參考現有的DDX檔案。
1. 設定執行階段選項以驗證DDX檔案。
1. 執行驗證。
1. 將驗證結果儲存在記錄檔中。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果AEM Forms部署在支援的J2EE應用程式伺服器上，而不是JBoss，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。

**建立PDF組合器使用者端**

您必須先建立Assembler服務使用者端，才能以程式設計方式執行Assembler作業。

**參考現有的DDX檔案**

若要驗證DDX檔案，您必須參考現有的DDX檔案。

**設定執行階段選項以驗證DDX檔案**

驗證DDX檔案時，您必須設定特定的執行階段選項，指示組合器服務驗證DDX檔案，而不是執行。 此外，您也可以增加Assembler服務寫入記錄檔的資訊量。

**執行驗證**

建立Assembler服務使用者端、參考DDX檔案並設定執行階段選項之後，您可以叫用 `invokeDDX` 驗證DDX檔案的作業。 驗證DDX檔案時，您可以通過 `null` 作為map引數(此引數通常會儲存Assembler執行DDX檔案中指定之作業所需的PDF檔案)。

如果驗證失敗，系統會擲回例外狀況，而記錄檔中包含說明DDX檔案無效原因的詳細資訊，您可從 `OperationException` 執行個體。 一旦通過基本的XML剖析和結構描述檢查，就會執行DDX規格的驗證。 所有位於DDX檔案中的錯誤都會在記錄中指定。

**將驗證結果儲存在記錄檔中**

Assembler服務會傳回您可以寫入XML記錄檔的驗證結果。 Assembler服務寫入記錄檔的詳細資訊量取決於您設定的執行階段選項。

**另请参阅**

[使用Java API驗證DDX檔案](#validate-a-ddx-document-using-the-java-api)

[使用網站服務API驗證DDX檔案](#validate-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組裝PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API驗證DDX檔案 {#validate-a-ddx-document-using-the-java-api}

使用組合器服務API (Java)驗證DDX檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值（指定DDX檔案的位置）來代表DDX檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定執行階段選項以驗證DDX檔案。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 設定執行階段選項，指示組合器服務透過叫用 `AssemblerOptionSpec` 物件的setValidateOnly方法和傳遞 `true`.
   * 透過叫用「 」，設定Assembler服務寫入記錄檔的資訊量 `AssemblerOptionSpec` 物件的 `getLogLevel` 方法和傳遞字串值符合您的需求。 驗證DDX檔案時，您想要將更多資訊寫入記錄檔，以協助進行驗證程式。 因此，您可以傳遞值 `FINE` 或 `FINER`.

1. 執行驗證。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 代表DDX檔案的物件。
   * 值 `null` java.io.Map物件(通常儲存PDF檔案)。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項的物件。

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含指定DDX檔案是否有效的資訊的物件。

1. 將驗證結果儲存在記錄檔中。

   * 建立 `java.io.File` 物件，並確認副檔名為.xml。
   * 叫用 `AssemblerResult` 物件的 `getJobLog` 方法。 此方法會傳回 `com.adobe.idp.Document` 包含驗證資訊的例項。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件至檔案。

   >[!NOTE]
   >
   >如果DDX檔案無效，請 `OperationException` 擲回。 在catch陳述式中，您可以叫用 `OperationException` 物件的 `getJobLog` 方法。

**另请参阅**

[驗證DDX檔案](#validating-ddx-documents)

[快速入門（SOAP模式）：使用Java API驗證DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API驗證DDX檔案 {#validate-a-ddx-document-using-the-web-service-api}

使用組合器服務API （Web服務）驗證DDX檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >將localhost取代為表單伺服器的IP位址。

1. 建立PDF組合器使用者端。

   * 建立 `AssemblerServiceClient` 物件（使用其預設建構函式）。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。
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
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 設定執行階段選項以驗證DDX檔案。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將值true指派給，設定執行階段選項，指示Assembler服務驗證DDX檔案。 `AssemblerOptionSpec` 物件的 `validateOnly` 資料成員。
   * 將字串值指派給，設定Assembler服務寫入記錄檔的資訊量。 `AssemblerOptionSpec` 物件的 `logLevel` 資料成員。 方法驗證DDX檔案時，您想要將更多資訊寫入記錄檔，以協助進行驗證程式。 因此，您可以指定值 `FINE` 或 `FINER`. 如需您可以設定的執行階段選項的相關資訊，請參閱 `AssemblerOptionSpec` 中的類別參考 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 執行驗證。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件。
   * 值 `null` 的 `Map` 通常儲存PDF檔案的物件。
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件。

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含指定DDX檔案是否有效的資訊的物件。

1. 將驗證結果儲存在記錄檔中。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表記錄檔檔案位置的字串值，以及用來開啟檔案的模式。 確認副檔名為.xml。
   * 建立 `BLOB` 物件，透過取得 `AssemblerResult` 物件的 `jobLog` 資料成員。
   * 建立位元組陣列，儲存 `BLOB` 物件。 透過取得 `BLOB` 物件的 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

   >[!NOTE]
   >
   >如果DDX檔案無效，請 `OperationException` 擲回。 在catch陳述式中，您可以取得 `OperationException` 物件的 `jobLog` 成員。

**另请参阅**

[驗證DDX檔案](#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
