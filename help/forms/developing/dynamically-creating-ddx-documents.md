---
title: 動態建立DDX檔案
seo-title: Dynamically Creating DDX Documents
description: 使用Java API和Web服務API動態建立DDX檔案。 動態建立DDX檔案可讓您使用在執行階段取得的DDX檔案中的值。
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# 動態建立DDX檔案 {#dynamically-creating-ddx-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

您可以動態建立可用來執行「組合器」作業的DDX檔案。 動態建立DDX檔案可讓您使用在執行階段取得的DDX檔案中的值。 若要動態建立DDX檔案，請使用屬於您使用之程式設計語言的類別。 例如，如果您使用Java開發使用者端應用程式，請使用屬於 `org.w3c.dom.*`封裝。 同樣地，如果您使用Microsoft .NET，請使用屬於 `System.Xml` 名稱空間。

在您可以將DDX檔案傳遞到Assembler服務之前，請先將XML從 `org.w3c.dom.Document` 執行個體變更為一個 `com.adobe.idp.Document` 執行個體。 如果您使用Web服務，請轉換用來建立XML的資料型別(例如， `XmlDocument`)至 `BLOB` 執行個體。

對於此討論，假設已動態建立下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX檔案會拆解PDF檔案。 建議您熟悉PDF檔案的拆解。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

若要使用動態建立的DDX檔案拆分PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 建立DDX檔案。
1. 轉換DDX檔案。
1. 設定執行階段選項。
1. 拆解PDF檔案。
1. 儲存已拆解的PDF檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立PDF組合器使用者端**

以程式設計方式執行Assembler作業之前，請先建立Assembler服務使用者端。

**建立DDX檔案**

使用您使用的程式設計語言建立DDX檔案。 若要建立可分解PDF檔案的DDX檔案，請確保該檔案包含 `PDFsFromBookmarks` 元素。 將用於建立DDX檔案的資料型別轉換為 `com.adobe.idp.Document` 例項。 如果您使用網站服務，請將資料型別轉換為 `BLOB` 執行個體。

**轉換DDX檔案**

使用建立的DDX檔案 `org.w3c.dom` 類別必須轉換為 `com.adobe.idp.Document` 物件。 若要在使用Java API時執行此工作，請使用Java XML轉換類別。 如果您使用Web服務，請將DDX檔案轉換為 `BLOB` 物件。

**參照要分解的PDF檔案**

若要拆解PDF檔案，請參照代表要拆解之PDF檔案的PDF檔案。 當傳遞至Assembler服務時，會針對檔案中的每個1級書籤傳回個別的PDF檔案。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。 若要設定執行階段選項，請使用 `AssemblerOptionSpec` 物件。

**分解PDF檔案**

PDF透過叫用 `invokeDDX` 作業。 傳遞動態建立的DDX檔案。 Assembler服務會傳回集合物件中已解譯的PDF檔案。

**儲存已拆解的PDF檔案**

所有已拆解的PDF檔案都會在集合物件中傳回。 逐一檢視集合物件，並將每個PDF檔案儲存為PDF檔案。

**另请参阅**

[使用Java API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用網站服務API動態建立DDX檔案](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式分解PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API動態建立DDX檔案 {#dynamically-create-a-ddx-document-using-the-java-api}

使用Assembler Service API (Java)動態建立DDX檔案並分解PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 建立DDX檔案。

   * 建立Java `DocumentBuilderFactory` 物件，方法是呼叫 `DocumentBuilderFactory` 類別&#39; `newInstance` 方法。
   * 建立Java `DocumentBuilder` 物件，方法是呼叫 `DocumentBuilderFactory` 物件的 `newDocumentBuilder` 方法。
   * 呼叫 `DocumentBuilder` 物件的 `newDocument` 具現化的方法 `org.w3c.dom.Document` 物件。
   * 透過叫用 `org.w3c.dom.Document` 物件的 `createElement` 方法。 此方法會建立 `Element` 代表根元素的物件。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接著，呼叫子元素的 `setAttribute` 方法。 最後，呼叫標題元素的，將元素附加至標題元素 `appendChild` 方法，並將子元素物件傳遞為引數。 下列幾行程式碼顯示此應用程式邏輯：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 建立 `PDFsFromBookmarks` 元素，方法是呼叫 `Document` 物件的 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 設定值 `PDFsFromBookmarks` 元素(透過呼叫其 `setAttribute` 方法。 附加 `PDFsFromBookmarks` 元素至 `DDX` 元素，方法是呼叫DDX元素的 `appendChild` 方法。 傳遞 `PDFsFromBookmarks` 元素物件做為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 建立 `PDF` 元素，方法是呼叫 `Document` 物件的 `createElement` 方法。 傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 設定值 `PDF` 元素(透過呼叫其 `setAttribute` 方法。 附加 `PDF` 元素至 `PDFsFromBookmarks` 元素，方法是呼叫 `PDFsFromBookmarks` 元素的 `appendChild` 方法。 傳遞 `PDF` 元素物件做為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 轉換DDX檔案。

   * 建立 `javax.xml.transform.Transformer` 物件(透過叫用 `javax.xml.transform.Transformer` 物件的靜態 `newInstance` 方法。
   * 建立 `Transformer` 物件(透過叫用 `TransformerFactory` 物件的 `newTransformer` 方法。
   * 建立 `ByteArrayOutputStream` 物件（使用其建構函式）。
   * 建立 `javax.xml.transform.dom.DOMSource` 物件（使用其建構函式）。 傳遞 `org.w3c.dom.Document` 代表DDX檔案的物件。
   * 建立 `javax.xml.transform.dom.DOMSource` 物件，使用它的建構函式並傳遞 `ByteArrayOutputStream` 物件。
   * 填入Java `ByteArrayOutputStream` 物件(透過叫用 `javax.xml.transform.Transformer` 物件的 `transform` 方法。 傳遞 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 物件。
   * 建立位元組陣列並配置的大小 `ByteArrayOutputStream` 物件至位元組陣列。
   * 透過叫用「 」填入位元組陣列 `ByteArrayOutputStream` 物件的 `toByteArray` 方法。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞位元組陣列。

1. 參照PDF檔案以分解。

   * 建立 `java.util.Map` 透過使用儲存輸入PDF檔案的物件 `HashMap` 建構函式。
   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞PDF檔案的位置以進行拆解。
   * 建立 `com.adobe.idp.Document` 物件。 傳遞 `java.io.FileInputStream` 包含要拆解之PDF檔案的物件。
   * 將專案新增至 `java.util.Map` 物件(透過叫用其 `put` 方法並傳遞下列引數：

      * 代表機碼名稱的字串值。 此值必須與DDX檔案中指定的PDF來源元素的值相符。 (在動態建立的DDX檔案中，值為 `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` 包含要拆解之PDF檔案的物件。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 透過叫用屬於以下專案的方法，設定執行階段選項以滿足您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用 `AssemblerOptionSpec` 物件的 `setFailOnError` 方法與傳遞 `false`.

1. 拆解PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 代表動態建立DDX檔案的物件
   * A `java.util.Map` 包含要拆解之PDF檔案的物件
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項的物件，包括預設字型和作業記錄層級

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 物件，其中包含已解組的PDF檔案以及發生的任何例外狀況。

1. 儲存已拆解的PDF檔案。

   若要取得已拆解的PDF檔案，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的 `getDocuments` 方法。 此方法會傳回 `java.util.Map` 物件。
   * 循環瀏覽 `java.util.Map` 物件，直到您找到結果為止 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 用於擷取PDF檔案的方法。

**另请参阅**

[快速入門（SOAP模式）：使用Java API動態建立DDX檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API動態建立DDX檔案 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用Assembler服務API （Web服務）動態建立DDX檔案並分解PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 設定服務參考時，請務必使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

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

1. 建立DDX檔案。

   * 建立 `System.Xml.XmlElement` 物件（使用其建構函式）。
   * 透過叫用 `XmlElement` 物件的 `CreateElement` 方法。 此方法會建立 `Element` 代表根元素的物件。 將代表元素名稱的字串值傳遞至 `CreateElement` 方法。 呼叫DDX元素的 `SetAttribute` 方法。 最後，透過呼叫 `XmlElement` 物件的 `AppendChild` 方法。 將DDX物件傳遞為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 建立DDX檔案的 `PDFsFromBookmarks` 元素，方法是呼叫 `XmlElement` 物件的 `CreateElement` 方法。 將代表元素名稱的字串值傳遞至 `CreateElement` 方法。 接著，呼叫元素的 `SetAttribute` 方法。 附加 `PDFsFromBookmarks` 元素至根元素，方法是呼叫 `DDX` 元素的 `AppendChild` 方法。 傳遞 `PDFsFromBookmarks` 元素物件做為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 建立DDX檔案的 `PDF` 元素，方法是呼叫 `XmlElement` 物件的 `CreateElement` 方法。 將代表元素名稱的字串值傳遞至 `CreateElement` 方法。 接著，呼叫子元素的 `SetAttribute` 方法。 附加 `PDF` 元素至 `PDFsFromBookmarks` 元素，方法是呼叫 `PDFsFromBookmarks` 元素的 `AppendChild` 方法。 傳遞 `PDF` 元素物件做為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 轉換DDX檔案。

   * 建立 `System.IO.MemoryStream` 物件（使用其建構函式）。
   * 填入 `MemoryStream` 物件與DDX檔案，請使用 `XmlElement` 代表DDX檔案的物件。 叫用 `XmlElement` 物件的 `Save` 方法並傳遞 `MemoryStream` 物件。
   * 建立位元組陣列，並以 `MemoryStream` 物件。 下列程式碼顯示此應用程式邏輯：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 建立 `BLOB` 物件。 將位元組陣列指派給 `BLOB` 物件的 `MTOM` 欄位。

1. 參照PDF檔案以分解。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入PDF檔案。 此 `BLOB` 物件傳遞至 `invokeOneDocument` 作為引數。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表輸入PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 屬性位元組陣列的內容。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將值指派給屬於下列專案的資料成員，以設定執行階段選項，符合您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請指派 `false` 至 `AssemblerOptionSpec` 物件的 `failOnError` 資料成員。

1. 拆解PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列值：

   * A `BLOB` 代表動態建立DDX檔案的物件
   * 此 `mapItem` 包含輸入PDF檔案的陣列
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含工作結果和發生之任何例外狀況的物件。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取 `AssemblerResult` 物件的 `documents` 欄位，即 `Map` 包含已拆解PDF檔案的物件。
   * 循環瀏覽 `Map` 物件以取得每個產生的檔案。 然後，轉換該陣列成員的 `value` 至 `BLOB`.
   * 存取代表PDF檔案的二進位資料 `BLOB` 物件的 `MTOM` 屬性。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
