---
title: 使用JavaAPI调用AEM Forms
seo-title: 使用JavaAPI调用AEM Forms
description: 使用AEM Forms Java API for RMI传输协议进行远程调用，使用VM传输进行本地调用，使用SOAP进行远程调用，使用不同的身份验证（如用户名和密码）以及同步和异步调用请求。
seo-description: 使用AEM Forms Java API for RMI传输协议进行远程调用，使用VM传输进行本地调用，使用SOAP进行远程调用，使用不同的身份验证（如用户名和密码）以及同步和异步调用请求。
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '5495'
ht-degree: 0%

---


# 使用Java API {#invoking-aem-forms-using-the-javaapi}调用AEM Forms

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

AEM Forms可以通过使用AEM Forms Java API来调用。 使用AEM Forms Java API时，您可以使用调用API或Java客户端库。 Java客户端库可用于服务，如Rights Management服务。 这些强类型API允许您开发调用AEM Forms的Java应用程序。

调用API是位于`com.adobe.idp.dsc`包中的类。 使用这些类，您可以将调用请求直接发送到服务并处理返回的调用响应。 使用调用API调用使用Workbench创建的短期或长期进程。

以编程方式调用服务的建议方法是使用与服务相对应的Java客户端库，而不是调用API。 例如，要调用加密服务，请使用加密服务客户端库。 要执行加密服务操作，请调用属于加密服务客户端对象的方法。 可以通过调用`EncryptionServiceClient`对象的`encryptPDFUsingPassword`方法，使用口令加密PDF文档。

Java API支持以下功能：

* 用于远程调用的RMI传输协议
* 用于本地调用的VM传输
* 用于远程调用的SOAP
* 不同的身份验证，如用户名和密码
* 同步和异步调用请求

**Adobe Developer网站**

Adobe开发人员网站包含以下文章，讨论使用Java API调用AEM Forms服务：

[使用Java Servlet调用AEM Forms进程](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[从Java调用AEM Forms Distiller API](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**另请参阅**

[包括AEM Forms Java库文件](#including-aem-forms-java-library-files)

[调用以人为中心的长寿命进程](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md)

[设置连接属性](#setting-connection-properties)

[使用Java API将数据传递到AEM Forms服务](#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客户端库调用服务](#invoking-a-service-using-a-java-client-library)

[使用调用API调用短时间进程](#invoking-a-short-lived-process-using-the-invocation-api)

[创建一个Java Web应用程序，它调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md)

## 包括AEM Forms Java库文件{#including-aem-forms-java-library-files}

要通过使用Java API以编程方式调用AEM Forms服务，请在Java项目的类路径中包含所需的库文件（JAR文件）。 包含在客户端应用程序的类路径中的JAR文件取决于以下几个因素：

* 要调用的AEM Forms服务。 客户端应用程序可以调用一个或多个服务。
* 要调用AEM Forms服务的模式。 可以使用EJB或SOAP模式。 （请参阅[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)。）

>[!NOTE]
>
>（仅限Turnkey Only）使用命令`standalone.bat -b <Server IP> -c lc_turnkey.xml`开始AEM Forms服务器，为EJB指定服务器IP

* 部署了AEM Forms的J2EE应用程序服务器。

### 特定于服务的JAR文件{#service-specific-jar-files}

下表列表了调用AEM Forms服务所需的JAR文件。

<table>
 <thead>
  <tr>
   <th><p>文件</p></th>
   <th><p>描述</p></th>
   <th><p>位置</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>必须始终包含在Java客户端应用程序的类路径中。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>必须始终包含在Java客户端应用程序的类路径中。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>必须始终包含在Java客户端应用程序的类路径中。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk//client-libs/&lt;app server=""&gt;<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>调用Application Manager服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>调用Assembler服务时必需。 </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>调用备份和还原服务API时需要。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>调用barcoded forms服务时需要。 </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>调用“转换PDF”服务时必需。 </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>调用Distiller服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>调用DocConverter服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>调用文档管理服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>调用加密服务时需要。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>调用Forms服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>调用表单数据集成服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>调用“生成PDF”服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>调用“生成3D PDF”服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>调用作业管理器服务时必需。 </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>调用输出服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>调用PDF实用程序或XMP实用程序服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>调用Acrobat Reader DC扩展服务时必需。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>调用存储库服务时需要。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs\thirdparty<i></i></p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>调用Rights Management服务时必需。</p><p>如果AEM Forms部署在JBoss上，请包含所有这些文件。 </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p><p>JBoss特定的lib目录</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>调用签名服务时需要。</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>调用任务管理器服务时必需。 </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>调用信任存储服务时需要。 </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
 </tbody>
</table>

### 连接模式和J2EE应用程序JAR文件{#connection-mode-and-j2ee-application-jar-files}

下表列表了依赖于连接模式和部署了AEM Forms的J2EE应用程序服务器的JAR文件。

<table>
 <thead>
  <tr>
   <th><p>文件</p> </th>
   <th><p>描述</p> </th>
   <th><p>位置</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>如果使用SOAP模式调用AEM Forms，请包括这些JAR文件。</p> </td>
   <td><p>&lt;&gt;install directory</em>&gt;/sdk/client-libs/thirdparty<em></em></p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>如果AEM Forms部署在JBoss Application Server上，请包含此JAR文件。</p> <p>如果jboss-client.jar和引用的jar不在同一位置，则classloader将找不到所需的类。</p> </td>
   <td><p>JBoss客户端库目录</p> <p>如果在同一J2EE应用程序服务器上部署客户端应用程序，则无需包含此文件。</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>如果AEM Forms部署在BEA WebLogic Server®上，则包含此JAR文件。</p> </td>
   <td><p>特定于WebLogic的lib目录</p> <p>如果在同一J2EE应用程序服务器上部署客户端应用程序，则无需包含此文件。</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>如果AEM Forms部署在WebSphere Application Server上，请包括这些JAR文件。</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar是Web服务调用的必需项)。</p> </li>
    </ul> </td>
   <td><p>特定于WebSphere的lib目录（<em>[WAS_HOME]</em>/运行时）</p> <p>如果在同一J2EE应用程序服务器上部署客户端应用程序，则不必包括这些文件。</p> </td>
  </tr>
 </tbody>
</table>

### 正在调用方案{#invoking-scenarios}

下表指定调用所需的JAR文件以成功调用AEM Forms的方案和列表。

<table>
 <thead>
  <tr>
   <th><p>服务</p> </th>
   <th><p>调用模式</p> </th>
   <th><p>J2EE应用程序服务器</p> </th>
   <th><p>所需的JAR文件</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Forms服务</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms服务</p> <p>Acrobat Reader DC extensions service</p> <p>签名服务</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms服务</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Forms服务</p> <p>Acrobat Reader DC extensions service</p> <p>签名服务</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### 升级JAR文件{#upgrading-jar-files}

如果从LiveCycle升级到AEM Forms，建议将AEM Forms JAR文件包含在Java项目的类路径中。 例如，如果您使用的是Rights Management服务等服务，则在类路径中不包含AEM Forms JAR文件时，将会遇到兼容性问题。

假设您要升级到AEM Forms。 要使用调用Rights Management服务的AEM Forms应用程序，请包括以下JAR文件的Java版本：

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API将数据传递到AEM Forms服务](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客户端库调用服务](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 设置连接属性{#setting-connection-properties}

使用Java API时，可将连接属性设置为调用AEM Forms。 设置连接属性时，指定是远程调用还是本地调用服务，还指定连接模式和身份验证值。 如果启用了服务安全，则需要身份验证值。 但是，如果禁用了服务安全性，则无需指定身份验证值。

连接模式可以是SOAP模式或EJB模式。 EJB模式使用RMI/IIOP协议，而EJB模式的性能优于SOAP模式的性能。 SOAP模式用于消除J2EE应用程序服务器依赖性，或当防火墙位于AEM Forms和客户端应用程序之间时。 SOAP模式使用https协议作为底层传输，并可以跨防火墙边界进行通信。 如果J2EE应用程序服务器依赖关系或防火墙都不是问题，则建议使用EJB模式。

要成功调用AEM Forms服务，请设置以下连接属性：

* **DSC_DEFAULT_EJB_ENDPOINT：如** 果使用EJB连接模式，则此值表示部署了AEM Forms的J2EE应用程序服务器的URL。要远程调用AEM Forms，请指定部署AEM Forms的J2EE应用程序服务器名。 如果您的客户端应用程序位于同一J2EE应用程序服务器上，则可以指定`localhost`。 根据部署的J2EE应用程序服务器AEM Forms，指定以下值之一：

   * JBoss:`https://<ServerName>:8080 (default port)`
   * WebSphere:`iiop://<ServerName>:2809 (default port)`
   * WebLogic:`t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**:如果您使用SOAP连接模式，则此值表示将调用请求发送到的端点。要远程调用AEM Forms，请指定部署AEM Forms的J2EE应用程序服务器名。 如果您的客户端应用程序位于同一J2EE应用程序服务器上，则可以指定`localhost`（例如，`http://localhost:8080`）。

   * 如果J2EE应用程序是JBoss，则端口值`8080`适用。 如果J2EE应用程序服务器是IBM® WebSphere®，请使用端口`9080`。 同样，如果J2EE应用程序服务器是WebLogic，则使用端口`7001`。 (这些值是默认端口值。 如果更改端口值，请使用适用的端口号。)

* **DSC_TRANSPORT_PROTOCOL**:如果使用EJB连接模式，请为 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 此值指定。如果使用SOAP连接模式，请指定`ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`。
* **DSC_SERVER_TYPE**:指定部署AEM Forms的J2EE应用程序服务器。有效值为`JBoss`、`WebSphere`、`WebLogic`。

   * 如果将此连接属性设置为`WebSphere`，则`java.naming.factory.initial`值将设置为`com.ibm.ws.naming.util.WsnInitCtxFactory`。
   * 如果将此连接属性设置为`WebLogic`，则`java.naming.factory.initial`值将设置为`weblogic.jndi.WLInitialContextFactory`。
   * 同样，如果将此连接属性设置为`JBoss`，则`java.naming.factory.initial`值将设置为`org.jnp.interfaces.NamingContextFactory`。
   * 如果您不想使用默认值，可以将`java.naming.factory.initial`属性设置为符合要求的值。

   >[!NOTE]
   >
   >您可以使用`ServiceClientFactoryProperties`类的静态成员，而不是使用字符串设置`DSC_SERVER_TYPE`连接属性。 可以使用以下值：`ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`、`ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`或`ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`。

* **DSC_CREDENTIAL_USERNAME：指** 定AEM表单用户名。要使用户成功调用AEM Forms服务，他们需要服务用户角色。 用户还可以具有包含服务调用权限的其他角色。 否则，当他们尝试调用服务时将引发异常。 如果禁用了服务安全性，则无需指定此连接属性。
* **DSC_CREDENTIAL_PASSWORD：指** 定相应的密码值。如果禁用了服务安全性，则无需指定此连接属性。
* **DSC_REQUEST_TIMEOUT:SOAP** 请求的默认请求超时限制为1200000毫秒（20分钟）。有时，请求可能需要更长的时间才能完成操作。 例如，检索大量记录的SOAP请求可能需要较长的超时限制。 可以使用`ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT`来增加SOAP请求的请求调用超时限制。

   **注意**:只有基于SOAP的调用支持DSC_REQUEST_TIMEOUT属性。

要设置连接属性，请执行以下任务:

1. 使用`java.util.Properties`对象的构造函数创建对象。
1. 要设置`DSC_DEFAULT_EJB_ENDPOINT`连接属性，请调用`java.util.Properties`对象的`setProperty`方法并传递以下值：

   * `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`明细列表值
   * 一个字符串值，它指定承载AEM Forms的J2EE应用程序服务器的URL

   >[!NOTE]
   >
   >如果使用SOAP连接模式，请指定`ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT`明细列表值，而不是`ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`明细列表值。

1. 要设置`DSC_TRANSPORT_PROTOCOL`连接属性，请调用`java.util.Properties`对象的`setProperty`方法并传递以下值：

   * `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`明细列表值
   * `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`明细列表值

   >[!NOTE]
   >
   >如果使用SOAP连接模式，请指定`ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`明细列表值，而不是`ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`明细列表值。

1. 要设置`DSC_SERVER_TYPE`连接属性，请调用`java.util.Properties`对象的`setProperty`方法并传递以下值：

   * `ServiceClientFactoryProperties.DSC_SERVER_TYPE`明细列表值
   * 一个字符串值，它指定承载AEM Forms的J2EE应用程序服务器(例如，如果AEM Forms部署在JBoss上，请指定`JBoss`)。

      1. 要设置`DSC_CREDENTIAL_USERNAME`连接属性，请调用`java.util.Properties`对象的`setProperty`方法并传递以下值：
   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`明细列表值
   * 一个字符串值，它指定调用AEM Forms所需的用户名

      1. 要设置`DSC_CREDENTIAL_PASSWORD`连接属性，请调用`java.util.Properties`对象的`setProperty`方法并传递以下值：
   * `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`明细列表值
   * 一个字符串值，它指定相应的密码值



**设置JBoss的EJB连接模式**

以下Java代码示例设置连接属性以调用在JBoss上部署的AEM Forms并使用EJB连接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**设置WebLogic的EJB连接模式**

以下Java代码示例设置连接属性以调用在WebLogic上部署的AEM Forms并使用EJB连接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**设置WebSphere的EJB连接模式**

以下Java代码示例设置连接属性以调用在WebSphere上部署的AEM Forms并使用EJB连接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**设置SOAP连接模式**

以下Java代码示例在SOAP模式下设置连接属性以调用在JBoss上部署的AEM Forms。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>如果选择SOAP连接模式，请确保在客户端应用程序的类路径中包含其他JAR文件。

**禁用服务安全时设置连接属性**

以下Java代码示例设置调用在JBoss Application Server上部署的AEM Forms和禁用服务安全时所需的连接属性。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>所有与AEM Forms编程关联的Java快速开始都显示EJB和SOAP连接设置。

**使用自定义请求超时限制设置SOAP连接模式**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**使用Context对象调用AEM Forms**

可以使用`com.adobe.idp.Context`对象与已验证的用户调用AEM Forms服务（`com.adobe.idp.Context`对象表示已验证的用户）。 使用`com.adobe.idp.Context`对象时，无需设置`DSC_CREDENTIAL_USERNAME`或`DSC_CREDENTIAL_PASSWORD`属性。 使用`AuthenticationManagerServiceClient`对象的`authenticate`方法验证用户时，可以获得`com.adobe.idp.Context`对象。

`authenticate`方法返回包含身份验证结果的`AuthResult`对象。 可以通过调用`com.adobe.idp.Context`对象的构造函数创建对象。 然后调用`com.adobe.idp.Context`对象的`initPrincipal`方法并传递`AuthResult`对象，如以下代码所示：

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

您可以调用`ServiceClientFactory`对象的`setContext`方法并传递`com.adobe.idp.Context`对象，而不是设置`DSC_CREDENTIAL_USERNAME`或`DSC_CREDENTIAL_PASSWORD`属性。 使用AEM表单用户调用服务时，请确保他们具有调用AEM Forms服务所需的`Services User`角色。

下面的代码示例说明如何在用于创建`EncryptionServiceClient`对象的连接设置中使用`com.adobe.idp.Context`对象。

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>有关对用户进行身份验证的完整详细信息，请参阅[对用户进行身份验证](/help/forms/developing/users.md#authenticating-users)。

### 正在调用方案{#invoking_scenarios-1}

本节将讨论以下调用情形：

* 在其自身的Java虚拟机(JVM)中运行的客户端应用程序调用独立的AEM Forms实例。
* 在其自身JVM中运行的客户端应用程序调用群集AEM Forms实例。

### 调用独立AEM Forms实例{#client-application-invoking-a-stand-alone-aem-forms-instance}的客户端应用程序

下图显示了在其自身JVM中运行并调用独立AEM Forms实例的客户端应用程序。

在这种情况下，客户端应用程序在其自己的JVM中运行并调用AEM Forms服务。

>[!NOTE]
>
>此方案是所有快速开始都基于的调用方案。

### 调用群集AEM Forms实例{#client-application-invoking-clustered-aem-forms-instances}的客户端应用程序

下图显示了在其自身的JVM中运行并调用群集中的AEM Forms实例的客户端应用程序。

此方案类似于调用独立AEM Forms实例的客户端应用程序。 但是，提供者URL不同。 如果客户端应用程序要连接到特定的J2EE应用程序服务器，则应用程序必须更改URL以引用特定的J2EE应用程序服务器。

不建议引用特定的J2EE应用程序服务器，因为如果应用程序服务器停止，客户端应用程序与AEM Forms之间的连接将终止。 建议提供程序URL引用单元格级JNDI管理器，而不是特定的J2EE应用程序服务器。

使用SOAP连接模式的客户端应用程序可以使用群集的HTTP负载平衡器端口。 使用EJB连接模式的客户端应用程序可以连接到特定J2EE应用程序服务器的EJB端口。 此操作处理群集节点之间的负载平衡。

**WebSphere**

以下示例显示用于连接到部署在WebSphere上的AEM Forms的jndi.properties文件的内容。

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

以下示例显示用于连接到部署在WebLogic上的AEM Forms的jndi.properties文件的内容。

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

以下示例显示用于连接到部署在JBoss上的AEM Forms的jndi.properties文件的内容。

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>请咨询管理员以确定J2EE应用程序服务器名和端口号。

**另请参阅**

[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java API将数据传递到AEM Forms服务](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客户端库调用服务](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java API {#passing-data-to-aem-forms-services-using-the-java-api}将数据传递到AEM Forms服务

AEM Forms服务操作通常使用或生成PDF文档。 调用服务时，有时需要将PDF文档(或其他文档类型，如XML数据)传递给服务。 同样，有时也需要处理从服务返回的PDF文档。 使您能够向AEM Forms服务传递数据和从Java服务传递数据的Java类为`com.adobe.idp.Document`。

AEM Forms服务不接受将PDF文档作为其他数据类型（如`java.io.InputStream`对象或字节数组）。 `com.adobe.idp.Document`对象还可用于将其他类型的数据（如XML数据）传递给服务。

`com.adobe.idp.Document`对象是Java可序列化类型，因此可通过RMI调用传递。 接收方可以配置（同一主机、同一类加载器）、本地（同一主机、不同类加载器）或远程（不同主机）。 每种情况下都会优化文档内容的传递。 例如，如果发送者和接收者位于同一主机上，则内容将通过本地文件系统传递。 (在某些情况下，文档可以在内存中传递。)

根据`com.adobe.idp.Document`对象大小，数据将在`com.adobe.idp.Document`对象中传输或存储在服务器的文件系统中。 在`com.adobe.idp.Document`处理后，由`com.adobe.idp.Document`对象占用的任何临时存储资源将自动删除。 (请参阅[处置文档对象](invoking-aem-forms-using-java.md#disposing-document-objects)。)

有时，在将`com.adobe.idp.Document`对象传递给服务之前，必须了解该对象的内容类型。 例如，如果某个操作需要特定的内容类型（如`application/pdf`），则建议您确定该内容类型。 (请参阅[确定文档的内容类型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)。)

`com.adobe.idp.Document`对象尝试使用提供的数据确定内容类型。 如果无法从提供的数据检索内容类型（例如，当数据作为字节数组提供时），请设置内容类型。 要设置内容类型，请调用`com.adobe.idp.Document`对象的`setContentType`方法。 (请参阅[确定文档的内容类型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

如果附属文件驻留在同一文件系统中，则创建`com.adobe.idp.Document`对象会更快。 如果附属文件驻留在远程文件系统上，则必须执行复制操作，这会影响性能。

应用程序可以同时包含`com.adobe.idp.Document`和`org.w3c.dom.Document`数据类型。 但是，请确保您完全符合`org.w3c.dom.Document`数据类型的条件。 有关将`org.w3c.dom.Document`对象转换为`com.adobe.idp.Document`对象的信息，请参阅[快速开始（EJB模式）：使用Java API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)使用可流式布局预填充Forms。

>[!NOTE]
>
>要防止在使用`com.adobe.idp.Document`对象时WebLogic中发生内存泄漏，请以2048字节或更少的块读取文档信息。 例如，以下代码以2048字节的块为单位读取文档信息：

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 创建文档{#creating-documents}

在调用需要PDF文档(或其他文档类型)作为输入值的服务操作之前，创建`com.adobe.idp.Document`对象。 `com.adobe.idp.Document`类提供了使您能够从以下内容类型创建文档的构造函数：

* 字节数组
* 现有`com.adobe.idp.Document`对象
* `java.io.File`对象
* `java.io.InputStream`对象
* `java.net.URL`对象

#### 创建基于字节数组{#creating-a-document-based-on-a-byte-array}的文档

下面的代码示例创建一个基于字节数组的`com.adobe.idp.Document`对象。

**创建基于字节数组的文档对象**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### 创建基于其他文档{#creating-a-document-based-on-another-document}的文档

下面的代码示例创建一个基于另一个`com.adobe.idp.Document`对象的`com.adobe.idp.Document`对象。

**创建基于其他文档的文档对象**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### 创建基于文件{#creating-a-document-based-on-a-file}的文档

下面的代码示例创建一个基于名为&#x200B;*map.pdf*&#x200B;的PDF文件的`com.adobe.idp.Document`对象。 此文件位于C硬盘的根目录中。 此构造函数尝试使用文件扩展名设置`com.adobe.idp.Document`对象的MIME内容类型。

接受`java.io.File`对象的`com.adobe.idp.Document`构造函数也接受布尔参数。 通过将此参数设置为`true`,`com.adobe.idp.Document`对象将删除文件。 此操作意味着将文件传递给`com.adobe.idp.Document`构造函数后，您不必删除该文件。

将此参数设置为`false`表示保留此文件的所有权。 将此参数设置为`true`更有效。 原因在于`com.adobe.idp.Document`对象可以将文件直接移动到本地管理区域，而不是复制它（速度较慢）。

**创建基于PDF文件的文档对象**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### 创建基于InputStream对象{#creating-a-document-based-on-an-inputstream-object}的文档

下面的Java代码示例创建基于`java.io.InputStream`对象的`com.adobe.idp.Document`对象。

**创建基于InputStream对象的文档**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### 根据可从URL {#creating-a-document-based-on-content-accessible-from-an-url}访问的内容创建文档

下面的Java代码示例创建一个`com.adobe.idp.Document`对象，该对象基于名为&#x200B;*map.pdf*&#x200B;的PDF文件。 此文件位于`localhost`上运行的名为`WebApp`的Web应用程序中。 此构造函数尝试使用URL协议返回的内容类型设置`com.adobe.idp.Document`对象的MIME内容类型。

提供给`com.adobe.idp.Document`对象的URL始终在创建原始`com.adobe.idp.Document`对象的一侧读取，如本例所示：

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

c:/temp/input.pdf文件必须位于客户端计算机（而非服务器计算机）上。 客户端计算机是读取URL和创建`com.adobe.idp.Document`对象的位置。

**根据可从URL访问的内容创建文档**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 处理返回的文档{#handling-returned-documents}

将PDF文档（或其他数据类型，如XML数据）返回为输出值的服务操作将返回`com.adobe.idp.Document`对象。 收到`com.adobe.idp.Document`对象后，可将其转换为以下格式：

* `java.io.File`对象
* `java.io.InputStream`对象
* 字节数组

下面的代码行将`com.adobe.idp.Document`对象转换为`java.io.InputStream`对象。 假设`myPDFDocument`表示`com.adobe.idp.Document`对象：

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同样，您也可以通过执行以下任务将`com.adobe.idp.Document`的内容复制到本地文件：

1. 创建`java.io.File`对象。
1. 调用`com.adobe.idp.Document`对象的`copyToFile`方法并传递`java.io.File`对象。

下面的代码示例将`com.adobe.idp.Document`对象的内容复制到名为&#x200B;*AnotherMap.pdf*&#x200B;的文件。

**将文档对象的内容复制到文件**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 确定文档{#determining-the-content-type-of-a-document}的内容类型

通过调用`com.adobe.idp.Document`对象的`getContentType`方法，确定`com.adobe.idp.Document`对象的MIME类型。 此方法返回一个字符串值，它指定`com.adobe.idp.Document`对象的内容类型。 下表描述了AEM Forms返回的不同内容类型。

<table>
 <thead>
  <tr>
   <th><p>MIME类型</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>PDF文档</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>XML数据打包(XDP)，用于导出的XML Forms体系架构(XFA)表单</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>书签、附件或其他XML文档</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Forms数据格式(FDF)，用于导出Acrobat表单</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms数据格式(XFDF)，用于导出的Acrobat表单</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>丰富数据格式和XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>通用数据格式</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>未指定MIME类型</p></td>
  </tr>
 </tbody>
</table>

下面的代码示例确定`com.adobe.idp.Document`对象的内容类型。

**确定文档对象的内容类型**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 处置文档对象{#disposing-document-objects}

当不再需要`Document`对象时，建议通过调用其`dispose`方法来处理该对象。 每个`Document`对象都使用一个文件描述符，并在应用程序的主机平台上占用多达75 MB的RAM空间。 如果`Document`对象未处置，则Java Garage收集过程将处理它。 但是，通过使用`dispose`方法更快地处理它，您可以释放由`Document`对象占用的内存。

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java客户端库调用服务](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java客户端库{#invoking-a-service-using-a-java-client-library}调用服务

AEM Forms服务操作可通过使用服务的强类型API（称为Java客户端库）来调用。 *Java客户端库*&#x200B;是一组具体类，提供对在服务容器中部署的服务的访问。 使用调用API实例化表示要调用的服务的Java对象，而不是创建`InvocationRequest`对象。 调用API用于调用在Workbench中创建的进程等长寿命进程。 （请参阅[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。）

要执行服务操作，请调用属于Java对象的方法。 Java客户端库包含通常将服务操作一对一映射的方法。 使用Java客户端库时，设置所需的连接属性。 （请参阅[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)。）

设置连接属性后，创建一个`ServiceClientFactory`对象，用于实例化允许调用服务的Java对象。 具有Java客户端库的每个服务都具有相应的客户端对象。 例如，要调用Repository服务，请使用`ResourceRepositoryClient`对象的构造函数创建一个`ServiceClientFactory`对象。 `ServiceClientFactory`对象负责维护调用AEM Forms服务所需的连接设置。

虽然获取`ServiceClientFactory`通常很快，但首次使用工厂时会涉及一些开销。 此对象经过优化以便重复使用，因此，在创建多个Java客户端对象时，尽可能使用相同的`ServiceClientFactory`对象。 也就是说，不要为您创建的每个客户端库对象创建单独的`ServiceClientFactory`对象。

“用户管理器”设置用于控制影响`ServiceClientFactory`对象的`com.adobe.idp.Context`对象内的SAML断言的存留期。 此设置控制整个AEM Forms中的所有身份验证上下文生命周期，包括使用Java API执行的所有调用。 默认情况下，可使用`ServiceCleintFactory`对象的时间段为两小时。

>[!NOTE]
>
>要说明如何使用Java API调用服务，将调用存储库服务的`writeResource`操作。 此操作会将新资源放入存储库中。

您可以通过使用Java客户端库并执行以下步骤来调用存储库服务：

1. 在Java项目的类路径中包含客户端JAR文件，如adobe-repository-client.jar。 有关这些文件位置的信息，请参阅[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 设置调用服务所需的连接属性。
1. 通过调用`ServiceClientFactory`对象的静态`createInstance`方法并传递包含连接属性的`java.util.Properties`对象，创建`ServiceClientFactory`对象。
1. 使用`ResourceRepositoryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。 使用`ResourceRepositoryClient`对象调用存储库服务操作。
1. 使用其构造函数创建`RepositoryInfomodelFactoryBean`对象，并传递`null`。 通过此对象，可创建一个`Resource`对象，它表示已添加到存储库的内容。
1. 通过调用`RepositoryInfomodelFactoryBean`对象的`newImage`方法并传递以下值，创建`Resource`对象：

   * 通过指定`new Id()`的唯一ID值。
   * 通过指定`new Lid()`的唯一UUID值。
   * 资源的名称。 可以指定XDP文件的文件名。

   将返回值转换为`Resource`。

1. 通过调用`RepositoryInfomodelFactoryBean`对象的`newImage`方法并将返回值转换为`ResourceContent`，创建`ResourceContent`对象。 此对象表示添加到存储库的内容。
1. 通过传递存储要添加到存储库的XDP文件的`java.io.FileInputStream`对象，创建`com.adobe.idp.Document`对象。 (请参阅[创建基于InputStream对象的文档](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)。)
1. 通过调用`ResourceContent`对象的`setDataDocument`方法，将`com.adobe.idp.Document`对象的内容添加到`ResourceContent`对象。 传递`com.adobe.idp.Document`对象。
1. 通过调用`ResourceContent`对象的`setMimeType`方法并传递`application/vnd.adobe.xdp+xml`，设置要添加到存储库的XDP文件的MIME类型。
1. 通过调用`Resource`对象&#39;s `setContent`方法并传递`ResourceContent`对象，将`ResourceContent`对象的内容添加到`Resource`对象。
1. 通过调用`Resource`对象&#39;s `setDescription`方法并传递表示资源描述的字符串值，添加资源描述。
1. 通过调用`ResourceRepositoryClient`对象的`writeResource`方法并传递以下值，将表单设计添加到存储库：

   * 一个字符串值，它指定包含新资源的资源集合的路径
   * 创建的`Resource`对象

**另请参阅**

[快速开始（EJB模式）：使用Java API编写资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 使用调用API {#invoking-a-short-lived-process-using-the-invocation-api}调用短时间进程

您可以使用Java调用API调用短时间进程。 使用调用API调用短时间进程时，使用`java.util.HashMap`对象传递所需的参数值。 对于要传递到服务的每个参数，调用`java.util.HashMap`对象的`put`方法并指定服务所需的名称 — 值对以执行指定的操作。 指定属于短时间进程的参数的确切名称。

>[!NOTE]
>
>有关调用长寿命进程的信息，请参阅[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

此处讨论的内容是使用调用API调用以下名为`MyApplication/EncryptDocument`的AEM Forms短时进程。

>[!NOTE]
>
>此过程不基于现有的AEM Forms进程。 要与代码示例一起使用，请使用Workbench创建一个名为`MyApplication/EncryptDocument`的进程。 （请参阅[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

调用此进程时，将执行以下操作：

1. 获取传递给该流程的不安全的PDF文档。 此操作基于`SetValue`操作。 此进程的输入参数是名为`inDoc`的`document`进程变量。
1. 使用密码加密PDF文档。 此操作基于`PasswordEncryptPDF`操作。 在名为`outDoc`的进程变量中返回密码加密的PDF文档。

### 使用Java调用API {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}调用MyApplication/EncryptDocument短时进程

使用Java调用API调用`MyApplication/EncryptDocument`短时进程：

1. 在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。 (请参阅[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)
1. 创建包含连接属性的`ServiceClientFactory`对象。 （请参阅[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)。）
1. 使用`ServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。 `ServiceClient`对象允许您调用服务操作。 它处理任务，如查找、调度和路由调用请求。
1. 使用`java.util.HashMap`对象的构造函数创建对象。
1. 为每个输入参数调用`java.util.HashMap`对象的`put`方法以传递到长寿命进程。 由于`MyApplication/EncryptDocument`短期进程需要一个类型为`Document`的输入参数，因此只需调用`put`方法一次，如以下示例所示。

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. 通过调用`ServiceClientFactory`对象的`createInvocationRequest`方法并传递以下值，创建`InvocationRequest`对象：

   * 一个字符串值，它指定要调用的长时间进程的名称。 要调用`MyApplication/EncryptDocument`进程，请指定`MyApplication/EncryptDocument`。
   * 一个字符串值，它表示进程操作名称。 通常，短时间进程操作的名称为`invoke`。
   * `java.util.HashMap`对象，其中包含服务操作所需的参数值。
   * 一个布尔值，它指定`true`，用于创建同步请求（此值适用于调用短时间进程）。

1. 通过调用`ServiceClient`对象的`invoke`方法并传递`InvocationRequest`对象，将调用请求发送到服务。 `invoke`方法返回`InvocationReponse`对象。

   >[!NOTE]
   >
   >通过传递值`false`作为`createInvocationRequest`方法的第四个参数，可以调用长寿命进程。 传递值&#x200B;`false`*将创建异步请求。*

1. 通过调用`InvocationReponse`对象的`getOutputParameter`方法并传递指定输出参数名称的字符串值，检索进程的返回值。 在这种情况下，请指定`outDoc`（`outDoc`是`MyApplication/EncryptDocument`进程的输出参数的名称）。 将返回值转换为`Document`，如下例所示。

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. 创建一个`java.io.File`对象，并确保文件扩展名为.pdf。
1. 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`com.adobe.idp.Document`对象的内容复制到文件。 请确保使用由`getOutputParameter`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[快速开始:使用调用API调用短时间进程](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)