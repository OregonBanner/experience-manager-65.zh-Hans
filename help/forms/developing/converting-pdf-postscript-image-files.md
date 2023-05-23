---
title: 將PDF轉換為Postscript和Image檔案
seo-title: Converting PDF to Postscript andImage Files
description: 使用Java API和Web服務API，使用轉換PDF服務將PDF檔案轉換為PostScript和多種影像格式(JPEG、JPEG2000、PNG和TIFF)。
seo-description: Use the Convert PDF service to convert PDF documents to PostScript and to a number of image formats (JPEG, JPEG 2000, PNG, and TIFF) using the Java API and Web Service API.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2809'
ht-degree: 0%

---

# 將PDF轉換為Postscript和影像檔案 {#converting-pdf-to-postscript-andimage-files}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於轉換PDF服務**

「轉換PDF」服務會將PDF檔案轉換為PostScript和多種影像格式(JPEG、JPEG2000、PNG和TIFF)。 將PDF檔案轉換為PostScript對於任何PostScript印表機上的自動伺服器式列印都很有用。 在不支援PDF檔案的內容管理系統中封存檔案時，將PDF檔案轉換為多頁TIFF檔案是可行的。

您可以使用轉換PDF服務完成這些工作：

* 將PDF檔案轉換為PostScript。
* 將PDF檔案轉換為影像格式。

>[!NOTE]
>
>如需有關轉換PDF服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將PDF檔案轉換為PostScript {#converting-pdf-documents-to-postscript}

本主題說明如何使用轉換PDF服務API （Java和Web服務），以程式設計方式將PDF檔案轉換為PostScript檔案。 轉換為PostScript檔案的PDF檔案必須是非互動式PDF檔案。 也就是說，如果您嘗試將互動式PDF檔案轉換為PostScript檔案，則會擲回例外狀況。

>[!NOTE]
>
>如需有關轉換PDF服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要將PDF檔案轉換為PostScript檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務使用者端。
1. 參照要轉換成PostScript檔案的PDF檔案。
1. 設定轉換執行階段選項。
1. 將PDF檔案轉換為PostScript檔案。
1. 儲存PostScript檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立轉換PDF使用者端**

您必須先建立轉換PDF服務使用者端，才能以程式設計方式執行轉換PDF服務作業。 如果您使用Java API，請建立 `ConvertPdfServiceClient` 物件。 如果您使用Web服務API，請建立 `ConvertPDFServiceService` 物件。

本節使用AEM Forms中介紹的Web服務功能。 若要存取新功能，您必須使用 `lc_version` 屬性。 (請參閱下列「使用Web服務存取新功能」： [使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**參照要轉換成PostScript檔案的PDF檔案**

參照您要轉換成PostScript檔案的PDF檔案。 如本主題先前所述，PDF檔案必須是非互動式PDF檔案。 如果您嘗試將互動式PDF檔案轉換為PostScript檔案，則會擲回例外狀況。

**設定轉換執行階段選項**

將PDF檔案轉換為PostScript檔案時，您可以定義執行階段選項，以指定所建立的PostScript型別。 例如，您可以定義第3級PostScript檔案。

一般而言，產生的PostScript檔案會反映輸入PDF檔案的大小。 如果您選取 `ShrinkToFit` 選項（縮減PostScript檔案的輸出以符合頁面），您不會看到輸入PDF檔案與產生的PostScript檔案之間的差異。 此 `ShrinkToFit` 只有當您選擇在小於輸入PDF檔案的頁面大小上列印時，選項才會生效。 若要選取較小的頁面大小，請定義 `PageSize` 選項。 此外，建議您將 `RotateAndCenter` 選項至 `true` 以取得正確的PostScript輸出。

同樣地，如果您選取 `ExpandToFit` 選項（會展開PostScript檔案的輸出以符合頁面），但只有在您選取在比輸入PDF檔案更大的頁面大小上列印時，它才會生效。 若要選取較大的頁面大小，請定義 `PageSize` 選項。 此外，建議您將 `RotateAndCenter` 選項至 `true` 以取得正確的PostScript輸出。

>[!NOTE]
>
>如需您可以設定的執行階段值相關資訊，請參閱 `ToPSOptionsSpec` 中的類別參考 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**將PDF檔案轉換為PostScript檔案**

建立服務使用者端並設定執行階段選項後，您可以叫用PostScript轉換作業。 此操作將需要轉換檔案的相關資訊，包括目標檔案的偏好PostScript層級。

**儲存PostScript檔案**

將PDF檔案轉換為PostScript後，您可以將輸出儲存為PostScript檔案。

**另请参阅**

[使用Java API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用網站服務API將PDF檔案轉換為PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速啟動](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為PS {#convert-a-pdf-document-to-ps-using-the-java-api}

使用轉換PDF服務API (Java)將PDF檔案轉換為PostScript：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-convertpdf-client.jar。

1. 建立轉換PDF使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `ConvertPdfServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參照要轉換成PostScript檔案的PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值，以指定要轉換的PDF檔案位置。
   * 建立 `com.adobe.idp.Document` 使用儲存PDF檔案的物件 `com.adobe.idp.Document` 建構函式。 傳遞 `java.io.FileInputStream` 包含PDF檔案的物件。

1. 設定轉換執行階段選項。

   * 建立 `ToPSOptionsSpec` 物件（透過叫用其建構函式）。
   * 叫用屬於下列專案的適當方法來設定執行階段選項： `ToPSOptionsSpec` 物件。 例如，若要定義建立的PostScript層級，請叫用 `ToPSOptionsSpec` 物件的 `setPsLevel` 方法並傳遞 `PSLevel` 指定PostScript層級的列舉值。 如需您可以設定的所有執行階段值的相關資訊，請參閱 `ToPSOptionsSpec` 中的類別參考 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 將PDF檔案轉換為PostScript檔案。

   叫用 `ConvertPdfServiceClient`物件的 `toPS2` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 物件，代表要轉換成PostScript檔案的PDF檔案。
   * A `ToPSOptionsSpec` 物件，指定PostScript執行階段選項。

   此 `toPS2` 方法傳回 `Document` 包含新PostScript檔案的物件。

1. 儲存PostScript檔案。

   * 建立 `java.io.File` 物件，並確認副檔名為.ps。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `toPS2` 方法)。

**另请参阅**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API將PDF檔案轉換為PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API將PDF檔案轉換為PS {#convert-a-pdf-document-to-ps-using-the-web-service-api}

使用轉換PDF服務API （Web服務）將PDF檔案轉換為PostScript：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立轉換PDF使用者端。

   * 建立 `ConvertPdfServiceClient` 物件（使用其預設建構函式）。
   * 建立 `ConvertPdfServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `ConvertPdfServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參照要轉換成PostScript檔案的PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存轉換成PostScript檔案的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表要轉換之PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置和串流長度以讀取。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 設定轉換執行階段選項。

   * 建立 `ToPSOptionsSpec` 物件（透過叫用其建構函式）。
   * 將值指派給，設定執行階段選項 `ToPSOptionsSpec` 物件的資料成員。 例如，若要定義已建立的PostScript層級，請指派 `PSLevel` 列舉值至 `ToPSOptionsSpec` 物件的 `psLevel` 資料成員。

1. 將PDF檔案轉換為PostScript檔案。

   叫用 `GeneratePDFServiceService` 物件的 `toPS2` 方法並傳遞下列值：

   * A `BLOB` 物件，代表要轉換成PostScript檔案的PDF檔案
   * A `ToPSOptionsSpec` 指定執行階段選項的物件

   轉換完成後，存取代表PostScript檔案的二進位資料 `BLOB` 物件的 `MTOM` 屬性。 這會傳回您可以寫出至PostScript檔案的位元組陣列。

1. 儲存PostScript檔案。

   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表PS檔案之檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `encryptPDFUsingPassword` 方法。 透過取得 `BLOB` 物件的 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 將PDF檔案轉換為影像格式 {#converting-pdf-documents-to-image-formats}

您可以使用「轉換PDF」服務，以程式設計方式將PDF檔案轉換為影像格式，包括JPEG、JPEG2000、TIFF和PNG。 將PDF檔案轉換為影像檔案後，您就可以將PDF檔案當成影像檔案使用。 例如，您可以將影像放入企業內容管理系統進行儲存。

將PDF檔案轉換為影像時，轉換PDF服務會為檔案中的每個頁面建立個別的影像。 也就是說，如果檔案有20頁，則「轉換PDF」服務會建立20個影像檔案。 將PDF檔案轉換為影像格式時，您可以為PDF檔案中的每個頁面建立個別影像，或為整個PDF檔案建立單一影像檔案。

>[!NOTE]
>
>如需有關轉換PDF服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

若要將PDF檔案轉換為任何支援的型別，請執行下列步驟：

1. 包含專案檔案。
1. 建立轉換PDF服務使用者端。
1. 擷取要轉換的PDF檔案。
1. 設定執行階段選項。
1. 將PDF轉換為影像。
1. 從集合中擷取影像檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立轉換PDF使用者端**

您必須先建立轉換PDF服務使用者端，才能以程式設計方式執行轉換PDF服務作業。 如果您使用Java API，請建立 `ConvertPdfServiceClient` 物件。 如果您使用Web服務API，請建立 `ConvertPDFServiceService` 物件。

**擷取要轉換的PDF檔案**

您必須擷取PDF檔案才能轉換為影像。 您無法將互動式PDF檔案轉換為影像。 如果您嘗試這麼做，則會擲回例外狀況。 若要將互動式PDF檔案轉換為影像檔案，您必須先將PDF檔案平面化，才能進行轉換。 (請參閱 [平面化PDF檔案](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**設定執行階段選項**

您必須設定執行階段選項，例如影像格式和解析度值。 如需有關執行階段值的資訊，請參閱 `ToImageOptionsSpec` 中的類別參考 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**將PDF轉換為影像**

建立服務使用者端並設定執行階段選項後，您可以將PDF檔案轉換為影像。 會傳回包含影像的集合物件。

**從集合中擷取影像檔案**

您可以從ConvertPDF服務傳回的集合物件擷取影像檔案。 集合中的每個元素都是 `com.adobe.idp.Document` 執行個體(或 `BLOB` 例項（如果您使用Web服務），則可儲存為影像檔案，例如JPG檔案。

影像檔案的格式取決於 `ImageConvertFormat` 執行階段選項。 也就是說，如果您將 `ImageConvertFormat` 執行階段選項 `ImageConvertFormat.JPEG`，您可以將影像檔案儲存為JPG檔案。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[轉換PDF服務API快速啟動](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API將PDF檔案轉換為影像檔案 {#convert-a-pdf-document-to-image-files-using-the-java-api}

使用轉換PDF服務API (Java)將PDF檔案轉換為影像格式：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-convertpdf-client.jar。

1. 建立轉換PDF使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `ConvertPdfServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取要轉換的PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，代表要轉換的PDF檔案，方法是使用其建構函式，並傳遞指定PDF檔案位置的字串值。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 設定執行階段選項。

   * 建立 `ToImageOptionsSpec` 物件（使用其建構函式）。
   * 視需要叫用屬於此物件的方法。 例如，透過叫用 `setImageConvertFormat` 方法和傳遞 `ImageConvertFormat` 指定格式型別的列舉值。

   >[!NOTE]
   >
   >設定 `ImageConvertFormat` 列舉值是必要的。

1. 將PDF轉換為影像。

   叫用 `ConvertPdfServiceClient` 物件的 `toImage2` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 代表要轉換之PDF檔案的物件。
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` 物件，其中包含有關目標影像格式的各種偏好設定。

   此 `toImage2` 方法傳回 `java.util.List` 包含影像的物件。 集合中的每個元素都是 `com.adobe.idp.Document` 執行個體。

1. 從集合中擷取影像檔案。

   循環瀏覽 `java.util.List` 物件來判斷影像是否存在。 每個元素都是 `com.adobe.idp.Document` 執行個體。 透過叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 方法和傳遞 `java.io.File` 物件。

**另请参阅**

[快速入門（SOAP模式）：使用Java API將PDF檔案轉換為JPEG檔案](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用Web服務API將PDF檔案轉換為影像檔案 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

使用轉換PDF服務API （Web服務）將PDF檔案轉換為影像格式：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立轉換PDF使用者端。

   * 建立 `ConvertPdfServiceClient` 物件（使用其預設建構函式）。
   * 建立 `ConvertPdfServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 不過，請指定 `?blob=mtom`.
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `ConvertPdfServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取要轉換的PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存PDF表單。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，指定PDF表單的位置和開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 透過取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 設定執行階段選項。

   * 建立 `ToImageOptionsSpec` 物件（使用其建構函式）。
   * 視需要叫用屬於此物件的方法。 例如，透過叫用 `setImageConvertFormat` 方法和傳遞 `ImageConvertFormat` 指定格式型別的列舉值。

   >[!NOTE]
   >
   >設定 `ImageConvertFormat` 列舉值是必要的。

1. 將PDF轉換為影像。

   叫用 `ConvertPDFServiceService` 物件的 `toImage2` 方法並傳遞下列值：

   * A `BLOB` 物件，代表要轉換的檔案
   * A `ToImageOptionsSpec` 包含目標影像格式各種偏好設定的物件

   此 `toImage2` 方法傳回 `MyArrayOfBLOB` 包含新建立之影像檔案的物件。

1. 從集合中擷取影像檔案。

   * 決定中的元素數量 `MyArrayOfBLOB` 物件，方法是取得其 `Count` 欄位。 每個元素都是 `BLOB` 包含影像的物件。
   * 循環瀏覽 `MyArrayOfBLOB` 物件並儲存每個影像檔案。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
