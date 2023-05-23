---
title: 使用XMP公用程式
seo-title: Working with XMP Utilities
description: 使用XMP公用程式Java和Web服務API，以程式設計方式將XMP中繼資料匯入PDF檔案，並從PDF檔案中擷取和儲存XMP中繼資料。
seo-description: Use the XMP Utilities Java and Web Service APIs to programmatically import XMP metadata into a PDF document and retrieve and save XMP metadata from a PDF document.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---

# 使用XMP公用程式 {#working-with-xmp-utilities}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於XMP公用程式服務**

PDF檔案包含中繼資料，這是與檔案內容（如文字和圖形）區別開的檔案相關資訊。 Adobe可延伸中繼資料平台(XMP)是處理檔案中繼資料的標準。

XMP Utilities服務可以從PDF檔案中擷取和儲存XMP中繼資料，以及將XMP中繼資料匯入PDF檔案。

您可以使用XMP Utilities服務完成這些工作：

* 將中繼資料匯入PDF檔案。 (請參閱 [將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents).)
* 從PDF檔案匯出中繼資料。 (請參閱 [從PDF檔案匯出中繼資料](xmp-utilities.md#exporting-metadata-from-pdf-documents).)

>[!NOTE]
>
>如需「XMP公用程式」服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將中繼資料匯入PDF檔案 {#importing-metadata-into-pdf-documents}

您可以使用XMP公用程式Java和Web服務API，以程式設計方式將XMP中繼資料匯入PDF檔案。 中繼資料提供有關PDF檔案的資訊，例如檔案的作者和與檔案相關的關鍵字。 中繼資料可位於檔案的「檔案屬性」對話方塊中，如下圖所示。

![ww_ww_metadatadatalog](assets/ww_ww_metadatadialog.png)

若要以程式設計方式將中繼資料匯入PDF檔案，您可以使用指定中繼資料值的現有XML檔案，也可以使用型別的物件 `XMPUtilityMetadata`. (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

>[!NOTE]
>
>本節討論如何使用XML檔案將中繼資料匯入PDF檔案。

下列XML程式碼包含對應至上圖的中繼資料值。 例如，請注意指定關鍵字的粗體專案。

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>如需「XMP公用程式」服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要將XMP中繼資料匯入PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立XMPUtilityService使用者端。
1. 叫用XMP中繼資料匯入作業。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立XMPUtilityService使用者端**

您必須先建立XMPUtilityService使用者端，才能以程式設計方式執行XMP Utilities作業。 使用Java API時，可透過建立 `XMPUtilityServiceClient` 物件。 使用Web服務API時，這是透過使用 `XMPUtilityServiceService` 物件。

**叫用XMP中繼資料匯入作業**

建立服務使用者端後，您可以叫用其中一個XMP中繼資料匯入操作，將XMP中繼資料匯入指定的PDF檔案。

**另请参阅**

[使用Java API匯入XMP中繼資料](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用Web服務API匯入XMP中繼資料](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API匯入XMP中繼資料 {#import-xmp-metadata-using-the-java-api}

使用XMP Utilities API (Java)匯入XMP中繼資料：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar檔案包含可讓您以程式設計方式叫用XMP Utilities服務的類別。

1. 建立XMPUtilityService使用者端

   建立 `XMPUtilityServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 叫用XMP中繼資料匯入作業

   若要修改XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件的 `importMetadata` 方法或其 `importXMP` 方法。

   如果您使用 `importMetadata` 方法，傳入下列值：

   * A `com.adobe.idp.Document` 代表PDF檔案的物件。
   * 一個 `XMPUtilityMetadata` 包含要匯入之中繼資料的物件。

   如果您使用 `importXMP` 方法，傳入下列值：

   * A `com.adobe.idp.Document` 代表PDF檔案的物件。
   * A `com.adobe.idp.Document` 物件，代表包含要匯入之中繼資料的XML檔案。

   在任一情況下，傳回的值為 `com.adobe.idp.Document` 物件，代表含有新匯入中繼資料的PDF檔案。 然後您可以將此物件儲存至磁碟。

**另请参阅**

[將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API匯入XMP中繼資料 {#importing-xmp-metadata-using-the-web-service-api}

若要使用XMP Utilities Web服務API以程式設計方式匯入XMP中繼資料，請執行下列工作：

1. 包含專案檔案

   * 建立使用XMP Utilities服務WSDL檔案的Microsoft .NET使用者端元件。 (請參閱 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)
   * 參考Microsoft .NET使用者端元件。 (請參閱 [建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. 建立XMPUtilityService使用者端

   建立 `XMPUtilityServiceService` 物件（使用proxy類別建構函式）。

1. 叫用XMP中繼資料匯入作業

   若要修改XMP中繼資料，請叫用 `XMPUtilityServiceService` 物件的 `importMetadata` 方法或其 `importXMP` 方法。

   如果您使用 `importMetadata` 方法，傳入下列值：

   * A `BLOB` 代表PDF檔案的物件。
   * 一個 `XMPUtilityMetadata` 包含要匯入之中繼資料的物件。

   如果您使用 `importXMP` 方法，傳入下列值：

   * A `BLOB` 代表PDF檔案的物件。
   * A `BLOB` 物件，代表包含要匯入之中繼資料的XML檔案。

   在任一情況下，傳回的值為 `BLOB` 物件，代表含有新匯入中繼資料的PDF檔案。 然後您可以將此物件儲存至磁碟。

**另请参阅**

[將中繼資料匯入PDF檔案](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 從PDF檔案匯出中繼資料 {#exporting-metadata-from-pdf-documents}

您可以使用XMP Utilities Java和Web服務API，以程式設計方式從PDF檔案中擷取和儲存XMP中繼資料。

>[!NOTE]
>
>如需「XMP公用程式」服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

若要從PDF檔案匯出XMP中繼資料，請執行下列步驟：

1. 包含專案檔案。
1. 建立XMPUtilityService使用者端。
1. 叫用XMP中繼資料匯出作業。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立XMPUtilityService使用者端**

您必須先建立XMPUtilityService使用者端，才能以程式設計方式執行XMP Utilities作業。 使用Java AP時，您可以透過建立 `XMPUtilityServiceClient` 物件。 使用Web服務API時，可使用 `XMPUtilityServiceService` 物件。

**叫用XMP中繼資料匯出作業**

建立服務使用者端後，您可以叫用其中一個XMP中繼資料匯出作業，該作業可用於檢查XMP中繼資料或將其儲存至磁碟。

**另请参阅**

[使用Java API匯入XMP中繼資料](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用Web服務API匯入XMP中繼資料](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API匯出XMP中繼資料 {#export-xmp-metadata-using-the-java-api}

使用XMP Utilities API (Java)匯出XMP中繼資料：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar檔案包含可讓您以程式設計方式叫用XMP公用程式服務的類別。

1. 建立XMPUtilityService使用者端

   建立 `XMPUtilityServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 叫用XMP中繼資料匯入作業

   若要檢查XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件的 `exportMetadata` 方法並傳入 `com.adobe.idp.Document` 代表PDF檔案的物件。 方法會傳回 `XMPUtilityMetadata` 包含已擷取中繼資料的物件。

   若要擷取和儲存XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件的 `exportXMP` 方法並傳入 `com.adobe.idp.Document` 代表PDF檔案的物件。 方法會傳回 `com.adobe.idp.Document` 包含擷取的中繼資料的物件，之後可儲存至磁碟做為XML檔案。

**另请参阅**

[從PDF檔案匯出中繼資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API匯出XMP中繼資料 {#export-xmp-metadata-using-the-web-service-api}

使用XMP Utilities API （Web服務）匯出XMP中繼資料：

1. 包含專案檔案

   * 建立使用XMP Utilities服務WSDL檔案的Microsoft .NET使用者端元件。
   * 參考Microsoft .NET使用者端元件。

1. 建立XMPUtilityService使用者端

   建立 `XMPUtilityServiceService` 物件（使用proxy類別建構函式）。

1. 叫用XMP中繼資料匯入作業

   若要檢查XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件的 `exportMetadata` 方法並傳入 `BLOB` 代表PDF檔案的物件。 方法會傳回 `XMPUtilityMetadata` 包含已擷取中繼資料的物件。

   若要擷取和儲存XMP中繼資料，請叫用 `XMPUtilityServiceClient` 物件的 `exportXMP` 方法並傳入 `BLOB` 代表PDF檔案的物件。 方法會傳回 `BLOB` 包含擷取的中繼資料的物件，之後可儲存至磁碟做為XML檔案。

**另请参阅**

[從PDF檔案匯出中繼資料](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[建立使用Base64編碼的.NET使用者端元件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
