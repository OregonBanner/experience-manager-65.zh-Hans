---
title: 建立可呈現Forms的網頁應用程式
seo-title: Creating Web Applications thatRenders Forms
description: 建立使用Java servlet來叫用Forms服務和轉譯表單的網頁型應用程式。 Java servlet可當作傳回表單的Forms服務與使用者端Web瀏覽器之間的連結。
seo-description: Create a web-based application that uses Java servlets to invoke the Forms service and render forms. The Java servlet serves as the link between the Forms service that returns a form and a client web browser.
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
role: Developer
exl-id: 85e00003-8c8b-463a-b728-66af174be295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 0%

---

# 建立轉譯Forms的網頁應用程式 {#creating-web-applications-thatrenders-forms}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 建立轉譯Forms的網頁應用程式 {#creating-web-applications-that-renders-forms}

您可以建立以Web為基礎的應用程式，此應用程式會使用Java servlet來叫用Forms服務及轉譯表單。 使用Java™ servlet的優點在於，您可以將處理程式的傳回值寫入使用者端Web瀏覽器。 也就是說，Java servlet可當作傳回表單的Forms服務與使用者端Web瀏覽器之間的連結。

>[!NOTE]
>
>本節說明如何建立使用叫用Forms服務及根據片段轉譯表單之Java servlet的網頁型應用程式。 (請參閱 [根據片段轉譯Forms](/help/forms/developing/rendering-forms-based-fragments.md).)

您可以使用Java Servlet將表單寫入使用者端網頁瀏覽器，讓客戶可以檢視表單並在表單中輸入資料。 將資料填入表單後，網頁使用者按一下表單上的提交按鈕，將資訊傳回Java servlet，以便擷取和處理資料。 例如，資料可以傳送至另一個程式。

本節說明如何建立網頁式應用程式，讓使用者能夠選取美式表單資料或加拿大表單資料，如下圖所示。

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

呈現的表單是基於片段的表單。 也就是說，如果使用者選取美國資料，則傳回的表單會使用以美國資料為基礎的片段。 例如，表單的頁尾包含美國地址，如下圖所示。

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

同樣地，如果使用者選取加拿大資料，則傳回的表單會包含加拿大地址，如下圖所示。

![cw_cw_fragementformfoternd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>如需有關根據片段建立表單設計的資訊，請參閱 [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

**範例檔案**

本節使用位於以下位置的範例檔案：

&lt;*Forms Designer安裝目錄*>/Samples/Forms/購買訂單/表單片段

其中&lt;*安裝目錄*>是安裝路徑。 就使用者端應用程式而言，Purchase Order Dynamic.xdp檔案是從此安裝位置複製而來，並部署至名為的Forms應用程式 *應用程式/表單應用程式*. Purchase Order Dynamic.xdp檔案放在名為FormsFolder的資料夾中。 同樣地，片段會放置在名為Fragments的資料夾中，如下圖所示。

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

若要存取採購單Dynamic.xdp表單設計，請指定 `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` 作為表單名稱(傳遞給 `renderPDFForm` 方法)和 `repository:///` 作為內容根URI值。

Web應用程式使用的XML資料檔案已從Data資料夾移至 `C:\Adobe`(屬於裝載AEM Forms的J2EE應用程式伺服器的檔案系統)。 檔案名稱為「採購單」 *加拿大.xml* 與採購單 *US.xml*.

>[!NOTE]
>
>如需使用Workbench建立Forms應用程式的詳細資訊，請參閱 [workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63).

### 步驟摘要 {#summary-of-steps}

若要建立根據片段轉譯表單的網頁型應用程式，請執行下列步驟：

1. 建立新的Web專案。
1. 建立代表Java servlet的Java應用程式邏輯。
1. 建立網頁應用程式的網頁。
1. 將Web應用程式封裝成WAR檔案。
1. 將WAR檔案部署至J2EE應用程式伺服器。
1. 測試您的網頁應用程式。

>[!NOTE]
>
>其中部分步驟取決於部署AEM Forms的J2EE應用程式。 例如，部署WAR檔案的方法取決於您使用的J2EE應用程式伺服器。 本節假設AEM Forms已部署在JBoss®上。

### 建立網站專案 {#creating-a-web-project}

建立包含可叫用Forms服務的Java servlet的Web應用程式的第一個步驟是建立新的Web專案。 此檔案所根據的Java IDE是Eclipse 3.3。使用Eclipse IDE建立Web專案，並將必要的JAR檔案新增至專案。 最後，新增名為的HTML頁面 *index.html* 以及專案的Java servlet。

下列清單指定您必須新增至Web專案的JAR檔案：

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

有關這些JAR檔案的位置，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**若要建立Web專案：**

1. 啟動Eclipse並按一下 **檔案** >  **新增專案**.
1. 在 **新增專案** 對話方塊，選取 **Web** > **動態Web專案**.
1. 型別 `FragmentsWebApplication` 取得專案名稱，然後按一下 **完成**.

**若要將必要的JAR檔案新增至專案：**

1. 在「專案總管」視窗中，以滑鼠右鍵按一下 `FragmentsWebApplication` 專案並選取 **屬性**.
1. 按一下 **Java建置路徑** 然後按一下 **資料庫** 標籤。
1. 按一下 **新增外部JAR** 按鈕並瀏覽到要包含的JAR檔案。

**若要將Java servlet新增至專案：**

1. 在「專案總管」視窗中，以滑鼠右鍵按一下 `FragmentsWebApplication` 專案並選取 **新增** >  **其他**.
1. 展開 **Web** 資料夾，選取 **Servlet**，然後按一下 **下一個**.
1. 在「建立Servlet」對話方塊中，輸入 `RenderFormFragment` 以取得servlet的名稱，然後按一下 **完成**.

**若要將HTML頁面新增至專案：**

1. 在「專案總管」視窗中，以滑鼠右鍵按一下 `FragmentsWebApplication` 專案並選取 **新增** > **其他**.
1. 展開 **Web** 資料夾，選取 **HTML**，然後按一下 **下一個**.
1. 在「新HTML」對話方塊中，輸入 `index.html` 檔案名稱，然後按一下 **完成**.

>[!NOTE]
>
>如需有關建立會叫用「 」的「HTML」頁面的資訊， `RenderFormFragment` Java servlet，請參閱 [建立網頁](/help/forms/developing/rendering-forms.md#creating-the-web-page).

### 為servlet建立Java應用程式邏輯 {#creating-java-application-logic-for-the-servlet}

您可以建立Java應用程式邏輯，以便從Java Servlet中叫用Forms服務。 下列程式碼顯示 `RenderFormFragment` Java Servlet：

```java
     public class RenderFormFragment extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the Forms service
             }
```

一般而言，您不會將使用者端代碼放在Java servlet的 `doGet` 或 `doPost` 方法。 較好的程式設計實務是將此程式碼放在另一個類別中，從 `doPost` 方法(或 `doGet` 方法)，並呼叫適當的方法。 不過，為求程式碼簡潔，本節中的程式碼範例會儘量減少，而程式碼範例會放在 `doPost` 方法。

若要使用Forms服務API根據片段呈現表單，請執行以下工作：

1. 在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。 如需有關這些檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. 擷取從HTML表單提交的選項按鈕值，並指定使用美國或加拿大資料。 若已提交American，請建立 `com.adobe.idp.Document` 將資料儲存在 *採購單US.xml*. 同樣地，如果是Canadian，則建立 `com.adobe.idp.Document` 將資料儲存在 *採購單Canada.xml* 檔案。
1. 建立 `ServiceClientFactory` 包含連線屬性的物件。 (請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。
1. 建立 `URLSpec` 物件，使用其建構函式儲存URI值。
1. 叫用 `URLSpec` 物件的 `setApplicationWebRoot` 方法，並傳遞代表應用程式網頁根的字串值。
1. 叫用 `URLSpec` 物件的 `setContentRootURI` 方法並傳遞字串值，以指定內容根URI值。 確保表單設計和片段位於內容根URI中。 如果沒有，Forms服務會擲回例外狀況。 若要參考AEM Forms存放庫，請指定 `repository://`.
1. 叫用 `URLSpec` 物件的 `setTargetURL` 並傳遞字串值，該值會指定將表單資料發佈到的目標URL值。 如果您在表單設計中定義目標URL，您可以傳遞空字串。 您也可以指定傳送表單的URL，以執行計算。
1. 叫用 `FormsServiceClient` 物件的 `renderPDFForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件（在步驟2中建立）。
   * A `PDFFormRenderSpec` 儲存執行階段選項的物件。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` 此物件包含Forms服務根據片段呈現表單所需的URI值。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `renderPDFForm` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

1. 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
1. 取得的內容型別 `com.adobe.idp.Document` 物件(透過叫用其 `getContentType` 方法。
1. 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `com.adobe.idp.Document` 物件。
1. 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
1. 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
1. 建立位元組陣列，叫用 `InputStream` 物件的 `read`方法，並將位元組陣列作為引數傳遞。
1. 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

下列程式碼範例代表Java servlet，它會叫用Forms服務並根據片段轉譯表單。

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import java.net.URL;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragment extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
 
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //Create an Document object to store form data
             Document oInputData = null;
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp";
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/RenderFormFragment");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

### 建立網頁 {#creating-the-web-page}

index.html網頁提供Java servlet的進入點並叫用Forms服務。 此網頁是基本HTML表單，包含兩個選項按鈕和一個提交按鈕。 選項按鈕的名稱是單選按鈕。 當使用者按一下提交按鈕時，表單資料會張貼到 `RenderFormFragment` Java servlet。

Java servlet會使用下列Java程式碼擷取從HTML頁面張貼的資料：

```java
             Document oInputData = null;
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
```

下列HTML程式碼位於開發環境設定期間建立的index.html檔案中。 (請參閱 [建立網站專案](/help/forms/developing/rendering-forms.md#creating-a-web-project).)

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://'[server]:[port]'/FragmentsWebApplication/RenderFormFragment" method="post">
      <table>
      <tr>
        <th>Forms Fragment Web Client</th>
      </tr>
      <tr>
        <td>
          <label>
          <input type="radio" name="radio" id="radio_Data" value="CANADIAN" />
          Canadian data<br />
          </label>
          <p>
            <label>
            <input type="radio" name="radio" id="radio_Data" value="AMERICAN" checked/>
            American data</label>
          </p>
        </td>
      </tr>
      <tr>
      <td>
        <label>
          <input type="submit" name="button_Submit" id="button_Submit" value="Submit" />
            </label>
            </td>
         </tr>
        </table>
      </form>
 </body>
 </html>
```

### 封裝網頁應用程式 {#packaging-the-web-application}

若要部署呼叫Forms服務的Java servlet，請將您的Web應用程式封裝成WAR檔案。 確保元件的商業邏輯所依賴的外部JAR檔案（例如adobe-livecycle-client.jar和adobe-forms-client.jar）也包含在WAR檔案中。

**若要將Web應用程式封裝成WAR檔案，請執行下列動作：**

1. 從 **專案總管** 視窗，用滑鼠右鍵按一下 `FragmentsWebApplication` 專案並選取 **匯出** > **WAR檔案**.
1. 在 **網頁模組** 文字方塊，文字 `FragmentsWebApplication` Java專案名稱的副標題。
1. 在 **目的地** 文字方塊，文字 `FragmentsWebApplication.war`**的**&#x200B;檔案名稱，指定WAR檔案的位置，然後按一下完成。

### 將WAR檔案部署至J2EE應用程式伺服器 {#deploying-the-war-file-to-the-j2ee-application-server}

您可以將WAR檔案部署至部署AEM Forms的J2EE應用程式伺服器。 部署WAR檔案後，您可以使用網頁瀏覽器存取HTML網頁。

**若要將WAR檔案部署至J2EE應用程式伺服器，請執行下列動作：**

* 將WAR檔案從匯出路徑複製到 `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`.

### 測試您的網頁應用程式 {#testing-your-web-application}

在您部署Web應用程式後，可以使用網頁瀏覽器來測試它。 假設您使用裝載AEM Forms的同一部電腦，您可以指定下列URL：

* http://localhost:8080/FragmentsWebApplication/index.html

   選取選擇鈕並按一下「提交」按鈕。 基於片段的表單將顯示在網頁瀏覽器中。 如果發生問題，請參閱J2EE應用程式伺服器的記錄檔。
