---
title: 使用條碼式表單
seo-title: Working with barcoded forms
description: 使用Java API和Web服務API從PDF表單或包含條碼的影像解碼資料。
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# 使用條碼式表單 {#working-with-barcoded-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 關於條碼式Forms服務 {#about-the-barcoded-forms-service}

條碼式表單服務可自動從填寫並列印的表單中擷取資料，並將擷取的資訊整合到組織的核心IT系統中。

使用條碼式表單服務，您可以將一維和二維條碼新增至互動式PDF forms。 接著，您就可以將條碼式表單發佈至網站，或透過電子郵件或CD分發。 當使用者使用Adobe Reader、Acrobat Professional或Acrobat Standard填寫條碼表單時，條碼會自動更新以編碼使用者提供的表單資料。 使用者可以電子方式提交表單，或列印成紙張，然後以郵件、傳真或手提方式提交。 您稍後可以擷取使用者提供的資料，作為自動化工作流程的一部分，在核准程式和業務系統之間路由資料。

如需條碼式表單服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 解碼條碼式表單資料 {#decoding-barcoded-form-data}

您可以使用條碼式表單服務API，將PDF表單或包含條碼之影像中的資料解碼。 解碼表單資料表示擷取位於條碼中的資料。 使用者必須先在表單中填入資料，才能從PDF表單（或影像）解碼資料。

>[!NOTE]
>
>如需條碼式表單服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要從PDF表單解碼資料，請執行下列步驟：

1. 包含專案檔案。
1. 建立條碼式formsClient API物件。
1. 取得包含條碼資料的PDF表單。
1. 解碼PDF表單中的資料。
1. 將資料轉換為XML資料來源。
1. 處理解碼的資料。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)
* xercesImpl.jar (位於 &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

如果將AEM Forms部署在非JBOSS的支援J2EE應用程式伺服器上，則您需要將adobe-utilities.jar和jbossall-client.jar取代為部署AEM Forms之J2EE應用程式伺服器專屬的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立條碼式表單使用者端API物件**

您必須先建立條碼式Forms服務使用者端，才能以程式設計方式執行條碼式表單服務作業。 如果您使用Java API，請建立 `BarcodedFormsServiceClient` 物件。 如果您使用條碼式表單Web服務API，請建立 `BarcodedFormsServiceService` 物件。

**取得包含條碼資料的PDF表單**

您必須取得內含已填入使用者資料條碼的PDF表單。

**解碼PDF表單中的資料**

取得包含條碼的PDF表單（或影像）後，您就可以將資料解碼。 條碼Forms服務支援下列型別的條碼：

* PDF417條碼。
* 資料矩陣條碼。
* QR碼。
* 代碼標籤條碼。
* 代碼128條碼。
* 代碼39條碼。
* ean-13條碼。
* EAN-8條碼。

在解碼API中以十六進位字元集輸入表示條碼的內容會編碼為十六進位字串。 例如，如果在表單中將UTF-8指定為字元編碼，並在解碼操作中指定Hex，則條碼的內容會在&lt;中編碼為十六進位字串 `xb:content`>已解碼輸出中的element。 您可以在使用者端應用程式中建立應用程式邏輯，轉換此Hex值以取得原始內容。

**將資料轉換為XML資料來源**

將表單資料解碼後，可將其轉換為XDP或XFDF資料。 例如，假設您要將資料匯入其他表單。 若要將資料匯入XFA表單，您必須將資料轉換為XDP資料。 如需詳細資訊，請參閱 [匯入表單資料](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**處理解碼的資料**

您可以處理轉換後的資料，以符合業務需求。 例如，在解碼和轉換資料後，您可以將其儲存至檔案、儲存在企業資料庫中、填入其他表單等。 本節討論如何將轉換的資料儲存為XML檔案。

>[!NOTE]
>
>當行分隔符號和欄位分隔符號引數具有相同的值時，條碼式表單服務無法解碼條碼資料

**另请参阅**

[使用Java API將條碼式表單資料解碼](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用網站服務API將條碼式表單資料解碼](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API將條碼式表單資料解碼 {#decode-barcoded-form-data-using-the-java-api}

使用條碼式Forms API (Java)將表單資料解碼：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案。

1. 建立條碼式表單使用者端API物件

   建立 `BarcodedFormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 取得包含條碼資料的PDF表單

   * 建立 `java.io.FileInputStream` 物件，代表包含條碼式資料的PDF表單，使用它的建構函式並傳遞指定PDF檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 解碼PDF表單中的資料

   透過叫用 `BarcodedFormsServiceClient` 物件的 `decode` 並傳遞下列值：

   * 此 `com.adobe.idp.Document` 包含PDF表單的物件。
   * A `java.lang.Boolean` 指定是否要解碼PDF417條碼的物件。
   * A `java.lang.Boolean` 指定是否要解碼資料矩陣條碼的物件。
   * A `java.lang.Boolean` 指定是否要解碼QR碼條碼的物件。
   * A `java.lang.Boolean` 物件，指定是否要解碼程式碼標籤條碼。
   * A `java.lang.Boolean` 物件，指定是否要解碼代碼128條碼。
   * A `java.lang.Boolean` 物件，指定是否將程式碼39條碼解碼。
   * A `java.lang.Boolean` 指定是否要解碼EAN-13條碼的物件。
   * A `java.lang.Boolean` 指定是否要解碼EAN-8條碼的物件。
   * A `com.adobe.livecycle.barcodedforms.CharSet` 列舉值，指定條碼中使用的字元集編碼值。

   此 `decode` 方法傳回 `org.w3c.dom.Document` 包含已解碼表單資料的物件。

1. 將資料轉換為XML資料來源

   透過叫用 `BarcodedFormsServiceClient` 物件的 `extractToXML` 並傳遞下列值：

   * 此 `org.w3c.dom.Document` 包含已解碼資料的物件(請確定您使用 `decode` 方法的傳回值)。
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 指定行分隔字元的列舉值。 建議您指定 `Delimiter.Carriage_Return`.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 指定欄位分隔字元的列舉值。 例如，指定 `Delimiter.Tab`.
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` 列舉值，指定要將條碼資料轉換為XDP或XFDF XML資料。 例如，指定 `XMLFormat.XDP` 將資料轉換為XDP資料。

   >[!NOTE]
   >
   >請勿為行分隔符號和欄位分隔符號引數指定相同的值。

   此 `extractToXML` 方法傳回 `java.util.List` 物件，其中每個元素為 `org.w3c.dom.Document` 物件。 表單上的每個條碼都有個別的元素。 也就是說，如果表單上有四個條碼，則傳回的元素有四個 `java.util.List` 物件。

1. 處理解碼的資料

   * 循環瀏覽 `java.util.List` 要取得每個專案的物件 `org.w3c.dom.Document` 物件。
   * 針對清單中的每個元素，將 `org.w3c.dom.Document` 物件至 `com.adobe.idp.Document` 物件。 (可轉換 `org.w3c.dom.Document` 物件放入 `com.adobe.idp.Document` 物件以（使用Java API範例）顯示在解碼條碼式表單資料中。
   * 透過叫用 `com.adobe.idp.Document` 物件的 `copyToFile`，並傳遞代表XML檔案的檔案物件。

**另请参阅**

[快速入門（SOAP模式）：使用Java API解碼條碼式表單資料](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將條碼式表單資料解碼 {#decode-barcoded-form-data-using-the-web-service-api}

使用條碼式Forms API （Web服務）將表單資料解碼：

1. 包含專案檔案

   * 建立使用條碼式表單服務WSDL的Microsoft .NET使用者端元件。 如需詳細資訊，請參閱 [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * 參考Microsoft .NET使用者端元件。 如需詳細資訊，請參閱以下的「參照.NET使用者端元件」： [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. 建立條碼式表單使用者端API物件

   使用使用條碼式表單服務WSDL的Microsoft .NET使用者端元件，建立 `BarcodedFormsServiceService` 物件，透過叫用其預設建構函式。

1. 取得包含條碼資料的PDF表單

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存包含條碼的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `binaryData` 具有位元組陣列內容的屬性。

1. 解碼PDF表單中的資料

   透過叫用 `BarcodedFormsServiceService` 物件的 `decode` 並傳遞下列值：

   * 此 `BLOB` 包含PDF表單的物件。
   * A `Boolean` 指定是否要解碼PDF417條碼的物件。
   * A `Boolean` 指定是否要解碼資料矩陣條碼的物件。
   * A `Boolean` 指定是否要解碼QR碼條碼的物件。
   * A `Boolean` 物件，指定是否要解碼程式碼標籤條碼。
   * A `Boolean` 物件，指定是否要解碼代碼128條碼。
   * A `Bolean` 物件，指定是否將程式碼39條碼解碼。
   * A `Boolean` 指定是否要解碼EAN-13條碼的物件。
   * A `Boolean` 指定是否要解碼EAN-8條碼的物件。
   * A `CharSet` 列舉值，指定條碼中使用的字元集編碼值。

   此 `decode` 方法會傳回包含已解碼表單資料的字串值。

1. 將資料轉換為XML資料來源

   透過叫用 `BarcodedFormsServiceService` 物件的 `extractToXML` 並傳遞下列值：

   * 包含已解碼資料的字串值(請務必使用 `decode` 方法的傳回值)。
   * A `Delimiter` 指定行分隔字元的列舉值。 建議您指定 `Delimiter.Carriage_Return`.
   * A `Delimiter` 指定欄位分隔字元的列舉值。 例如，指定 `Delimiter.Tab`.
   * A `XMLFormat` 列舉值，指定要將條碼資料轉換為XDP或XFDF XML資料。 例如，指定 `XMLFormat.XDP` 將資料轉換為XDP資料。

   >[!NOTE]
   >
   >請勿為行分隔符號和欄位分隔符號引數指定相同的值。

   此 `extractToXML` 方法傳回 `Object` 陣列，其中每個元素為 `BLOB` 執行個體。 表單上的每個條碼都有個別的元素。 也就是說，如果表單上有四個條碼，則傳回的元素有四個 `Object` 陣列。

1. 處理解碼的資料

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表受保護PDF檔案檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `encryptPDFUsingPassword` 方法。 透過取得 `BLOB` 物件的 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
