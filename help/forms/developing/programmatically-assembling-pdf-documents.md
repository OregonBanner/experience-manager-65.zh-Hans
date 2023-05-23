---
title: 以程式設計方式組裝PDF檔案
seo-title: Programmatically Assembling PDF Documents
description: 使用Assembler服務API，透過Java API和Web服務API將多個PDF檔案組合成單一PDF檔案。
seo-description: Use the Assembler service API to assemble multiple PDF documents into a single PDF document using the Java API and the Web Service API.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 0%

---

# 以程式設計方式組裝PDF檔案 {#programmatically-assembling-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

您可以使用Assembler Service API將多個PDF檔案組合成單一PDF檔案。 下圖顯示三份PDF檔案合併為單一PDF檔案。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

若要將兩個或多個PDF檔案組合成單一PDF檔案，您需要DDX檔案。 DDX檔案說明Assembler服務產生的PDF檔案。 也就是說，DDX檔案會指示Assembler服務要執行的動作。

為了進行此討論，假設使用下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

此DDX檔案合併兩個名為的PDF檔案 *map.pdf* 和 *directions.pdf* 放入單一PDF檔案中。

>[!NOTE]
>
>若要檢視可分解PDF檔案的DDX檔案，請參閱 [以程式設計方式分解PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 使用Web服務叫用Assembler服務時的注意事項 {#considerations-when-invoking-assembler-service-using-web-services}

在組裝大型檔案期間新增頁首和頁尾時，您可能會遇到 `OutOfMemory` 錯誤且無法組裝檔案。 若要減少此問題發生的機率，請新增 `DDXProcessorSetting` 元素加入您的DDX檔案，如下列範例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

您可以將此元素新增為 `DDX` 元素或作為的子項 `PDF result` 元素。 此設定的預設值為0 （零），這會關閉核取指標，而DDX的行為就像是 `DDXProcessorSetting` 元素不存在。 如果您遇到 `OutOfMemory` 錯誤，您可能需要將值設定為整數，通常介於500到5000之間。 較小的查核點值會導致更頻繁的檢查點。

## 步驟摘要 {#summary-of-steps}

若要從多個PDF檔案組合單一PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考輸入PDF檔案。
1. 設定執行階段選項。
1. 組合輸入PDF檔案。
1. 擷取結果。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，則必須將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。

**建立PDF組合器使用者端**

您必須先建立Assembler使用者端，才能以程式設計方式執行Assembler作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF檔案。 例如，請考量本節介紹的DDX檔案。 此DDX檔案會指示Assembler服務將兩個PDF檔案合併為單一PDF檔案。

**參考輸入PDF檔案**

參考您要傳遞至組合器服務的輸入PDF檔案。 例如，如果要傳遞兩個名為「地圖」和「方向」的輸入PDF檔案，則必須傳遞相應的PDF檔案。

map.pdf檔案和directions.pdf檔案都必須放置在集合物件中。 金鑰的名稱必須與DDX檔案中PDF來源屬性的值相符。 如果DDX檔案中的索引鍵和來源屬性相符，則PDF檔案的名稱並不重要。

>[!NOTE]
>
>一個 `AssemblerResult` 物件，包含集合物件，若您叫用 `invokeDDX` 作業。 將兩個或多個輸入PDF檔案傳遞至組合器服務時，會使用此作業。 不過，如果您只傳遞一個輸入PDF至Assembler服務，並且只期望有一個傳回檔案，請叫用 `invokeOneDocument` 作業。 叫用此作業時，會傳回單一檔案。 如需使用此作業的詳細資訊，請參閱 [組合已加密的PDF檔案](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。 如需您可以設定的執行階段選項的相關資訊，請參閱 `AssemblerOptionSpec` 中的類別參考 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**組合輸入PDF檔案**

建立服務使用者端、參考DDX檔案、建立儲存輸入PDF檔案的集合物件，以及設定執行階段選項之後，您可以叫用DDX作業。 使用本節中指定的DDX檔案時，map.pdf和direction.pdf檔案會合併為一個PDF檔案。

**擷取結果**

組合器服務傳回 `java.util.Map` 物件，可從 `AssemblerResult` 物件，以及包含作業結果的物件。 傳回的 `java.util.Map` 物件包含產生的檔案和任何例外狀況。

下表總結了一些鍵值和物件型別，這些值和物件型別可以位於傳回的 `java.util.Map` 物件。

<table>
 <thead>
  <tr>
   <th><p>索引鍵值</p></th>
   <th><p>物件型別</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>包含在DDX結果元素中指定的結果檔案</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>包含檔案的任何例外狀況</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>包含工作記錄</p></td>
  </tr>
 </tbody>
</table>

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式分解PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API組合PDF檔案 {#assemble-pdf-documents-using-the-java-api}

使用組合器服務API (Java)組合PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值（指定DDX檔案的位置）來代表DDX檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 參考輸入PDF檔案。

   * 建立 `java.util.Map` 透過使用儲存輸入PDF檔案的物件 `HashMap` 建構函式。
   * 針對每個輸入PDF檔案，建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞輸入PDF檔案的位置。
   * 針對每個輸入PDF檔案，建立 `com.adobe.idp.Document` 物件並傳遞 `java.io.FileInputStream` 包含PDF檔案的物件。
   * 對於每個輸入檔案，新增一個專案至 `java.util.Map` 物件(透過叫用其 `put` 方法並傳遞下列引數：

      * 代表機碼名稱的字串值。 此值必須與DDX檔案中指定的PDF來源元素的值相符。
      * A `com.adobe.idp.Document` 物件(或 `java.util.List` 物件（指定多個檔案），其中包含來源PDF檔案。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 透過叫用屬於以下專案的方法，設定執行階段選項以滿足您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用 `AssemblerOptionSpec` 物件的 `setFailOnError` 方法與傳遞 `false`.

1. 組合輸入PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列必要值：

   * A `com.adobe.idp.Document` 代表要使用的DDX檔案的物件
   * A `java.util.Map` 包含要組裝之輸入PDF檔案的物件
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項的物件，包括預設字型和作業記錄層級

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含工作結果和發生之任何例外狀況的物件。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的 `getDocuments` 方法。 這會傳回 `java.util.Map` 物件。
   * 循環瀏覽 `java.util.Map` 物件，直到您找到結果為止 `com.adobe.idp.Document` 物件。 (您可以使用DDX檔案中指定的PDF結果元素來取得檔案。)
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 用於擷取PDF檔案的方法。

   >[!NOTE]
   >
   >若 `LOG_LEVEL` 設定為產生記錄，您可使用 `AssemblerResult` 物件的 `getJobLog` 方法。

**另请参阅**

[快速入門（SOAP模式）：使用Java API組合PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API組合PDF檔案 {#assemble-pdf-documents-using-the-web-service-api}

使用Assembler服務API （Web服務）組合PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 參考輸入PDF檔案。

   * 針對每個輸入PDF檔案，建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此集合物件是用來儲存輸入PDF檔案。
   * 針對每個輸入PDF檔案，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。 例如，如果使用兩個輸入PDF檔案，請建立兩個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `key` 欄位。 此值必須與DDX檔案中指定的PDF來源元素的值相符。 (針對每個輸入PDF檔案執行此工作。)
   * 指派 `BLOB` 將PDF檔案儲存至的物件 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `value` 欄位。 (針對每個輸入PDF檔案執行此工作。)
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件至 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` 物件的 `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 (針對每個輸入PDF檔案執行此工作。)

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將值指派給屬於下列專案的資料成員，以設定執行階段選項，符合您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請指派 `false` 至 `AssemblerOptionSpec` 物件的 `failOnError` 資料成員。

1. 組合輸入PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invoke` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件。
   * 此 `mapItem` 包含輸入PDF檔案的陣列。 其索引鍵必須與PDF來源檔案的名稱相符，其值必須是 `BLOB` 對應至這些檔案的物件。
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件。

   此 `invoke` 方法傳回 `AssemblerResult` 物件，包含工作結果以及可能發生的任何例外狀況。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取 `AssemblerResult` 物件的 `documents` 欄位，即 `Map` 包含結果PDF檔案的物件。
   * 循環瀏覽 `Map` 物件，直到找到符合結果檔名稱的鍵為止。 然後轉換該陣列成員的 `value` 至 `BLOB`.
   * 存取代表PDF檔案的二進位資料 `BLOB` 物件的 `MTOM` 屬性。 這會傳回您可以寫出至PDF檔案的位元組陣列。

   >[!NOTE]
   >
   >若 `LOG_LEVEL` 設定為產生記錄，您可以透過取得 `AssemblerResult` 物件的 `jobLog` 資料成員。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
