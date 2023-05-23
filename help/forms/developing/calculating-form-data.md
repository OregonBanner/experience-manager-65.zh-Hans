---
title: 計算表單資料
seo-title: Calculating Form Data
description: 使用Forms服務來計算使用者在表單中輸入的值並顯示結果。 Forms服務會使用Java API和Web服務API計算值。
seo-description: Use the Forms service to calculate values that a user enters into a form and display the results. Forms service calculates the values using the Java API and Web Service API.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 1%

---

# 計算表單資料 {#calculating-form-data}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

Forms服務可以計算使用者在表單中輸入的值並顯示結果。 若要計算表單資料，您必須執行兩項工作。 首先，建立表單設計指令碼，以計算表單資料。 表單設計支援三種指令碼型別。 一種指令碼型別在使用者端上執行，另一種在伺服器上執行，第三種型別同時在伺服器和使用者端上執行。 本主題中討論的指令碼型別會在伺服器上執行。 HTML、PDF和表單指南（已棄用）轉換支援伺服器端計算。

在表單設計過程中，您可以使用計算和指令碼來提供更豐富的使用者體驗。 計算與指令碼可新增至大多數表單欄位與物件。 您必須建立表單設計指令碼，才能對使用者輸入互動式表單的資料執行計算操作。

使用者在表單中輸入值，然後按一下「計算」按鈕以檢視結果。 下列程式說明可讓使用者計算資料的範例應用程式：

* 使用者會存取名為StartLoan.html的HTML頁面，做為網頁應用程式的起始頁面。 此頁面會叫用名為的Java Servlet `GetLoanForm`.
* 此 `GetLoanForm` servlet轉譯貸款表單。 此表單包含指令碼、互動式欄位、計算按鈕和提交按鈕。
* 使用者在表單的欄位中輸入值，然後按一下計算按鈕。 表單會傳送至 `CalculateData` 執行指令碼的Java Servlet。 表單會傳回給使用者，其計算結果會顯示在表單中。
* 使用者繼續輸入和計算值，直到顯示令人滿意的結果為止。 滿意後，使用者按一下「提交」按鈕以處理表單。 表單會傳送給另一個名為的Java Servlet `ProcessForm` 負責擷取已提交資料的使用者。 (請參閱 [處理已提交的Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)


下圖顯示應用程式的邏輯流程。

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

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
   <td><p>此 <code>GetLoanForm</code> 系統會從HTML起始頁面叫用Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>此 <code>GetLoanForm</code> Java Servlet使用Forms服務使用者端API將貸款表單轉譯給使用者端網頁瀏覽器。 轉譯包含設定為在伺服器上執行之指令碼的表單與轉譯不包含指令碼的表單的區別在於，您必須指定用於執行指令碼的目標位置。 如果未指定目標位置，則不會執行設定為在伺服器上執行的指令碼。 例如，請考量本節中介紹的應用程式。 此 <code>CalculateData</code> Java Servlet是執行指令碼的目標位置。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>使用者在互動式欄位中輸入資料，然後按一下「計算」按鈕。 表單會傳送至 <code>CalculateData</code> 執行指令碼的Java Servlet。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>表單會呈現回網頁瀏覽器，其計算結果會顯示在表單中。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>當值符合要求時，使用者按一下「提交」按鈕。 表單會傳送給另一個名為的Java Servlet <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

通常，作為PDF內容提交的表單包含使用者端執行的指令碼。 不過，也可以執行伺服器端計算。 「提交」按鈕無法用於計算指令碼。 在此情況下，不會執行計算，因為Forms服務會將互動視為完成。

為了說明表單設計指令碼的使用情況，本節將檢查一個簡單的互動式表單，其中包含設定為在伺服器上執行的指令碼。 下圖顯示一個表單設計，其中包含指令碼，該指令碼會新增使用者在前兩個欄位輸入的值，並在第三個欄位中顯示結果。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**答：** 名為NumericField1的欄位 **B.** 名為NumericField2的欄位 **C.** 名為NumericField3的欄位

此表單設計中指令碼的語法如下：

```javascript
     NumericField3 = NumericField2 + NumericField1
```

在此表單設計中，「計算」按鈕是命令按鈕，而指令碼位於此按鈕的 `Click` 事件。 當使用者在前兩個欄位（NumericField1和NumericField2）中輸入值並按一下「計算」按鈕時，表單會傳送到Forms服務，並在其中執行指令碼。 Forms服務會將表單轉譯回使用者端裝置，且計算結果會顯示在NumericField3欄位中。

>[!NOTE]
>
>如需建立表單設計指令碼的詳細資訊，請參閱 [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

>[!NOTE]
>
>如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步驟摘要 {#summary-of-steps}

若要計算表單資料，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 擷取包含計算指令碼的表單。
1. 將表單資料流寫回使用者端網頁瀏覽器

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立Forms服務使用者端，才能以程式設計方式執行Forms服務使用者端API操作。 如果您使用Java API，請建立 `FormsServiceClient` 物件。 如果您使用Forms Web服務API，請建立 `FormsServiceService` 物件。

**擷取包含計算指令碼的表單**

您可以使用Forms服務使用者端API建立應用程式邏輯，以處理包含設定為在伺服器上執行的指令碼的表單。 此程式與處理提交的表單類似。 (請參閱 [處理已提交的Forms](/help/forms/developing/handling-submitted-forms.md).)

確認與已提交表單關聯的處理狀態為 `1` `(Calculate)`，這表示Forms服務正在表單資料上執行計算操作，且結果必須寫回給使用者。 在此情況下，會自動執行設定為要在伺服器上執行的指令碼。

**將表單資料流寫回使用者端網頁瀏覽器**

確認與已提交表單關聯的處理狀態為後 `1`，您必須將結果寫回使用者端Web瀏覽器。 顯示表單時，計算值將顯示在適當的欄位中。

**另请参阅**

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[使用Java API計算表單資料](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[使用Web服務API計算表單資料](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)
[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API計算表單資料 {#calculate-form-data-using-the-java-api}

使用Forms API (Java)計算表單資料：

1. 包含專案檔案

   在Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取包含計算指令碼的表單

   * 若要擷取包含計算指令碼的表單資料，請建立 `com.adobe.idp.Document` 物件，方法是使用其建構函式並叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getInputStream` 建構函式中的方法。
   * 叫用 `FormsServiceClient` 物件的 `processFormSubmission` 方法並傳遞下列值：

      * 此 `com.adobe.idp.Document` 包含表單資料的物件。
      * 字串值，指定包含所有相關HTTP標頭的環境變數。 您必須指定一或多個值，以指定要處理的內容型別。 `CONTENT_TYPE` 環境變數。 例如，若要處理XML和PDF資料，請為此引數指定下列字串值： `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * 字串值，指定 `HTTP_USER_AGENT` 標頭值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 儲存執行階段選項的物件。

      此 `processFormSubmission` 方法傳回 `FormsResult` 包含表單提交結果的物件。

   * 確認與已提交表單關聯的處理狀態為 `1` 藉由叫用 `FormsResult` 物件的 `getAction` 方法。 如果此方法傳回值 `1`，會執行計算，而資料可回寫至使用者端Web瀏覽器。


1. 將表單資料流寫回使用者端網頁瀏覽器

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流傳送至使用者端web瀏覽器的物件。
   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件的 `read` 方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**


[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API計算表單資料 {#calculate-form-data-using-the-web-service-api}

使用Forms API （Web服務）計算表單資料：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 擷取包含計算指令碼的表單

   * 若要擷取發佈至Java Servlet的表單資料，請建立 `BLOB` 物件（使用其建構函式）。
   * 建立 `java.io.InputStream` 物件，使用 `javax.servlet.http.HttpServletResponse` 物件的 `getInputStream` 方法。
   * 建立 `java.io.ByteArrayOutputStream` 物件，使用它的建構函式傳遞 `java.io.InputStream` 物件。
   * 複製以下專案的內容： `java.io.InputStream` 物件放入 `java.io.ByteArrayOutputStream` 物件。
   * 透過叫用建立位元組陣列 `java.io.ByteArrayOutputStream` 物件的 `toByteArray` 方法。
   * 填入 `BLOB` 物件(透過叫用其 `setBinaryData` 方法，並將位元組陣列作為引數傳遞。
   * 建立 `RenderOptionsSpec` 物件（使用其建構函式）。 透過叫用 `RenderOptionsSpec` 物件的 `setLocale` 方法並傳遞字串值，以指定地區設定值。
   * 叫用 `FormsServiceClient` 物件的 `processFormSubmission` 方法並傳遞下列值：

      * 此 `BLOB` 包含表單資料的物件。
      * 字串值，指定包含所有相關HTTP標頭的環境變數。 例如，您可以指定下列字串值： `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * 字串值，指定 `HTTP_USER_AGENT` 標頭值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 儲存執行階段選項的物件。 有关更多信息, .
      * 空白 `BLOBHolder` 方法填入的物件。
      * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。
      * 空白 `BLOBHolder` 方法填入的物件。
      * 空白 `BLOBHolder` 方法填入的物件。
      * 空白 `javax.xml.rpc.holders.ShortHolder` 方法填入的物件。
      * 空白 `MyArrayOf_xsd_anyTypeHolder` 方法填入的物件。 此引數用於儲存與表單一起提交的檔案附件。
      * 空白 `FormsResultHolder` 使用已提交表單之方法填入的物件。

      此 `processFormSubmission` 方法填入 `FormsResultHolder` 引數以及表單提交的結果。 此 `processFormSubmission` 方法傳回 `FormsResult` 包含表單提交結果的物件。

   * 確認與已提交表單關聯的處理狀態為 `1` 藉由叫用 `FormsResult` 物件的 `getAction` 方法。 如果此方法傳回值 `1`，會執行計算，而資料可回寫至使用者端Web瀏覽器。


1. 將表單資料流寫回使用者端網頁瀏覽器

   * 建立 `javax.servlet.ServletOutputStream` 用於將表單資料流傳送至使用者端web瀏覽器的物件。
   * 建立 `BLOB` 包含表單資料的物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
   * 建立位元組陣列，並透過叫用 `BLOB` 物件的 `getBinaryData` 方法。 此任務指派 `FormsResult` 物件至位元組陣列。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另請參閱**
[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
