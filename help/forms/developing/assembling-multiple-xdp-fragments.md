---
title: 組合多個XDP片段
seo-title: Assembling Multiple XDP Fragments
description: 使用Java API和Web服務API將多個XDP片段組合成一個XDP檔案。
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# 組合多個XDP片段{#assembling-multiple-xdp-fragments}

您可以將多個XDP片段組合成一個XDP檔案。 例如，考慮XDP片段，其中每個XDP檔案都包含一個或多個用於建立健康情況表單的子表單。 下圖顯示輪廓檢視(代表tuc018_template_flowed.xdp檔案，用於 *組合多個XDP片段* 快速入門)：

![am_am_forma](assets/am_am_forma.png)

下圖顯示病人區段(代表tuc018_contact.xdp檔案，用於 *組合多個XDP片段* 快速入門)：

![am_am_formb](assets/am_am_formb.png)

下圖顯示病人健康部分(代表tuc018_patient.xdp檔案，用於 *組合多個XDP片段* 快速入門)：

![am_am_formc](assets/am_am_formc.png)

此片段包含兩個名為的子表單 *subPatientPhysical* 和 *subPatientHealth*. 這兩個子表單都會在傳遞至組合器服務的DDX檔案中參考。 使用Assembler服務，您可以將所有這些XDP片段合併到單一XDP檔案中，如下圖所示。

![am_am_formd](assets/am_am_formd.png)

下列DDX檔案將多個XDP片段組合到XDP檔案中。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

DDX檔案包含XDP `result` 指定結果名稱的標籤。 在此情況下，值為 `tuc018result.xdp`. 在Assembler服務傳回結果後，此值會在用於擷取XDP檔案的應用程式邏輯中參考。 例如，考慮用於擷取已組裝XDP檔案的下列Java應用程式邏輯（請注意值為粗體）：

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

此 `XDP source` tag指定代表完整XDP檔案的XDP檔案，該檔案可用作新增XDP片段的容器，或作為按順序附加在一起的多個檔案之一。 在此情況下，XDP檔案僅會作為容器使用(第一個圖例顯示於 *組合多個XDP片段*)。 也就是說，其他XDP檔案會放置在XDP容器中。

您可以為每個子表單新增 `XDPContent` 元素（此元素為選用）。 在上述範例中，請注意有三個子表單： `subPatientContact`， `subPatientPhysical`、和 `subPatientHealth`. 兩者皆有 `subPatientPhysical` 子表單和 `subPatientHealth` 子表單位於相同的XDP檔案tuc018_patient.xdp中。 片段元素會指定子表單的名稱，如Designer中所定義。

>[!NOTE]
>
>如需有關組合器服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>如需有關DDX檔案的詳細資訊，請參閱 [組合器服務和DDX參考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步驟摘要 {#summary-of-steps}

若要組合多個XDP片段，請執行下列工作：

1. 包含專案檔案。
1. 建立PDF組合器使用者端。
1. 參考現有的DDX檔案。
1. 參考XDP檔案。
1. 設定執行階段選項。
1. 組合多個XDP檔案。
1. 擷取組裝的XDP檔案。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

必須將以下JAR檔案新增到專案的類別路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (如果AEM Forms部署在JBoss上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss上，則為必要)

**建立PDF組合器使用者端**

以程式設計方式執行Assembler作業之前，請先建立Assembler服務使用者端。

**參考現有的DDX檔案**

必須參考DDX檔案才能組合多個XDP檔案。 此DDX檔案必須包含 `XDP result`， `XDP source`、和 `XDPContent` 元素。

**參考XDP檔案**

若要組裝多個XDP檔案，請參照用來組裝結果XDP檔案的所有XDP檔案。 請確定所參考的XDP檔案中包含的子表單名稱 `source` 屬性指定於 `fragment` 屬性。 子表單在Designer中定義。 例如，請考量下列XML。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名為的子表單 *subPatientContact* 必須位於名為的XDP檔案中 *tuc018_contact.xdp*.

**設定執行階段選項**

您可以設定執行階段選項，控制Assembler服務執行工作時的行為。 例如，您可以設定一個選項，在遇到錯誤時指示Assembler服務繼續處理工作。

**組合多個XDP檔案**

若要組合多個XDP檔案，請呼叫 `invokeDDX` 作業。 Assembler服務會傳回集合物件中的已組裝XDP檔案。

**擷取組裝的XDP檔案**

已組裝的XDP檔案會在集合物件中傳回。 逐一檢視集合物件，並將XDP檔案儲存為XDP檔案。 您也可以將XDP檔案傳遞至其他AEM Forms服務，例如輸出。

**另请参阅**

[使用Java API組合多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用網站服務API組合多個XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以程式設計方式組裝PDF檔案](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段建立PDF檔案](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API組合多個XDP片段 {#assemble-multiple-xdp-fragments-using-the-java-api}

使用組合器服務API (Java)組合多個XDP片段：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-assembler-client.jar。

1. 建立PDF組合器使用者端。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `AssemblerServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考現有的DDX檔案。

   * 建立 `java.io.FileInputStream` 物件，使用它的建構函式並傳遞字串值（指定DDX檔案的位置）來代表DDX檔案。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞 `java.io.FileInputStream` 物件。

1. 參考XDP檔案。

   * 建立 `java.util.Map` 用來儲存輸入XDP檔案的物件(使用 `HashMap` 建構函式。
   * 建立 `com.adobe.idp.Document` 物件並傳遞 `java.io.FileInputStream` 包含輸入XDP檔案的物件（對每個XDP檔案重複此工作）。
   * 將專案新增至 `java.util.Map` 物件(透過叫用其 `put` 方法並傳遞下列引數：

      * 代表機碼名稱的字串值。 此值必須與 `source` DDX檔案中指定的元素值（對每個XDP檔案重複此工作）。
      * A `com.adobe.idp.Document` 包含對應至物件的XDP檔案 `source` 元素（對每個XDP檔案重複此工作）。

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 透過叫用屬於以下專案的方法，設定執行階段選項以滿足您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請叫用 `AssemblerOptionSpec` 物件的 `setFailOnError` 方法與傳遞 `false`.

1. 組合多個XDP檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列必要值：

   * A `com.adobe.idp.Document` 代表要使用的DDX檔案的物件
   * A `java.util.Map` 包含輸入XDP檔案的物件
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定執行階段選項的物件，包括預設字型和作業記錄層級

   此 `invokeDDX` 方法傳回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含組合XDP檔案的物件。

1. 擷取組裝的XDP檔案。

   若要取得組裝的XDP檔案，請執行下列動作：

   * 叫用 `AssemblerResult` 物件的 `getDocuments` 方法。 此方法會傳回 `java.util.Map` 物件。
   * 循環瀏覽 `java.util.Map` 物件，直到您找到結果為止 `com.adobe.idp.Document` 物件。
   * 叫用 `com.adobe.idp.Document` 物件的 `copyToFile` 擷取組合XDP檔案的方法。

**另请参阅**

[組合多個XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[快速入門（SOAP模式）：使用Java API組裝多個XDP片段](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用網站服務API組合多個XDP片段 {#assemble-multiple-xdp-fragments-using-the-web-service-api}

使用組合器服務API （Web服務）組合多個XDP片段：

1. 包含專案檔案。

   建立使用MTOM的Microsoft .NET專案。 設定服務參考時，請務必使用下列WSDL定義：

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Replace `localhost` 搭配裝載AEM Forms之伺服器的IP位址。

1. 建立PDF組合器使用者端。

   * 建立 `AssemblerServiceClient` 物件（使用其預設建構函式）。
   * 建立 `AssemblerServiceClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務，例如 `https://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。
   * 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `AssemblerServiceClient.Endpoint.Binding` 欄位。 將傳回值轉換為 `BasicHttpBinding`.
   * 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 欄位至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
   * 執行下列工作來啟用基本HTTP驗證：

      * 將AEM表單使用者名稱指派給 `AssemblerServiceClient.ClientCredentials.UserName.UserName` 欄位。
      * 將對應的密碼值指派給 `AssemblerServiceClient.ClientCredentials.UserName.Password`欄位。
      * 指派 `HttpClientCredentialType.Basic` 的常數值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`欄位。
      * 指派 `BasicHttpSecurityMode.TransportCredentialOnly` 的常數值 `BasicHttpBindingSecurity.Security.Mode`欄位。

1. 參考現有的DDX檔案。

   * 建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件可用來儲存DDX檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表DDX檔案檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置和串流長度以讀取。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 具有位元組陣列內容的屬性。

1. 參考XDP檔案。

   * 針對每個輸入XDP檔案，建立 `BLOB` 物件（使用其建構函式）。 此 `BLOB` 物件是用來儲存輸入檔案。
   * 建立 `System.IO.FileStream` 物件，方法是叫用其建構函式，並傳遞代表輸入檔案的檔案位置和開啟檔案的模式的字串值。
   * 建立位元組陣列，儲存 `System.IO.FileStream` 物件。 您可以取得 `System.IO.FileStream` 物件的 `Length` 屬性。
   * 叫用 `System.IO.FileStream` 物件的 `Read` 方法。 傳遞位元組陣列、起始位置和串流長度以讀取。
   * 填入 `BLOB` 物件，透過指派其 `MTOM` 包含位元組陣列內容的欄位。
   * 建立 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 此集合物件用於儲存建立組合XDP檔案所需的輸入檔案。
   * 針對每個輸入檔案，建立 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件。
   * 將代表索引鍵名稱的字串值指派給 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `key` 欄位。 此值必須與DDX檔案中指定的元素值相符。 （對每個輸入XDP檔案執行此工作。）
   * 指派 `BLOB` 物件，將輸入檔案儲存至 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件的 `value` 欄位。 （對每個輸入XDP檔案執行此工作。）
   * 新增 `MyMapOf_xsd_string_To_xsd_anyType_Item` 物件至 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 叫用 `MyMapOf_xsd_string_To_xsd_anyType` 物件的 `Add` 方法並傳遞 `MyMapOf_xsd_string_To_xsd_anyType` 物件。 （針對每個輸入XDP檔案執行此工作。）

1. 設定執行階段選項。

   * 建立 `AssemblerOptionSpec` 物件，使用其建構函式來儲存執行階段選項。
   * 將值指派給屬於下列專案的資料成員，以設定執行階段選項，符合您的業務需求： `AssemblerOptionSpec` 物件。 例如，若要指示Assembler服務在發生錯誤時繼續處理工作，請指派 `false` 至 `AssemblerOptionSpec` 物件的 `failOnError` 資料成員。

1. 組合多個XDP檔案。

   叫用 `AssemblerServiceClient` 物件的 `invokeDDX` 方法並傳遞下列值：

   * A `BLOB` 代表DDX檔案的物件
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含必要檔案的物件
   * 一個 `AssemblerOptionSpec` 指定執行階段選項的物件

   此 `invokeDDX` 方法傳回 `AssemblerResult` 包含工作結果和發生之任何例外狀況的物件。

1. 擷取組裝的XDP檔案。

   若要取得新建立的XDP檔案，請執行下列動作：

   * 存取 `AssemblerResult` 物件的 `documents` 欄位，即 `Map` 包含結果PDF檔案的物件。
   * 循環瀏覽 `Map` 物件以取得每個產生的檔案。 然後，轉換該陣列成員的 `value` 至 `BLOB`.
   * 存取代表PDF檔案的二進位資料 `BLOB` 物件的 `MTOM` 屬性。 這會傳回您可以寫出至XDP檔案的位元組陣列。

**另请参阅**

[組合多個XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
