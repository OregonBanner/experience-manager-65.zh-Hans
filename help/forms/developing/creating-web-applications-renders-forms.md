---
title: 创建呈现表单的Web 应用程序
seo-title: 创建呈现表单的Web 应用程序
description: 'null'
seo-description: 'null'
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 创建呈现表单的Web 应用程序 {#creating-web-applications-thatrenders-forms}

## 创建呈现表单的Web 应用程序 {#creating-web-applications-that-renders-forms}

您可以创建一个基于Web的应用程序，该应用程序使用Java Servlet调用Forms服务和呈现表单。 使用Java™ servlet的一个优点是可以将进程的返回值写入客户端Web浏览器。 即，Java servlet可用作返回表单的Forms服务与客户端Web浏览器之间的链接。

>[!NOTE]
>
>本节介绍如何创建基于Web的应用程序，该应用程序使用调用Forms服务的Java servlet并基于片段呈现表单。 (请参 [阅基于片段渲染表单](/help/forms/developing/rendering-forms-based-fragments.md)。)

使用Java Servlet，您可以将表单写入客户端Web浏览器，以便客户能够视图并在表单中输入数据。 使用数据填充表单后，Web用户单击表单上的提交按钮，将信息发回Java servlet，在Java Servlet中可以检索和处理数据。 例如，数据可以发送到另一个进程。

本节讨论如何创建基于Web的应用程序，该应用程序使用户能够选择基于美国的表单数据或基于加拿大的表单数据，如下图所示。

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

呈现的表单是基于片段的表单。 也就是说，如果用户选择美国数据，则返回的表单使用基于美国数据的片段。 例如，表单的页脚包含美国地址，如下图所示。

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

同样，如果用户选择加拿大数据，则返回的表单包含加拿大地址，如下图所示。

![cw_cw_fragementformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>有关创建基于片段的表单设计的信息，请参阅 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)。

**示例文件**

此部分使用可位于以下位置的示例文件：

&lt;*Forms Designer install directory*>/Samples/Forms/Purchase Order/Form Fragments

其中&lt;*install directory*>是安装路径。 出于客户端应用程序的目的，从此安装位置复制了Purchase Order Dynamic.xdp文件，并将其部署到名为 *Applications/FormsApplication的Forms应用程序*。 Purchase Order Dynamic.xdp文件位于名为FormsFolder的文件夹中。 同样，片段也放在名为“片段”的文件夹中，如下图所示。

![cw_cw_fragments存储库](assets/cw_cw_fragmentsrepository.png)

要访问Purchase Order Dynamic.xdp表单设计，请指 `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` 定为表单名称（传递给方法的第一个参数）和 `renderPDFForm``repository:///` 内容根URI值。

Web应用程序使用的XML数据文件已从“数据”文件夹移至 `C:\Adobe`（属于承载AEM Forms的J2EE应用程序服务器的文件系统）。 文件名为Purchase Order *Canada.xml* and Purchase Order *US.xml*。

>[!NOTE]
>
>有关使用Workbench创建Forms应用程序的信息，请参阅工作 [台帮助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

### 步骤摘要 {#summary-of-steps}

要创建基于Web的应用程序，以基于片段呈现表单，请执行以下步骤：

1. 创建新Web项目。
1. 创建表示Java servlet的Java应用程序逻辑。
1. 为Web应用程序创建网页。
1. 将Web应用程序打包到WAR文件。
1. 将WAR文件部署到J2EE应用程序服务器。
1. 测试Web应用程序。

>[!NOTE]
>
>其中某些步骤取决于部署了AEM Forms的J2EE应用程序。 例如，用于部署WAR文件的方法取决于您所使用的J2EE应用程序服务器。 本节假定AEM Forms已部署在JBoss®上。

### 创建Web项目 {#creating-a-web-project}

创建包含Java servlet的Web应用程序（可调用Forms服务）的第一步是创建新的Web项目。 此文档所基于的Java IDE是Eclipse 3.3。使用Eclipse IDE，创建一个Web项目并将所需的JAR文件添加到您的项目。 最后，将名为 *index.html* 的HTML页和Java servlet添加到项目中。

以下列表指定了必须添加到Web项目的JAR文件：

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

有关这些JAR文件的位置，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**要创建Web项目，请执行以下操作：**

1. 开始Eclipse，然后单击“ **文件** ”>“ **新建项目”**。
1. 在“新 **建项目** ”对话框中，选择“ **Web** ” **>“**&#x200B;动态Web项目”。
1. 键入 `FragmentsWebApplication` 项目名称，然后单击“完 **成”**。

**要将所需的JAR文件添加到项目，请执行以下操作：**

1. 在“项目浏览器”窗口中，右键单击项目，然 `FragmentsWebApplication` 后选择“属 **性”**。
1. 单击 **Java构建路径** ，然后单击“库 **”选项卡** 。
1. 单击“ **添加外部JAR** ”按钮并浏览至要包含的JAR文件。

**要将Java servlet添加到项目，请执行以下操作：**

1. 在“项目浏览器”窗口中，右键单击项目，然 `FragmentsWebApplication` 后选择“新 **建** >其 **他**”。
1. 展开 **Web文件夹** ，选择 **Servlet**，然后单击“下 **一步**”。
1. 在“创建Servlet”对话框中，键 `RenderFormFragment` 入servlet的名称，然后单击“完 **成”**。

**要将HTML页面添加到项目，请执行以下操作：**

1. 在“项目浏览器”窗口中，右键单击项目，然 `FragmentsWebApplication` 后选择“新 **建** >其 **他**”。
1. 展开 **Web文件夹** ，选择 **HTML**，然后单击“下 **一步**”。
1. 在“新建HTML”对话框中，键入 `index.html` 文件名，然后单击“完 **成”**。

>[!NOTE]
>
>有关创建调用 `RenderFormFragment` Java servlet的HTML页的信息，请参[阅创建网页](/help/forms/developing/rendering-forms.md#creating-the-web-page)。

### 创建Servlet的Java应用程序逻辑 {#creating-java-application-logic-for-the-servlet}

您可以创建从Java servlet内调用Forms服务的Java应用程序逻辑。 以下代码显示了 `RenderFormFragment` Java Servlet的语法：

```as3
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

通常，您不会将客户端代码放在Java servlet或方 `doGet` 法中 `doPost` 。 一个更好的编程实践是将此代码放在一个单独的类中，从该方法（或方法）中实 `doPost` 例化该类，并调 `doGet` 用相应的方法。 但是，对于代码简单性，本节中的代码示例将保持为最小值，并且代码示例将放在方法中 `doPost` 。

要使用Forms服务API渲染基于片段的表单，请执行以下任务:

1. 在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。 有关这些文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 检索从HTML表单提交的单选按钮的值，并指定是使用美国数据还是加拿大数据。 如果提交了American，请创建一 `com.adobe.idp.Document` 个存储Purchase Order US.xml中 *的数据的库*。 同样，如果是加拿大人，则创建 `com.adobe.idp.Document` 一个存储 *Purchase Order Canada.xml文件中的数据* 。
1. 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
1. 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。
1. 使用 `URLSpec` 其构造函数创建存储URI值的对象。
1. 调用对 `URLSpec` 象的方 `setApplicationWebRoot` 法并传递一个表示应用程序Web根目录的字符串值。
1. 调用对 `URLSpec` 象的方 `setContentRootURI` 法并传递一个指定内容根URI值的字符串值。 确保表单设计和片段位于内容根URI中。 否则，Forms服务将引发异常。 要引用AEM Forms存储库，请指定 `repository://`。
1. 调用对 `URLSpec` 象的方 `setTargetURL` 法并传递一个字符串值，该字符串值指定将表单数据发布到的位置。 如果在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL以执行计算。
1. 调用对 `FormsServiceClient` 象的方 `renderPDFForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。
   * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象（在步骤2中创建）。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。 有关详细信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 包 `URLSpec` 含Forms服务需要的URI值的对象，用于基于片段呈现表单。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   该方 `renderPDFForm` 法返回一个对 `FormsResult` 象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
1. 通过调用对象的方 `com.adobe.idp.Document` 法获取对象的内容 `getContentType` 类型。
1. 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `com.adobe.idp.Document` 类型。
1. 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
1. 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
1. 通过调用对象的方法并将字节数组作为参数传递，创建一个用表 `InputStream` 单数据流 `read`填充该字节数组的字节数组。
1. 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

以下代码示例表示调用Forms服务并基于片段呈现表单的Java servlet。

```as3
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

### 创建网页 {#creating-the-web-page}

index.html网页提供Java servlet的入口点并调用Forms服务。 此网页是一个基本的HTML表单，其中包含两个单选按钮和一个提交按钮。 单选按钮的名称是单选按钮。 当用户单击提交按钮时，表单数据将发布到 `RenderFormFragment` Java servlet。

Java servlet通过使用以下Java代码捕获从HTML页发布的数据：

```as3
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

以下HTML代码位于在开发环境设置过程中创建的index.html文件中。 (请参 [阅创建Web项目](/help/forms/developing/rendering-forms.md#creating-a-web-project)。)

```as3
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

### 打包Web应用程序 {#packaging-the-web-application}

要部署调用Forms服务的Java servlet，请将Web应用程序打包到WAR文件。 确保组件业务逻辑所依赖的外部JAR文件（如adobe-livecycle-client.jar和adobe-forms-client.jar）也包含在WAR文件中。

**将Web应用程序打包到WAR文件：**

1. 在“项 **目浏览器** ”窗口中，右键单击项 `FragmentsWebApplication` 目并选择“导 **出** > **WAR文件”**。
1. 在“ **Web模块** ”文本框中，键 `FragmentsWebApplication` 入Java项目的名称。
1. 在“目 **标** ”文本框中，键 `FragmentsWebApplication.war`**入&#x200B;**文件名，指定WAR文件的位置，然后单击“完成”。

### 将WAR文件部署到J2EE应用程序服务器 {#deploying-the-war-file-to-the-j2ee-application-server}

您可以将WAR文件部署到部署了AEM Forms的J2EE应用程序服务器。 部署WAR文件后，您可以使用Web浏览器访问HTML网页。

**将WAR文件部署到J2EE应用程序服务器：**

* 将WAR文件从导出路径复制到 `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`。

### 测试Web应用程序 {#testing-your-web-application}

部署Web应用程序后，可以使用Web浏览器对其进行测试。 假定您使用承载AEM Forms的同一台计算机，则可指定以下URL:

* http://localhost:8080/FragmentsWebApplication/index.html

   选择单选按钮，然后单击“提交”按钮。 基于片段的表单将显示在Web浏览器中。 如果出现问题，请查看J2EE应用程序服务器的日志文件。

