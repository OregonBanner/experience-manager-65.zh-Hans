---
title: 組合已加密的PDF檔案
seo-title: Assembling Encrypted PDF Documents
description: 使用Java API和Web服務API彙編加密的PDF檔案。
seo-description: Assemble encrypted PDF documents using the Java API and Web Service API.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 0%

---

# 組合已加密的PDF檔案 {#assembling-encrypted-pdf-documents}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

您可以使用Assembler服務，以密碼加密PDF檔案。 使用密碼加密PDF檔案後，使用者必須指定密碼，才能在Adobe Reader或Acrobat中檢視PDF檔案。 若要使用密碼加密PDF檔案，DDX檔案必須包含加密PDF檔案所需的加密元素值。

為了進行此討論，假設使用下列DDX檔案。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

在此DDX檔案中，請注意已將值指派給來源屬性 `inDoc`. 在只有一個輸入PDF檔案傳遞到Assembler服務並傳回一個PDF檔案的情況下，您呼叫 `invokeOneDocument` 作業，指派值 `inDoc` 至PDF來源屬性。 叫用 `invokeOneDocument` 作業， `inDoc` value是預先定義的索引鍵，必須在DDX檔案中指定。

相反地，將兩個或多個輸入PDF檔案傳遞至組合器服務時，您可以叫用 `invokeDDX` 作業。 在此情況下，將輸入PDF檔案的檔案名稱指派給 `source` 屬性。

加密服務不一定要成為AEM表單安裝的一部分，才能使用密碼加密PDF檔案。 另請參閱 [加密和解密PDF檔案](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

若要組合已加密的PDF檔案，請執行下列步驟：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考不安全的PDF檔案。
1. 設定執行階段選項。
1. 加密檔案。
1. 儲存加密的PDF檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

如果AEM Forms部署在支援的J2EE應用程式伺服器上，而不是JBoss，您必須將adobe-utilities.jar和jbossall-client.jar檔案取代為特定於AEM Forms部署所在之J2EE應用程式伺服器的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立組合器使用者端**

您必須先建立Assembler服務使用者端，才能以程式設計方式執行Assembler作業。

**參考現有的DDX檔案**

必須參考DDX檔案才能組裝PDF檔案。 例如，請考量本節介紹的DDX檔案。 若要加密PDF檔案，DDX檔案必須包含 `PasswordEncryptionProfile` 元素。

**參考不安全的PDF檔案**

必須參考不安全的PDF檔案，並將其傳遞至彙編程式服務以進行加密。 如果您參照已加密的PDF檔案，則會擲回例外狀況。

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。 如需您可以設定的執行階段選項的相關資訊，請參閱 `AssemblerOptionSpec` 中的類別參考 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**加密檔案**

建立Assembler服務使用者端、參照包含加密資訊的DDX檔案、參照不安全的PDF檔案，以及設定執行階段選項之後，您可以叫用 `invokeOneDocument` 作業。 由於只有一個輸入PDF檔案傳遞到Assembler服務（並且會傳回一個檔案），因此您可以使用 `invokeOneDocument` 操作而非 `invokeDDX` 作業。

**儲存加密的PDF檔案**

如果只有單一PDF檔案傳遞至Assembler服務，Assembler服務會傳回單一檔案，而非集合物件。 也就是說，叫用 `invokeOneDocument` 作業時，會傳回單一檔案。 由於本節中參考的DDX檔案包含加密資訊，因此Assembler服務會傳回使用密碼加密的PDF檔案。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組裝PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API彙編加密的PDF檔案 {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值（指定DDX檔案的位置）來代表DDX檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 參考不安全的PDF檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞不安全PDF檔案的位置。
   * 建立 `com.adobe.idp.Document` 物件並傳遞 `java.io.FileInputStream` 包含PDF檔案的物件。 此 `com.adobe.idp.Document` 物件傳遞至 `invokeOneDocument` 方法。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 透過叫用屬於以下專案的方法，設定執行階段選項以滿足您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用 `AssemblerOptionSpec` 物件的 `setFailOnError` 方法與傳遞 `false`.

1. 加密檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeOneDocument` 方法並傳遞下列值：

   * A `com.adobe.idp.Document` 代表DDX檔案的物件。 確定此DDX檔案包含值 `inDoc` (PDF來源元素)。
   * A `com.adobe.idp.Document` 包含不安全PDF檔案的物件。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項的物件，包括預設字型和作業記錄層級。

   此 `invokeOneDocument` 方法傳回 `com.adobe.idp.Document` 包含密碼加密PDF檔案的物件。

1. 儲存加密的PDF檔案。

   * 建立 `java.io.File` 物件並確保副檔名為.pdf。
   * 叫用 `Document` 物件的 `copyToFile` 複製目錄內容的方法 `Document` 物件至檔案。 確保您使用 `Document` 物件， `invokeOneDocument` 方法已傳回。

**另请参阅**

[快速入門（SOAP模式）：使用Java API組合已加密的PDF檔案](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## 使用Web服務API彙編加密的PDF檔案 {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 設定服務參考時，請務必使用下列WSDL定義： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立組合器使用者端。

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
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 參考不安全的PDF檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入PDF檔案。 此 `BLOB` 物件傳遞至 `invokeOneDocument` 作為引數。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表輸入PDF檔案的檔案位置以及開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法，並傳遞位元組陣列、起始位置以及要讀取的資料流長度。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將值指派給屬於下列專案的資料成員，以設定執行階段選項，符合您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請指派 `false` 至 `AssemblerOptionSpec` 物件的 `failOnError` 資料成員。

1. 加密檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeOneDocument` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件
   * A `BLOB` 代表不安全PDF檔案的物件
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件

   此 `invokeOneDocument` 方法傳回 `BLOB` 包含加密PDF檔案的物件。

1. 儲存加密的PDF檔案。

   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表加密PDF檔案檔案位置的字串值，以及用來開啟檔案的模式。
   * 建立位元組陣列，儲存 `BLOB` 物件， `invokeOneDocument` 方法已傳回。 透過取得 `BLOB` 物件的 `MTOM` 資料成員。
   * 建立 `System.IO.BinaryWriter` 物件，方法是叫用其建構函式並傳遞 `System.IO.FileStream` 物件。
   * PDF透過叫用 `System.IO.BinaryWriter` 物件的 `Write` 方法並傳遞位元組陣列。

**另请参阅**

[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
