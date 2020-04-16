---
title: 使用JavaAPI调用AEM Forms
seo-title: 使用JavaAPI调用AEM Forms
description: 'null'
seo-description: 'null'
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 使用Java API调用AEM Forms {#invoking-aem-forms-using-the-javaapi}

可以使用AEM Forms Java API调用AEM Forms。 使用AEM Forms Java API时，您可以使用调用API或Java客户端库。 Java客户端库可用于Rights Management服务等服务。 这些强类型API允许您开发调用AEM Forms的Java应用程序。

调用API是位于包中的 `com.adobe.idp.dsc` 类。 使用这些类，您可以将调用请求直接发送到服务并处理返回的调用响应。 使用调用API调用使用Workbench创建的短期或长期进程。

以编程方式调用服务的建议方法是使用与服务相对应的Java客户端库，而不是调用API。 例如，要调用加密服务，请使用加密服务客户端库。 要执行加密服务操作，请调用属于加密服务客户端对象的方法。 您可以通过调用对象的方法来使用口令加 `EncryptionServiceClient` 密PDF文档 `encryptPDFUsingPassword` 。

Java API支持以下功能：

* 用于远程调用的RMI传输协议
* 用于本地调用的虚拟机传输
* 用于远程调用的SOAP
* 不同的身份验证，如用户名和密码
* 同步和异步调用请求

**Adobe开发人员网站**

Adobe开发人员网站包含以下文章，其中讨论如何使用Java API调用AEM Forms服务：

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

[创建调用以人为中心的长寿命流程的Java Web应用程序](/help/forms/developing/invoking-human-centric-long-lived.md)

## 包括AEM Forms Java库文件 {#including-aem-forms-java-library-files}

要通过使用Java API以编程方式调用AEM Forms服务，请在Java项目的类路径中包含所需的库文件（JAR文件）。 包含在客户端应用程序的类路径中的JAR文件取决于以下几个因素：

* 要调用的AEM Forms服务。 客户端应用程序可以调用一个或多个服务。
* 要调用AEM Forms服务的模式。 可以使用EJB或SOAP模式。 (请参阅 [设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)。)

>[!NOTE]
>
>（仅限统包）用命令开始AEM Forms服务器，以 `standalone.bat -b <Server IP> -c lc_turnkey.xml` 指定EJB的服务器IP

* 部署了AEM Forms的J2EE应用程序服务器。

### 特定于服务的JAR文件 {#service-specific-jar-files}

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
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>必须始终包含在Java客户端应用程序的类路径中。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>必须始终包含在Java客户端应用程序的类路径中。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk//client-libs/&lt;app server&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>调用Application Manager服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>调用Assembler服务时必需。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>调用备份和还原服务API时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>调用条形码表单服务时必需。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>调用“转换PDF”服务时需要。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>调用Distiller服务时必需。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>调用DocConverter服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>调用文档管理服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>调用加密服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>调用表单服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>调用表单数据集成服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>调用“生成PDF”服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>调用“生成3D PDF”服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>调用作业管理器服务时需要。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>调用输出服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>调用PDF实用程序或XMP实用程序服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>调用Acrobat Reader DC扩展服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>调用存储库服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>install directory</i>&gt;/sdk/client-libs\thirdparty</p></td>
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
   <td><p>调用Rights Management服务时需要。</p><p>如果AEM Forms部署在JBoss上，请包括所有这些文件。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p><p>特定于JBoss的lib目录</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>调用签名服务时需要。</p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>调用任务管理器服务时必需。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>调用信任存储服务时需要。 </p></td>
   <td><p>&lt;<i>install directory</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### 连接模式和J2EE应用程序JAR文件 {#connection-mode-and-j2ee-application-jar-files}

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
     <li><p>jaxen-1.1 beta-9.jar</p> </li>
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
   <td><p>如果使用SOAP模式调用AEM表单，请包括这些JAR文件。</p> </td>
   <td><p>&lt;<em>install directory</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>如果AEM Forms部署在JBoss Application Server上，请包含此JAR文件。</p> <p>如果jboss-client.jar和引用的jar未共同位置，则classloader将找不到必需的类。</p> </td>
   <td><p>JBoss客户端库目录</p> <p>如果在同一J2EE应用程序服务器上部署客户端应用程序，则无需包含此文件。</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>如果AEM Forms部署在BEA WebLogic Server®上，则包括此JAR文件。</p> </td>
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
   <td><p>特定于WebSphere的lib目<em>录([WAS_HOME]</em>/运行时)</p> <p>如果在同一J2EE应用程序服务器上部署客户端应用程序，则不必包括这些文件。</p> </td>
  </tr>
 </tbody>
</table>

### 调用方案 {#invoking-scenarios}

下表指定调用方案并列表所需的JAR文件以成功调用AEM Forms。

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
   <td><p>表单服务</p> </td>
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
   <td><p>表单服务</p> <p>Acrobat Reader DC扩展服务</p> <p>签名服务</p> </td>
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
   <td><p>表单服务</p> </td>
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
     <li><p>jaxen-1.1 beta-9.jar</p> </li>
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
   <td><p>表单服务</p> <p>Acrobat Reader DC扩展服务</p> <p>签名服务</p> </td>
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
     <li><p>jaxen-1.1 beta-9.jar</p> </li>
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

### 升级JAR文件 {#upgrading-jar-files}

如果从LiveCycle升级到AEM Forms，建议将AEM Forms JAR文件包含在Java项目的类路径中。 例如，如果您使用Rights Management服务等服务，则在类路径中不包括AEM Forms JAR文件时，将会遇到兼容性问题。

假设您要升级到AEM Forms。 要使用调用Rights Management服务的Java应用程序，请包括以下JAR文件的AEM Forms版本：

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API将数据传递到AEM Forms服务](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客户端库调用服务](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 设置连接属性 {#setting-connection-properties}

使用Java API时，可设置连接属性以调用AEM Forms。 在设置连接属性时，指定远程还是本地调用服务，还指定连接模式和身份验证值。 如果启用了服务安全性，则需要身份验证值。 但是，如果禁用了服务安全性，则无需指定身份验证值。

连接模式可以是SOAP模式或EJB模式。 EJB模式使用RMI/IIOP协议，EJB模式的性能优于SOAP模式的性能。 SOAP模式用于消除J2EE应用程序服务器依赖性，或当防火墙位于AEM Forms和客户端应用程序之间时。 SOAP模式使用https协议作为底层传输，并可以跨防火墙边界通信。 如果J2EE应用程序服务器依赖关系或防火墙都不是问题，则建议使用EJB模式。

要成功调用AEM Forms服务，请设置以下连接属性：

* **DSC_DEFAULT_EJB_ENDPOINT:** 如果使用EJB连接模式，则此值表示部署了AEM Forms的J2EE应用程序服务器的URL。 要远程调用AEM表单，请指定部署AEM表单的J2EE应用程序服务器名称。 如果您的客户端应用程序位于同一J2EE应用程序服务器上，则可以指定 `localhost`。 根据部署J2EE应用程序服务器AEM Forms时所在的位置，指定以下值之一：

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**:如果您使用SOAP连接模式，此值表示向其发送调用请求的端点。 要远程调用AEM表单，请指定部署AEM表单的J2EE应用程序服务器名称。 如果您的客户端应用程序位于同一J2EE应用程序服务器上，则可以指 `localhost` 定(例如， `http://localhost:8080`)

   * 如果J2EE应 `8080` 用程序是JBoss，则端口值适用。 如果J2EE应用程序服务器是IBM® WebSphere®，请使用端口 `9080`。 同样，如果J2EE应用程序服务器是WebLogic，则使用端口 `7001`。 (这些值是默认端口值。 如果更改端口值，请使用适用的端口号。)

* **DSC_TRANSPORT_PROTOCOL**:如果使用EJB连接模式，请为 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 此值指定。 如果使用SOAP连接模式，请指定 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`。
* **DSC_SERVER_TYPE**:指定部署AEM Forms的J2EE应用程序服务器。 有效值 `JBoss`为， `WebSphere`、 `WebLogic`。

   * 如果将此连接属性设 `WebSphere`置为， `java.naming.factory.initial` 则值将设置为 `com.ibm.ws.naming.util.WsnInitCtxFactory`。
   * 如果将此连接属性设 `WebLogic`置为， `java.naming.factory.initial` 则值将设置为 `weblogic.jndi.WLInitialContextFactory`。
   * 同样，如果将此连接属性设 `JBoss`置为， `java.naming.factory.initial` 则该值将设置为 `org.jnp.interfaces.NamingContextFactory`。
   * 如果您不 `java.naming.factory.initial` 想使用默认值，可以将属性设置为符合要求的值。
   >[!NOTE]
   >
   >可以使用类的静态成员，而 `DSC_SERVER_TYPE` 不是使用字符串设置连接属 `ServiceClientFactoryProperties` 性。 可以使用以下值： `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`、 `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`或 `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`。

* **DSC_CREDENTIAL_USERNAME:** 指定AEM表单用户名。 要使用户成功调用AEM Forms服务，他们需要服务用户角色。 用户还可以具有包含服务调用权限的其他角色。 否则，当他们尝试调用服务时会引发异常。 如果禁用了服务安全性，则无需指定此连接属性。
* **DSC_CREDENTIAL_PASSWORD:** 指定相应的口令值。 如果禁用了服务安全性，则无需指定此连接属性。
* **DSC_REQUEST_TIMEOUT:** SOAP请求的默认请求超时限制为1200000毫秒（20分钟）。 有时，请求可能需要更长的时间才能完成操作。 例如，检索大量记录的SOAP请求可能需要更长的超时限制。 您可以使用 `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` 来增加SOAP请求的请求调用超时限制。

   **注意**:只有基于SOAP的调用支持DSC_REQUEST_TIMEOUT属性。

要设置连接属性，请执行以下任务:

1. 使用对 `java.util.Properties` 象的构造函数创建对象。
1. 要设置连 `DSC_DEFAULT_EJB_ENDPOINT` 接属性，请调用对 `java.util.Properties` 象的方法并 `setProperty` 传递以下值：

   * 明细列表 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 值
   * 一个字符串值，它指定承载AEM Forms的J2EE应用程序服务器的URL
   >[!NOTE]
   >
   >如果使用SOAP连接模式，请指定明细列表 `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` 值而不是明细列表 `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` 值。

1. 要设置连 `DSC_TRANSPORT_PROTOCOL` 接属性，请调用对 `java.util.Properties` 象的方法并 `setProperty` 传递以下值：

   * 明细列表 `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` 值
   * 明细列表 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 值
   >[!NOTE]
   >
   >如果使用SOAP连接模式，请指定 `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`明细列表值而不是 `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` 明细列表值。

1. 要设置连 `DSC_SERVER_TYPE` 接属性，请调用对 `java.util.Properties` 象的方法并 `setProperty` 传递以下值：

   * 明细列表 `ServiceClientFactoryProperties.DSC_SERVER_TYPE`值
   * 一个字符串值，它指定承载AEM Forms的J2EE应用程序服务器(例如，如果AEM Forms部署在JBoss上，请指定 `JBoss`)。

      1. 要设置连 `DSC_CREDENTIAL_USERNAME` 接属性，请调用对 `java.util.Properties` 象的方法并 `setProperty` 传递以下值：
   * 明细列表 `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` 值
   * 一个字符串值，它指定调用AEM Forms所需的用户名

      1. 要设置连 `DSC_CREDENTIAL_PASSWORD` 接属性，请调用对 `java.util.Properties` 象的方法并 `setProperty` 传递以下值：
   * 明细列表 `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` 值
   * 指定相应密码值的字符串值



**为JBoss设置EJB连接模式**

以下Java代码示例设置连接属性以调用在JBoss上部署的AEM Forms，并使用EJB连接模式。

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**为WebLogic设置EJB连接模式**

以下Java代码示例设置连接属性以调用在WebLogic上部署的AEM Forms，并使用EJB连接模式。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**为WebSphere设置EJB连接模式**

以下Java代码示例设置连接属性以调用在WebSphere上部署的AEM Forms，并使用EJB连接模式。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**设置SOAP连接模式**

以下Java代码示例在SOAP模式中设置连接属性以调用在JBoss上部署的AEM Forms。

```as3
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

**在禁用服务安全性时设置连接属性**

以下Java代码示例设置调用在JBoss Application Server上部署的AEM Forms以及禁用服务安全性时所需的连接属性。

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>与AEM Forms编程关联的所有Java快速开始都显示EJB和SOAP连接设置。

**使用自定义请求超时限制设置SOAP连接模式**

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**使用Context对象调用AEM Forms**

您可以使用对 `com.adobe.idp.Context` 象与已验证的用户(对象表示已验证的用 `com.adobe.idp.Context` 户)调用AEM Forms服务。 使用对 `com.adobe.idp.Context` 象时，无需设置或 `DSC_CREDENTIAL_USERNAME` 属 `DSC_CREDENTIAL_PASSWORD` 性。 使用对象的方 `com.adobe.idp.Context` 法验证用户时，可以获 `AuthenticationManagerServiceClient` 得对象的身 `authenticate` 份。

该方 `authenticate` 法返回一 `AuthResult` 个包含验证结果的对象。 可以通过调用 `com.adobe.idp.Context` 对象的构造函数来创建对象。 然后调用 `com.adobe.idp.Context` 对象的方 `initPrincipal` 法并传递 `AuthResult` 对象，如以下代码所示：

```as3
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

您可以调用对象 `DSC_CREDENTIAL_USERNAME` 的方法并传递对象，而不 `DSC_CREDENTIAL_PASSWORD` 是设置或 `ServiceClientFactory``setContext``com.adobe.idp.Context` 属性。 使用AEM Forms用户调用服务时，请确保他们具有名为的角色，该角 `Services User` 色是调用AEM Forms服务所必需的。

下面的代码示例演示如何在用 `com.adobe.idp.Context` 于创建对象的连接设置中使用对 `EncryptionServiceClient` 象。

```as3
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
>有关对用户进行身份验证的完整详细信息，请参阅对 [用户进行身份验证](/help/forms/developing/users.md#authenticating-users)。

### 调用方案 {#invoking_scenarios-1}

本节将讨论以下调用场景：

* 在其自己的Java虚拟机(JVM)中运行的客户端应用程序调用独立的AEM Forms实例。
* 在其自身的JVM中运行的客户端应用程序调用群集化的AEM Forms实例。

### 调用独立AEM Forms实例的客户端应用程序 {#client-application-invoking-a-stand-alone-aem-forms-instance}

下图显示了在其自己的JVM中运行并调用独立AEM Forms实例的客户端应用程序。

在此方案中，客户端应用程序在其自己的JVM中运行并调用AEM Forms服务。

>[!NOTE]
>
>此方案是所有快速开始所基于的调用方案。

### 调用群集化AEM Forms实例的客户端应用程序 {#client-application-invoking-clustered-aem-forms-instances}

下图显示了在其自己的JVM中运行并调用位于群集中的AEM Forms实例的客户端应用程序。

此方案类似于调用独立AEM Forms实例的客户端应用程序。 但是，提供者URL不同。 如果客户端应用程序要连接到特定的J2EE应用程序服务器，则应用程序必须更改URL以引用特定的J2EE应用程序服务器。

不建议引用特定的J2EE应用程序服务器，因为如果应用程序服务器停止，则客户端应用程序与AEM Forms之间的连接将终止。 建议提供者URL引用单元格级JNDI管理器，而不是特定的J2EE应用程序服务器。

使用SOAP连接模式的客户端应用程序可以使用群集的HTTP负载平衡器端口。 使用EJB连接模式的客户端应用程序可以连接到特定J2EE应用程序服务器的EJB端口。 此操作处理群集节点之间的负载平衡。

**WebSphere**

以下示例显示了用于连接到在WebSphere上部署的AEM Forms的jndi.properties文件的内容。

```as3
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

以下示例显示了用于连接到在WebLogic上部署的AEM Forms的jndi.properties文件的内容。

```as3
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

以下示例显示了用于连接到JBoss上部署的AEM Forms的jndi.properties文件的内容。

```as3
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>请咨询您的管理员以确定J2EE应用程序服务器名称和端口号。

**另请参阅**

[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java API将数据传递到AEM Forms服务](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[使用Java客户端库调用服务](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java API将数据传递到AEM Forms服务 {#passing-data-to-aem-forms-services-using-the-java-api}

AEM Forms服务操作通常使用或生成PDF文档。 调用服务时，有时需要将PDF文档(或其他文档类型，如XML数据)传递给服务。 同样，有时也需要处理从服务返回的PDF文档。 允许您向AEM Forms服务传递数据和从AEM Forms服务传递数据的Java类是 `com.adobe.idp.Document`。

AEM Forms服务不接受PDF文档作为其他数据类型，如对 `java.io.InputStream` 象或字节数组。 对 `com.adobe.idp.Document` 象还可用于将XML数据等其他类型的数据传递给服务。

对 `com.adobe.idp.Document` 象是Java可序列化类型，因此可以通过RMI调用传递它。 接收方可以配置（同一主机、同一类加载器）、本地（同一主机、不同类加载器）或远程（不同主机）。 针对每种情况优化了文档内容的传递。 例如，如果发送方和接收方位于同一主机上，则内容会通过本地文件系统进行传递。 (在某些情况下，文档可以在内存中传递。)

根据对 `com.adobe.idp.Document` 象大小，数据将被传输到对象中或 `com.adobe.idp.Document` 存储在服务器的文件系统中。 该对象占用的任何临时存储资 `com.adobe.idp.Document` 源在处置时自动被移 `com.adobe.idp.Document` 除。 (请参阅 [处理文档对象](invoking-aem-forms-using-java.md#disposing-document-objects)。)

有时，在将对象传递给服务之前， `com.adobe.idp.Document` 必须了解该对象的内容类型。 例如，如果某个操作需要特定的内容类型(如 `application/pdf`，建议您确定内容类型)。 (请参 [阅确定文档的内容类型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document)。)

对 `com.adobe.idp.Document` 象尝试使用提供的数据确定内容类型。 如果无法从提供的数据检索内容类型（例如，当数据作为字节数组提供时），请设置内容类型。 要设置内容类型，请调用对 `com.adobe.idp.Document` 象的方 `setContentType` 法。 (请参 [阅确定文档的内容类型](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

如果附属文件位于同一文件系统中，则创建对象的 `com.adobe.idp.Document` 速度会更快。 如果附属文件驻留在远程文件系统上，则必须执行复制操作，这会影响性能。

应用程序可以同时包含 `com.adobe.idp.Document` 数据 `org.w3c.dom.Document` 类型和数据类型。 但是，请确保您完全限定了数 `org.w3c.dom.Document` 据类型。 有关将对象转换 `org.w3c.dom.Document` 为对象的 `com.adobe.idp.Document` 信息，请参 [阅快速开始（EJB模式）:使用Java API使用可流动布局预填充表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)。

>[!NOTE]
>
>为了在使用对象时防止WebLogic中的内存泄漏， `com.adobe.idp.Document` 请以2048字节或更少的块读取文档信息。 例如，以下代码以2048字节的块为单位读取文档信息：

```as3
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

### 创建文档 {#creating-documents}

在调用 `com.adobe.idp.Document` 需要PDF文档(或其他文档类型)作为输入值的服务操作之前，先创建一个对象。 类提 `com.adobe.idp.Document` 供了使您能够从以下内容类型创建文档的构造函数：

* 字节数组
* 现有对 `com.adobe.idp.Document` 象
* 对 `java.io.File` 象
* 对 `java.io.InputStream` 象
* 对 `java.net.URL` 象

#### 创建基于字节数组的文档 {#creating-a-document-based-on-a-byte-array}

下面的代码示例创建 `com.adobe.idp.Document` 一个基于字节数组的对象。

**创建基于字节数组的文档对象**

```as3
 Document myPDFDocument = new Document(myByteArray);
```

#### 创建基于其他文档的文档 {#creating-a-document-based-on-another-document}

下面的代码示例创建一 `com.adobe.idp.Document` 个基于另一个对象的 `com.adobe.idp.Document` 对象。

**创建基于其他文档的文档对象**

```as3
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

#### 创建基于文件的文档 {#creating-a-document-based-on-a-file}

下面的代码示例创建 `com.adobe.idp.Document` 一个基于名为map.pdf的PDF文件 *的对象*。 此文件位于C硬盘的根目录下。 此构造函数尝试使用文件扩展名设置对 `com.adobe.idp.Document` 象的MIME内容类型。

接受 `com.adobe.idp.Document` 对象的构造函 `java.io.File` 数也接受Boolean参数。 通过将此参数设 `true`置为， `com.adobe.idp.Document` 对象将删除文件。 此操作意味着您不必在将文件传递给构造函数后删除该文 `com.adobe.idp.Document` 件。

将此参数设 `false` 置为表示您保留此文件的所有权。 将此参数设置 `true` 为更高效。 原因是对象可 `com.adobe.idp.Document` 以将文件直接移到本地管理区域，而不是复制它（速度较慢）。

**创建基于PDF文件的文档对象**

```as3
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### 创建基于InputStream对象的文档 {#creating-a-document-based-on-an-inputstream-object}

下面的Java代码示例创建 `com.adobe.idp.Document` 一个基于对象的对 `java.io.InputStream` 象。

**创建基于InputStream对象的文档**

```as3
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### 根据可从URL访问的内容创建文档 {#creating-a-document-based-on-content-accessible-from-an-url}

以下Java代码示例创建一 `com.adobe.idp.Document` 个基于名为map.pdf的PDF文件 *的对象*。 此文件位于运行于的名为Web `WebApp` 的应用程序中 `localhost`。 此构造函数尝试使 `com.adobe.idp.Document` 用随URL协议返回的内容类型设置对象的MIME内容类型。

提供给对象的URL `com.adobe.idp.Document` 始终在创建原始对象的一 `com.adobe.idp.Document` 侧读取，如以下示例所示：

```as3
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

c:/temp/input.pdf文件必须位于客户端计算机（而非服务器计算机）上。 客户端计算机是读取URL和创建对象 `com.adobe.idp.Document` 的位置。

**根据可从URL访问的内容创建文档**

```as3
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 处理返回的文档 {#handling-returned-documents}

将PDF文档（或其他数据类型，如XML数据）返回为输出值的服务操作将返回一个对 `com.adobe.idp.Document` 象。 在您收到对 `com.adobe.idp.Document` 象后，可以将其转换为以下格式：

* 对 `java.io.File` 象
* 对 `java.io.InputStream` 象
* 字节数组

下面的代码行将对象 `com.adobe.idp.Document` 转换为对 `java.io.InputStream` 象。 假定它 `myPDFDocument` 表示对 `com.adobe.idp.Document` 象：

```as3
     java.io.InputStream resultStream = myDocument.getInputStream();
```

同样，您也可以通过执行以 `com.adobe.idp.Document` 下任务将本地文件的内容复制到：

1. 创建对 `java.io.File` 象。
1. 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法并传递对 `java.io.File`象。

下面的代码示例将对象的内容复 `com.adobe.idp.Document` 制到名为 *AnotherMap.pdf的文件*。

**将文档对象的内容复制到文件**

```as3
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 确定文档的内容类型 {#determining-the-content-type-of-a-document}

通过调用对象的方 `com.adobe.idp.Document` 法确定对 `com.adobe.idp.Document` 象的MIME类 `getContentType` 型。 此方法返回一个字符串值，它指定对象的内容类 `com.adobe.idp.Document` 型。 下表介绍了AEM Forms返回的不同内容类型。

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
   <td><p>XML数据打包(XDP)，用于导出的XML表单体系结构(XFA)表单</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>书签、附件或其他XML文档</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>表单数据格式(FDF)，用于导出的Acrobat表单</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML表单数据格式(XFDF)，用于导出的Acrobat表单</p></td>
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

以下代码示例确定对象的内容类 `com.adobe.idp.Document` 型。

**确定文档对象的内容类型**

```as3
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)

### 处理文档对象 {#disposing-document-objects}

当您不再需要对 `Document` 象时，建议您通过调用其方法来处理该对 `dispose` 象。 每个 `Document` 对象都会在应用程序的主机平台上使用一个文件描述符和高达75 MB的RAM空间。 如果未 `Document` 放置对象，则Java Garage收集进程将其放置。 但是，通过使用该方法，可以更 `dispose` 快地处理它，从而释放对象占用的内 `Document` 存。

**另请参阅**

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[使用Java客户端库调用服务](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## 使用Java客户端库调用服务 {#invoking-a-service-using-a-java-client-library}

可以使用服务的强类型API（称为Java客户端库）调用AEM Forms服务操作。 *Java客户端库是一组具体类* ，它们提供对服务容器中部署的服务的访问。 您将表示要调用的服务的Java对象实例化，而不是使用调 `InvocationRequest` 用API创建对象。 调用API用于调用在Workbench中创建的进程等长期进程。 (请参 [阅调用以人为中心的长寿命流程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。)

要执行服务操作，请调用属于Java对象的方法。 Java客户端库包含通常将一对一与服务操作映射的方法。 使用Java客户端库时，请设置所需的连接属性。 (请参阅 [设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)。)

在设置连接属性后，创建 `ServiceClientFactory` 一个对象，该对象用于实例化Java对象，通过它可以调用服务。 每个具有Java客户端库的服务都有一个相应的客户端对象。 例如，要调用存储库服务，请使用其构造 `ResourceRepositoryClient` 函数并传递对象来创建对 `ServiceClientFactory` 象。 对 `ServiceClientFactory` 象负责维护调用AEM Forms服务所需的连接设置。

虽然获取 `ServiceClientFactory` 的速度通常很快，但在首次使用工厂时会涉及一些开销。 此对象经过优化以便重复使用，因此，在创建多个Java客 `ServiceClientFactory` 户端对象时，如果可能，请使用同一对象。 也就是说，请勿为您创建的每 `ServiceClientFactory` 个客户端库对象创建单独的对象。

“用户管理器”设置用于控制SAML断言的生命周期，该断言位于影响对 `com.adobe.idp.Context` 象的对象 `ServiceClientFactory` 内。 此设置控制整个AEM Forms中的所有身份验证上下文使用期，包括使用Java API执行的所有调用。 默认情况下，可使用对象 `ServiceCleintFactory` 的时间段为两小时。

>[!NOTE]
>
>要说明如何使用Java API调用服务，将调用存储库服务 `writeResource` 的操作。 此操作会将新资源放入存储库中。

您可以通过使用Java客户端库并通过执行以下步骤调用存储库服务：

1. 在Java项目的类路径中包含客户端JAR文件，如adobe-repository-client.jar。 有关这些文件的位置的信息，请参 [阅包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 设置调用服务所需的连接属性。
1. 通过调 `ServiceClientFactory` 用对象的静态方 `ServiceClientFactory` 法并传递包含连接属性 `createInstance` 的对 `java.util.Properties` 象来创建对象。
1. 使用对 `ResourceRepositoryClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。 使用该对 `ResourceRepositoryClient` 象调用存储库服务操作。
1. 使用对 `RepositoryInfomodelFactoryBean` 象的构造函数和传递创建对象 `null`。 通过此对象，您可以创 `Resource` 建一个对象，它表示已添加到存储库的内容。
1. 通过调 `Resource` 用对象的方法并 `RepositoryInfomodelFactoryBean` 传递以 `newImage` 下值来创建对象：

   * 通过指定唯一的ID值 `new Id()`。
   * 通过指定的唯一UUID值 `new Lid()`。
   * 资源的名称。 可以指定XDP文件的文件名。
   将返回值转换为 `Resource`。

1. 通过调 `ResourceContent` 用对象的方 `RepositoryInfomodelFactoryBean` 法并将返回值转 `newImage` 换为，创建对象 `ResourceContent`。 此对象表示添加到存储库的内容。
1. 通过传 `com.adobe.idp.Document` 递存储XDP文件的对 `java.io.FileInputStream` 象来创建一个对象，并将其添加到存储库。 (请参 [阅基于InputStream对象创建文档](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)。)
1. 通过调用对 `com.adobe.idp.Document` 象的方 `ResourceContent` 法，将对象 `ResourceContent` 的内容添加到对 `setDataDocument` 象。 传递对 `com.adobe.idp.Document` 象。
1. 通过调用对象的方法并传递，设置要添加到存储库的XDP `ResourceContent` 文件的MIME `setMimeType` 类型 `application/vnd.adobe.xdp+xml`。
1. 通过调用对 `ResourceContent` 象“s”方 `Resource` 法并传递对象，将对 `Resource` 象的内 `setContent` 容添加到对 `ResourceContent` 象。
1. 通过调用对象“s”方法并传递 `Resource` 表示资源 `setDescription` 描述的字符串值，添加资源的描述。
1. 通过调用对象的方法并传递以下值，将表 `ResourceRepositoryClient` 单设计添 `writeResource` 加到存储库中：

   * 一个字符串值，它指定包含新资源的资源集合的路径
   * 创 `Resource` 建的对象

**另请参阅**

[快速开始（EJB模式）:使用Java API编写资源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[使用Java API调用AEM Forms](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## 使用调用API调用短时间进程 {#invoking-a-short-lived-process-using-the-invocation-api}

您可以使用Java调用API调用短时间进程。 使用调用API调用短时间进程时，可使用对象传递所需的参 `java.util.HashMap` 数值。 对于要传递到服务的每个参数，调用对象的方 `java.util.HashMap``put` 法并指定服务所需的名称——值对，以执行指定的操作。 指定属于短期进程的参数的确切名称。

>[!NOTE]
>
>有关调用长寿命进程的信息，请参 [阅调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

此处讨论的内容是使用调用API调用以下名为的AEM Forms短期进程 `MyApplication/EncryptDocument`。

>[!NOTE]
>
>此过程不基于现有的AEM Forms流程。 要跟随代码示例，请使用Workbench创建一个名为的 `MyApplication/EncryptDocument` 进程。 (请参 [阅使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

调用此进程时，它将执行以下操作：

1. 获取传递给该流程的不安全的PDF文档。 此操作基于操 `SetValue` 作。 此进程的输入参数是一个名为的 `document` 进程变量 `inDoc`。
1. 使用密码加密PDF文档。 此操作基于操 `PasswordEncryptPDF` 作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`。

### 使用Java调用API调用MyApplication/EncryptDocument短时进程 {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

使用 `MyApplication/EncryptDocument` Java调用API调用短期进程：

1. 在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。 (请参 [阅包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)
1. 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](invoking-aem-forms-using-java.md#setting-connection-properties)。)
1. 使用对 `ServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。 对象 `ServiceClient` 允许您调用服务操作。 它处理诸如查找、调度和路由调用请求等任务。
1. 使用对 `java.util.HashMap` 象的构造函数创建对象。
1. 为每个输 `java.util.HashMap` 入参数调 `put` 用对象的方法，以传递到长寿命进程。 由于短 `MyApplication/EncryptDocument` 期进程需要一个类型的输入参数 `Document`，您只需调用一次方法， `put` 如下例所示。

   ```as3
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. 通过调 `InvocationRequest` 用对象的方法并 `ServiceClientFactory` 传递以 `createInvocationRequest` 下值来创建对象：

   * 一个字符串值，它指定要调用的长寿命进程的名称。 要调用该 `MyApplication/EncryptDocument` 进程，请指定 `MyApplication/EncryptDocument`。
   * 表示进程操作名称的字符串值。 通常，短期进程操作的名称是 `invoke`。
   * 包 `java.util.HashMap` 含服务操作所需的参数值的对象。
   * 一个布尔值，它指 `true`定创建同步请求（此值适用于调用短时间进程）。

1. 通过调用对象的方法并传递对象，将调 `ServiceClient` 用请求发 `invoke` 送到服务 `InvocationRequest` 中。 该方 `invoke` 法返回一个 `InvocationReponse` 对象。

   >[!NOTE]
   >
   >通过传递值作为方法的第四个参数，可以调 `false`用一个长寿命的过 `createInvocationRequest` 程。 传递该值会 `false`*创建异步请求。*

1. 通过调用对象的方法并传递指定输 `InvocationReponse` 出参数名 `getOutputParameter` 称的字符串值，检索进程的返回值。 在这种情况下， `outDoc` 请指 `outDoc` 定(进程的输出参数的名 `MyApplication/EncryptDocument` 称)。 将返回值转 `Document`换为，如下例所示。

   ```as3
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
1. 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复 `com.adobe.idp.Document` 制到文件。 确保使用由 `com.adobe.idp.Document` 该方法返回的对 `getOutputParameter` 象。

**另请参阅**

[快速开始:使用调用API调用短时间进程](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[调用以人为中心的长寿命进程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[包括AEM Forms Java库文件](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)