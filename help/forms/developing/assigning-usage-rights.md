---
title: 指派使用許可權
seo-title: Assigning Usage Rights
description: 使用Acrobat Reader DC擴充功能Java使用者端API和Web服務API ，套用並移除PDF檔案中的使用許可權。
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3926'
ht-degree: 0%

---

# 指派使用許可權 {#assigning-usage-rights}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 關於Acrobat Reader DC擴充功能服務 {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC擴充功能服務可擴充Adobe Reader的功能，讓您的組織輕鬆共用互動式PDF檔案。 Acrobat Reader DC擴充功能服務完全支援任何PDF檔案，最高支援（包括）PDF1.7。它可搭配Adobe Reader 7.0和更新版本使用。 此服務會將使用許可權新增至PDF檔案，並啟動使用Adobe Reader開啟PDF檔案時通常無法使用的功能。 協力廠商使用者不需要其他軟體或外掛程式即可使用啟用許可權的檔案。

您可以使用Acrobat Reader DC擴充功能服務完成這些工作：

* 套用使用許可權至PDF檔案。 如需詳細資訊，請參閱 [將使用許可權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* 從PDF檔案中移除使用許可權。 如需詳細資訊，請參閱 [從PDF檔案中移除使用許可權](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* 擷取認證詳細資料。 如需詳細資訊，請參閱 [正在擷取認證資訊](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 將使用許可權套用至PDF檔案 {#applying-usage-rights-to-pdf-documents}

您可以使用Acrobat Reader DC擴充功能Java使用者端API和Web服務，將使用許可權套用至PDF檔案。 使用許可權與Acrobat中預設提供但Adobe Reader中預設不提供的功能相關，例如新增註解至表單或填寫表單欄位及儲存表單的功能。 已套用使用許可權的PDF檔案稱為許可權啟用檔案。 在Adobe Reader中開啟許可權啟用檔案的使用者可以執行為該特定檔案啟用的操作。

>[!NOTE]
>
>使用將使用許可權套用至PDF檔案時 `applyUsageRights` 方法，是Java API的一部分，您可以設定 `isModeFinal` 的引數 `ReaderExtensionsOptionSpec` 物件至 `false`. 這會導致已處理表單的計數器未更新且效能提高。 如果您不介意更新已處理的表單計數器，建議您將 `isModeFinal` 引數至 `false`.

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要將使用許可權套用至PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能使用者端物件。
1. 擷取PDF檔案。
1. 指定要套用的使用許可權。
1. 將使用許可權套用至PDF檔案。
1. 儲存啟用許可權的PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Acrobat Reader DC擴充功能使用者端物件**

若要以程式設計方式執行Acrobat Reader DC擴充功能服務作業，您必須建立Acrobat Reader DC擴充功能服務使用者端物件。 如果您使用Acrobat Reader DC擴充功能Java API，請建立 `ReaderExtensionsServiceClient` 物件。 如果您使用Acrobat Reader DC擴充功能Web服務API，請建立 `ReaderExtensionsServiceService` 物件。

**擷取PDF檔案**

您必須擷取PDF檔案才能套用使用許可權。 啟用許可權的PDF檔案包含使用許可權字典。 當Adobe Reader開啟包含這類字典的檔案時，它只會啟用字典中為該檔案指定的使用許可權。 如果檔案未包含使用許可權字典，Acrobat Reader DC擴充功能服務會建立一個使用許可權字典。 如果其中已包含字典，Acrobat Reader DC擴充功能服務會以您指定的使用許可權覆寫現有使用許可權。 字典會指定已啟用哪些使用許可權。 當使用者在Adobe Reader中開啟檔案時，僅允許字典中指定的使用許可權。

**指定要套用的使用許可權**

您可以設定的使用許可權取決於您從Adobe Systems Incorporated購買的認證。 憑證通常會提供許可權來設定一組相關的使用許可權，例如與互動式表單相關的使用許可權。 每個認證都提供建立特定數量已啟用許可權的PDF檔案的權利。 評估認證可讓您建立不限數量的草稿檔案。

>[!NOTE]
>
>如果您嘗試指派認證不允許的使用許可權，則會造成例外狀況。

**將使用許可權套用至PDF檔案**

若要將使用許可權套用至PDF檔案，請參考您用來套用使用許可權的認證別名(認證通常會在安裝AEM Forms期間安裝)。 您也必須指定套用使用許可權的PDF檔案。 如需設定認證的相關資訊，請參閱應用程式伺服器的安裝和部署指南。

**儲存啟用許可權的PDF檔案**

Acrobat Reader DC擴充功能服務將使用許可權套用至PDF檔案後，您可以將啟用許可權的PDF檔案儲存為PDF檔案。

**另请参阅**

[使用Java API套用使用許可權](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[使用網站服務API套用使用許可權](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API套用使用許可權 {#apply-usage-rights-using-the-java-api}

使用Acrobat Reader DC擴充功能API (Java)套用使用許可權至PDF檔案：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴充功能使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `ReaderExtensionsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值來表示PDF檔案，該字串值指定PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 指定要套用的使用許可權。

   * 建立 `UsageRights` 使用物件建構函式表示使用許可權的物件。
   * 對於要套用的每個使用權利，叫用屬於的對應方法 `UsageRights` 物件。 例如，若要新增 `enableFormFillIn` 使用許可權，叫用 `UsageRights` 物件的 `enableFormFillIn` 方法與傳遞 `true`. （對要套用的每個使用許可權重複此步驟）。

1. 將使用許可權套用至PDF檔案。

   * 建立 `ReaderExtensionsOptionSpec` 物件（使用其建構函式）。 此物件包含Acrobat Reader DC擴充功能服務所需的執行階段選項。 叫用此建構函式時，您必須指定下列值：

      * 此 `UsageRights` 包含要套用至檔案之使用許可權的物件。
      * 字串值，指定在Adobe Reader 7.x中開啟啟用許可權的PDF檔案時，使用者看到的訊息。Adobe Reader 8.0中未顯示此訊息。
   * PDF透過叫用 `ReaderExtensionsServiceClient` 物件的 `applyUsageRights` 並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含套用使用許可權之PDF檔案的物件。
      * 字串值，指定可讓您套用使用許可權的認證別名。
      * 字串值，指定對應的密碼值。 (目前會忽略此引數。 您可以通過 `null`.)
   * 此 `ReaderExtensionsOptionSpec` 包含執行階段選項的物件。

   此 `applyUsageRights` 方法傳回 `com.adobe.idp.Document` 包含已啟用許可權的PDF檔案的物件。

1. 儲存啟用許可權的PDF檔案。

   * 建立 `java.io.File` 物件，並確認副檔名為.pdf。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 複製目錄內容的方法 `com.adobe.idp.Document` 物件放入檔案(請確定您使用 `com.adobe.idp.Document` 物件，由 `applyUsageRights` 方法)。

**另请参阅**

[將使用許可權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[快速入門（SOAP模式）：使用Java API套用使用許可權](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API套用使用許可權 {#apply-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC擴充功能API （Web服務）套用使用許可權至PDF檔案：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Acrobat Reader DC擴充功能使用者端物件。

   * 建立 `ReaderExtensionsServiceClient` 物件（使用其預設建構函式）。
   * 建立 `ReaderExtensionsServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 請務必指定 `?blob=mtom`.)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `ReaderExtensionsServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存已套用使用許可權的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 指定要套用的使用許可權。

   * 建立 `UsageRights` 使用物件建構函式表示使用許可權的物件。
   * 對於要套用的每個使用權利，指派值 `true` 至屬於的對應資料成員 `UsageRights` 物件。 例如，若要新增 `enableFormFillIn` 使用許可權，指派 `true` 至 `UsageRights` 物件的 `enableFormFillIn` 資料成員。 （對要套用的每個使用許可權重複此步驟）。

1. 將使用許可權套用至PDF檔案。

   * 建立 `ReaderExtensionsOptionSpec` 物件（使用其建構函式）。 此物件包含Acrobat Reader DC擴充功能服務所需的執行階段選項。
   * 指派 `UsageRights` 物件至 `ReaderExtensionsOptionSpec` 物件的 `usageRights` 資料成員。
   * 將字串值指派給，指定當在Adobe Reader中開啟啟用許可權的PDF檔案時，使用者看到的訊息 `ReaderExtensionsOptionSpec` 物件的 `message` 資料成員。
   * PDF透過叫用 `ReaderExtensionsServiceClient` 物件的 `applyUsageRights` 並傳遞下列值：

      * 此 `BLOB` 包含套用使用許可權之PDF檔案的物件。
      * 字串值，指定可讓您套用使用許可權的認證別名。
      * 字串值，指定對應的密碼值。 (目前會忽略此引數。 您可以通過 `null`.)
   * 此 `ReaderExtensionsOptionSpec` 包含執行階段選項的物件。

   此 `applyUsageRights` 方法傳回 `BLOB` 包含已啟用許可權的PDF檔案的物件。

1. 儲存啟用許可權的PDF檔案。

   * 建立 `System.IO.FileStream` 物件（透過叫用其建構函式）。 傳遞代表已啟用許可權之PDF檔案之檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `applyUsageRights` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[將使用許可權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 從PDF檔案中移除使用許可權 {#removing-usage-rights-from-pdf-documents}

您可以從啟用許可權的檔案中移除使用許可權。 若要在啟用許可權的PDF檔案上執行其他AEM Forms作業，也需要移除其使用許可權。 例如，您必須先數位簽署（或認證）PDF檔案，才能設定使用許可權。 因此，如果您要對啟用許可權的檔案執行操作，您必須從PDF檔案中移除使用許可權，執行其他操作，例如以數位方式簽署檔案，然後重新將使用許可權套用至檔案。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

若要從啟用許可權的PDF檔案中移除使用許可權，請執行下列步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能使用者端物件。
1. 擷取已啟用許可權的PDF檔案。
1. 從PDF檔案中移除使用許可權。
1. 儲存PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Acrobat Reader DC擴充功能使用者端物件**

您必須先建立Acrobat Reader DC擴充功能服務使用者端物件，才能以程式設計方式執行Acrobat Reader DC擴充功能服務作業。 如果您使用Java API，請建立 `ReaderExtensionsServiceClient` 物件。 如果您使用Acrobat Reader DC擴充功能Web服務API，請建立 `ReaderExtensionsServiceService` 物件。

**擷取啟用許可權的PDF檔案**

擷取已啟用許可權的PDF檔案，以移除使用許可權。

**從PDF檔案中移除使用許可權**

擷取啟用許可權的PDF檔案後，您可以移除使用許可權。 移除使用許可權後，在Adobe Reader中檢視PDF檔案時，不會有任何額外的功能。

**儲存PDF檔案**

您可以將不再包含使用許可權的PDF檔案儲存為PDF檔案。 儲存為PDF檔案後，即可在Adobe Reader或Acrobat中檢視PDF檔案。

**另请参阅**

[使用Java API移除使用許可權](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服務API移除使用許可權](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[將使用許可權套用至PDF檔案](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### 使用Java API移除使用許可權 {#remove-usage-rights-using-the-java-api}

使用Acrobat Reader DC擴充功能API (Java)，從啟用許可權的PDF檔案中移除使用許可權：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴充功能使用者端物件。

   建立 `ReaderExtensionsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 擷取PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用物件的建構函式並傳遞字串值(指定PDF檔案的位置)來表示啟用許可權的PDF檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 從PDF檔案中移除使用許可權。

   叫用「 」，從PDF檔案中移除使用許可權 `ReaderExtensionsServiceClient` 物件的 `removeUsageRights` 方法和傳遞 `com.adobe.idp.Document` 包含已啟用許可權的PDF檔案的物件。 此方法會傳回 `com.adobe.idp.Document` 包含沒有使用許可權之PDF檔案的物件。

1. 將使用許可權套用至PDF檔案。

   * 建立 `java.io.File` 物件，並確認副檔名為。PDF。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件放入檔案(請確定您使用 `Document` 物件，由 `removeUsageRights` 方法)。

**另请参阅**

[從PDF檔案中移除使用許可權](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[快速入門（SOAP模式）：使用Java API從PDF檔案中移除使用許可權](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API移除使用許可權 {#remove-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC擴充功能API （Web服務），從啟用許可權的PDF檔案中移除使用許可權：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Acrobat Reader DC擴充功能使用者端物件。

   * 建立 `ReaderExtensionsServiceClient` 物件（使用其預設建構函式）。
   * 建立 `ReaderExtensionsServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 請務必指定 `?blob=mtom`.)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `ReaderExtensionsServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存啟用許可權的PDF檔案，使用許可權會從中移除。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 從PDF檔案中移除使用許可權。

   叫用「 」，從PDF檔案中移除使用許可權 `ReaderExtensionsServiceClient` 物件的 `removeUsageRights` 方法和傳遞 `BLOB` 包含已啟用許可權的PDF檔案的物件。 此方法會傳回 `BLOB` 包含沒有使用許可權之PDF檔案的物件。

1. 將使用許可權套用至PDF檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表PDF檔案位置的字串值。
   * 建立位元組陣列，儲存 `BLOB` 物件，由 `removeUsageRights` 方法。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。

**另请参阅**

[從PDF檔案中移除使用許可權](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 正在擷取認證資訊 {#retrieving-credential-information}

您可以擷取用來將使用許可權套用至啟用許可權的PDF檔案的認證相關資訊。 透過擷取認證的相關資訊，您可以取得憑證不再有效的日期等資訊。

>[!NOTE]
>
>如需Acrobat Reader DC擴充功能服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

若要擷取用於套用使用許可權至PDF檔案的認證相關資訊，請執行下列步驟：

1. 包含專案檔案。
1. 建立Acrobat Reader DC擴充功能使用者端物件。
1. 擷取已啟用許可權的PDF檔案。
1. 擷取認證的相關資訊。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

**建立Acrobat Reader DC擴充功能使用者端物件**

您必須先建立Acrobat Reader DC擴充功能服務使用者端物件，才能以程式設計方式執行Acrobat Reader DC擴充功能服務作業。 如果您使用Java API，請建立 `ReaderExtensionsServiceClient` 物件。 如果您使用Acrobat Reader DC擴充功能Web服務API，請建立 `ReaderExtensionsServiceService` 物件。

**擷取啟用許可權的PDF檔案**

您必須擷取已啟用許可權的PDF檔案，才能擷取關於認證的資訊。 您也可以透過指定認證的別名來擷取其相關資訊；不過，如果您要擷取用於套用使用許可權至特定啟用許可權的PDF檔案的認證相關資訊，則必須擷取該檔案。

**擷取認證的相關資訊**

擷取啟用許可權的PDF檔案後，您可以取得用來套用使用許可權的認證相關資訊。 您可以取得下列關於認證的資訊：

* 當啟用許可權的PDF檔案開啟時，Adobe Reader中顯示的訊息。
* 認證不再有效的日期。
* 認證無效的日期。
* 為此許可權啟用的PDF檔案設定的使用許可權。
* 已使用認證的次數。

**另请参阅**

[使用Java API移除使用許可權](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服務API移除使用許可權](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC擴充功能服務API快速入門](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API擷取認證資訊 {#retrieve-credential-information-using-the-java-api}

使用Acrobat Reader DC擴充功能API (Java)擷取認證資訊：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-reader-extensions-client.jar。

1. 建立Acrobat Reader DC擴充功能使用者端物件。

   建立 `ReaderExtensionsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 包含連線屬性的物件。

1. 擷取PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用許可權啟用PDF檔案的建構函式，並傳遞字串值(指定許可權啟用PDF檔案的位置)來代表許可權啟用檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 從PDF檔案中移除使用許可權。

   * 透過叫用，擷取用於套用使用許可權至PDF檔案的認證相關資訊 `ReaderExtensionsServiceClient` 物件的 `getDocumentUsageRights` 方法和傳遞 `com.adobe.idp.Document` 包含已啟用許可權的PDF檔案的物件。 此方法會傳回 `GetUsageRightsResult` 包含認證資訊的物件。
   * 透過叫用 `GetUsageRightsResult` 物件的 `getNotAfter` 方法。 此方法會傳回 `java.util.Date` 物件，代表認證不再有效的日期。
   * 透過叫用「 」，擷取在啟用許可權的PDF檔案開啟時在Adobe Reader中顯示的訊息 `GetUsageRightsResult` 物件的 `getMessage` 方法。 此方法會傳回代表訊息的字串值。

**另请参阅**

[正在擷取認證資訊](assigning-usage-rights.md#retrieving-credential-information)

[快速入門（SOAP模式）：使用Java API擷取認證資訊](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API擷取認證資訊 {#retrieve-credential-information-using-the-web-service-api}

使用Acrobat Reader DC擴充功能API （Web服務）擷取認證資訊：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 請確定您使用下列WSDL定義： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立Acrobat Reader DC擴充功能使用者端物件。

   * 建立 `ReaderExtensionsServiceClient` 物件（使用其預設建構函式）。
   * 建立 `ReaderExtensionsServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 請務必指定 `?blob=mtom`.)
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `ReaderExtensionsServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 將對應的密碼值指派給欄位 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 指派常數值 `HttpClientCredentialType.Basic` 至欄位 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至欄位 `BasicHttpBindingSecurity.Security.Mode`.

1. 擷取PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存啟用許可權的PDF檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表已啟用rights之PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 從PDF檔案中移除使用許可權。

   * 透過叫用，擷取用於套用使用許可權至PDF檔案的認證相關資訊 `ReaderExtensionsServiceClient` 物件的 `getDocumentUsageRights` 方法和傳遞 `com.adobe.idp.Document` 包含已啟用許可權的PDF檔案的物件。 此方法會傳回 `GetUsageRightsResult` 包含認證資訊的物件。
   * 透過取得「 」的值，擷取認證不再有效的日期 `GetUsageRightsResult` 物件的 `notAfter` 資料成員。 此資料成員的資料型別為 `System.DateTime`.
   * 透過取得「 」的值，擷取在Adobe Reader中開啟啟用許可權的PDF檔案時顯示的訊息 `GetUsageRightsResult` 物件的 `message` 資料成員。 此資料成員的資料型別為字串。
   * 透過取得「 」的值，擷取使用認證的次數 `GetUsageRightsResult` 物件的 `useCount` 資料成員。 此資料成員的資料型別是整數。

**另请参阅**

[正在擷取認證資訊](assigning-usage-rights.md#retrieving-credential-information)

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
