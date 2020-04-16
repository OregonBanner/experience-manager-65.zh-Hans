---
title: Forms Service API快速开始
seo-title: Forms Service API快速开始
description: 'null'
seo-description: 'null'
uuid: dfce259a-e392-4929-ad7e-6d902faceaeb
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 9fe48243-24c6-4e08-9886-148cd99dec87
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Forms Service API快速开始 {#forms-service-api-quick-starts}

Forms服务提供以下快速开始:

[快速开始（SOAP模式）:使用Java API渲染交互式PDF表单](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-interactive-pdf-form-using-the-java-api)

[快速开始（SOAP模式）:使用Java API在客户端渲染表单](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[快速开始（SOAP模式）:使用Java API渲染基于片段的表单](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[快速开始（SOAP模式）:使用Java API渲染支持权限的表单](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[快速开始（SOAP模式）:使用Java API渲染HTML表单](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[快速开始（SOAP模式）:使用Java API使用自定义工具栏渲染HTML表单](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[快速开始（SOAP模式）:使用Java API处理作为XML提交的PDF表单](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[快速开始（SOAP模式）:使用Java API处理作为PDF提交的PDF表单](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[快速开始（SOAP模式）:使用Java API处理作为XML提交的HTML表单](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[快速开始（SOAP模式）:使用Java API使用提交的XML数据创建PDF文档](forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)

[快速开始（SOAP模式）:使用Java API使用可流动布局预填充表单](forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[快速开始（SOAP模式）:使用Java API处理包含计算脚本的表单](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-a-form-containing-a-calculation-script-using-the-java-api)

[快速开始（SOAP模式）:使用Java API优化性能](forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[快速开始（SOAP模式）:使用Java API按值呈现](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[快速开始（SOAP模式）:使用Java API将文档传递到Forms服务](forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

使用Forms服务API的应用程序逻辑作为Java Servlet实现。 AEM Forms操作可以使用AEM Forms强类型API执行，连接模式应设置为SOAP。

>[!NOTE]
>
>使用v进行编程中的快速开始基于您正在使用其他操作系统（如Unix）的表单服务器，将特定于窗口的路径替换为适用操作系统支持的路径。 同样，如果您使用的是另一台J2EE应用程序服务器，请确保指定有效的连接属性。 请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**提示**:Adobe开发人员网站包含以下文章，其中讨论了如何创建调用Forms服务并呈现表单的ASP.NET应用程序。 请参 [阅创建表单渲染ASP.NET应用程序](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)。

## 快速开始（SOAP模式）:使用Java API渲染交互式PDF表单 {#quick-start-soap-mode-rendering-an-interactive-pdf-form-using-the-java-api}

以下代码示例将名为 *Loan.xdp的交互式PDF表单渲染到客户端Web浏览器* 。 文件将附加到表单。 请注意，表单设计是应用程序的一部分，它使用内容根URI值引用 `repository:///`。 (请参阅 [渲染交互式PDF表单](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderPDFForm extends HttpServlet implements Servlet {
 
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
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
 
             byte[]    cData = "".getBytes();
             Document oInputData = new Document(cData);
 
             //Set run-time options using a PDFFormRenderSpec instance
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
             pdfFormRenderSpec.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
             //Specify URI values that are required to render a form
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
             //Specify file attachments to attach to the form
             FileInputStream fileAttachment = new FileInputStream("C:\\rideau1.jpg");
             Document attachment1 = new Document(fileAttachment);
             String fileName = "rideau1.jpg";
             Map fileAttachments = new HashMap();
             fileAttachments.put(fileName, attachment1);
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         fileAttachments            //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse objects content type
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
                  e.printStackTrace();
               }
         }
 }
```

## 快速开始（SOAP模式）:使用Java API在客户端渲染表单 {#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api}

以下代码示例使用Forms服务Java API在客 *户端呈现名为Loan.xdp* 的表单。 请注意，表单设计是应用程序的一部分，它使用内容根URI值引用 `repository:///`。 (请参阅 [在客户端渲染表单](/help/forms/developing/rendering-forms.md#rendering-forms-at-the-client)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderPDFFormClient extends HttpServlet implements Servlet {
 
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
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a FormsServiceClient object
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set parameter values required by the renderPDFForm method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set a run-time option required to render a form on the client
         PDFFormRenderSpec pdfRenderSpec = new PDFFormRenderSpec();
         pdfRenderSpec.setRenderAtClient(RenderAtClient.Yes);
 
         //Specify URI values required to render a form
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
         //Invoke the renderPDFForm method to render
         //an interactive PDF form on the client
         FormsResult formOut = formsClient.renderPDFForm(
                 formName,
                 oInputData,
                 pdfRenderSpec,
                 uriValues,
                 null
             );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response and
         //set the HttpServletResponse objects content type
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

## 快速开始（SOAP模式）:使用Java API渲染指南（已弃用） {#quick-start-soap-mode-rendering-a-guide-deprecated-using-the-java-api}

以下代码示例将名为TLALifeClaim.xdp的指南（已弃用）呈现 *到客户端Web浏览器* 。

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import java.io.InputStream;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormGuide extends HttpServlet implements Servlet {
 
 
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
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Specify the parameters for the renderActivityGuide method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/TLALifeClaim.xdp";
         byte[] cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Cache the PDF form
         PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
         pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
         //Set Form Guide run-time options
         ActivityGuideRenderSpec renderSpec = new ActivityGuideRenderSpec();
         renderSpec.setGuidePDF(false);
 
         //Specify URI values that are required to render a form
         //design located in the AEM Forms repository
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
 
         //Invoke the renderFormGuide method
         FormsResult formOut = formsClient.renderFormGuide(
                 formName,            //formQuery
                 oInputData,          //inDataDoc
                 pdfFormRenderSpec,    //pdfFormRenderSpec
                 renderSpec,           //activityGuideRenderSpec
                 uriValues              //urlSpec
                 );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response
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
              System.out.println("The following exception occured: "+e.getMessage());
               }
      }
 }
 
```

## 快速开始（SOAP模式）:使用Java API渲染基于片段的表单 {#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api}

下面的代码示例渲染基于片段的表单。 表单设计的名称为 *PurchaseOrderDynamic.xdp* ，它位于AEM Forms存储库中（XDP文件存储在存储库中名为FormsFolder的文件夹中）。 此外，POFragment表单引用的片段还必须位于存储库中。 (请参 [阅基于片段渲染表单](/help/forms/developing/rendering-forms.md#rendering-forms-based-on-fragments)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragments extends HttpServlet implements Servlet {
 
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
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/PurchaseOrderDynamic.xdp";
 
             FileInputStream myFormData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
             Document oInputData = new Document(myFormData);
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
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

## 快速开始（SOAP模式）:使用Java API渲染支持权限的表单 {#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api}

下面的代码示例向客户端Web浏览器呈现一个启用权限的表单。 此代码示例中设置的使用权限允许用户在表单中添加注释并保存表单数据。 (请参 [阅渲染支持权限的表单](/help/forms/developing/rendering-forms.md#rendering-rights-enabled-forms)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class RenderUsageRightsForms extends HttpServlet implements Servlet {
 
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
 
         //Create a FormsServiceClient object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set parameter values for the renderPDFFormWithUsageRights method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set run-time options
         PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
         pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
         //Set usage-rights run-time options
         ReaderExtensionSpec reOptions = new ReaderExtensionSpec();
         reOptions.setReCredentialAlias("RE2");
         reOptions.setReCommenting(true);
         reOptions.setReFillIn(true);
 
         //Specify URI values required to render the form
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
         //Render a rights-enabled PDF form
         FormsResult formOut = formsClient.renderPDFFormWithUsageRights(
             formName,            //formQuery
             oInputData,          //inDataDoc
             pdfFormRenderSpec,   //renderFormOptionsSpec
             reOptions,              //applicationWebRoot
             uriValues            //targetURL
             );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response and
         //set the HttpServletResponse objects content type
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

## 快速开始（SOAP模式）:使用Java API渲染HTML表单 {#quick-start-soap-mode-rendering-an-html-form-using-the-java-api}

以下代码示例使用Forms服务Java API呈现HTML表单。 工具栏会添加到HTML表单以及两个文件附件。 此外，从对象获得用户代理 `HttpServletRequest` 值。 (请参阅 [将表单渲染为HTML](/help/forms/developing/rendering-forms.md#rendering-forms-as-html)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import java.io.FileInputStream;
 
 
 public class RenderHTMLForms extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             try{
 
                 //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
                 connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");
                 connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
                 connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
                 connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the (Deprecated) renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
 
                 //Obtain the user agent value from the HttpServletRequest object
                 String userAgent = req.getHeader("user-agent");
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
                 htmlRS.setHTMLToolbar(HTMLToolbar.Vertical);
 
                 //Specify the locale value
                 htmlRS.setLocale("en_US");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Set style information that controls the presentation of the HTML form
                 htmlRS.setStyleGenerationLevel(StyleGenerationLevel.InlineAndInternalStyles);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleSubmittedHTMLForm");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the (Deprecated) renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
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

## 快速开始（SOAP模式）:使用Java API渲染使用CSS文件的HTML表单 {#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api}

以下代码示例使用Forms服务客户端API呈现HTML表单。 引用的自定义CSS文件的名称为 *custom.css*。 (请参 [阅使用自定义CSS文件渲染HTML表单](/help/forms/developing/rendering-forms.md#rendering-html-forms-using-custom-css-files)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 import java.io.FileInputStream;
 
 
 public class RenderHTMLCSS extends HttpServlet implements Servlet {
 
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
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the (Deprecated) renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
                 String userAgent = "" ;
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
 
                 //Specify the locale value
                 htmlRS.setLocale("en_US");
 
                 //Specify a custom CSS file to use
                 htmlRS.setCustomCSSURI("C:\\Adobe\custom.css");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the (Deprecated) renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
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

## 快速开始（SOAP模式）:使用Java API使用自定义工具栏渲染HTML表单 {#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api}

以下代码示例呈现一个HTML表单，其中工具栏以法语显示。 fscmenu.xml的位置为C:\Adobe （此文件夹必须位于承载AEM Forms的服务器上）。 注意区域设置值为 `fr_FR`。 讨论如何使用自定义工具栏呈现HTML表单的部分显示了此快速开始中使用的fscmenu.xml文件的语法。 (请参阅 [使用自定义工具栏渲染HTML表单](/help/forms/developing/rendering-forms.md#rendering-html-forms-with-custom-toolbars)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import java.io.FileInputStream;
 
 
 public class RenderCustomToolbar extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             try{
                 //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
                 connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");
                 connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
                 connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
                 connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
                 String userAgent = "" ;
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
                 htmlRS.setHTMLToolbar(HTMLToolbar.Vertical);
 
                 //Specify the URI location of the
                 // fscmenu.xml file that contains French
                 htmlRS.setToolbarURI("C:\\Adobe");
 
                 //Specify the locale value
                 htmlRS.setLocale("fr_FR");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
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

## 快速开始（SOAP模式）:使用Java API处理作为XML提交的PDF表单 {#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api}

以下代码示例处理作为XML提交的表单。 传递给方法的内容类 `processFormSubmission` 型值是 `CONTENT_TYPE=text/xml`。 将显示与名为、和的字 `mortgageAmount`段对 `lastName`应 `firstName` 的值。 此快速开始中使用名 `getNodeText` 为的用户定义方法。 它接受一个 `org.w3c.dom.Document` 实例和一个指定节点名称的字符串值。 此方法返回一个表示节点值的字符串值。 (请参阅 [处理提交的表单](/help/forms/developing/rendering-forms.md#handling-submitted-forms)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 9. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleData extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=text/xml",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
               System.out.println("THE CONTENT TYPS IS" +myContentType);
 
                if (myContentType.equals("application/vnd.adobe.xdp+xml"))    {
 
                 //Get the form data
                 Document formOutput = formOut.getOutputContent();
                 InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
                 org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                 //Call for each field in the form
                 String Amount = getNodeText("mortgageAmount", myDOM);
                 String myLastName =  getNodeText("lastName", myDOM);
                 String myFirstName = getNodeText("firstName", myDOM);
 
                 //Write the form data to the web browser
                 pp.println("<p> The form data is :<br><br>" +
                         "<li> The mortgage amount is "+ Amount+"" +
                         "<li> Last name is "+ myLastName+"" +
                         "<li> First name is "+ myFirstName+"")    ;
 
 
                 }
              }
             }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
     //This method returns the value of the specified node
     private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
     {
       //Get the XML node by name
       NodeList oList = myDOM.getElementsByTagName(nodeName);
       Node myNode = oList.item(0);
       NodeList oChildNodes = myNode.getChildNodes();
 
      String sText = "";
      for (int i = 0; i < oChildNodes.getLength(); i++)
      {
          Node oItem = oChildNodes.item(i);
         if (oItem.getNodeType() == Node.TEXT_NODE)
          {
            sText = sText.concat(oItem.getNodeValue());
          }
      }
     return sText;
     }
 }
 
```

>[!NOTE]
>
>在同一应 `com.adobe.idp.Document` 用程序中使 `org.w3c.dom.Document` 用对象和对象时，完全符合条件 `org.w3c.dom.Document`。

## 快速开始（SOAP模式）:使用Java API处理作为PDF提交的PDF表单 {#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api}

以下代码示例处理作为PDF数据提交的表单。 传递给方法的内容类 `processFormSubmission` 型值是 `CONTENT_TYPE=application/pdf`。 提交的表单将保存为名为tempPDF.pdf *的PDF文件*。 此外，由于表单是以PDF形式提交的，因此可以检索文件附件。 任何文件附件都会保存为JPEG文件。 (请参阅 [处理提交的表单](/help/forms/developing/rendering-forms.md#handling-submitted-forms)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleSubmittedPDFData extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=application/pdf",
             "",
             processSpec);
 
             //Determine if the form contains file attachments
             //It is assumed that file attachments are JPG files
             List fileAttachments = formOut.getAttachments();
 
             //Create an Iterator object and iterate through
             //the List object
             Iterator iter = fileAttachments.iterator();
             int i = 0 ;
             while (iter.hasNext()) {
                 Document file = (Document)iter.next();
                 file.copyToFile(new File("C:\\Adobe\tempFile"+i+".jpg"));
                 i++;
             }
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
 
               if (myContentType.equals("application/pdf")){
 
                     //Get the form data
                     Document myPDFfile = formOut.getOutputContent();
 
                     //Create a PDF object
                     File myPDFFile = new File("C:\\Adobe\tempPDF.pdf");
 
                     //Populate the PDF file
                     myPDFfile.copyToFile(myPDFFile);
                     pp.println("<p> The PDF file is saved as C:\\Adobe\tempPDF.pdf") ;
 
                 }
               }
         }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
 }
 
 
 
```

## 快速开始（SOAP模式）:使用Java API处理作为XML提交的HTML表单 {#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api}

以下代码示例处理作为XML数据提交的HTML表单。 传递给方法的内容类 `processFormSubmission` 型值 `CONTENT_TYPE=application/x-www-form-urlencoded`为。将显示与名为、和的字段 `mortgageAmount`对应 `lastName`的 `firstName` 值。 此快速开始中使用名 `getNodeText` 为的用户定义方法。 它接受一个 `org.w3c.dom.Document` 实例和一个指定节点名称的字符串值。 此方法返回一个表示节点值的字符串值。 (请参阅 [处理提交的表单](/help/forms/developing/rendering-forms.md#handling-submitted-forms)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 /*
     * This quick start handles data submitted as XML from a rendered HTML form
     */
 public class HandleSubmittedHTMLForm extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=application/x-www-form-urlencoded",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
 
                     //Get the form data
                     Document formOutput = formOut.getOutputContent();
                     InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                     //Create DocumentBuilderFactory and DocumentBuilder objects
                     DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                     DocumentBuilder builder = factory.newDocumentBuilder();
                     org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                     //Call for each field in the form
                     String Amount = getNodeText("mortgageAmount", myDOM);
                     String myLastName =  getNodeText("lastName", myDOM);
                     String myFirstName = getNodeText("firstName", myDOM);
 
                     //Write the form data to the web browser
                     pp.println("<p> The form data is :<br><br>" +
                             "<li> The mortgage amount is "+ Amount+"" +
                             "<li> Last name is "+ myLastName+"" +
                             "<li> First name is "+ myFirstName+"")    ;
                      }
                 }
             catch (Exception e) {
                  e.printStackTrace();
               }
         }
 
         //This method returns the value of the specified node
         private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
         {
           //Get the XML node by name
           NodeList oList = myDOM.getElementsByTagName(nodeName);
           Node myNode = oList.item(0);
           NodeList oChildNodes = myNode.getChildNodes();
 
          String sText = "";
          for (int i = 0; i < oChildNodes.getLength(); i++)
          {
              Node oItem = oChildNodes.item(i);
             if (oItem.getNodeType() == Node.TEXT_NODE)
              {
                sText = sText.concat(oItem.getNodeValue());
              }
          }
         return sText;
         }
     }
 
```

## 快速开始（SOAP模式）:使用Java API使用提交的XML数据创建PDF文档 {#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api}

以下Java代码示例处理作为XML提交的表单数据。 表单数据是使用Forms API从表单提交中检索的，并发送到输出服务。 表单数据和表单设计用于创建非交互式PDF文档。 非交互式PDF文档存储在名为的“内容服务”（已弃用）节点中 `/Company Home/Test Directory`。 表单的名称会动态创建。 即，用户的名和姓用于命名PDF文件。 将新内容的资源标识符写出到客户端Web浏览器。 (请参阅 [使用提交的XML数据创建PDF文档](/help/forms/developing/rendering-forms.md#creating-pdf-documents-with-submitted-xml-data)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     * 20. adobe-output-client.jar
     * 21. adobe-contentservices-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 
 import com.adobe.livecycle.contentservices.client.CRCResult;
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl;
 import com.adobe.livecycle.contentservices.client.impl.UpdateVersionType;
 import com.adobe.livecycle.formsservice.client.*;
 import com.adobe.livecycle.output.client.OutputClient;
 import com.adobe.livecycle.output.client.OutputResult;
 import com.adobe.livecycle.output.client.PDFOutputOptionsSpec;
 import com.adobe.livecycle.output.client.TransformationFormat;
 
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleDataSendToOutput extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=text/xml",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
 
               if (myContentType.equals("application/vnd.adobe.xdp+xml"))    {
 
                 //Get the form data
                 Document formOutput = formOut.getOutputContent();
                 InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
                 org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                 //Call for each field in the form
                 String Amount = getNodeText("mortgageAmount", myDOM);
                 String myLastName =  getNodeText("lastName", myDOM);
                 String myFirstName = getNodeText("firstName", myDOM);
 
                 //Write the form data to the web browser
                 pp.println("<p> The form data is :<br><br>" +
                         "<li> The mortgage amount is "+ Amount+"" +
                         "<li> Last name is "+ myLastName+"" +
                         "<li> First name is "+ myFirstName+"")    ;
 
 
                 //Create a non-interactive PDF document by invoking the Output service
                 Document myPDFform = GeneratePDFDocument(myFactory, formOutput);
 
                 //Create the name of the PDF file to store
                 String pdfName = "Loan_"+myLastName+"_"+myFirstName+".pdf" ;
                 String userName = myFirstName+" "+myLastName ;
 
                 //Store the PDF form into Content Services (deprecated)
                 String resourceID = StorePDFDocument(myFactory, myPDFform, pdfName,userName);
                 pp.println("<p> The pdf document was store in :<br><br>" +
                         "<li> /Company home "+
                         "<li> The identifier value of the new resource is "+ resourceID+"");
                   }
             }
         }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
 
     //Store the PDF document in /Company Home/Test Directory using the
     //AEM Forms Content Service API
     private String StorePDFDocument(ServiceClientFactory myFactory, com.adobe.idp.Document pdfDoc, String formName, String userName)
     {
         try
         {
             //Create a DocumentManagementServiceClientImpl object
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);
 
             //Specify the store and node name
             String storeName ="SpacesStore";
             String nodeName = "/Company Home/Test Directory";
 
             //Create a MAP instance to store attributes
             Map<String,Object> inputs = new HashMap<String,Object>();
 
             //Specify attributes that belong to the new content
             String creator = "{https://www.alfresco.org/model/content/1.0}creator";
             String description = "{https://www.alfresco.org/model/content/1.0}description";
 
             inputs.put(creator,userName);
             inputs.put(description,"A mortgage application form");
 
             //Store MortgageForm.pdf in /Company Home/Test Directory
             CRCResult result = docManager.storeContent(storeName,
                      nodeName,
                      formName,
                     "{https://www.alfresco.org/model/content/1.0}content",
                     pdfDoc,
                     "UTF-8",
                     UpdateVersionType.INCREMENT_MAJOR_VERSION,
                     null,
                     inputs);
             //Get the identifier value of the new resource
             String id = result.getNodeUuid();
             return id;
     }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
         return null ;
     }
 
 
     //This method returns the value of the specified node
     private com.adobe.idp.Document GeneratePDFDocument(ServiceClientFactory myFactory, com.adobe.idp.Document formData)
     {
         try
         {
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Set PDF run-time options
         com.adobe.livecycle.output.client.PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setLocale("en_US");
 
         //Set rendering run-time options
         com.adobe.livecycle.output.client.RenderOptionsSpec pdfOptions = new com.adobe.livecycle.output.client.RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
 
         //Create a PDF document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfOptions,
             formData
         );
 
         //Get the Generated PDF file
         Document ouputDoc = outputDocument.getGeneratedDoc();
         return ouputDoc ;
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
         return null;
     }
 
     //This method returns the value of the specified node
     private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
     {
       //Get the XML node by name
       NodeList oList = myDOM.getElementsByTagName(nodeName);
       Node myNode = oList.item(0);
       NodeList oChildNodes = myNode.getChildNodes();
 
      String sText = "";
      for (int i = 0; i < oChildNodes.getLength(); i++)
      {
          Node oItem = oChildNodes.item(i);
         if (oItem.getNodeType() == Node.TEXT_NODE)
          {
            sText = sText.concat(oItem.getNodeValue());
          }
      }
     return sText;
     }
 }
```

## 快速开始（SOAP模式）:使用Java API使用可流动布局预填充表单 {#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api}

下面的代码示例预填充了一个包含动态数据源的表单。 也就是说，数据源是在运行时创建的，不包含在XML文件中或在设计时创建的。 此代码示例包含三种用户定义的方法：

* `createDataSource`:创建一 `org.w3c.dom.Document` 个对象，它表示用于预填充表单的数据源。 此用户定义的方法返回该 `org.w3c.dom.Document` 对象。
* `convertDataSource`:将对象 `org.w3c.dom.Document` 转换为对 `com.adobe.idp.Document` 象。 此方法接受 `org.w3c.dom.Document` 对象作为输入参数并返回对 `com.adobe.idp.Document` 象。
* `renderPOForm`:使用Forms服务Java API渲染动态采购订单表。 由 `com.adobe.idp.Document` 方法返回的对象 `convertDataSource` 用于预填充表单。

   从Java servlet的方法中调用所有这些方 `doPost` 法。 (请参阅 [使用可流式布局预填充表单](/help/forms/developing/rendering-forms.md#prepopulating-forms-with-flowable-layouts)。)

```java
/*
* This Java Quick Start uses the following JAR files
* 1. adobe-forms-client.jar
* 2. adobe-livecycle-client.jar
* 3. adobe-usermanager-client.jar
* 4. activation.jar (required for SOAP mode)
* 5. axis.jar (required for SOAP mode)
* 6. commons-codec-1.3.jar (required for SOAP mode)
* 7. commons-collections-3.2.jar (required for SOAP mode)
* 8. commons-discovery.jar (required for SOAP mode)
* 9. commons-logging.jar (required for SOAP mode)
* 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
* 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
* 12. jaxrpc.jar (required for SOAP mode)
* 13. log4j.jar (required for SOAP mode)
* 14. mail.jar (required for SOAP mode)
* 15. saaj.jar (required for SOAP mode)
* 16. wsdl4j.jar (required for SOAP mode)
* 17. xalan.jar (required for SOAP mode)
* 18. xbean.jar (required for SOAP mode)
* 19. xercesImpl.jar (required for SOAP mode)
*
* (Because Forms quick starts are implemented as Java servlets, it is
* not necessary to include J2EE specific JAR files - the Java project
* that contains this quick start is exported as a WAR file which
* is deployed to the J2EE application server)
*
* These JAR files are located in the following path:
* <install directory>/sdk/client-libs/common
*
* For complete details about the location of these JAR files,
* see "Including AEM Forms library files" in Programming with AEM forms
*/
import java.io.IOException;
import javax.servlet.Servlet;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import com.adobe.livecycle.formsservice.client. * ;
import java.util. * ;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import org.w3c.dom.Element;
import javax.xml.parsers. * ;
import javax.xml.transform. * ;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
public class RenderDynamicForm extends HttpServlet implements Servlet {
 public void doGet(HttpServletRequest req, HttpServletResponse resp)
 throws ServletException,
 IOException {
  doPost(req, resp);
 }
 public void doPost(HttpServletRequest req, HttpServletResponse resp)
 throws ServletException,
 IOException {
  //Render a dynamic purchase order form
  //Create an org.w3c.dom.Document object
  org.w3c.dom.Document myDom = createDataSource();
  //Convert the org.w3c.dom.Document object
  //to a com.adobe.idp.Document object
  com.adobe.idp.Document formData = convertDataSource(myDom);
  //Render the dynamic form using data located within the
  //com.adobe.idp.Document object
  renderPOForm(resp, formData);
 }
 //Creates an org.w3c.dom.Document object
 private org.w3c.dom.Document createDataSource() {
  org.w3c.dom.Document document = null;
  try {
   //Create DocumentBuilderFactory and DocumentBuilder objects
   DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
   DocumentBuilder builder = factory.newDocumentBuilder();
   //Create a new Document object
   document = builder.newDocument();
   //Create the root element and append it to the XML DOM
   Element root = (Element) document.createElement("transaction");
   document.appendChild(root);
   //Create the header element
   Element header = (Element) document.createElement("header");
   root.appendChild(header);
   //Create the txtPONum element and append it to the
   //header element
   Element txtPONum = (Element) document.createElement("txtPONum");
   txtPONum.appendChild(document.createTextNode("8745236985"));
   header.appendChild(txtPONum);
   //Create the dtmDate element and append it to the
   //header element
   Element dtmDate = (Element) document.createElement("dtmDate");
   dtmDate.appendChild(document.createTextNode("2007-02-08"));
   header.appendChild(dtmDate);
   //Create the orderedByAddress element and append
   //it to the header element
   Element orderedByAddress = (Element) document.createElement("orderedByAddress");
   orderedByAddress.appendChild(document.createTextNode("222, Any Blvd"));
   header.appendChild(orderedByAddress);
   //Create the txtOrderedByPhone element and append
   //it to the header element
   Element txtOrderedByPhone = (Element) document.createElement("txtOrderedByPhone");
   txtOrderedByPhone.appendChild(document.createTextNode("(555) 555-2334"));
   header.appendChild(txtOrderedByPhone);
   //Create the txtOrderedByFax element and append
   //it to the header element
   Element txtOrderedByFax = (Element) document.createElement("txtOrderedByFax");
   txtOrderedByFax.appendChild(document.createTextNode("(555) 555-9334"));
   header.appendChild(txtOrderedByFax);
   //Create the txtOrderedByContactName element and append
   //it to the header element
   Element txtOrderedByContactName = (Element) document.createElement("txtOrderedByContactName");
   txtOrderedByContactName.appendChild(document.createTextNode("Frank Jones"));
   header.appendChild(txtOrderedByContactName);
   //Create the deliverToAddress element and append
   //it to the header element
   Element deliverToAddress = (Element) document.createElement("deliverToAddress");
   deliverToAddress.appendChild(document.createTextNode("555, Any Blvd"));
   header.appendChild(deliverToAddress);
   //Create the txtDeliverToPhone element and append
   //it to the header element
   Element txtDeliverToPhone = (Element) document.createElement("txtDeliverToPhone");
   txtDeliverToPhone.appendChild(document.createTextNode("(555) 555-9098"));
   header.appendChild(txtDeliverToPhone);
   //Create the txtDeliverToFax element and append
   //it to the header element
   Element txtDeliverToFax = (Element) document.createElement("txtDeliverToFax");
   txtDeliverToFax.appendChild(document.createTextNode("(555) 555-9000"));
   header.appendChild(txtDeliverToFax);
   //Create the txtDeliverToContactName element and
   //append it to the header element
   Element txtDeliverToContactName = (Element) document.createElement("txtDeliverToContactName");
   txtDeliverToContactName.appendChild(document.createTextNode("Jerry Johnson"));
   header.appendChild(txtDeliverToContactName);
   //Create the detail element and append it to the root
   Element detail = (Element) document.createElement("detail");
   root.appendChild(detail);

   //Create the txtPartNum element and append it to the
   //detail element
   Element txtPartNum = (Element) document.createElement("txtPartNum");
   txtPartNum.appendChild(document.createTextNode("00010-100"));
   detail.appendChild(txtPartNum);
   //Create the txtDescription element and append it
   //to the detail element
   Element txtDescription = (Element) document.createElement("txtDescription");
   txtDescription.appendChild(document.createTextNode("Monitor"));
   detail.appendChild(txtDescription);
   //Create the numQty element and append it to
   //the detail element
   Element numQty = (Element) document.createElement("numQty");
   numQty.appendChild(document.createTextNode("1"));
   detail.appendChild(numQty);
   //Create the numUnitPrice element and append it
   //to the detail element
   Element numUnitPrice = (Element) document.createElement("numUnitPrice");
   numUnitPrice.appendChild(document.createTextNode("350.00"));
   detail.appendChild(numUnitPrice);
   //Create another detail element named detail2 and
   //append it to root
   Element detail2 = (Element) document.createElement("detail");
   root.appendChild(detail2);
   //Create the txtPartNum element and append it to the
   //detail2 element
   Element txtPartNum2 = (Element) document.createElement("txtPartNum");
   txtPartNum2.appendChild(document.createTextNode("00010-200"));
   detail2.appendChild(txtPartNum2);
   //Create the txtDescription element and append it
   //to the detail2 element
   Element txtDescription2 = (Element) document.createElement("txtDescription");
   txtDescription2.appendChild(document.createTextNode("Desk lamps"));
   detail2.appendChild(txtDescription2);
   //Create the numQty element and append it to the
   //detail2 element
   Element numQty2 = (Element) document.createElement("numQty");
   numQty2.appendChild(document.createTextNode("3"));
   detail2.appendChild(numQty2);
   //Create the NUMUNITPRICE element
   Element numUnitPrice2 = (Element) document.createElement("numUnitPrice");
   numUnitPrice2.appendChild(document.createTextNode("55.00"));
   detail2.appendChild(numUnitPrice2);
  }
  catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  return document;

 }
 //Converts an org.w3c.dom.Document object to a
 //com.adobe.idp.Document object
 private Document convertDataSource(org.w3c.dom.Document myDOM) {
  byte[] mybytes = null;
  try {
   //Create a Java Transformer object
   TransformerFactory transFact = TransformerFactory.newInstance();
   Transformer transForm = transFact.newTransformer();
   //Create a Java ByteArrayOutputStream object
   ByteArrayOutputStream myOutStream = new ByteArrayOutputStream();
   //Create a Java Source object
   javax.xml.transform.dom.DOMSource myInput = new DOMSource(myDOM);
   //Create a Java Result object
   javax.xml.transform.stream.StreamResult myOutput = new StreamResult(myOutStream);
   //Populate the Java ByteArrayOutputStream object
   transForm.transform(myInput, myOutput);
   // Get the size of the ByteArrayOutputStream buffer
   int myByteSize = myOutStream.size();
   //Allocate myByteSize to the byte array
   mybytes = new byte[myByteSize];
   //Copy the content to the byte array
   mybytes = myOutStream.toByteArray();
  }
  catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  //Create a com.adobe.idp.Document object and copy the
  //contents of the byte array
  Document myDocument = new Document(mybytes);
  return myDocument;
 }
 //Render the purchase order form using the specified
 //com.adobe.idp.Document object
 private void renderPOForm(HttpServletResponse resp, Document formData) {
  try {
   //Set connection properties required to invoke AEM Forms
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceC
   lientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
   //Create a ServiceClientFactory object
   ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
   //Create a FormsServiceClient object
   FormsServiceClient formsClient = new FormsServiceClient(myFactory);
   //Set the parameter values for the renderPDFForm method
   String formName = "Applications/FormsApplication/1.0/FormsFolder/PO.xdp";
   //Cache the form
   PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
   pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
   //Specify URI values that are required to render a form
   URLSpec uriValues = new URLSpec();
   uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
   uriValues.setContentRootURI("repository:///");
   uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
   //Invoke the renderForm method
   FormsResult formOut = formsClient.renderPDFForm(
   formName, //formQuery
   formData, //inDataDoc
   pdfFormRenderSpec, //PDFFormRenderSpec
   uriValues, //urlSpec
   null //attachments
   );
   //Create a ServletOutputStream object
   ServletOutputStream oOutput = resp.getOutputStream();
   //Create a Document object that stores form data
   Document myData = formOut.getOutputContent();
   //Create an InputStream object
   InputStream inputStream = myData.getInputStream();
   //Write the data stream to the web browser
   byte[] data = new byte[4096];
   int bytesRead = 0;
   while ((bytesRead = inputStream.read(data)) > 0) {
    oOutput.write(data, 0, bytesRead);
   }
  } catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
 }
}
```

## 快速开始（SOAP模式）:使用Java API处理包含计算脚本的表单 {#quick-start-soap-mode-handling-a-form-containing-a-calculation-script-using-the-java-api}

下面的代码示例处理一个包含计算脚本的表单并将结果写回客户端Web浏览器。 (请参阅 [计算表单数据](/help/forms/developing/rendering-forms.md#calculating-form-data)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CalculateData extends HttpServlet implements Servlet {
 
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
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
             RenderOptionsSpec processSpec = new RenderOptionsSpec();
             processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,"CONTENT_TYPE=application/pdf&CONTENT_TYPE=application/vnd.adobe.xdp+xml","",processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is calculated
             if (processState == 1)
             {
 
                 //Write the data back to to the client web browser
                 ServletOutputStream oOutput = resp.getOutputStream();
                 Document calData = formOut.getOutputContent();
 
                 //Create an InputStream object
                 InputStream inputStream = calData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
              }
             }
         catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
         }
     }
 }
```

## 快速开始（SOAP模式）:使用Java API优化性能 {#quick-start-soap-mode-optimizing-performance-using-the-java-api}

下面的代码示例通过设置缓存、独立和线性化选项来优化性能。 线性化文件经过优化，可在Web上投放。 (请参 [阅优化Forms服务的性能](/help/forms/developing/rendering-forms.md#optimizing-the-performance-of-the-forms-service)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormsPerformance extends HttpServlet implements Servlet {
 
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
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a FormsServiceClient object
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set the parameter values for the renderForm method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set performance run-time options
         PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
         renderSpec.setCacheEnabled(new Boolean(true));
         renderSpec.setLinearizedPDF(true);
 
         //Specify URI values that are required to render a form
         //design located in the AEM Forms Repository
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
         //Invoke the renderPDFForm method and write the
         //results to a client web browser
         FormsResult formOut = formsClient.renderPDFForm(
                     formName,       //formQuery
                     oInputData,     //inDataDoc
                     renderSpec,     //PDFFormRenderSpec
                     uriValues,        //urlSpec
                     null            //attachments
                     );
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
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

## 快速开始（SOAP模式）:使用Java API按值呈现 {#quick-start-soap-mode-rendering-by-value-using-the-java-api}

以下Java快速开始渲染交互式PDF表单，该表单基于名为 *Loan.xdp的表单设计(按值* )。 请注意，表单设计用于填充名为 `com.adobe.idp.Document` inputXDP的 *对象*。 (请参阅 [按值呈现表单](/help/forms/developing/rendering-forms.md#rendering-forms-by-value)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderByValue extends HttpServlet implements Servlet {
 
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
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Retrieve the form design
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xdp");
             Document inputXDP = new Document(fileInputStream);
 
             //Specify URI values that are required to render a form
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
             //Invoke the renderPDFForm method and pass the
             //form design by value
             FormsResult formOut = formsClient.renderPDFForm(
                         "",                     //formQuery
                         inputXDP,                 //inDataDoc
                         new PDFFormRenderSpec(), //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object?s content type
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
                  e.printStackTrace();
               }
         }
 }
```

## 快速开始（SOAP模式）:使用Java API将文档传递到Forms服务 {#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api}

以下Java快速开始从Content Services（已弃用）中检索文件Loan.xdp。 此XDP文件位于空间中 `/Company Home/Form Designs`。 XDP文件在实例中返 `com.adobe.idp.Document` 回。 实 `com.adobe.idp.Document` 例将传递给Forms服务。 交互式表单被写入客户端Web浏览器。 (请参 [阅将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)。)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-contentservices-client.jar
     * 3. adobe-livecycle-client.jar
     * 4. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 
 import com.adobe.livecycle.contentservices.client.CRCResult;
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormsFromContentServices extends HttpServlet implements Servlet {
 
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
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Create an empty Document that represents form data
             byte[]    cData = "".getBytes();
             Document oInputData = new Document(cData);
 
             //Get the form design from Content Services (deprecated)
             Document formDesign =  GetFormDesign(myFactory);
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Invoke the renderPDFForm2 and pass to the
             //Document that contains the form design
             FormsResult formOut = formsClient.renderPDFForm2(
                     formDesign,
                     oInputData,
                     pdfFormRenderSpec,
                     null,
                     null
                     );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object?s content type
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
                  e.printStackTrace();
               }
         }
 
     //Retrieve the form design from Content Services (deprecated)
     private Document GetFormDesign(ServiceClientFactory myFactory)
     {
         try{
 
         //Create a DocumentManagementServiceClientImpl object
         DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);
 
         //Specify the name of the store and the content to retrieve
            String storeName = "SpacesStore";
            String nodeName  = "/Company Home/Form Designs/Loan.xdp";
 
            //Retrieve /Company Home/Form Designs/Loan.xdp
            CRCResult content = docManager.retrieveContent(
                      storeName,
                      nodeName,
                      "");
 
            //Return the Document instance
             Document doc =content.getDocument();
             return  doc;
          }
 
         catch(Exception e)
         {
             e.printStackTrace();
         }
         return null;
     }
 
 }
 
```

