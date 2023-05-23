---
title: 在檔案格式和PDF之間轉換
seo-title: Converting Between File Formats and PDF
description: 使用「產生PDF」服務將原生檔案格式轉換為PDF。 「產生PDF」服務也會將PDF轉換為其他檔案格式，並最佳化PDF檔案的大小。
seo-description: Use the Generate PDF service to convert native file formats to PDF. Generate PDF service also converts PDF to other file formats and optimizes the size of PDF documents.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '7850'
ht-degree: 0%

---

# 在檔案格式和PDF之間轉換 {#converting-between-file-formatsand-pdf}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於產生PDF服務**

「產生PDF」服務會將原生檔案格式轉換為PDF。 它也會將PDF轉換為其他檔案格式，並最佳化PDF檔案的大小。

「產生PDF」服務使用原生應用程式將下列檔案格式轉換為PDF。 除非另有指示，否則僅支援這些應用程式的德文、法文、英文和日文版本。 *僅限Windows* 表示僅支援Windows Server® 2003和Windows Server 2008。

* Microsoft Office 2003和2007可轉換DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX、XPS和PUB （僅限Windows）

>[!NOTE]
>
>需要Acrobat® 9.2或更新版本，才能將Microsoft XPS格式轉換為PDF。

* Autodesk AutoCAD 2005、2006、2007、2008和2009轉換DWF、DWG和DXW （僅限英文）
* Corel WordPerfect 12和X4可轉換WPD、QPW、SHW （僅限英文）
* OpenOffice 2.0、2.4、3.0.1和3.1，可轉換ODT、ODS、ODP、ODG、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX和PUB

>[!NOTE]
>
>產生PDF服務不支援64位元版本的OpenOffice。

* Adobe Photoshop® CS2轉換PSD（僅限Windows）

>[!NOTE]
>
>不支援Photoshop CS3和CS4，因為它們不支援Windows Server 2003或Windows Server 2008。

* Adobe FrameMaker® 7.2和8可轉換FM （僅限Windows）
* AdobePageMaker® 7.0可轉換PMD、PM6、P65和PM （僅限Windows）
* 協力廠商應用程式支援的原生格式（需要開發應用程式專用的安裝檔案） （僅限Windows）

「產生PDF」服務會將下列以標準為基礎的檔案格式轉換為PDF。

* 視訊格式：SWF、FLV （僅限Windows）
* 影像格式：JPEG、JPG、JP2、J2Kí、JPC、J2C、GIF、BMP、TIFF、TIF、PNG、JPF
* HTML(Windows、Sun™Solaris™和Linux®)

產生PDF服務會將PDF轉換為下列檔案格式（僅限Windows）：

* 封裝式PostScript (EPS)
* HTML3.2
* HTML4.01與CSS 1.0
* DOC (Microsoft Word格式)
* RTF
* 文字（可存取和純文字）
* XML
* 只使用DeviceRGB色彩空間的PDF/A-1a
* 僅使用DeviceRGB色彩空間的PDF/A-1b

「產生PDF」服務要求您執行下列管理工作：

* 在託管AEM Forms的電腦上安裝必要的原生應用程式
* 在託管AEM Forms的電腦上安裝Adobe Acrobat Professional或Acrobat Pro Extended 9.2
* 執行安裝後設定工作

使用JBoss Turnkey安裝和部署AEM Forms中會說明這些工作。

您可以使用「產生PDF」服務完成這些工作：

* 從原生檔案格式轉換成PDF。
* 將HTML檔案轉換為PDF檔案。
* 將PDF檔案轉換為檔案格式。

>[!NOTE]
>
>如需「產生PDF」服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將Word檔案轉換為PDF檔案 {#converting-word-documents-to-pdf-documents}

本節說明如何使用產生PDFAPI，以程式設計方式將Microsoft Word檔案轉換為PDF檔案。

>[!NOTE]
>
>如需其他檔案格式的詳細資訊，請參閱 [新增對其他原生檔案格式的支援](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
>如需「產生PDF」服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要將Microsoft Word檔案轉換為PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立「產生PDF」使用者端。
1. 擷取檔案以轉換為PDF檔案。
1. 將檔案轉換為PDF檔案。
1. 擷取結果。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立產生PDF使用者端**

以程式設計方式執行產生PDF作業之前，請先建立產生PDF服務使用者端。 如果您使用Java API，請建立 `GeneratePdfServiceClient` 物件。 如果您使用Web服務API，請建立 `GeneratePDFServiceService` 物件。

**擷取檔案以轉換為PDF檔案**

擷取Microsoft Word檔案以轉換為PDF檔案。

**將檔案轉換為PDF檔案**

建立「產生PDF服務」使用者端後，您可以叫用 `createPDF2` 方法。 此方法需要轉換檔案的相關資訊，包括副檔名。

**擷取結果**

將檔案轉換為PDF檔案後，您可以擷取結果。 例如，將Word檔案轉換為PDF檔案後，您可以擷取並儲存PDF檔案。

**另请参阅**

[使用Java API將Word檔案轉換為PDF檔案](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[使用Web服務API將Word檔案轉換為PDF檔案](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速啟動](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將Word檔案轉換為PDF檔案 {#convert-word-documents-to-pdf-documents-using-the-java-api}

使用產生PDFAPI (Java)將Microsoft Word檔案轉換為PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立「產生PDF」使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `GeneratePdfServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取檔案以轉換為PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，代表要透過其建構函式轉換的Word檔案。 傳遞指定檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 將檔案轉換為PDF檔案。

   PDF透過叫用 `GeneratePdfServiceClient` 物件的 `createPDF2` 並傳遞下列值：

   * A `com.adobe.idp.Document` 物件，代表要轉換的檔案。
   * A `java.lang.String` 包含副檔名的物件。
   * A `java.lang.String` 包含轉換中所要使用的檔案型別設定的物件。 檔案型別設定提供不同檔案型別（例如.doc或.xls）的轉換設定。
   * A `java.lang.String` 包含要使用的PDF設定名稱的物件。 例如，您可以指定 `Standard`.
   * A `java.lang.String` 包含要使用的安全性設定名稱的物件。
   * 選填 `com.adobe.idp.Document` 包含產生PDF檔案時要套用之設定的物件。
   * 選填 `com.adobe.idp.Document` 包含要套用至PDF檔案之中繼資料資訊的物件。

   此 `createPDF2` 方法傳回 `CreatePDFResult` 包含新PDF檔案和記錄資訊的物件。 記錄檔通常包含轉換請求產生的錯誤或警告訊息。

1. 擷取結果。

   若要取得PDF檔案，請執行下列動作：

   * 叫用 `CreatePDFResult` 物件的 `getCreatedDocument` 方法，會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 從上一步建立的物件中擷取PDF檔案的方法。

   如果您使用 `createPDF2` 取得記錄檔案的方法(不適用於HTML轉換)，請執行下列動作：

   * 叫用 `CreatePDFResult` 物件的 `getLogDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 擷取記錄檔案的方法。


**另请参阅**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API將Microsoft Word檔案轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將Word檔案轉換為PDF檔案 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

使用產生PDFAPI （Web服務）將Microsoft Word檔案轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立「產生PDF」使用者端。

   * 建立 `GeneratePDFServiceClient` 物件（使用其預設建構函式）。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `GeneratePDFServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取檔案以轉換為PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存您要轉換成PDF檔案的檔案。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，該值代表要轉換的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派給其 `MTOM` 屬性位元組陣列的內容。

1. 將檔案轉換為PDF檔案。

   PDF透過叫用 `GeneratePDFServiceService` 物件的 `CreatePDF2` 並傳遞下列值：

   * A `BLOB` 物件，代表要轉換的檔案。
   * 包含副檔名的字串。
   * A `java.lang.String` 包含轉換中所要使用的檔案型別設定的物件。 檔案型別設定提供不同檔案型別（例如.doc或.xls）的轉換設定。
   * 字串物件，包含要使用的PDF設定。 您可以指定 `Standard`.
   * 字串物件，包含要使用的安全性設定。 您可以指定 `No Security`.
   * 選填 `BLOB` 包含產生PDF檔案時要套用之設定的物件。
   * 選填 `BLOB` 包含要套用至PDF檔案之中繼資料資訊的物件。
   * 型別的輸出引數 `BLOB` 由填入的 `CreatePDF2` 方法。 此 `CreatePDF2` 方法會以轉換後的檔案填入此物件。 （只有Web服務呼叫需要此引數值）。
   * 型別的輸出引數 `BLOB` 由填入的 `CreatePDF2` 方法。 此 `CreatePDF2` 方法會將記錄檔案填入此物件。 （只有Web服務呼叫需要此引數值）。

1. 擷取結果。

   * 透過指派以下專案來擷取轉換後的PDF檔案 `BLOB` 物件的 `MTOM` 位元組陣列的欄位。 位元組陣列代表轉換後的PDF檔案。 確保您使用 `BLOB` 物件，用作 `createPDF2` 方法。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表轉換PDF檔案之檔案位置的字串值。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將HTML檔案轉換為PDF檔案 {#converting-html-documents-to-pdf-documents}

本節說明如何使用產生PDFAPI，以程式設計方式將HTML檔案轉換為PDF檔案。

>[!NOTE]
>
>如需「產生PDF」服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

若要將HTML檔案轉換為PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立「產生PDF」使用者端。
1. 擷取HTML內容以轉換為PDF檔案。
1. 將HTML內容轉換為PDF檔案。
1. 擷取結果。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立產生PDF使用者端**

您必須先建立產生PDF服務使用者端，才能以程式設計方式執行產生PDF作業。 如果您使用Java API，請建立 `GeneratePdfServiceClient` 物件。 如果您使用Web服務API，請建立 `GeneratePDFServiceService`.

**擷取HTML內容以轉換為PDF檔案**

參考您要轉換成HTML檔案的PDF內容。 您可以參照HTML內容，例如HTML檔案或可使用URL存取的HTML內容。

**將HTML內容轉換為PDF檔案**

建立服務使用者端後，您可以叫用適當的PDF建立作業。 此操作需要有關要轉換的檔案的資訊，包括目標檔案的路徑。

**擷取結果**

將HTML內容轉換為PDF檔案後，您可以擷取結果並儲存PDF檔案。

**另请参阅**

[使用Java API將HTML內容轉換為PDF檔案](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[使用Web服務API將HTML內容轉換為PDF檔案](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速啟動](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將HTML內容轉換為PDF檔案 {#convert-html-content-to-a-pdf-document-using-the-java-api}

使用產生HTMLAPI (Java)將PDF檔案轉換為PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立「產生PDF」使用者端。

   建立 `GeneratePdfServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 擷取HTML內容以轉換為PDF檔案。

   建立字串變數並指派指向HTML內容的URL，以擷取HTML內容。

1. 將HTML內容轉換為PDF檔案。

   叫用 `GeneratePdfServiceClient` 物件的 `htmlToPDF2` 方法並傳遞下列值：

   * A `java.lang.String` 包含要轉換之HTML檔案URL的物件。
   * A `java.lang.String` 包含轉換中所要使用的檔案型別設定的物件。 檔案型別設定可包含漸層級。
   * A `java.lang.String` 包含要使用的安全性設定名稱的物件。
   * 選填 `com.adobe.idp.Document` 包含產生PDF檔案時要套用之設定的物件。 如果未提供此資訊，則會根據前三個引數自動選擇設定。
   * 選填 `com.adobe.idp.Document` 包含要套用至PDF檔案之中繼資料資訊的物件。

1. 擷取結果。

   此 `htmlToPDF2` 方法傳回 `HtmlToPdfResult` 包含所產生新PDF檔案的物件。 若要取得新建立的PDF檔案，請執行下列動作：

   * 叫用 `HtmlToPdfResult` 物件的 `getCreatedDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 從上一步建立的物件中擷取PDF檔案的方法。

**另请参阅**

[將HTML檔案轉換為PDF檔案](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[快速入門（SOAP模式）：使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將HTML內容轉換為PDF檔案 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

使用產生HTMLAPI （Web服務）將PDF內容轉換為PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立「產生PDF」使用者端。

   * 建立 `GeneratePDFServiceClient` 物件（使用其預設建構函式）。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `GeneratePDFServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取HTML內容以轉換為PDF檔案。

   建立字串變數並指派指向HTML內容的URL，以擷取HTML內容。

1. 將HTML內容轉換為PDF檔案。

   透過叫用「 」，將HTML內容轉換為PDF檔案 `GeneratePDFServiceService` 物件的 `HtmlToPDF2` 方法並傳遞下列值：

   * 包含要轉換之HTML內容的字串。
   * A `java.lang.String` 包含轉換中所要使用的檔案型別設定的物件。
   * 字串物件，包含要使用的安全性設定。
   * 選填 `BLOB` 包含產生PDF檔案時要套用之設定的物件。
   * 選填 `BLOB` 包含要套用至PDF檔案之中繼資料資訊的物件。
   * 型別的輸出引數 `BLOB` 由填入的 `CreatePDF2` 方法。 此 `CreatePDF2` 方法會以轉換後的檔案填入此物件。 （只有Web服務呼叫需要此引數值）。

1. 擷取結果。

   * 透過指派以下專案來擷取轉換後的PDF檔案 `BLOB` 物件的 `MTOM` 位元組陣列的欄位。 位元組陣列代表轉換後的PDF檔案。 確保您使用 `BLOB` 物件，用作 `HtmlToPDF2` 方法。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表轉換PDF檔案之檔案位置的字串值。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[將HTML檔案轉換為PDF檔案](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF檔案轉換為非影像格式 {#converting-pdf-documents-to-non-image-formats}

本節說明如何使用產生PDFJava API和Web服務API，以程式設計方式將PDF檔案轉換為RTF檔案（非影像格式的範例）。 其他非影像格式包括HTML、文字、DOC和EPS。 將PDF檔案轉換為RTF時，請確保PDF檔案不包含表單元素，例如提交按鈕。 不會轉換表單元素。

>[!NOTE]
>
>如需「產生PDF」服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

若要將PDF檔案轉換為任何支援的型別，請執行下列步驟：

1. 包含專案檔案。
1. 建立「產生PDF」使用者端。
1. 擷取要轉換的PDF檔案。
1. 轉換PDF檔案。
1. 儲存轉換後的檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立產生PDF使用者端**

您必須先建立產生PDF服務使用者端，才能以程式設計方式執行產生PDF作業。 如果您使用Java API，請建立 `GeneratePdfServiceClient` 物件。 如果您使用Web服務API，請建立 `GeneratePDFServiceService` 物件。

**擷取要轉換的PDF檔案**

擷取PDF檔案以轉換為非影像格式。

**轉換PDF檔案**

建立服務使用者端後，您可以叫用PDF匯出作業。 此操作需要有關要轉換的檔案的資訊，包括目標檔案的路徑。

**儲存轉換的檔案**

儲存轉換後的檔案。 例如，如果您將PDF檔案轉換為RTF檔案，請將轉換的檔案儲存為RTF檔案。

**另请参阅**

[使用Java API將PDF檔案轉換為RTF檔案](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[使用Web服務API將PDF檔案轉換為RTF檔案](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[產生PDF服務API快速啟動](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為RTF檔案 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

使用產生PDFAPI (Java)將PDF檔案轉換為RTF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-generatepdf-client.jar。

1. 建立「產生PDF」使用者端。

   建立 `GeneratePdfServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 擷取要轉換的PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，代表使用建構函式轉換的PDF檔案。 傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 轉換PDF檔案。

   叫用 `GeneratePdfServiceClient` 物件的 `exportPDF2` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 代表要轉換之PDF檔案的物件。
   * A `java.lang.String` 包含要轉換之檔案名稱的物件。
   * A `java.lang.String` 包含Adobe PDF設定名稱的物件。
   * A `ConvertPDFFormatType` 指定轉換目標檔案型別的物件。
   * 選填 `com.adobe.idp.Document` 包含產生PDF檔案時要套用之設定的物件。

   此 `exportPDF2` 方法傳回 `ExportPDFResult` 包含轉換檔案的物件。

1. 轉換PDF檔案。

   若要取得新建立的檔案，請執行下列動作：

   * 叫用 `ExportPDFResult` 物件的 `getConvertedDocument` 方法。 這會傳回 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 用於擷取新檔案的方法。

**另请参阅**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API將HTML內容轉換為PDF檔案](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將PDF檔案轉換為RTF檔案 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

使用產生PDFAPI （Web服務）將PDF檔案轉換為RTF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立「產生PDf」使用者端。

   * 建立 `GeneratePDFServiceClient` 物件（使用其預設建構函式）。
   * 建立 `GeneratePDFServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `GeneratePDFServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取要轉換的PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存已轉換的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派給其 `MTOM` 屬性位元組陣列的內容。

1. 轉換PDF檔案。

   叫用 `GeneratePDFServiceServiceWse` 物件的 `ExportPDF2` 方法並傳遞下列值：

   * A `BLOB` 代表要轉換之PDF檔案的物件。
   * 包含要轉換之檔案的路徑名稱的字串。
   * A `java.lang.String` 指定檔案位置的物件。
   * 字串物件，指定轉換的目標檔案型別。 指定 `RTF`.
   * 選填 `BLOB` 包含產生PDF檔案時要套用之設定的物件。
   * 型別的輸出引數 `BLOB` 由填入的 `ExportPDF2` 方法。 此 `ExportPDF2` 方法會以轉換後的檔案填入此物件。 （只有Web服務呼叫需要此引數值）。

1. 儲存轉換後的檔案。

   * 透過指派以下專案來擷取轉換後的RTF檔案： `BLOB` 物件的 `MTOM` 位元組陣列的欄位。 位元組陣列代表轉換的RTF檔案。 確保您使用 `BLOB` 物件，用作 `ExportPDF2` 方法。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表RTF檔案位置的字串值。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 新增對其他原生檔案格式的支援 {#adding-support-for-additional-native-file-formats}

本節說明如何新增對其他原生檔案格式的支援。 它提供「產生PDF」服務與此服務用來將原生檔案格式轉換為PDF的原生應用程式之間的互動概述。

本節也說明下列內容：

* 如何修改產生PDF服務提供給此產品已用來將原生檔案格式轉換為PDF的原生應用程式的回應
* 「產生PDF」服務、「產生PDF服務應用程式監視器」(AppMon)元件與原生應用程式(例如Microsoft Word)之間的互動
* XML文法在這些互動中所扮演的角色

### 元件互動 {#component-interactions}

「產生PDF」服務會呼叫與檔案格式相關聯的應用程式，然後與應用程式互動，使用預設印表機列印檔案，藉此轉換原生檔案格式。 預設印表機必須設定為Adobe PDF印表機。

此圖例顯示原生應用程式支援的相關元件和驅動程式。 它也提到了影響互動的XML語法。

原生檔案轉換的元件互動

本檔案使用術語 *原生應用程式* 表示用來產生原生檔案格式的應用程式，例如Microsoft Word。

*AppMon* 是企業元件，會以使用者導覽至該應用程式顯示的對話方塊的方式，與原生應用程式互動。 AppMon用來指示應用程式(例如Microsoft Word)開啟和列印檔案的XML文法涉及以下循序工作：

1. 選取「檔案」>「開啟」以開啟檔案
1. 確定出現「開啟」對話方塊；如果沒有，則處理錯誤
1. 在「檔案名稱」欄位中提供檔案名稱，然後按一下「開啟」按鈕
1. 確定檔案實際開啟
1. 選取「檔案」>「列印」以開啟「列印」對話方塊
1. 確定顯示列印對話方塊

AppMon使用標準Win32 API與協力廠商應用程式互動，以傳輸按鍵和滑鼠點按等UI事件，這有助於控制這些應用程式以從中產生PDF檔案。

由於這些Win32 API的限制，AppMon無法將這些UI事件傳送至某些特定型別的視窗，例如浮動選單列（可在某些應用程式如TextPad中找到）以及某些無法使用Win32 API擷取其內容的對話方塊。

透過視覺化方式可輕鬆識別浮動功能表列，但僅透過視覺化方式可能無法識別特殊對話方塊型別。 您需要協力廠商應用程式，例如Microsoft Spy++ (Microsoft Visual C++開發環境的一部分)或其同等的WinID (可從以下網址免費下載： [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID))來檢查對話方塊，以判斷AppMon是否能夠使用標準Win32 API與其互動。

如果WinID能夠擷取對話方塊內容（例如文字、子視窗、視窗類別ID等），則AppMon也能夠這樣做。

此表格列出列印原生檔案格式所使用的資訊型別。

<table>
 <thead>
  <tr>
   <th><p>資訊型別</p></th>
   <th><p>描述</p></th>
   <th><p>修改/建立與原生檔案相關的專案 </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>管理設定 </p></td>
   <td><p>包括PDF設定、安全性設定和檔案型別設定。 </p><p>檔案型別設定會將副檔名與對應的原生應用程式相關聯。 檔案型別設定也指定用於列印原生檔案的原生應用程式設定。 </p></td>
   <td><p>若要變更已支援原生應用程式的設定，系統管理員會在管理主控台中設定「檔案型別設定」。 </p><p>若要新增對新的原生檔案格式的支援，您必須手動編輯檔案。 (請參閱 <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">新增或修改對原生檔案格式的支援</a>.) </p></td>
  </tr>
  <tr>
   <td><p>脚本 </p></td>
   <td><p>指定「產生PDF」服務與原生應用程式之間的互動。 這類互動通常會引導應用程式將檔案列印至Adobe PDF驅動程式。 </p><p>指令碼包含指示，指示原生應用程式開啟特定對話方塊，並為這些對話方塊中的欄位和按鈕提供特定回應。 </p></td>
   <td><p>「產生PDF」服務包含所有支援原生應用程式的指令碼檔案。 您可以使用XML編輯應用程式來修改這些檔案。</p><p>若要新增對新的原生應用程式的支援，您必須建立新的指令碼檔案。 (請參閱 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">為原生應用程式建立或修改其他對話方塊XML檔案</a>.) </p></td>
  </tr>
  <tr>
   <td><p>一般對話方塊指示 </p></td>
   <td><p>指定如何回應多個應用程式通用的對話方塊。 這類對話方塊是由作業系統、輔助應用程式（例如PDFMaker）和驅動程式所產生。 </p><p>包含此資訊的檔案是appmon.global.en_US.xml。</p></td>
   <td><p>請勿修改此檔案。 </p></td>
  </tr>
  <tr>
   <td><p>應用程式專用對話方塊指示</p></td>
   <td><p>指定如何回應應用程式專用的對話方塊。 </p><p>包含此資訊的檔案為appmon。<i>'[appname]'</i>.dialog.<i>'[locale]'</i>.xml （例如appmon.word.en_US.xml）。</p></td>
   <td><p>請勿修改此檔案。 </p><p>若要新增新原生應用程式的對話方塊指示，請參閱 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">為原生應用程式建立或修改其他對話方塊XML檔案</a>.</p></td>
  </tr>
  <tr>
   <td><p>其他應用程式專屬對話方塊指示 </p></td>
   <td><p>指定覆寫和新增至應用程式特定對話方塊指示。 區段會提供這類資訊的範例。 </p><p>包含此資訊的檔案為appmon。<i>'[appname]'</i>.addition.<i>'[locale]'</i>.xml. 例如appmon.addition.en_US.xml。</p></td>
   <td><p>可以使用XML編輯應用程式來建立和修改此型別的檔案。 (請參閱 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">為原生應用程式建立或修改其他對話方塊XML檔案</a>.) </p><p><strong>重要</strong>：您必須針對伺服器將支援的每個原生應用程式，建立其他應用程式專用的對話方塊指示。 </p></td>
  </tr>
 </tbody>
</table>

### 關於指令碼和對話方塊XML檔案 {#about-the-script-and-dialog-xml-files}

指令碼XML檔案會指示產生PDF服務透過應用程式對話方塊進行瀏覽，其方式與使用者透過應用程式對話方塊進行瀏覽相同。 指令碼XML檔案也指示「產生PDF」服務透過執行如按按鈕、選取或取消選取核取方塊或選取功能表專案等動作來回應對話方塊。

相對地，對話方塊XML檔案只會以指令碼XML檔案中使用的相同動作型別來回應對話方塊。

#### 對話方塊和視窗元素術語 {#dialog-box-and-window-element-terminology}

本節和下一節會根據所說明的透視，對對話方塊及其包含的元件使用不同的術語。 對話方塊元件是按鈕、欄位和下拉式方塊等專案。

當本節和下一節從使用者的角度描述對話方塊及其元件時，例如 *對話方塊*， *按鈕*， *欄位*、和 *下拉式方塊* 已使用。

當本節和下一節從內部表示的角度描述對話方塊及其元件時，術語 *視窗元素* 已使用。 視窗元素的內部表示是階層，其中每個視窗元素例項都由標籤標識。 視窗元素例項也描述其實體特性和行為。

從使用者的角度來看，對話方塊及其元件會顯示不同的行為，其中某些對話方塊元素會隱藏直到啟動。 從內部表示的角度來看，不存在此類行為問題。 例如，對話方塊的內部表示看起來類似於它所包含的元件，但元件巢狀地置於對話方塊內除外。

本節說明為AppMon提供指示的XML元素。 這些元素的名稱如下 `dialog` 元素和 `window` 元素。 本檔案使用等寬字型來區分XML元素。 此 `dialog` element會識別XML指令碼檔案可能導致顯示（有意或無意地）的對話方塊。 此 `window` element可識別視窗元素（對話方塊或對話方塊的元件）。

#### 階層 {#hierarchy}

此圖表顯示指令碼和對話方塊XML的階層。 指令碼XML檔案符合script.xsd架構，其中包括（在XML意義上） window.xsd架構。 同樣地，對話方塊XML檔案符合dialog.xsd架構，其中也包含window.xsd架構。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

指令碼和對話方塊XML的階層

#### 指令碼XML檔案 {#script-xml-files}

A *指令碼XML檔案* 指定一系列步驟，指示原生應用程式瀏覽至特定視窗元素，然後提供這些元素的回應。 大多數回應是文字或按鍵，對應於使用者提供給對應對話方塊中的欄位、組合方塊或按鈕的輸入。

「產生PDF」服務支援指令碼XML檔案的目的是指示原生應用程式列印原生檔案。 不過，指令碼XML檔案可用於完成使用者在與原生應用程式的對話方塊互動時可執行的任何工作。

指令碼XML檔案中的步驟會依序執行，而不會產生任何分支機會。 唯一支援的條件式測試是逾時/重試，如果步驟在特定時段內以及特定重試次數後未成功完成，會導致指令碼終止。

除了循序的步驟外，步驟中的指示也會依序執行。 您必須確保步驟和指示反映使用者執行這些相同步驟的順序。

指令碼XML檔案中的每個步驟都會識別在步驟指示成功執行時預期出現的視窗元素。 如果在執行指令碼步驟時出現未預期的對話方塊，則產生PDF服務會依照下一節所述搜尋對話方塊XML檔案。

#### 對話方塊XML檔案 {#dialog-xml-files}

執行原生應用程式會顯示不同的對話方塊，無論原生應用程式處於可見還是不可見模式，都會顯示對話方塊。 對話方塊可由作業系統或應用程式本身產生。 當原生應用程式在產生PDF服務的控制下執行時，系統和原生應用程式對話方塊會顯示在隱藏的視窗中。

A *對話方塊XML檔案* 指定產生PDF服務如何回應系統或原生應用程式對話方塊。 對話方塊XML檔案允許「產生PDF」服務以有助於轉換過程的方式回應未提示的對話方塊。

當系統或原生應用程式顯示目前執行的指令碼XML檔案未處理的對話方塊時，產生PDF服務會依此順序搜尋對話方塊XML檔案，並在找到相符專案時停止：

* appmon。`[appname]`其他……`[locale]`.xml
* appmon。`[appname]`。`[locale]`.xml （請勿修改此檔案。）
* appmon.global.`[locale]`.xml （請勿修改此檔案。）

如果「產生PDF」服務找到對話方塊的相符專案，則會藉由傳送按鍵或針對對話方塊指定的其他動作來解除該專案。 如果對話方塊的指示指定了中止訊息，則產生PDF服務會終止目前執行的工作並產生錯誤訊息。 中止訊息會指定於 `abortMessage` 指令碼XML語法中的元素。

如果「產生PDF」服務遇到的對話方塊未在任何先前列出的檔案中說明，則「產生PDF」服務會將該對話方塊的註解合併到記錄檔案專案中。 目前執行的工作最終逾時。 然後，您可以使用記錄檔中的資訊來撰寫原生應用程式之其他對話方塊XML檔案中的新指示。

### 新增或修改對原生檔案格式的支援 {#adding-or-modifying-support-for-a-native-file-format}

本節說明支援其他原生檔案格式或修改已支援之原生檔案格式的支援所必須執行的工作。

您必須先完成下列工作，才能新增或修改支援。

#### 選擇用來識別視窗元素的工具 {#choosing-a-tool-for-identifying-window-elements}

對話方塊和指令碼XML檔案要求您識別對話方塊或指令碼元素所回應的視窗元素（對話方塊、欄位或其他對話方塊元件）。 例如，指令碼叫用原生應用程式的選單後，指令碼必須識別該選單上要套用按鍵或動作的視窗元素。

您可以透過對話方塊標題列中顯示的註解輕鬆識別對話方塊。 不過，您必須使用Microsoft Spy++之類的工具來識別較低層級的視窗元素。 較低層級的視窗元素可透過各種屬性來識別，這些屬性並不明顯。 此外，每個原生應用程式可能會以不同方式識別其視窗元素。 因此，有多種方式可識別視窗元素。 以下是考慮視窗元素識別的建議順序：

1. 註解本身（如果它是唯一的）
1. 控制項ID，對於指定的對話方塊來說，它可能是唯一的，也可能不是唯一的
1. 類別名稱，不一定是唯一的

您可以使用這三個屬性的任何一個或組合來識別視窗。

如果屬性無法識別註解，您可以改為使用相對於其父項的索引來識別視窗元素。 一個 *索引* 指定視窗元素相對於其同層級視窗元素的位置。 通常，索引是識別組合方塊的唯一方法。

請注意下列問題：

* Microsoft Spy++會使用&amp;符號來識別註解的熱鍵，以顯示註解。 例如，Spy++會將一個「列印」對話方塊的註解顯示為 `Pri&nt`，表示快速鍵為 *n*. 指令碼和對話方塊XML檔案中的註解標題必須省略&amp;符號。
* 部分註解包含分行符號。 「產生PDF」服務無法識別分行符號。 如果註解包含分行符號，請包含足夠的註解以與其他選單專案區分開來，然後對省略的零件使用規則運算式。 範例為( `^Long caption title$`)。 (請參閱 [在註解屬性中使用規則運算式](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* 使用字元實體（也稱為逸出序列）作為保留的XML字元。 例如，使用 `&` 對於&amp;符號， `<` 和 `>` 小於和大於符號， `&apos;` 單引號，和 `&quot;` （對於引號）。

如果您打算使用對話方塊或指令碼XML檔案，則應安裝應用程式Microsoft Spy++。

#### 取消封裝對話方塊和指令碼檔案 {#unpackaging-the-dialog-and-script-files}

對話方塊和指令碼檔案位於appmondata.jar檔案中。 您必須先取消封裝此JAR檔案，才能修改這些檔案中的任何一個或新增指令碼或對話方塊檔案。 例如，假設您想要新增對EditPlus應用程式的支援。 您可以建立兩個XML檔案，分別命名為appmon.editplus.script.en_US.xml和appmon.editplus.script.addition.en_US.xml。 這些XML指令碼必須新增至adobe-appmondata.jar檔案的兩個位置，如下所示：

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon。 adobe-livecycle-native-jboss-x86_win32.ear檔案位於匯出資料夾： `[AEM forms install directory]\configurationManager`. (如果將AEM Forms部署在其他J2EE應用程式伺服器上，請將adobe-livecycle-native-jboss-x86_win32.ear檔案取代為對應至您J2EE應用程式伺服器的EAR檔案。)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jar檔案位於adobe-generatepdf-dsc.jar檔案中）。 adobe-generatepdf-dsc.jar檔案位於 `[AEM forms install directory]\deploy` 資料夾。

將這些XML檔案新增至adobe-appmondata.jar檔案後，您必須重新部署GeneratePDF元件。 若要將對話方塊和指令碼XML檔案新增至adobe-appmondata.jar檔案，請執行下列工作：

1. 使用WinZip或WinRAR等工具，開啟adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar檔案。
1. 將對話方塊和指令碼XML檔案新增至appmondata.jar檔案，或修改此檔案中的現有XML檔案。 (請參閱 [建立或修改原生應用程式的指令碼XML檔案](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)和 [為原生應用程式建立或修改其他對話方塊XML檔案](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. 使用WinZip或WinRAR等工具，開啟adobe-generatepdf-dsc.jar > adobe-appmondata.jar。
1. 將對話方塊和指令碼XML檔案新增至appmondata.jar檔案，或修改此檔案中的現有XML檔案。 (請參閱 [建立或修改原生應用程式的指令碼XML檔案](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)和 [為原生應用程式建立或修改其他對話方塊XML檔案](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) 將XML檔案新增至adobe-appmondata.jar檔案後，請將新的adobe-appmondata.jar檔案置入adobe-generatepdf-dsc.jar檔案中。
1. 如果您新增其他原生檔案格式的支援，請建立提供應用程式路徑的系統環境變數(請參閱 [建立環境變數來尋找原生應用程式](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application).)

**重新部署GeneratePDF元件的方式**

1. 登入Workbench。
1. 選取 **視窗** > **顯示檢視** > **元件**. 此動作會將「元件」檢視新增至Workbench。
1. 以滑鼠右鍵按一下GeneratePDF元件，然後選取 **停止元件**.
1. 當元件停止時，按一下滑鼠右鍵並選取「解除安裝元件」來移除元件。
1. 以滑鼠右鍵按一下 **元件** 圖示並選取 **安裝元件**.
1. 瀏覽並選取修改過的adobe-generatepdf-dsc.jar檔案，然後按一下「開啟」。 請注意，GeneratePDF元件旁會出現一個紅色方塊。
1. 展開GeneratePDF元件，選取「服務描述元」，然後按一下滑鼠右鍵「產生PDF服務」並選取「啟動服務」。
1. 在出現的組態對話方塊中，輸入適用的組態值。 如果您將這些值留白，則會使用預設設定值。
1. 以滑鼠右鍵按一下「產生PDF」並選取「啟動元件」。
1. 展開Active Services。 如果服務名稱正在執行，其旁邊會顯示綠色箭頭。 否則，服務會處於停止狀態。
1. 如果服務處於停止狀態，請用滑鼠右鍵按一下服務名稱，然後選取啟動服務。

### 建立或修改原生應用程式的指令碼XML檔案 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

如果要將檔案導向新的原生應用程式，則必須為該應用程式建立指令碼XML檔案。 如果您要修改「產生PDF」服務與已支援的原生應用程式互動的方式，則必須修改該應用程式的指令碼。

指令碼包含瀏覽原生應用程式的視窗元素以及提供這些元素特定回應的指示。 包含此資訊的檔案是 `appmon.`[appname]&quot; `.script.`[地區設定]`.xml`. 例如appmon.notepad.script.en_US.xml。

#### 識別指令碼必須執行的步驟 {#identifying-steps-the-script-must-execute}

使用原生應用程式，決定您必須瀏覽的視窗元素，以及列印檔案時必須執行的每個回應。 請注意任何回應所產生的對話方塊。 這些步驟將類似於以下步驟：

1. 選取「檔案>開啟」。
1. 指定路徑，然後按一下「開啟」。
1. 在功能表列上選取「檔案」>「列印」。
1. 指定印表機所需的屬性。
1. 選取「列印」，並等待「另存新檔」對話方塊出現。 「產生PDF」服務需要「另存新檔」對話方塊才能指定PDF檔案的目的地。

#### 識別註解屬性中指定的對話方塊 {#identifying-the-dialogs-specified-in-caption-attributes}

使用Microsoft Spy++取得原生應用程式中視窗元素屬性的身分識別。 您必須具備這些身分才能撰寫指令碼。

#### 在註解屬性中使用規則運算式 {#using-regular-expressions-in-caption-attributes}

您可以在註解規格中使用規則運算式。 「產生PDF」服務會使用 `java.util.regex.Matcher` 類別以支援規則運算式。 該公用程式支援中所述的規則運算式 `java.util.regex.Pattern`.

**規則運算式，可容納記事本橫幅中記事本前端的檔案名稱**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**區分列印與列印設定的規則運算式**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### 排序視窗和windowList元素 {#ordering-the-window-and-windowlist-elements}

您必須訂購 `window` 和 `windowList` 元素如下所示：

* 當多個 `window` 元素會顯示為中的子項 `windowList` 或 `dialog` 元素，對其排序 `window` 元素以遞減順序排列，長度 `caption` 指示順序中位置的名稱。
* 當多個 `windowList` 元素會出現在 `window` 元素，對其排序 `windowList` 元素以遞減順序排列，長度 `caption` 第一個屬性 `indexes/`指示順序中位置的元素。

**排序對話方塊檔案中的視窗元素**

```xml
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**在windowList元素中排序視窗元素**

```xml
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### 為原生應用程式建立或修改其他對話方塊XML檔案 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

如果您為先前不支援的原生應用程式建立指令碼，您也必須為該應用程式建立額外的對話方塊XML檔案。 AppMon使用的每個原生應用程式只能有一個額外的對話方塊XML檔案。 即使沒有預期的未經請求的對話方塊，也需要其他對話方塊XML檔案。 其他對話方塊必須至少有一個 `window` 元素，即使是 `window` 元素只是預留位置。

>[!NOTE]
>
>在此上下文中，「附加」一詞指的是 `appmon.[applicationname].addition.[locale].xml` 檔案。 這類檔案會指定對話方塊XML檔案的覆寫和新增內容。

您也可以修改原生應用程式的其他對話方塊XML檔案，以達到下列目的：

* 覆寫具有不同回應的應用程式之對話方塊XML檔案
* 若要將回應新增至該應用程式的對話方塊XML檔案中未定址的對話方塊

識別其他dialogXML檔案的檔案名稱是 `appmon.[appname].addition.[locale].xml`. 例如appmon.excel.addition.en_US.xml。

其他對話方塊XML檔案的名稱必須使用格式 `appmon.[applicationname].addition.[locale].xml`，其中 *applicationname* 必須與XML組態檔和指令碼中使用的應用程式名稱完全相符。

>[!NOTE]
>
>native2pdfconfig.xml組態檔中指定的泛型應用程式都沒有主要對話方塊XML檔案。 區段 [新增或修改對原生檔案格式的支援](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) 說明這些規格。

您必須訂購 `windowList` 在中顯示為子項的元素 `window` 元素。 (請參閱 [排序視窗和windowList元素](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### 修改一般對話方塊XML檔案 {#modifying-the-general-dialog-xml-file}

您可以修改一般對話方塊XML檔案，以回應系統產生的對話方塊，或回應多個應用程式通用的對話方塊。

#### 在XML組態檔中新增檔案型別專案 {#adding-a-filetype-entry-in-the-xml-configuration-file}

此程式說明如何更新產生PDF服務組態檔，以將檔案型別與原生應用程式相關聯。 若要更新此組態檔，您必須使用管理主控台將組態資料匯出至檔案。 組態資料的預設檔案名稱為native2pdfconfig.xml。

**更新產生PDF服務組態檔**

1. 選取 **首頁** > **服務** > **Adobe PDF Generator** > **組態檔**，然後選取 **匯出設定**.
1. 修改 `filetype-settings` 元素（視需要）。
1. 選取 **首頁** > **服務** > **Adobe PDF Generator** >**組態檔**，然後選取 **匯入設定**. 組態資料會匯入產生PDF服務，取代先前的設定。

>[!NOTE]
>
>應用程式的名稱指定為 `GenericApp` 元素的 `name` 屬性。 此值必須與您為該應用程式開發的指令碼中指定的對應名稱完全相符。 同樣地， `GenericApp` 元素的 `displayName` 屬性應該完全符合對應的指令碼 `expectedWindow` 視窗註解。 在解析中出現的任何規則運算式後，會評估此類等同性 `displayName` 或 `caption` 屬性。

在此範例中，已修改產生PDF服務所提供的預設設定資料，以指定應使用Notepad (而非Microsoft Word)來處理副檔名為.txt的檔案。 在此修改之前，Microsoft Word被指定為應該處理此類檔案的原生應用程式。

**將文字檔導向至記事本(native2pdfconfig.xml)的修改**

```xml
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### 建立環境變數來尋找原生應用程式 {#creating-an-environment-variable-to-locate-the-native-application}

建立環境變數，指定原生應用程式可執行檔的位置。 變數必須使用格式 `[applicationname]_PATH`，其中 *applicationname* 必須與XML組態檔和指令碼中使用的應用程式名稱完全相符，而且路徑中包含以雙引號括住可執行檔的路徑。 此類環境變數的範例為 `Photoshop_PATH`.

建立新環境變數後，您必須重新啟動部署產生PDF服務的伺服器。

**在Windows XP環境中建立系統變數**

1. 選取 **「控制面板」>「系統」**.
1. 在「系統屬性」對話方塊中，按一下 **進階** 標籤，然後按一下 **環境變數**.
1. 在「環境變數」對話方塊的「系統變數」下，按一下 **新增**.
1. 在「新增系統變數」對話方塊的 **變數名稱** 方塊中，輸入使用格式的名稱 `[applicationname]_PATH`.
1. 在 **變數值** 方塊中，輸入應用程式可執行檔的完整路徑和檔案名稱，然後按一下 **確定**. 例如，輸入： `c:\windows\Notepad.exe`
1. 在「環境變數」對話方塊中，按一下 **確定**.

**從命令列建立系統變數**

1. 在命令列視窗中，使用此格式輸入變數定義：

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   例如，輸入： `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 啟動新的命令列提示，讓系統變數生效。

#### XML檔案 {#xml-files}

AEM Forms包含範例XML檔案，這些檔案會讓「產生PDF」服務使用「記事本」來處理任何副檔名為.txt的檔案。 此程式碼包含在本節中。 此外，您必須進行本節中說明的其他修改。

#### 其他對話方塊XML檔案 {#additional-dialog-xml-file}

此範例包含記事本應用程式的其他對話方塊。 除了產生PDF服務所指定的對話方塊之外，這些對話方塊也可以是其他對話方塊。

**記事本對話方塊(appmon.notepad.addition.en_US.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### 指令碼XML檔案 {#script-xml-file}

此範例指定「產生PDF」服務應如何與記事本互動，以使用Adobe PDF印表機列印檔案。

**Notepad指令碼XML檔案(appmon.notepad.script.en_US.xml)**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```
