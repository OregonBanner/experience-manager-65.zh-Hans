---
title: 调用以人为中心的长寿过程
seo-title: Invoking Human-Centric Long-Lived Processes
description: 以编程方式调用在Workbench中创建的以人为中心的长生命周期进程，该进程使用基于Java的客户端应用程序（该应用程序使用调用API）、使用Web服务的ASP.NET应用程序，以及使用Remoting的Flex构建的客户端应用程序。
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

# 调用以人为中心的长寿过程 {#invoking-human-centric-long-lived-processes}

您可以使用以下客户端应用程序以编程方式调用在Workbench中创建的以人为中心的长生命周期流程：

* 使用调用API的基于Java Web的客户端应用程序。 (请参阅 [使用Java API调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)。)
* 使用Web服务的ASP.NET应用程序。 (请参阅 [使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* 使用Flex构建的使用远程处理的客户端应用程序。 (请参阅 [使用调用AEM Forms(AEM表单已弃用)AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

调用的长期进程名为 *FirstAppSolution/PreLoanProcess*. 您可以按照 [创建您的第一个AEM Forms应用程序](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).

以人为中心的流程涉及一个用户可以使用工作区响应的任务。 例如，使用Workbench，您可以创建一个流程，让银行经理批准或拒绝贷款申请。 下图显示了该过程 *FirstAppSolution/PreLoanProcess*.

的 *FirstAppSolution/PreLoanProcess* 进程接受名为的输入参数 *formData* 数据类型为XML的URL。 XML数据将与名为 *PreLoanForm.xdp*. 下图显示了一个表单，该表单表示分配给用户以批准或拒绝贷款应用程序的任务。 用户使用工作区批准或拒绝应用程序。 工作区用户可以通过单击下图中显示的批准按钮来批准贷款请求。 同样，用户也可以通过单击拒绝按钮来拒绝贷款请求。

由于以下因素，可异步调用长生命周期进程，且无法同步调用：

* 流程可以跨越大量时间。
* 流程可以跨组织边界。
* 进程需要外部输入才能完成。 例如，假设某个表单被发送给不在办公室的经理。 在这种情况下，在管理器返回并填写表单之前，该过程不会完成。

在调用长生命周期进程时，AEM Forms会创建调用标识符值，以作为创建记录的一部分。 该记录跟踪长寿命进程的状态，并存储在AEM Forms数据库中。 使用调用标识符值，可以跟踪长生命周期进程的状态。 此外，您还可以使用进程调用标识符值来执行进程管理器操作，如终止正在运行的进程实例。

>[!NOTE]
>
>AEM Forms在调用短期进程时不会创建调用标识符值或记录。

的 `FirstAppSolution/PreLoanProcess` 申请人提交以XML数据表示的申请时，将调用该流程。 输入进程变量的名称为 `formData` 其数据类型为XML。 就本讨论而言，假定以下XML数据用作 `FirstAppSolution/PreLoanProcess` 进程。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

传递给某个进程的XML数据必须匹配该进程中使用的表单中的字段。 否则，数据不会显示在表单中。 调用 `FirstAppSolution/PreLoanProcess` 进程必须传递此XML数据源。 在中创建的应用程序 *调用以人为中心的长寿过程* 根据用户输入到web客户端的值动态创建XML数据源。

使用客户端应用程序，您可以发送 *FirstAppSolution/PreLoanProcess* 处理所需的XML数据。 长生命周期进程返回调用标识符值作为其返回值。 下图显示了调用*FirstAppSolution/PreLoanProcess的客户端应用程序，该过程使用时间很长。 客户端应用程序发送XML数据并返回表示调用标识符值的字符串值。

**另请参阅**

[创建一个Java Web应用程序，该应用程序会调用以人为中心的长寿过程](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[创建ASP.NET Web应用程序，该应用程序调用以人为中心的长生命周期流程](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[创建使用Flex构建的客户端应用程序，该应用程序会调用以人为中心的长寿过程](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 创建一个Java Web应用程序，该应用程序会调用以人为中心的长寿过程 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

您可以创建基于Web的应用程序，该应用程序使用Java Servlet来调用 `FirstAppSolution/PreLoanProcess` 进程。 要从Java Servlet调用此进程，请使用Java Servlet中的调用API。 (请参阅 [使用Java API调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

下图显示了一个基于Web的客户端应用程序，该应用程序会发布名称、电话（或电子邮件）和金额值。 当用户单击“提交应用程序”按钮时，这些值会发送到Java Servlet。

Java Servlet执行以下任务：

* 检索从HTML页发布到Java Servlet的值。
* 动态创建要传递到的XML数据源 *FirstAppSolution/PreLoanProcess* 进程。 名称、电话（或电子邮件）和金额值在XML数据源中指定。
* 调用 *FirstAppSolution/PreLoanProcess* 进程。
* 将调用标识符值返回给客户端Web浏览器。

### 步骤摘要 {#summary-of-steps}

创建基于Web的Java应用程序，该应用程序将调用 `FirstAppSolution/PreLoanProcess` 处理，请执行以下步骤：

1. [创建Web项目](invoking-human-centric-long-lived.md#create-a-web-project).
1. [为servlet创建Java应用程序逻辑](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [为Web应用程序创建网页](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [将Web应用程序打包到WAR文件](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file).
1. [将WAR文件部署到托管AEM Forms的J2EE应用程序服务器](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms).
1. [测试Web应用程序](invoking-human-centric-long-lived.md#test-your-web-application).

>[!NOTE]
>
>其中某些步骤取决于部署了AEM Forms的J2EE应用程序。 例如，您用于部署WAR文件的方法取决于您所使用的J2EE应用程序服务器。 假定AEM Forms部署在JBoss®上。

### 创建Web项目 {#create-a-web-project}

创建Web应用程序的第一步是创建Web项目。 本文档所基于的Java IDE是Eclipse 3.3。使用Eclipse IDE，创建一个Web项目并将所需的JAR文件添加到您的项目中。 添加名为的HTML页面 *index.html*  和Java Servlet添加到您的项目。

以下列表指定要包含在Web项目中的JAR文件：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

有关这些JAR文件的位置，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>J2EE.jar文件定义Java Servlet使用的数据类型。 您可以从部署了AEM Forms的J2EE应用程序服务器中获取此JAR文件。

**创建Web项目**

1. 启动Eclipse并单击 **文件** >  **新建项目**.
1. 在 **新建项目** 对话框，选择 **Web** > **动态Web项目**.
1. 类型 `InvokePreLoanProcess` ，然后单击 **完成**.

**将所需的JAR文件添加到您的项目中**

1. 在“项目资源管理器”窗口中，右键单击 `InvokePreLoanProcess` 项目，选择 **属性**.
1. 单击 **Java构建路径** ，然后单击 **库** 选项卡。
1. 单击 **添加外部JAR** 按钮并浏览到要包含的JAR文件。

**将Java Servlet添加到您的项目**

1. 在“项目资源管理器”窗口中，右键单击 `InvokePreLoanProcess` 项目，选择 **新建** >  **其他**.
1. 展开 **Web** 文件夹，选择 **Servlet**，然后单击 **下一个**.
1. 在“创建Servlet”对话框中，键入 `SubmitXML` ，然后单击 **完成**.

**将HTML页面添加到您的项目**

1. 在“项目资源管理器”窗口中，右键单击 `InvokePreLoanProcess` 项目，选择 **新建** > **其他**.
1. 展开 **Web** 文件夹，选择 **HTML**，然后单击 **下一个**.
1. 在“新建HTML”对话框中，键入 `index.html` ，然后单击 **完成**.

>[!NOTE]
>
>有关创建调用SubmitXML Java Servlet的HTML内容的信息，请参阅 [为Web应用程序创建网页](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application).

### 为servlet创建Java应用程序逻辑 {#create-java-application-logic-for-the-servlet}

创建调用 `FirstAppSolution/PreLoanProcess` 从Java servlet中处理。 以下代码显示 `SubmitXML` Java Servlet:

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

通常，您不会将客户端代码放在Java Servlet的 `doGet` 或 `doPost` 方法。 一个更好的编程实践是将此代码放在一个单独的类中。 然后，从中实例化类 `doPost` 方法(或 `doGet` 方法)，并调用相应的方法。 但是，对于代码简短性，代码示例会保持在最小值，并且会放置在 `doPost` 方法。

调用 `FirstAppSolution/PreLoanProcess` 使用调用API进行处理，请执行以下任务：

1. 将客户端JAR文件（如adobe-livecycle-client.jar）包含在您Java项目的类路径中。 有关这些文件位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. 从HTML页面检索提交的名称、电话和金额值。 使用这些值动态创建发送到的XML数据源 `FirstAppSolution/PreLoanProcess` 进程。 您可以使用 `org.w3c.dom` 类以创建XML数据源（此应用程序逻辑如以下代码示例中所示）。
1. 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. 创建 `ServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。 A `ServiceClient` 对象允许您调用服务操作。 它处理诸如查找、调度和路由调用请求等任务。
1. 创建 `java.util.HashMap` 对象。
1. 调用 `java.util.HashMap` 对象 `put` 方法，以将每个输入参数传递到长寿命进程。 确保指定进程输入参数的名称。 因为 `FirstAppSolution/PreLoanProcess` 进程需要一个类型的输入参数 `XML` (已命名 `formData`)，您只需调用 `put` 方法一次。

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. 创建 `InvocationRequest` 对象 `ServiceClientFactory` 对象 `createInvocationRequest` 方法和传递以下值：

   * 一个字符串值，用于指定要调用的长生命周期进程的名称。 调用 `FirstAppSolution/PreLoanProcess` 进程，指定 `FirstAppSolution/PreLoanProcess`.
   * 表示流程操作名称的字符串值。 长生命周期流程操作的名称为 `invoke`.
   * 的 `java.util.HashMap` 包含服务操作所需参数值的对象。
   * 一个布尔值，用于指定 `false`，用于创建异步请求（此值适用于调用长生命周期的进程）。

   >[!NOTE]
   >
   >*通过将值true作为createInvocationRequest方法的第四个参数传递，可以调用短时的进程。 传递值true会创建同步请求。*

1. 通过调用 `ServiceClient` 对象 `invoke` 方法和通过 `InvocationRequest` 对象。 的 `invoke` 方法返回 `InvocationReponse` 对象。
1. 长生命周期进程返回表示调用标识值的字符串值。 通过调用 `InvocationReponse` 对象 `getInvocationId` 方法。

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 将调用标识值写入客户端Web浏览器。 您可以使用 `java.io.PrintWriter` 将此值写入客户端web浏览器的实例。

### 快速入门：使用调用API调用长期的进程 {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

以下Java代码示例表示调用 `FirstAppSolution/PreLoanProcess` 进程。

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

### 为Web应用程序创建网页 {#create-the-web-page-for-the-web-application}

的 *index.html* 网页提供一个指向Java servlet的入口点，该Java Servlet调用 `FirstAppSolution/PreLoanProcess` 进程。 此网页是一个基本的HTML表单，其中包含HTML表单和提交按钮。 当用户单击提交按钮时，表单数据会发布到 `SubmitXML` Java Servlet。

Java Servlet使用以下Java代码捕获从HTML页面发布的数据：

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

以下HTML代码表示在开发环境设置期间创建的index.html文件。 (请参阅 [创建Web项目](invoking-human-centric-long-lived.md#create-a-web-project).)

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

### 将Web应用程序打包到WAR文件 {#package-the-web-application-to-a-war-file}

部署调用 `FirstAppSolution/PreLoanProcess` 进程，请将web应用程序打包到WAR文件。 请确保组件业务逻辑所依赖的外部JAR文件（例如adobe-livecycle-client.jar和adobe-usermanager-client.jar）也包含在WAR文件中。

下图显示了Eclipse项目的内容，该内容已打包到WAR文件中。

>[!NOTE]
>
>在上图中，JPG文件可被任何JPG图像文件替换。

**将Web应用程序打包到WAR文件：**

1. 从 **项目资源管理器** 窗口，右键单击 `InvokePreLoanProcess` 项目，选择 **导出** > **战争文件**.
1. 在 **Web模块** 文本框，文字 `InvokePreLoanProcess` ，以获取Java项目的名称。
1. 在 **目标** 文本框，文字 `PreLoanProcess.war`**对于**&#x200B;文件名，指定WAR文件的位置，然后单击“完成”。

### 将WAR文件部署到托管AEM Forms的J2EE应用程序服务器 {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

将WAR文件部署到部署了AEM Forms的J2EE应用程序服务器。 要将WAR文件部署到J2EE应用程序服务器，请将WAR文件从导出路径复制到 `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`.

>[!NOTE]
>
>如果AEM Forms未在JBoss上部署，则必须按照托管AEM Forms的J2EE应用程序服务器来部署WAR文件。

### 测试Web应用程序 {#test-your-web-application}

部署Web应用程序后，可以使用Web浏览器对其进行测试。 假定您使用的是托管AEM Forms的同一台计算机，则可以指定以下URL:

* http://localhost:8080/PreLoanProcess/index.html

   在HTML表单字段中输入值，然后单击“提交申请”按钮。 如果出现问题，请参阅J2EE应用程序服务器的日志文件。

>[!NOTE]
>
>要确认Java应用程序调用了该过程，请启动Workspace并接受贷款。

## 创建ASP.NET Web应用程序，该应用程序调用以人为中心的长生命周期流程 {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

您可以创建调用 `FirstAppSolution/PreLoanProcess` 进程。 要从ASP.NET应用程序调用此过程，请使用Web服务。 (请参阅 [使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

下图显示了ASP.NET客户端应用程序从最终用户处获取数据。 数据将放入XML数据源中，并发送到 `FirstAppSolution/PreLoanProcess` 进程。

注意，调用进程后，将显示调用标识符值。 将创建调用标识符值作为跟踪长期进程状态的记录的一部分。

ASP.NET应用程序执行以下任务：

* 检索用户在网页中输入的值。
* 动态创建一个XML数据源，该数据源被传递到* FirstAppSolution/PreLoanProcess *process。 这三个值在XML数据源中指定。
* 使用Web服务调用* FirstAppSolution/PreLoanProcess *进程。
* 将调用标识符值和长期操作的状态返回给客户端Web浏览器。

### 步骤摘要 {#summary_of_steps-1}

要创建能够调用FirstAppSolution/PreLoanProcess进程的ASP.NET应用程序，请执行以下步骤：

1. [创建ASP.NET Web应用程序](invoking-human-centric-long-lived.md#create-an-asp-net-web-application).
1. [创建调用FirstAppSolution/PreLoanProcess的ASP页面](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [运行ASP.NET应用程序](invoking-human-centric-long-lived.md#run-the-asp-net-application).

### 创建ASP.NET Web应用程序 {#create-an-asp-net-web-application}

创建Microsoft .NET C# ASP.NET Web应用程序。 下图显示了名为的ASP.NET项目的内容 *InvokePreLoanProcess*.

请注意，在“服务参考”下，有两个项目。 第一项名为* JobManager*。 此引用使ASP.NET应用程序能够调用作业管理器服务。 此服务返回有关长期进程状态的信息。 例如，如果进程当前正在运行，则此服务会返回一个数字值，指定当前正在运行的进程。 第二个引用名为&#x200B;*PreLoanProcess*. 此服务引用表示对* FirstAppSolution/PreLoanProcess *进程的引用。 创建服务引用后，与AEM Forms服务关联的数据类型可在.NET项目中使用。

**创建ASP.NET项目：**

1. 启动Microsoft Visual Studio 2008。
1. 从 **文件** 菜单，选择 **新建**, **网站**.
1. 在 **模板** 列表，选择 **ASP.NET网站**.
1. 在 **位置** 框中，选择项目的位置。 命名项目 *InvokePreLoanProcess*.
1. 在 **语言** 框中，选择Visual C#
1. 单击确定。

**添加服务引用：**

1. 在项目菜单中，选择 **添加服务参考**.
1. 在 **地址** 对话框中，为作业管理器服务指定WSDL。

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 在命名空间字段中，键入 `JobManager`.
1. 单击 **开始**&#x200B;然后单击&#x200B;**确定**.
1. 在 **项目** 菜单，选择 **添加服务参考**.
1. 在 **地址** 对话框中，将WSDL指定到FirstAppSolution/PreLoanProcess进程。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 在命名空间字段中，键入 `PreLoanProcess`.
1. 单击 **开始**&#x200B;然后单击&#x200B;**确定**.

>[!NOTE]
>
>替换 `hiro-xp` 具有托管AEM Forms的J2EE应用程序服务器的IP地址。 的 `lc_version` 选项可确保AEM Forms功能（如MTOM）可用。 不指定 `lc_version`选项，则无法使用MTOM调用AEM Forms。 (请参阅 [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

### 创建调用FirstAppSolution/PreLoanProcess的ASP页面 {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

在ASP.NET项目中，添加一个Web窗体（ASPX文件），该窗体负责向贷款申请人显示HTML页面。 Web窗体基于从 `System.Web.UI.Page`. 调用的C#应用程序逻辑 `FirstAppSolution/PreLoanProcess` 位于 `Button1_Click` 方法（此按钮表示“提交应用程序”按钮）。

下图显示了ASP.NET应用程序

下表列出了属于此ASP.NET应用程序的控件。

<table>
 <thead>
  <tr>
   <th><p>控件名称</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>TextBoxName</p></td>
   <td><p>指定客户的名字和姓氏。 </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>指定客户的电话或电子邮件地址。 </p></td>
  </tr>
  <tr>
   <td><p>TextBoxAmount</p></td>
   <td><p>指定贷款金额。</p></td>
  </tr>
  <tr>
   <td><p>按钮1</p></td>
   <td><p>表示“提交应用程序”按钮。</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>一个标签控件，用于指定调用标识符值的值。</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>用于指定作业状态值的标签控件。 通过调用作业管理器服务来检索此值。 </p></td>
  </tr>
 </tbody>
</table>

作为ASP.NET应用程序一部分的应用程序逻辑必须动态创建XML数据源以传递到 `FirstAppSolution/PreLoanProcess` 进程。 申请人在HTML页面中输入的值必须在XML数据源中指定。 在工作区中查看表单时，这些数据值会合并到表单中。 位于 `System.Xml` 命名空间用于创建XML数据源。

调用需要ASP.NET应用程序中的XML数据的进程时，可以使用XML数据类型。 也就是说，您不能通过 `System.Xml.XmlDocument` 实例添加到进程。 要传递到进程的此XML实例的完全限定名称是 `InvokePreLoanProcess.PreLoanProcess.XML`. 转换 `System.Xml.XmlDocument` 实例 `InvokePreLoanProcess.PreLoanProcess.XML`. 您可以使用以下代码执行此任务。

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

创建调用 `FirstAppSolution/PreLoanProcess` 进程，请在 `Button1_Click` 方法：

1. 创建 `FirstAppSolution_PreLoanProcessClient` 对象。
1. 创建 `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务和编码类型：

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请确保指定 `?blob=mtom`.

   >[!NOTE]
   >
   >替换 `hiro-xp`*包含托管AEM Forms的J2EE应用程序服务器的IP地址。*

1. 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` 数据成员。 将返回值转换为 `BasicHttpBinding`.
1. 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 数据成员到 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
1. 通过执行以下任务，启用基本HTTP身份验证：

   * 将AEM表单用户名分配给数据成员 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * 为数据成员分配相应的密码值 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * 指定常量值 `HttpClientCredentialType.Basic` 到数据成员 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到数据成员 `BasicHttpBindingSecurity.Security.Mode`.

   以下代码示例显示了这些任务。

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

1. 检索用户在网页中输入的名称、电话和金额值。 使用这些值动态创建发送到的XML数据源 `FirstAppSolution/PreLoanProcess` 进程。 创建 `System.Xml.XmlDocument` 表示要传递到流程的XML数据源（此应用程序逻辑如下面的代码示例所示）。
1. 转换 `System.Xml.XmlDocument` 实例 `InvokePreLoanProcess.PreLoanProcess.XML` （以下代码示例中显示了此应用程序逻辑）。
1. 调用 `FirstAppSolution/PreLoanProcess` 进程 `FirstAppSolution_PreLoanProcessClient` 对象 `invoke_Async` 方法。 此方法会返回一个字符串值，该值表示长生命周期进程的调用标识符值。
1. 创建 `JobManagerClient` 使用is构造函数。 （确保已设置对作业管理器服务的服务引用。）
1. 重复步骤1-5。 为步骤2指定以下URL: `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. 创建 `JobId` 对象。
1. 设置 `JobId` 对象 `id` 返回值为 `FirstAppSolution_PreLoanProcessClient` 对象 `invoke_Async` 方法。
1. 分配 `value` 对 `JobId` 对象 `persistent` 数据成员。
1. 创建 `JobStatus` 对象 `JobManagerService` 对象s `getStatus` 方法和通过 `JobId` 对象。
1. 通过检索 `JobStatus` 对象 `statusCode` 数据成员。
1. 将调用标识符值分配给 `LabelJobID.Text` 字段。
1. 将状态值分配给 `LabelStatus.Text` 字段。

### 快速入门：使用Web服务API调用长期的进程 {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

以下C#代码示例将调用 `FirstAppSolution/PreLoanProcess`进程。

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
>getJobDescription用户定义的方法中的值与作业管理器服务返回的值相对应。

### 运行ASP.NET应用程序 {#run-the-asp-net-application}

编译和部署ASP.NET应用程序后，可以使用Web浏览器执行它。 假定ASP.NET项目的名称为 *InvokePreLoanProcess*，在Web浏览器中指定以下URL:

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

其中，localhost是托管ASP.NET项目的web服务器的名称，1629是端口号。 在编译和构建ASP.NET应用程序时，Microsoft Visual Studio会自动对其进行部署。

>[!NOTE]
>
>要确认ASP.NET应用程序调用了该过程，请启动Workspace并接受贷款。

## 创建使用Flex构建的客户端应用程序，该应用程序会调用以人为中心的长寿过程 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

您可以创建使用Flex构建的客户端应用程序，以调用 *FirstAppSolution/PreLoanProcess* 进程。 此应用程序使用Remoting调用 *FirstAppSolution/PreLoanProcess* 进程。 (请参阅 [使用调用AEM Forms(AEM表单已弃用)AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

下图显示了一个使用Flex构建的客户端应用程序，该应用程序从最终用户那里收集数据。 数据将放入XML数据源中，并发送到进程。

注意，调用进程后，将显示调用标识符值。 将创建调用标识符值作为跟踪长期进程状态的记录的一部分。

使用Flex构建的客户端应用程序将执行以下任务：

* 检索用户在网页中输入的值。
* 动态创建传递到 *FirstAppSolution/PreLoanProcess* 进程。 这三个值在XML数据源中指定。
* 调用 *FirstAppSolution/PreLoanProcess* 进程。
* 返回长生命周期进程的调用标识符值。

### 步骤摘要 {#summary_of_steps-2}

要创建使用Flex构建的能够调用FirstAppSolution/PreLoanProcess流程的客户端应用程序，请执行以下步骤：

1. 启动新的Flex项目。
1. 将adobe-remoting-provider.swc文件包含到您项目的类路径中。 (请参阅 [包含AEM Forms Flex库文件](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file).)
1. 创建 `mx:RemoteObject` 实例(通过ActionScript或MXML)。 (请参阅 [创建mx:RemoteObject实例](/help/forms/developing/invoking-aem-forms-using-remoting.md))
1. 设置 `ChannelSet` 与AEM Forms通信，并将其与 `mx:RemoteObject` 实例。 (请参阅 [创建到AEM Forms的渠道](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. 调用ChannelSet的 `login` 方法或服务 `setCredentials` 方法来指定用户标识符值和密码。 (请参阅 [使用单点登录](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. 创建要传递到的XML数据源 `FirstAppSolution/PreLoanProcess` 进程。 （以下代码示例中显示了此应用程序逻辑。）
1. 使用其构造函数创建Object类型的对象。 通过指定进程输入参数的名称将XML分配给对象，如以下代码所示：

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. 调用 `FirstAppSolution/PreLoanProcess` 过程 `mx:RemoteObject` 实例 `invoke_Async` 方法。 传递 `Object` ，其中包含输入参数。 (请参阅 [传递输入值](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. 检索从长生命周期进程返回的调用标识值，如以下代码所示：

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### 使用Remoting调用长期的进程 {#invoking-a-long-lived-process-using-remoting}

以下Flex代码示例将调用 `FirstAppSolution/PreLoanProcess` 进程。

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
