---
title: 使用網站服務API驗證DDX檔案
seo-title: Validate a DDX document using theweb service API
description: 使用組合器服務API來驗證DDX檔案。
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 使用網站服務API驗證DDX檔案 {#validate-a-ddx-document-using-theweb-service-api}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

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

[驗證DDX檔案](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
