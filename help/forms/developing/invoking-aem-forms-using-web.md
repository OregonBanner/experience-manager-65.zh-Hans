---
title: 使用Web服务调用AEM Forms
description: 使用Web服务调用AEM Forms进程，并完全支持WSDL生成。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 3139564f-9346-4933-8e39-2e1642bff097
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '9887'
ht-degree: 0%

---

# 使用Web服务调用AEM Forms {#invoking-aem-forms-using-web-services}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

服务容器中的大多数AEM Forms服务都配置为公开Web服务，完全支持Web服务定义语言(WSDL)的生成。 即，您可以创建使用AEM Forms服务的本机SOAP栈栈的代理对象。 因此，AEM Forms服务可以交换和处理以下SOAP消息：

* **SOAP请求**：由请求操作的客户端应用程序发送到Forms服务。
* **SOAP响应**：在处理SOAP请求后，由Forms服务发送到客户端应用程序。

使用Web服务，您可以执行与使用Java API执行的AEM Forms服务操作相同的操作。 使用Web服务调用AEM Forms服务的好处是，您可以在支持SOAP的开发环境中创建客户端应用程序。 客户端应用程序未绑定到特定的开发环境或编程语言。 例如，您可以使用Microsoft Visual Studio .NET和C#作为编程语言来创建客户端应用程序。

AEM Forms服务通过SOAP协议公开，并符合WSI Basic Profile 1.1。 Web服务互操作性(Web Services Interoperability， WSI)是一个开放式标准组织，旨在促进跨平台的Web服务互操作性。 有关信息，请参阅 [https://www.ws-i.org/](https://www.ws-i.org).

AEM Forms支持以下Web服务标准：

* **编码**：仅支持文档和文本编码（根据WSI基本配置文件，这是首选编码）。 (请参阅 [使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**：表示一种使用SOAP请求编码附件的方法。 (请参阅 [使用MTOM调用AEM Forms](#invoking-aem-forms-using-mtom).)
* **SwaRef**：表示使用SOAP请求编码附件的另一种方法。 (请参阅 [使用SwaRef调用AEM Forms](#invoking-aem-forms-using-swaref).)
* **带有附件的SOAP**：支持MIME和DIME(Direct Internet Message Encapsulation)。 这些协议是通过SOAP发送附件的标准方法。 Microsoft Visual Studio .NET应用程序使用DIME。 (请参阅 [使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**：支持用户名密码令牌配置文件，这是作为WS安全SOAP标头的一部分发送用户名和密码的标准方法。 AEM Forms还支持HTTP基本身份验证。 s

要使用Web服务调用AEM Forms服务，通常需要创建一个使用服务WSDL的代理库。 此 *使用Web服务调用AEM Forms* 部分使用JAX-WS创建Java代理类来调用服务。 (请参阅 [使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws).)

您可以通过指定以下URL定义来检索服务WDSL（括号中的项是可选的）：

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

其中：

* *your_serverhost* 表示托管AEM Forms的J2EE应用程序服务器的IP地址。
* *your_port* 表示J2EE应用程序服务器使用的HTTP端口。
* *service_name* 表示服务名称。
* *版本* 表示服务的目标版本（默认情况下使用最新的服务版本）。
* `async` 指定值 `true` 要为异步调用启用其他操作( `false` 默认情况下)。
* *lc_version* 表示要调用的AEM Forms版本。

下表列出了服务WSDL定义(假设AEM Forms部署在本地主机上并且帖子为8080)。

<table>
 <thead>
  <tr>
   <th><p>服务</p></th>
   <th><p>WSDL定义</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>汇编程序</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>备份和恢复</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>条形码表单</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>转换PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>docconverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>文档管理</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>加密 </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Forms</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>表单数据集成</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>生成PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>生成3DPDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>输出</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF实用工具 </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Acrobat Reader DC扩展</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>存储库</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>签名 </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>XMP实用程序</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**AEM Forms流程WSDL定义**

在WSDL定义中指定应用程序名称和进程名称，以访问属于在Workbench中创建的进程的WSDL。 假定应用程序的名称为 `MyApplication` 进程名称为 `EncryptDocument`. 在这种情况下，请指定以下WSDL定义：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>有关示例的信息 `MyApplication/EncryptDocument` 短期进程，请参见 [短期进程示例](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>应用程序可以包含文件夹。 在这种情况下，请在WSDL定义中指定文件夹名称：

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**使用Web服务访问新功能**

可使用Web服务访问新的AEM Forms服务功能。 例如，在AEM Forms中，引入了使用MTOM对附件进行编码的功能。 (请参阅 [使用MTOM调用AEM Forms](#invoking-aem-forms-using-mtom).)

要访问AEM Forms中引入的新功能，请指定 `lc_version` WSDL定义中的属性。 例如，要访问新的服务功能（包括MTOM支持），请指定以下WSDL定义：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>设置 `lc_version` 属性，确保使用三位数。 例如，9.0.1等于版本9.0。

**Web服务BLOB数据类型**

AEM Forms服务WSDL定义了多种数据类型。 Web服务中公开的最重要数据类型之一是 `BLOB` 类型。 此数据类型映射到 `com.adobe.idp.Document` 类在使用AEM Forms Java API时。 (请参阅 [使用Java API将数据传递到AEM Forms服务](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

A `BLOB` 对象向和从AEM Forms服务发送和检索二进制数据(例如，PDF文件、XML数据等)。 此 `BLOB` 类型在服务WSDL中定义如下：

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

此 `MTOM` 和 `swaRef` 仅在AEM Forms中支持字段。 只有在指定的URL中包含 `lc_version` 属性。

**在服务请求中提供BLOB对象**

如果AEM Forms服务操作需要 `BLOB` 键入作为输入值，创建 `BLOB` 键入应用程序逻辑。 (许多Web服务快速启动于 *使用AEM表单编程* 显示如何使用BLOB数据类型。)

将值分配给属于 `BLOB` 实例如下所示：

* **比值64**：要以Base64格式编码的文本形式传递数据，请在文档的 `BLOB.binaryData` 字段并设置MIME格式的数据类型(例如 `application/pdf`) `BLOB.contentType` 字段。 (请参阅 [使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**：要在MTOM附件中传递二进制数据，请在 `BLOB.MTOM` 字段。 此设置使用Java JAX-WS框架或SOAP框架的本机API将数据附加到SOAP请求。 (请参阅 [使用MTOM调用AEM Forms](#invoking-aem-forms-using-mtom).)
* **SwaRef**：要在WS-I SwaRef附件中传递二进制数据，请在 `BLOB.swaRef` 字段。 此设置使用Java JAX-WS框架将数据附加到SOAP请求。 (请参阅 [使用SwaRef调用AEM Forms](#invoking-aem-forms-using-swaref).)
* **MIME或DIME附件**：要在MIME或DIME附件中传递数据，请使用SOAP框架的本机API将数据附加到SOAP请求。 在中设置附件标识符 `BLOB.attachmentID` 字段。 (请参阅 [使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding).)
* **远程URL**：如果数据托管在Web服务器上并可通过HTTP URL访问，则在 `BLOB.remoteURL` 字段。 (请参阅 [通过HTTP使用BLOB数据调用AEM Forms](#invoking-aem-forms-using-blob-data-over-http).)

**访问从服务返回的BLOB对象中的数据**

返回的传输协议 `BLOB` 对象取决于多个因素，这些因素按照以下顺序考虑，当满足主要条件时停止：

1. **目标URL指定传输协议**. 如果在SOAP调用中指定的目标URL包含参数 `blob="`*BLOB类型*“，则 *BLOB类型* 确定传输协议。 *BLOB类型* 是base64、dime、mime、http、mtom或swaref的占位符。
1. **服务SOAP终结点是智能的**. 如果满足以下条件，则使用与输入文档相同的传输协议返回输出文档：

   * 服务的SOAP端点参数“输出Blob对象的默认协议”设置为“智能”。

     对于具有SOAP端点的每个服务，管理控制台允许您为任何返回的blob指定传输协议。 (请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * AEM Forms服务将获取一个或多个文档作为输入。

1. **服务SOAP端点不是智能的**. 所配置的协议确定文档传输协议，并在相应的协议中返回数据 `BLOB` 字段。 例如，如果SOAP端点设置为DIME，则返回的blob位于 `blob.attachmentID` 字段，不考虑任何输入文档的传输协议。
1. **否则**. 如果服务未将文档类型作为输入，则输出文档将返回到 `BLOB.remoteURL` 字段。

如第一个条件中所述，您可以通过扩展带有后缀的SOAP端点URL来确保任何返回文档的传输类型，如下所示：

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

以下是传输类型与从中获取数据的字段之间的相关性：

* **Base64格式**：设置 `blob` 后缀至 `base64` 以返回数据 `BLOB.binaryData` 字段。
* **MIME或DIME附件**：设置 `blob` 后缀至 `DIME` 或 `MIME` 将数据作为对应的附件类型返回，并将中返回的附件标识符作为 `BLOB.attachmentID` 字段。 使用SOAP框架的专有API从附件中读取数据。
* **远程URL**：设置 `blob` 后缀至 `http` 将数据保留在应用程序服务器上，并返回指向 `BLOB.remoteURL` 字段。
* **MTOM或SwaRef**：设置 `blob` 后缀至 `mtom` 或 `swaref` 将数据作为对应的附件类型返回，并将中返回的附件标识符作为 `BLOB.MTOM` 或 `BLOB.swaRef` 字段。 使用SOAP框架的本机API从附件中读取数据。

>[!NOTE]
>
>建议您在填充 `BLOB` 对象(通过调用其 `setBinaryData` 方法。 否则，可能会出现以下情况 `OutOfMemory` 出现异常。

>[!NOTE]
>
>使用MTOM传输协议的基于JAX WS的应用程序被限制为25MB的发送和接收数据。 此限制是由于JAX-WS中的错误所致。 如果发送和接收文件的组合大小超过25MB，请使用SwaRef传输协议，而不是MTOM传输协议。 否则，可能会出现 `OutOfMemory` 例外。

**base64编码的字节数组的MTOM传输**

除了 `BLOB` 对象，MTOM协议支持任何复杂类型的字节数组参数或字节数组字段。 这意味着支持MTOM的客户端SOAP框架可以发送任何 `xsd:base64Binary` 元素作为MTOM附件（而不是base64编码的文本）。 AEM Forms SOAP端点可以读取此类型的字节阵列编码。 但是，AEM Forms服务始终将字节数组类型作为base64编码文本返回。 输出字节数组参数不支持MTOM。

返回大量二进制数据的AEM Forms服务使用Document/BLOB类型，而不是字节数组类型。 文档类型在传输大量数据时更为有效。

## Web服务数据类型 {#web-service-data-types}

下表列出了Java数据类型，并显示了相应的Web服务数据类型。

<table>
 <thead>
  <tr>
   <th><p>Java数据类型</p></th>
   <th><p>Web服务数据类型</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>此 <code>DATE</code> 类型，在服务WSDL中定义如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服务操作需要 <code>java.util.Date</code> 值作为输入，SOAP客户端应用程序必须将日期 <code>DATE.date</code> 字段。 设置 <code>DATE.calendar</code> 字段在此情况下会导致运行时异常。 如果服务返回 <code>java.util.Date</code>，日期将在中返回 <code>DATE.date</code> 字段。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>此 <code>DATE</code> 类型，在服务WSDL中定义如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服务操作需要 <code>java.util.Calendar</code> 值作为输入，SOAP客户端应用程序必须将日期 <code>DATE.caledendar</code> 字段。 设置 <code>DATE.date</code> 字段会导致运行时异常。 如果服务返回 <code>java.util.Calendar</code>，则日期会返回到 <code>DATE.calendar</code> 字段。 </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p>此 <code>apachesoap:Map</code>，在服务WSDL中定义如下：</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>Map表示为键/值对的序列。</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>XML类型，在服务WSDL中定义，如下所示：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服务操作接受 <code>org.w3c.dom.Document</code> 值，将XML数据传递到 <code>XML.document</code> 字段。</p><p>设置 <code>XML.element</code> 字段导致运行时异常。 如果服务返回 <code>org.w3c.dom.Document</code>，则XML数据将在 <code>XML.document</code> 字段。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML类型，在服务WSDL中定义，如下所示：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服务操作需要 <code>org.w3c.dom.Element</code> 作为输入，将XML数据传递到 <code>XML.element</code> 字段。</p><p>设置 <code>XML.document</code> 字段导致运行时异常。 如果服务返回 <code>org.w3c.dom.Element</code>，则XML数据将在 <code>XML.element</code> 字段。</p></td>
  </tr>
 </tbody>
</table>

## 使用JAX-WS创建Java代理类 {#creating-java-proxy-classes-using-jax-ws}

您可以使用JAX-WS将Forms服务WSDL转换为Java代理类。 利用这些类，可调用AEM Forms服务操作。 Apache Ant允许您创建一个生成脚本，该脚本通过引用AEM Forms服务WSDL来生成Java代理类。 可通过执行以下步骤来生成JAX-WS代理文件：

1. 在客户端计算机上安装Apache Ant。 (请参阅 [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * 将bin目录添加到类路径中。
   * 设置 `ANT_HOME` 环境变量到安装Ant的目录。

1. 安装JDK 1.6或更高版本。

   * 将JDK bin目录添加到类路径中。
   * 将JRE bin目录添加到类路径中。 此箱位于 `[JDK_INSTALL_LOCATION]/jre` 目录。
   * 设置 `JAVA_HOME` 环境变量到安装JDK的目录。

   JDK 1.6包括在build.xml文件中使用的wsimport程序。 JDK 1.5不包括该程序。

1. 在客户端计算机上安装JAX-WS。 (请参阅 [适用于XML Web服务的Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. 使用JAX-WS和Apache Ant生成Java代理类。 创建Ant生成脚本以完成此任务。 以下脚本是一个名为build.xml的示例Ant生成脚本：

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   在此Ant生成脚本中，请注意 `url` 属性设置为引用在localhost上运行的加密服务WSDL。 此 `username` 和 `password` 属性必须设置为有效的AEM表单用户名和密码。 请注意，URL包含 `lc_version` 属性。 不指定 `lc_version` 选项，您无法调用新的AEM Forms服务操作。

   >[!NOTE]
   >
   >替换 `EncryptionService`，其中包含您要使用Java代理类调用的AEM Forms服务名称。 例如，要为Rights Management服务创建Java代理类，请指定：

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. 创建BAT文件以执行Ant构建脚本。 以下命令可以位于负责执行Ant构建脚本的BAT文件中：

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   将ANT生成脚本放置到C:\Program Files\Java\jaxws-ri\bin目录中。 脚本将JAVA文件写入。/classes文件夹。 该脚本生成可调用服务的JAVA文件。

1. 将JAVA文件打包到JAR文件中。 如果您在使用Eclipse，请执行以下步骤：

   * 创建一个Java项目，该项目用于将代理JAVA文件打包到JAR文件中。
   * 在项目中创建源文件夹。
   * 创建 `com.adobe.idp.services` 包中。
   * 选择 `com.adobe.idp.services` 包，然后将JAVA文件从adobe/idp/services文件夹导入到包中。
   * 如有必要，请创建 `org/apache/xml/xmlsoap` 包中。
   * 选择源文件夹，然后从org/apache/xml/xmlsoap文件夹导入JAVA文件。
   * 将Java编译器的兼容级别设置为5.0或更高。
   * 生成项目。
   * 将项目导出为JAR文件。
   * 在客户端项目的类路径中导入此JAR文件。 此外，还将所有JAR文件导入 &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.

   >[!NOTE]
   >
   >使用AEM窗体编程中的所有Java Web服务快速启动(Forms服务除外)使用JAX-WS创建Java代理文件。 此外，所有Java Web服务都快速启动，使用SwaRef。 (请参阅 [使用SwaRef调用AEM Forms](#invoking-aem-forms-using-swaref).)

**另请参阅**

[使用Apache Axis创建Java代理类](#creating-java-proxy-classes-using-apache-axis)

[使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[通过HTTP使用BLOB数据调用AEM Forms](#invoking-aem-forms-using-blob-data-over-http)

[使用SwaRef调用AEM Forms](#invoking-aem-forms-using-swaref)

## 使用Apache Axis创建Java代理类 {#creating-java-proxy-classes-using-apache-axis}

您可以使用Apache Axis WSDL2Java工具将Forms服务转换为Java代理类。 利用这些类，可调用Forms服务操作。 使用Apache Ant，您可以从服务WSDL生成Axis库文件。 您可以通过URL下载Apache Axis [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>与Forms服务关联的Web服务快速启动使用使用Apache Axis创建的Java代理类。 Forms Web服务快速启动还使用Base64作为编码类型。 (请参阅 [Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

可通过执行以下步骤来生成Axis Java库文件：

1. 在客户端计算机上安装Apache Ant。 它位于 [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * 将bin目录添加到类路径中。
   * 设置 `ANT_HOME` 环境变量到安装Ant的目录。

1. 在客户端计算机上安装Apache Axis 1.4。 它位于 [https://ws.apache.org/axis/](https://ws.apache.org/axis/).
1. 设置类路径以在Web服务客户端中使用Axis JAR文件，如以下位置的Axis安装说明中所述 [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. 使用Axis中的Apache WSDL2Java工具生成Java代理类。 创建Ant生成脚本以完成此任务。 以下脚本是一个名为build.xml的示例Ant生成脚本：

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   在此Ant生成脚本中，请注意 `url` 属性设置为引用在localhost上运行的加密服务WSDL。 此 `username` 和 `password` 属性必须设置为有效的AEM表单用户名和密码。

1. 创建BAT文件以执行Ant构建脚本。 以下命令可以位于负责执行Ant构建脚本的BAT文件中：

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA文件将写入C:\JavaFiles文件夹，该文件夹由 `output` 属性。 要成功调用Forms服务，请将这些JAVA文件导入类路径中。

   默认情况下，这些文件属于名为的Java包 `com.adobe.idp.services`. 建议将这些JAVA文件放入JAR文件中。 然后将JAR文件导入到客户端应用程序的类路径中。

   >[!NOTE]
   >
   >有多种不同的方法可将.JAVA文件放入JAR中。 一种方法是使用Java IDE，如Eclipse。 创建Java项目并创建 `com.adobe.idp.services`包（所有.JAVA文件都属于此包）。 接下来，将所有.JAVA文件导入到包中。 最后，将项目导出为JAR文件。

1. 修改URL `EncryptionServiceLocator` 类指定编码类型。 例如，要使用base64，请指定 `?blob=base64` 以确保 `BLOB` 对象返回二进制数据。 也就是说，在 `EncryptionServiceLocator` 类中，找到以下代码行：

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   并将其更改为：

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. 将以下Axis JAR文件添加到Java项目的类路径中：

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   这些JAR文件位于 `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` 目录。

**另请参阅**

[使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws)

[使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[通过HTTP使用BLOB数据调用AEM Forms](#invoking-aem-forms-using-blob-data-over-http)

## 使用Base64编码调用AEM Forms {#invoking-aem-forms-using-base64-encoding}

您可以使用Base64编码调用AEM Forms服务。 Base64编码会对随Web服务调用请求发送的附件进行编码。 那就是， `BLOB` 数据采用Base64编码，而不是整个SOAP消息。

“使用Base64编码调用AEM Forms”中讨论了调用以下AEM Forms短期进程： `MyApplication/EncryptDocument` 使用Base64编码。

>[!NOTE]
>
>此流程并非基于现有的AEM Forms流程。 要遵循代码示例，请创建一个名为的进程 `MyApplication/EncryptDocument` 使用Workbench。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

调用此进程时，将执行以下操作：

1. 获取传递到进程的不安全PDF文档。 此操作基于 `SetValue` 操作。 此进程的输入参数为 `document` 进程变量已命名 `inDoc`.
1. 使用密码加密PDF文档。 此操作基于 `PasswordEncryptPDF` 操作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`.

### 创建使用Base64编码的.NET客户端程序集 {#creating-a-net-client-assembly-that-uses-base64-encoding}

您可以创建一个.NET客户端程序集，以从Microsoft Visual Studio .NET项目调用Forms服务。 要创建使用base64编码的.NET客户端程序集，请执行以下步骤：

1. 根据AEM Forms调用URL创建代理类。
1. 创建生成.NET客户端程序集的Microsoft Visual Studio .NET项目。

**创建代理类**

可以使用随Microsoft Visual Studio提供的工具创建一个用于创建.NET客户端程序集的代理类。 该工具的名称为wsdl.exe，位于Microsoft Visual Studio安装文件夹中。 要创建代理类，请打开命令提示符并导航到包含wsdl.exe文件的文件夹。 有关wsdl.exe工具的更多信息，请参见 *MSDN帮助*.

在命令提示符下输入以下命令：

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

默认情况下，此工具会在基于WSDL名称的同一文件夹中创建一个CS文件。 在这种情况下，会创建一个名为的CS文件 *EncryptDocumentService.cs*. 您可以使用此CS文件创建一个代理对象，以便调用调用URL中指定的服务。

修改proxy类中的URL以包含 `?blob=base64` 以确保 `BLOB` 对象返回二进制数据。 在proxy类中，找到以下代码行：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

并将其更改为：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

此 *使用Base64编码调用AEM Forms* 区域使用 `MyApplication/EncryptDocument` 举个例子。 如果要为其他Forms服务创建.NET客户端程序集，请确保将 `MyApplication/EncryptDocument` 服务的名称。

**开发.NET客户端程序集**

创建生成.NET客户端程序集的Visual Studio类库项目。 您使用wsdl.exe创建的CS文件可以导入此项目中。 此项目会生成一个DLL文件（.NET客户端程序集），您可以在其他Visual Studio .NET项目中使用它来调用服务。

1. 启动Microsoft Visual Studio .NET。
1. 创建类库项目并将其命名为DocumentService。
1. 导入使用wsdl.exe创建的CS文件。
1. 在 **项目** 菜单，选择 **添加引用**.
1. 在“添加参照”对话框中，选择 **System.Web.Services.dll**.
1. 单击 **选择** 然后单击 **确定**.
1. 编译和构建项目。

>[!NOTE]
>
>此过程创建一个名为DocumentService.dll的.NET客户端程序集，您可以使用它将SOAP请求发送到 `MyApplication/EncryptDocument` 服务。

>[!NOTE]
>
>确保您已添加 `?blob=base64` 到代理类中用于创建.NET客户端程序集的URL。 否则，您将无法从检索二进制数据 `BLOB` 对象。

**引用.NET客户端程序集**

将新创建的.NET客户端程序集放在您正在开发客户端应用程序的计算机上。 将.NET客户机程序集放置到目录后，可以从项目中引用它。 另请参考 `System.Web.Services` 库。 如果不引用此库，则无法使用.NET客户端程序集调用服务。

1. 在 **项目** 菜单，选择 **添加引用**.
1. 单击 **.NET** 选项卡。
1. 单击 **浏览** 并找到DocumentService.dll文件。
1. 单击 **选择** 然后单击 **确定**.

**使用使用Base64编码的.NET客户端程序集调用服务**

您可以调用 `MyApplication/EncryptDocument` 服务（在Workbench中构建），使用使用Base64编码的.NET客户端程序集。 要调用 `MyApplication/EncryptDocument` 服务，请执行以下步骤：

1. Microsoft创建一个使用 `MyApplication/EncryptDocument` 服务WSDL。
1. 创建客户端Microsoft .NET项目。 在客户端项目中引用Microsoft .NET客户端程序集。 另请参阅 `System.Web.Services`.
1. 使用Microsoft .NET客户端程序集，创建 `MyApplication_EncryptDocumentService` 对象。
1. 设置 `MyApplication_EncryptDocumentService` 对象的 `Credentials` 属性带有 `System.Net.NetworkCredential` 对象。 在 `System.Net.NetworkCredential` 构造函数，指定AEM forms用户名和相应密码。 设置身份验证值以使.NET客户端应用程序能够与AEM Forms成功交换SOAP消息。
1. 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储传递给的PDF文档 `MyApplication/EncryptDocument` 进程。
1. 创建 `System.IO.FileStream` 对象通过调用其构造函数。 传递一个字符串值，该值表示PDF文档的文件位置以及打开文件的模式。
1. 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
1. 通过调用 `System.IO.FileStream` 对象的 `Read` 方法。 传递字节数组、起始位置和要读取的流长度。
1. 填充 `BLOB` 对象，通过指定其 `binaryData` 属性与字节数组的内容。
1. 调用 `MyApplication/EncryptDocument` 通过调用 `MyApplication_EncryptDocumentService` 对象的 `invoke` 方法和传递 `BLOB` 包含PDF文档的对象。 此过程会返回PDF文档在 `BLOB` 对象。
1. 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值表示密码加密文档的文件位置。
1. 创建一个字节数组，用于存储 `BLOB` 返回的对象 `MyApplicationEncryptDocumentService` 对象的 `invoke` 方法。 通过获取的值，填充字节数组 `BLOB` 对象的 `binaryData` 数据成员。
1. 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
1. PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

### 使用Java代理类和Base64编码调用服务 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

您可以使用Java代理类和Base64调用AEM Forms服务。 要调用 `MyApplication/EncryptDocument` 服务使用Java代理类，请执行以下步骤：

1. 使用JAX-WS创建使用 `MyApplication/EncryptDocument` 服务WSDL。 使用以下WSDL端点：

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >替换 `hiro-xp` *包含托管AEM Forms的J2EE应用程序服务器的IP地址。*

1. 将使用JAX-WS创建的Java代理类打包到JAR文件中。
1. 在以下路径中包含Java代理JAR文件和JAR文件：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客户端项目的类路径中。

1. 创建 `MyApplicationEncryptDocumentService` 对象。
1. 创建 `MyApplicationEncryptDocument` 对象，方法是调用 `MyApplicationEncryptDocumentService` 对象的 `getEncryptDocument` 方法。
1. 通过为以下数据成员分配值，设置调用AEM Forms所需的连接值：

   * 将WSDL端点和编码类型分配给 `javax.xml.ws.BindingProvider` 对象的 `ENDPOINT_ADDRESS_PROPERTY` 字段。 要调用 `MyApplication/EncryptDocument` 服务使用Base64编码，请指定以下URL值：

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * 将AEM Forms用户分配给 `javax.xml.ws.BindingProvider` 对象的 `USERNAME_PROPERTY` 字段。
   * 将相应的密码值分配给 `javax.xml.ws.BindingProvider` 对象的 `PASSWORD_PROPERTY` 字段。

   以下代码示例显示了此应用程序逻辑：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 检索要发送给的PDF文档 `MyApplication/EncryptDocument` 通过创建 `java.io.FileInputStream` 对象。 传递一个指定PDF文档位置的字符串值。
1. 创建字节数组，然后使用 `java.io.FileInputStream` 对象。
1. 创建 `BLOB` 对象。
1. 填充 `BLOB` 对象(通过调用其 `setBinaryData` 和传递字节数组。 此 `BLOB` 对象的 `setBinaryData` 是使用Base64编码时要调用的方法。 请参阅在服务请求中提供BLOB对象。
1. 调用 `MyApplication/EncryptDocument` 通过调用 `MyApplicationEncryptDocument` 对象的 `invoke` 方法。 传递 `BLOB` 包含PDF文档的对象。 调用方法返回 `BLOB` 包含加密PDF文档的对象。
1. PDF通过调用 `BLOB` 对象的 `getBinaryData` 方法。
1. 将加密的PDF文档另存为PDF文件。 将字节数组写入文件。

**另请参阅**

[快速入门：使用Java代理文件和Base64编码调用服务](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](#creating-a-net-client-assembly-that-uses-base64-encoding)

## 使用MTOM调用AEM Forms {#invoking-aem-forms-using-mtom}

您可以使用Web服务标准MTOM调用AEM Forms服务。 该标准定义如何通过Internet或Intranet传输二进制数据，如PDF文档。 MTOM的一个功能是使用 `XOP:Include` 元素。 此元素在XML二进制优化打包(XOP)规范中定义，以引用SOAP消息的二进制附件。

此处的讨论是关于使用MTOM调用以下名为的AEM Forms短期进程 `MyApplication/EncryptDocument`.

>[!NOTE]
>
>此流程并非基于现有的AEM Forms流程。 要遵循代码示例，请创建一个名为的进程 `MyApplication/EncryptDocument` 使用Workbench。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

调用此进程时，将执行以下操作：

1. 获取传递到进程的不安全PDF文档。 此操作基于 `SetValue` 操作。 此进程的输入参数为 `document` 进程变量已命名 `inDoc`.
1. 使用密码加密PDF文档。 此操作基于 `PasswordEncryptPDF` 操作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`.

>[!NOTE]
>
>AEM Forms版本9中添加了MTOM支持。

>[!NOTE]
>
>使用MTOM传输协议的基于JAX WS的应用程序被限制为25MB的发送和接收数据。 此限制是由于JAX-WS中的错误所致。 如果发送和接收文件的组合大小超过25MB，请使用SwaRef传输协议，而不是MTOM传输协议。 否则，可能会出现 `OutOfMemory` 例外。

此处的讨论是关于在Microsoft .NET项目中使用MTOM来调用AEM Forms服务。 使用的.NET Framework为3.5，开发环境为Visual Studio 2008。 如果您的开发计算机上安装了Web服务增强功能(WSE)，请将其删除。 .NET 3.5框架支持名为Windows Communication Foundation (WCF)的SOAP框架。 使用MTOM调用AEM Forms时，仅支持WCF（不支持WSE）。

### 创建使用MTOM调用服务的.NET项目 {#creating-a-net-project-that-invokes-a-service-using-mtom}

您可以创建一个Microsoft .NET项目，该项目可以使用Web服务调用AEM Forms服务。 首先，使用Visual Studio 2008创建一个Microsoft .NET项目。 要调用AEM Forms服务，请创建要在项目中调用的AEM Forms服务的服务引用。 在创建服务引用时，请指定指向AEM Forms服务的URL：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

替换 `localhost` ，其中包含托管AEM Forms的J2EE应用程序服务器的IP地址。 替换 `MyApplication/EncryptDocument` 要调用的AEM Forms服务的名称。 例如，要调用Rights Management操作，请指定：

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

此 `lc_version` 选项可确保AEM Forms功能（如MTOM）可用。 不指定 `lc_version` 选项，您无法使用MTOM调用AEM Forms。

创建服务引用后，与AEM Forms服务关联的数据类型便可在.NET项目中使用。 要创建调用AEM Forms服务的.NET项目，请执行以下步骤：

1. 使用Microsoft Visual Studio 2008创建.NET项目。
1. 在 **项目** 菜单，选择 **添加服务引用**.
1. 在 **地址** 对话框中，指定AEM Forms服务的WSDL。 例如，

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. 单击 **开始** 然后单击 **确定**.

### 在.NET项目中使用MTOM调用服务 {#invoking-a-service-using-mtom-in-a-net-project}

考虑 `MyApplication/EncryptDocument` 接受不安全的PDF文档并返回密码加密的PDF文档的进程。 要调用 `MyApplication/EncryptDocument` 通过使用MTOM进行处理（内建于Workbench中），请执行以下步骤：

1. 创建一个Microsoft .NET项目。
1. 创建 `MyApplication_EncryptDocumentClient` 对象使用默认构造函数。
1. 创建 `MyApplication_EncryptDocumentClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务和编码类型：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请确保您指定 `?blob=mtom`.

   >[!NOTE]
   >
   >替换 `hiro-xp` *包含托管AEM Forms的J2EE应用程序服务器的IP地址。*

1. 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `EncryptDocumentClient.Endpoint.Binding` 数据成员。 将返回值强制转换为 `BasicHttpBinding`.
1. 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 数据成员至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
1. 通过执行以下任务启用基本HTTP身份验证：

   * 将AEM表单用户名分配给数据成员 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * 将相应的密码值分配给数据成员 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * 分配常量值 `HttpClientCredentialType.Basic` 至数据成员 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 至数据成员 `BasicHttpBindingSecurity.Security.Mode`.

   以下代码示例显示了这些任务。

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. 创建 `BLOB` 对象。 此 `BLOB` PDF对象用于存储要传递给 `MyApplication/EncryptDocument` 进程。
1. 创建 `System.IO.FileStream` 对象通过调用其构造函数。 传递一个字符串值，该值表示PDF文档的文件位置以及打开文件的模式。
1. 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
1. 通过调用 `System.IO.FileStream` 对象的 `Read` 方法。 传递字节数组、起始位置和要读取的流长度。
1. 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的数据成员。
1. 调用 `MyApplication/EncryptDocument` 通过调用 `MyApplication_EncryptDocumentClient` 对象的 `invoke` 方法。 传递 `BLOB` 包含PDF文档的对象。 此过程会返回PDF文档在 `BLOB` 对象。
1. 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个表示受保护PDF文档的文件位置的字符串值。
1. 创建一个字节数组，用于存储 `BLOB` 返回的对象 `invoke` 方法。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
1. 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
1. PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

>[!NOTE]
>
>大多数AEM Forms服务操作都有MTOM快速入门。 您可以在服务的相应快速入门部分中查看这些快速启动。 例如，要查看“输出”快速入门部分，请参阅 [输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**另请参阅**

[快速入门：在.NET项目中使用MTOM调用服务](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[使用Web服务访问多个服务](#accessing-multiple-services-using-web-services)

[创建可调用以人为中心的长期进程的ASP.NET Web应用程序](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## 使用SwaRef调用AEM Forms {#invoking-aem-forms-using-swaref}

您可以使用SwaRef调用AEM Forms服务。 的内容 `wsi:swaRef` XML元素作为附件在SOAP主体中发送，SOAP主体存储对附件的引用。 使用SwaRef调用Forms服务时，请使用Java API for XML Web Services (JAX-WS)创建Java代理类。 (请参阅 [适用于XML Web服务的Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

此处的讨论将调用以下Forms短期进程，该进程名为 `MyApplication/EncryptDocument` 通过使用SwaRef。

>[!NOTE]
>
>此流程并非基于现有的AEM Forms流程。 要遵循代码示例，请创建一个名为的进程 `MyApplication/EncryptDocument` 使用Workbench。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

调用此进程时，将执行以下操作：

1. 获取传递到进程的不安全PDF文档。 此操作基于 `SetValue` 操作。 此进程的输入参数为 `document` 进程变量已命名 `inDoc`.
1. 使用密码加密PDF文档。 此操作基于 `PasswordEncryptPDF` 操作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`.

>[!NOTE]
>
>AEM Forms中添加了SwaRef支持

以下讨论是关于如何在Java客户端应用程序中使用SwaRef调用Forms服务。 Java应用程序使用使用JAX-WS创建的代理类。

### 使用使用SwaRef的JAX-WS库文件调用服务 {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

要调用 `MyApplication/EncryptDocument` 通过使用通过JAX-WS和SwaRef创建的Java代理文件进行处理，请执行以下步骤：

1. 使用JAX-WS创建使用 `MyApplication/EncryptDocument` 服务WSDL。 使用以下WSDL端点：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   有关信息，请参阅 [使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >替换 `hiro-xp` *，其中包含托管AEM Forms的J2EE应用程序服务器的IP地址。*

1. 将使用JAX-WS创建的Java代理类打包到JAR文件中。
1. 在以下路径中包含Java代理JAR文件和JAR文件：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客户端项目的类路径中。

1. 创建 `MyApplicationEncryptDocumentService` 对象。
1. 创建 `MyApplicationEncryptDocument` 对象，方法是调用 `MyApplicationEncryptDocumentService` 对象的 `getEncryptDocument` 方法。
1. 通过为以下数据成员分配值，设置调用AEM Forms所需的连接值：

   * 将WSDL端点和编码类型分配给 `javax.xml.ws.BindingProvider` 对象的 `ENDPOINT_ADDRESS_PROPERTY` 字段。 要调用 `MyApplication/EncryptDocument` 服务使用SwaRef编码，请指定以下URL值：

     ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * 将AEM Forms用户分配给 `javax.xml.ws.BindingProvider` 对象的 `USERNAME_PROPERTY` 字段。
   * 将相应的密码值分配给 `javax.xml.ws.BindingProvider` 对象的 `PASSWORD_PROPERTY` 字段。

   以下代码示例显示了此应用程序逻辑：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 检索要发送给的PDF文档 `MyApplication/EncryptDocument` 通过创建 `java.io.File` 对象。 传递一个指定PDF文档位置的字符串值。
1. 创建 `javax.activation.DataSource` 对象 `FileDataSource` 构造函数。 传递 `java.io.File` 对象。
1. 创建 `javax.activation.DataHandler` 对象，使用它的构造函数传递 `javax.activation.DataSource` 对象。
1. 创建 `BLOB` 对象。
1. 填充 `BLOB` 对象(通过调用其 `setSwaRef` 方法和传递 `javax.activation.DataHandler` 对象。
1. 调用 `MyApplication/EncryptDocument` 通过调用 `MyApplicationEncryptDocument` 对象的 `invoke` 方法和传递 `BLOB` 包含PDF文档的对象。 调用方法返回 `BLOB` 包含加密PDF文档的对象。
1. 填充 `javax.activation.DataHandler` 对象，方法是调用 `BLOB` 对象的 `getSwaRef` 方法。
1. 转换 `javax.activation.DataHandler` 对象到 `java.io.InputSteam` 通过调用 `javax.activation.DataHandler` 对象的 `getInputStream` 方法。
1. 写入 `java.io.InputSteam` 实例到表示加密PDF文档的PDF文件。

>[!NOTE]
>
>大多数AEM Forms服务操作都有一个SwaRef快速入门。 您可以在服务的相应快速入门部分中查看这些快速启动。 例如，要查看“输出”快速入门部分，请参阅 [输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**另请参阅**

[快速入门：在Java项目中使用SwaRef调用服务](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## 通过HTTP使用BLOB数据调用AEM Forms {#invoking-aem-forms-using-blob-data-over-http}

您可以使用Web服务调用AEM Forms服务，并通过HTTP传递BLOB数据。 通过HTTP传递BLOB数据是替代技术，无需使用base64编码、DIME或MIME。 例如，在使用Web服务增强功能3.0（不支持DIME或MIME）的Microsoft .NET项目中，您可以通过HTTP传递数据。 通过HTTP使用BLOB数据时，在调用AEM Forms服务之前会上传输入数据。

“通过HTTP使用BLOB数据调用AEM Forms”讨论了调用以下AEM Forms短期进程： `MyApplication/EncryptDocument` 通过HTTP传递BLOB数据。

>[!NOTE]
>
>此流程并非基于现有的AEM Forms流程。 要遵循代码示例，请创建一个名为的进程 `MyApplication/EncryptDocument` 使用Workbench。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

调用此进程时，将执行以下操作：

1. 获取传递到进程的不安全PDF文档。 此操作基于 `SetValue` 操作。 此进程的输入参数为 `document` 进程变量已命名 `inDoc`.
1. 使用密码加密PDF文档。 此操作基于 `PasswordEncryptPDF` 操作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`.

>[!NOTE]
>
>建议您熟悉使用SOAP调用AEM Forms 。 (请参阅 [使用Web服务调用AEM Forms](#invoking-aem-forms-using-web-services).)

### 创建通过HTTP使用数据的.NET客户端程序集 {#creating-a-net-client-assembly-that-uses-data-over-http}

要创建通过HTTP使用数据的客户端程序集，请按照中指定的过程操作 [使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding). 但是，修改代理类中的URL以包含 `?blob=http` 而不是 `?blob=base64`. 此操作可确保数据通过HTTP进行传递。 在proxy类中，找到以下代码行：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

并将其更改为：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**引用.NET clientMyApplication/EncryptDocument程序集**

将新的.NET客户端程序集放在开发客户端应用程序的计算机上。 将.NET客户机程序集放置到目录后，可以从项目中引用它。 参考 `System.Web.Services` 库。 如果不引用此库，则无法使用.NET客户端程序集调用服务。

1. 在 **项目** 菜单，选择 **添加引用**.
1. 单击 **.NET** 选项卡。
1. 单击 **浏览** 并找到DocumentService.dll文件。
1. 单击 **选择** 然后单击 **确定**.

**使用通过HTTP使用BLOB数据的.NET客户端程序集调用服务**

您可以调用 `MyApplication/EncryptDocument` 服务（在Workbench中构建），使用通过HTTP使用数据的.NET客户端程序集。 要调用 `MyApplication/EncryptDocument` 服务，请执行以下步骤：

1. 创建.NET客户端程序集。
1. 引用Microsoft .NET客户端程序集。 创建客户端Microsoft .NET项目。 在客户端项目中引用Microsoft .NET客户端程序集。 另请参阅 `System.Web.Services`.
1. 使用Microsoft .NET客户端程序集，创建 `MyApplication_EncryptDocumentService` 对象。
1. 设置 `MyApplication_EncryptDocumentService` 对象的 `Credentials` 属性带有 `System.Net.NetworkCredential` 对象。 在 `System.Net.NetworkCredential` 构造函数，指定AEM forms用户名和相应密码。 设置身份验证值以使.NET客户端应用程序能够与AEM Forms成功交换SOAP消息。
1. 创建 `BLOB` 对象。 此 `BLOB` 对象用于将数据传递到 `MyApplication/EncryptDocument` 进程。
1. 将字符串值分配给 `BLOB` 对象的 `remoteURL` 指定要传递给的PDF文档的URI位置的数据成员 `MyApplication/EncryptDocument`服务。
1. 调用 `MyApplication/EncryptDocument` 通过调用 `MyApplication_EncryptDocumentService` 对象的 `invoke` 方法和传递 `BLOB` 对象。 此过程会返回PDF文档在 `BLOB` 对象。
1. 创建 `System.UriBuilder` 对象，方法是使用其构造函数并传递返回的值 `BLOB` 对象的 `remoteURL` 数据成员。
1. 转换 `System.UriBuilder` 对象到 `System.IO.Stream` 对象。 （此列表后面的C#快速入门说明了如何执行此任务。）
1. 创建字节数组，然后使用 `System.IO.Stream` 对象。
1. 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
1. PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

### 通过HTTP使用Java代理类和BLOB数据调用服务 {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

您可以通过HTTP使用Java代理类和BLOB数据调用AEM Forms服务。 要调用 `MyApplication/EncryptDocument` 服务使用Java代理类，请执行以下步骤：

1. 使用JAX-WS创建使用 `MyApplication/EncryptDocument` 服务WSDL。 使用以下WSDL端点：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   有关信息，请参阅 [使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >替换 `hiro-xp` *，其中包含托管AEM Forms的J2EE应用程序服务器的IP地址。*

1. 将使用JAX-WS创建的Java代理类打包到JAR文件中。
1. 在以下路径中包含Java代理JAR文件和JAR文件：

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客户端项目的类路径中。

1. 创建 `MyApplicationEncryptDocumentService` 对象。
1. 创建 `MyApplicationEncryptDocument` 对象，方法是调用 `MyApplicationEncryptDocumentService` 对象的 `getEncryptDocument` 方法。
1. 通过为以下数据成员分配值，设置调用AEM Forms所需的连接值：

   * 将WSDL端点和编码类型分配给 `javax.xml.ws.BindingProvider` 对象的 `ENDPOINT_ADDRESS_PROPERTY` 字段。 要调用 `MyApplication/EncryptDocument` 服务使用BLOB over HTTP编码，请指定以下URL值：

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * 将AEM Forms用户分配给 `javax.xml.ws.BindingProvider` 对象的 `USERNAME_PROPERTY` 字段。
   * 将相应的密码值分配给 `javax.xml.ws.BindingProvider` 对象的 `PASSWORD_PROPERTY` 字段。

   以下代码示例显示了此应用程序逻辑：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 创建 `BLOB` 对象。
1. 填充 `BLOB` 对象(通过调用其 `setRemoteURL` 方法。 传递一个字符串值，该值指定要传递给的PDF文档的URI位置 `MyApplication/EncryptDocument` 服务。
1. 调用 `MyApplication/EncryptDocument` 通过调用 `MyApplicationEncryptDocument` 对象的 `invoke` 方法和传递 `BLOB` 包含PDF文档的对象。 此过程会返回PDF文档在 `BLOB` 对象。
1. 创建字节数组以存储表示加密PDF文档的数据流。 调用 `BLOB` 对象的 `getRemoteURL` 方法(使用 `BLOB` 返回的对象 `invoke` 方法)。
1. 创建 `java.io.File` 对象。 此对象表示加密的PDF文档。
1. 创建 `java.io.FileOutputStream` 对象，使用它的构造函数传递 `java.io.File` 对象。
1. 调用 `java.io.FileOutputStream` 对象的 `write` 方法。 传递包含表示加密PDF文档的数据流的字节数组。

## 使用DIME调用AEM Forms {#invoking-aem-forms-using-dime}

您可以使用带有附件的SOAP调用AEM Forms服务。 AEM Forms支持MIME和DIME Web服务标准。 DIME允许您发送二进制附件(如PDF文档)以及调用请求，而不是对附件进行编码。 此 *使用DIME调用AEM Forms* 部分将讨论调用以下AEM Forms短期进程： `MyApplication/EncryptDocument` 用DIME。

调用此进程时，将执行以下操作：

1. 获取传递到进程的不安全PDF文档。 此操作基于 `SetValue` 操作。 此进程的输入参数为 `document` 进程变量已命名 `inDoc`.
1. 使用密码加密PDF文档。 此操作基于 `PasswordEncryptPDF` 操作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`.

此流程并非基于现有的AEM Forms流程。 要遵循代码示例中的说明，请创建一个名为的进程 `MyApplication/EncryptDocument` 使用Workbench。 (请参阅 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>不建议使用DIME调用AEM Forms服务操作。 建议您使用MTOM。 (请参阅 [使用MTOM调用AEM Forms](#invoking-aem-forms-using-mtom).)

### 创建使用DIME的.NET项目 {#creating-a-net-project-that-uses-dime}

要创建可使用DIME调用Forms服务的.NET项目，请执行以下任务：

* 在开发计算机上安装Web服务增强功能2.0。
* 在.NET项目中，创建对FormsAEM Forms服务的Web引用。

**安装Web服务增强功能2.0**

在开发计算机上安装Web服务增强功能2.0，并将其与Microsoft Visual Studio .NET集成。 您可以从以下位置下载Web服务增强功能2.0： [Microsoft下载中心。](https://www.microsoft.com/downloads/search.aspx)

在此网页中，搜索Web服务增强功能2.0并将其下载到开发计算机上。 此下载文件会将名为Microsoft WSE 2.0 SPI.msi的文件放置到您的计算机上。 运行安装程序并按照联机说明进行操作。

>[!NOTE]
>
>Web服务增强功能2.0支持DIME。 使用Web服务增强功能2.0时，支持的Microsoft Visual Studio版本是2003。Web服务增强功能3.0不支持DIME；但是，它支持MTOM。

**创建对AEM Forms服务的Web引用**

在开发计算机上安装Web服务增强功能2.0并创建Microsoft .NET项目后，请创建对Forms服务的Web引用。 例如，要创建Web引用 `MyApplication/EncryptDocument` 进程并假定本地计算机上安装了Forms，请指定以下URL：

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

创建Web引用后，可以在.NET项目中使用以下两种代理数据类型： `EncryptDocumentService` 和 `EncryptDocumentServiceWse`. 要调用 `MyApplication/EncryptDocument` 使用DIME处理，使用 `EncryptDocumentServiceWse` 类型。

>[!NOTE]
>
>在创建对Forms服务的Web引用之前，请确保在项目中引用Web服务增强功能2.0。 （请参阅“安装Web服务增强功能2.0”。）

**引用WSE库**

1. 在“项目”菜单中，选择“添加引用”。
1. 在“添加引用”对话框中，选择Microsoft.Web.Services2.dll。
1. 选择System.Web.Services.dll。
1. 单击“Select（选择）” ，然后单击“OK（确定）”。

**创建Forms服务的Web引用**

1. 在“项目”菜单中，选择“添加Web引用”。
1. 在URL对话框中，指定Forms服务的URL。
1. 单击“开始”，然后单击“添加参照”。

>[!NOTE]
>
>确保启用.NET项目以使用WSE库。 在项目资源管理器中，右键单击项目名称并选择启用WSE 2.0。确保已选中出现的对话框上的复选框。

**在.NET项目中使用DIME调用服务**

您可以使用DIME调用Forms服务。 考虑 `MyApplication/EncryptDocument` 接受不安全的PDF文档并返回密码加密的PDF文档的进程。 要调用 `MyApplication/EncryptDocument` 使用DIME处理，请执行以下步骤：

1. 创建一个Microsoft .NET项目，该项目使您能够使用DIME调用Forms服务。 确保包含Web服务增强功能2.0并创建对AEM Forms服务的Web引用。
1. 在设置Web引用之后， `MyApplication/EncryptDocument` 流程，创建 `EncryptDocumentServiceWse` 对象使用默认构造函数。
1. 设置 `EncryptDocumentServiceWse` 对象的 `Credentials` 具有的数据成员 `System.Net.NetworkCredential` 值，指定AEM表单的用户名和密码值。
1. 创建 `Microsoft.Web.Services2.Dime.DimeAttachment` 对象，方法是使用其构造函数并传递以下值：

   * 指定GUID值的字符串值。 您可以通过调用 `System.Guid.NewGuid.ToString` 方法。
   * 一个字符串值，它指定内容类型。 由于此过程需要PDF文档，请指定 `application/pdf`.
   * A `TypeFormat` 枚举值。 指定 `TypeFormat.MediaType`.
   * 一个字符串值，它指定要传递到AEM Forms进程的PDF文档的位置。

1. 创建 `BLOB` 对象。
1. 将DIME附件添加到 `BLOB` 对象，方法是 `Microsoft.Web.Services2.Dime.DimeAttachment` 对象的 `Id` 数据成员值到 `BLOB` 对象的 `attachmentID` 数据成员。
1. 调用 `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` 方法并传递 `Microsoft.Web.Services2.Dime.DimeAttachment` 对象。
1. 调用 `MyApplication/EncryptDocument` 通过调用 `EncryptDocumentServiceWse` 对象的 `invoke` 方法和传递 `BLOB` 包含DIME附件的对象。 此过程会返回PDF文档在 `BLOB` 对象。
1. 通过获取返回的值获取附件标识符值 `BLOB` 对象的 `attachmentID` 数据成员。
1. 循环访问中的附件 `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` 并使用附件标识符值获取加密的PDF文档。
1. 获取 `System.IO.Stream` 对象，方法是获取 `Attachment` 对象的 `Stream` 数据成员。
1. 创建字节数组，并将该字节数组传递给 `System.IO.Stream` 对象的 `Read` 方法。 此方法使用表示加密PDF文档的数据流填充字节数组。
1. 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递表示PDF文件位置的字符串值。 此对象表示加密的PDF文档。
1. 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
1. 通过调用，将字节数组的内容写入PDF文件 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

### 创建使用DIME的Apache Axis Java代理类 {#creating-apache-axis-java-proxy-classes-that-use-dime}

您可以使用Apache Axis WSDL2Java工具将服务WSDL转换为Java代理类，以便调用服务操作。 使用Apache Ant，您可以通过AEM Forms服务WSDL生成Axis库文件，从而调用该服务。 (请参阅 [使用Apache Axis创建Java代理类](#creating-java-proxy-classes-using-apache-axis).)

Apache Axis WSDL2Java工具生成JAVA文件，这些文件包含用于向服务发送SOAP请求的方法。 服务接收的SOAP请求由轴生成的库解码并返回为方法和参数。

要调用 `MyApplication/EncryptDocument` 服务（在Workbench中构建）使用轴生成的库文件和DIME，请执行以下步骤：

1. 创建使用 `MyApplication/EncryptDocument` 使用Apache Axis为WSDL提供服务。 (请参阅 [使用Apache Axis创建Java代理类](#creating-java-proxy-classes-using-apache-axis).)
1. 将Java代理类包含在类路径中。
1. 创建 `MyApplicationEncryptDocumentServiceLocator` 对象。
1. 创建 `URL` 对象，方法是使用其构造函数并传递一个字符串值，该值指定AEM Forms服务WSDL定义。 请确保您指定 `?blob=dime` SOAP端点URL末尾。 例如，使用

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. 创建 `EncryptDocumentSoapBindingStub` 对象通过调用其构造函数并传递 `MyApplicationEncryptDocumentServiceLocator`对象和 `URL` 对象。
1. AEM通过调用 `EncryptDocumentSoapBindingStub` 对象的 `setUsername` 和 `setPassword` 方法。

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. 检索要发送给的PDF文档 `MyApplication/EncryptDocument` 通过创建 `java.io.File` 对象。 传递一个指定PDF文档位置的字符串值。
1. 创建 `javax.activation.DataHandler` 对象，使用它的构造函数传递 `javax.activation.FileDataSource` 对象。 此 `javax.activation.FileDataSource` 对象可以通过使用其构造函数并传递 `java.io.File` 表示PDF文档的对象。
1. 创建 `org.apache.axis.attachments.AttachmentPart` 对象，使用它的构造函数传递 `javax.activation.DataHandler` 对象。
1. 通过调用 `EncryptDocumentSoapBindingStub` 对象的 `addAttachment` 方法和传递 `org.apache.axis.attachments.AttachmentPart` 对象。
1. 创建 `BLOB` 对象。 填充 `BLOB` 具有附件标识符值的对象 `BLOB` 对象的 `setAttachmentID` 方法，并传递附件标识符值。 此值可以通过调用 `org.apache.axis.attachments.AttachmentPart` 对象的 `getContentId` 方法。
1. 调用 `MyApplication/EncryptDocument` 通过调用 `EncryptDocumentSoapBindingStub` 对象的 `invoke` 方法。 传递 `BLOB` 包含DIME附件的对象。 此过程会返回PDF文档在 `BLOB` 对象。
1. 通过调用返回的获取附件标识符值 `BLOB` 对象的 `getAttachmentID` 方法。 此方法返回代表返回附件的标识符值的字符串值。
1. 通过调用 `EncryptDocumentSoapBindingStub` 对象的 `getAttachments` 方法。 此方法返回的数组 `Objects` 代表附件。
1. 逐一查看附件( `Object` 数组)并使用附件标识符值获取加密的PDF文档。 每个元素都是一个 `org.apache.axis.attachments.AttachmentPart` 对象。
1. 获取 `javax.activation.DataHandler` 通过调用 `org.apache.axis.attachments.AttachmentPart` 对象的 `getDataHandler` 方法。
1. 获取 `java.io.FileStream` 对象，方法是调用 `javax.activation.DataHandler` 对象的 `getInputStream` 方法。
1. 创建字节数组，并将该字节数组传递给 `java.io.FileStream` 对象的 `read` 方法。 此方法使用表示加密PDF文档的数据流填充字节数组。
1. 创建 `java.io.File` 对象。 此对象表示加密的PDF文档。
1. 创建 `java.io.FileOutputStream` 对象，使用它的构造函数传递 `java.io.File` 对象。
1. 调用 `java.io.FileOutputStream` 对象的 `write` 方法，并传递包含表示加密PDF文档的数据流的字节数组。

**另请参阅**

[快速入门：在Java项目中使用DIME调用服务](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## 使用基于SAML的身份验证 {#using-saml-based-authentication}

在调用服务时，AEM Forms支持各种Web服务身份验证模式。 一种验证模式是使用Web服务调用中的基本授权标头同时指定用户名和密码值。 AEM Forms还支持基于SAML断言的身份验证。 当客户端应用程序使用Web服务调用AEM Forms服务时，该客户端应用程序可以通过以下方式之一提供身份验证信息：

* 作为基本授权的一部分传递凭据
* 将用户名令牌作为WS-Security标头的一部分传递
* 作为WS-Security标头的一部分传递SAML断言
* 作为WS-Security标头的一部分传递Kerberos令牌

AEM Forms不支持标准的基于证书的身份验证，但它不支持其他形式的基于证书的身份验证。

>[!NOTE]
>
>Web服务在“使用AEM Forms进行编程”中快速启动，用于指定执行授权的用户名和密码值。

AEM表单用户的身份可以通过使用密钥签名的SAML断言来表示。 以下XML代码显示了SAML断言的示例。

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

此示例断言是为管理员用户发出的。 此断言包含以下值得注意的项目：

* 在特定期限内有效。
* 它是为特定用户颁发的。
* 它是用数字签名的。 所以任何修改都会破坏签名。
* 它可以作为用户身份的令牌提供给AEM Forms，类似于用户名和密码。

AEM Forms客户端应用程序可以从返回 `AuthResult` 对象。 您可以获取 `AuthResult` 执行下面两种方法之一，执行实例：

* 使用AuthenticationManager API公开的任何身份验证方法来对用户进行身份验证。 通常使用用户名和密码；但是，您还可以使用证书身份验证。
* 使用 `AuthenticationManager.getAuthResultOnBehalfOfUser` 方法。 此方法允许客户端应用程序获取 `AuthResult` 任何AEM表单用户的对象。

可以使用获取的SAML令牌对AEM Forms用户进行身份验证。 此SAML断言（xml片段）可以作为WS-Security标头的一部分发送，并使用户身份验证的Web服务调用。 通常，客户端应用程序已经对用户进行了身份验证，但尚未存储用户凭据。 （或者，用户已通过使用用户名和密码以外的机制登录该客户端。） 在这种情况下，客户端应用程序必须调用AEM Forms并模拟允许调用AEM Forms的特定用户。

要模拟特定用户，请调用 `AuthenticationManager.getAuthResultOnBehalfOfUser` 方法使用web服务。 此方法会返回 `AuthResult` 包含该用户的SAML断言的实例。

接下来，使用该SAML断言来调用任何需要身份验证的服务。 此操作包括作为SOAP标头的一部分发送断言。 使用此断言进行Web服务调用时，AEM Forms将用户标识为该断言所表示的用户。 也就是说，声明中指定的用户是调用服务的用户。

### 使用Apache Axis类和基于SAML的身份验证 {#using-apache-axis-classes-and-saml-based-authentication}

您可以通过使用Axis库创建的Java代理类调用AEM Forms服务。 (请参阅 [使用Apache Axis创建Java代理类](#creating-java-proxy-classes-using-apache-axis).)

使用使用基于SAML的身份验证的AXIS时，请通过Axis注册请求和响应处理程序。 Apache Axis在向AEM Forms发送调用请求之前调用处理程序。 要注册处理程序，请创建扩展的Java类 `org.apache.axis.handlers.BasicHandler`.

**创建带有轴的AssertionHandler**

以下Java类，已命名 `AssertionHandler.java`，显示了扩展的Java类的示例 `org.apache.axis.handlers.BasicHandler`.

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**注册处理程序**

要向Axis注册处理程序，请创建一个client-config.wsdd文件。 默认情况下，Axis会查找具有此名称的文件。 以下XML代码是client-config.wsdd文件的一个示例。 有关详细信息，请参阅坐标轴文档。

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**调用AEM Forms服务**

以下代码示例使用基于SAML的身份验证调用AEM Forms服务。

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### 使用.NET客户端程序集和基于SAML的身份验证 {#using-a-net-client-assembly-and-saml-based-authentication}

您可以通过使用.NET客户端程序集和基于SAML的身份验证来调用Forms服务。 为此，您必须使用Web服务增强功能3.0 (WSE)。 有关创建使用WSE的.NET客户机程序集的信息，请参见 [创建使用DIME的.NET项目](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>DIME部分使用WSE 2.0。要使用基于SAML的身份验证，请按照DIME主题中指定的相同说明进行操作。 但是，请将WSE 2.0替换为WSE 3.0。在开发计算机上安装Web服务增强功能3.0，并将其与Microsoft Visual Studio .NET集成。 您可以从以下位置下载Web服务增强功能3.0： [Microsoft下载中心](https://www.microsoft.com/downloads/search.aspx).

WSE体系结构使用策略、声明和SecurityToken数据类型。 简言之，对于Web服务调用，请指定策略。 一个策略可以有多个断言。 每个断言都可以包含过滤器。 过滤器在Web服务调用的某些阶段调用，此时可以修改SOAP请求。 有关完整的详细信息，请参阅Web服务增强功能3.0文档。

**创建断言和过滤器**

以下C#代码示例创建过滤器和断言类。 此代码示例创建一个SamlAssertionOutputFilter。 在将SOAP请求发送到AEM Forms之前，此过滤器由WSE框架调用。

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**创建SAML令牌**

创建一个类来表示SAML断言。 此类执行的主要任务是将数据值从字符串转换为xml并保留空格。 此断言xml稍后将导入到SOAP请求中。

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**调用AEM Forms服务**

以下C#代码示例使用基于SAML的身份验证调用Forms服务。

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## 使用Web服务时的相关注意事项 {#related-considerations-when-using-web-services}

在使用Web服务调用某些AEM Forms服务操作时，有时会出现问题。 本讨论的目标是确定这些问题并提供解决方案（如果有）。

### 异步调用服务操作 {#invoking-service-operations-asynchronously}

如果尝试异步调用AEM Forms服务操作，如生成PDF `htmlToPDF` 操作， a `SoapFaultException` 发生。 要解决此问题，请创建一个自定义绑定XML文件，该文件映射 `ExportPDF_Result` 元素和其他元素分类到不同的类中。 以下XML表示自定义绑定文件。

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

在使用JAX-WS创建Java代理文件时，请使用此XML文件。 (请参阅 [使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws).)

在使用 —  `b` 命令行选项。 更新 `wsdlLocation` 元素，用于指定AEM Forms的URL。

要确保异步调用正常工作，请修改端点URL值并指定 `async=true`. 例如，对于使用JAX-WS创建的Java代理文件，请为 `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

以下列表指定了异步调用时需要自定义绑定文件的其他服务：

* PDFG3D
* 任务管理器
* 应用程序管理器
* 目录管理器
* Distiller
* Rights Management
* 文档管理

### J2EE应用程序服务器的差异 {#differences-in-j2ee-application-servers}

有时，使用特定J2EE应用程序服务器创建的代理库无法成功调用托管在其他J2EE应用程序服务器上的AEM Forms。 考虑使用部署在WebSphere上的AEM Forms生成的代理库。 此代理库无法成功调用部署在JBoss应用程序服务器上的AEM Forms服务。

某些AEM Forms复杂数据类型，例如 `PrincipalReference`，在将AEM Forms部署到WebSphere上时的定义与JBoss Application Server中的定义不同。 不同J2EE应用程序服务所使用的JDK的差异是WSDL定义存在差异的原因。 因此，请使用从同一J2EE应用程序服务器生成的代理库。

### 使用Web服务访问多个服务 {#accessing-multiple-services-using-web-services}

由于命名空间冲突，数据对象无法在多个服务WSDL之间共享。 不同的服务可以共享数据类型，因此服务在WSDL中共享这些类型的定义。 例如，不能添加两个包含 `BLOB` 数据类型到同一.NET客户端项目。 如果尝试这样做，则会发生编译错误。

以下列表指定了多个服务WSDL之间不能共享的数据类型：

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

为了避免此问题，建议您完全限定数据类型。 例如，考虑使用服务引用同时引用Forms服务和签名服务的.NET应用程序。 两个服务引用都将包含 `BLOB` 类。 要使用 `BLOB` 实例，完全限定 `BLOB` 对象。 以下代码示例显示了此方法。 有关此代码示例的信息，请参见 [对交互式Forms进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

以下C#代码示例对由Forms服务呈现的交互式表单进行签名。 客户端应用程序有两个服务引用。 此 `BLOB` 与Forms服务关联的实例属于 `SignInteractiveForm.ServiceReference2` 命名空间。 同样， `BLOB` 与签名服务关联的实例属于 `SignInteractiveForm.ServiceReference1` 命名空间。 已签名的交互式表单另存为名为的PDF文件 *LoanXFASigned.pdf*.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully-qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify a XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify a XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### 以字母I开头的服务生成无效的代理文件 {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

使用Microsoft .Net 3.5和WCF时，某些AEM Forms生成的代理类的名称不正确。 为IBMFilenetContentRepositoryConnector、IPSchedulerService或其名称以字母I开头的任何其他服务创建代理类时，会出现此问题。例如，如果存在IBMFileNetContentRepositoryConnector，则生成的客户端的名称是 `BMFileNetContentRepositoryConnectorClient`. 生成的代理类中缺少字母I。
