---
title: 將Postscript轉換為PDF檔案
seo-title: Converting Postscript to PDF Documents
description: 使用Distiller服務，透過網路將PostScript®、封裝式PostScript (EPS)和PRN檔案轉換為緊湊、可靠且更安全的PDF檔案。 Distiller服務使用Java API和Web服務API將大量列印檔案轉換為電子檔案，例如發票和對帳單。
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---

# 將Postscript轉換為PDF檔案 {#converting-postscript-to-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 關於Distiller服務 {#about-the-distiller-service}

Distiller®服務可透過網路將PostScript®、Encapsulated PostScript (EPS)和PRN檔案轉換為緊湊、可靠且更安全的PDF檔案。 Distiller服務通常用於將大量列印檔案轉換為電子檔案，例如發票和結算單。 將檔案轉換為PDF也可讓企業向客戶傳送檔案的書面版本和電子版本。

>[!NOTE]
>
>如需Distiller服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將PostScript轉換為PDF檔案 {#converting-postscript-to-pdf-documents-inner}

本主題說明如何使用Distiller服務API （Java和Web服務）以程式設計方式將PostScript (PS)、Encapsulated PostScript (EPS)和PRN檔案轉換為PDF檔案。

>[!NOTE]
>
>如需Distiller服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>若要將PostScript檔案轉換成PDF檔案，必須在託管AEM Forms的伺服器上安裝下列其中一項功能： Acrobat 9或Microsoft Visual C++ 2005可轉散發套件。

### 步驟摘要 {#summary-of-steps}

若要將任何支援的型別轉換為PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Distiller服務使用者端。
1. 擷取要轉換的檔案。
1. 叫用PDF建立作業。
1. 儲存PDF檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Distiller服務使用者端**

您必須先建立Distiller服務使用者端，才能以程式設計方式執行Distiller服務操作。 如果您使用Java API，請建立 `DistillerServiceClient` 物件。 如果您使用Web服務API，請建立 `DistillerServiceService` 物件。

**擷取要轉換的檔案**

您必須擷取要轉換的檔案。 例如，若要將PS檔案轉換為PDF檔案，您必須擷取PS檔案。

**叫用PDF建立作業**

建立服務使用者端後，您可以叫用PDF建立作業。 此操作將需要有關要轉換檔案的資訊，包括目標檔案的路徑。

**儲存PDF檔案**

您可以將PDF檔案儲存為PDF檔案。

**另请参阅**

[使用Java API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用Web服務API將PostScript檔案轉換為PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API將PostScript檔案轉換為PDF {#convert-a-postscript-file-to-pdf-using-the-java-api}

使用Distiller Service API (Java)將PostScript檔案轉換為PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-distiller-client.jar。

1. 建立Distiller服務使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `DistillerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取要轉換的檔案。

   * 建立 `java.io.FileInputStream` 物件，代表要轉換的檔案，使用它的建構函式並傳遞字串值，指定檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 叫用PDF建立作業。

   叫用 `DistillerServiceClient` 物件的 `createPDF` 方法並傳遞下列值：

   * 此 `com.adobe.idp.Document` 代表要轉換之PS、EPS或PRN檔案的物件
   * A `java.lang.String` 包含要轉換之檔案名稱的物件
   * A `java.lang.String` 包含要使用的Adobe PDF設定名稱的物件
   * A `java.lang.String` 包含要使用的安全性設定名稱的物件
   * 選填 `com.adobe.idp.Document` 包含產生PDF檔案時要套用之設定的物件
   * 選填 `com.adobe.idp.Document` 包含要套用至PDF檔案之中繼資料資訊的物件

   此 `createPDF` 方法傳回 `CreatePDFResult` 包含新PDF檔案和可能產生的記錄檔的物件。 記錄檔通常包含轉換請求產生的錯誤或警告訊息。

1. 儲存PDF檔案。

   若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用 `CreatePDFResult` 物件的 `getCreatedDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 用於擷取PDF檔案的方法。

   同樣地，若要取得記錄檔案，請執行下列動作。

   * 叫用 `CreatePDFResult` 物件的 `getLogDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 擷取記錄檔案的方法。


**另请参阅**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API將PostScript檔案轉換為PDF檔案](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PostScript檔案轉換為PDF {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

使用Distiller服務API （Web服務）將PostScript檔案轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Distiller服務使用者端。

   * 建立 `DistillerServiceClient` 物件（使用其預設建構函式）。
   * 建立 `DistillerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `DistillerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取要轉換的檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存要轉換成PDF檔案的檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表檔案位置和開啟檔案模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 叫用PDF建立作業。

   叫用 `DistillerServiceService` 物件的 `CreatePDF2` 方法並傳遞下列必要值：

   * 此 `BLOB` 代表要轉換之PS檔案的物件
   * 包含要轉換之檔案的路徑名稱的字串
   * 字串物件，包含要使用的Adobe PDF設定(例如 `Standard`)
   * 字串物件，包含要使用的安全性設定(例如， `No Securit`y)
   * 選填 `BLOB` 包含產生PDF檔案時要套用之設定的物件
   * 選填 `BLOB` 包含要套用至PDF檔案之中繼資料資訊的物件
   * A `BLOB` 用來儲存PDF檔案的輸出引數
   * A `BLOB` 用來儲存記錄檔的輸出引數

1. 儲存PDF檔案。

   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表已簽署PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `CreatePDF2` 方法（輸出引數）。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
