---
title: 使用Web服务调用AEM Forms
seo-title: 使用Web服务调用AEM Forms
description: 'null'
seo-description: 'null'
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '9966'
ht-degree: 0%

---


# 使用Web服务调用AEM Forms {#invoking-aem-forms-using-web-services}

服务容器中的大多数AEM Forms服务都配置为公开Web服务，完全支持Web服务定义语言(WSDL)生成。 也就是说，您可以创建使用AEM Forms服务的本机SOAP堆栈的代理对象。 因此，AEM Forms服务可以交换和处理以下SOAP消息：

* **SOAP请求**: 由请求操作的客户端应用程序发送到Forms服务。
* **SOAP响应**: 在处理SOAP请求后，由Forms服务发送到客户端应用程序。

使用Web服务，您可以执行与使用Java API相同的AEM Forms服务操作。 使用Web服务调用AEM Forms服务的一个好处是，您可以在支持SOAP的开发环境中创建客户端应用程序。 客户端应用程序不绑定到特定的开发环境或编程语言。 例如，可以使用Microsoft Visual Studio .NET和C#作为编程语言创建客户端应用程序。

AEM Forms服务通过SOAP协议公开，并且符合WSI Basic用户档案1.1。 Web服务互操作性(WSI)是一个开放标准组织，它促进跨平台的Web服务互操作性。 有关信息，请参 [阅https://www.ws-i.org/](https://www.ws-i.org)。

AEM Forms支持以下Web服务标准：

* **编码**: 仅支持文档和文本编码(根据WSI Basic用户档案，这是首选编码)。 (请参 [阅使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **MTOM**: 表示一种使用SOAP请求对附件进行编码的方法。 (请参 [阅使用MTOM调用AEM Forms](#invoking-aem-forms-using-mtom)。)
* **SwaRef**: 表示使用SOAP请求对附件进行编码的另一种方式。 (请参 [阅使用SwaRef调用AEM Forms](#invoking-aem-forms-using-swaref)。)
* **带附件的SOAP**: 支持MIME和DIME（直接Internet消息封装）。 这些协议是通过SOAP发送附件的标准方式。 Microsoft Visual Studio .NET应用程序使用DIME。 (请参 [阅使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **WS-安全性**: 支持用户名密码令牌用户档案，这是作为WS Security SOAP头的一部分发送用户名和密码的标准方式。 AEM Forms还支持HTTP基本身份验证。 (请参 [阅使用WS-Security头传递凭据](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html)。)

要使用Web服务调用AEM Forms服务，通常需要创建一个使用服务WSDL的代理库。 使 *用Web服务调用AEM Forms* (Invering Services)部分使用JAX-WS创建Java代理类以调用服务。 (请参 [阅使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws)。)

可通过指定以下URL定义来检索服务WDSL（括号中的项是可选项）:

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

其中：

* *your_serverhost* 表示承载AEM Forms的J2EE应用程序服务器的IP地址。
* *your_port* 表示J2EE应用程序服务器使用的HTTP端口。
* *service_name* 表示服务名称。
* *version* 表示服务的目标版本（默认情况下使用最新服务版本）。
* `async` 指定值以 `true` 启用其他异步调用操作(默 `false` 认情况)。
* *lc_version* 表示要调用的AEM Forms的版本。

下表列表服务WSDL定义(假定AEM Forms部署在本地主机上，而帖子为8080)。

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
   <td><p>返回和恢复</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>条形码</p></td>
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
   <td><p>DocConverter </p></td>
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
   <td><p>表单</p></td>
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
   <td><p>生成3D PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>输出</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF实用程序 </p></td>
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
   <td><p>权限管理 </p></td>
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

**AEM Forms进程WSDL定义**

必须在WSDL定义中指定应用程序名称和进程名称，才能访问属于在Workbench中创建的进程的WSDL。 假定应用程序的名 `MyApplication` 称为，进程的名称为 `EncryptDocument`。 在这种情况下，请指定以下WSDL定义：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>有关示例短期进 `MyApplication/EncryptDocument` 程的信息，请参阅 [短期进程示例](/help/forms/developing/aem-forms-processes.md)。

>[!NOTE]
>
>应用程序可以包含文件夹。 在这种情况下，请在WSDL定义中指定文件夹名称：

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**使用Web服务访问新功能**

新的AEM Forms服务功能可以使用Web服务进行访问。 例如，在AEM Forms中，引入了使用MTOM对附件进行编码的功能。 (请参 [阅使用MTOM调用AEM Forms](#invoking-aem-forms-using-mtom)。)

要访问AEM Forms中引入的新功能，请在WSDL `lc_version` 定义中指定属性。 例如，要访问新的服务功能（包括MTOM支持），请指定以下WSDL定义：

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>设置属 `lc_version` 性时，请确保使用三位数字。 例如，9.0.1等于9.0版。

**Web服务BLOB数据类型**

AEM Forms服务WSDL定义了许多数据类型。 Web服务中公开的最重要的数据类型之一是类 `BLOB` 型。 使用AEM FormsJava API时， `com.adobe.idp.Document` 此数据类型将映射到类。 (请参 [阅使用Java API将数据传递到AEM Forms服务](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)。)

对 `BLOB` 象向AEM Forms服务发送和检索二进制数据（例如，PDF文件、XML数据等）。 在 `BLOB` 服务WSDL中定义类型如下：

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

只有 `MTOM` AEM Forms `swaRef` 支持和字段。 仅当指定包含属性的URL时，才能使用这些新字 `lc_version` 段。

**在服务请求中提供BLOB对象**

如果AEM Forms服务操作需 `BLOB` 要将类型作为输入值，请在应用程序逻辑 `BLOB` 中创建该类型的实例。 (使用AEM表单进行编程中的许多Web *服务快速开始* ，都显示了如何使用BLOB数据类型。)

按如下方式将值分配给属 `BLOB` 于实例的字段：

* **Base64**: 要将数据作为以Base64格式编码的文本进行传递，请在字 `BLOB.binaryData` 段中设置数据，并在字段中以MIME格式( `application/pdf`例如)设置数 `BLOB.contentType` 据类型。 (请参 [阅使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **MTOM**: 要在MTOM附件中传递二进制数据，请在字段中设置 `BLOB.MTOM` 数据。 此设置使用Java JAX-WS框架或SOAP框架的本机API将数据附加到SOAP请求。 (请参 [阅使用MTOM调用AEM Forms](#invoking-aem-forms-using-mtom)。)
* **SwaRef**: 要在WS-I SwaRef附件中传递二进制数据，请在字段中设置 `BLOB.swaRef` 数据。 此设置使用Java JAX-WS框架将数据附加到SOAP请求。 (请参 [阅使用SwaRef调用AEM Forms](#invoking-aem-forms-using-swaref)。)
* **MIME或DIME附件**: 要在MIME或DIME附件中传递数据，请使用SOAP框架的本机API将数据附加到SOAP请求。 在字段中设置附件标 `BLOB.attachmentID` 识符。 (请参 [阅使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding)。)
* **远程URL**: 如果数据托管在Web服务器上并可通过HTTP URL访问，请在字段中设置HTTP `BLOB.remoteURL` URL。 (请参 [阅通过HTTP使用BLOBAEM Forms调用](#invoking-aem-forms-using-blob-data-over-http)。)

**访问从服务返回的BLOB对象中的数据**

返回对象的传输协 `BLOB` 议取决于多个因素，这些因素按以下顺序考虑，当满足主要条件时停止：

1. **目标URL指定传输协议**。 如果在SOAP调用中指定的目标URL包 `blob="`*含参数&#x200B;*BLOB_TYPE*”，则&#x200B;*BLOB_TYPE将确定传输协议。* BLOB_TYPE是&#x200B;*base64、dime、mime、http、mtom或swaref的占位符。
1. **服务SOAP端点为智能**。 如果满足以下条件，则使用与输入文档相同的传输协议返回输出文档:

   * 服务的SOAP端点参数输出Blob对象的默认协议设置为智能。

      对于具有SOAP端点的每个服务，管理控制台允许您为任何返回的Blob指定传输协议。 (请参阅 [管理帮助](https://www.adobe.com/go/learn_aemforms_admin_63)。)

   * AEM Forms服务将一个或多个文档作为输入。

1. **服务SOAP端点不是智能**。 所配置的协议确定文档传输协议，并在相应字段中返回数 `BLOB` 据。 例如，如果SOAP端点设置为DIME，则返回的blob将位于字段中，而 `blob.attachmentID` 不管任何输入文档的传输协议。
1. **否则**。 如果服务不将文档类型作为输入，则输出文档将在HTTP协议 `BLOB.remoteURL` 的字段中返回。

正如第一个条件中所述，您可以通过扩展带有后缀的SOAP端点URL来确保任何返回文档的传输类型，如下所示：

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

下面是传输类型与从中获取数据的字段之间的关联：

* **Base64格式**: 设置后 `blob` 缀以 `base64` 返回字段中的 `BLOB.binaryData` 数据。
* **MIME或DIME附件**: 将后缀 `blob` 设置为 `DIME` 或将 `MIME` 数据返回为相应的附件类型，并在字段中返回附件标识 `BLOB.attachmentID` 符。 使用SOAP框架的专有API从附件读取数据。
* **远程URL**: 设置后 `blob` 缀以保 `http` 留应用程序服务器上的数据，并返回指向字段中数据的URL `BLOB.remoteURL` 。
* **MTOM或SwaRef**: 将后缀 `blob` 设置为 `mtom` 或将数据 `swaref` 返回为相应的附件类型，并在或字段中返回附 `BLOB.MTOM` 件标 `BLOB.swaRef` 识符。 使用SOAP框架的本机API从附件读取数据。

>[!NOTE]
>
>建议在通过调用对象的方法填充对象时 `BLOB` 不要超过30 `setBinaryData` MB。 否则，可能会发生 `OutOfMemory` 异常。

>[!NOTE]
>
>使用MTOM传输协议的基于JAX WS的应用程序仅限于25MB的发送和接收数据。 此限制是由于JAX-WS中的错误造成的。 如果已发送和已接收文件的总大小超过25MB，请使用SwaRef传输协议而不是MTOM协议。 否则，可能会出现例外 `OutOfMemory` 情况。

**基64编码字节阵列的MTOM传输**

除对象外， `BLOB` MTOM协议还支持任何复杂类型的字节数组参数或字节数组字段。 这意味着支持MTOM的客户端SOAP框架可以将 `xsd:base64Binary` 任何元素作为MTOM附件（而不是基于64编码的文本）发送。 AEM FormsSOAP端点可以读取此类字节数组编码。 但是，AEM Forms服务始终返回一个字节数组类型作为基64编码的文本。 输出字节数组参数不支持MTOM。

返回大量二进制数据的AEM Forms服务使用文档/BLOB类型，而不是字节数组类型。 文档类型在传输大量数据时效率更高。

## Web服务数据类型 {#web-service-data-types}

下表列表了Java数据类型并显示相应的Web服务数据类型。

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
   <td><p>类 <code>DATE</code> 型，在服务WSDL中定义如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服务操作以 <code>java.util.Date</code> 值作为输入，则SOAP客户端应用程序必须在字段中传递该 <code>DATE.date</code> 日期。 在这种情况下 <code>DATE.calendar</code> ，设置字段会导致运行时异常。 如果服务返回 <code>java.util.Date</code>日期，则在字段中重新调 <code>DATE.date</code> 整日期。</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>类 <code>DATE</code> 型，在服务WSDL中定义如下：</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服务操作以 <code>java.util.Calendar</code> 值作为输入，则SOAP客户端应用程序必须在字段中传递该 <code>DATE.caledendar</code> 日期。 在此 <code>DATE.date</code> 情况下设置字段会导致运行时异常。 如果服务返回 <code>java.util.Calendar</code>日期，则在字段中返回 <code>DATE.calendar</code> 日期。 </p></td>
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
   <td><p>在 <code>apachesoap:Map</code>服务WSDL中定义，如下所示：</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>映射表示为键／值对的序列。</p></td>
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
   <td><p>XML类型，在服务WSDL中定义如下：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服务操作接 <code>org.w3c.dom.Document</code> 受某个值，请在字段中传递 <code>XML.document</code> XML数据。</p><p>设置字 <code>XML.element</code> 段会导致运行时异常。 如果服务返回 <code>org.w3c.dom.Document</code>一个，则在字段中返回XML数 <code>XML.document</code> 据。</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>XML类型，在服务WSDL中定义如下：</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>如果AEM Forms服务操作采 <code>org.w3c.dom.Element</code> 用输入，请在字段中传递XML <code>XML.element</code> 数据。</p><p>设置字 <code>XML.document</code> 段会导致运行时异常。 如果服务返回 <code>org.w3c.dom.Element</code>一个，则在字段中重新调整XML <code>XML.element</code> 数据。</p></td>
  </tr>
 </tbody>
</table>

**Adobe开发人员网站**

Adobe开发人员网站包含以下文章，其中讨论使用Web服务API调用AEM Forms服务：

[创建表单渲染ASP.NET应用程序](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[使用自定义组件调用Web服务](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>使用自定义组件调用Web服务描述如何创建调用第三方Web服务的AEM Forms组件。

## 使用JAX-WS创建Java代理类 {#creating-java-proxy-classes-using-jax-ws}

可以使用JAX-WS将Forms服务WSDL转换为Java代理类。 这些类允许您调用AEM Forms服务操作。 Apache Ant允许您通过引用AEM Forms服务WSDL创建生成Java代理类的构建脚本。 通过执行以下步骤，可以生成JAX-WS代理文件：

1. 在客户端计算机上安装Apache Ant。 (请参 [阅https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)。)

   * 将bin目录添加到类路径。
   * 将环境 `ANT_HOME` 变量设置为安装Ant的目录。

1. 安装JDK 1.6或更高版本。

   * 将JDK bin目录添加到类路径。
   * 将JRE bin目录添加到类路径。 此bin位于目 `[JDK_INSTALL_LOCATION]/jre` 录中。
   * 将环境 `JAVA_HOME` 变量设置为安装JDK的目录。

   JDK 1.6包含在build.xml文件中使用的wsimport项目。 JDK 1.5不包含该项目。

1. 在客户机上安装JAX-WS。 (请参 [阅用于XML Web服务的Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)。)
1. 使用JAX-WS和Apache Ant生成Java代理类。 创建Ant构建脚本以完成此任务。 以下脚本是名为build.xml的示例Ant构建脚本：

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

   在此Ant构建脚本中，请注 `url` 意将属性设置为引用在localhost上运行的加密服务WSDL。 必须将 `username` 和 `password` 属性设置为有效的AEM表单用户名和密码。 请注意，URL包含属 `lc_version` 性。 如果不指定 `lc_version` 该选项，则无法调用新AEM Forms服务操作。

   >[!NOTE]
   >
   >使 `EncryptionService`用要使用Java代理类调用的AEM Forms服务名替换。 例如，要为Rights Management服务创建Java代理类，请指定：

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. 创建一个BAT文件以执行Ant构建脚本。 以下命令可以位于负责执行Ant构建脚本的BAT文件中：

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   将ANT构建脚本放在C:\Program Files\Java\jaxws-ri\bin directory目录中。 脚本将JAVA文件写入。/classes文件夹。 脚本生成可调用服务的JAVA文件。

1. 将JAVA文件打包到JAR文件中。 如果您正在使用Eclipse，请按照以下步骤操作：

   * 新建一个Java项目，用于将代理JAVA文件打包到JAR文件中。
   * 在项目中创建源文件夹。
   * 在“源 `com.adobe.idp.services` ”文件夹中创建包。
   * 选择 `com.adobe.idp.services` 包，然后将JAVA文件从adobe/idp/services文件夹导入包。
   * 如有必要，请在“ `org/apache/xml/xmlsoap` 源”文件夹中创建包。
   * 选择源文件夹，然后从org/apache/xml/xmlsoap文件夹导入JAVA文件。
   * 将Java编译器的规范级别设置为5.0或更高。
   * 构建项目。
   * 将项目导出为JAR文件。
   * 将此JAR文件导入客户端项目的类路径中。 此外，导入位于&lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty中的所有JAR文件。

   >[!NOTE]
   >
   >使用AEM表单编程中的所有Java Web服务快速开始（Forms服务除外）均使用JAX-WS创建Java代理文件。 此外，所有Java Web服务快速开始均使用SwaRef。 (请参 [阅使用SwaRef调用AEM Forms](#invoking-aem-forms-using-swaref)。)

**另请参阅**

[使用Apache Axis创建Java代理类](#creating-java-proxy-classes-using-apache-axis)

[使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[通过HTTP使用BLOBAEM Forms调用](#invoking-aem-forms-using-blob-data-over-http)

[使用SwaRef调用AEM Forms](#invoking-aem-forms-using-swaref)

## 使用Apache Axis创建Java代理类 {#creating-java-proxy-classes-using-apache-axis}

您可以使用Apache Axis WSDL2Java工具将Forms服务转换为Java代理类。 这些类允许您调用Forms服务操作。 使用Apache Ant，可以通过服务WSDL生成Axis库文件。 您可以通过URL https://ws.apache.org/axis/下载Apache [Axis](https://ws.apache.org/axis/)。

>[!NOTE]
>
>与Forms服务关联的Web服务快速开始使用使用Apache Ax创建的Java代理类。 Forms Web服务快速开始还使用Base64作为编码类型。 (请参 [阅Forms Service API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)。)

通过执行以下步骤，可以生成Axis Java库文件：

1. 在客户端计算机上安装Apache Ant。 网址为https://ant.apache.org/bindownload.cgi [](https://ant.apache.org/bindownload.cgi).

   * 将bin目录添加到类路径。
   * 将环境 `ANT_HOME` 变量设置为安装Ant的目录。

1. 在客户端计算机上安装Apache Axis 1.4。 网址为https://ws.apache.org/axis/ [](https://ws.apache.org/axis/.md).
1. 设置类路径以在Web服务客户端中使用Axis JAR文件，如https://ws.apache.org/axis/java/install.html上的Axis安装说明中 [所述](https://ws.apache.org/axis/java/install.html)。
1. 使用Axis中的Apache WSDL2Java工具生成Java代理类。 创建Ant构建脚本以完成此任务。 以下脚本是名为build.xml的示例Ant构建脚本：

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

   在此Ant构建脚本中，请注 `url` 意将属性设置为引用在localhost上运行的加密服务WSDL。 必须将 `username` 和 `password` 属性设置为有效的AEM表单用户名和密码。

1. 创建一个BAT文件以执行Ant构建脚本。 以下命令可以位于负责执行Ant构建脚本的BAT文件中：

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA文件将写入C:\JavaFiles folder as specified by the 属性 `output` 。 要成功调用Forms服务，请将这些JAVA文件导入类路径。

   默认情况下，这些文件属于名为的Java包 `com.adobe.idp.services`。 建议将这些JAVA文件放入JAR文件中。 然后，将JAR文件导入客户端应用程序的类路径。

   >[!NOTE]
   >
   >将。JAVA文件放入JAR的方法不同。 一种方式是使用Java IDE（如Eclipse）。 创建一个Java项目并创 `com.adobe.idp.services`建一个包（所有。JAVA文件都属于此包）。 然后，将所有。JAVA文件导入包中。 最后，将项目导出为JAR文件。

1. 修改类中的 `EncryptionServiceLocator` URL以指定编码类型。 例如，要使用base64，请指 `?blob=base64` 定以确保对 `BLOB` 象返回二进制数据。 即，在类中 `EncryptionServiceLocator` ，找到以下代码行：

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

   这些JAR文件位于目 `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` 录中。

**另请参阅**

[使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws)

[使用Base64编码调用AEM Forms](#invoking-aem-forms-using-base64-encoding)

[通过HTTP使用BLOBAEM Forms调用](#invoking-aem-forms-using-blob-data-over-http)

## 使用Base64编码调用AEM Forms {#invoking-aem-forms-using-base64-encoding}

您可以使用Base64编码调用AEM Forms服务。 Base64编码对随Web服务调用请求发送的附件进行编码。 即，数据 `BLOB` 是Base64编码的，而不是整个SOAP消息。

“使用Base64编码调用AEM Forms”讨论调用以下AEM Forms短时进程(使用Base64 `MyApplication/EncryptDocument` 编码命名)。

>[!NOTE]
>
>此过程不基于现有AEM Forms流程。 要与代码示例一起操作，请使用Workbench创建一个名 `MyApplication/EncryptDocument` 为的流程。 (请参 [阅使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

调用此进程时，它将执行以下操作：

1. 获取传递给该流程的不安全PDF文档。 此操作基于操 `SetValue` 作。 此进程的输入参数是一个名 `document` 为的进程变量 `inDoc`。
1. 用密码加密PDF文档。 此操作基于操 `PasswordEncryptPDF` 作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`。

### 创建使用Base64编码的。NET客户端程序集 {#creating-a-net-client-assembly-that-uses-base64-encoding}

您可以创建。NET客户端程序集，从Microsoft Visual Studio .NET项目调用Forms服务。 要创建使用base64编码的。NET客户端程序集，请执行以下步骤：

1. 根据AEM Forms调用URL创建代理类。
1. 创建一个生成。NET客户端程序集的Microsoft Visual Studio .NET项目。

**创建代理类**

可以使用Microsoft Visual Studio附带的工具创建用于创建。NET客户端程序集的代理类。 该工具的名称为wsdl.exe，它位于Microsoft Visual Studio安装文件夹中。 要创建代理类，请打开命令提示符并导航到包含wsdl.exe文件的文件夹。 有关wsdl.exe工具的详细信息，请参阅“MSDN *帮助”*。

在命令提示符下输入以下命令：

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

默认情况下，此工具会在基于WSDL名称的同一文件夹中创建CS文件。 在这种情况下，它将创建一个名为EncryptDocumentService. *cs的CS文件*。 使用此CS文件创建代理对象，用于调用在调用URL中指定的服务。

修改代理类中的URL以包 `?blob=base64` 含，确保对 `BLOB` 象返回二进制数据。 在代理类中，找到以下代码行：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

并将其更改为：

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

使 *用Base64 Encoding调用AEM Forms* , `MyApplication/EncryptDocument` 此部分用作示例。 如果要为其他Forms服务创建。NET客户端程序集，请确保 `MyApplication/EncryptDocument` 用服务的名称替换。

**开发。NET客户端程序集**

创建生成。NET客户端程序集的Visual Studio类库项目。 可以使用wsdl.exe创建的CS文件可以导入到此项目中。 此项目生成一个DLL文件（.NET客户端程序集），您可以在其他Visual Studio .NET项目中使用它调用服务。

1. 开始Microsoft Visual Studio .NET。
1. 创建类库项目并将其命名为DocumentService。
1. 导入您使用wsdl.exe创建的CS文件。
1. 在“项 **目** ”菜单中，选 **择“添加引用**”。
1. 在“添加引用”对话 **框中，选择System.Web.Services.dll**。
1. 单击 **选择** ，然后单 **击确定**。
1. 编译和构建项目。

>[!NOTE]
>
>此过程创建一个名为DocumentService.dll的。NET客户端程序集，您可以使用它向服务发送SOAP `MyApplication/EncryptDocument` 请求。

>[!NOTE]
>
>确保已添加 `?blob=base64` 到用于创建。NET客户端程序集的代理类中的URL。 否则，无法从对象检索二进制 `BLOB` 数据。

**引用。NET客户端程序集**

将新创建的。NET客户端程序集放在正在开发客户端应用程序的计算机上。 将。NET客户端程序集放置到目录后，可从项目中引用它。 还可从您的 `System.Web.Services` 项目中引用库。 如果不引用此库，则无法使用。NET客户端程序集调用服务。

1. 在“项 **目** ”菜单中，选 **择“添加引用**”。
1. Click the **.NET** tab.
1. 单击 **“浏览** ”并找到DocumentService.dll文件。
1. 单击 **选择** ，然后单 **击确定**。

**使用使用Base64编码的。NET客户端程序集调用服务**

您可以使用 `MyApplication/EncryptDocument` 使用Base64编码的。NET客户端程序集调用服务（在Workbench中构建）。 要调用服 `MyApplication/EncryptDocument` 务，请执行以下步骤：

1. 创建一个使用服务WSDL的Microsoft .NET客 `MyApplication/EncryptDocument` 户端程序集。
1. 创建客户端Microsoft .NET项目。 在客户端项目中引用Microsoft .NET客户端程序集。 也可参考 `System.Web.Services`。
1. 使用Microsoft .NET客户端程序集，通过调 `MyApplication_EncryptDocumentService` 用其默认构造函数创建对象。
1. 用对 `MyApplication_EncryptDocumentService` 象设置对 `Credentials` 象的属 `System.Net.NetworkCredential` 性。 在构造 `System.Net.NetworkCredential` 函数中，指定AEM表单用户名和相应的口令。 设置身份验证值，使您的。NET客户端应用程序能够与AEM Forms成功交换SOAP消息。
1. 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储PDF文档传递到该 `MyApplication/EncryptDocument` 过程。
1. 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示PDF文档的文件位置以及打开文件的模式。
1. 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
1. 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
1. 通过 `BLOB` 将对象属性 `binaryData` 赋予字节数组的内容来填充对象。
1. 通过调 `MyApplication/EncryptDocument` 用对象的方 `MyApplication_EncryptDocumentService` 法并传递包 `invoke``BLOB` 含PDF文档的对象来调用该过程。 此过程在对象中返回加密的PDF `BLOB` 文档。
1. 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示密码加密文档的文件位置。
1. 创建一个字节数组，用于存储对象 `BLOB` 方法返回的对 `MyApplicationEncryptDocumentService` 象的数据 `invoke` 内容。 通过获取对象数据成员的值 `BLOB` 填充字节 `binaryData` 数组。
1. 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
1. 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组内 `Write` 容写入PDF文件。

### 使用Java代理类和Base64编码调用服务 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

可以使用Java代理类和Base64调用AEM Forms服务。 要使用Java代 `MyApplication/EncryptDocument` 理类调用服务，请执行以下步骤：

1. 使用使用服务WSDL的JAX-WS创建Java代 `MyApplication/EncryptDocument` 理类。 使用以下WSDL端点：

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >替 `hiro-xp` 换为 *J2EE应用程序服务器托管AEM Forms的IP地址。*

1. 将使用JAX-WS创建的Java代理类打包到JAR文件中。
1. 在以下路径中包含Java代理JAR文件和JAR文件：

   &lt;安装目录>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客户端项目的类路径中。

1. 使用对 `MyApplicationEncryptDocumentService` 象的构造函数创建对象。
1. 通过 `MyApplicationEncryptDocument` 调用对象的 `MyApplicationEncryptDocumentService` 方法创建 `getEncryptDocument` 对象。
1. 通过为以下数据成员分配值来设置调用AEM Forms所需的连接值：

   * 将WSDL端点和编码类型指 `javax.xml.ws.BindingProvider` 定给对象 `ENDPOINT_ADDRESS_PROPERTY` 字段。 要使用Base64 `MyApplication/EncryptDocument` 编码调用服务，请指定以下URL值：

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * 将AEM表单用户分配 `javax.xml.ws.BindingProvider` 到对象的字 `USERNAME_PROPERTY` 段。
   * 为对象的字段指 `javax.xml.ws.BindingProvider` 定相应的口 `PASSWORD_PROPERTY` 令值。

   以下代码示例显示此应用程序逻辑：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 通过使用对象的构造函数创建 `MyApplication/EncryptDocument` 对象，检索要发 `java.io.FileInputStream` 送到该进程的PDF文档。 传递一个指定PDF文档位置的字符串值。
1. 创建一个字节数组，并用对象的内容填充该 `java.io.FileInputStream` 数组。
1. 使用对 `BLOB` 象的构造函数创建对象。
1. 通过调 `BLOB` 用对象的方法并 `setBinaryData` 传递字节数组来填充对象。 对 `BLOB` 象是使 `setBinaryData` 用Base64编码时要调用的方法。 请参阅在服务请求中提供BLOB对象。
1. 通过调 `MyApplication/EncryptDocument` 用对象的方 `MyApplicationEncryptDocument` 法来调用 `invoke` 进程。 传递 `BLOB` 包含PDF文档的对象。 invoke方法返回包 `BLOB` 含已加密PDF文档的对象。
1. 通过调用对象的方法，创建包含已加密PDF文档 `BLOB` 的字节数 `getBinaryData` 组。
1. 将加密的PDF文档另存为PDF文件。 将字节数组写入文件。

**另请参阅**

[快速开始: 使用Java代理文件和Base64编码调用服务](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[创建使用Base64编码的。NET客户端程序集](#creating-a-net-client-assembly-that-uses-base64-encoding)

## 使用MTOM调用AEM Forms {#invoking-aem-forms-using-mtom}

您可以通过使用Web服务标准MTOM调用AEM Forms服务。 此标准定义二进制数据(如PDF文档)如何通过Internet或Intranet传输。 MTOM的一个功能是使用元 `XOP:Include` 素。 此元素在XML二进制优化打包(XOP)规范中定义，以引用SOAP消息的二进制附件。

此处讨论的是使用MTOM调用以下名为的AEM Forms短期进程 `MyApplication/EncryptDocument`。

>[!NOTE]
>
>此过程不基于现有AEM Forms流程。 要与代码示例一起操作，请使用Workbench创建一个名 `MyApplication/EncryptDocument` 为的流程。 (请参 [阅使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

调用此进程时，它将执行以下操作：

1. 获取传递给该流程的不安全PDF文档。 此操作基于操 `SetValue` 作。 此进程的输入参数是一个名 `document` 为的进程变量 `inDoc`。
1. 用密码加密PDF文档。 此操作基于操 `PasswordEncryptPDF` 作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`。

>[!NOTE]
>
>MTOM支持在AEM Forms版本9中添加。

>[!NOTE]
>
>使用MTOM传输协议的基于JAX WS的应用程序仅限于25MB的发送和接收数据。 此限制是由于JAX-WS中的错误造成的。 如果已发送和已接收文件的总大小超过25MB，请使用SwaRef传输协议而不是MTOM协议。 否则，可能会出现例外 `OutOfMemory` 情况。

此处讨论的是在Microsoft .NET项目中使用MTOM调用AEM Forms服务。 使用的。NET框架为3.5，开发环境为Visual Studio 2008。 如果您的开发计算机上已安装Web服务增强(WSE)，请将其删除。 .NET 3.5框架支持名为Windows Communication Foundation(WCF)的SOAP框架。 当使用MTOM调用AEM Forms时，仅支持WCF（不支持WSE）。

### 创建使用MTOM调用服务的。NET项目 {#creating-a-net-project-that-invokes-a-service-using-mtom}

您可以创建一个Microsoft .NET项目，它可以使用Web服务调用AEM Forms服务。 首先，使用Visual Studio 2008创建Microsoft .NET项目。 要调用AEM Forms服务，请为要在项目中调用的AEM Forms服务创建服务引用。 创建服务引用时，请指定AEM Forms服务的URL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

替换 `localhost` 为承载AEM Forms的J2EE应用程序服务器的IP地址。 替换 `MyApplication/EncryptDocument` 为要调用的AEM Forms服务的名称。 例如，要调用Rights Management操作，请指定：

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

该选 `lc_version` 项确保AEM Forms功能（如MTOM）可用。 如果不指定 `lc_version` 选项，则无法使用MTOM调用AEM Forms。

创建服务引用后，与AEM Forms服务关联的数据类型可在您的。NET项目中使用。 要创建调用AEM Forms服务的。NET项目，请执行以下步骤：

1. 使用Microsoft Visual Studio 2008创建。NET项目。
1. 在“项 **目** ”菜单中，选 **择“添加服务引用”**。
1. 在“地 **址** ”对话框中，指定AEM Forms服务的WSDL。 例如，

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. 单击 **“Go** ”，然后单 **击“OK**”。

### 在。NET项目中使用MTOM调用服务 {#invoking-a-service-using-mtom-in-a-net-project}

请考虑接 `MyApplication/EncryptDocument` 受不安全的PDF文档并返回口令加密的PDF文档的过程。 要使用MTOM `MyApplication/EncryptDocument` 调用流程（在Workbench中构建），请执行以下步骤：

1. 创建Microsoft .NET项目。
1. 使用对象 `MyApplication_EncryptDocumentClient` 的默认构造函数创建对象。
1. 使用构 `MyApplication_EncryptDocumentClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务和编码类型：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请确保指定 `?blob=mtom`。

   >[!NOTE]
   >
   >替 `hiro-xp` 换为 *J2EE应用程序服务器托管AEM Forms的IP地址。*

1. 通过 `System.ServiceModel.BasicHttpBinding` 获取数据成员的值创建 `EncryptDocumentClient.Endpoint.Binding` 对象。 将返回值转换为 `BasicHttpBinding`。
1. 将对 `System.ServiceModel.BasicHttpBinding` 象的数据 `MessageEncoding` 成员设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
1. 通过执行以下任务启用基本HTTP身份验证：

   * 将AEM表单用户名分配给数据成员 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`。
   * 为数据成员分配相应的口令值 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`。
   * 为数据成 `HttpClientCredentialType.Basic` 员指定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为数据成 `BasicHttpSecurityMode.TransportCredentialOnly` 员指定常量值 `BasicHttpBindingSecurity.Security.Mode`。

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

1. 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储PDF文档以传递到该 `MyApplication/EncryptDocument` 过程。
1. 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示PDF文档的文件位置以及打开文件的模式。
1. 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
1. 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
1. 通过 `BLOB` 为对象的数据成 `MTOM` 员分配字节数组的内容来填充对象。
1. 通过调 `MyApplication/EncryptDocument` 用对象的方 `MyApplication_EncryptDocumentClient` 法来调用 `invoke` 进程。 传递 `BLOB` 包含PDF文档的对象。 此过程在对象中返回加密的PDF `BLOB` 文档。
1. 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示受保护PDF文档的文件位置。
1. 创建一个字节数组，它存储由方 `BLOB` 法返回的对象的数据 `invoke` 内容。 通过获取对象数据成员的 `BLOB` 值填充字 `MTOM` 节数组。
1. 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
1. 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入PDF文件。

>[!NOTE]
>
>大多数AEM Forms服务操作都具有MTOM快速开始。 您可以在服务的相应快速视图部分开始这些快速开始。 例如，要查看“输出快速开始”部分，请参 [阅输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**另请参阅**

[快速开始: 在。NET项目中使用MTOM调用服务](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[使用Web服务访问多个服务](#accessing-multiple-services-using-web-services)

[创建一个ASP.NET Web应用程序，它调用以人为中心的长寿命流程](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## 使用SwaRef调用AEM Forms {#invoking-aem-forms-using-swaref}

可以使用SwaRef调用AEM Forms服务。 XML元素的内 `wsi:swaRef` 容作为附件发送到SOAP主体中，该SOAP主体存储对附件的引用。 使用SwaRef调用Forms服务时，请使用Java API for XML Web Services(JAX-WS)创建Java代理类。 (请参 [阅用于XML Web服务的Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)。)

此处讨论的是调用以下使用SwaRef命名的短 `MyApplication/EncryptDocument` 期表单进程。

>[!NOTE]
>
>此过程不基于现有AEM Forms流程。 要与代码示例一起操作，请使用Workbench创建一个名 `MyApplication/EncryptDocument` 为的流程。 (请参 [阅使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

调用此进程时，它将执行以下操作：

1. 获取传递给该流程的不安全PDF文档。 此操作基于操 `SetValue` 作。 此进程的输入参数是一个名 `document` 为的进程变量 `inDoc`。
1. 用密码加密PDF文档。 此操作基于操 `PasswordEncryptPDF` 作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`。

>[!NOTE]
>
>在AEM Forms中添加了SwaRef支持

下面讨论如何在Java客户端应用程序中使用SwaRef调用表单服务。 Java应用程序使用使用JAX-WS创建的代理类。

### 使用使用SwaRef的JAX-WS库文件调用服务 {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

要使用使用 `MyApplication/EncryptDocument` JAX-WS和SwaRef创建的Java代理文件调用该过程，请执行以下步骤：

1. 使用使用服务WSDL的JAX-WS创建Java代 `MyApplication/EncryptDocument` 理类。 使用以下WSDL端点：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   有关信息，请 [参阅使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws)。

   >[!NOTE]
   >
   >替 `hiro-xp` 换为 *承载AEM Forms的J2EE应用程序服务器的IP地址。*

1. 将使用JAX-WS创建的Java代理类打包到JAR文件中。
1. 在以下路径中包含Java代理JAR文件和JAR文件：

   &lt;安装目录>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客户端项目的类路径中。

1. 使用对 `MyApplicationEncryptDocumentService` 象的构造函数创建对象。
1. 通过 `MyApplicationEncryptDocument` 调用对象的 `MyApplicationEncryptDocumentService` 方法创建 `getEncryptDocument` 对象。
1. 通过为以下数据成员分配值来设置调用AEM Forms所需的连接值：

   * 将WSDL端点和编码类型指 `javax.xml.ws.BindingProvider` 定给对象 `ENDPOINT_ADDRESS_PROPERTY` 字段。 要使用SwaRef `MyApplication/EncryptDocument` 编码调用服务，请指定以下URL值：

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * 将AEM表单用户分配 `javax.xml.ws.BindingProvider` 到对象的字 `USERNAME_PROPERTY` 段。
   * 为对象的字段指 `javax.xml.ws.BindingProvider` 定相应的口 `PASSWORD_PROPERTY` 令值。

   以下代码示例显示此应用程序逻辑：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 通过使用对象的构造函数创建 `MyApplication/EncryptDocument` 对象，检索要发 `java.io.File` 送到该进程的PDF文档。 传递一个指定PDF文档位置的字符串值。
1. 使用构 `javax.activation.DataSource` 造函数创建 `FileDataSource` 对象。 传递对 `java.io.File` 象。
1. 使用对 `javax.activation.DataHandler` 象的构造函数并传递该对 `javax.activation.DataSource` 象。
1. 使用对 `BLOB` 象的构造函数创建对象。
1. 通过调 `BLOB` 用对象的方法并 `setSwaRef` 传递对象来填充 `javax.activation.DataHandler` 对象。
1. 通过调 `MyApplication/EncryptDocument` 用对象的方 `MyApplicationEncryptDocument` 法并传递包 `invoke``BLOB` 含PDF文档的对象来调用该过程。 invoke方法返回包 `BLOB` 含加密PDF文档的对象。
1. 通过 `javax.activation.DataHandler` 调用对象的方 `BLOB` 法填充对 `getSwaRef` 象。
1. 通过调 `javax.activation.DataHandler` 用对象 `java.io.InputSteam` 的方法将对 `javax.activation.DataHandler` 象转换为实 `getInputStream` 例。
1. 将实 `java.io.InputSteam` 例写入表示加密PDF文档的PDF文件。

>[!NOTE]
>
>大多数AEM Forms服务操作都有SwaRef快速开始。 您可以在服务的相应快速视图部分开始这些快速开始。 例如，要查看“输出快速开始”部分，请参 [阅输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)。

**另请参阅**

[快速开始: 在Java项目中使用SwaRef调用服务](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## 通过HTTP使用BLOBAEM Forms调用 {#invoking-aem-forms-using-blob-data-over-http}

您可以使用Web服务调用AEM Forms服务并通过HTTP传递BLOB数据。 通过HTTP传递BLOB数据是一种替代技术，而不是使用base64编码、DIME或MIME。 例如，在使用Web服务增强3.0（不支持DIME或MIME）的Microsoft .NET项目中，可以通过HTTP传递数据。 通过HTTP使用BLOB数据时，在调用AEM Forms服务之前上传输入数据。

“通过HTTP使用BLOBAEM Forms调用”讨论通过HTTP传递BLOB数据来调用名为的以 `MyApplication/EncryptDocument` 下AEM Forms短期进程。

>[!NOTE]
>
>此过程不基于现有AEM Forms流程。 要与代码示例一起操作，请使用Workbench创建一个名 `MyApplication/EncryptDocument` 为的流程。 (请参 [阅使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

调用此进程时，它将执行以下操作：

1. 获取传递给该流程的不安全PDF文档。 此操作基于操 `SetValue` 作。 此进程的输入参数是一个名 `document` 为的进程变量 `inDoc`。
1. 用密码加密PDF文档。 此操作基于操 `PasswordEncryptPDF` 作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`。

>[!NOTE]
>
>建议您熟悉使用SOAP调用AEM Forms。 (请参 [阅使用Web服务调用AEM Forms](#invoking-aem-forms-using-web-services)。)

### 创建通过HTTP使用数据的。NET客户端程序集 {#creating-a-net-client-assembly-that-uses-data-over-http}

要创建通过HTTP使用数据的客户端程序集，请按照使用Base64编 [码调用AEM Forms中指定的过程](#invoking-aem-forms-using-base64-encoding)。 但是，请修改代理类中的URL以包含 `?blob=http` 而不是 `?blob=base64`。 此操作确保数据通过HTTP传递。 在代理类中，找到以下代码行：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

并将其更改为：

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**引用。NET clienMyApplication/EncryptDocument程序集**

将新的。NET客户端程序集放在要开发客户端应用程序的计算机上。 将。NET客户端程序集放置到目录后，可从项目中引用它。 从您的 `System.Web.Services` 项目引用库。 如果不引用此库，则无法使用。NET客户端程序集调用服务。

1. 在“项 **目** ”菜单中，选 **择“添加引用**”。
1. Click the **.NET** tab.
1. 单击 **“浏览** ”并找到DocumentService.dll文件。
1. 单击 **选择** ，然后单 **击确定**。

**使用通过HTTP使用BLOB数据的。NET客户端程序集调用服务**

您可以使用 `MyApplication/EncryptDocument` 通过HTTP使用数据的。NET客户端程序集调用服务（在Workbench中构建）。 要调用服 `MyApplication/EncryptDocument` 务，请执行以下步骤：

1. 创建。NET客户端程序集。
1. 引用Microsoft .NET客户端程序集。 创建客户端Microsoft .NET项目。 在客户端项目中引用Microsoft .NET客户端程序集。 也可参考 `System.Web.Services`。
1. 使用Microsoft .NET客户端程序集，通过调 `MyApplication_EncryptDocumentService` 用其默认构造函数创建对象。
1. 用对 `MyApplication_EncryptDocumentService` 象设置对 `Credentials` 象的属 `System.Net.NetworkCredential` 性。 在构造 `System.Net.NetworkCredential` 函数中，指定AEM表单用户名和相应的口令。 设置身份验证值，使您的。NET客户端应用程序能够与AEM Forms成功交换SOAP消息。
1. 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于将数据传递给 `MyApplication/EncryptDocument` 进程。
1. 为对象的数据成 `BLOB` 员指 `remoteURL` 定一个字符串值，它指定要传递给服务的PDF文档的URI `MyApplication/EncryptDocument`位置。
1. 通过调 `MyApplication/EncryptDocument` 用对象的方 `MyApplication_EncryptDocumentService` 法并传递 `invoke` 对象来调用 `BLOB` 进程。 此过程在对象中返回加密的PDF `BLOB` 文档。
1. 使用 `System.UriBuilder` 对象的构造函数并传递返回对象的数 `BLOB` 据成员 `remoteURL` 的值。
1. 将对象 `System.UriBuilder` 转换为对 `System.IO.Stream` 象。 (此列表后面的C#快速开始说明了如何执行此任务。)
1. 创建一个字节数组，并用该对象中的数据填充该 `System.IO.Stream` 数组。
1. 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
1. 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组内 `Write` 容写入PDF文件。

### 通过HTTP使用Java代理类和BLOB数据调用服务 {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

可以使用Java代理类和BLOBAEM Forms通过HTTP调用服务。 要使用Java代 `MyApplication/EncryptDocument` 理类调用服务，请执行以下步骤：

1. 使用使用服务WSDL的JAX-WS创建Java代 `MyApplication/EncryptDocument` 理类。 使用以下WSDL端点：

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   有关信息，请 [参阅使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws)。

   >[!NOTE]
   >
   >替 `hiro-xp` 换为 *承载AEM Forms的J2EE应用程序服务器的IP地址。*

1. 将使用JAX-WS创建的Java代理类打包到JAR文件中。
1. 在以下路径中包含Java代理JAR文件和JAR文件：

   &lt;安装目录>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   到Java客户端项目的类路径中。

1. 使用对 `MyApplicationEncryptDocumentService` 象的构造函数创建对象。
1. 通过 `MyApplicationEncryptDocument` 调用对象的 `MyApplicationEncryptDocumentService` 方法创建 `getEncryptDocument` 对象。
1. 通过为以下数据成员分配值来设置调用AEM Forms所需的连接值：

   * 将WSDL端点和编码类型指 `javax.xml.ws.BindingProvider` 定给对象 `ENDPOINT_ADDRESS_PROPERTY` 字段。 要使用BLOB `MyApplication/EncryptDocument` over HTTP编码调用服务，请指定以下URL值：

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * 将AEM表单用户分配 `javax.xml.ws.BindingProvider` 到对象的字 `USERNAME_PROPERTY` 段。
   * 为对象的字段指 `javax.xml.ws.BindingProvider` 定相应的口 `PASSWORD_PROPERTY` 令值。

   以下代码示例显示此应用程序逻辑：

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 使用对 `BLOB` 象的构造函数创建对象。
1. 通过调 `BLOB` 用对象的方法来填 `setRemoteURL` 充对象。 传递一个字符串值，它指定要传递给服务的PDF文档的URI `MyApplication/EncryptDocument` 位置。
1. 通过调 `MyApplication/EncryptDocument` 用对象的方 `MyApplicationEncryptDocument` 法并传递包 `invoke``BLOB` 含PDF文档的对象来调用该过程。 此过程在对象中返回加密的PDF `BLOB` 文档。
1. 创建一个字节数组以存储表示加密的PDF文档的数据流。 调用对 `BLOB` 象的方 `getRemoteURL` 法(使用 `BLOB` 方法返回的 `invoke` 对象)。
1. 使用对 `java.io.File` 象的构造函数创建对象。 此对象表示加密的PDF文档。
1. 使用对 `java.io.FileOutputStream` 象的构造函数并传递该对 `java.io.File` 象。
1. 调用 `java.io.FileOutputStream` 对象的方 `write` 法。 传递包含表示加密PDF文档的数据流的字节数组。

## 使用DIME调用AEM Forms {#invoking-aem-forms-using-dime}

您可以使用带附件的SOAP调用AEM Forms服务。 AEM Forms支持MIME和DIME Web服务标准。 DIME允许您发送二进制附件(如PDF文档)以及调用请求，而不是对附件进行编码。 使用 *DIME调用AEM Forms* 一节讨论调用以下AEM Forms短时进程(使用DIME `MyApplication/EncryptDocument` 命名)。

调用此进程时，它将执行以下操作：

1. 获取传递给该流程的不安全PDF文档。 此操作基于操 `SetValue` 作。 此进程的输入参数是一个名 `document` 为的进程变量 `inDoc`。
1. 用密码加密PDF文档。 此操作基于操 `PasswordEncryptPDF` 作。 密码加密的PDF文档在名为的进程变量中返回 `outDoc`。

此过程不基于现有AEM Forms流程。 要与代码示例一起使用，请创建一个使用Workbench命 `MyApplication/EncryptDocument` 名的流程。 (请参 [阅使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

>[!NOTE]
>
>已弃用使用DIME调用AEM Forms服务操作。 建议您使用MTOM。 (请参 [阅使用MTOM调用AEM Forms](#invoking-aem-forms-using-mtom)。)

### 创建使用DIME的。NET项目 {#creating-a-net-project-that-uses-dime}

要创建可使用DIME调用Forms服务的。NET项目，请执行以下任务:

* 在您的开发计算机上安装Web服务增强2.0。
* 从您的。NET项目中，创建对FormsAEM Forms服务的Web引用。

**安装Web服务增强2.0**

在开发计算机上安装Web Services Enhancements 2.0，并将其与Microsoft Visual Studio .NET集成。 您可以从Microsoft下载中心下载Web服 [务增强2.0。](https://www.microsoft.com/downloads/search.aspx)

从此网页中，搜索Web服务增强2.0并将其下载到开发计算机上。 此下载将名为Microsoft WSE 2.0 SPI.msi的文件放在您的计算机上。 运行安装项目并遵循联机指示。

>[!NOTE]
>
>Web服务增强2.0支持DIME。 使用Web服务增强2.0时，支持的Microsoft Visual Studio版本为2003。Web服务增强3.0不支持DIME; 但是，它支持MTOM。

**创建对AEM Forms服务的Web引用**

在开发计算机上安装Web服务增强2.0并创建Microsoft .NET项目后，请创建对Forms服务的Web引用。 例如，要创建对该过程的Web引 `MyApplication/EncryptDocument` 用并假设Forms安装在本地计算机上，请指定以下URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

创建Web引用后，可在。NET项目中使用以下两种代理数据类型： `EncryptDocumentService` 和 `EncryptDocumentServiceWse`。 要使用DIME `MyApplication/EncryptDocument` 调用进程，请使用 `EncryptDocumentServiceWse` 类型。

>[!NOTE]
>
>在创建对Forms服务的Web引用之前，请确保在项目中引用Web服务增强2.0。 （请参阅“安装Web服务增强2.0”。）

**引用WSE库**

1. 在“项目”菜单中，选择“添加引用”。
1. 在“添加引用”对话框中，选择Microsoft.Web.Services2.dll。
1. 选择System.Web.Services.dll。
1. 单击“选择”，然后单击“确定”。

**创建对Forms服务的Web引用**

1. 在“项目”菜单中，选择“添加Web引用”。
1. 在“URL”对话框中，指定Forms服务的URL。
1. 单击“Go”（开始），然后单击“Add Reference”（添加引用）。

>[!NOTE]
>
>确保启用。NET项目以使用WSE库。 在项目资源管理器中，右键单击项目名称并选择“启用WSE 2.0”。确保选中出现的对话框上的复选框。

**在。NET项目中使用DIME调用服务**

您可以使用DIME调用表单服务。 请考虑接 `MyApplication/EncryptDocument` 受不安全的PDF文档并返回口令加密的PDF文档的过程。 要使用DIME调 `MyApplication/EncryptDocument` 用进程，请执行以下步骤：

1. 创建一个Microsoft .NET项目，它允许您使用DIME调用Forms服务。 确保包含Web服务增强2.0并创建对AEM Forms服务的Web引用。
1. 在设置对进程的Web引 `MyApplication/EncryptDocument` 用后，使用 `EncryptDocumentServiceWse` 其默认构造函数创建对象。
1. 设置对 `EncryptDocumentServiceWse` 象的数 `Credentials` 据成员的值， `System.Net.NetworkCredential` 该值指定AEM表单用户名和口令值。
1. 使用对 `Microsoft.Web.Services2.Dime.DimeAttachment` 象的构造函数并传递以下值来创建对象：

   * 指定GUID值的字符串值。 可以通过调用方法获得GUID `System.Guid.NewGuid.ToString` 值。
   * 指定内容类型的字符串值。 由于此过程需要PDF文档，请指定 `application/pdf`。
   * 明细列表 `TypeFormat` 值。 Specify `TypeFormat.MediaType`.
   * 一个字符串值，它指定要传递到文档进程的PDFAEM Forms的位置。

1. 使用对 `BLOB` 象的构造函数创建对象。
1. 通过将对象的数据成 `BLOB` 员值分配给对 `Microsoft.Web.Services2.Dime.DimeAttachment` 象的数据成 `Id` 员，将DIME附 `BLOB` 件添加到 `attachmentID` 对象。
1. 调用方 `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` 法并传递对 `Microsoft.Web.Services2.Dime.DimeAttachment` 象。
1. 通过调 `MyApplication/EncryptDocument` 用对象的方 `EncryptDocumentServiceWse` 法并传递包 `invoke``BLOB` 含DIME附件的对象来调用进程。 此过程在对象中返回加密的PDF `BLOB` 文档。
1. 通过获取返回对象的数据成员的值，获 `BLOB` 取附件标 `attachmentID` 识符值。
1. 对位于中的附件进 `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` 行迭代，并使用附件标识符值获取加密的PDF文档。
1. 通过 `System.IO.Stream` 获取对象数据成 `Attachment` 员的值来获 `Stream` 取对象。
1. 创建一个字节数组并将该字节数组传递 `System.IO.Stream` 给对象的 `Read` 方法。 此方法使用表示加密的PDF文档的数据流填充字节数组。
1. 通过调 `System.IO.FileStream` 用对象的构造函数并传递表示PDF文件位置的字符串值来创建对象。 此对象表示加密的PDF文档。
1. 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
1. 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入PDF文件。

### 创建使用DIME的Apache Axis Java代理类 {#creating-apache-axis-java-proxy-classes-that-use-dime}

您可以使用Apache Axis WSDL2Java工具将服务WSDL转换为Java代理类，以便调用服务操作。 使用Apache Ant，您可以通过AEM Forms服务WSDL生成Axis库文件，它允许您调用服务。 (请参 [阅使用Apache Axis创建Java代理类](#creating-java-proxy-classes-using-apache-axis)。)

Apache Axis WSDL2Java工具生成JAVA文件，其中包含用于向服务发送SOAP请求的方法。 由服务接收的SOAP请求由Axis生成的库进行解码，并返回为方法和参数。

要使用轴 `MyApplication/EncryptDocument` 生成的库文件和DIME调用服务（在Workbench中构建），请执行以下步骤：

1. 使用Apache Axis创建使用服 `MyApplication/EncryptDocument` 务WSDL的Java代理类。 (请参 [阅使用Apache Axis创建Java代理类](#creating-java-proxy-classes-using-apache-axis)。)
1. 将Java代理类包含到类路径中。
1. 使用对 `MyApplicationEncryptDocumentServiceLocator` 象的构造函数创建对象。
1. 通过使 `URL` 用其构造函数并传递指定AEM Forms服务WSDL定义的字符串值，创建对象。 确保在SOAP `?blob=dime` 端点URL的末尾指定。 例如，使用

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. 通过调 `EncryptDocumentSoapBindingStub` 用对象的构造函数并传递对 `MyApplicationEncryptDocumentServiceLocator`象和对象来创 `URL` 建对象。
1. 通过调用对象和方法来设置AEM表单 `EncryptDocumentSoapBindingStub` 的用户名 `setUsername` 和口 `setPassword` 令值。

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. 通过创建对象检索要发 `MyApplication/EncryptDocument` 送到服务的PDF文档 `java.io.File` 符。 传递指定PDF文档位置的字符串值。
1. 使用对 `javax.activation.DataHandler` 象的构造函数并传递对象来创建 `javax.activation.FileDataSource` 对象。 可以 `javax.activation.FileDataSource` 通过使用其构造函数并传递表示PDF文档 `java.io.File` 的对象来创建该对象。
1. 使用对 `org.apache.axis.attachments.AttachmentPart` 象的构造函数并传递该对 `javax.activation.DataHandler` 象。
1. 通过调用对象的方 `EncryptDocumentSoapBindingStub` 法并传递 `addAttachment` 对象来附加 `org.apache.axis.attachments.AttachmentPart` 附件。
1. 使用对 `BLOB` 象的构造函数创建对象。 通过调 `BLOB` 用对象的方法并传递附件标识 `BLOB` 符值， `setAttachmentID` 用附件标识符值填充对象。 可通过调用对象的方法 `org.apache.axis.attachments.AttachmentPart` 来获取此 `getContentId` 值。
1. 通过调 `MyApplication/EncryptDocument` 用对象的方 `EncryptDocumentSoapBindingStub` 法来调用 `invoke` 进程。 传递 `BLOB` 包含DIME附件的对象。 此过程在对象中返回加密的PDF `BLOB` 文档。
1. 通过调用返回对象的方法获 `BLOB` 取附件标识符 `getAttachmentID` 值。 此方法返回一个字符串值，它表示返回的附件的标识符值。
1. 通过调用对象的方 `EncryptDocumentSoapBindingStub` 法检索附 `getAttachments` 件。 此方法返回表示附 `Objects` 件的数组。
1. 在附件（数组）中 `Object` 进行迭代，并使用附件标识符值获取加密的PDF文档。 每个元素都是一个 `org.apache.axis.attachments.AttachmentPart` 对象。
1. 通过调 `javax.activation.DataHandler` 用对象的方法，获取与附 `org.apache.axis.attachments.AttachmentPart` 件关联的 `getDataHandler` 对象。
1. 通过 `java.io.FileStream` 调用对象的方 `javax.activation.DataHandler` 法获取对 `getInputStream` 象。
1. 创建一个字节数组并将该字节数组传递 `java.io.FileStream` 给对象的 `read` 方法。 此方法使用表示加密的PDF文档的数据流填充字节数组。
1. 使用对 `java.io.File` 象的构造函数创建对象。 此对象表示加密的PDF文档。
1. 使用对 `java.io.FileOutputStream` 象的构造函数并传递该对 `java.io.File` 象。
1. 调用对 `java.io.FileOutputStream` 象的方 `write` 法并传递包含表示已加密PDF文档的数据流的字节数组。

**另请参阅**

[快速开始: 在Java项目中使用DIME调用服务](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## 使用基于SAML的身份验证 {#using-saml-based-authentication}

AEM Forms在调用服务时支持各种web服务身份验证模式。 一种身份验证模式是使用Web服务调用中的基本授权头指定用户名和密码值。 AEM Forms还支持基于SAML断言的身份验证。 当客户端应用程序使用Web服务调用AEM Forms服务时，客户端应用程序可以以下列方式之一提供身份验证信息：

* 作为基本授权的一部分传递凭据
* 作为WS-Security头的一部分传递用户名令牌
* 将SAML断言作为WS-Security头的一部分进行传递
* 作为WS-Security头的一部分传递Kerberos令牌

AEM Forms不支持标准的基于证书的身份验证，但支持不同形式的基于证书的身份验证。

>[!NOTE]
>
>“使用开始进行编程”中的Web服务快速AEM Forms指定用户名和口令值以执行授权。

AEM表单用户的标识可以通过使用密钥签名的SAML断言来表示。 以下XML代码显示SAML断言的示例。

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

* 它在特定持续时间内有效。
* 为特定用户发布。
* 已进行数字签名。 因此，对签名所做的任何修改都会破坏签名。
* 它可以作为与用户名和口令类似的用户标识的令牌呈现给AEM Forms。

客户端应用程序可以从任何返回对象的AEM FormsAuthenticationManager API中检索断 `AuthResult` 言。 您可以通过执 `AuthResult` 行以下两种方法之一获得实例：

* 使用AuthenticationManager API公开的任何验证方法验证用户身份。 通常，用户使用用户名和密码； 但是，您也可以使用证书身份验证。
* 使用方 `AuthenticationManager.getAuthResultOnBehalfOfUser` 法。 此方法允许客户端应用程序为任 `AuthResult` 何AEM表单用户获取对象。

AEM表单用户可以使用获取的SAML令牌进行身份验证。 此SAML断言（xml片段）可作为WS-Security头的一部分发送，该头包含用于用户身份验证的Web服务调用。 通常，客户端应用程序已对用户进行身份验证，但未存储用户凭据。 （或者用户已通过除使用用户名和密码之外的其他机制登录到该客户端。） 在这种情况下，客户端应用程序必须调用AEM Forms并模拟允许调用AEM Forms的特定用户。

要模拟特定用户，请使用 `AuthenticationManager.getAuthResultOnBehalfOfUser` Web服务调用方法。 此方法返回 `AuthResult` 包含该用户的SAML断言的实例。

然后，使用该SAML断言调用任何需要身份验证的服务。 此操作涉及将断言作为SOAP头的一部分进行发送。 当使用此断言进行Web服务调用时，AEM Forms将用户标识为由该断言表示的用户。 即，断言中指定的用户是调用服务的用户。

### 使用Apache Axis类和基于SAML的身份验证 {#using-apache-axis-classes-and-saml-based-authentication}

可以通过使用Axis库创建的Java代理类调用AEM Forms服务。 (请参 [阅使用Apache Axis创建Java代理类](#creating-java-proxy-classes-using-apache-axis)。)

当使用使用基于SAML的身份验证的AXIS时，请用Axis注册请求和响应处理程序。 Apache Axis在向AEM Forms发送调用请求之前调用该处理函数。 要注册处理程序，请创建扩展的Java类 `org.apache.axis.handlers.BasicHandler`。

**创建带轴的AssertionHandler**

以下名为的Java `AssertionHandler.java`类显示了扩展的Java类的示例 `org.apache.axis.handlers.BasicHandler`。

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

要向Axis注册处理程序，请创建client-config.wsdd文件。 默认情况下，Axis会查找具有此名称的文件。 以下XML代码是client-config.wsdd文件的示例。 有关详细信息，请参阅Axis文档。

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

### 使用。NET客户端程序集和基于SAML的身份验证 {#using-a-net-client-assembly-and-saml-based-authentication}

您可以通过使用。NET客户端程序集和基于SAML的身份验证来调用Forms服务。 为此，必须使用Web服务增强3.0(WSE)。 有关创建使用WSE的。NET客户端程序集的信息，请 [参阅创建使用DIME的。NET项目](#creating-a-net-project-that-uses-dime)。

>[!NOTE]
>
>DIME部分使用WSE 2.0。要使用基于SAML的身份验证，请按照与DIME主题中指定的相同说明操作。 但是，将WSE 2.0替换为WSE 3.0。在开发计算机上安装Web服务增强功能3.0，并将其与Microsoft Visual Studio .NET集成。 您可以从Microsoft下载中心下载Web服 [务增强3.0](https://www.microsoft.com/downloads/search.aspx)。

WSE体系结构使用策略、断言和SecurityToken数据类型。 对于Web服务调用，请简要指定策略。 策略可以有多个断言。 每个断言都可以包含过滤器。 在Web服务调用的特定阶段调用过滤器，当时，过滤器可以修改SOAP请求。 有关详细信息，请参阅Web服务增强3.0文档。

**创建断言和筛选器**

以下C#代码示例创建过滤器和断言类。 此代码示例创建一个SamlAssertionOutputFilter。 在将SOAP请求发送到AEM Forms之前，WSE框架会调用此过滤器。

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

创建一个类以表示SAML断言。 此类执行的主要任务是将数据值从字符串转换为xml并保留空格。 此断言xml稍后会导入到SOAP请求中。

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

使用Web服务调用某些AEM Forms服务操作时，有时会出现问题。 本讨论的目的是确定这些问题，并提供解决办法（如果有）。

### 异步调用服务操作 {#invoking-service-operations-asynchronously}

如果尝试异步调用AEM Forms服务操作（如“生成PDF”操作）, `htmlToPDF` 则会发 `SoapFaultException` 生。 要解决此问题，请创建一个自定义绑定XML文件，将元素和 `ExportPDF_Result` 其他元素映射到不同的类。 以下XML表示自定义绑定文件。

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

使用JAX-WS创建Java代理文件时，请使用此XML文件。 (请参 [阅使用JAX-WS创建Java代理类](#creating-java-proxy-classes-using-jax-ws)。)

使用——命令行选项执行JAX-WS工具(wsimport.exe)时，请引用此 `b` XML文件。 更新 `wsdlLocation` 绑定XML文件中的元素以指定AEM Forms的URL。

要确保异步调用正常工作，请修改端点URL值并指定 `async=true`。 例如，对于使用JAX-WS创建的Java代理文件，请为指定以下内容 `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`。

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

以下列表指定异步调用时需要自定义绑定文件的其他服务：

* PDFG3D
* 任务管理器
* 应用程序管理器
* 目录管理器
* Distiller
* 权限管理
* 文档管理

### J2EE应用程序服务器的差异 {#differences-in-j2ee-application-servers}

有时，使用特定J2EE应用程序服务器创建的代理库无法成功调用在其他J2EE应用程序服务器上托管的AEM Forms。 考虑使用WebSphere上部署的AEM Forms生成的代理库。 此代理库无法成功调用在JBoss应用程序服务器上部署的AEM Forms服务。

与JBoss Application Server相比，在WebSphere上部 `PrincipalReference`署AEM Forms时，某些AEM Forms复杂数据类型的定义方式不同。 不同J2EE应用程序服务使用的JDK中的差异是WSDL定义存在差异的原因。 因此，请使用从同一J2EE应用程序服务器生成的代理库。

### 使用Web服务访问多个服务 {#accessing-multiple-services-using-web-services}

由于命名空间冲突，数据对象无法在多个服务WSDL之间共享。 不同的服务可以共享数据类型，因此服务在WSDL中共享这些类型的定义。 例如，不能向同一。NET客户端项目添加包含数 `BLOB` 据类型的两个。NET客户端程序集。 如果尝试这样做，则会发生编译错误。

以下列表指定了无法在多个服务WSDL之间共享的数据类型：

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

为避免出现此问题，建议您完全限定数据类型。 例如，考虑一个。NET应用程序，它使用服务引用引用Forms服务和签名服务。 两个服务引用都将包含 `BLOB` 类。 要使用实 `BLOB` 例，请在声明对象 `BLOB` 时完全限定该对象。 下面的代码示例说明了这种方法。 有关此代码示例的信息，请参阅对交互 [式表单进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)。

以下C#代码示例对Forms服务呈现的交互式表单进行签名。 客户端应用程序有两个服务引用。 与 `BLOB` Forms服务关联的实例属于 `SignInteractiveForm.ServiceReference2` 命名空间。 同样， `BLOB` 与签名服务关联的实例属于 `SignInteractiveForm.ServiceReference1` 命名空间。 签名的交互式表单将保存为名为LoanXFASpided. *pdf的PDF文件*。

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

使用Microsoft .Net 3.5和WCF时，某些AEM Forms生成的代理类的名称不正确。 当为IBMFilenetContentRepositoryConnector、IDPShedulerService或其名称开始字母I的任何其他服务创建代理类时，会发生此问题。例如，在IBMFileNetContentRepositoryConnector的情况下，生成的客户端的名称为 `BMFileNetContentRepositoryConnectorClient`。 生成的代理类中缺少字母I。

