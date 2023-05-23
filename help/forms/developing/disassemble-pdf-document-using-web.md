---
title: 使用Web服務API分解PDF檔案
seo-title: Disassemble a PDF document usingthe web service API
description: 使用組合器服務API分解PDF檔案
seo-description: Disassemble a PDF document using the Assembler Service API
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
role: Developer
exl-id: de2f90ad-5dea-40a0-8c6d-d6b08228310d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# 使用Web服務API分解PDF檔案 {#disassemble-a-pdf-document-usingthe-web-service-api}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

使用Assembler服務API （Web服務）分解PDF檔案：

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
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，代表DDX檔案的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 參照PDF檔案以分解。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入PDF檔案。 此 `BLOB` 物件傳遞至 `invokeOneDocument` 作為引數。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 欄位位位元組陣列的內容。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此集合物件是用來儲存要拆解的PDF。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `key` 欄位。 此值必須與DDX檔案中指定的PDF來源元素的值相符。
   * 指派 `BLOB` 將PDF檔案儲存至的物件 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `value` 欄位。
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件至 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` object` `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將值指派給屬於下列專案的資料成員，以設定執行階段選項，符合您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請指派 `false` 至 `AssemblerOptionSpec` 物件的 `failOnError` 欄位。

1. 拆解PDF檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列值：

   * A `BLOB` 物件，代表拆解PDF檔案的DDX檔案
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含要拆解之PDF檔案的物件
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含工作結果和發生之任何例外狀況的物件。

1. 儲存已拆解的PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 存取 `AssemblerResult` 物件的 `documents` 欄位，即 `Map` 包含已拆解PDF檔案的物件。
   * 循環瀏覽 `Map` 物件以取得每個產生的檔案。 然後，轉換該陣列成員的 `value` 至 `BLOB`.
   * 存取代表PDF檔案的二進位資料 `BLOB` 物件的 `MTOM` 屬性。 這會傳回您可以寫出至PDF檔案的位元組陣列。

**另请参阅**

[以程式設計方式分解PDF檔案](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
