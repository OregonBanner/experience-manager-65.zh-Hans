---
title: 使用Bates編號組合檔案
seo-title: Assembling Documents Using Bates Numbering
description: 使用Bates編號，以使用Java和Web服務API組合PDF檔案。
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---

# 使用Bates編號組合檔案 {#assembling-documents-using-bates-numbering}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

您可以使用Bates編號來組合包含唯一頁面識別碼的PDF檔案。 *Bates編號* 是一種將唯一識別套用至一批相關檔案的方法。 檔案（或檔案集）中的每個頁面都指定一個Bates編號，可唯一識別頁面。 例如，包含用料表資訊且與組裝料號生產相關聯的製造檔案可以包含識別碼。 Bates數字包含循序遞增的數值，以及選用的首碼和尾碼。 前置詞+數值+後置詞稱為 *bates圖樣*.

下圖顯示的PDF檔案包含位於檔案標題中的唯一識別碼。

![au_au_batesnumber](assets/au_au_batesnumber.png)

為了進行此討論，唯一頁面識別碼會放置在檔案的頁首中。 假設使用下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

此DDX檔案合併兩個名為的PDF檔案 *map.pdf* 和 *directions.pdf* 放入單一PDF檔案中。 產生的PDF檔案包含由唯一頁面識別碼組成的標頭。 例如，上圖中的檔案顯示000016。

>[!NOTE]
>
>閱讀本節之前，建議您先熟悉使用Assembler服務組裝PDF檔案。 本節不討論相關概念，例如建立包含輸入檔案的集合物件，或從傳回的集合物件中擷取結果。 (請參閱 [以程式設計方式組裝PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

若要組合包含唯一頁面識別碼（Bates編號）的PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考輸入PDF檔案。
1. 設定初始Bates數字值。
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

如果將AEM Forms部署在JBoss以外的受支援J2EE應用程式伺服器上，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立PDF組合器使用者端**

您必須先建立Assembler服務使用者端，才能以程式設計方式執行Assembler作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF檔案。 例如，請考量本節介紹的DDX檔案。 若要組合包含唯一頁面識別碼的PDF檔案，DDX檔案必須包含 `BatesNumber` 元素。

**參考輸入PDF檔案**

必須參考輸入PDF檔案才能組裝PDF檔案。 例如，必須參照map.pdf和directions.pdf檔案，才能將這些PDF檔案組合成單一PDF檔案。

**設定初始Bates數字值**

您可以設定初始Bates編號值，以符合您的業務需求。 例如，假設需要將初始值設為000100。 如果您未設定初始值，則會顯000000第一頁的值。

**組合輸入PDF檔案**

建立Assembler服務使用者端後，請參考包含下列內容的DDX檔案 `BatesNumber` 元素資訊、參考輸入PDF檔案以及設定執行階段選項，您可以叫用 `invokeDDX` 作業會導致Assembler服務組裝包含唯一頁面識別碼的PDF檔案。

**擷取結果**

Assembler服務會傳回包含工作結果的集合物件。 您可以擷取結果PDF檔案以及擲回的任何例外狀況。 在此情況下，加密的PDF檔案會位於集合物件內。

>[!NOTE]
>
>若您叫用 `invokeDDX` 作業。 將兩個或多個輸入PDF檔案傳遞至Assembler服務時，會使用此作業。 不過，如果您只傳遞一個輸入PDF檔案至組合器服務，則應叫用 `invokeOneDocument` 作業。 如需使用此作業的詳細資訊，請參閱 [組合已加密的PDF檔案](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組裝PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API以Bates編號組合檔案 {#assemble-documents-with-bates-numbering-using-the-java-api}

使用Assembler Service API (Java)來組合使用唯一頁面識別碼（Bates編號）的PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值（指定DDX檔案的位置）來代表DDX檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 參考輸入PDF檔案。

   * 建立 `java.util.Map` 使用儲存輸入PDF檔案的物件 `HashMap` 建構函式。
   * 針對每個輸入PDF檔案，建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞輸入PDF檔案的位置。 在此情況下，請傳遞不安全PDF檔案的位置。
   * 針對每個輸入PDF檔案，建立 `com.adobe.idp.Document` 物件並傳遞 `java.io.FileInputStream` 包含PDF檔案的物件。
   * 將專案新增至 `java.util.Map` 物件(透過叫用其 `put` 方法並傳遞下列引數：

      * 代表機碼名稱的字串值。 此值必須與DDX檔案中指定的PDF來源元素的值相符。 例如，本節介紹的DDX檔案中指定的PDF來源檔案名稱為Loan.pdf。
      * A `com.adobe.idp.Document` 包含不安全PDF檔案的物件。

1. 設定初始Bates數字值。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 透過叫用設定初始Bates編號 `AssemblerOptionSpec` 物件的 `setFirstBatesNumber` 和傳遞指定初始值的數值。

1. 組合輸入PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列必要值：

   * A `com.adobe.idp.Document` 代表DDX檔案的物件。
   * A `java.util.Map` 包含輸入不安全PDF檔案的物件。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項的物件，包括預設字型和作業記錄層級。

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含密碼加密PDF檔案的物件。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的 `getDocuments` 方法。 此動作會傳回 `java.util.Map` 物件。
   * 循環瀏覽 `java.util.Map` 物件，直到您找到 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 用於擷取PDF檔案的方法。

**另请参阅**

[快速入門（SOAP模式）：使用Java API組合Bates編號的PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API以Bates編號組合檔案 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

使用Assembler Service API （Web服務）來組合使用唯一頁面識別碼（Bates編號）的PDF檔案：

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
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表DDX檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 參考輸入PDF檔案。

   * 針對每個輸入PDF檔案，建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入PDF檔案。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表輸入PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此集合物件是用來儲存輸入PDF檔案。
   * 針對每個輸入PDF檔案，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。 例如，如果使用兩個輸入PDF檔案，請建立兩個 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `key` 欄位。 此值必須與DDX檔案中指定的PDF來源元素的值相符。 (針對每個輸入PDF檔案執行此工作。)
   * 指派 `BLOB` 將PDF檔案儲存至的物件 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `value` 欄位。 (針對每個輸入PDF檔案執行此工作。)
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件至 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` 物件的 `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 (針對每個輸入PDF檔案執行此工作。)

1. 設定初始Bates數字值。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將數值指定給，以設定初始Bates編號 `firstBatesNumber` 屬於下列專案的資料成員： `AssemblerOptionSpec` 物件。

1. 組合輸入PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invoke` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件。
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含輸入PDF檔案的物件。 其索引鍵必須與PDF來源檔案的名稱相符，其值必須是 `BLOB` 與這些檔案對應的物件。
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件。

   此 `invoke` 方法傳回 `AssemblerResult` 包含工作結果和發生之任何例外狀況的物件。

1. 擷取結果。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取 `AssemblerResult` 物件的 `documents` 欄位，即 `Map` 包含結果PDF檔案的物件。
   * 循環瀏覽 `Map` 物件，直到找到符合結果檔名稱的鍵為止。 然後轉換該陣列成員的 `value` 至 `BLOB`.
   * 存取代表PDF檔案的二進位資料 `BLOB` 物件的 `MTOM` 屬性。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
