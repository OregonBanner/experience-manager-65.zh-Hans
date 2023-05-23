---
title: 數位簽署和認證檔案
seo-title: Digitally Signing and Certifying Documents
description: 使用簽名服務來新增和刪除數位簽名欄位到PDF檔案、擷取位於PDF檔案中的簽名欄位名稱、修改簽名欄位、數位簽署PDF檔案、驗證PDF檔案中的數位簽名、驗證PDFPDF檔案中的所有數位簽名，以及從簽名欄位中移除數位簽名。
seo-description: Use the Signature service to add and delete digital signature fields to a PDF document, retrieve the names of signature fields located in a PDF document, modify signature fields, digitally sign PDF documents, certify PDF documents, validate digital signatures located in a PDF document, validate all digital signatures located in a PDF document, and remove a digital signature from a signature field.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '17046'
ht-degree: 0%

---

# 數位簽署和認證檔案 {#digitally-signing-and-certifying-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於簽名服務**

簽名服務可讓貴組織保護所散發及接收的Adobe PDF檔案之安全性與隱私權。 此服務使用數位簽名和認證，以確保只有預期的收件者才能變更檔案。 由於安全性功能會套用至檔案本身，因此檔案在其整個生命週期中都會保持安全和受控。 當檔案離線下載以及將檔案送回您的組織時，防火牆外仍會保持安全。

>[!NOTE]
>
>您可以為叫用某些作業(例如簽署PDF檔案)時所叫用的簽名服務建立自訂簽名處理常式。

**簽章欄位名稱**

某些簽章服務作業需要您指定執行作業的簽章欄位名稱。 例如，在簽署PDF檔案時，您可以指定要簽署的簽名欄位名稱。 假設簽名欄位的完整名稱是 `form1[0].Form1[0].SignatureField1[0]`. 您可以指定 `SignatureField1[0]` 而非 `form1[0].Form1[0].SignatureField1[0]`.

有時衝突會導致簽名服務簽署（或執行另一個需要簽名欄位名稱的操作）錯誤的欄位。 此衝突是名稱的結果 `SignatureField1[0]` 出現在同一PDF檔案中的兩個或多個位置。 例如，假設一個PDF檔案包含兩個名為的簽名欄位 `form1[0].Form1[0].SignatureField1[0]` 和 `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` 並且您指定 `SignatureField1[0]`. 在這種情況下，簽名服務會在重複檔案中的所有簽名欄位時找到第一個簽名欄位進行簽名。

如果PDF檔案中有多個簽名欄位，建議您指定簽名欄位的完整名稱。 也就是說，指定 `form1[0].Form1[0].SignatureField1[0]`而非 `SignatureField1[0]`.

您可以使用「簽名」服務完成這些工作：

* 新增和刪除數位簽名欄位至PDF檔案。 (請參閱 [新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields).)
* 擷取位於PDF檔案中的簽名欄位名稱。 (請參閱 [正在擷取簽章欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* 修改簽名欄位。 (請參閱 [修改簽章欄位](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* 數位簽署PDF檔案。 (請參閱 [數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* 認證PDF檔案。 (請參閱 [認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* 驗證PDF檔案中的數位簽名。 (請參閱 [驗證數位簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 驗證PDF檔案中的所有數位簽名。 (請參閱 [驗證多個數位簽名](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 從簽名欄位中移除數位簽名。 (請參閱 [移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>如需Signature服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)..

## 新增簽名欄位 {#adding-signature-fields}

數位簽章會出現在簽章欄位中，這些欄位是包含簽章圖形表示的表單欄位。 簽名欄位可以顯示或隱藏。 簽名者可以使用預先存在的簽名欄位，也可以以程式設計方式新增簽名欄位。 在任何一種情況下，簽章欄位都必須存在，才能簽署PDF檔案。

您可以使用簽名服務Java API或簽名Web服務API，以程式設計方式新增簽名欄位。 您可以將多個簽章欄位新增至PDF檔案，但每個簽章欄位名稱必須是唯一的。

>[!NOTE]
>
>有些PDF檔案型別不允許您以程式設計方式新增簽名欄位。 如需有關簽名服務和新增簽名欄位的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要將簽名欄位新增至PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得新增簽名欄位的PDF檔案。
1. 新增簽名欄位。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立簽名使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得新增簽名欄位的PDF檔案**

您必須取得新增簽名欄位的PDF檔案。

**新增簽名欄位**

若要成功將簽名欄位新增到PDF檔案中，請指定可識別簽名欄位位置的座標值。 （如果您新增隱藏的簽章欄位，這些值不是必要值。） 此外，您也可以指定在將簽章套用至簽章欄位後，要鎖定PDF檔案中的哪些欄位。

**將PDF檔案儲存為PDF檔案**

簽名服務將簽名欄位新增到PDF檔案後，您可以將檔案儲存為PDF檔案，以便使用者在Acrobat或Adobe Reader中開啟它。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API新增簽名欄位 {#add-signature-fields-using-the-java-api}

使用Signature API (Java)新增簽名欄位：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 取得新增簽名欄位的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表簽名欄位新增至的PDF檔案，方法是使用其建構函式，並傳遞字串值，以指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 新增簽名欄位

   * 建立 `PositionRectangle` 物件，使用其建構函式來指定簽章欄位位置。 在建構函式中，指定座標值。
   * 如有需要，請建立 `FieldMDPOptions` 物件，指定將數位簽章套用至簽章欄位時鎖定的欄位。
   * 透過叫用「 」將簽名欄位新增到PDF檔案 `SignatureServiceClient` 物件的 `addSignatureField` 並傳遞下列值：

      * A `com.adobe.idp`. `Document` 物件，代表新增簽名欄位的PDF檔案。
      * 字串值，指定簽名欄位的名稱。
      * A `java.lang.Integer` 代表新增簽名欄位的頁碼值。
      * A `PositionRectangle` 指定簽名欄位位置的物件。
      * A `FieldMDPOptions` 物件，指定PDF檔案中數位簽章套用至簽章欄位後鎖定的欄位。 此引數值為選用，您可以傳遞 `null`.
   * A `PDFSeedValueOptions` 指定各種執行階段值的物件。 此引數值為選用，您可以傳遞 `null`.

      此 `addSignatureField` 方法傳回 `com.adobe.idp`. `Document` 物件，代表包含簽名欄位的PDF檔案。
   >[!NOTE]
   >
   >您可以叫用 `SignatureServiceClient` 物件的 `addInvisibleSignatureField` 方法以新增不可見的簽章欄位。

1. 將PDF檔案儲存為PDF檔案

   * 建立 `java.io.File` 物件，並確認副檔名為.pdf。
   * 叫用 `com.adobe.idp`. `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件至檔案。 確保您使用 `com.adobe.idp`. `Document` 物件，由 `addSignatureField` 方法。

**另请参阅**

[簽名服務API快速啟動](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用Web服務API新增簽名欄位 {#add-signature-fields-using-the-web-service-api}

若要使用Signature API （Web服務）新增簽名欄位：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得新增簽名欄位的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存將包含簽名欄位的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 新增簽名欄位

   透過叫用「 」，將簽名欄位新增到PDF檔案 `SignatureServiceClient` 物件的 `addSignatureField` 並傳遞下列值：

   * A `BLOB` 物件，代表新增簽名欄位的PDF檔案。
   * 字串值，指定簽名欄位名稱。
   * 整數值，代表要新增簽名欄位的頁碼。
   * A `PositionRect` 指定簽名欄位位置的物件。
   * A `FieldMDPOptions` 物件，指定PDF檔案中數位簽章套用至簽章欄位後鎖定的欄位。 此引數值為選用，您可以傳遞 `null`.
   * A `PDFSeedValueOptions` 指定各種執行階段值的物件。 此引數值為選用，您可以傳遞 `null`.

   此 `addSignatureField` 方法傳回 `BLOB` 物件，代表包含簽名欄位的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞字串值，該值代表PDF檔案的檔案位置，其中將包含簽名欄位和開啟檔案的模式。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `addSignatureField` 方法。 透過取得 `BLOB` 物件的 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 正在擷取簽章欄位名稱 {#retrieving-signature-field-names}

您可以擷取位於要簽署或認證之PDF檔案中的所有簽名欄位名稱。 如果您不確定位於PDF檔案中的簽名欄位名稱，或者您想要驗證這些名稱，則可以使用程式擷取它們。 Signature服務會傳回簽名欄位的完整名稱，例如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>如需Signature服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步驟摘要 {#summary_of_steps-1}

若要擷取簽章欄位名稱，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含簽名欄位的PDF檔案。
1. 擷取簽名欄位名稱。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得包含簽名欄位的PDF檔案**

擷取包含簽名欄位的PDF檔案。

**擷取簽名欄位名稱**

在擷取包含一個或多個簽名欄位的PDF檔案後，您可以擷取簽名欄位名稱。

**另请参阅**

[使用Java API擷取簽名欄位名稱](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用Web服務API擷取簽名欄位](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API擷取簽名欄位名稱 {#retrieve-signature-field-names-using-the-java-api}

使用簽名API (Java)擷取簽名欄位名稱：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 取得包含簽名欄位的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表包含簽名欄位的PDF檔案，方法是使用其建構函式並傳遞指定PDF檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 擷取簽名欄位名稱

   * 透過叫用擷取簽名欄位名稱 `SignatureServiceClient` 物件的 `getSignatureFieldList` 方法和傳遞 `com.adobe.idp.Document` 包含包含簽名欄位之PDF檔案的物件。 此方法會傳回 `java.util.List` 物件，其中每個元素都包含 `PDFSignatureField` 物件。 使用此物件，您可以取得有關簽名欄位的額外資訊，例如它是否可見。
   * 循環瀏覽 `java.util.List` 物件來判斷是否有簽名欄位名稱。 對於PDF檔案中的每個簽名欄位，您可以取得單獨的 `PDFSignatureField` 物件。 若要取得簽名欄位的名稱，請叫用 `PDFSignatureField` 物件的 `getName` 方法。 此方法會傳回指定簽名欄位名稱的字串值。

**另请参阅**

[正在擷取簽章欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入門（SOAP模式）：使用Java API擷取簽名欄位名稱](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API擷取簽名欄位 {#retrieve-signature-field-using-the-web-service-api}

使用簽名API （Web服務）擷取簽名欄位名稱：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得包含簽名欄位的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存包含簽名欄位的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 欄位位位元組陣列內容。

1. 擷取簽名欄位名稱

   * 透過叫用擷取簽名欄位名稱 `SignatureServiceClient` 物件的 `getSignatureFieldList` 方法和傳遞 `BLOB` 包含包含簽名欄位之PDF檔案的物件。 此方法會傳回 `MyArrayOfPDFSignatureField` 集合物件，其中每個元素包含 `PDFSignatureField` 物件。
   * 循環瀏覽 `MyArrayOfPDFSignatureField` 物件來判斷是否有簽名欄位名稱。 對於PDF檔案中的每個簽名欄位，您可以取得 `PDFSignatureField` 物件。 若要取得簽名欄位的名稱，請叫用 `PDFSignatureField` 物件的 `getName` 方法。 此方法會傳回指定簽名欄位名稱的字串值。

**另请参阅**

[正在擷取簽章欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改簽章欄位 {#modifying-signature-fields}

您可以使用Java API和Web服務API來修改位於PDF檔案中的簽名欄位。 修改簽章欄位涉及處理其簽章欄位鎖定字典值或種子值字典值。

A *欄位鎖定字典* 指定簽名欄位簽署時鎖定的欄位清單。 鎖定的欄位可防止使用者變更欄位。 A *種子值字典* 包含套用簽章時使用的限制資訊。 例如，您可以變更在不使簽名失效的情況下控制可能發生的動作的許可權。

透過修改現有的簽名欄位，您可以變更PDF檔案，以反映不斷變化的業務需求。 例如，新的業務需求可能需要在簽署檔案後鎖定所有檔案欄位。

本節說明如何修改欄位鎖定字典和種子值字典值，以修改簽名欄位。 簽名欄位簽署時，對簽名欄位鎖定字典所做的變更會導致PDF檔案中的所有欄位被鎖定。 對種子值字典所做的變更會禁止對檔案進行特定型別的變更。

>[!NOTE]
>
>如需有關簽名服務和修改簽名欄位的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

若要修改位於PDF檔案中的簽名欄位，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含要修改之簽名欄位的PDF檔案。
1. 設定字典值。
1. 修改簽名欄位。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含LiveCycleJava程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得包含要修改之簽名欄位的PDF檔案**

擷取包含要修改之簽名欄位的PDF檔案。

**設定字典值**

若要修改簽章欄位，請將值指派給其欄位鎖定字典或種子值字典。 指定簽名欄位鎖定字典值涉及指定簽名欄位簽署時鎖定的PDF檔案欄位。 （本節討論如何鎖定所有欄位。）

可以設定以下種子值字典值：

* **修訂檢查**：指定簽章套用至簽章欄位時是否執行撤銷檢查。
* **憑證選項**：將值指派給憑證種子值字典。 在指定憑證選項之前，建議您先熟悉憑證種子值字典。 (請參閱 [PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **摘要選項**：指派用於簽署的摘要演演算法。 有效值為SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **篩選**：指定與簽章欄位搭配使用的篩選器。 例如，您可以使用Adobe.PPKLite篩選器。 (請參閱 [PDF參考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **標幟選項**：指定與此簽章欄位關聯的旗標值。 值1表示簽署者只能使用專案的指定值。 值0表示允許其他值。 以下是Bit位置：

   * **1 （篩選）：** 用於簽署簽名欄位的簽名處理常式
   * **2 (SubFilter)：** 一個名稱陣列，指示簽署時要使用的可接受編碼
   * **3 (V)**：簽署簽名欄位所使用的簽名處理常式的最低版本號碼
   * **4 （原因）：** 指定簽署檔案可能原因的字串陣列
   * **5 (PDFLegalWarnings)：** 字串陣列，指定可能合法的證明

* **法律證明**：當檔案通過驗證時，會自動掃描特定型別的內容，這會使檔案的可見內容含糊或誤導使用者。 例如，註解可能會模糊文字，而這些文字對於瞭解認證內容非常重要。 掃描程式會產生警告，指出存在此型別的內容。 此外，也會針對可能產生警告的內容提供額外說明。
* **許可權**：指定可用於不會使簽名失效的PDF檔案的許可權。
* **原因**：指定必須簽署此檔案的原因。
* **時間戳記**：指定時間戳記選項。 例如，您可以設定所用時間戳記伺服器的URL。
* **版本**：指定用於簽署簽名欄位的簽名處理常式的最小版本號碼。

**修改簽名欄位**

建立「簽名」服務使用者端、擷取包含要修改之簽名欄位的PDF檔案並設定說明值之後，您可以指示「簽名」服務修改簽名欄位。 然後Signature service會傳回包含修改過之簽章欄位的PDF檔案。 原始PDF檔案不受影響。

**將PDF檔案儲存為PDF檔案**

將包含已修改簽名欄位的PDF檔案儲存為PDF檔案，以便使用者可以在Acrobat或Adobe Reader中將其開啟。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[簽名服務API快速啟動](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API修改簽名欄位 {#modify-signature-fields-using-the-java-api}

使用簽名API (Java)修改簽名欄位：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 取得包含要修改之簽名欄位的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表包含簽名欄位的PDF檔案，可透過使用其建構函式並傳遞指定PDF檔案位置的字串值來修改。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定字典值

   * 建立 `PDFSignatureFieldProperties` 物件（使用其建構函式）。 A `PDFSignatureFieldProperties` 物件儲存簽章欄位鎖定字典和種子值字典資訊。
   * 建立 `PDFSeedValueOptionSpec` 物件（使用其建構函式）。 此物件可讓您設定種子值字典值。
   * 透過叫用「 」，不允許變更PDF檔案 `PDFSeedValueOptionSpec` 物件的 `setMdpValue` 方法和傳遞 `MDPPermissions.NoChanges` 列舉值。
   * 建立 `FieldMDPOptionSpec` 物件（使用其建構函式）。 此物件可讓您設定簽章欄位鎖定字典值。
   * 叫用「 」，鎖定PDF檔案中的所有欄位 `FieldMDPOptionSpec` 物件的 `setMdpValue` 方法和傳遞 `FieldMDPAction.ALL` 列舉值。
   * 透過叫用設定種子值字典資訊 `PDFSignatureFieldProperties` 物件的 `setSeedValue` 方法和傳遞 `PDFSeedValueOptionSpec` 物件。
   * 透過叫用設定簽章欄位鎖定字典資訊 `PDFSignatureFieldProperties`物件的 `setFieldMDP` 方法和傳遞 `FieldMDPOptionSpec` 物件。

   >[!NOTE]
   >
   >若要檢視所有可設定的種子值字典值，請參閱 `PDFSeedValueOptionSpec` 類別參考。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. 修改簽名欄位

   透過叫用 `SignatureServiceClient` 物件的 `modifySignatureField` 並傳遞下列值：

   * 此 `com.adobe.idp.Document` 儲存包含要修改之簽名欄位的PDF檔案的物件
   * 字串值，指定簽名欄位的名稱
   * 此 `PDFSignatureFieldProperties` 儲存簽章欄位鎖定字典和種子值字典資訊的物件

   此 `modifySignatureField` 方法傳回 `com.adobe.idp.Document` 物件，用來儲存包含已修改簽名欄位的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立 `java.io.File` 物件並確保副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件至檔案。 確保您使用 `com.adobe.idp.Document` 物件， `modifySignatureField` 方法已傳回。

### 使用Web服務API修改簽名欄位 {#modify-signature-fields-using-the-web-service-api}

使用Signature API （Web服務）修改簽名欄位：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得包含要修改之簽名欄位的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存包含要修改之簽名欄位的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 屬性位元組陣列的內容。

1. 設定字典值

   * 建立 `PDFSignatureFieldProperties` 物件（使用其建構函式）。 此物件儲存簽章欄位鎖定字典和種子值字典資訊。
   * 建立 `PDFSeedValueOptionSpec` 物件（使用其建構函式）。 此物件可讓您設定種子值字典值。
   * 透過指派「 」來禁止對PDF檔案進行變更 `MDPPermissions.NoChanges` 列舉值至 `PDFSeedValueOptionSpec` 物件的 `mdpValue` 資料成員。
   * 建立 `FieldMDPOptionSpec` 物件（使用其建構函式）。 此物件可讓您設定簽章欄位鎖定字典值。
   * 透過指派以下專案來鎖定PDF檔案中的所有欄位： `FieldMDPAction.ALL` 列舉值至 `FieldMDPOptionSpec` 物件的 `mdpValue` 資料成員。
   * 透過指派以下專案設定種子值字典資訊： `PDFSeedValueOptionSpec` 物件至 `PDFSignatureFieldProperties` 物件的 `seedValue` 資料成員。
   * 透過指派以下專案來設定簽章欄位鎖定字典資訊 `FieldMDPOptionSpec` 物件至 `PDFSignatureFieldProperties` 物件的 `fieldMDP` 資料成員。

   >[!NOTE]
   >
   >若要檢視所有可設定的種子值字典值，請參閱 `PDFSeedValueOptionSpec` 類別參考。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改簽名欄位

   透過叫用 `SignatureServiceClient` 物件的 `modifySignatureField` 並傳遞下列值：

   * 此 `BLOB` 儲存包含要修改之簽名欄位的PDF檔案的物件
   * 字串值，指定簽名欄位的名稱
   * 此 `PDFSignatureFieldProperties` 儲存簽章欄位鎖定字典和種子值字典資訊的物件

   此 `modifySignatureField` 方法傳回 `BLOB` 物件，用來儲存包含已修改簽名欄位的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式並傳遞字串值，該字串值代表將包含簽名欄位的PDF檔案的檔案位置，以及開啟檔案的模式。
   * 建立位元組陣列，儲存 `BLOB` 物件， `addSignatureField` 方法會傳回。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署PDF檔案 {#digitally-signing-pdf-documents}

數位簽章可套用至PDF檔案，以提供安全等級。 數位簽章（例如手寫簽章）提供簽署者識別自己並對檔案發表宣告的方法。 用於數位簽署檔案的技術有助於確保簽署者和收件者都清楚已簽署的內容，並且確信檔案在簽署後未曾變更。

PDF檔案是以公開金鑰技術簽署。 簽署者有兩個金鑰：公開金鑰和私密金鑰。 私密金鑰會儲存在使用者的認證中，在簽署時必須可供使用。 公開金鑰儲存在使用者的憑證中，收件人必須可以使用它來驗證簽名。 憑證撤銷清單(CRL)和線上憑證狀態通訊協定(OCSP)回應(由憑證授權單位(CA)發佈)中會提供關於撤銷憑證的資訊。 簽署時間可從稱為時間戳記授權單位的可信來源取得。

>[!NOTE]
>
>您必須確定將憑證新增至AEM Forms，才能數位簽署PDF檔案。 憑證是使用管理控制檯或使用Trust Manager API以程式設計方式新增。 (請參閱 [使用信任管理員API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

您可以以程式設計方式數位簽署PDF檔案。 數位簽署PDF檔案時，您必須參考AEM Forms中存在的安全性認證。 認證是用於簽署的私密金鑰。

簽章服務會在簽署PDF檔案時執行下列步驟：

1. Signature service會傳遞要求中指定的別名，從Truststore擷取認證。
1. 信任庫會搜尋指定的認證。
1. 認證會傳回至簽章服務，並用來簽署檔案。 也會針對別名快取認證，以供日後請求使用。

如需有關處理安全性認證的資訊，請參閱 *安裝和部署AEM Forms* 應用程式伺服器的指南。

>[!NOTE]
>
>簽署和認證檔案之間存在差異。 (請參閱 [認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>並非所有PDF檔案都支援簽署。 如需有關簽名服務和數位簽署檔案的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Signature服務不支援內嵌PDF資料的XDP檔案作為作業的輸入，例如證明檔案。 此動作會導致簽名服務擲回 `PDFOperationException`. 若要解決此問題，請使用PDF公用程式服務，將XDP檔案轉換為PDF檔案，然後將轉換的PDF檔案傳遞至簽名服務作業。 (請參閱 [使用PDF公用程式](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**nCipher nShield HSM認證**

使用nCipher nShield HSM認證簽署或認證PDF檔案時，必須重新啟動AEM Forms部署所在的J2EE應用程式伺服器，才能使用新的認證。 不過，您可以設定組態值，使簽署或認證作業正常運作，而不需重新啟動J2EE應用程式伺服器。

您可以在cknfastrc檔案中新增下列設定值，該檔案位於/opt/nfast/cknfastrc （或c：\nfast\cknfastrc）：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此組態值新增至cknfastrc檔案之後，您就可以使用新的認證，而不需重新啟動J2EE應用程式伺服器。

**簽章不受信任**

當認證和簽署相同的PDF檔案時，如果認證簽名不受信任，則在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名旁邊會出現一個黃色三角形。 必須信任憑證簽章才能避免這種情況。

**簽署以XFA為基礎的表格**

如果您嘗試使用簽名服務API簽署以XFA為基礎的表單，則可能遺漏以下專案中的資料： `View` `Signed` `Version` 位於Acrobat。 例如，請考量下列工作流程：

* 使用使用Designer建立的XDP檔案，合併包含簽名欄位的表單設計以及包含表單資料的XML資料。 您可以使用Forms服務產生互動式PDF檔案。
* 您可以使用Signature service API簽署PDF檔案。

### 步驟摘要 {#summary_of_steps-3}

若要數位簽署PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章服務使用者端。
1. 取得要簽署的PDF檔案。
1. 簽署PDF檔案。
1. 將已簽署的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立簽名使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得要簽署的PDF檔案**

若要簽署PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法簽名。 簽名欄位可透過使用設計工具或以程式設計方式新增。

**簽署PDF檔案**

簽署PDF檔案時，您可以設定簽名服務使用的執行階段選項。 您可以設定下列選項：

* 外觀選項
* 撤銷檢查
* 時間戳記值

您可使用 `PDFSignatureAppearanceOptionSpec` 物件。 例如，您可以透過叫用 `PDFSignatureAppearanceOptionSpec` 物件的 `setShowDate` 方法與傳遞 `true`.

您也可以指定是否要執行撤銷檢查，以判斷用於數位簽署PDF檔案的憑證是否已撤銷。 若要執行撤銷檢查，您可以指定下列其中一個值：

* **NoCheck**：不執行撤銷檢查。
* **BestEfort**：一律嘗試檢查鏈結中所有憑證的撤銷。 如果檢查時發生任何問題，系統會假設撤銷有效。 如果發生任何失敗，則假設憑證未被撤銷。
* **CheckIfAvailable：** 如果有可用的撤銷資訊，則檢查鏈結中所有憑證的撤銷。 如果檢查時發生任何問題，則會假設撤銷無效。 如果發生任何失敗，假設憑證被撤銷且無效。 （這是預設值。）
* **AlwaysCheck**：檢查鏈結中所有憑證的撤銷。 如果任何憑證中都沒有撤銷資訊，則會假設撤銷無效。

若要對憑證執行撤銷檢查，您可以使用 `CRLOptionSpec` 物件。 不過，如果您要執行撤銷檢查但未指定CRL伺服器的URL，則簽章服務會從憑證取得該URL。

執行撤銷檢查時，您可以使用線上憑證狀態通訊協定(OCSP)伺服器，而不使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，撤銷檢查的執行速度會更快。 (請參閱「線上憑證狀態通訊協定」，網址為 [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

您可以使用Adobe應用程式和服務來設定Signature服務使用的CRL和OCSP伺服器順序。 例如，如果先在Adobe應用程式和服務中設定OCSP伺服器，則會檢查OCSP伺服器，然後檢查CRL伺服器。 （請參閱AAC說明中的「使用信任存放區管理憑證和認證」）。

如果您指定不執行撤銷檢查，則Signature service不會檢查用於簽署或證明檔案的憑證是否已撤銷。 也就是說，會忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>雖然您可以在憑證中指定CRL或OCSP伺服器，但您可以使用 `CRLOptionSpec` 和 `OCSPOptionSpec` 物件。 例如，若要覆寫CRL伺服器，您可以叫用 `CRLOptionSpec` 物件的 `setLocalURI` 方法。

時間戳記是指追蹤已簽署或已驗證檔案修改時間的程式。 檔案簽署後即不應修改，即使檔案擁有者亦然。 時間戳記有助於強制實施已簽署或已驗證檔案的有效性。 您可以使用設定時間戳記選項 `TSPOptionSpec` 物件。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務逐步瀏覽區段及對應的快速啟動中，會使用撤銷檢查。 因為未指定CRL或OCSP伺服器資訊，所以伺服器資訊會從用來數位簽署PDF檔案的憑證取得。

若要成功簽署PDF檔案，您可以指定包含數位簽章之簽章欄位的完整名稱，例如 `form1[0].#subform[1].SignatureField3[3]`. 使用XFA表單欄位時，也可使用簽名欄位的部分名稱： `SignatureField3[3]`.

您也必須參考安全性認證，才能數位簽署PDF檔案。 若要參照安全性認證，請指定別名。 別名是實際認證的參考，可能位於PKCS#12檔案（具有.pfx副檔名）或硬體安全模組(HSM)中。 如需安全性認證的相關資訊，請參閱 *安裝和部署AEM Forms* 應用程式伺服器的指南。

**儲存已簽署的PDF檔案**

簽名服務以數位方式簽署PDF檔案後，您可以將檔案儲存為PDF檔案，讓使用者可在Acrobat或Adobe Reader中開啟檔案。

**另请参阅**

[使用Java API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用Web服務API數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

[正在擷取簽章欄位名稱](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API數位簽署PDF檔案 {#digitally-sign-pdf-documents-using-the-java-api}

使用簽名API (Java)數位簽署PDF檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 取得要簽署的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表要數位簽名的PDF檔案，使用它的建構函式並傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 簽署PDF檔案

   叫用PDF檔案以簽署 `SignatureServiceClient` 物件的 `sign` 並傳遞下列值：

   * A `com.adobe.idp.Document` 代表要簽署之PDF檔案的物件。
   * 字串值，代表將包含數位簽章之簽章欄位的名稱。
   * A `Credential` 物件，代表用來數位簽署PDF檔案的認證。 建立 `Credential` 物件(透過叫用 `Credential` 物件的靜態 `getInstance` 和傳遞字串值，字串值會指定對應至安全性認證的別名值。
   * A `HashAlgorithm` 指定靜態資料成員的物件，代表用來摘要PDF檔案的雜湊演演算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1演演算法。
   * 字串值，代表PDF檔案經過數位簽署的原因。
   * 代表簽署者聯絡資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數位簽章外觀的物件。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * A `java.lang.Boolean` 指定是否對簽署者的憑證執行撤銷檢查的物件。
   * 一個 `OCSPOptionSpec` 儲存線上憑證狀態通訊協定(OCSP)支援偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `CRLPreferences` 儲存憑證撤銷清單(CRL)偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳記提供者(TSP)支援之偏好設定的物件。 此引數為選用引數，可以是 `null`. 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   此 `sign` 方法傳回 `com.adobe.idp.Document` 代表已簽署PDF檔案的物件。

1. 儲存已簽署的PDF檔案

   * 建立 `java.io.File` 物件，並確認副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 方法與傳遞 `java.io.File`以複製 `Document` 物件至檔案。 確保您使用 `com.adobe.idp.Document` 物件，由 `sign` 方法。

**另请参阅**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入門（SOAP模式）：使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API數位簽署PDF檔案 {#digitally-signing-pdf-documents-using-the-web-service-api}

若要使用Signature API （Web服務）數位簽署PDF檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得要簽署的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存已簽署的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表要簽署之PDF檔案的檔案位置，以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 屬性位元組陣列的內容。

1. 簽署PDF檔案

   叫用PDF檔案以簽署 `SignatureServiceClient` 物件的 `sign` 並傳遞下列值：

   * A `BLOB` 代表要簽署之PDF檔案的物件。
   * 字串值，代表將包含數位簽章之簽章欄位的名稱。
   * A `Credential` 物件，代表用來數位簽署PDF檔案的認證。 建立 `Credential` 物件，使用它的建構函式，並透過指派值給 `Credential` 物件的 `alias` 屬性。
   * A `HashAlgorithm` 指定靜態資料成員的物件，代表用來摘要PDF檔案的雜湊演演算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1演演算法。
   * Boolean值，指定是否使用雜湊演演算法。
   * 字串值，代表PDF檔案經過數位簽署的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數位簽章外觀的物件。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * A `System.Boolean` 指定是否對簽署者的憑證執行撤銷檢查的物件。 如果完成此撤銷檢查，則會嵌入簽名中。 默认为 `false`。
   * 一個 `OCSPOptionSpec` 儲存線上憑證狀態通訊協定(OCSP)支援偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`. 如需此物件的相關資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 儲存憑證撤銷清單(CRL)偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳記提供者(TSP)支援之偏好設定的物件。 此引數為選用引數，可以是 `null`.

   此 `sign` 方法傳回 `BLOB` 代表已簽署PDF檔案的物件。

1. 儲存已簽署的PDF檔案

   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表已簽署PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `sign` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 數位簽署互動式Forms {#digitally-signing-interactive-forms}

您可以簽署Forms服務建立的互動式表單。 例如，請考量下列工作流程：

* 您可以使用Designer建立的XFAPDF表單，與使用Forms服務位於XML檔案中的表單資料合併。 Forms伺服器會轉譯互動式表單。
* 您可以使用Signature service API簽署互動式表單。

結果會是數位簽署的互動式PDF表單。 在簽署以XFA表單為基礎的PDF表單時，請確定您將PDF檔案儲存為Adobe靜態PDF表單。 如果您嘗試簽署儲存為PDF動態PDF表單的Adobe表單，則會發生例外狀況。 由於您簽署的是從Forms服務傳回的表單，因此請確保表單包含簽名欄位。

>[!NOTE]
>
>您必須確定將憑證新增至AEM Forms，才能以數位方式簽署互動式表單。 憑證是使用管理控制檯或使用Trust Manager API以程式設計方式新增。 (請參閱 [使用信任管理員API匯入認證](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

使用Forms Service API時，請將 `GenerateServerAppearance` 執行階段選項 `true`. 此執行階段選項可確保伺服器上產生的表單外觀在Acrobat或Adobe Reader中開啟時保持有效。 產生互動式表單以使用Forms API簽署時，建議您設定此執行階段選項。

>[!NOTE]
>
>閱讀數位簽署互動式Forms之前，建議您先熟悉簽署PDF檔案。 (請參閱 [數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### 步驟摘要 {#summary_of_steps-4}

若要數位簽署Forms服務傳回的互動式表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms和簽名使用者端。
1. 使用Forms服務取得互動式表單。
1. 簽署互動式表單。
1. 將已簽署的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立Forms和簽名使用者端**

由於此工作流程會同時叫用Forms和簽名服務，因此請建立Forms服務使用者端和簽名服務使用者端。

**使用Forms服務取得互動式表單**

您可以使用Forms服務來取得要簽署的互動式PDF表單。 自AEM Forms起，您可以傳遞 `com.adobe.idp.Document` 物件重新命名為Forms服務，其中包含要轉譯的表單。 此方法的名稱為 `renderPDFForm2`. 此方法會傳回 `com.adobe.idp.Document` 包含要簽署的表單的物件。 您可以傳遞此 `com.adobe.idp.Document` 簽章服務的執行個體。

同樣地，如果您使用Web服務，您可以傳遞 `BLOB` Forms服務傳回至簽名服務的執行個體。

>[!NOTE]
>
>與「數位簽署互動式Forms」區段相關的快速入門會叫用 `renderPDFForm2` 方法。

**簽署互動式表單**

簽署PDF檔案時，您可以設定Signature service使用的執行階段選項。 您可以設定下列選項：

* 外觀選項
* 撤銷檢查
* 時間戳記值

您可使用 `PDFSignatureAppearanceOptionSpec` 物件。 例如，您可以透過叫用 `PDFSignatureAppearanceOptionSpec` 物件的 `setShowDate` 方法與傳遞 `true`.

**儲存已簽署的PDF檔案**

簽名服務以數位方式簽署PDF檔案後，您可以將其儲存為PDF檔案。 PDF檔案可在Acrobat或Adobe Reader中開啟。

**另请参阅**

[使用Java API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用Web服務API數位簽署互動式表單](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[數位簽署PDF檔案](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[呈現互動式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API數位簽署互動式表單 {#digitally-sign-an-interactive-form-using-the-java-api}

使用Forms和簽名API (Java)數位簽署互動式表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 建立Forms和簽名使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 使用Forms服務取得互動式表單

   * 建立 `java.io.FileInputStream` 物件，代表要透過其建構函式傳遞至Forms服務的PDF檔案。 傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。
   * 建立 `java.io.FileInputStream` 物件，代表包含表單資料的XML檔案，以使用它的建構函式傳遞至Forms服務。 傳遞指定XML檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。
   * 建立 `PDFFormRenderSpec` 用來設定執行階段選項的物件。 叫用 `PDFFormRenderSpec` 物件的 `setGenerateServerAppearance` 方法與傳遞 `true`.
   * 叫用 `FormsServiceClient` 物件的 `renderPDFForm2` 方法並傳遞下列值：

      * A `com.adobe.idp.Document` 包含要呈現之PDF表單的物件。
      * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。
      * A `PDFFormRenderSpec` 儲存執行階段選項的物件。
      * A `URLSpec` 包含Forms服務所需URI值的物件。 您可以指定 `null` （此引數值）。
      * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

      此 `renderPDFForm2` 方法傳回 `FormsResult` 包含表單資料流的物件

   * 透過叫用「 」擷取PDF表單 `FormsResult` 物件的 `getOutputContent` 方法。 此方法會傳回 `com.adobe.idp.Document` 代表互動式表單的物件。


1. 簽署互動式表單

   叫用PDF檔案以簽署 `SignatureServiceClient` 物件的 `sign` 並傳遞下列值：

   * A `com.adobe.idp.Document` 代表要簽署之PDF檔案的物件。 確定此物件為 `com.adobe.idp.Document` 物件(從Forms服務取得)。
   * 代表已簽署之簽名欄位名稱的字串值。
   * A `Credential` 物件，代表用來數位簽署PDF檔案的認證。 建立 `Credential` 物件(透過叫用 `Credential` 物件的靜態 `getInstance` 方法。 傳遞字串值，指定與安全性認證對應的別名值。
   * A `HashAlgorithm` 指定靜態資料成員的物件，代表用來摘要PDF檔案的雜湊演演算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1演演算法。
   * 字串值，代表PDF檔案經過數位簽署的原因。
   * 代表簽署者聯絡資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數位簽章外觀的物件。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * A `java.lang.Boolean` 指定是否對簽署者的憑證執行撤銷檢查的物件。
   * 一個 `OCSPPreferences` 儲存線上憑證狀態通訊協定(OCSP)支援偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `CRLPreferences` 儲存憑證撤銷清單(CRL)偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳記提供者(TSP)支援之偏好設定的物件。 此引數為選用引數，可以是 `null`.

   此 `sign` 方法傳回 `com.adobe.idp.Document` 代表已簽署PDF檔案的物件。

1. 儲存已簽署的PDF檔案

   * 建立 `java.io.File` 物件，並確認副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 方法與傳遞 `java.io.File`以複製 `Document` 物件至檔案。 確保您使用 `com.adobe.idp.Document` 物件， `sign` 方法已傳回。

**另请参阅**

[數位簽署互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入門（SOAP模式）：使用Java API數位簽署PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API數位簽署互動式表單 {#digitally-sign-an-interactive-form-using-the-web-service-api}

使用Forms和簽名API （Web服務）數位簽署互動式表單：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 由於此使用者端應用程式會叫用兩個AEM Forms服務，請建立兩個服務參考。 對與Signature服務相關聯的服務參照使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   使用下列WSDL定義作為與Forms服務相關聯的服務參考： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   因為 `BLOB` 資料型別對兩個服務參考都是通用的，完全限定 `BLOB` 使用時的資料型別。 在對應的Web服務快速入門中，全部 `BLOB` 執行個體已完整合格。

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Forms和簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >對Forms服務使用者端重複這些步驟。

1. 使用Forms服務取得互動式表單

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存已簽署的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表要簽署之PDF檔案的檔案位置，以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 屬性位元組陣列的內容。
   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存表單資料。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表包含表單資料之XML檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 屬性位元組陣列的內容。
   * 建立 `PDFFormRenderSpec` 用來設定執行階段選項的物件。 指派值 `true` 至 `PDFFormRenderSpec` 物件的 `generateServerAppearance` 欄位。
   * 叫用 `FormsServiceClient` 物件的 `renderPDFForm2` 方法並傳遞下列值：

      * A `BLOB` 包含要呈現之PDF表單的物件。
      * A `BLOB` 包含要與表單合併之資料的物件。
      * A `PDFFormRenderSpec` 儲存執行階段選項的物件。
      * A `URLSpec` 包含Forms服務所需URI值的物件。 您可以指定 `null` （此引數值）。
      * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。
      * 用於儲存表單中頁數的長輸出引數。
      * 用於地區設定值的字串輸出引數。
      * A `FormResult` 用來儲存互動式表單的輸出引數值。
   * 叫用「 」以擷取PDF表單 `FormsResult` 物件的 `outputContent` 欄位。 此欄位會儲存 `BLOB` 代表互動式表單的物件。


1. 簽署互動式表單

   叫用PDF檔案以簽署 `SignatureServiceClient` 物件的 `sign` 並傳遞下列值：

   * A `BLOB` 代表要簽署之PDF檔案的物件。 使用 `BLOB` Forms服務傳回的執行個體。
   * 代表已簽署之簽名欄位名稱的字串值。
   * A `Credential` 物件，代表用來數位簽署PDF檔案的認證。 建立 `Credential` 物件，使用它的建構函式，並透過指派值給 `Credential` 物件的 `alias` 屬性。
   * A `HashAlgorithm` 指定靜態資料成員的物件，代表用來摘要PDF檔案的雜湊演演算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1演演算法。
   * Boolean值，指定是否使用雜湊演演算法。
   * 字串值，代表PDF檔案經過數位簽署的原因。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * A `PDFSignatureAppearanceOptions` 控制數位簽章外觀的物件。 例如，您可以使用此物件將自訂標誌新增至數位簽名。
   * A `System.Boolean` 指定是否對簽署者的憑證執行撤銷檢查的物件。 如果完成此撤銷檢查，則會嵌入簽名中。 默认为 `false`。
   * 一個 `OCSPPreferences` 儲存線上憑證狀態通訊協定(OCSP)支援偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`. 如需此物件的相關資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 儲存憑證撤銷清單(CRL)偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳記提供者(TSP)支援之偏好設定的物件。 此引數為選用引數，可以是 `null`.

   此 `sign` 方法傳回 `BLOB` 代表已簽署PDF檔案的物件。

1. 儲存已簽署的PDF檔案

   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表已簽署PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `sign` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[數位簽署互動式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 認證PDF檔案 {#certifying-pdf-documents}

您可以使用稱為認證簽名的特定簽名型別來認證PDF檔案，以保護檔案安全。 認證簽名與數位簽名的區別如下：

* 它必須是套用至PDF檔案的第一個簽章；也就是說，在套用已驗證簽章時，檔案中的任何其他簽章欄位都必須未簽署。 PDF檔案中只允許一個已驗證的簽章。 如果您想要簽署和認證PDF檔案，您必須在簽署之前先認證它。 在您認證PDF檔案後，您可以數位簽署其他簽名欄位。
* 檔案的作者或建立者可以指定檔案可以特定方式修改，而不會使已驗證的簽名失效。 例如，檔案可能允許填寫表單或新增註釋。 如果作者指定不允許特定修改，Acrobat會限制使用者不得以這種方式修改檔案。 如果已進行此類修改（例如使用其他應用程式），則認證簽名無效，且Acrobat會在使用者開啟檔案時發出警告。 （使用未經認證的簽名，不會阻止修改，正常的編輯操作也不會使原始簽名失效。）
* 簽署時，會掃描檔案以找出可能使檔案內容含糊或誤導的特定內容型別。 例如，註解可能會遮蔽頁面上的一些文字，而這些文字對瞭解正在認證的內容非常重要。 可提供此類內容的說明（法律證明）。

您可以使用簽名服務Java API或簽名Web服務API，以程式設計方式認證PDF檔案。 在認證PDF檔案時，您必須參考存在於認證服務中的安全性認證。 如需安全性認證的相關資訊，請參閱 *安裝和部署AEM Forms* 應用程式伺服器的指南。

>[!NOTE]
>
>當認證和簽署相同的PDF檔案時，如果認證簽名不受信任，當您在Acrobat或Adobe Reader中開啟PDF檔案時，第一個簽名簽名旁邊會出現一個黃色三角形。 必須信任認證簽章以避免這種情況。

>[!NOTE]
>
>使用nCipher nShield HSM認證來簽署或認證PDF檔案時，必須重新啟動部署AEM Forms的J2EE應用程式伺服器，才能使用新的認證。 不過，您可以設定組態值，使簽署或認證作業正常運作，而不需重新啟動J2EE應用程式伺服器。

您可以在cknfastrc檔案中新增下列設定值，該檔案位於/opt/nfast/cknfastrc （或c：\nfast\cknfastrc）：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

將此組態值新增至cknfastrc檔案之後，您就可以使用新的認證，而不需重新啟動J2EE應用程式伺服器。

>[!NOTE]
>
>如需有關簽名服務與證明檔案的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-5}

若要認證PDF檔案，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得要認證的PDF檔案。
1. 認證PDF檔案。
1. 將認證的PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名使用者端**

您必須先建立簽名使用者端，才能以程式設計方式執行簽名作業。

**取得PDF檔案以認證**

若要認證PDF檔案，您必須取得包含簽名欄位的PDF檔案。 如果PDF檔案不包含簽名欄位，則無法認證。 簽名欄位可透過使用設計工具或以程式設計方式新增。 如需以程式設計方式新增簽名欄位的資訊，請參閱 [新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields).

**認證PDF檔案**

若要成功認證PDF檔案，您需要下列輸入值，這些值由簽名服務用來認證PDF檔案：

* **PDF檔案**：包含簽名欄位的PDF檔案，簽名欄位是包含已驗證簽名的圖形表示的表單欄位。 PDF檔案必須先包含簽名欄位，才能進行認證。 簽名欄位可透過使用設計工具或以程式設計方式新增。 (請參閱 [新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **簽章欄位名稱**：已驗證的簽名欄位的完整名稱。 以下值為範例： `form1[0].#subform[1].SignatureField3[3]`. 使用XFA表單欄位時，也可使用簽名欄位的部分名稱： `SignatureField3[3]`. 如果為欄位名稱傳遞null值，則會動態建立並驗證不可見的簽章欄位。
* **安全性認證**：用於認證PDF檔案的認證。 此安全性認證包含密碼和別名，必須與Credential服務內認證中顯示的別名相符。 別名是實際認證的參考，可能位於PKCS#12檔案（具有.pfx副檔名）或硬體安全模組(HSM)中。
* **雜湊演演算法**：用於摘要PDF檔案的雜湊演演算法。
* **簽署原因**：顯示在Acrobat或Adobe Reader中的值，讓其他使用者知道PDF檔案獲得認證的原因。
* **簽署者的位置**：認證所指定的簽署者位置。
* **連絡資訊**：簽署者的聯絡資訊，例如地址和電話號碼。
* **許可權資訊**：控制一般使用者可在檔案上執行的動作，而不會導致已驗證簽名無效的許可權。 例如，您可以設定許可權，以便對PDF檔案所做的任何變更都會導致認證簽名無效。
* **法律說明**：當檔案通過驗證時，會自動掃描特定型別的內容，這可能會使檔案的內容含糊或誤導使用者。 例如，註解可能會遮蔽頁面上的一些文字，而這些文字對瞭解正在認證的內容非常重要。 掃描程式會產生有關這些內容型別的警告。 此值提供可能產生警告之內容的額外說明。
* **外觀選項**：控制已驗證簽章外觀的選項。 例如，已驗證的簽章可顯示日期資訊。
* **撤銷檢查**：此值會指定是否對簽署者的憑證執行撤銷檢查。 的預設設定 `false` 表示尚未執行撤銷檢查。
* **OCSP設定**：線上憑證狀態通訊協定(OCSP)支援的設定，此設定提供有關用於認證PDF檔案的認證狀態的資訊。 例如，您可以指定伺服器的URL，以提供您用來登入PDF檔案的認證相關資訊。
* **CRL設定**：憑證撤銷清單(CRL)偏好設定的設定（如果已執行撤銷檢查）。 例如，您可以指定一律檢查認證是否被撤銷。
* **時間戳記**：定義套用至已驗證簽章的時間戳記資訊的設定。 時間戳記表示特定資料是在特定時間之前建立的。 此知識有助於在簽署者和驗證者之間建立信任關係。

**將認證的PDF檔案儲存為PDF檔案**

簽名服務驗證PDF檔案後，您可以將其儲存為PDF檔案，以便使用者可以在Acrobat或Adobe Reader中開啟它。

**另请参阅**

[使用Java API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用Web服務API認證PDF檔案](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API認證PDF檔案 {#certify-pdf-documents-using-the-java-api}

使用簽名API (Java)認證PDF檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 取得PDF檔案以認證

   * 建立 `java.io.FileInputStream` 物件，代表要透過使用其建構函式並傳遞指定PDF檔案位置的字串值來認證的PDF檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 認證PDF檔案

   PDF透過叫用 `SignatureServiceClient` 物件的 `certify` 並傳遞下列值：

   * 此 `com.adobe.idp.Document` 代表要認證之PDF檔案的物件。
   * 字串值，代表將包含簽章的簽章欄位名稱。
   * A `Credential` 物件，代表用來認證PDF檔案的認證。 建立 `Credential` 物件(透過叫用 `Credential` 物件的靜態 `getInstance` 和傳遞字串值，字串值會指定對應至安全性認證的別名值。
   * A `HashAlgorithm` 指定靜態資料成員的物件，代表用於摘要PDF檔案的雜湊演演算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1演演算法。
   * 代表PDF檔案獲得認證之原因的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * A `MDPPermissions` 物件，指定可在使簽章失效的PDF檔案上執行的動作。
   * A `PDFSignatureAppearanceOptions` 控制認證簽名外觀的物件。 如有需要，請叫用方法修改簽章的外觀，例如 `setShowDate`.
   * 字串值，說明哪些動作會使簽章失效。
   * A `java.lang.Boolean` 指定是否對簽署者的憑證執行撤銷檢查的物件。 如果完成此撤銷檢查，則會嵌入簽名中。 默认为 `false`。
   * A `java.lang.Boolean` 指定正在驗證的簽章欄位是否已鎖定的物件。 如果欄位已鎖定，則簽章欄位會標示為唯讀，其屬性無法修改，且沒有必要許可權的任何人都無法清除。 默认为 `false`。
   * 一個 `OCSPPreferences` 儲存線上憑證狀態通訊協定(OCSP)支援偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`. 如需此物件的相關資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 儲存憑證撤銷清單(CRL)偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳記提供者(TSP)支援之偏好設定的物件。 例如，在您建立 `TSPPreferences` 物件，您可以呼叫 `TSPPreferences` 物件的 `setTspServerURL` 方法。 此引數為選用引數，可以是 `null`. 如需詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

   此 `certify` 方法傳回 `com.adobe.idp.Document` 代表已驗證PDF檔案的物件。

1. 將認證的PDF檔案儲存為PDF檔案

   * 建立 `java.io.File` 物件，並確認副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件至檔案。

**另请参阅**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入門（SOAP模式）：使用Java API認證PDF檔案](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API認證PDF檔案 {#certify-pdf-documents-using-the-web-service-api}

使用簽名API （Web服務）認證PDF檔案：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得PDF檔案以認證

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存已驗證的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式並傳遞字串值，該字串值代表PDF檔案要認證的檔案位置，以及開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 資料成員位元組陣列的內容。

1. 認證PDF檔案

   PDF透過叫用 `SignatureServiceClient` 物件的 `certify` 並傳遞下列值：

   * 此 `BLOB` 代表要認證之PDF檔案的物件。
   * 字串值，代表將包含簽章的簽章欄位名稱。
   * A `Credential` 物件，代表用來認證PDF檔案的認證。 建立 `Credential` 物件，並透過指派值給 `Credential` 物件的 `alias` 屬性。
   * A `HashAlgorithm` 指定靜態資料成員的物件，代表用於摘要PDF檔案的雜湊演演算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1演演算法。
   * Boolean值，指定是否使用雜湊演演算法。
   * 代表PDF檔案獲得認證之原因的字串值。
   * 代表簽署者位置的字串值。
   * 代表簽署者聯絡資訊的字串值。
   * 一個 `MDPPermissions` 物件的靜態資料成員，指定可在PDF檔案上執行的使簽名失效的動作。
   * Boolean值，指定是否使用 `MDPPermissions` 作為上一個引數值傳遞的物件。
   * 字串值，說明哪些動作會使簽章失效。
   * A `PDFSignatureAppearanceOptions` 控制認證簽名外觀的物件。 建立 `PDFSignatureAppearanceOptions` 物件（使用其建構函式）。 您可以藉由設定特徵碼的其中一個資料成員來修改特徵碼的外觀。
   * A `System.Boolean` 指定是否對簽署者的憑證執行撤銷檢查的物件。 如果完成此撤銷檢查，則會嵌入簽名中。 默认为 `false`。
   * A `System.Boolean` 指定正在驗證的簽章欄位是否已鎖定的物件。 如果欄位已鎖定，則簽章欄位會標示為唯讀，其屬性無法修改，且沒有必要許可權的任何人都無法清除。 默认为 `false`。
   * A `System.Boolean` 指定簽章欄位是否鎖定的物件。 也就是說，如果您通過 `true` 至上一個引數，然後傳遞 `true` 至此引數。
   * 一個 `OCSPPreferences` 此物件儲存線上憑證狀態通訊協定(OCSP)支援的偏好設定，可提供用於認證PDF檔案的認證狀態相關資訊。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `CRLPreferences` 儲存憑證撤銷清單(CRL)偏好設定的物件。 如果未完成撤銷檢查，則不會使用此引數，而且您可以指定 `null`.
   * A `TSPPreferences` 儲存時間戳記提供者(TSP)支援之偏好設定的物件。 例如，在您建立 `TSPPreferences` 物件，您可以設定TSP的URL `TSPPreferences` 物件的 `tspServerURL` 資料成員。 此引數為選用引數，可以是 `null`.

   此 `certify` 方法傳回 `BLOB` 代表已驗證PDF檔案的物件。

1. 將認證的PDF檔案儲存為PDF檔案

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式並傳遞字串值，該字串值代表將包含已驗證PDF檔案的PDF檔案的檔案位置，以及開啟檔案的模式。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `certify` 方法。 透過取得 `BLOB` 物件的 `binaryData` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[認證PDF檔案](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證數位簽名 {#verifying-digital-signatures}

可以驗證數位簽章，以確保已簽署的PDF檔案未被修改且數位簽章有效。 驗證數位簽章時，您可以檢查簽章的狀態和簽章的屬性，例如簽署者的身分。 在信任數位簽名之前，建議您先驗證它。 驗證數位簽名時，請參考包含數位簽名的PDF檔案。

假設簽署者的身分不明。 當您在Acrobat中開啟PDF檔案時，會出現一則警告訊息，指出簽署者的身分不明，如下圖所示。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同樣地，當您以程式設計方式驗證數位簽名時，您可以判斷簽名者的身分狀態。 例如，如果您驗證上圖所示檔案中的數位簽名，結果會是簽名者的身分不明。

>[!NOTE]
>
>如需有關簽名服務和驗證數位簽名的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-6}

若要驗證數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含要驗證之簽名的PDF檔案。
1. 設定PKI執行階段選項。
1. 驗證數位簽名。
1. 判斷簽章的狀態。
1. 判斷簽署者的身分。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名使用者端**

以程式設計方式執行簽名服務操作之前，請先建立簽名服務使用者端。

**取得包含要驗證之簽名的PDF檔案**

若要驗證用於數位簽署或認證PDF檔案的簽名，請取得包含簽名的PDF檔案。

**設定PKI執行階段選項**

設定Signature service在PDF檔案中驗證簽名時所使用的PKI執行階段選項：

* 驗證時間
* 撤銷檢查
* 時間戳記值

在設定這些選項時，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），以指出要使用目前時間。 如需不同時間值的詳細資訊，請參閱 `VerificationTime` 列舉值於 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

您也可以指定是否在驗證程式中執行撤銷檢查。 例如，您可以執行撤銷檢查來決定是否撤銷憑證。 有關撤銷檢查選項的資訊，請參閱 `RevocationCheckStyle` 列舉值於 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

若要對憑證執行撤銷檢查，請使用 `CRLOptionSpec` 物件。 不過，如果您未指定CRL伺服器的URL，則簽章服務會從憑證中取得該URL。

執行撤銷檢查時，您可以使用線上憑證狀態通訊協定(OCSP)伺服器，而不使用CRL伺服器。 通常，當使用OCSP伺服器而不是CRL伺服器時，撤銷檢查的執行速度會更快。 (請參閱 [線上憑證狀態通訊協定](https://tools.ietf.org/html/rfc2560).)

您可以使用Adobe應用程式和服務來設定Signature服務使用的CRL和OCSP伺服器順序。 例如，如果先在Adobe應用程式和服務中設定OCSP伺服器，則會檢查OCSP伺服器，然後檢查CRL伺服器。

如果您未執行撤銷檢查，Signature service就不會檢查憑證是否被撤銷。 也就是說，會忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用覆寫憑證中指定的URL `CRLOptionSpec` 和 `OCSPOptionSpec` 物件。 例如，若要覆寫CRL伺服器，您可以叫用 `CRLOptionSpec` 物件的 `setLocalURI` 方法。

時間戳記是追蹤已簽署或已驗證檔案修改時間的程式。 檔案簽署後，任何人都無法修改。 時間戳記有助於強制實施已簽署或已驗證檔案的有效性。 您可以使用設定時間戳記選項 `TSPOptionSpec` 物件。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間設定為 `VerificationTime.CURRENT_TIME` 且撤銷檢查設為 `RevocationCheckStyle.BestEffort`. 因為未指定CRL或OCSP伺服器資訊，所以會從憑證取得伺服器資訊。

**驗證數位簽名**

若要成功驗證簽名，請指定包含簽名的簽名欄位的完整名稱，例如 `form1[0].#subform[1].SignatureField3[3]`. 使用XFA表單欄位時，您還可以使用簽名欄位的部分名稱： `SignatureField3`.

依預設，簽名服務將驗證後檔案可簽署的時間限製為65分鐘。 如果使用者嘗試在目前時間驗證簽名，且簽署時間晚於目前時間且在65分鐘內，則簽名服務不會建立驗證錯誤。

>[!NOTE]
>
>有關驗證簽名時所需的其他值，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**判斷簽章的狀態**

在驗證數位簽章時，您可以檢查簽章的狀態。

**判斷簽署者的身分**

您可以決定簽署者的身分，身分可以是下列其中一個值：

* **未知**：此簽署者不明，因為無法執行簽署者驗證。
* **受信任**：此簽署者值得信任。
* **不受信任**：此簽署者不受信任。

**另请参阅**

[使用Java API驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[使用Web服務API驗證數位簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證數位簽名 {#verify-digital-signatures-using-the-java-api}

使用Signature Service API (Java)驗證數位簽名：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 取得包含要驗證之簽名的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表包含簽名的PDF檔案，以使用它的建構函式進行驗證。 傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定PKI執行階段選項

   * 建立 `PKIOptions` 物件（使用其建構函式）。
   * 透過叫用設定驗證時間 `PKIOptions` 物件的 `setVerificationTime` 方法和傳遞 `VerificationTime` 指定驗證時間的列舉值。
   * 透過叫用設定撤銷檢查選項 `PKIOptions` 物件的 `setRevocationCheckStyle` 方法和傳遞 `RevocationCheckStyle` 指定是否執行撤銷檢查的列舉值。

1. 驗證數位簽名

   透過叫用 `SignatureServiceClient` 物件的 `verify2` 並傳遞下列值：

   * A `com.adobe.idp.Document` 包含數位簽署或認證之PDF檔案的物件。
   * 字串值，代表包含要驗證之簽章的簽章欄位名稱。
   * A `PKIOptions` 包含PKI執行階段選項的物件。
   * A `VerifySPIOptions` 包含SPI資訊的執行個體。 您可以指定 `null` 此引數的。

   此 `verify2` 方法傳回 `PDFSignatureVerificationInfo` 包含可用於驗證數位簽章之資訊的物件。

1. 判斷簽章的狀態

   * 透過叫用 `PDFSignatureVerificationInfo` 物件的 `getStatus` 方法。 此方法會傳回 `SignatureStatus` 指定簽章狀態的物件。 例如，如果未修改已簽署的PDF檔案，則此方法會傳回 `SignatureStatus.DocumentSigNoChanges`.

1. 判斷簽署者的身分

   * 透過叫用 `PDFSignatureVerificationInfo` 物件的 `getSigner` 方法。 此方法會傳回 `IdentityInformation` 物件。
   * 叫用 `IdentityInformation` 物件的 `getStatus` 判斷簽署者身分的方法。 此方法會傳回 `IdentityStatus` 指定身分的列舉值。 例如，如果簽署者受到信任，則此方法會傳回 `IdentityStatus.TRUSTED`.

**另请参阅**

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[快速入門（SOAP模式）：使用Java API驗證數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API驗證數位簽名 {#verify-digital-signatures-using-the-web-service-api}

使用Signature Service API （Web服務）驗證數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得包含要驗證之簽名的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存包含要驗證的數位或認證簽名的PDF檔案。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表已簽署PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 屬性位元組陣列的內容。

1. 設定PKI執行階段選項

   * 建立 `PKIOptions` 物件（使用其建構函式）。
   * 透過指派 `PKIOptions` 物件的 `verificationTime` 資料成員a `VerificationTime` 指定驗證時間的列舉值。
   * 透過指派以下專案設定撤銷檢查選項 `PKIOptions` 物件的 `revocationCheckStyle` 資料成員a `RevocationCheckStyle` 指定是否執行撤銷檢查的列舉值。

1. 驗證數位簽名

   透過叫用 `SignatureServiceClient` 物件的 `verify2` 並傳遞下列值：

   * 此 `BLOB` 包含數位簽署或認證之PDF檔案的物件。
   * 字串值，代表包含要驗證之簽章的簽章欄位名稱。
   * A `PKIOptions` 包含PKI執行階段選項的物件。
   * A `VerifySPIOptions` 包含SPI資訊的執行個體。 您可以指定 `null` 此引數的。

   此 `verify2` 方法傳回 `PDFSignatureVerificationInfo` 包含可用於驗證數位簽章之資訊的物件。

1. 判斷簽章的狀態

   透過取得「 」的值，判斷簽章的狀態 `PDFSignatureVerificationInfo` 物件的 `status` 資料成員。 此資料成員會儲存 `SignatureStatus` 指定簽章狀態的物件。 例如，如果修改已簽署的PDF檔案，則 `status` 資料成員會儲存值 `SignatureStatus.DocumentSigNoChanges`.

1. 判斷簽署者的身分

   * 透過擷取 `PDFSignatureVerificationInfo` 物件的 `signer` 資料成員。 此成員傳回 `IdentityInformation` 物件。
   * 擷取 `IdentityInformation` 物件的 `status` 用於判斷簽署者身分的資料成員。 此資料成員傳回 `IdentityStatus` 指定身分的列舉值。 例如，如果簽署者受到信任，則此成員會傳回 `IdentityStatus.TRUSTED`.

**另请参阅**

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 驗證多個數位簽名 {#verifying-multiple-digital-signatures}

AEM Forms提供可驗證位於PDF檔案中的所有數位簽名的方法。 假設PDF檔案包含多個數位簽名，因為業務流程需要來自多個簽名者的簽名。 例如，假設一項金融交易需要貸款專員和經理的簽名。 您可以使用Signature service Java API或Web服務API來驗證PDF檔案中的所有簽名。 驗證多個數位簽章時，您可以檢查每個簽章的狀態和屬性。 在您信任數位簽名之前，建議您先驗證它。 建議您熟悉驗證單一數位簽名。

>[!NOTE]
>
>如需有關簽名服務和驗證數位簽名的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-7}

若要驗證多個數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含要驗證之簽名的PDF檔案。
1. 設定PKI執行階段選項。
1. 擷取所有數位簽名。
1. 逐一檢視所有簽章。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名使用者端**

以程式設計方式執行簽名服務操作之前，請先建立簽名服務使用者端。

**取得包含要驗證之簽名的PDF檔案**

若要驗證用於數位簽署或認證PDF檔案的簽名，請取得包含簽名的PDF檔案。

**設定PKI執行階段選項**

設定Signature service在驗證PDF檔案中的所有簽名時所使用的下列PKI執行階段選項：

* 驗證時間
* 撤銷檢查
* 時間戳記值

在設定這些選項時，您可以指定驗證時間。 例如，您可以選取目前時間（驗證器電腦上的時間），以指出要使用目前時間。 如需不同時間值的詳細資訊，請參閱 `VerificationTime` 列舉值於 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

您也可以指定是否在驗證程式中執行撤銷檢查。 例如，您可以執行撤銷檢查來決定是否撤銷憑證。 有關撤銷檢查選項的資訊，請參閱 `RevocationCheckStyle` 列舉值於 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

若要對憑證執行撤銷檢查，請使用 `CRLOptionSpec` 物件。 不過，如果您未指定CRL伺服器的URL，則簽章服務會從憑證取得該URL。

執行撤銷檢查時，您可以使用線上憑證狀態通訊協定(OCSP)伺服器，而不使用CRL伺服器。 通常，使用OCSP伺服器而非CRL伺服器時，撤銷檢查的執行速度會更快。 (請參閱 [線上憑證狀態通訊協定](https://tools.ietf.org/html/rfc2560).)

您可以使用Adobe應用程式和服務來設定Signature服務使用的CRL和OCSP伺服器順序。 例如，如果先在Adobe應用程式和服務中設定OCSP伺服器，則會檢查OCSP伺服器，然後檢查CRL伺服器。

如果您未執行撤銷檢查，Signature service就不會檢查憑證是否被撤銷。 也就是說，會忽略CRL和OCSP伺服器資訊。

>[!NOTE]
>
>您可以使用覆寫憑證中指定的URL `CRLOptionSpec` 和 `OCSPOptionSpec` 物件。 例如，若要覆寫CRL伺服器，您可以叫用 `CRLOptionSpec` 物件的 `setLocalURI` 方法。

時間戳記是追蹤已簽署或已驗證檔案修改時間的程式。 檔案簽署後，任何人都無法修改。 時間戳記有助於強制實施已簽署或已驗證檔案的有效性。 您可以使用 `TSPOptionSpec` 物件。 例如，您可以指定時間戳記提供者(TSP)伺服器的URL。

>[!NOTE]
>
>在Java和Web服務快速啟動中，驗證時間設定為 `VerificationTime.CURRENT_TIME` 且撤銷檢查設為 `RevocationCheckStyle.BestEffort`. 因為未指定CRL或OCSP伺服器資訊，所以會從憑證取得伺服器資訊。

**擷取所有數位簽名**

若要驗證PDF檔案中的所有數位簽名，請從PDF檔案中擷取數位簽名。 所有簽名都會傳回清單中。 在驗證數位簽章時，請檢查簽章的狀態。

>[!NOTE]
>
>與驗證單一數位簽章不同，驗證多個簽章時，您不需要指定簽章欄位名稱。

**逐一檢視所有簽章**

逐一檢視每個簽章。 也就是說，對於每個簽名，驗證數位簽名，並檢查簽名者的身份和每個簽名的狀態。 (請參閱 [驗證數位簽名](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>如果要求是整個檔案，則不需要反複檢查所有簽名。

**另请参阅**

[使用Java API驗證多個數位簽名](#verify-digital-signatures-using-the-java-api)

[使用Web服務API驗證多個數位簽名](#verify-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API驗證多個數位簽名 {#verify-multiple-digital-signatures-using-the-java-api}

使用Signature Service API (Java)驗證多個數位簽名：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽名使用者端

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 取得包含要驗證之簽名的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表包含多個數位簽章的PDF檔案，以透過其建構函式進行驗證。 傳遞字串值，指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定PKI執行階段選項

   * 建立 `PKIOptions` 物件（使用其建構函式）。
   * 透過叫用設定驗證時間 `PKIOptions` 物件的 `setVerificationTime` 方法和傳遞 `VerificationTime` 指定驗證時間的列舉值。
   * 透過叫用設定撤銷檢查選項 `PKIOptions` 物件的 `setRevocationCheckStyle` 方法和傳遞 `RevocationCheckStyle` 指定是否執行撤銷檢查的列舉值。

1. 擷取所有數位簽名

   叫用 `SignatureServiceClient` 物件的 `verifyPDFDocument` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 包含包含包含多個數位簽名的PDF檔案的物件。
   * A `PKIOptions` 包含PKI執行階段選項的物件。
   * A `VerifySPIOptions` 包含SPI資訊的執行個體。 您可以指定 `null` 此引數的。

   此 `verifyPDFDocument` 方法傳回 `PDFDocumentVerificationInfo` 包含位於PDF檔案中所有數位簽名相關資訊的物件。

1. 逐一檢視所有簽章

   * 透過叫用 `PDFDocumentVerificationInfo` 物件的 `getVerificationInfos` 方法。 此方法會傳回 `java.util.List` 物件，其中每個元素為 `PDFSignatureVerificationInfo` 物件。 使用 `java.util.Iterator` 物件，逐一檢視簽名清單。
   * 使用 `PDFSignatureVerificationInfo` 物件時，您可以執行工作，例如透過叫用 `PDFSignatureVerificationInfo` 物件的 `getStatus` 方法。 此方法會傳回 `SignatureStatus` 其靜態資料成員通知您簽名狀態的物件。 例如，如果簽章不明，此方法會傳回 `SignatureStatus.DocumentSignatureUnknown`.

**另请参阅**

[驗證多個數位簽名](#verifying-multiple-digital-signatures)

[快速入門（SOAP模式）：使用Java API驗證多個數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[驗證數位簽名](#verify-digital-signatures-using-the-java-api)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API驗證多個數位簽名 {#verifying-multiple-digital-signatures-using-the-web-service-api}

使用Signature Service API （Web服務）驗證多個數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得包含要驗證之簽名的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件會儲存包含多個要驗證的數位簽名的PDF檔案。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 屬性位元組陣列的內容。

1. 設定PKI執行階段選項

   * 建立 `PKIOptions` 物件（使用其建構函式）。
   * 透過指派 `PKIOptions` 物件的 `verificationTime` 資料成員a `VerificationTime` 指定驗證時間的列舉值。
   * 透過指派以下專案來設定撤銷檢查選項 `PKIOptions` 物件的 `revocationCheckStyle` 資料成員a `RevocationCheckStyle` 指定是否執行撤銷檢查的列舉值。

1. 擷取所有數位簽名

   叫用 `SignatureServiceClient` 物件的 `verifyPDFDocument` 方法並傳遞下列值：

   * A `BLOB` 包含包含包含多個數位簽名的PDF檔案的物件。
   * A `PKIOptions` 包含PKI執行階段選項的物件。
   * A `VerifySPIOptions` 包含SPI資訊的執行個體。 您可以為此引數指定null。

   此 `verifyPDFDocument` 方法傳回 `PDFDocumentVerificationInfo` 包含位於PDF檔案中所有數位簽名相關資訊的物件。

1. 逐一檢視所有簽章

   * 透過取得 `PDFDocumentVerificationInfo` 物件的 `verificationInfos` 資料成員。 此資料成員傳回 `Object` 陣列，其中每個元素為 `PDFSignatureVerificationInfo` 物件。
   * 使用 `PDFSignatureVerificationInfo` 物件，您可以透過取得 `PDFSignatureVerificationInfo` 物件的 `status` 資料成員。 此資料成員傳回 `SignatureStatus` 其靜態資料成員通知您簽名狀態的物件。 例如，如果簽章不明，此方法會傳回 `SignatureStatus.DocumentSignatureUnknown`.

**另请参阅**

[驗證多個數位簽名](#verifying-multiple-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 移除數位簽名 {#removing-digital-signatures}

數位簽章必須先從簽章欄位中移除，才能套用更新的數位簽章。 無法覆寫數位簽章。 如果您嘗試將數位簽章套用至包含簽章的簽章欄位，會發生例外狀況。

>[!NOTE]
>
>如需Signature服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-8}

若要從簽名欄位中移除數位簽名，請執行下列工作：

1. 包含專案檔案。
1. 建立簽章使用者端。
1. 取得包含要移除之簽名的PDF檔案。
1. 從簽名欄位中移除數位簽名。
1. 將PDF檔案儲存為PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立簽名使用者端**

您必須先建立簽名服務使用者端，才能以程式設計方式執行簽名服務作業。

**取得包含要移除之簽名的PDF檔案**

若要從PDF檔案中移除簽名，您必須取得包含簽名的PDF檔案。

**從簽名欄位中移除數位簽名**

若要成功從PDF檔案中移除數位簽名，您必須指定包含數位簽名的簽名欄位名稱。 此外，您必須擁有移除數位簽章的許可權；否則，會發生例外狀況。

**將PDF檔案儲存為PDF檔案**

簽名服務從簽名欄位中移除數位簽名後，您可以將PDF檔案儲存為PDF檔案，以便使用者可以在Acrobat或Adobe Reader中開啟它。

**另请参阅**

[使用Java API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用Web服務API移除數位簽名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[新增簽名欄位](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API移除數位簽名 {#remove-digital-signatures-using-the-java-api}

使用簽名API (Java)移除數位簽名：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-signatures-client.jar。

1. 建立簽章使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `SignatureServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 取得包含要移除之簽名的PDF檔案

   * 建立 `java.io.FileInputStream` 物件，代表PDF檔案，其中包含要移除的簽名，方法是使用其建構函式並傳遞指定PDF檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 從簽名欄位中移除數位簽名

   透過叫用「 」，從簽名欄位中移除數位簽名 `SignatureServiceClient` 物件的 `clearSignatureField` 並傳遞下列值：

   * A `com.adobe.idp.Document` 物件，代表包含要移除之簽名的PDF檔案。
   * 字串值，指定包含數位簽章的簽章欄位名稱。

   此 `clearSignatureField` 方法傳回 `com.adobe.idp.Document` 物件，代表從中移除數位簽名的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立 `java.io.File` 物件，並確認副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 方法。 傳遞 `java.io.File` 物件，以複製 `com.adobe.idp.Document` 物件至檔案。 確保您使用 `Document` 物件，由 `clearSignatureField` 方法。

**另请参阅**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入門（SOAP模式）：使用Java API移除數位簽名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API移除數位簽名 {#remove-digital-signatures-using-the-web-service-api}

使用Signature API （Web服務）移除數位簽名：

1. 包含專案檔案

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立簽名使用者端

   * 建立 `SignatureServiceClient` 物件（使用其預設建構函式）。
   * 建立 `SignatureServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `SignatureServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 取得包含要移除之簽名的PDF檔案

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存包含要移除的數位簽名的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表已簽署PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 從簽名欄位中移除數位簽名

   透過叫用 `SignatureServiceClient` 物件的 `clearSignatureField` 並傳遞下列值：

   * A `BLOB` 包含已簽署PDF檔案的物件。
   * 字串值，代表包含要移除之數位簽章的簽章欄位名稱。

   此 `clearSignatureField` 方法傳回 `BLOB` 物件，代表從中移除數位簽名的PDF檔案。

1. 將PDF檔案儲存為PDF檔案

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式並傳遞字串值，該值代表PDF檔案的檔案位置，該檔案包含空白簽名欄位和開啟檔案的模式。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `sign` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[移除數位簽名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
