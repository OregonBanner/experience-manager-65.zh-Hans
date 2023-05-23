---
title: 使用可流動版面預先填入Forms
seo-title: Prepopulating Forms with Flowable Layouts
description: 以可流動版面配置預先填入表單，以使用Java API和Web服務API在轉譯的表單內向使用者顯示資料。
seo-description: Prepopulate forms with flowable layout to display data to users within a rendered form using the Java API and the Web Service API.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 0%

---

# 使用可流動版面預先填入Forms {#prepopulating-forms-with-flowable-layouts1}

## 使用可流動版面預先填入Forms {#prepopulating-forms-with-flowable-layouts2}

預先填入表單會在轉譯的表單中向使用者顯示資料。 例如，假設使用者使用使用者名稱和密碼登入網站。 如果驗證成功，使用者端應用程式會查詢資料庫以取得使用者資訊。 資料會合併至表單，然後表單會呈現給使用者。 因此，使用者可以在表單中檢視個人化資料。

預先填入表單具有以下優點：

* 讓使用者在表單中檢視自訂資料。
* 減少輸入使用者填寫表單的次數。
* 控制資料放置的位置，確保資料完整性。

下列兩個XML資料來源可以預先填入表單：

* XDP資料來源，即符合XFA語法的XML (或是預先填入使用Acrobat建立的表單的XFDF資料)。
* 任意XML資料來源，包含符合表單欄位名稱的名稱/值組（本節中的範例使用任意XML資料來源）。

要預先填入的每個表單欄位都必須有XML元素。 XML元素名稱必須符合欄位名稱。 如果XML元素未對應至表單欄位，或XML元素名稱不符合欄位名稱，則會忽略該元素。 只要已指定所有XML元素，就不需要比對XML元素的顯示順序。

預先填入已包含資料的表單時，您必須指定已在XML資料來源中顯示的資料。 假設包含10個欄位的表單有4個欄位中的資料。 接下來，假設您要預先填入其餘六個欄位。 在此情況下，您必須在XML資料來源中指定10個XML元素，用於預先填入表單。 如果您只指定六個元素，則原始的四個欄位為空白。

例如，您可以預先填入表單，例如範例確認表單。 (請參閱下列「確認表單」： [呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)

若要預先填入範例確認表單，您必須建立包含三個XML元素的XML資料來源，這些XML元素符合表單中的三個欄位。 此表單包含下列三個欄位： `FirstName`， `LastName`、和 `Amount`. 第一步是建立XML資料來源，其中包含符合表單設計中欄位的XML元素。 下一步是將資料值指派給XML元素，如下列XML程式碼所示。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

使用此XML資料來源預先填入確認表單，然後轉譯表單後，您指派給XML元素的資料值會顯示出來，如下圖所示。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 使用可流動版面預先填入表單 {#prepopulating_forms_with_flowable_layouts-1}

具有可流動版面的Forms在向使用者顯示未確定的資料量時很有用。 由於表單的版面會自動根據合併的資料量進行調整，因此您不需要像處理具有固定版面的表單那樣預先決定表單的固定版面或頁數。

表單通常會填入執行階段期間取得的資料。 因此，您可以建立記憶體內XML資料來源，並將資料直接放入記憶體內XML資料來源，以預先填入表單。

考慮網路型應用程式，例如線上商店。 線上購物者完成購買料號後，所有購買料號都會放入記憶體中的XML資料來源，用來預先填入表單。 下圖顯示此程式，圖後的表格對此程式進行了說明。

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

下表說明此圖表中的步驟。

<table>
 <thead>
  <tr>
   <th><p>步骤</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>使用者從網路型線上商店購買商品。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>使用者完成採購料號並按一下「提交」按鈕後，即會建立記憶體內XML資料來源。 購買的專案和使用者資訊會放入記憶體中的XML資料來源中。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML資料來源可用來預先填入採購單表單（此表單的範例顯示於此表格下方）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>採購單表單會呈現至使用者端網頁瀏覽器。 </p></td>
  </tr>
 </tbody>
</table>

下圖顯示採購單表單的範例。 表格中的資訊可根據XML資料中的記錄數進行調整。

![pf_pf_proform](assets/pf_pf_poform.png)

>[!NOTE]
>
>表單可以預先填入其他來源（例如企業資料庫或外部應用程式）的資料。

### 表單設計考量事項 {#form-design-considerations}

具有可流動版面的Forms是根據在Designer中建立的表單設計。 表單設計會指定一組版面、顯示和資料擷取規則，包括根據使用者輸入計算值。 將資料輸入表單時會套用規則。 新增至表單的欄位是表單設計內的子表單。 例如，在上圖所示的採購單表單中，每一行都是子表單。 如需有關建立包含子表單的表單設計的資訊，請參閱 [建立具有可流程配置的採購單表單](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### 瞭解資料子群組 {#understanding-data-subgroups}

XML資料來源可用來預先填入具有固定版面和可流動版面的表單。 不過，不同之處在於，以可流動版面配置預先填入表單的XML資料來源，包含用於預先填入表單內重複的子表單的重複XML元素。 這些重複的XML元素稱為資料子群組。

用來預先填入上圖所示之採購單表單的XML資料來源包含四個重複資料子群組。 每個資料子群組都與購買的專案相對應。 購買的專案包括顯示器、檯燈、電話和通訊錄。

下列XML資料來源可用來預先填入採購單表單。

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

請注意，每個資料子群組都包含四個對應至下列資訊的XML元素：

* 專案零件編號
* 專案說明
* 料號數量
* 單價

資料子群組的父項XML元素名稱必須與表單設計中的子表單名稱相符。 例如，在上圖中，請注意資料子群組的父項XML元素名稱為 `detail`. 這會對應到位於採購單表單所依據之表單設計中的子表單名稱。 如果資料子群組的父XML元素名稱與子表單不符，則不會預先填入伺服器端表單。

每個資料子群組都必須包含符合子表單中欄位名稱的XML元素。 此 `detail` 位於表單設計中的子表單包含以下欄位：

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>如果您嘗試使用包含重複XML元素的資料來源預先填入表單，並設定 `RenderAtClient` 選項至 `No`，只有第一筆資料記錄會合併至表單中。 為確保所有資料記錄都合併至表單中，請設定 `RenderAtClient` 至 `Yes`. 如需關於以下專案的資訊： `RenderAtClient` 選項，請參閱 [在使用者端轉譯Forms](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要以可流動的版面配置預先填入表單，請執行下列工作：

1. 包含專案檔案。
1. 建立記憶體中的XML資料來源。
1. 轉換XML資料來源。
1. 呈現預先填入的表單。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立記憶體內XML資料來源**

您可以使用 `org.w3c.dom` 類別來建立記憶體內XML資料來源，以預先填入具有可流動配置的表單。 您必須將資料放入符合表單的XML資料來源中。 如需有關具有可流動版面的表單與XML資料來源之間關係的資訊，請參閱 [瞭解資料子群組](#understanding-data-subgroups).

**轉換XML資料來源**

使用建立的記憶體內XML資料來源 `org.w3c.dom` 類別可以轉換為 `com.adobe.idp.Document` 物件，才能用來預先填入表單。 您可以使用Java XML轉換類別來轉換記憶體中的XML資料來源。

>[!NOTE]
>
>如果您使用Forms服務的WSDL預先填入表單，您必須將 `org.w3c.dom.Document` 物件放入 `BLOB` 物件。

**呈現預先填入的表單**

您呈現的預先填入表單與其他表單類似。 唯一的區別是您使用 `com.adobe.idp.Document` 包含要預先填入表單之XML資料來源的物件。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API預先填入表單 {#prepopulating-forms-using-the-java-api}

若要使用Forms API (Java)預先填入具有流動版面的表單，請執行以下步驟：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。 如需有關這些檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. 建立記憶體內XML資料來源

   * 建立Java `DocumentBuilderFactory` 物件，方法是呼叫 `DocumentBuilderFactory` 類別&#39; `newInstance` 方法。
   * 建立Java `DocumentBuilder` 物件，方法是呼叫 `DocumentBuilderFactory` 物件的 `newDocumentBuilder` 方法。
   * 呼叫 `DocumentBuilder` 物件的 `newDocument` 具現化的方法 `org.w3c.dom.Document` 物件。
   * 透過叫用 `org.w3c.dom.Document` 物件的 `createElement` 方法。 這會建立 `Element` 代表根元素的物件。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，透過呼叫 `Document` 物件的 `appendChild` 方法，並將根元素物件傳遞為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫 `Document` 物件的 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，透過呼叫 `root` 物件的 `appendChild` 方法，並將標頭元素物件傳遞為引數。 附加至標頭元素的XML元素會對應至表單的靜態部分。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 建立屬於header元素的子元素，方法是呼叫 `Document` 物件的 `createElement` 方法，並傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 接著，呼叫子元素的 `appendChild` 方法，並傳遞 `Document` 物件的 `createTextNode` 作為引數的方法。 指定顯示為子專案值的字串值。 最後，呼叫標題元素的，將子元素附加至標題元素 `appendChild` 方法，並將子元素物件傳遞為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * 重複表單靜態部分出現的每個欄位的最後一個子步驟（在XML資料來源圖表中，這些欄位顯示在A節中），將所有剩餘的元素新增到標題元素中。(請參閱 [瞭解資料子群組](#understanding-data-subgroups).)
   * 呼叫 `Document` 物件的 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，透過呼叫 `root` 物件的 `appendChild` 方法，並將詳細資訊元素物件作為引數傳遞。 附加至詳細資訊元素的XML元素會對應至表單的動態部分。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫「 」以建立屬於詳細資料元素的子元素。 `Document` 物件的 `createElement` 方法，並傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 接著，呼叫子元素的 `appendChild` 方法，並傳遞 `Document` 物件的 `createTextNode` 作為引數的方法。 指定顯示為子專案值的字串值。 最後，藉由呼叫詳細資料元素的，將子元素附加至詳細資料元素 `appendChild` 方法，並將子元素物件傳遞為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加至詳細資料元素。 若要正確建立用來填入採購單表單的XML資料來源，您必須將下列XML元素附加至明細元素： `txtDescription`， `numQty`、和 `numUnitPrice`.
   * 對用於預先填入表單的所有資料專案重複前兩個子步驟。

1. 轉換XML資料來源

   * 建立 `javax.xml.transform.Transformer` 物件(透過叫用 `javax.xml.transform.Transformer` 物件的靜態 `newInstance` 方法。
   * 建立 `Transformer` 物件(透過叫用 `TransformerFactory` 物件的 `newTransformer` 方法。
   * 建立 `ByteArrayOutputStream` 物件（使用其建構函式）。
   * 建立 `javax.xml.transform.dom.DOMSource` 物件，使用它的建構函式並傳遞 `org.w3c.dom.Document` 在步驟1中建立的物件。
   * 建立 `javax.xml.transform.dom.DOMSource` 物件，使用它的建構函式並傳遞 `ByteArrayOutputStream` 物件。
   * 填入Java `ByteArrayOutputStream` 物件(透過叫用 `javax.xml.transform.Transformer` 物件的 `transform` 方法和傳遞 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 物件。
   * 建立位元組陣列並配置的大小 `ByteArrayOutputStream` 物件至位元組陣列。
   * 透過叫用「 」填入位元組陣列 `ByteArrayOutputStream` 物件的 `toByteArray` 方法。
   * 建立 `com.adobe.idp.Document` 物件，使用它的建構函式並傳遞位元組陣列。

1. 呈現預先填入的表單

   叫用 `FormsServiceClient` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。 確保您使用 `com.adobe.idp.Document` 在步驟1和2中建立的物件。
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流傳送至使用者端web瀏覽器的物件。
   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，叫用 `InputStream` 物件的 `read` 方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。


**另请参阅**

[快速入門（SOAP模式）：使用Java API以可流動的版面預先填入Forms](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API預先填入表單 {#prepopulating-forms-using-the-web-service-api}

若要使用Forms API （Web服務）預先填入具有流動版面的表單，請執行以下步驟：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。 (請參閱 [使用Apache Axis建立Java Proxy類別](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立記憶體內XML資料來源

   * 建立Java `DocumentBuilderFactory` 物件，方法是呼叫 `DocumentBuilderFactory` 類別&#39; `newInstance` 方法。
   * 建立Java `DocumentBuilder` 物件，方法是呼叫 `DocumentBuilderFactory` 物件的 `newDocumentBuilder` 方法。
   * 呼叫 `DocumentBuilder` 物件的 `newDocument` 具現化的方法 `org.w3c.dom.Document` 物件。
   * 透過叫用 `org.w3c.dom.Document` 物件的 `createElement` 方法。 這會建立 `Element` 代表根元素的物件。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，透過呼叫 `Document` 物件的 `appendChild` 方法，並將根元素物件傳遞為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * 呼叫 `Document` 物件的 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，透過呼叫 `root` 物件的 `appendChild` 方法，並將標頭元素物件傳遞為引數。 附加至標頭元素的XML元素會對應至表單的靜態部分。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * 建立屬於header元素的子元素，方法是呼叫 `Document` 物件的 `createElement` 方法，並傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 接著，呼叫子元素的 `appendChild` 方法，並傳遞 `Document` 物件的 `createTextNode` 作為引數的方法。 指定顯示為子專案值的字串值。 最後，呼叫標題元素的，將子元素附加至標題元素 `appendChild` 方法，並將子元素物件傳遞為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * 重複表單靜態部分出現的每個欄位的最後一個子步驟（在XML資料來源圖表中，這些欄位顯示在A節中），將所有剩餘的元素新增到標題元素中。(請參閱 [瞭解資料子群組](#understanding-data-subgroups).)
   * 呼叫 `Document` 物件的 `createElement` 方法。 將代表元素名稱的字串值傳遞至 `createElement` 方法。 將傳回值轉換為 `Element`. 接下來，透過呼叫 `root` 物件的 `appendChild` 方法，並將詳細資訊元素物件作為引數傳遞。 附加至詳細資訊元素的XML元素會對應至表單的動態部分。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 呼叫「 」以建立屬於詳細資料元素的子元素。 `Document` 物件的 `createElement` 方法，並傳遞代表元素名稱的字串值。 將傳回值轉換為 `Element`. 接著，呼叫子元素的 `appendChild` 方法，並傳遞 `Document` 物件的 `createTextNode` 作為引數的方法。 指定顯示為子專案值的字串值。 最後，藉由呼叫詳細資料元素的，將子元素附加至詳細資料元素 `appendChild` 方法，並將子元素物件傳遞為引數。 下列幾行程式碼顯示此應用程式邏輯：

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 對所有XML元素重複最後一個子步驟，以附加至詳細資料元素。 若要正確建立用來填入採購單表單的XML資料來源，您必須將下列XML元素附加至明細元素： `txtDescription`， `numQty`、和 `numUnitPrice`.
   * 對用於預先填入表單的所有資料專案重複前兩個子步驟。

1. 轉換XML資料來源

   * 建立 `javax.xml.transform.Transformer` 物件(透過叫用 `javax.xml.transform.Transformer` 物件的靜態 `newInstance` 方法。
   * 建立 `Transformer` 物件(透過叫用 `TransformerFactory` 物件的 `newTransformer` 方法。
   * 建立 `ByteArrayOutputStream` 物件（使用其建構函式）。
   * 建立 `javax.xml.transform.dom.DOMSource` 物件，使用它的建構函式並傳遞 `org.w3c.dom.Document` 在步驟1中建立的物件。
   * 建立 `javax.xml.transform.dom.DOMSource` 物件，使用它的建構函式並傳遞 `ByteArrayOutputStream` 物件。
   * 填入Java `ByteArrayOutputStream` 物件(透過叫用 `javax.xml.transform.Transformer` 物件的 `transform` 方法和傳遞 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 物件。
   * 建立位元組陣列並配置的大小 `ByteArrayOutputStream` 物件至位元組陣列。
   * 透過叫用「 」填入位元組陣列 `ByteArrayOutputStream` 物件的 `toByteArray` 方法。
   * 建立 `BLOB` 物件（使用其建構函式）並叫用其 `setBinaryData` 方法並傳遞位元組陣列。

1. 呈現預先填入的表單

   叫用 `FormsService` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * A `BLOB` 包含要與表單合併之資料的物件。 確保您使用 `BLOB` 在步驟一和步驟二中建立的物件。
   * A `PDFFormRenderSpecc` 儲存執行階段選項的物件。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 方法填入的物件。 這可用來儲存轉譯的PDF表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 方法填入的物件。 （此引數會儲存表單中的頁數）。
   * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。 （此引數會儲存地區設定值）。
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 將包含此作業結果的物件。

   此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 以表單資料流傳遞作為最後一個引數值的物件，必須寫入使用者端Web瀏覽器。

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件的 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
   * 取得的內容型別 `BLOB` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立位元組陣列，並透過叫用 `BLOB` 物件的 `getBinaryData` 方法。 此任務指派 `FormsResult` 物件至位元組陣列。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

   >[!NOTE]
   >
   >此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 以表單資料流傳遞作為最後一個引數值的物件，必須寫入使用者端Web瀏覽器。

**另请参阅**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
