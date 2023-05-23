---
title: 叫用以人為中心的長期流程
seo-title: Invoking Human-Centric Long-Lived Processes
description: 使用使用叫用API的Java網頁型使用者端應用程式、使用Web服務的ASP.NET應用程式，以及使用使用Remoting的Flex建立的使用者端應用程式，以程式設計方式叫用在Workbench中建立以人為中心的長期流程。
seo-description: Programmatically invoke human-centric long-lived processes created in Workbench using a Java web-based client application that uses the Invocation API, an ASP.NET application that uses web services, and a client application built with Flex that uses Remoting.
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
role: Developer
exl-id: c9ebad8b-b631-492d-99a3-094e892b2ddb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 0%

---

# 叫用以人為中心的長期流程 {#invoking-human-centric-long-lived-processes}

您可以使用下列使用者端應用程式，以程式設計方式叫用在Workbench中建立的以人為中心的長期流程：

* 使用「叫用API」的Java Web型使用者端應用程式。 (請參閱 [使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)。)
* 使用網站服務的ASP.NET應用程式。 (請參閱 [使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* 使用Remoting以Flex建置的使用者端應用程式。 (請參閱 [使用AEM Forms叫用(AEM表單已棄用) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

叫用的長效程式已命名 *FirstAppSolution/PreLoanProcess*. 您可以依照中指定的教學課程來建立此程式 [建立您的第一個AEM Forms應用程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).

以人為中心的程式涉及使用者可以使用工作區來回應的任務。 例如，您可以使用Workbench建立流程，讓銀行經理核准或拒絕貸款申請。 下圖顯示了該程式 *FirstAppSolution/PreLoanProcess*.

此 *FirstAppSolution/PreLoanProcess* 處理序接受名為的輸入引數 *formData* 其資料型別為XML。 XML資料會與名為的表單設計合併 *PreLoanForm.xdp*. 下圖顯示一個表單，代表指派給使用者的任務，可核准或拒絕貸款申請。 使用者使用Workspace核准或拒絕應用程式。 Workspace使用者可以按一下下圖所示的「核准」按鈕來核准貸款請求。 同樣地，使用者可以按一下拒絕按鈕來拒絕貸款請求。

系統會以非同步方式叫用長期程式，但因下列因素而無法同步叫用：

* 一個程式可能需花費相當長的時間。
* 一個程式可以跨越組織邊界。
* 程式需要外部輸入才能完成。 例如，考慮將表單傳送給不在辦公室的經理的情況。 在此情況下，除非管理員返回並填寫表單，否則程式不會完成。

叫用長期處理程式時，AEM Forms會在建立記錄時建立叫用識別碼值。 記錄會追蹤長期處理序的狀態，並儲存在AEM Forms資料庫中。 您可以使用叫用識別碼值來追蹤長效處理序的狀態。 此外，您可以使用處理序呼叫識別碼值來執行「處理序管理員」作業，例如終止執行中的處理序執行處理。

>[!NOTE]
>
>叫用短期程式時，AEM Forms不會建立叫用識別碼值或記錄。

此 `FirstAppSolution/PreLoanProcess` 當應徵者提交以XML資料表示的申請時，會叫用處理。 輸入程式變數的名稱為 `formData` 且其資料型別為XML。 就本討論而言，假設使用下列XML資料作為 `FirstAppSolution/PreLoanProcess` 程式。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

傳遞至程式的XML資料必須符合程式中所使用表單中的欄位。 否則，資料不會顯示在表單中。 所有叫用的應用程式 `FirstAppSolution/PreLoanProcess` 處理程式必須傳遞此XML資料來源。 在中建立的應用程式 *叫用以人為中心的長期流程* 動態地從使用者輸入到Web使用者端的值建立XML資料來源。

您可以使用使用者端應用程式來傳送 *FirstAppSolution/PreLoanProcess* 處理必要的XML資料。 長效程式會傳回叫用識別碼值作為其傳回值。 下圖顯示叫用*FirstAppSolution/PreLoanProcess長期處理序的使用者端應用程式。 使用者端應用程式會傳送XML資料，並取得代表引動識別碼值的字串值。

**另请参阅**

[建立可叫用以人為中心的長期流程的Java Web應用程式](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[建立ASP.NET網頁應用程式，叫用以人為中心的長期程式](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[使用Flex建立使用者端應用程式，叫用以人為中心的長期流程](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 建立可叫用以人為中心的長期流程的Java Web應用程式 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

您可以建立使用Java servlet叫用的網頁型應用程式 `FirstAppSolution/PreLoanProcess` 程式。 若要從Java servlet叫用此程式，請使用Java servlet內的Invocation API。 (請參閱 [使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

下圖顯示一個網頁型使用者端應用程式，它會張貼姓名、電話（或電子郵件）和金額值。 當使用者按一下「提交應用程式」按鈕時，這些值會傳送至Java servlet。

Java servlet會執行下列工作：

* 擷取從HTML頁面發佈到Java servlet的值。
* 動態建立XML資料來源以傳遞至 *FirstAppSolution/PreLoanProcess* 程式。 名稱、電話（或電子郵件）和金額值是在XML資料來源中指定的。
* 叫用 *FirstAppSolution/PreLoanProcess* 使用AEM Forms Invocation API進行處理。
* 傳回叫用識別碼值給使用者端Web瀏覽器。

### 步驟摘要 {#summary-of-steps}

若要建立叫用 `FirstAppSolution/PreLoanProcess` 處理，請執行下列步驟：

1. [建立Web專案](invoking-human-centric-long-lived.md#create-a-web-project).
1. [為servlet建立Java應用程式邏輯](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [建立網頁應用程式的網頁](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [將網頁應用程式封裝成WAR檔案](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file).
1. [將WAR檔案部署至裝載AEM Forms的J2EE應用程式伺服器](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms).
1. [測試您的網頁應用程式](invoking-human-centric-long-lived.md#test-your-web-application).

>[!NOTE]
>
>其中部分步驟取決於部署AEM Forms的J2EE應用程式。 例如，部署WAR檔案的方法取決於您使用的J2EE應用程式伺服器。 我們假設已在JBoss®上部署AEM Forms。

### 建立Web專案 {#create-a-web-project}

建立Web應用程式的第一個步驟是建立Web專案。 此檔案所根據的Java IDE是Eclipse 3.3。使用Eclipse IDE建立Web專案，並將必要的JAR檔案新增至專案。 新增名為的HTML頁面 *index.html*  以及專案的Java servlet。

下列清單指定要包含在Web專案中的JAR檔案：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

有關這些JAR檔案的位置，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>J2EE.jar檔案會定義Java servlet使用的資料型別。 您可以從部署AEM Forms的J2EE應用程式伺服器取得此JAR檔案。

**建立Web專案**

1. 啟動Eclipse並按一下 **檔案** >  **新增專案**.
1. 在 **新增專案** 對話方塊，選取 **Web** > **動態Web專案**.
1. 型別 `InvokePreLoanProcess` 取得專案名稱，然後按一下 **完成**.

**將必要的JAR檔案新增至專案**

1. 在「專案總管」視窗中，以滑鼠右鍵按一下 `InvokePreLoanProcess` 專案並選取 **屬性**.
1. 按一下 **Java建置路徑** 然後按一下 **資料庫** 標籤。
1. 按一下 **新增外部JAR** 按鈕並瀏覽到要包含的JAR檔案。

**新增Java servlet至您的專案**

1. 在「專案總管」視窗中，以滑鼠右鍵按一下 `InvokePreLoanProcess` 專案並選取 **新增** >  **其他**.
1. 展開 **Web** 資料夾，選取 **Servlet**，然後按一下 **下一個**.
1. 在「建立Servlet」對話方塊中，輸入 `SubmitXML` 以取得servlet的名稱，然後按一下 **完成**.

**將HTML頁面新增至專案**

1. 在「專案總管」視窗中，以滑鼠右鍵按一下 `InvokePreLoanProcess` 專案並選取 **新增** > **其他**.
1. 展開 **Web** 資料夾，選取 **HTML**，然後按一下 **下一個**.
1. 在「新HTML」對話方塊中，輸入 `index.html` 檔案名稱，然後按一下 **完成**.

>[!NOTE]
>
>如需有關建立叫用SubmitXML Java Servlet的HTML內容的資訊，請參閱 [建立網頁應用程式的網頁](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application).

### 為servlet建立Java應用程式邏輯 {#create-java-application-logic-for-the-servlet}

建立叫用的Java應用程式邏輯 `FirstAppSolution/PreLoanProcess` 從Java servlet中處理。 下列程式碼顯示 `SubmitXML` Java Servlet：

```java
     public class SubmitXML extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the FirstAppSolution/PreLoanProcess process
             }
```

一般而言，您不會將使用者端代碼放在Java servlet的 `doGet` 或 `doPost` 方法。 較好的程式設計實務是將此程式碼放在個別的類別中。 然後從內例項化類別 `doPost` 方法(或 `doGet` 方法)，並呼叫適當的方法。 不過，為求程式碼簡潔，程式碼範例會保持在最低限度，並放在 `doPost` 方法。

叫用 `FirstAppSolution/PreLoanProcess` 使用「叫用API」進行處理，請執行下列工作：

1. 在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。 如需有關這些檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. 擷取從HTML頁面提交的名稱、電話和金額值。 使用這些值可動態建立傳送至 `FirstAppSolution/PreLoanProcess` 程式。 您可以使用 `org.w3c.dom` 類別來建立XML資料來源（此應用程式邏輯如下列程式碼範例所示）。
1. 建立 `ServiceClientFactory` 包含連線屬性的物件。 (請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. 建立 `ServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。 A `ServiceClient` 物件可讓您叫用服務作業。 它會處理如尋找、分派及路由呼叫請求等工作。
1. 建立 `java.util.HashMap` 物件（使用其建構函式）。
1. 叫用 `java.util.HashMap` 物件的 `put` 傳遞至長效處理序的每個輸入引數方法。 請確定您指定處理序輸入引數的名稱。 因為 `FirstAppSolution/PreLoanProcess` 處理序需要型別為的輸入引數 `XML` (已命名 `formData`)，您只需叫用 `put` 方法一次。

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. 建立 `InvocationRequest` 物件(透過叫用 `ServiceClientFactory` 物件的 `createInvocationRequest` 並傳遞下列值：

   * 字串值，指定要叫用的長效處理序名稱。 叫用 `FirstAppSolution/PreLoanProcess` 程式，指定 `FirstAppSolution/PreLoanProcess`.
   * 代表處理作業名稱的字串值。 長效程式操作的名稱是 `invoke`.
   * 此 `java.util.HashMap` 包含服務作業所需引數值的物件。
   * 布林值，指定 `false`，會建立非同步要求（此值適用於叫用長期程式）。

   >[!NOTE]
   >
   >*您可以傳遞值true做為createInvocationRequest方法的第四個引數，以叫用短期程式。 傳遞值true會建立同步要求。*

1. 透過叫用將叫用請求傳送至AEM Forms `ServiceClient` 物件的 `invoke` 方法和傳遞 `InvocationRequest` 物件。 此 `invoke` 方法傳回 `InvocationReponse` 物件。
1. 長效程式會傳回代表叫用識別值的字串值。 透過叫用擷取此值 `InvocationReponse` 物件的 `getInvocationId` 方法。

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 將叫用識別值寫入使用者端Web瀏覽器。 您可以使用 `java.io.PrintWriter` 將此值寫入使用者端Web瀏覽器的執行個體。

### 快速入門：使用叫用API叫用長效程式 {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

以下Java程式碼範例代表叫用 `FirstAppSolution/PreLoanProcess` 程式。

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     *
     * (Because this  quick start is implemented as a Java servlet, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     * */
 import java.io.ByteArrayOutputStream;
 import java.io.File;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import javax.xml.parsers.DocumentBuilder;
 import javax.xml.parsers.DocumentBuilderFactory;
 import javax.xml.transform.Transformer;
 import javax.xml.transform.TransformerFactory;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import org.w3c.dom.Element;
 
     public class SubmitXML extends javax.servlet.http.HttpServlet implements javax.servlet.Servlet {
       static final long serialVersionUID = 1L;
 
        public SubmitXML() {
         super();
     }
 
 
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
         // TODO Auto-generated method stub
         doPost(request,response);
     }
 
     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = myFactory.getServiceClient();
 
             //Get the values that are passed from the Loan HTML page
             String name = (String)request.getParameter("name");
             String phone = (String)request.getParameter("phone");
             String amount = (String)request.getParameter("amount");
 
             //Create XML to pass to the FirstAppSolution/PreLoanProcess process
             org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
 
             //Create a Map object to store the XML input parameter value
             Map params = new HashMap();
             params.put("formData", inXML);
 
             //Create an InvocationRequest object
             InvocationRequest lcRequest =  myFactory.createInvocationRequest(
                 "FirstAppSolution/PreLoanProcess", //Specify the long-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     false);               //Create an asynchronous request
 
             //Send the invocation request to the long-lived process and
             //get back an invocation response object
             InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
             String invocationId = lcResponse.getInvocationId();
 
             //Create a PrintWriter instance
             PrintWriter pp = response.getWriter();
 
             //Write the invocation identifier value back to the client web browser
             pp.println("The job status identifier value is: " +invocationId);
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 
 
      //Create XML data to pass to the long-lived process
      private static org.w3c.dom.Document GetDataSource(String name, String phone, String amount)
      {
             org.w3c.dom.Document document = null;
 
             try
             {
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
 
                 //Create a new Document object
                 document = builder.newDocument();
 
                 //Create MortgageApp - the root element in the XML
                 Element root = (Element)document.createElement("LoanApp");
                 document.appendChild(root);
 
                 //Create an XML element for Name
                 Element nameElement = (Element)document.createElement("Name");
                 nameElement.appendChild(document.createTextNode(name));
                 root.appendChild(nameElement);
 
                 //Create an XML element for Phone
                 Element phoneElement = (Element)document.createElement("PhoneOrEmail");
                 phoneElement.appendChild(document.createTextNode(phone));
                 root.appendChild(phoneElement);
 
                 //Create an XML element for amount
                 Element loanElement = (Element)document.createElement("LoanAmount");
                 loanElement.appendChild(document.createTextNode(amount));
                 root.appendChild(loanElement);
 
                 //Create an XML element for ApprovalStatus
                 Element approveElement = (Element)document.createElement("ApprovalStatus");
                 approveElement.appendChild(document.createTextNode("PENDING APPROVAL"));
                 root.appendChild(approveElement);
 
               }
          catch (Exception e) {
                   System.out.println("The following exception occurred: "+e.getMessage());
                }
         return document;
          }
         }
```

### 建立網頁應用程式的網頁 {#create-the-web-page-for-the-web-application}

此 *index.html* 網頁會提供進入點來叫用 `FirstAppSolution/PreLoanProcess` 程式。 此網頁是基本HTML表單，包含HTML表單和提交按鈕。 當使用者按一下提交按鈕時，表單資料會張貼到 `SubmitXML` Java servlet。

Java servlet會使用下列Java程式碼擷取從HTML頁面張貼的資料：

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

下列HTML程式碼代表在設定開發環境期間建立的index.html檔案。 (請參閱 [建立Web專案](invoking-human-centric-long-lived.md#create-a-web-project).)

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
 <title>Insert title here</title>
 </head>
 <body>
 <table>
     <TBODY>
         <TR>
             <td><img src="financeCorpLogo.jpg" width="172" height="62"></TD>
             <td><FONT size="+2"><strong>Java Loan Application Page</strong></FONT></TD>
             <td> </TD>
             <td> </TD>
         </TR>
 
     </TBODY>
 </TABLE>
     <FORM action="https://hiro-xp:8080/PreLoanProcess/SubmitXML" method="post">
        <table>
          <TBODY>
                <TR>
                      <td><LABEL for="name">Name: </LABEL></TD>
                  <td><INPUT type="text" name="name"></TD>
                  <td><input type="submit" value="Submit Application"></TD>
                  </TR>
            <TR>
                  <td> <LABEL for="phone">Phone/Email: </LABEL></TD>
              <td><INPUT type="text" name="phone"></TD>
                  <td></TD>
              </TR>
 
            <TR>
                  <td><LABEL for="amount">Amount: </LABEL></TD>
              <td><INPUT type="text" name="amount"></TD>
                 <td></TD>
             </TR>
          </TBODY>
 </TABLE>
       </FORM>
 </body>
 </html>
```

### 將網頁應用程式封裝成WAR檔案 {#package-the-web-application-to-a-war-file}

部署叫用 `FirstAppSolution/PreLoanProcess` 程式，將您的Web應用程式封裝成WAR檔案。 確保元件的商業邏輯所依賴的外部JAR檔案（例如adobe-livecycle-client.jar和adobe-usermanager-client.jar）也包含在WAR檔案中。

下圖顯示Eclipse專案的內容，此內容已封裝成WAR檔案。

>[!NOTE]
>
>在上圖中，JPG檔案可以由任何JPG影像檔案取代。

**將Web應用程式封裝成WAR檔案：**

1. 從 **專案總管** 視窗，用滑鼠右鍵按一下 `InvokePreLoanProcess` 專案並選取 **匯出** > **WAR檔案**.
1. 在 **網頁模組** 文字方塊，文字 `InvokePreLoanProcess` Java專案名稱的副標題。
1. 在 **目的地** 文字方塊，文字 `PreLoanProcess.war`**的**&#x200B;檔案名稱，指定WAR檔案的位置，然後按一下完成。

### 將WAR檔案部署至裝載AEM Forms的J2EE應用程式伺服器 {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

將WAR檔案部署到部署AEM Forms的J2EE應用程式伺服器。 若要將WAR檔案部署至J2EE應用程式伺服器，請將WAR檔案從匯出路徑複製到 `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`.

>[!NOTE]
>
>如果未在JBoss上部署AEM Forms，則必須部署WAR檔案，以符合託管AEM Forms的J2EE應用程式伺服器。

### 測試您的網頁應用程式 {#test-your-web-application}

在您部署Web應用程式後，可以使用網頁瀏覽器來測試它。 假設您使用裝載AEM Forms的同一部電腦，您可以指定下列URL：

* http://localhost:8080/PreLoanProcess/index.html

   在HTML表單欄位中輸入值，然後按一下「提交申請」按鈕。 如果發生問題，請參閱J2EE應用程式伺服器的記錄檔。

>[!NOTE]
>
>若要確認Java應用程式已叫用此程式，請啟動Workspace並接受貸款。

## 建立ASP.NET網頁應用程式，叫用以人為中心的長期程式 {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

您可以建立ASP.NET應用程式，叫用 `FirstAppSolution/PreLoanProcess` 程式。 若要從ASP.NET應用程式叫用此程式，請使用Web服務。 (請參閱 [使用Web服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

下圖顯示ASP.NET使用者端應用程式從一般使用者取得資料。 資料會放入XML資料來源並傳送至 `FirstAppSolution/PreLoanProcess` 處理使用者按一下「提交申請」按鈕。

請注意，叫用處理序後，會顯示叫用識別碼值。 叫用識別碼值是建立為記錄的一部分，以追蹤長效處理序的狀態。

ASP.NET應用程式會執行下列工作：

* 擷取使用者在網頁中輸入的值。
* 動態建立傳遞至* FirstAppSolution/PreLoanProcess *程式的XML資料來源。 在XML資料來源中指定這三個值。
* 使用網頁服務叫用* FirstAppSolution/PreLoanProcess *程式。
* 傳回叫用識別碼值和長期作業的狀態給使用者端網頁瀏覽器。

### 步驟摘要 {#summary_of_steps-1}

若要建立能夠叫用FirstAppSolution/PreLoanProcess程式的ASP.NET應用程式，請執行下列步驟：

1. [建立ASP.NET網頁應用程式](invoking-human-centric-long-lived.md#create-an-asp-net-web-application).
1. [建立叫用FirstAppSolution/PreLoanProcess的ASP頁面](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [執行ASP.NET應用程式](invoking-human-centric-long-lived.md#run-the-asp-net-application).

### 建立ASP.NET網頁應用程式 {#create-an-asp-net-web-application}

建立Microsoft .NET C# ASP.NET Web應用程式。 下圖顯示名為的ASP.NET專案內容 *InvokePreLoanProcess*.

請注意，在「服務參考」下，有兩個專案。 第一個專案名為* JobManager*。 此參考可讓ASP.NET應用程式呼叫工作管理員服務。 此服務會傳回長效處理序的狀態相關資訊。 例如，如果處理序目前正在執行，則此服務會傳回一個數值，指定處理序目前正在執行。 第二個參照已命名&#x200B;*PreLoanProcess*. 此服務參考代表對* FirstAppSolution/PreLoanProcess *流程的參考。 建立服務參考後，與AEM Forms服務相關聯的資料型別便可在.NET專案中使用。

**建立ASP.NET專案：**

1. 啟動Microsoft Visual Studio 2008。
1. 從 **檔案** 功能表，選取 **新增**， **網站**.
1. 在 **範本** 清單，選取 **ASP.NET網站**.
1. 在 **位置** 方塊中，選取專案的位置。 為您的專案命名 *InvokePreLoanProcess*.
1. 在 **語言** 方塊中，選取Visual C#
1. 单击确定。

**新增服務參考：**

1. 在「專案」功能表中，選取 **新增服務參考**.
1. 在 **地址** 對話方塊中，指定「工作管理員」服務的WSDL。

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 在名稱空間欄位中，輸入 `JobManager`.
1. 按一下 **前往**&#x200B;然後按一下&#x200B;**確定**.
1. 在 **專案** 功能表，選取 **新增服務參考**.
1. 在 **地址** 對話方塊中，指定FirstAppSolution/PreLoanProcess程式的WSDL。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 在名稱空間欄位中，輸入 `PreLoanProcess`.
1. 按一下 **前往**&#x200B;然後按一下&#x200B;**確定**.

>[!NOTE]
>
>Replace `hiro-xp` IP位址為J2EE應用程式伺服器(主控AEM Forms)。 此 `lc_version` 選項可確保可使用AEM Forms功能，例如MTOM。 不指定 `lc_version`選項，您無法使用MTOM叫用AEM Forms。 (請參閱 [使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

### 建立叫用FirstAppSolution/PreLoanProcess的ASP頁面 {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

在ASP.NET專案中，新增負責向貸款申請人顯示HTML頁面的網頁表單（ASPX檔案）。 網頁表單是以衍生自下列專案的類別為基礎 `System.Web.UI.Page`. 叫用的C#應用程式邏輯 `FirstAppSolution/PreLoanProcess` 位於 `Button1_Click` 方法（此按鈕代表「提交申請」按鈕）。

下圖顯示ASP.NET應用程式

下表列出屬於此ASP.NET應用程式的控制項。

<table>
 <thead>
  <tr>
   <th><p>控制項名稱</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>TextBoxName</p></td>
   <td><p>指定客戶的名字和姓氏。 </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>指定客戶的電話或電子郵件地址。 </p></td>
  </tr>
  <tr>
   <td><p>文字方塊金額</p></td>
   <td><p>指定貸款金額。</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>代表「提交應用程式」按鈕。</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>指定引動識別碼值值的Label控制項。</p></td>
  </tr>
  <tr>
   <td><p>標籤狀態</p></td>
   <td><p>指定工作狀態值的標籤控制項。 此值是透過叫用「工作管理員」服務來擷取。 </p></td>
  </tr>
 </tbody>
</table>

屬於ASP.NET應用程式一部分的應用程式邏輯必須動態建立XML資料來源，以傳遞至 `FirstAppSolution/PreLoanProcess` 程式。 應徵者輸入至HTML頁面的值必須在XML資料來源中指定。 在Workspace中檢視表單時，這些資料值會合併至表單中。 位於 `System.Xml` 名稱空間可用來建立XML資料來源。

當叫用需要來自ASP.NET應用程式的XML資料的程式時，XML資料型別可供您使用。 也就是說，您無法傳遞 `System.Xml.XmlDocument` 執行個體至處理序。 要傳遞給處理序的此XML執行個體的完整名稱是 `InvokePreLoanProcess.PreLoanProcess.XML`. 轉換 `System.Xml.XmlDocument` 執行個體至 `InvokePreLoanProcess.PreLoanProcess.XML`. 您可以使用下列程式碼來執行此工作。

```java
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

若要建立叫用 `FirstAppSolution/PreLoanProcess` 流&#39;b5&#39;7b，在 `Button1_Click` 方法：

1. 建立 `FirstAppSolution_PreLoanProcessClient` 物件（使用其預設建構函式）。
1. 建立 `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` 物件，使用 `System.ServiceModel.EndpointAddress` 建構函式。 將指定WSDL的字串值傳遞至AEM Forms服務與編碼型別：

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   您不需要使用 `lc_version` 屬性。 當您建立服務參考時，會使用此屬性。 不過，請務必指定 `?blob=mtom`.

   >[!NOTE]
   >
   >Replace `hiro-xp`*搭配裝載AEM Forms之J2EE應用程式伺服器的IP位址。*

1. 建立 `System.ServiceModel.BasicHttpBinding` 物件，方法是取得 `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` 資料成員。 將傳回值轉換為 `BasicHttpBinding`.
1. 設定 `System.ServiceModel.BasicHttpBinding` 物件的 `MessageEncoding` 資料成員至 `WSMessageEncoding.Mtom`. 此值可確保使用MTOM。
1. 執行下列工作來啟用基本HTTP驗證：

   * 將AEM表單使用者名稱指派給資料成員 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * 將對應的密碼值指派給資料成員 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * 指派常數值 `HttpClientCredentialType.Basic` 至資料成員 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指派常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 至資料成員 `BasicHttpBindingSecurity.Security.Mode`.

   下列程式碼範例顯示這些工作。

   ```as3
    //Enable BASIC HTTP authentication
    BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
    b.MessageEncoding = WSMessageEncoding.Mtom;
    mortgageClient.ClientCredentials.UserName.UserName = "administrator";
    mortgageClient.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 2000000;
    b.MaxBufferSize = 2000000;
    b.ReaderQuotas.MaxArrayLength = 2000000;
   ```

1. 擷取使用者輸入網頁的名稱、電話和金額值。 使用這些值可動態建立傳送至 `FirstAppSolution/PreLoanProcess` 程式。 建立 `System.Xml.XmlDocument` 代表要傳遞至程式的XML資料來源（此應用程式邏輯如下列程式碼範例所示）。
1. 轉換 `System.Xml.XmlDocument` 執行個體至 `InvokePreLoanProcess.PreLoanProcess.XML` （此應用程式邏輯如下列程式碼範例所示）。
1. 叫用 `FirstAppSolution/PreLoanProcess` 透過叫用 `FirstAppSolution_PreLoanProcessClient` 物件的 `invoke_Async` 方法。 此方法會傳回代表長效處理序之呼叫識別碼值的字串值。
1. 建立 `JobManagerClient` 使用is建構函式。 （請確定您已設定「工作管理員」服務的服務參考。）
1. 重複步驟1-5。 為步驟2指定下列URL： `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. 建立 `JobId` 物件（使用其建構函式）。
1. 設定 `JobId` 物件的 `id` 傳回值的資料成員 `FirstAppSolution_PreLoanProcessClient` 物件的 `invoke_Async` 方法。
1. 指派 `value` true to the `JobId` 物件的 `persistent` 資料成員。
1. 建立 `JobStatus` 物件(透過叫用 `JobManagerService` 物件 `getStatus` 方法和傳遞 `JobId` 物件。
1. 透過擷取的值取得狀態值 `JobStatus` 物件的 `statusCode` 資料成員。
1. 將叫用識別碼值指派給 `LabelJobID.Text` 欄位。
1. 將狀態值指派給 `LabelStatus.Text` 欄位。

### 快速入門：使用Web服務API叫用長效程式 {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

以下C#程式碼範例會叫用 `FirstAppSolution/PreLoanProcess`程式。

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
 
 
 using System;
 using System.Collections;
 using System.Configuration;
 using System.Data;
 using System.Linq;
 using System.Web;
 using System.ServiceModel;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.HtmlControls;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Xml.Linq;
 using System.Xml;
 using System.IO;
 
 //A reference to FirstAppSolution/PreLoanProcess
 using InvokePreLoanProcess.PreLoanProcess;
 
 //A reference to JobManager service
 using InvokePreLoanProcess.JobManager;
 
 
 namespace InvokePreLoanProcess
 {
        public partial class _Default : System.Web.UI.Page
        {
            //This method is called when the Submit Application button is
            //Clicked
            protected void Button1_Click(object sender, EventArgs e)
            {
                //Create a FirstAppSolution_PreLoanProcessClient object
                FirstAppSolution_PreLoanProcessClient mortgageClient = new FirstAppSolution_PreLoanProcessClient();
                mortgageClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
                b.MessageEncoding = WSMessageEncoding.Mtom;
                mortgageClient.ClientCredentials.UserName.UserName = "administrator";
                mortgageClient.ClientCredentials.UserName.Password = "password";
                b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b.MaxReceivedMessageSize = 2000000;
                b.MaxBufferSize = 2000000;
                b.ReaderQuotas.MaxArrayLength = 2000000;
 
                //Retrieve values that user entered into the web page
                String userName = TextBoxName.Text;
                String phone = TextBoxPhone.Text;
                String amount = TextBoxAmount.Text;
 
                //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument myXML = CreateXML(userName, phone, amount);
 
                StringWriter sw = new StringWriter();
                XmlTextWriter xw = new XmlTextWriter(sw);
                myXML.WriteTo(xw);
 
                InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
                inXML.document = sw.ToString();
 
                //INvoke the FirstAppSolution/PreLoanProcess process
                String invocationID =  mortgageClient.invoke_Async(inXML);
 
                //Create a JobManagerClient object to obtain the status of the long-lived operation
                JobManagerClient jobManager = new JobManagerClient();
                jobManager.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/JobManager?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b1 = (BasicHttpBinding)jobManager.Endpoint.Binding;
                b1.MessageEncoding = WSMessageEncoding.Mtom;
                jobManager.ClientCredentials.UserName.UserName = "administrator";
                jobManager.ClientCredentials.UserName.Password = "password";
                b1.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b1.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b1.MaxReceivedMessageSize = 2000000;
                b1.MaxBufferSize = 2000000;
                b1.ReaderQuotas.MaxArrayLength = 2000000;
 
 
                //Create a JobID object that represents the status of the
                //long-lived operation
                JobId jobId = new JobId();
                jobId.id = invocationID;
                jobId.persistent = true;
                JobStatus jobStatus = jobManager.getStatus(jobId);
                System.Int16 val2 = jobStatus.statusCode;
                LabelJobID.Text = "The job status identifier value is " + invocationID;
                LabelStatus.Text = "The status of the long-lived operation is " + getJobDescription(val2);
 
            }
 
            private static XmlDocument CreateXML(String name, String phone, String amount)
            {
                //This method dynamically creates a DDX document
                //to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument xmlDoc = new XmlDocument();
 
                //Create the root element and append it to the XML DOM
                System.Xml.XmlElement root = xmlDoc.CreateElement("LoanApp");
                xmlDoc.AppendChild(root);
 
                //Create the Name element
                XmlElement nameElement = xmlDoc.CreateElement("Name");
                nameElement.AppendChild(xmlDoc.CreateTextNode(name));
                root.AppendChild(nameElement);
 
                //Create the LoanAmount element
                XmlElement LoanAmount = xmlDoc.CreateElement("LoanAmount");
                LoanAmount.AppendChild(xmlDoc.CreateTextNode(amount));
                root.AppendChild(LoanAmount);
 
                //Create the PhoneOrEmail element
                XmlElement PhoneOrEmail = xmlDoc.CreateElement("PhoneOrEmail");
                PhoneOrEmail.AppendChild(xmlDoc.CreateTextNode(phone));
                root.AppendChild(PhoneOrEmail);
 
                //Create the ApprovalStatus element
                XmlElement ApprovalStatus = xmlDoc.CreateElement("ApprovalStatus");
                ApprovalStatus.AppendChild(xmlDoc.CreateTextNode("PENDING APPROVAL"));
                root.AppendChild(ApprovalStatus);
 
                //Return the XmlElement instance
                return xmlDoc;
            }
 
 
            //Returns the String value of the Job Manager status code
            private String getJobDescription(int val)
            {
                switch(val)
                {
                    case 0:
                        return "JOB_STATUS_UNKNOWN";
 
                    case 1:
                        return "JOB_STATUS_QUEUED";
 
                    case 2:
                        return "JOB_STATUS_RUNNING";
 
                    case 3:
                        return "JOB_STATUS_COMPLETED";
 
                    case 4:
                        return "JOB_STATUS_FAILED";
 
                     case 5:
                        return "JOB_STATUS_COMPLETED";
 
                    case 6:
                        return "JOB_STATUS_SUSPENDED";
 
                    case 7:
                        return "JOB_STATUS_COMPLETE_REQUESTED";
 
                    case 8:
                        return "JOB_STATUS_TERMINATE_REQUESTED";
 
                     case 9:
                        return "JOB_STATUS_SUSPEND_REQUESTED";
 
                       case 10:
                        return "JOB_STATUS_RESUME_REQUESTED";
                }
 
                return "";
            }
       }
 }
 
```

>[!NOTE]
>
>位於getJobDescription使用者定義方法中的值對應到Job Manager服務傳回的值。

### 執行ASP.NET應用程式 {#run-the-asp-net-application}

編譯和部署ASP.NET應用程式後，您可以使用網頁瀏覽器執行它。 假設ASP.NET專案名稱為 *InvokePreLoanProcess*，請在網頁瀏覽器中指定下列URL：

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

其中localhost是裝載ASP.NET專案的網頁伺服器名稱，而1629是連線埠號碼。 當您編譯及建置ASP.NET應用程式時，Microsoft Visual Studio會自動部署它。

>[!NOTE]
>
>若要確認ASP.NET應用程式已叫用此程式，請啟動Workspace並接受貸款。

## 使用Flex建立使用者端應用程式，叫用以人為中心的長期流程 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

您可以建立以Flex建置的使用者端應用程式，以叫用 *FirstAppSolution/PreLoanProcess* 程式。 此應用程式使用Remoting來叫用 *FirstAppSolution/PreLoanProcess* 程式。 (請參閱 [使用AEM Forms叫用(AEM表單已棄用) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

下圖顯示使用Flex建立的使用者端應用程式，可從一般使用者收集資料。 資料會放入XML資料來源中，並傳送至程式。

請注意，叫用處理序後，會顯示叫用識別碼值。 叫用識別碼值是建立為記錄的一部分，以追蹤長效處理序的狀態。

使用Flex建立的使用者端應用程式會執行下列工作：

* 擷取使用者在網頁中輸入的值。
* 動態建立傳遞至的XML資料來源 *FirstAppSolution/PreLoanProcess* 程式。 在XML資料來源中指定這三個值。
* 叫用 *FirstAppSolution/PreLoanProcess* 使用Remoting進行處理。
* 傳回長效處理序的叫用識別碼值。

### 步驟摘要 {#summary_of_steps-2}

若要建立以Flex建置且能夠叫用FirstAppSolution/PreLoanProcess流程的使用者端應用程式，請執行下列步驟：

1. 開始新的Flex專案。
1. 在專案的類別路徑中加入adobe-remoting-provider.swc檔案。 (請參閱 [包含AEM Forms Flex程式庫檔案](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file).)
1. 建立 `mx:RemoteObject` 透過ActionScript或MXML執行個體。 (請參閱 [建立mx：RemoteObject執行個體](/help/forms/developing/invoking-aem-forms-using-remoting.md))
1. 設定 `ChannelSet` 執行個體以與AEM Forms通訊，並將其與 `mx:RemoteObject` 執行個體。 (請參閱 [建立AEM Forms的管道](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. 呼叫ChannelSet `login` 服務的方法或 `setCredentials` 指定使用者識別碼值和密碼的方法。 (請參閱 [使用單一登入](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. 建立XML資料來源以傳遞至 `FirstAppSolution/PreLoanProcess` 建立XML執行個體來進行處理。 （此應用程式邏輯如下列程式碼範例所示。）
1. 使用物件的建構函式建立物件型別。 指定處理序輸入引數的名稱，將XML指派給物件，如下列程式碼所示：

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. 叫用 `FirstAppSolution/PreLoanProcess` 透過呼叫 `mx:RemoteObject` 執行個體的 `invoke_Async` 方法。 傳遞 `Object` 包含輸入引數的變數。 (請參閱 [傳遞輸入值](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. 擷取從長期處理程式傳回的叫用識別值，如下列程式碼所示：

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### 使用Remoting叫用長效處理序 {#invoking-a-long-lived-process-using-remoting}

以下Flex程式碼範例會叫用 `FirstAppSolution/PreLoanProcess` 程式。

```java
 <?xml version="1.0" encoding="utf-8"?>
 
 <mx:Application  xmlns="*" backgroundColor="#FFFFFF"
      creationComplete="initializeChannelSet();">
 
 <mx:Script>
          <![CDATA[
 
             import mx.controls.Alert;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import flash.net.navigateToURL;
             import mx.messaging.ChannelSet;
             import mx.messaging.channels.AMFChannel;
             import mx.collections.ArrayCollection;
             import mx.rpc.livecycle.JobId;
             import mx.rpc.livecycle.JobStatus;
             import mx.rpc.livecycle.DocumentReference;
             import mx.formatters.NumberFormatter;
 
             // Holds the job ID returned by LC.JobManager
             private var ji:JobId;
 
             private function initializeChannelSet():void
              {
              var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("remoting-amf", "https://hiro-xp:8080/remoting/messagebroker/amf"));
         LC_MortgageApp.setCredentials("tblue", "password");
         LC_MortgageApp.channelSet = cs;
              }
 
            private function submitApplication():void
             {
             //Get the XML data to pass to the AEM Forms process
             var xml:XML = createXML();
             var params:Object = new Object();
             params["formData"]=xml;
             LC_MortgageApp.invoke_Async(params);
             }
 
             // Handles async call that invokes the long-lived process
             private function resultHandler(event:ResultEvent):void
             {
                ji = event.result as JobId;
                jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
             }
 
             private function createXML():XML
             {
                //Calculate the Mortgage value to place in the XML data
                var propertyPrice:String = txtAmount.text ;
                var name:String = txtName.text ;
                var phone:String = txtPhone.text ;;
 
                var model:XML =
 
                  <LoanApp>
                           <Name>{name}</Name>
                           <LoanAmount>{propertyPrice}</LoanAmount>
                           <PhoneOrEmail>{phone}</PhoneOrEmail>
                           <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
                  </LoanApp>
 
              return model;
             }
 
 
          ]]>
       </mx:Script>
 
       <!-- Declare the RemoteObject and set its destination to the mortgage-app remoting endpoint defined in AEM Forms. -->
       <mx:RemoteObject id="LC_MortgageApp" destination="FirstAppSolution/PreLoanProcess" result="resultHandler(event);">
          <mx:method name="invoke_Async" result="resultHandler(event)"/>
      </mx:RemoteObject>
 
 
     <mx:Grid x="229" y="186">
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Image>
                     <mx:source>file:///D|/LiveCycle_9/FirstApp/financeCorpLogo.jpg</mx:source>
                 </mx:Image>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Flex Loan Application Page" fontSize="20"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Name:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtName"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Button label="Submit Application" click="submitApplication()"/>
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Phone/Email:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtPhone"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Amount:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtAmount"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Label" id="jobStatusDisplay" enabled="true" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
     </mx:Grid>
 
 </mx:Application>
 
```
