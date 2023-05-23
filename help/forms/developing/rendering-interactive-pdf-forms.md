---
title: 呈現互動式PDF forms
seo-title: Rendering Interactive PDF Forms
description: 使用Forms服務向客戶裝置（通常是網頁瀏覽器）呈現互動式PDF forms，以便從使用者收集資訊。 您可以使用Forms服務，透過Java API和Web服務API來轉譯互動式表單。
seo-description: Use the Forms service to render interactive PDF forms to client devices, typically web browsers, to collect information from users. You can use Forms service to render interactive forms using the Java API and Web Service API.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 0%

---

# 呈現互動式PDF forms {#rendering-interactive-pdf-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

Forms服務會將互動式PDF forms轉譯給使用者端裝置（通常是網頁瀏覽器），以從使用者收集資訊。 呈現互動式表單後，使用者可在表單欄位中輸入資料，然後按一下表單上的提交按鈕，將資訊傳回Forms服務。 使用者端Web瀏覽器所在的電腦必須安裝Adobe Reader或Acrobat，互動式PDF表單才能顯示。

>[!NOTE]
>
>使用Forms服務轉譯表單之前，請先建立表單設計。 通常，表單設計會在Designer中建立並儲存為XDP檔案。 如需建立表單設計的相關資訊，請參閱 [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

**範例貸款申請**

引入範例貸款應用程式，以示範Forms服務如何使用互動式表單從使用者收集資訊。 此應用程式可讓使用者填寫包含取得貸款所需資料的表單，然後將資料提交至Forms服務。 下圖顯示貸款應用程式的邏輯流程。

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

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
   <td><p>此 <code>GetLoanForm</code> 從HTML頁面叫用Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>此 <code>GetLoanForm</code> Java Servlet使用Forms服務使用者端API將貸款表單轉譯給使用者端網頁瀏覽器。 (請參閱 <a href="#render-an-interactive-pdf-form-using-the-java-api">使用Java API演算互動式PDF表單</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者填寫貸款表單並按一下提交按鈕後，資料就會提交至 <code>HandleData</code> Java Servlet。 (請參閱 <i>"貸款表單"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>此 <code>HandleData</code> Java Servlet使用Forms服務使用者端API來處理表單提交和擷取表單資料。 然後，資料會儲存在企業資料庫中。 (請參閱 <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">處理已提交的Forms</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認表單會轉譯回網頁瀏覽器。 使用者名字和姓氏等資料在轉譯前會與表單合併。 (請參閱 <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">使用可流動版面預先填入Forms</a>.)</p></td>
  </tr>
 </tbody>
</table>

**貸款表單**

此互動式貸款表單由範例貸款申請表的 `GetLoanForm` Java Servlet。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認表單**

此表單由範例貸款申請的 `HandleData` Java Servlet。

![ri_ri_confirm](assets/ri_ri_confirm.png)

此 `HandleData` Java Servlet會使用使用者的名字、姓氏及數量預先填入此表單。 預先填入表單後，會傳送至使用者端Web瀏覽器。 (請參閱 [使用可流動版面預先填入Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Java Servlet**

範例貸款應用程式是以Java Servlet存在的Forms服務應用程式範例。 Java Servlet是在J2EE應用程式伺服器（例如WebSphere）上執行的Java程式，並包含Forms服務使用者端API程式碼。

下列程式碼顯示名為GetLoanForm的Java Servlet語法：

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

一般而言，您不會將Forms服務使用者端API程式碼放在Java Servlet的 `doGet` 或 `doPost` 方法。 程式設計實務最好將此程式碼放在另一個類別中，從內部例項化類別 `doPost` 方法(或 `doGet` 方法)，並呼叫適當的方法。 不過，為求程式碼簡潔，本節中的程式碼範例會儘量減少，而程式碼範例會放在 `doPost` 方法。

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

**步驟摘要**

若要呈現互動式PDF表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 指定URI值。
1. 將檔案附加至表單（選擇性）。
1. 演算互動式PDF表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms使用者端API物件，才能以程式設計方式執行Forms服務使用者端API作業。 如果您使用Java API，請建立 `FormsServiceClient` 物件。 如果您使用Forms Web服務API，請建立 `FormsService` 物件。

**指定URI值**

您可以指定Forms服務轉譯表單所需的URI值。 使用內容根URI值，可參考儲存為Forms應用程式一部分的表單設計 `repository:///`. 例如，考慮以下名為的表單設計 *Loan.xdp* 位在名為的Forms應用程式中 *表單應用程式*：

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

若要存取此表單設計，請指定 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` 作為表單名稱(傳遞給 `renderPDFForm` 方法)和 `repository:///` 作為內容根URI值。

>[!NOTE]
>
>如需使用Workbench建立Forms應用程式的詳細資訊，請參閱 [Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63).

位於Forms應用程式中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

下列值顯示一些URI值的範例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

當您轉譯互動式表單時，可以定義URI值，例如將表單資料發佈到的目標URL。 目標URL可透過下列其中一種方式定義：

* 在Designer中設計表單設計時按一下「提交」按鈕
* 使用Forms服務使用者端API

如果目標URL是在表單設計內定義，請勿使用Forms服務使用者端API加以覆寫。 也就是說，使用Forms API設定目標URL會將表單設計中的指定URL重設為使用API指定的URL。 如果您想要將PDF表單提交至表單設計中所指定的目標URL，則以程式設計方式將目標URL設定為空字串。

如果您的表單包含提交按鈕和計算按鈕（具有在伺服器上執行的對應指令碼），您可以以程式設計方式定義將表單傳送至哪個URL以執行指令碼。 使用表單設計上的提交按鈕，指定將表單資料發佈到的URL。 (請參閱 [計算表單資料](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>您也可以傳遞URL值來參照XDP檔案，而不是指定URL值 `com.adobe.idp.Document` Forms服務的執行個體。 此 `com.adobe.idp.Document` 例項包含表單設計。 (請參閱 [將檔案傳遞至Forms服務](/help/forms/developing/passing-documents-forms-service.md).)

**將檔案附加至表單**

您可以將檔案附加至表單。 當您轉譯含有檔案附件的PDF表單時，使用者可以使用檔案附件窗格在Acrobat中擷取檔案附件。 您可以將不同的檔案型別附加至表單（例如文字檔案）或二進位檔案(例如JPG檔案)。

>[!NOTE]
>
>將檔案附件附加至表單為選用。

**演算互動式PDF表單**

若要呈現表單，請使用在Designer中建立並儲存為XDP或PDF檔案的表單設計。 您也可以呈現使用Acrobat建立並儲存為PDF檔案的表單。 若要呈現互動式PDF表單，請叫用 `FormsServiceClient` 物件的 `renderPDFForm` 方法或 `renderPDFForm2` 方法。

此 `renderPDFForm` 使用 `URLSpec` 物件。 XDP檔案的內容根目錄會使用傳遞至Forms服務 `URLSpec` 物件的 `setContentRootURI` 方法。 表單設計名稱( `formQuery`)以個別引數值傳遞。 這兩個值會串連起來，以取得表單設計的絕對參照。

此 `renderPDFForm2` 方法接受 `com.adobe.idp.Document` 包含要呈現的XDP或PDF檔案的例項。

>[!NOTE]
>
>如果輸入檔案是PDF檔案，則無法設定標籤的PDF執行階段選項。 如果輸入檔案是XDP檔案，則可以設定標籤的PDF選項。

## 使用Java API演算互動式PDF表單 {#render-an-interactive-pdf-form-using-the-java-api}

使用Forms API (Java)演算互動式PDF表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 指定URI值

   * 建立 `URLSpec` 物件，使用其建構函式儲存URI值。
   * 叫用 `URLSpec` 物件的 `setApplicationWebRoot` 方法，並傳遞代表應用程式網頁根的字串值。
   * 叫用 `URLSpec` 物件的 `setContentRootURI` 方法並傳遞字串值，以指定內容根URI值。 確認表單設計位於內容根URI中。 如果沒有，Forms服務會擲回例外狀況。 若要參照存放庫，請指定 `repository:///`.
   * 叫用 `URLSpec` 物件的 `setTargetURL` 並傳遞字串值，該值會指定將表單資料發佈到的目標URL值。 如果您在表單設計中定義目標URL，您可以傳遞空字串。 您也可以指定傳送表單的URL，以執行計算。

1. 將檔案附加至表單

   * 建立 `java.util.HashMap` 物件以使用其建構函式來儲存檔案附件。
   * 叫用 `java.util.HashMap` 物件的 `put` 每個檔案附加至演算表單的方法。 將下列值傳遞至此方法：

      * 字串值，指定檔案附件的名稱，包括副檔名。
   * A `com.adobe.idp.Document` 包含檔案附件的物件。

   >[!NOTE]
   >
   >對每個要附加至表單的檔案重複此步驟。 此步驟為選用，您可以通過 `null` 如果您不想傳送檔案附件。

1. 演算互動式PDF表單

   叫用 `FormsServiceClient` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。 此為選用引數，您可以指定 `null` 如果您不想指定執行階段選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得的內容型別 `com.adobe.idp.Document` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件的 `read` 方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

## 使用Web服務API演算互動式PDF表單 {#render-an-interactive-pdf-form-using-the-web-service-api}

使用Forms API （Web服務）演算互動式PDF表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 指定URI值

   * 建立 `URLSpec` 物件，使用其建構函式儲存URI值。
   * 叫用 `URLSpec` 物件的 `setApplicationWebRoot` 方法，並傳遞代表應用程式網頁根的字串值。
   * 叫用 `URLSpec` 物件的 `setContentRootURI` 方法並傳遞字串值，以指定內容根URI值。 確認表單設計位於內容根URI中。 如果沒有，Forms服務會擲回例外狀況。 若要參照存放庫，請指定 `repository:///`.
   * 叫用 `URLSpec` 物件的 `setTargetURL` 並傳遞字串值，該值會指定將表單資料發佈到的目標URL值。 如果您在表單設計中定義目標URL，您可以傳遞空字串。 您也可以指定傳送表單的URL，以執行計算。

1. 將檔案附加至表單

   * 建立 `java.util.HashMap` 物件以使用其建構函式來儲存檔案附件。
   * 叫用 `java.util.HashMap` 物件的 `put` 每個檔案附加至演算表單的方法。 將下列值傳遞至此方法：

      * 字串值，指定檔案附件的名稱，包括副檔名
   * A `BLOB` 包含檔案附件的物件

   >[!NOTE]
   >
   >對每個要附加至表單的檔案重複此步驟。

1. 演算互動式PDF表單

   叫用 `FormsService` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞 `null`.
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。 此為選用引數，您可以指定 `null` 如果您不想指定執行階段選項。
   * A `URLSpec` 包含Forms服務所需URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 方法填入的物件。 這可用來儲存轉譯的PDF表單。
   * 空白 `javax.xml.rpc.holders.LongHolder` 方法填入的物件。 （此引數會儲存表單中的頁數。）
   * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。 （此引數將會儲存地區設定值。）
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 將包含此作業結果的物件。

   此 `renderPDFForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 以表單資料流傳遞作為最後一個引數值的物件，必須寫入使用者端Web瀏覽器。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件的 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
   * 取得的內容型別 `BLOB` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立位元組陣列，並透過叫用 `BLOB` 物件的 `getBinaryData` 方法。 此任務指派 `FormsResult` 物件至位元組陣列。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，使用者可看見表單。
