---
title: 匯入和匯出資料
seo-title: Importing and Exporting Data
description: 使用Form Data Integration Service將資料匯入PDF表單，並使用Java API和Web Service API從PDF表單匯出資料。
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 0%

---

# 匯入和匯出資料 {#importing-and-exporting-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 關於表單資料整合服務 {#about-the-form-data-integration-service}

表單資料整合服務可將資料匯入PDF表單，並從PDF表單匯出資料。 匯入和匯出作業支援兩種PDF forms：

* Acrobat表單(在Acrobat中建立)是包含表單欄位的PDF檔案。
* AdobeXML表單（在Designer中建立）是符合XMLAdobeXML Forms架構(XFA)的PDF檔案。

根據PDF表單的型別，表單資料可以下列格式之一存在：

* XFDF檔案，這是Acrobat表單資料格式的XML版本。
* XDP檔案，此檔案為包含表單欄位定義的XML檔案。 其中也可能包含表單欄位資料和內嵌PDF檔案。 Designer產生的XDP檔案只能在其攜帶內嵌base-64編碼PDF檔案時使用。

您可以使用表單資料整合服務完成這些工作：

* 將資料匯入PDF forms。 如需詳細資訊，請參閱 [匯入表單資料](importing-exporting-data.md#importing-form-data).
* 從PDF forms匯出資料。 如需詳細資訊，請參閱 [匯出表單資料](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 匯入表單資料 {#importing-form-data}

您可以使用表單資料整合服務，將表單資料匯入互動式PDF forms。 互動式PDF表單是一份PDF檔案，其中包含一個或多個用於向使用者收集資訊或用於顯示自訂資訊的欄位。 表單資料整合服務不支援表單計算、驗證或指令碼。

若要將資料匯入在Designer中建立的表單，您必須參考有效的XDP XML資料來源。 請考量下列範例抵押申請表單。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

若要將資料值匯入此表單，您必須擁有與表單對應的有效XDP XML資料來源。 您無法使用任意XML資料來源，將資料匯入使用「表單資料整合」服務的表單。 任意XML資料來源和XDP XML資料來源之間的差異在於XDP資料來源符合XML Forms架構(XFA)。 下列XML代表與範例抵押應用程式表單對應的XDP XML資料來源。

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

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要將表單資料匯入PDF表單，請執行下列步驟：

1. 包含專案檔案。
1. 建立表單資料整合服務使用者端。
1. 參考PDF表單。
1. 參照XML資料來源。
1. 將資料匯入PDF表單。
1. 將PDF表單儲存為PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

有關這些JAR檔案位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立表單資料整合服務使用者端**

您必須先建立資料整合服務使用者端，才能以程式設計方式將資料從使用者端API匯入PDF。 建立服務使用者端時，您可以定義呼叫服務所需的連線設定。 如需詳細資訊，請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**參考PDF表單**

若要將資料匯入PDF表單，您必須參考在Designer中建立的XML表單，或在Acrobat中建立的Acrobat表單。

**參考XML資料來源**

若要匯入表單資料，您必須參考有效的資料來源。 若要將資料匯入在Designer中建立的XFA XML表單，您必須使用XDP XML資料來源。 如果您參照Acrobat表單，則必須使用XFDF資料來源。 對於您要將資料匯入到的每個欄位，都必須指定一個值。 如果位於XML資料來源中的元素未對應至表單中的欄位，則會忽略該元素。

**將資料匯入PDF表單**

參照PDF表單和有效的XML資料來源後，即可將資料匯入PDF表單。

**將PDF表單儲存為PDF檔案**

將資料匯入表單後，可將表單儲存為PDF檔案。 儲存為PDF檔案後，使用者就可以在Adobe Reader或Acrobat中開啟表單，並檢視包含匯入資料的表單。

**另请参阅**

[使用Java API匯入表單資料](importing-exporting-data.md#import-form-data-using-the-java-api)

[使用Web服務API匯入表單資料](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速入門](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[匯出表單資料](importing-exporting-data.md#exporting-form-data)

### 使用Java API匯入表單資料 {#import-form-data-using-the-java-api}

使用表單資料整合API (Java)匯入表單資料：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormDataIntegrationClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考PDF表單。

   * 建立 `java.io.FileInputStream` 物件（使用其建構函式）。 傳遞字串值，指定PDF表單的位置。
   * 建立 `com.adobe.idp.Document` 使用儲存PDF表單的物件 `com.adobe.idp.Document` 建構函式。 傳遞 `java.io.FileInputStream` 包含建構函式PDF表單的物件。

1. 參照XML資料來源。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式，並傳遞字串值，該字串值指定包含要匯入表單之資料的XML檔案的位置。
   * 建立 `com.adobe.idp.Document` 使用儲存表單資料的物件 `com.adobe.idp.Document` 建構函式。 傳遞 `java.io.FileInputStream` 包含表單資料至建構函式的物件。

1. 將資料匯入PDF表單。

   透過叫用將資料匯入PDF表單 `FormDataIntegrationClient` 物件的 `importData` 並傳遞下列值：

   * 此 `com.adobe.idp.Document` 儲存PDF表單的物件。
   * 此 `com.adobe.idp.Document` 儲存表單資料的物件。

   此 `importData` 方法傳回 `com.adobe.idp.Document` 物件，用來儲存PDF表單，其中包含位於XML資料來源中的資料。

1. 將PDF表單儲存為PDF檔案。

   * 建立 `java.io.File` 物件，並確認副檔名為「。PDF」。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `importData` 方法)。

**另请参阅**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API匯入表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API匯入表單資料 {#import-form-data-using-the-web-service-api}

使用表單資料整合API （Web服務）匯入表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立表單資料整合服務使用者端。

   * 建立 `FormDataIntegrationClient` 物件（使用其預設建構函式）。
   * 建立 `FormDataIntegrationClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `FormDataIntegrationClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參考PDF表單。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存PDF表單。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，指定PDF表單的位置和開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 參照XML資料來源。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存匯入表單的資料。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，指定包含要匯入資料之XML檔案的位置，以及開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 將資料匯入PDF表單。

   叫用「 」，將資料匯入PDF表單 `FormDataIntegrationClient` 物件的 `importData` 並傳遞下列值：

   * 此 `BLOB` 儲存PDF表單的物件。
   * 此 `BLOB` 儲存表單資料的物件。

   此 `importData` 方法傳回 `BLOB` 物件，用來儲存PDF表單，其中包含位於XML資料來源中的資料。

1. 將PDF表單儲存為PDF檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案之檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `importData` 方法。 透過取得 `BLOB` 物件的 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 匯出表單資料 {#exporting-form-data}

您可以使用「表單資料整合」服務，從互動式PDF表單匯出表單資料。 匯出的資料格式取決於表單型別。 如果表單型別是在Acrobat中建立的Acrobat表單，則匯出的資料為XFDF。 如果表單型別是在Designer中建立的XML表單，則匯出的資料為XDP。

>[!NOTE]
>
>如需表單資料整合服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

若要從PDF表單匯出表單資料，請執行下列步驟：

1. 包含專案檔案
1. 建立表單資料整合服務使用者端。
1. 參考PDF表單。
1. 從PDF表單匯出資料。
1. 將匯出的資料儲存為XML檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

下列JAR檔案必須新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立表單資料整合服務使用者端**

您必須先建立資料整合服務使用者端，才能以程式設計方式將資料匯入PDFformClient API。 建立服務使用者端時，您可以定義呼叫服務所需的連線設定。 如需詳細資訊， [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**參考PDF表單**

若要從PDF表單匯出資料，您必須參照在Designer或Acrobat中建立且包含表單資料的PDF表單。 如果您嘗試從空白的PDF表單匯出資料，將會得到空白的XML結構描述。

**從PDF表單匯出資料**

參照包含表單資料的PDF表單後，您可以從表單匯出資料。 資料會匯出至以表單為基礎的XML結構描述中。

**將表單資料儲存為XML檔案**

匯出表單資料後，可將資料儲存為XML檔案。 儲存為XML檔案後，您可以在XML檢視器中開啟XML檔案，以檢視表單資料。

**另请参阅**

[使用Java API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-java-api)

[使用Web服務API匯出表單資料](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[表單資料整合服務API快速入門](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[匯入表單資料](importing-exporting-data.md#importing-form-data)

### 使用Java API匯出表單資料 {#export-form-data-using-the-java-api}

使用表單資料整合API (Java)匯出表單資料：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-formdataintegration-client.jar。

1. 建立表單資料整合服務使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormDataIntegrationClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考PDF表單。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值，該值會指定包含要匯出之資料的PDF表單的位置。
   * 建立 `com.adobe.idp.Document` 使用儲存PDF表單的物件 `com.adobe.idp.Document` 建構函式。 傳遞 `java.io.FileInputStream` 包含建構函式PDF表單的物件。

1. 從PDF表單匯出資料。

   透過叫用 `FormDataIntegrationClient` 物件的 `exportData` 方法並傳遞 `com.adobe.idp.Document` 儲存PDF表單的物件。 此方法會傳回 `com.adobe.idp.Document` 將表單資料儲存為XML結構描述的物件。

1. 將PDF表單儲存為PDF檔案。

   * 建立 `java.io.File` 物件，並確認副檔名為XML。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `exportData` 方法)。

**另请参阅**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[快速入門（SOAP模式）：使用Java API匯出表單資料](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API匯出表單資料 {#export-form-data-using-the-web-service-api}

使用表單資料整合API （Web服務）匯出表單資料：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立表單資料整合服務使用者端。

   * 建立 `FormDataIntegrationClient` 物件（使用其預設建構函式）。
   * 建立 `FormDataIntegrationClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請指定 `?blob=mtom` 以使用MTOM。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `FormDataIntegrationClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 參考PDF表單。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存從中匯出資料的PDF表單。
   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞字串值，指定PDF表單的位置和開啟檔案的模式。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 從PDF表單匯出資料。

   透過叫用將資料匯入PDF表單 `FormDataIntegrationClient` 物件的 `exportData` 方法並傳遞 `BLOB` 儲存PDF表單的物件。 此方法會傳回 `BLOB` 將表單資料儲存為XML結構描述的物件。

1. 將PDF表單儲存為PDF檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表XML檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `exportData` 方法。 透過取得 `BLOB` 物件的 `MTOM` 欄位。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * 透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[步驟摘要](importing-exporting-data.md#summary-of-steps)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
