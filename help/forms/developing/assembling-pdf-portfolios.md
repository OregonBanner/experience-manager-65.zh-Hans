---
title: 組裝PDFPortfolio
seo-title: Assembling PDF Portfolios
description: 組合PDF組合以組合多種型別的檔案，包括Word檔案、影像檔案和PDF檔案。 您可以使用Java API和Web服務API組合PDF組合。
seo-description: Assemble a PDF portfolio to combine several documents of various types, including word file, image files, and PDF documents. You can assemble a PDF portfolio using a Java API and a Web Service API.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---

# 組裝PDFPortfolio {#assembling-pdf-portfolios}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

您可以使用組合器Java和Web服務API組合PDFPortfolio。 產品組合可以組合多種型別的檔案，包括Word檔案、影像檔案（例如jpeg檔案）和PDF檔案。 產品組合的版面配置可設定為不同的樣式，例如 *有預覽的格線*，則 *在影像上* 版面配置或平均 *旋轉*.

下圖是投資組合的熒幕擷圖，其中包含 *在影像上* 樣式配置。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

建立PDFPortfolio可作為傳遞檔案集合的無紙化替代方法。 您可以使用AEM Forms透過結構化DDX檔案叫用Assembler服務來建立投資組合。 下列DDX檔案是建立PDFPortfolio的DDX檔案範例。

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXX檔案必須包含 `Portfolio` 具有巢狀結構的標籤 `Navigator` 標籤之間。 記下標籤 `<Resource name="navigator/image.xxx" source="myImage.png"/>` 僅在以下情況下需要 `myNavigator` 會指派為onImage版面配置導覽器： `AdobeOnImage.nav`. 此標籤可讓Assembler服務選取要作為投資組合背景的影像。 包含 `PackageFiles` 和 `File` 標籤定義封裝檔案的檔案名稱和MIME型別。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

若要建立PDFPortfolio，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考必要的檔案。
1. 設定執行階段選項。
1. 組合投資組合。
1. 儲存組裝的產品組合。

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

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDFPortfolio。 此DDX檔案必須包含 `Portfolio`， `Navigator` 和 `PackageFiles` 元素。

**參考必要的檔案**

若要組裝PDFPortfolio，請參照代表要組裝檔案的所有檔案。 例如，將DDX檔案中指定的所有影像檔案傳遞至組合器服務。 請注意，這些檔案會在本節所指定的DDX檔案中參照： *myImage.png* 和 *saint_bernard.jpg*.

組裝PDFPortfolio時，請將NAV檔案（導覽器檔案）傳遞至Assembler服務。 您傳遞至組合器服務的NAV檔案取決於要建立的PDFPortfolio型別。 例如，若要建立 *在影像上* 配置，傳遞AdobeOnImage.nav檔案。 您可以在下列資料夾中找到NAV檔案：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

從Acrobat 9 （或更新版本）安裝目錄複製NAV檔案。 將NAV檔案放在使用者端應用程式可存取的位置。 所有檔案都會傳遞到Map集合物件中的Assembler服務。

>[!NOTE]
>
>與組裝PDFPortfolio相關的快速入門使用AdobeOnImage.nav。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。

**組合投資組合**

若要組合PDFPortfolio，請呼叫 `invokeDDX` 作業。 Assembler服務會傳回集合物件中的PDFPortfolio。

**儲存組裝的產品組合**

PDFPortfolio會在集合物件中傳回。 逐一檢視集合物件，並將PDFPortfolio儲存為PDF檔案。

**另请参阅**

[使用Java API組合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-java-api)

[使用Web服務API組合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組裝PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API組合PDFPortfolio {#assemble-a-pdf-portfolio-using-the-java-api}

使用Assembler Service API (Java)組合PDFPortfolio：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值（指定DDX檔案的位置）來代表DDX檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 參考必要的檔案。

   * 建立 `java.util.Map` 透過使用儲存輸入PDF檔案的物件 `HashMap` 建構函式。
   * 建立 `java.io.FileInputStream` 物件（使用其建構函式）。 傳遞所需NAV檔案的位置（對建立投資組合所需的每個檔案重複此工作）。
   * 建立 `com.adobe.idp.Document` 物件並傳遞 `java.io.FileInputStream` 包含NAV檔案的物件（對建立投資組合所需的每個檔案重複此工作）。
   * 將專案新增至 `java.util.Map` 物件(透過叫用其 `put` 方法並傳遞下列引數：

      * 代表機碼名稱的字串值。 此值必須與DDX檔案中指定的來源元素的值相符。 （針對建立投資組合所需的每個檔案重複此工作）。
      * A `com.adobe.idp.Document` 包含PDF檔案的物件。 （針對建立投資組合所需的每個檔案重複此工作）。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 透過叫用屬於以下專案的方法，設定執行階段選項以滿足您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用 `AssemblerOptionSpec` 物件的 `setFailOnError` 方法與傳遞 `false`.

1. 組合投資組合。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列必要值：

   * A `com.adobe.idp.Document` 代表要使用的DDX檔案的物件
   * A `java.util.Map` 包含建置PDFPortfolio所需檔案的物件。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項的物件，包括預設字型和作業記錄層級

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含組合PDFPortfolio和發生之任何例外狀況的物件。

1. 儲存組裝的產品組合。

   若要取得PDFPortfolio，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的 `getDocuments` 方法。 此方法會傳回 `java.util.Map` 物件。
   * 循環瀏覽 `java.util.Map` 物件，直到您找到結果為止 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 擷取PDFPortfolio的方法。

**另请参阅**

[快速入門（SOAP模式）：使用Java API組合PDFPortfolio](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API組合PDFPortfolio {#assemble-a-pdf-portfolio-using-the-web-service-api}

使用Assembler服務API （Web服務）組合PDFPortfolio：

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

1. 參考現有的DDX檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存DDX檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表DDX檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 參考必要的檔案。

   * 針對每個輸入檔案，建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表輸入檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此集合物件用於儲存建立PDFPortfolio所需的輸入檔案。
   * 針對每個輸入檔案，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `key` 欄位。 此值必須與DDX檔案中指定的元素值相符。 （針對每個輸入檔案執行此工作。）
   * 指派 `BLOB` 物件，將輸入檔案儲存至 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `value` 欄位。 (針對每個輸入PDF檔案執行此工作。)
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件至 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` 物件的 `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 (針對每個輸入PDF檔案執行此工作。)

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將值指派給屬於下列專案的資料成員，以設定執行階段選項，符合您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請指派 `false` 至 `AssemblerOptionSpec` 物件的 `failOnError` 資料成員。

1. 組合投資組合。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含必要檔案的物件
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含工作結果和發生之任何例外狀況的物件。

1. 儲存組裝的產品組合。

   若要取得新建立的PDFPortfolio，請執行下列動作：

   * 存取 `AssemblerResult` 物件的 `documents` 欄位，即 `Map` 包含結果PDF檔案的物件。
   * 循環瀏覽 `Map` 物件以取得每個產生的檔案。 然後，轉換該陣列成員的 `value` 至 `BLOB`.
   * 存取代表PDF檔案的二進位資料 `BLOB` 物件的 `MTOM` 屬性。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
