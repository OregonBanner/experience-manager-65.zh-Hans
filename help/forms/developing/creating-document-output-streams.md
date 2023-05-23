---
title: 建立檔案輸出資料流
seo-title: Creating Document Output Streams
description: 使用Output服務將檔案轉換為PDF(包括PDF/A檔案)、PostScript、印表機控制語言(PCL)和Zebra - ZPL、Intermec - IPL、Datamax - DPL和TecToshiba - TPCL標籤格式。
seo-description: Use the Output service to convert documents as PDF (including PDF/A documents), PostScript, Printer Control Language (PCL), and Zebra - ZPL, Intermec - IPL, Datamax - DPL, and TecToshiba - TPCL label formats.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 0%

---

# 建立檔案輸出資料流  {#creating-document-output-streams}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於輸出服務**

「輸出」服務可讓您將檔案輸出為PDF(包括PDF/A檔案)、PostScript、印表機控制語言(PCL)和以下標籤格式：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用「輸出」服務，您可以將XML表單資料與表單設計合併，並將檔案輸出到網路印表機或檔案。

有兩種方式可以將表單設計（XDP檔案）傳遞到Output服務。 您可以傳遞 `com.adobe.idp.Document` 包含表單設計至Output服務的例項。 或者，您可以傳遞指定表單設計位置的URI值。 這兩種方法的討論位置如下： *使用AEM表單程式設計*.

>[!NOTE]
>
>Output服務不支援包含應用程式物件特定指令碼的AcroformPDF檔案。 包含應用程式物件特定指令碼的AcroformPDF檔案不會轉譯。

以下小節說明如何使用URI值將表單設計傳遞到Output服務：

* [建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents)

以下小節說明如何在中傳遞表單設計 `com.adobe.idp.Document` 例項：

* [將位於Content Services （已棄用）中的檔案傳遞至Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

決定使用哪種技術時，其中一個考量事項是您是否從其他AEM Forms服務取得表單設計，然後在內傳遞它 `com.adobe.idp.Document` 執行個體。 兩者皆有 *將檔案傳遞至Output Service* 和 *使用片段建立PDF檔案* 部分說明如何從其他AEM Forms服務取得表單設計。 第一節　從Content Services （已棄用）擷取表單設計。 第二區段會從Assembler服務擷取表單設計。

如果您從固定位置（例如檔案系統）取得表單設計，則可以使用任一技術。 也就是說，您可以指定XDP檔案的URI值或使用 `com.adobe.idp.Document` 執行個體。

若要傳遞在建立PDF檔案時指定表單設計位置的URI值，請使用 `generatePDFOutput` 方法。 同樣地，若要傳遞 `com.adobe.idp.Document` 建立PDF檔案時，執行Output服務的例項，使用 `generatePDFOutput2` 方法。

將輸出資料流傳送至網路印表機時，您也可以使用其中一種技術。 若要傳送輸出資料流至印表機，請傳遞 `com.adobe.idp.Document` 包含表單設計的例項，請使用 `sendToPrinter2`方法。 若要傳遞URI值以傳送輸出資料流至印表機，請使用 `sendToPrinter`方法。 此 *傳送列印資料流至印表機* 區段使用 `sendToPrinter` 方法。

您可以使用Output服務完成這些工作：

* [建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)
* [建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents)
* [將位於Content Services （已棄用）中的檔案傳遞至Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [列印至檔案](creating-document-output-streams.md#printing-to-files)
* [傳送列印資料流至印表機](creating-document-output-streams.md#sending-print-streams-to-printers)
* [建立多個輸出檔案](creating-document-output-streams.md#creating-multiple-output-files)
* [建立搜尋規則](creating-document-output-streams.md#creating-search-rules)
* [平面化PDF檔案](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 建立PDF檔案 {#creating-pdf-documents}

您可以使用Output服務來建立以您提供的表單設計和XML表單資料為基礎的PDF檔案。 Output服務建立的PDF檔案不是互動式PDF檔案；使用者無法輸入或修改表單資料。

如果要建立用於長期儲存的PDF檔案，建議您建立PDF/A檔案。 (請參閱 [建立PDF/A檔案](creating-document-output-streams.md#creating-pdf-a-documents).)

若要建立可讓使用者輸入資料的互動式PDF表單，請使用Forms服務。 (請參閱 [呈現互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要建立PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參照XML資料來源。
1. 設定PDF執行階段選項。
1. 設定演算執行階段選項。
1. 產生PDF檔案。
1. 擷取作業的結果。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立 `OutputClient` 物件。 如果您使用輸出Web服務API，請建立 `OutputServiceService` 物件。

**參考XML資料來源**

若要將資料與表單設計合併，您必須參照包含資料的XML資料來源。 您計畫填入資料的每個表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

請考量下列範例貸款申請表。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

若要將資料合併至此表單設計，您必須建立與表單相對應的XML資料來源。 下列XML代表與範例抵押應用程式表單對應的XDP XML資料來源。

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

**設定PDF執行階段選項**

建立PDF檔案時設定檔案URI選項。 此選項會指定Output服務產生的PDF檔案的名稱和位置。

>[!NOTE]
>
>除了設定檔案URI執行階段選項之外，您還可以以程式設計方式從輸出服務傳回的複雜資料型別中擷取PDF檔案。 不過，透過設定檔案URI執行階段選項，您不需要建立以程式擷取PDF檔案的應用程式邏輯。

**設定演算執行階段選項**

建立PDF檔案時，您可以設定演算執行階段選項。 雖然這些選項並非必要(不同於必要的PDF執行階段選項)，但您可以執行工作，例如改善Output服務的效能。 例如，您可以快取Output服務使用的表單設計以提高其效能。

如果您使用已標籤的Acrobat表單作為輸入，則無法使用輸出服務Java或Web服務API來關閉已標籤的設定。 如果您嘗試以程式設計方式將此選項設為 `false`，仍會標籤結果PDF檔案。

>[!NOTE]
>
>如果您未指定演算執行階段選項，則會使用預設值。 如需有關演算執行階段選項的資訊，請參閱 `RenderOptionsSpec` 類別參考。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**產生PDF檔案**

在參照包含表單資料的有效XML資料來源並設定執行階段選項後，您可以叫用Output服務，這會產生一個PDF檔案。

產生PDF檔案時，您可以指定Output服務建立PDF檔案所需的URI值。 表單設計可儲存在伺服器檔案系統等位置或作為AEM Forms應用程式的一部分。 若表單設計（或其他資源，例如影像檔案）屬於Forms應用程式的一部分，則可使用內容根URI值加以參照 `repository:///`. 例如，考慮以下名為的表單設計 *Loan.xdp* 位在名為的Forms應用程式中 *應用程式/表單應用程式*：

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

若要存取上圖所示的Loan.xdp檔案，請指定 `repository:///Applications/FormsApplication/1.0/FormsFolder/` 作為第三個引數傳遞至 `OutputClient` 物件的 `generatePDFOutput` 方法。 指定表單名稱(*Loan.xdp*)作為第二個引數傳遞至 `OutputClient` 物件的 `generatePDFOutput` 方法。

如果XDP檔案包含影像（或其他資源，例如片段），請將資源放在與XDP檔案相同的應用程式資料夾中。 AEM Forms使用內容根URI作為基本路徑，以解析對影像的參照。 例如，如果Loan.xdp檔案包含影像，請確定您將該影像放在 `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>叫用時，您可以參考Forms應用程式URI `OutputClient` 物件的 `generatePDFOutput` 或 `generatePrintedOutput` 方法。

>[!NOTE]
>
>若要檢視透過參考Forms應用程式中的XDP來建立PDF檔案的完整快速入門，請參閱 [快速入門（EJB模式）：使用Java API根據應用程式XDP檔案建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**擷取作業的結果**

Output服務執行作業之後，會傳回各種資料專案，例如指定作業是否成功的狀態XML資料。

**另请参阅**

[使用Java API建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[使用Web服務API建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立PDF檔案 {#create-a-pdf-document-using-the-java-api}

使用Output API (Java)建立PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參照XML資料來源。

   * 建立 `java.io.FileInputStream` 物件，代表使用建構函式並傳遞指定XML檔案位置的字串值來填入PDF檔案的XML資料來源。
   * 建立 `com.adobe.idp.Document` 物件（使用其建構函式）。 傳遞 `java.io.FileInputStream` 物件。

1. 設定PDF執行階段選項。

   * 建立 `PDFOutputOptionsSpec` 物件（使用其建構函式）。
   * 透過叫用 `PDFOutputOptionsSpec` 物件的 `setFileURI` 方法。 傳遞字串值，指定輸出服務產生的PDF檔案位置。 檔案URI選項是相對於裝載AEM Forms的J2EE應用程式伺服器，而不是使用者端電腦。

1. 設定演算執行階段選項。

   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。
   * 快取表單設計以透過叫用 `RenderOptionsSpec` 物件的 `setCacheEnabled` 和傳遞 `true`.

   >[!NOTE]
   >
   >您無法使用設定PDF檔案的版本 `RenderOptionsSpec` 物件的 `setPdfVersion` 方法：輸入檔案是Acrobat表單(在Acrobat中建立的表單)或已簽署或認證的XFA檔案。 輸出PDF檔案會保留原始PDF版本。 Adobe PDF同樣地，您無法透過叫用 `RenderOptionsSpec` 物件的 `setTaggedPDF` 方法(如果輸入檔案是Acrobat表單或已簽署或已認證的XFA檔案)。

   >[!NOTE]
   >
   >您無法透過以下方式設定線性PDF選項： `RenderOptionsSpec` 物件的 `setLinearizedPDF` 方法(如果輸入PDF檔案經過認證或數位簽署)。 (請參閱 [數位簽署PDF檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. 產生PDF檔案。

   透過叫用建立PDF檔案 `OutputClient` 物件的 `generatePDFOutput` 並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `com.adobe.idp.Document` 包含要與表單設計合併之資料之XML資料來源的物件。

   此 `generatePDFOutput` 方法傳回 `OutputResult` 包含作業結果的物件。

   >[!NOTE]
   >
   >PDF當透過叫用 `generatePDFOutput` 方法，請注意，您無法將資料與已簽署或認證的XFAPDF表單合併。 (請參閱 [數位簽署和認證檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >此 `OutputResult` 物件的 `getRecordLevelMetaDataList` 方法傳回 `null`*.*

   >[!NOTE]
   >
   >PDF您也可以透過叫用 `OutputClient` 物件的 `generatePDFOutput2` 方法。 (請參閱 [將位於Content Services （已棄用）中的檔案傳遞至Output Service ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 擷取作業的結果。

   * 擷取 `com.adobe.idp.Document` 代表「 」狀態的物件 `generatePDFOutput` 操作方式：叫用 `OutputResult` 物件的 `getStatusDoc` 方法。 此方法會傳回指定作業是否成功的狀態XML資料。
   * 建立 `java.io.File` 包含作業結果的物件。 確認副檔名為.xml。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件放入檔案(請確定您使用 `com.adobe.idp.Document` 物件，由 `getStatusDoc` 方法)。

   雖然Output服務會將PDF檔案寫入傳遞至的引數所指定的位置 `PDFOutputOptionsSpec` 物件的 `setFileURI` PDF方法，您可以透過叫用 `OutputResult` 物件的 `getGeneratedDoc` 方法。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立PDF檔案 {#create-a-pdf-document-using-the-web-service-api}

使用Output API （Web服務）建立PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參照XML資料來源。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存將與PDF檔案合併的XML資料。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表包含表單資料之XML檔案的檔案位置的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 設定PDF執行階段選項

   * 建立 `PDFOutputOptionsSpec` 物件（使用其建構函式）。
   * 透過指派字串值來設定檔案URI選項，該字串值指定輸出服務產生的PDF檔案的位置 `PDFOutputOptionsSpec` 物件的 `fileURI` 資料成員。 檔案URI選項是相對於裝載AEM Forms的J2EE應用程式伺服器，而不是使用者端電腦。

1. 設定演算執行階段選項。

   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。
   * 快取表單設計以指派值來改善Output服務的效能 `true` 至 `RenderOptionsSpec` 物件的 `cacheEnabled` 資料成員。

   >[!NOTE]
   >
   >您無法使用設定PDF檔案的版本 `RenderOptionsSpec` 物件的 `setPdfVersion` 方法：輸入檔案是Acrobat表單(在Acrobat中建立的表單)或已簽署或認證的XFA檔案。 輸出PDF檔案會保留原始PDF版本。 Adobe PDF同樣地，您無法透過叫用 `RenderOptionsSpec` 物件的 `setTaggedPDF`*方法(如果輸入檔案是Acrobat表單或已簽署或已認證的XFA檔案)。*

   >[!NOTE]
   >
   >您無法透過以下方式設定線性PDF選項： `RenderOptionsSpec` 物件的 `linearizedPDF` 如果輸入PDF檔案經過認證或數位簽署，則為成員。 (請參閱 [數位簽署PDF檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. 產生PDF檔案。

   透過叫用建立PDF檔案 `OutputServiceService` 物件的 `generatePDFOutput`並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `BLOB` 包含要與表單設計合併之資料之XML資料來源的物件。
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會使用產生的描述檔案的中繼資料填入此物件。 （只有Web服務呼叫需要此引數值）。
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會將結果資料填入此物件中。 （只有Web服務呼叫需要此引數值）。
   * 一個 `OutputResult` 包含作業結果的物件。 （只有Web服務呼叫需要此引數值）。

   >[!NOTE]
   >
   >PDF當透過叫用 `generatePDFOutput` 方法，請注意，您無法將資料與已簽署或認證的XFAPDF表單合併。 (請參閱 [數位簽署和認證檔案&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >PDF您也可以透過叫用 `OutputClient` 物件的 `generatePDFOutput2` 方法。 (請參閱 [將位於Content Services （已棄用）中的檔案傳遞至Output Service ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 擷取作業的結果。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確認副檔名為.xml。
   * 建立位元組陣列，儲存 `BLOB` 填入結果資料的物件 `OutputServiceService` 物件的 `generatePDFOutput` 方法（第八個引數）。 透過取得 `BLOB` 物件的 `MTOM` `field`.
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

   另请参阅

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >此 `OutputServiceService` 物件的 `generateOutput` 方法已過時。

## 建立PDF/A檔案 {#creating-pdf-a-documents}

您可以使用Output服務來建立PDF/A檔案。 由於PDF/A是用於長期儲存檔案內容的封存格式，因此所有字型都會嵌入，且檔案會解壓縮。 因此，PDF/A 文档通常比标准 PDF 文档大。此外，PDF/檔案不包含音訊和視訊內容。 如同其他Output服務工作，您提供表單設計和資料以與表單設計合併，以建立PDF/A檔案。

PDF/A-1規格包含兩個一致性層級，即a和b。兩者之間的主要差異在於邏輯結構（協助工具）支援，這是符合性層級b所不需要的。無論一致性等級為何，PDF/A-1會指定所有字型都內嵌在產生的PDF/A檔案中。

雖然PDF/A是封存PDF檔案的標準，但如果標準PDF檔案符合貴公司的需求，則不強制使用PDF/A進行封存。 PDF/A標準的目的是建立可長期儲存的PDF檔案，並符合檔案儲存要求。 例如，URL無法內嵌於PDF/A中，因為隨著時間推移，URL可能會變得無效。

您的組織必須評估其自身需求、您打算保留檔案的時間長度、檔案大小考量，並決定您自己的封存策略。 您可以使用DocConverter服務，以程式設計方式判斷PDF檔案是否符合PDF/A規範。 (請參閱 [以程式設計方式決定PDF/合規性](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

PDF/A檔案必須使用在表單設計中指定的字型，且字型不能被取代。 因此，如果PDF檔案內的字型在主機作業系統(OS)上無法使用，則會發生例外狀況。

在Acrobat中開啟PDF/A檔案時，會顯示一則訊息，確認檔案為PDF/A檔案，如下圖所示。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM網站有一個PDF/常見問題集區段，您可以在此存取 [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_65).

### 步驟摘要 {#summary_of_steps-1}

若要建立PDF/A檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參照XML資料來源。
1. 設定PDF/執行階段選項。
1. 設定演算執行階段選項。
1. 產生PDF/檔案。
1. 擷取作業的結果。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立自訂應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立 `OutputClient` 物件。 如果您使用輸出Web服務API，請建立 `OutputServiceService` 物件。

**參考XML資料來源**

若要將資料與表單設計合併，您必須參照包含資料的XML資料來源。 每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

**設定PDF/執行階段選項**

建立PDF/A檔案時，您可以設定「檔案URI」選項。 URI是相對於裝載AEM Forms的J2EE應用程式伺服器。 也就是說，如果您設定C:\Adobe，檔案會寫入伺服器上的資料夾，而非使用者端電腦。 URI會指定輸出服務產生的PDF/A檔案的名稱和位置。

**設定演算執行階段選項**

建立PDF/A檔案時，您可以設定演算執行階段選項。 您可以設定的兩個PDF/A相關選項為 `PDFAConformance` 和 `PDFARevisionNumber` 值。 此 `PDFAConformance` 值是指PDF檔案如何遵循指定如何保留長期電子檔案的要求。 此選項的有效值為 `A` 和 `B`. 如需有關層級a和b相容性的資訊，請參閱標題為PDF/A-1 ISO規格 *ISO 19005-1檔案管理*.

此 `PDFARevisionNumber` 值是指PDF/A檔案的修訂版本編號。 如需PDF/A檔案修訂版本的資訊，請參閱標題為PDF/A-1 ISO規格 *ISO 19005-1檔案管理*.

>[!NOTE]
>
>您無法將標籤的Adobe PDF選項設為 `false` 建立PDF/A 1A檔案時。 PDF/A 1A將永遠是標籤的PDF檔案。 此外，您無法將標籤的Adobe PDF選項設為 `true` 建立PDF/A 1B檔案時。 PDF/A 1B將永遠是未標籤的PDF檔案。

**產生PDF/檔案**

在您參照包含表單資料的有效XML資料來源並設定執行階段選項後，可以叫用Output服務，使其產生PDF/A檔案。

**擷取作業的結果**

Output服務執行作業之後，會傳回各種資料專案，例如XML資料，指定作業是否成功。

**另请参阅**

[使用Java API建立PDF/檔案](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[使用Web服務API建立PDF/檔案](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立PDF/檔案 {#create-a-pdf-a-document-using-the-java-api}

使用Output API (Java)建立PDF/檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參照XML資料來源。

   * 建立 `java.io.FileInputStream` 物件，代表使用建構函式並傳遞指定XML檔案位置的字串值來填入PDF/A檔案的XML資料來源。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定PDF/執行階段選項。

   * 建立 `PDFOutputOptionsSpec` 物件（使用其建構函式）。
   * 透過叫用 `PDFOutputOptionsSpec` 物件的 `setFileURI` 方法。 傳遞字串值，指定輸出服務產生的PDF檔案位置。 檔案URI選項是相對於裝載AEM Forms的J2EE應用程式伺服器，而不是使用者端電腦。

1. 設定演算執行階段選項。

   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。
   * 設定 `PDFAConformance` 值(透過叫用 `RenderOptionsSpec` 物件的 `setPDFAConformance` 方法和傳遞 `PDFAConformance` 指定一致性層級的列舉值。 例如，若要指定一致性層級A，請通過 `PDFAConformance.A`.
   * 設定 `PDFARevisionNumber` 值(透過叫用 `RenderOptionsSpec` 物件的 `setPDFARevisionNumber` 方法與傳遞 `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >PDF/A檔案的PDF版本是1.4，無論您為哪個值指定 `RenderOptionsSpec` 物件的 `setPdfVersion`*方法。*

1. 產生PDF/檔案。

   透過叫用建立PDF/檔案 `OutputClient` 物件的 `generatePDFOutput` 並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF/A檔案，請指定 `TransformationFormat.PDFA`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `com.adobe.idp.Document` 包含要與表單設計合併之資料之XML資料來源的物件。

   此 `generatePDFOutput` 方法傳回 `OutputResult` 包含作業結果的物件。

   >[!NOTE]
   >
   >此 `OutputResult` 物件的 `getRecordLevelMetaDataList` 方法傳回 `null`.

   >[!NOTE]
   >
   >PDF您也可以叫用 `OutputClient` 物件的 `generatePDFOutput`2個方法。 (請參閱 [將位於Content Services （已棄用）中的檔案傳遞至Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 擷取作業的結果。

   * 建立 `com.adobe.idp.Document` 代表「 」狀態的物件 `generatePDFOutput` 方法，方法是叫用 `OutputResult` 物件的 `getStatusDoc` 方法。
   * 建立 `java.io.File` 將包含作業結果的物件。 確認副檔名為.xml。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件放入檔案(請確定您使用 `com.adobe.idp.Document` 物件，由 `getStatusDoc` 方法)。

   >[!NOTE]
   >
   >雖然Output服務會將PDF/A檔案寫入傳遞至的引數所指定的位置 `PDFOutputOptionsSpec` 物件的 `setFileURI` PDF方法，您可以透過叫用 `OutputResult` 物件的 `getGeneratedDoc` 方法。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API建立PDF/檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 使用Web服務API建立PDF/檔案 {#create-a-pdf-a-document-using-the-web-service-api}

使用Output API （Web服務）建立PDF/A檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參照XML資料來源。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存將與PDF/A檔案合併的資料。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表要加密之PDF檔案的檔案位置，以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 設定PDF/執行階段選項。

   * 建立 `PDFOutputOptionsSpec` 物件（使用其建構函式）。
   * 透過指派字串值來設定檔案URI選項，該字串值指定輸出服務產生的PDF檔案的位置 `PDFOutputOptionsSpec` 物件的 `fileURI` 資料成員。 檔案URI選項是相對於主控AEM Forms的J2EE應用程式伺服器，而不是使用者端電腦

1. 設定演算執行階段選項。

   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。
   * 設定 `PDFAConformance` 值（透過指派） `PDFAConformance` 列舉值至 `RenderOptionsSpec` 物件的 `PDFAConformance` 資料成員。 例如，若要指定一致性層級A，請指派 `PDFAConformance.A` 至此資料成員。
   * 設定 `PDFARevisionNumber` 值（透過指派） `PDFARevisionNumber` 列舉值至 `RenderOptionsSpec` 物件的 `PDFARevisionNumber` 資料成員。 指派 `PDFARevisionNumber.Revision_1` 至此資料成員。

   >[!NOTE]
   >
   >PDF/A檔案的PDF版本是1.4，無論您指定哪個值。

1. 產生PDF/檔案。

   透過叫用建立PDF檔案 `OutputServiceService` 物件的 `generatePDFOutput`並傳遞下列值：

   * TransformationFormat列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDFA`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `BLOB` 包含要與表單設計合併之資料之XML資料來源的物件。
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會使用產生的描述檔案的中繼資料填入此物件。 （只有Web服務呼叫需要此引數值。）
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會將結果資料填入此物件中。 （只有Web服務呼叫需要此引數值。）
   * 一個 `OutputResult` 包含作業結果的物件。 （只有Web服務呼叫需要此引數值。）

   >[!NOTE]
   >
   >PDF您也可以叫用 `OutputClient` 物件的 `generatePDFOutput`2個方法。 (請參閱 [將位於Content Services （已棄用）中的檔案傳遞至Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 擷取作業的結果。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確認副檔名為.xml。
   * 建立位元組陣列，儲存 `BLOB` 填入結果資料的物件 `OutputServiceService` 物件的 `generatePDFOutput` 方法（第八個引數）。 透過取得 `BLOB` 物件的 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將位於Content Services （已棄用）中的檔案傳遞至Output Service {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Output服務會根據通常儲存為XDP檔案並在Designer中建立的表單設計來轉譯非互動式PDF表單。 您可以傳遞 `com.adobe.idp.Document` 包含表單設計至Output服務的物件。 然後Output服務會轉譯位於 `com.adobe.idp.Document` 物件。

傳遞的優點 `com.adobe.idp.Document` object to the Output service是其他AEM Forms服務作業會傳回 `com.adobe.idp.Document` 執行個體。 也就是說，您可以取得 `com.adobe.idp.Document` 執行個體，並加以轉譯。 例如，假設XDP檔案儲存在名為的內容服務（已棄用）節點中 `/Company Home/Form Designs`，如下圖所示。

您可以程式設計方式從內容服務（已棄用）擷取Loan.xdp，並將XDP檔案傳遞至中的輸出服務 `com.adobe.idp.Document` 物件。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

若要將從Content Services （已棄用）取得的檔案傳遞至Output服務，請執行下列工作：

1. 包含專案檔案。
1. 建立輸出和Document Management使用者端API物件。
1. 從內容服務擷取表單設計（已棄用）。
1. 演算非互動式PDF表單。
1. 使用資料串流執行動作。

**包含專案檔案**

將必要的檔案納入您的開發專案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立輸出和Document Management使用者端API物件**

以程式設計方式執行輸出服務API操作之前，請先建立輸出使用者端API物件。 此外，由於此工作流程會從內容服務中擷取XDP檔案（已棄用），請建立檔案管理API物件。

**從內容服務擷取表單設計（已棄用）**

使用Java或Web服務API從內容服務擷取XDP檔案（已棄用）。 XDP檔案會傳回 `com.adobe.idp.Document` 執行個體(或 `BLOB` 例項（若您使用網站服務）。 然後，您可以傳遞 `com.adobe.idp.Document` 執行個體到輸出服務。

**演算非互動式PDF表單**

若要呈現非互動式表單，請傳遞 `com.adobe.idp.Document` 從Content Services （已棄用）傳回至輸出服務的例項。

>[!NOTE]
>
>兩個命名的新方法 `generatePDFOutput2`和g `eneratePrintedOutput2`接受 `com.adobe.idp.Document` 包含表單設計的物件。 您也可以傳遞 `com.adobe.idp.Document`將列印資料流傳送至網路印表機時，包含輸出服務的表單設計。

**使用表單資料流執行動作**

您可以將非互動式表單儲存為PDF檔案。 此表單可在Adobe Reader或Acrobat中檢視。

**另请参阅**

[使用Java API將檔案傳遞到Output Service](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[使用Web服務API將檔案傳遞到Output Service](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[使用片段建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### 使用Java API將檔案傳遞到Output Service {#pass-documents-to-the-output-service-using-the-java-api}

使用輸出服務和內容服務（已棄用） API (Java)傳遞從內容服務（已棄用）擷取的檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar和adobe-contentservices-client.jar。

1. 建立輸出和Document Management使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。 (請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。
   * 建立 `DocumentManagementServiceClientImpl` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 從內容服務擷取表單設計（已棄用）。

   叫用 `DocumentManagementServiceClientImpl` 物件的 `retrieveContent` 方法並傳遞下列值：

   * 字串值，指定新增內容的存放區。 預設存放區為 `SpacesStore`. 此值為必要引數。
   * 字串值，指定要擷取之內容的完整路徑(例如 `/Company Home/Form Designs/Loan.xdp`)。 此值為必要引數。
   * 字串值，指定版本。 此值是選用引數，您可以傳遞空字串。 在此情況下，會擷取最新版本。

   此 `retrieveContent` 方法傳回 `CRCResult` 包含XDP檔案的物件。 擷取 `com.adobe.idp.Document` 執行個體(透過叫用 `CRCResult` 物件的 `getDocument` 方法。

1. 演算非互動式PDF表單。

   叫用 `OutputClient` 物件的 `generatePDFOutput2` 方法並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定影像等其他資源所在的內容根。
   * A `com.adobe.idp.Document` 代表表單設計的物件(使用 `CRCResult` 物件的 `getDocument` 方法)。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `com.adobe.idp.Document` 包含要與表單設計合併之資料之XML資料來源的物件。

   此 `generatePDFOutput2` 方法傳回 `OutputResult` 包含作業結果的物件。

1. 使用表單資料流執行動作。

   * 擷取 `com.adobe.idp.Document` 代表非互動式表單的物件。 `OutputResult` 物件的 `getGeneratedDoc` 方法。
   * 建立 `java.io.File` 包含作業結果的物件。 確認副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件放入檔案(請確定您使用 `com.adobe.idp.Document` 物件，由 `getGeneratedDoc` 方法)。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API將檔案傳遞到「輸出服務」](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[快速入門（SOAP模式）：使用Java API將檔案傳遞至輸出服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API將檔案傳遞到Output Service {#pass-documents-to-the-output-service-using-the-web-service-api}

使用輸出服務和內容服務（已棄用） API （網頁服務），傳遞從內容服務（已棄用）擷取的檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 由於此使用者端應用程式會叫用兩個AEM Forms服務，請建立兩個服務參考。 對與Output服務相關聯的服務參考使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   使用下列WSDL定義作為與Document Management服務相關聯的服務參考： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   因為 `BLOB` 資料型別對兩個服務參考都是通用的，完全限定 `BLOB` 使用時的資料型別。 在對應的Web服務快速入門中，全部 `BLOB` 執行個體已完整合格。

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出和Document Management使用者端API物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >對重複這些步驟 `DocumentManagementServiceClient`服務使用者端。

1. 從內容服務擷取表單設計（已棄用）。

   透過叫用擷取內容 `DocumentManagementServiceClient` 物件的 `retrieveContent` 並傳遞下列值：

   * 字串值，指定新增內容的存放區。 預設存放區為 `SpacesStore`. 此值為必要引數。
   * 字串值，指定要擷取之內容的完整路徑(例如 `/Company Home/Form Designs/Loan.xdp`)。 此值為必要引數。
   * 字串值，指定版本。 此值是選用引數，您可以傳遞空字串。 在此情況下，會擷取最新版本。
   * 儲存瀏覽連結值的字串輸出引數。
   * A `BLOB` 儲存內容的輸出引數。 您可以使用此輸出引數來擷取內容。
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 儲存內容屬性的輸出引數。
   * A `CRCResult` 輸出引數。 除了使用此物件外，您還可以使用 `BLOB` 擷取內容的輸出引數。

1. 演算非互動式PDF表單。

   叫用 `OutputServiceClient` 物件的 `generatePDFOutput2` 方法並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定影像等其他資源所在的內容根。
   * A `BLOB` 代表表單設計的物件(使用 `BLOB` 內容服務傳回的例項（已棄用）。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `BLOB` 包含要與表單設計合併之資料之XML資料來源的物件。
   * 輸出 `BLOB` 由填入的物件 `generatePDFOutput2` 方法。 此 `generatePDFOutput2` 方法會使用產生的描述檔案的中繼資料填入此物件。 （只有Web服務呼叫需要此引數值）。
   * 輸出 `OutputResult` 包含作業結果的物件。 （只有Web服務呼叫需要此引數值）。

   此 `generatePDFOutput2` 方法傳回 `BLOB` 包含非互動式PDF表單的物件。

1. 使用表單資料流執行動作。

   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，該值代表互動式PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，儲存 `BLOB` 物件擷取自 `generatePDFOutput2` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 將存放庫中的檔案傳遞至輸出服務 {#passing-documents-located-in-the-repository-to-the-output-service}

Output服務會根據通常儲存為XDP檔案並在Designer中建立的表單設計來轉譯非互動式PDF表單。 您可以傳遞 `com.adobe.idp.Document` 包含表單設計至Output服務的物件。 然後Output服務會轉譯位於 `com.adobe.idp.Document` 物件。

傳遞的優點 `com.adobe.idp.Document` object to the Output service是其他AEM Forms服務作業會傳回 `com.adobe.idp.Document` 執行個體。 也就是說，您可以取得 `com.adobe.idp.Document` 執行個體，並加以轉譯。 例如，假設XDP檔案儲存在AEM Forms存放庫中，如下圖所示。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

此 *FormsFolder* 資料夾是AEM Forms存放庫中的使用者定義位置（此位置為範例，預設不存在）。 在此範例中，名為Loan.xdp的表單設計位於此資料夾中。 除了表單設計之外，其他表單附屬資料（例如影像）也可以儲存在此位置。 位於AEM Forms存放庫中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

您可以利用程式設計方式從AEM Forms存放庫擷取Loan.xdp，並將其傳遞至內的輸出服務。 `com.adobe.idp.Document` 物件。

您可以使用兩種方式之一，根據存放庫中的XDP檔案建立PDF。 您可以參考傳遞XDP位置，或以程式設計方式從存放庫擷取XDP，並將其傳遞到XDP檔案中的輸出服務。

[快速入門（EJB模式）：使用Java API根據應用程式XDP檔案建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （顯示如何透過參考傳遞XDP檔案的位置）。

[快速入門（EJB模式）：使用Java API將位於AEM Forms儲存庫中的檔案傳遞到Output服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (說明如何以程式設計方式從AEM Forms存放庫擷取XDP檔案，並將其傳遞至內的輸出服務) `com.adobe.idp.Document` 執行個體)。 （本節討論如何執行此工作）

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-3}

若要將從AEM Forms存放庫取得的檔案傳遞至輸出服務，請執行下列工作：

1. 包含專案檔案。
1. 建立輸出和Document Management使用者端API物件。
1. 從AEM Forms存放庫擷取表單設計。
1. 演算非互動式PDF表單。
1. 使用資料串流執行動作。

**包含專案檔案**

將必要的檔案納入您的開發專案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立輸出和Document Management使用者端API物件**

以程式設計方式執行輸出服務API操作之前，請先建立輸出使用者端API物件。 此外，由於此工作流程會從內容服務中擷取XDP檔案（已棄用），請建立檔案管理API物件。

**從AEM Forms存放庫擷取表單設計**

使用存放庫API從AEM Forms存放庫擷取XDP檔案。 (請參閱 [正在讀取資源](/help/forms/developing/aem-forms-repository.md#reading-resources).)

XDP檔案會傳回 `com.adobe.idp.Document` 執行個體(或 `BLOB` 例項（若您使用網站服務）。 然後，您可以傳遞 `com.adobe.idp.Document` Output服務的例項。

**演算非互動式PDF表單**

若要呈現非互動式表單，請傳遞 `com.adobe.idp.Document` 使用AEM Forms Repository API傳回的執行個體。

>[!NOTE]
>
>兩個命名的新方法 `generatePDFOutput2`和 `generatePrintedOutput2`接受 `com.adobe.idp.Document`包含表單設計的物件。 您也可以傳遞 `com.adobe.idp.Document` 將列印資料流傳送至網路印表機時，包含輸出服務的表單設計。

**使用表單資料流執行動作**

您可以將非互動式表單儲存為PDF檔案。 此表單可在Adobe Reader或Acrobat中檢視。

**另请参阅**

[使用Java API將存放庫中的檔案傳遞至輸出服務](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

資源存放庫使用者端

### 使用Java API將存放庫中的檔案傳遞至輸出服務 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

使用輸出服務和存放庫API (Java)傳遞從存放庫擷取的檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar和adobe-repository-client.jar。

1. 建立輸出和Document Management使用者端API物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。 (請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。
   * 建立 `DocumentManagementServiceClientImpl` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 從AEM Forms存放庫擷取表單設計。

   叫用 `ResourceRepositoryClient` 物件的 `readResourceContent` 方法，並將指定URI位置的字串值傳遞至XDP檔案。 例如， `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. 此值為必要值。 此方法會傳回 `com.adobe.idp.Document` 代表XDP檔案的例項。

1. 演算非互動式PDF表單。

   叫用 `OutputClient` 物件的 `generatePDFOutput2` 方法並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定影像等其他資源所在的內容根。 例如：`repository:///Applications/FormsApplication/1.0/FormsFolder/`。
   * A `com.adobe.idp.Document` 代表表單設計的物件(使用 `ResourceRepositoryClient` 物件的 `readResourceContent` 方法)。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `com.adobe.idp.Document` 包含要與表單設計合併之資料之XML資料來源的物件。

   此 `generatePDFOutput2` 方法傳回 `OutputResult` 包含作業結果的物件。

1. 使用表單資料流執行動作。

   * 擷取 `com.adobe.idp.Document` 代表非互動式表單的物件。 `OutputResult` 物件的 `getGeneratedDoc` 方法。
   * 建立 `java.io.File` 包含作業結果的物件。 確認副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件放入檔案(請確定您使用 `com.adobe.idp.Document` 物件，由 `getGeneratedDoc` 方法)。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API將位於AEM Forms儲存庫中的檔案傳遞到Output服務](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用片段建立PDF檔案 {#creating-pdf-documents-using-fragments}

您可以使用輸出和組合器服務來建立以片段為基礎的輸出資料流，例如PDF檔案。 Assembler服務會根據位於多個XDP檔案中的片段來組合XDP檔案。 組裝的XDP檔案會傳遞到Output服務，該服務會建立PDF檔案。 雖然此工作流程顯示正在產生的PDF檔案，但「輸出」服務可以為此工作流程產生其他輸出型別，例如ZPL。 PDF檔案僅供討論之用。

下圖顯示此工作流程。

![cp_cp_outputassemblegments](assets/cp_cp_outputassemblefragments.png)

閱讀前 *使用片段建立PDF檔案*，建議您熟悉如何使用組合器服務來組合多個XDP檔案。 (請參閱 [組合多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>您也可以將由Assembler服務組裝的表單設計傳遞至Forms服務，而非Output服務。 Output服務與Forms服務的主要差異在於Forms服務會產生互動式PDF檔案，而Output服務會產生非互動式PDF檔案。 此外，Forms服務無法產生ZPL等印表機輸出資料流。

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-4}

若要根據片段建立PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出和組合器使用者端物件。
1. 使用Assembler服務產生表單設計。
1. 使用Output服務產生PDF檔案。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立輸出和組合器使用者端物件**

以程式設計方式執行輸出服務API操作之前，請先建立輸出使用者端API物件。 此外，由於此工作流程會叫用Assembler服務來建立表單設計，因此請建立Assembler使用者端API物件。

**使用Assembler服務產生表單設計**

使用Assembler服務產生使用片段的表單設計。 組合器服務傳回 `com.adobe.idp.Document` 包含表單設計的例項。

**使用Output服務產生PDF檔案**

您可以使用Output服務，使用Assembler服務建立的表單設計來產生PDF檔案。 傳遞 `com.adobe.idp.Document` 組合器服務傳回至輸出服務的執行個體。

**將PDF檔案儲存為PDF檔案**

在Output服務產生PDF檔案後，您可以將其儲存為PDF檔案。

**另请参阅**

[使用Java API根據片段建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[使用Web服務API根據片段建立PDF檔案](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[組合多個XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[建立PDF檔案](creating-document-output-streams.md#creating-pdf-documents)

### 使用Java API根據片段建立PDF檔案 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

使用輸出服務API和組合器服務API (Java)，根據片段建立PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出和組合器使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 使用Assembler服務產生表單設計。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列必要值：

   * A `com.adobe.idp.Document` 代表要使用的DDX檔案的物件。
   * A `java.util.Map` 包含輸入XDP檔案的物件。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 物件，指定執行階段選項，包括預設字型和作業記錄層級。

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含組合XDP檔案的物件。 若要擷取組裝的XDP檔案，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的 `getDocuments` 方法。 此方法會傳回 `java.util.Map` 物件。
   * 循環瀏覽 `java.util.Map` 物件，直到您找到結果為止 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 擷取組合XDP檔案的方法。


1. 使用Output服務產生PDF檔案。

   叫用 `OutputClient` 物件的 `generatePDFOutput2` 方法並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`
   * 字串值，指定其他資源（例如影像）所在的內容根
   * A `com.adobe.idp.Document` 代表表單設計的物件（使用Assembler服務傳回的例項）
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件
   * 此 `com.adobe.idp.Document` 包含要與表單設計合併之資料之XML資料來源的物件

   此 `generatePDFOutput2` 方法傳回 `OutputResult` 包含作業結果的物件

1. 將PDF檔案儲存為PDF檔案。

   * 擷取 `com.adobe.idp.Document` 代表PDF檔案的物件(透過叫用 `OutputResult` 物件的 `getGeneratedDoc` 方法。
   * 建立 `java.io.File` 包含作業結果的物件。 請確認副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件至檔案。 (請確定您使用 `com.adobe.idp.Document` 物件， `getGeneratedDoc` 方法已傳回。)。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[快速入門（SOAP模式）：使用Java API根據片段建立PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 使用Web服務API根據片段建立PDF檔案 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

使用輸出服務API和組合器服務API （Web服務），根據片段建立PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 對與Output服務相關聯的服務參考使用下列WSDL定義：

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   針對與Assembler服務相關聯的服務參考使用下列WSDL定義：

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   因為 `BLOB` 資料型別對兩個服務參考都是通用的，完全限定 `BLOB` 使用時的資料型別。 在對應的Web服務快速入門中，全部 `BLOB` 執行個體已完整合格。

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出和組合器使用者端物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給 `OutputServiceClient.ClientCredentials.UserName.UserName`欄位。
      * 將對應的密碼值指派給 `OutputServiceClient.ClientCredentials.UserName.Password`欄位。
      * 指派常數值 `HttpClientCredentialType.Basic` 至 `BasicHttpBindingSecurity.Transport.ClientCredentialType`欄位。
   * 指派 `BasicHttpSecurityMode.TransportCredentialOnly` 的常數值 `BasicHttpBindingSecurity.Security.Mode`欄位。

   >[!NOTE]
   >
   >對重複這些步驟 `AssemblerServiceClient`物件。

1. 使用Assembler服務產生表單設計。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含必要檔案的物件
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含工作結果和發生之任何例外狀況的物件。 若要取得新建立的XDP檔案，請執行下列動作：

   * 存取 `AssemblerResult` 物件的 `documents` 欄位，即 `Map` 包含結果PDF檔案的物件。
   * 循環瀏覽 `Map` 物件，以擷取組裝的表單設計。 轉換該陣列成員的 `value` 至 `BLOB`. 傳遞此 `BLOB` 執行個體到輸出服務。


1. 使用Output服務產生PDF檔案。

   叫用 `OutputServiceClient` 物件的 `generatePDFOutput2` 方法並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定其他資源（例如影像）所在的內容根。
   * A `BLOB` 代表表單設計的物件(使用 `BLOB` 執行個體（由組合器服務傳回）。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `BLOB` 包含要與表單設計合併之資料之XML資料來源的物件。
   * 輸出 `BLOB` 物件， `generatePDFOutput2` 方法會填入。 此 `generatePDFOutput2` 方法會使用產生的描述檔案的中繼資料填入此物件。 （只有Web服務呼叫需要此引數值）。
   * 輸出 `OutputResult` 包含作業結果的物件。 （只有Web服務呼叫需要此引數值）。

   此 `generatePDFOutput2` 方法傳回 `BLOB` 包含非互動式PDF表單的物件。

1. 將PDF檔案儲存為PDF檔案。

   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，該值代表互動式PDF檔案的檔案位置以及開啟檔案的模式。
   * 建立位元組陣列，儲存 `BLOB` 物件擷取自 `generatePDFOutput2` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 列印至檔案 {#printing-to-files}

您可以使用Output服務將如PostScript、印表機控制語言(PCL)或下列標籤格式等串流列印到檔案中：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用Output服務，您可以將XML資料與表單設計合併，並將表單列印到檔案中。 下圖顯示建立雷射和標籤檔案的Output服務。

>[!NOTE]
>
>如需傳送列印資料流至印表機的詳細資訊，請參閱 [傳送列印資料流至印表機](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-5}

若要列印至檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參照XML資料來源。
1. 設定列印至檔案所需的列印執行階段選項。
1. 將列印資料流列印到檔案。
1. 擷取作業的結果。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。 (請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立 `OutputClient` 物件。 如果您使用輸出Web服務API，請建立 `OutputServiceService` 物件。

**參考XML資料來源**

若要列印包含資料的檔案，您必須針對每個要填入資料的表單欄位，參考包含XML元素的XML資料來源。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

**設定列印至檔案所需的列印執行階段選項**

若要列印至檔案，您必須指定Output服務列印的檔案位置和名稱，以設定File URI執行階段選項。 例如，指示Output服務列印名為的PostScript檔案 *MortgageForm.ps* 若要C:\Adobe，請指定C:\Adobe\MortgageForm.ps。

>[!NOTE]
>
>您可以選擇定義執行階段選項。 如需可設定之所有選項的相關資訊，請參閱 `PrintedOutputOptionsSpec` 中的類別參考 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**將列印資料流列印到檔案**

在參照包含表單資料的有效XML資料來源並設定列印執行階段選項後，您可以叫用Output服務，使其列印檔案。

**擷取作業的結果**

Output服務執行作業之後，會傳回指定作業是否成功的各種資料專案，例如XML資料。

**另请参阅**

[使用Java API列印至檔案](creating-document-output-streams.md#print-to-files-using-the-java-api)

[使用Web服務API列印至檔案](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API列印至檔案 {#print-to-files-using-the-java-api}

使用Output API (Java)列印至檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參照XML資料來源。

   * 建立 `java.io.FileInputStream` 物件，代表XML資料來源，透過其建構函式並傳遞指定XML檔案位置的字串值，用來填入檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定列印至檔案所需的列印執行階段選項。

   * 建立 `PrintedOutputOptionsSpec` 物件（使用其建構函式）。
   * 透過叫用PrintedOutputOptionsSpec物件的 `setFileURI` 方法，並傳遞代表檔案名稱和位置的字串值。 例如，如果您希望Output服務列印到位於C:\Adobe中名為MortgageForm.ps的PostScript檔案，請指定C:\\Adobe\MortgageForm.ps。
   * 透過叫用「 」，指定要列印的份數 `PrintedOutputOptionsSpec` 物件的 `setCopies` 方法，並傳遞代表份數的整數值。

1. 將列印資料流列印到檔案。

   透過叫用 `OutputClient` 物件的 `generatePrintedOutput` 並傳遞下列值：

   * A `PrintFormat` 列舉值，指定要建立的列印資料流格式。 例如，若要建立PostScript列印資料流，請傳遞 `PrintFormat.PostScript`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定相關附屬檔案（例如影像檔案）的位置。
   * 字串值，指定要使用的XDC檔案位置(您可以傳遞 `null` 如果您透過使用 `PrintedOutputOptionsSpec` 物件)。
   * 此 `PrintedOutputOptionsSpec` 包含列印至檔案所需的執行階段選項的物件。
   * 此 `com.adobe.idp.Document` 包含包含表單資料之XML資料來源的物件。

   此 `generatePrintedOutput` 方法傳回 `OutputResult` 包含作業結果的物件。

   >[!NOTE]
   >
   >此 `OutputResult` 物件的 `getRecordLevelMetaDataList` 方法傳回 `null`.

1. 擷取作業的結果。

   * 建立 `com.adobe.idp.Document` 代表「 」狀態的物件 `generatePrintedOutput` 方法，方法是叫用 `OutputResult` 物件的 `getStatusDoc` 方法 `OutputResult` 物件由 `generatePrintedOutput` 方法)。
   * 建立 `java.io.File` 將包含作業結果的物件。 確定副檔名為XML。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件放入檔案(請確定您使用 `com.adobe.idp.Document` 物件，由 `getStatusDoc` 方法)。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API列印至檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 使用Web服務API列印至檔案 {#print-to-files-using-the-web-service-api}

使用Output API （Web服務）列印至檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參照XML資料來源。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存表單資料。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞字串值，指定包含表單資料的XML檔案位置。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `binaryData` 具有位元組陣列內容的屬性。

1. 設定列印至檔案所需的列印執行階段選項。

   * 建立 `PrintedOutputOptionsSpec` 物件（使用其建構函式）。
   * 指定字串值來指定檔案，該字串值代表檔案的位置和名稱 `PrintedOutputOptionsSpec` 物件的 `fileURI` 資料成員。 例如，如果您希望Output服務列印至名為的PostScript檔案 *MortgageForm.ps* 位於C:\Adobe，請指定C:\\Adobe\MortgageForm.ps。
   * 指定整數值，代表列印的份數，以指定要列印的份數。 `PrintedOutputOptionsSpec` 物件的 `copies` 資料成員。

1. 將列印資料流列印到檔案。

   透過叫用 `OutputServiceService` 物件的 `generatePrintedOutput` 並傳遞下列值：

   * A `PrintFormat` 列舉值，指定要建立的列印資料流格式。 例如，若要建立PostScript列印資料流，請傳遞 `PrintFormat.PostScript`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定相關附屬檔案（例如影像檔案）的位置。
   * 字串值，指定要使用的XDC檔案位置(您可以傳遞 `null` 如果您透過使用 `PrintedOutputOptionsSpec` 物件)。
   * 此 `PrintedOutputOptionsSpec` 包含列印至檔案所需的列印執行階段選項的物件。
   * 此 `BLOB` 包含表單資料之XML資料來源的物件。
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會使用產生的描述檔案的中繼資料填入此物件。 （只有Web服務呼叫需要此引數值。）
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會將結果資料填入此物件中。 （只有Web服務呼叫需要此引數值。）
   * 一個 `OutputResult` 包含作業結果的物件。 （只有Web服務呼叫需要此引數值。）

1. 擷取作業的結果。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確定副檔名為XML。
   * 建立位元組陣列，儲存 `BLOB` 填入結果資料的物件 `OutputServiceService` 物件的 `generatePDFOutput` 方法（第八個引數）。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 傳送列印資料流至印表機 {#sending-print-streams-to-printers}

您可以使用Output服務將列印資料流(例如PostScript、印表機控制語言(PCL))或下列標籤格式傳送至網路印表機：

* 斑馬 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用Output服務，您可以將XML資料與表單設計合併，並將表單輸出為列印資料流。 例如，您可以建立PostScript列印資料流，並將其傳送至網路印表機。 下圖顯示Output服務傳送列印資料流至網路印表機。

>[!NOTE]
>
>為了示範如何將列印資料流傳送至網路印表機，本節使用SharedPrinter印表機通訊協定，將PostScript列印資料流傳送至網路印表機。

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-6}

若要將列印資料流傳送至網路印表機，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參照XML資料來源。
1. 設定列印執行階段選項
1. 擷取要列印的檔案。
1. 將檔案傳送至網路印表機。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出使用者端物件**

以程式設計方式執行輸出服務作業之前，請先建立輸出服務使用者端物件。 如果您使用Java API，請建立 `OutputClient` 物件。 如果您使用輸出Web服務API，請建立 `OutputServiceClient` 物件。

**參考XML資料來源**

若要列印包含資料的檔案，您必須針對每個要填入資料的表單欄位，參考包含XML元素的XML資料來源。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

**設定列印執行階段選項**

當傳送列印資料流至印表機時，您可以設定執行階段選項，包括下列選項：

* **份數**：指定要傳送至印表機的復本數。 默认值为 1。
* **裝訂**：使用裝訂器時會設定XCI選項。 此選項可由裝訂元素在組態模型中指定，且僅用於PS和PCL印表機。
* **OutputJog**：XCI選項是在輸出頁面應慢跑（在輸出匣中實際移動）時設定。 此選項僅適用於PS和PCL印表機。
* **輸出紙匣**：用來讓列印驅動程式選取適當輸出紙匣的XCI值。

>[!NOTE]
>
>如需您可以設定的所有執行階段選項的詳細資訊，請參閱 `PrintedOutputOptionsSpec` 類別參考。

**擷取要列印的檔案**

擷取要傳送至印表機的列印資料流。 例如，您可以擷取PostScript檔案並將其傳送至印表機。

如果您的印表機支援PDF，您可以選擇傳送PDF檔案。 不過，將PDF檔案傳送至印表機的問題是每個印表機製造商都有不同的PDF解譯器實作。 也就是說，有些列印製造商會使用Adobe PDF的解讀，但這取決於印表機。 其他印表機有自己的PDF解譯器。 因此，列印結果可能會有所不同。

傳送PDF檔案至印表機的另一個限制是它只會列印；除了透過印表機的設定，它不能存取雙面列印、紙匣選擇和裝訂。

若要擷取要列印的檔案，請使用 `generatePrintedOutput` 方法。 下表指定在使用時，為指定列印資料流設定的內容型別 `generatePrintedOutput` 方法。

<table>
 <thead>
  <tr>
   <th><p>列印格式 </p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>依預設或自訂xdc輸出串流建立dpl203.xdc。</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>建立DPL 300 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>建立DPL 400 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>建立DPL 600 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>建立一般色彩PCL (5c)輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>建立一般PostScript Level 3輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>建立自訂IPL輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>建立IPL 300 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>建立IPL 400 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>建立一般單色PCL (5e)輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>建立一般PostScript Level 2輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>建立自訂TPCL輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>建立TPCL 305 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>建立TPCL 600 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>建立ZPL 203 DPI輸出資料流。</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>建立ZPL 300 DPI輸出資料流。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您也可以使用將列印資料流傳送到印表機 `generatePrintedOutput2` 方法。 不過，與「傳送列印資料流至印表機」段落相關的快速啟動會使用 `generatePrintedOutput` 方法。

**傳送列印資料流至網路印表機**

擷取要列印的檔案後，您可以叫用Output服務，使其將列印資料流傳送至網路印表機。 若要讓「輸出」服務成功找到印表機，您必須同時指定列印伺服器和印表機名稱。 此外，您也必須指定列印通訊協定。

>[!NOTE]
>
>如果PDFG安裝在表單伺服器上，且伺服器在Windows Server 2008上執行，則無法使用SharedPrinter屬性。 在此情況下，請使用不同的印表機通訊協定。

>[!NOTE]
>
>如果您使用網路印表機，且存取機製為SharedPrinter，則需要指定印表機的完整網路路徑。使用Java API將列印資料流傳送至網路印表機

使用輸出API (Java)將列印資料流傳送至網路印表機：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考XML資料來源

   * 建立 `java.io.FileInputStream` 物件，代表XML資料來源，透過其建構函式並傳遞指定XML檔案位置的字串值，用來填入檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定列印執行階段選項

   建立 `PrintedOutputOptionsSpec` 代表列印執行階段選項的物件。 例如，您可以透過叫用 `PrintedOutputOptionsSpec` 物件的 `setCopies` 方法。

   >[!NOTE]
   >
   >您無法透過以下方式設定分頁值： `PrintedOutputOptionsSpec` 物件的 `setPagination` 方法（如果您要產生ZPL列印資料流）。 同樣地，您無法為ZPL列印資料流設定下列選項：OutputJog、PageOffset和Staple。 此 `setPagination` 方法對於PostScript產生無效。 它只適用於PCL產生。

1. 擷取要列印的檔案

   * 透過叫用來擷取要列印的檔案 `OutputClient` 物件的 `generatePrintedOutput` 並傳遞下列值：

      * A `PrintFormat` 指定列印資料流的列舉值。 例如，若要建立PostScript列印資料流，請傳遞 `PrintFormat.PostScript`.
      * 字串值，指定表單設計的名稱。
      * 字串值，指定相關附屬檔案（例如影像檔案）的位置。
      * 字串值，指定要使用的XDC檔案位置。
      * 此 `PrintedOutputOptionsSpec` 包含列印至檔案所需之執行階段選項的物件。
      * 此 `com.adobe.idp.Document` 物件，代表包含要與表單設計合併之表單資料的XML資料來源。

      此方法會傳回 `OutputResult` 包含作業結果的物件。

   * 建立 `com.adobe.idp.Document` 要透過叫用至印表機的物件 `OutputResult` 物件 `getGeneratedDoc` 方法。 此方法會傳回 `com.adobe.idp.Document` 物件。


1. 傳送列印資料流至網路印表機

   透過叫用將列印資料流傳送到網路印表機 `OutputClient` 物件的 `sendToPrinter` 並傳遞下列值：

   * A `com.adobe.idp.Document` 代表要傳送至印表機的列印資料流的物件。
   * A `PrinterProtocol` 列舉值，指定要使用的印表機通訊協定。 例如，若要指定SharedPrinter通訊協定，請傳遞 `PrinterProtocol.SharedPrinter`.
   * 指定列印伺服器名稱的字串值。 例如，假設列印伺服器的名稱為PrintSever1，請通過 `\\\PrintSever1`.
   * 字串值，指定印表機的名稱。 例如，假設印表機的名稱為Printer1，請通過 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >此 `sendToPrinter` 方法已新增至8.2.1版的AEM Forms API。

### 使用網站服務API傳送列印資料流至印表機 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

使用Output API （Web服務）將列印資料流傳送至網路印表機：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參照XML資料來源。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存表單資料。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，指定包含表單資料之XML檔案的位置。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 透過取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 設定列印執行階段選項。

   建立 `PrintedOutputOptionsSpec` 物件（使用其建構函式）。 例如，您可以指定整數值，代表要列印的份數。 `PrintedOutputOptionsSpec` 物件的 `copies` 資料成員。

   >[!NOTE]
   >
   >您無法透過以下方式設定分頁值： `PrintedOutputOptionsSpec` 物件的 `pagination` 資料成員（如果您要產生ZPL列印資料流）。 同樣地，您無法為ZPL列印資料流設定下列選項：OutputJog、PageOffset和Staple。 此 `pagination` 資料成員對PostScript產生無效。 它只適用於PCL產生。

1. 擷取要列印的檔案。

   * 透過叫用來擷取要列印的檔案 `OutputServiceService` 物件的 `generatePrintedOutput` 並傳遞下列值：

      * A `PrintFormat` 指定列印資料流的列舉值。 例如，若要建立PostScript列印資料流，請傳遞 `PrintFormat.PostScript`.
      * 字串值，指定表單設計的名稱。
      * 字串值，指定相關附屬檔案（例如影像檔案）的位置。
      * 字串值，指定要使用的XDC檔案位置。
      * 此 `PrintedOutputOptionsSpec` 包含列印執行時間選項的物件，在傳送列印資料流至網路印表機時使用。
      * 此 `BLOB` 包含表單資料之XML資料來源的物件。
      * A `BLOB` 由填入的物件 `generatePrintedOutput` 方法。 此 `generatePrintedOutput` 方法會使用產生的描述檔案的中繼資料填入此物件。 （只有Web服務呼叫需要此引數值。）
      * A `BLOB` 由填入的物件 `generatePrintedOutput` 方法。 此 `generatePrintedOutput` 方法會將結果資料填入此物件中。 （只有Web服務呼叫需要此引數值。）
      * 一個 `OutputResult` 包含作業結果的物件。 （只有Web服務呼叫需要此引數值。）
   * 建立 `BLOB` 要傳送至印表機的物件，方法是取得 `OutputResult` 物件 `generatedDoc` 方法。 此方法會傳回 `BLOB` 包含由傳回之PostScript資料的物件 `generatePrintedOutput` 方法。


1. 將列印資料流傳送至網路印表機。

   透過叫用將列印資料流傳送到網路印表機 `OutputClient` 物件的 `sendToPrinter` 並傳遞下列值：

   * A `BLOB` 代表要傳送至印表機的列印資料流的物件。
   * A `PrinterProtocol` 列舉值，指定要使用的印表機通訊協定。 例如，若要指定SharedPrinter通訊協定，請傳遞 `PrinterProtocol.SharedPrinter`.
   * A `bool` 指定是否要使用先前引數值的值。 傳遞值 `true`. （只有Web服務呼叫需要此引數值。）
   * 指定列印伺服器名稱的字串值。 例如，假設列印伺服器的名稱為PrintSever1，請通過 `\\\PrintSever1`.
   * 字串值，指定印表機的名稱。 例如，假設印表機的名稱為Printer1，請通過 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >此 `sendToPrinter` 方法已新增至8.2.1版的AEM Forms API。

## 建立多個輸出檔案 {#creating-multiple-output-files}

Output服務可以為XML資料來源內的每個記錄建立個別的檔案，或是包含所有記錄的單一檔案（此功能為預設值）。 例如，假設有10筆記錄位於XML資料來源中，而您指示輸出服務使用輸出服務API，為每個記錄建立個別的PDF檔案（或其他型別的輸出）。 因此，Output服務會產生十份PDF檔案。 （您可以將多個列印資料流傳送至印表機，而不建立檔案。）

下圖也顯示處理包含多個記錄之XML資料檔案的Output服務。 不過，假設您指示Output服務建立包含所有資料記錄的單一PDF檔案。 在這種情況下，Output服務會產生一個包含所有記錄的檔案。

下圖顯示處理包含多個記錄之XML資料檔案的Output服務。 假設您指示Output服務為每個資料記錄建立單獨的PDF檔案。 在這種情況下，Output服務會為每個資料記錄產生個別的PDF檔案。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

下列XML資料顯示包含三個資料記錄的資料檔案範例。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

請注意，每個資料記錄開始和結束的XML元素為 `LoanRecord`. 產生多個檔案的應用程式邏輯會參考此XML元素。

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-7}

若要根據XML資料來源建立多個PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參照XML資料來源。
1. 設定PDF執行階段選項。
1. 設定演算執行階段選項。
1. 產生多個PDF檔案。
1. 擷取作業的結果。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立 `OutputClient` 物件。 如果您使用輸出Web服務API，請建立 `OutputServiceService` 物件。

**參考XML資料來源**

參考包含多個記錄的XML資料來源。 必須使用XML元素來分隔資料記錄。 例如，在本節前面顯示的範例XML資料來源中，分隔資料記錄的XML元素命名為 `LoanRecord`.

每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 如果已指定所有XML元素，則不必比對XML元素的顯示順序。

**設定PDF執行階段選項**

您必須為輸出服務設定下列執行階段選項，才能根據XML資料來源成功建立多個檔案：

* **許多檔案**：指定Output服務是建立單一檔案還是多個檔案。 您可以指定true或false。 若要為XML資料來源中的每個資料記錄建立個別的檔案，請指定true。
* **檔案URI**：指定輸出服務產生之檔案的位置。 例如，假設您指定C:\\Adobe\forms\Loan.pdf。 在此情況下，Output服務會建立名為Loan.pdf的檔案，並將該檔案放在C:\\Adobe\forms資料夾中。 有多個檔案時，檔案名稱為Loan0001.pdf、Loan0002.pdf、Loan0003.pdf等。 如果您指定檔案位置，檔案會放在伺服器上，而不是使用者端電腦上。
* **記錄名稱**：指定資料來源中用於分隔資料記錄的XML元素名稱。 例如，在本節先前顯示的範例XML資料來源中，會呼叫分隔資料記錄的XML元素 `LoanRecord`. (您不必設定「記錄名稱」執行階段選項，而是可以將「記錄層級」指派為數字值，指出包含資料記錄的元素層級，以設定「記錄層級」。 不過，您只能設定「記錄名稱」或「記錄層次」。 您無法同時設定這兩個值。)

**設定演算執行階段選項**

您可以在建立多個檔案時設定演算執行階段選項。 雖然這些選項並非必要（不同於必要的輸出執行階段選項），但您可以執行工作，例如改善Output服務的效能。 例如，您可以快取Output服務使用的表單設計以提高效能。

Output服務處理批次記錄時，會以累加方式讀取包含多個記錄的資料。 也就是說，Output服務會將資料讀入記憶體，並在批次記錄處理時釋出資料。 設定兩個執行階段選項之一時，Output服務會以累加方式載入資料。 如果您設定「記錄名稱」執行階段選項，Output服務會以累加方式讀取資料。 同樣地，如果您將「記錄層級」執行時間選項設為2或更大，Output服務會以累加方式讀取資料。

您可以使用「 」控制Output服務是否執行增量載入 `PDFOutputOptionsSpec` 或 `PrintedOutputOptionSpec` 物件的 `setLazyLoading` 方法。 您可以傳遞值 `false` 關閉增量載入的這個方法。

**產生多個PDF檔案**

在參照包含多個資料記錄並設定執行階段選項的有效XML資料來源後，您可以叫用Output服務，使其產生多個檔案。 產生多個記錄時， `OutputResult` 物件的 `getGeneratedDoc` 方法傳回 `null`.

**擷取作業的結果**

Output服務執行作業之後，會傳回指定作業是否成功的XML資料。 下列XML由Output服務傳回。 在此情況下，Output服務會產生42份檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立多個PDF檔案 {#create-multiple-pdf-files-using-the-java-api}

使用Output API (Java)建立多個PDF檔案：

1. 包含專案檔案」

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。.

1. 建立輸出使用者端物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考XML資料來源

   * 建立 `java.io.FileInputStream` 物件，代表包含多個記錄的XML資料來源，方法是使用其建構函式，並傳遞指定XML檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定PDF執行階段選項

   * 建立 `PDFOutputOptionsSpec` 物件（使用其建構函式）。
   * 透過叫用 `PDFOutputOptionsSpec` 物件的 `setGenerateManyFiles` 方法。 例如，傳遞值 `true` 指示Output服務為XML資料來源中的每個記錄建立個別的PDF檔案。 (如果通過 `false`，輸出服務會產生包含所有記錄的單一PDF檔案)。
   * 透過叫用 `PDFOutputOptionsSpec` 物件的 `setFileUri` 和傳遞字串值，該值指定輸出服務產生之檔案的位置。 檔案URI選項是相對於裝載AEM Forms的J2EE應用程式伺服器，而不是使用者端電腦。
   * 透過叫用 `OutputOptionsSpec` 物件的 `setRecordName` 方法並傳遞字串值，該值會指定資料來源中，用於分隔資料記錄的XML元素名稱。 (例如，請考量本節前面所示的XML資料來源。 分隔資料記錄的XML元素名稱為LoanRecord)。

1. 設定演算執行階段選項

   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。
   * 快取表單設計以透過叫用 `RenderOptionsSpec` 物件的 `setCacheEnabled` 並傳遞 `Boolean` 值 `true`.

1. 產生多個PDF檔案

   透過叫用多個PDF檔案 `OutputClient` 物件的 `generatePDFOutput` 並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `com.adobe.idp.Document` 包含要與表單設計合併之資料之XML資料來源的物件。

   此 `generatePDFOutput` 方法傳回 `OutputResult` 包含作業結果的物件。

1. 擷取作業的結果

   * 建立 `java.io.File` 物件，代表將包含結果的XML檔案 `generatePDFOutput` 方法。 確認副檔名為.xml。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件放入檔案(請確定您使用 `com.adobe.idp.Document` 物件，由 `applyUsageRights` 方法)。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API建立多個PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立多個PDF檔案 {#create-multiple-pdf-files-using-the-web-service-api}

使用Output API （Web服務）建立多個PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參照XML資料來源。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存包含多個記錄的表單資料。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表包含多個記錄之XML檔案的檔案位置的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 設定PDF執行階段選項。

   * 建立 `PDFOutputOptionsSpec` 物件（使用其建構函式）。
   * 將布林值指派給，以設定「多個檔案」選項 `OutputOptionsSpec` 物件的 `generateManyFiles` 資料成員。 例如，指派值 `true` 指示輸出服務為XML資料來源中的每個記錄建立個別的PDF檔案。 (如果您指派 `false` 之後，Output服務會產生包含所有記錄的單一PDF)。
   * 透過指派字串值來設定檔案URI選項，該字串值指定輸出服務產生給的檔案位置。 `OutputOptionsSpec` 物件的 `fileURI` 資料成員。 檔案URI選項是相對於裝載AEM Forms的J2EE應用程式伺服器，而不是使用者端電腦。
   * 藉由指定字串值來設定記錄名稱選項，該字串值指定資料來源中的XML元素名稱，該資料來源會將資料記錄分隔至 `OutputOptionsSpec` 物件的 `recordName` 資料成員。
   * 透過指定整數值來設定複製選項，整數值會指定輸出服務產生給 `OutputOptionsSpec` 物件的 `copies` 資料成員。

1. 設定演算執行階段選項。

   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。
   * 快取表單設計以指派值來改善Output服務的效能 `true` 至 `RenderOptionsSpec` 物件的 `cacheEnabled` 資料成員。

1. 產生多個PDF檔案。

   透過叫用多個PDF檔案 `OutputServiceService` 物件的 `generatePDFOutput`並傳遞下列值：

   * TransformationFormat列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `BLOB` 包含要與表單設計合併之資料之XML資料來源的物件。
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會使用產生的描述檔案的中繼資料填入此物件。
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會將結果資料填入此物件中。
   * 一個 `OutputResult` 包含作業結果的物件。

1. 擷取作業的結果

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確認副檔名為.xml。
   * 建立位元組陣列，儲存 `BLOB` 填入結果資料的物件 `OutputServiceService` 物件的 `generatePDFOutput` 方法（第八個引數）。 透過取得 `BLOB` 物件的 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 建立搜尋規則 {#creating-search-rules}

您可以建立搜尋規則，讓Output服務檢查輸入資料，並根據資料內容使用不同的表單設計來產生輸出。 例如，如果文字 *按揭* 位在輸入資料中，則Output服務可使用名為Mortgage.xdp的表單設計。 同樣地，如果文字 *汽車* 位於輸入資料中，則Output服務可使用儲存為AutomobileLoan.xdp的表單設計。 雖然Output服務可以產生不同的輸出型別，但本節假設了Output服務會產生PDF檔案。 下圖顯示Output服務透過處理XML資料檔案並使用多種表單設計之一來產生PDF檔案。

此外，Output服務能夠產生檔案套件，其中資料集中提供了多個記錄，每個記錄都與一個表單設計相符，並且由多個表單設計產生單個檔案。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-8}

若要指示Output服務在產生檔案時使用搜尋規則，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 參照XML資料來源。
1. 定義搜尋規則。
1. 設定PDF執行階段選項。
1. 設定演算執行階段選項。
1. 產生PDF檔案。
1. 擷取作業的結果。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，則您需要將adobe-utilities.jar和jbossall-client.jar取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。

**參考XML資料來源**

每個要填入資料的表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 只要已指定所有XML元素，就不需要比對XML元素的顯示順序。

**定義搜尋規則**

若要定義搜尋規則，您可以定義「輸出」服務在輸入資料中搜尋的一或多個文字模式。 對於您定義的每個文字模式，指定在文字模式所在位置所使用的對應表單設計。 如果找到文字模式，則Output服務會使用對應的表單設計來產生輸出。 文字模式的範例為 *按揭*.

>[!NOTE]
>
>如果找不到文字圖樣，則會使用預設的表單。 請確定您使用的所有表單設計都位於內容根目錄中。

**設定PDF執行階段選項**

設定下列PDF執行階段選項，讓Output服務根據多個表單設計成功建立PDF檔案：

* **檔案URI**：指定Output服務產生的PDF檔案名稱和位置。
* **規則**：指定您定義的規則。
* **LookAhead**：指定從輸入資料檔案開頭起要用於掃描已定義文字模式的位元組數。 預設值為500位元組。

**設定演算執行階段選項**

您可以在建立PDF檔案時設定演算執行階段選項。 雖然這些選項不是必要選項(不同於PDF執行階段選項)，但您可以執行工作，例如改善Output服務的效能。 例如，您可以快取Output服務使用的表單設計以提高效能。

**產生PDF檔案**

參照有效的XML資料來源並設定執行階段選項後，您可以叫用Output服務，使其產生PDF檔案。 如果Output服務在輸入資料中找到指定的文字模式，則會使用對應的表單設計。 如果未使用文字模式，則Output服務會使用預設的表單設計。

**擷取作業的結果**

Output服務執行作業之後，會傳回指定作業是否成功的XML資料。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API建立搜尋規則 {#create-search-rules-using-the-java-api}

使用Output API (Java)建立搜尋規則：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參照XML資料來源。

   * 建立 `java.io.FileInputStream` 物件，代表使用建構函式並傳遞指定XML檔案位置的字串值來填入PDF檔案的XML資料來源。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 定義搜尋規則。

   * 建立 `Rule` 物件（使用其建構函式）。
   * 透過叫用定義文字模式 `Rule` 物件的 `setPattern` 和傳遞指定文字模式的字串值。
   * 透過叫用 `Rule` 物件的 `setForm` 方法。 傳遞指定表單設計名稱的字串值。

   >[!NOTE]
   >
   >針對您要定義的每個文字模式，重複前三個子步驟。

   * 建立 `java.util.List` 物件(使用 `java.util.ArrayList` 建構函式。
   * 針對每個 `Rule` 您建立的物件，呼叫 `java.util.List` 物件的 `add` 方法並傳遞 `Rule` 物件。


1. 設定PDF執行階段選項。

   * 建立 `PDFOutputOptionsSpec` 物件（使用其建構函式）。
   * PDF指定Output服務透過叫用 `PDFOutputOptionsSpec` 物件的 `setFileURI` 方法。 傳遞字串值，指定PDF檔案的位置。 檔案URI選項是相對於裝載AEM Forms的J2EE應用程式伺服器，而不是使用者端電腦。
   * 透過叫用 `PDFOutputOptionsSpec` 物件的 `setRules` 方法。 傳遞 `java.util.List` 包含 `Rule` 物件。
   * 透過叫用「 」，設定要掃描已定義文字模式的位元組數 `PDFOutputOptionsSpec` 物件的 `setLookAhead` 方法。 傳遞代表位元組數的整數值。

1. 設定演算執行階段選項。

   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。
   * 快取表單設計，以透過叫用 `RenderOptionsSpec` 物件的 `setCacheEnabled` 和傳遞 `true`.

1. 產生PDF檔案。

   透過叫用，產生以多個表單設計為基礎的PDF檔案 `OutputClient` 物件的 `generatePDFOutput` 並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定預設表單設計的名稱。 亦即，在找不到文字模式時所使用的表單設計。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `com.adobe.idp.Document` 包含表單資料的物件，由Output服務針對定義的文字模式進行搜尋。

   此 `generatePDFOutput` 方法傳回 `OutputResult` 包含作業結果的物件。

1. 擷取作業的結果。

   * 建立 `com.adobe.idp.Document` 代表「 」狀態的物件 `generatePDFOutput` 方法，方法是叫用 `OutputResult` 物件的 `getStatusDoc` 方法。
   * 建立 `java.io.File` 將包含作業結果的物件。 確認副檔名為.xml。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件放入檔案(請確定您使用 `com.adobe.idp.Document` 物件，由 `getStatusDoc` 方法)。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API建立搜尋規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[快速入門（SOAP模式）：使用Java API建立搜尋規則](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立搜尋規則 {#create-search-rules-using-the-web-service-api}

使用Output API （Web服務）建立搜尋規則：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參照XML資料來源。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存將與PDF檔案合併的資料。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表要加密之PDF檔案的檔案位置，以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 定義搜尋規則。

   * 建立 `Rule` 物件（使用其建構函式）。
   * 藉由指定字串值來定義文字模式，該字串值會指定文字模式 `Rule` 物件的 `pattern` 資料成員。
   * 藉由指派字串值來定義對應的表單設計，該字串值會指定表單設計給 `Rule` 物件的 `form` 資料成員。

   >[!NOTE]
   >
   >針對您要定義的每個文字模式，重複前三個子步驟。

   * 建立 `MyArrayOf_xsd_anyType` 儲存規則的物件。
   * 指派每一個 `Rule` 物件至的元素 `MyArrayOf_xsd_anyType` 陣列。 叫用 `MyArrayOf_xsd_anyType` 物件的 `Add` 每個專案的方法 `Rule` 物件。


1. 設定PDF執行階段選項

   * 建立 `PDFOutputOptionsSpec` 物件（使用其建構函式）。
   * 透過指派字串值來設定檔案URI選項，該字串值會指定Output服務產生的PDF檔案的位置 `PDFOutputOptionsSpec` 物件的 `fileURI` 資料成員。 檔案URI選項是相對於裝載AEM Forms的J2EE應用程式伺服器，而不是使用者端電腦。
   * 透過指定整數值來設定複製選項，整數值會指定輸出服務產生給 `PDFOutputOptionsSpec` 物件的 `copies` 資料成員。
   * 設定您透過指派 `MyArrayOf_xsd_anyType` 將規則儲存到的物件 `PDFOutputOptionsSpec` 物件的 `rules` 資料成員。
   * 將代表要掃描位元組數的整數值指派給，以設定要掃描已定義文字模式的位元組數。 `PDFOutputOptionsSpec` 物件的 `lookAhead` 資料方法。

1. 設定演算執行階段選項

   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。
   * 快取表單設計，以便透過指派值來改善Output服務的效能 `true` 至 `RenderOptionsSpec` 物件的 `cacheEnabled` 資料成員。

   >[!NOTE]
   >
   >您無法使用設定PDF檔案的版本 `RenderOptionsSpec` 物件的 `pdfVersion` 成員(如果輸入檔案是Acrobat表單)。 輸出PDF檔案會保留Acrobat表單的PDF版本。 同樣地，您無法透過以下方式設定標籤PDF選項： `RenderOptionsSpec` 物件的 `taggedPDF` 方法(如果輸入檔案是Acrobat表單)。

   >[!NOTE]
   >
   >您無法透過以下方式設定線性PDF選項： `RenderOptionsSpec` 物件的 `linearizedPDF` 如果輸入PDF檔案經過認證或數位簽署，則為成員。 如需詳細資訊，請參閱 [數位簽署PDF檔案](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. 產生PDF檔案

   透過叫用建立PDF檔案 `OutputServiceService` 物件的 `generatePDFOutput`並傳遞下列值：

   * A `TransformationFormat` 列舉值。 若要產生PDF檔案，請指定 `TransformationFormat.PDF`.
   * 字串值，指定表單設計的名稱。
   * 字串值，指定表單設計所在的內容根。
   * A `PDFOutputOptionsSpec` 包含PDF執行階段選項的物件。
   * A `RenderOptionsSpec` 包含演算執行階段選項的物件。
   * 此 `BLOB` 包含要與表單設計合併之資料之XML資料來源的物件。
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會使用產生的描述檔案的中繼資料填入此物件。 （只有Web服務呼叫需要此引數值）。
   * A `BLOB` 由填入的物件 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法會將結果資料填入此物件中。 （只有Web服務呼叫需要此引數值）。
   * 一個 `OutputResult` 包含作業結果的物件。 （只有Web服務呼叫需要此引數值）。

   >[!NOTE]
   >
   >PDF當透過叫用 `generatePDFOutput` 方法，請注意，您無法將資料與已簽署、已驗證或包含使用許可權的XFAPDF表單合併。 如需使用許可權的詳細資訊，請參閱 [將使用許可權套用至PDF檔案](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. 擷取作業的結果

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表包含結果資料之XML檔案位置的字串值。 確定副檔名為XML。
   * 建立位元組陣列，儲存 `BLOB` 填入結果資料的物件 `OutputServiceService` 物件的 `generatePDFOutput` 方法（第八個引數）。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 平面化PDF檔案 {#flattening-pdf-documents}

您可以使用Output服務將互動式PDF檔案轉換為非互動式PDF。 互動式PDF檔案可讓使用者輸入或修改PDF檔案欄位中的資料。 將互動式PDF檔案轉換為非互動式PDF檔案的程式稱為 *平面化*. 當PDF檔案平面化時，使用者無法修改檔案欄位中的資料。 平面化PDF檔案的一個原因是為了確保無法修改資料。

您可以平面化下列PDF檔案型別：

* 互動式XFAPDF檔案
* Acrobat Forms

嘗試平面化非互動式PDF檔案的PDF會產生例外狀況。

>[!NOTE]
>
>如需Output服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-9}

若要將互動式PDF檔案平面化為非互動式PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立輸出使用者端物件。
1. 擷取互動式PDF檔案。
1. 轉換PDF檔案。
1. 將非互動式PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您是使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果將AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，您需要將adobe-utilities.jar和jbossall-client.jar檔案取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立輸出使用者端物件**

您必須先建立輸出服務使用者端物件，才能以程式設計方式執行輸出服務作業。 如果您使用Java API，請建立 `OutputClient` 物件。 如果您使用輸出Web服務API，請建立 `OutputServiceService` 物件。

**擷取互動式PDF檔案**

擷取您想要轉換為非互動式PDF檔案的互動式PDF檔案。 嘗試轉換非互動式PDF檔案會產生例外狀況。

**轉換PDF檔案**

擷取互動式PDF檔案後，可將其轉換為非互動式PDF檔案。 Output服務會傳回非互動式PDF檔案。

**將非互動式PDF檔案儲存為PDF檔案**

您可以將非互動式PDF檔案儲存為PDF檔案。

**另请参阅**

[使用Java API平面化PDF檔案](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[使用Web服務API平面化PDF檔案](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API快速啟動](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API平面化PDF檔案 {#flatten-a-pdf-document-using-the-java-api}

使用Output API (Java)將互動式PDF檔案平面化為非互動式PDF檔案：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-output-client.jar。

1. 建立輸出使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `OutputClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取互動式PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，代表要轉換的互動式PDF檔案，使用它的建構函式，並傳遞字串值，指定互動式PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 轉換PDF檔案。

   透過叫用「 」，將互動PDF檔案轉換為非互動PDF檔案 `OutputServiceService` 物件的 `transformPDF` 並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含互動式PDF檔案的物件。
   * A `TransformationFormat` 列舉值。 若要產生非互動式PDF檔案，請指定 `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` 指定修訂版本編號的列舉值。 由於此引數適用於PDF/A檔案，因此您可以指定 `null`.
   * 代表修訂編號和年份的字串值，以冒號分隔。 由於此引數適用於PDF/A檔案，因此您可以指定 `null`.
   * A `PDFAConformance` 代表PDF/A一致性層級的列舉值。 由於此引數適用於PDF/A檔案，因此您可以指定 `null`.

   此 `transformPDF` 方法傳回 `com.adobe.idp.Document` 包含非互動式PDF檔案的物件。

1. 將非互動式PDF檔案儲存為PDF檔案。

   * 建立 `java.io.File` 物件並確保副檔名為.pdf。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `transformPDF` 方法)。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[快速入門（EJB模式）：使用Java API轉換PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[快速入門（SOAP模式）：使用Java API轉換PDF檔案](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API平面化PDF檔案 {#flatten-a-pdf-document-using-the-web-service-api}

使用Output API （Web服務）將互動式PDF檔案平面化為非互動式PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立輸出使用者端物件。

   * 建立 `OutputServiceClient` 物件（使用其預設建構函式）。
   * 建立 `OutputServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `OutputServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取互動式PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存互動式PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表互動式PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 轉換PDF檔案。

   透過叫用「 」，將互動PDF檔案轉換為非互動PDF檔案 `OutputClient` 物件的 `transformPDF` 並傳遞下列值：

   * A `BLOB` 包含互動式PDF檔案的物件。
   * A `TransformationFormat` 列舉值。 若要產生非互動式PDF檔案，請指定 `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` 指定修訂版本編號的列舉值。
   * Boolean值，指定 `PDFARevisionNumber` 使用列舉值。 由於此引數適用於PDF/A檔案，因此您可以指定 `false`.
   * 代表修訂編號和年份的字串值，以冒號分隔。 由於此引數適用於PDF/A檔案，因此您可以指定 `null`.
   * A `PDFAConformance` 代表PDF/A一致性層級的列舉值。
   * 布林值，指定 `PDFAConformance` 使用列舉值。 由於此引數適用於PDF/A檔案，因此您可以指定 `false`.

   此 `transformPDF` 方法傳回 `BLOB` 包含非互動式PDF檔案的物件。

1. 將非互動式PDF檔案儲存為PDF檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表非互動式PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `transformPDF` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
