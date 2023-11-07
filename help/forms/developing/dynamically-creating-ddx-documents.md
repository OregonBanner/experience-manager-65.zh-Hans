---
title: 动态创建DDX文档
seo-title: Dynamically Creating DDX Documents
description: 使用Java API和Web服务API动态创建DDX文档。 通过动态创建DDX文档，可以使用在运行期间获取的DDX文档中的值。
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2162'
ht-degree: 0%

---

# 动态创建DDX文档 {#dynamically-creating-ddx-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

您可以动态创建可用于执行Assembler操作的DDX文档。 通过动态创建DDX文档，可以使用在运行期间获取的DDX文档中的值。 要动态创建DDX文档，请使用属于正在使用的编程语言的类。 例如，如果您使用Java开发客户端应用程序，请使用属于 `org.w3c.dom.*`包。 同样，如果您使用的是Microsoft .NET，请使用属于 `System.Xml` 命名空间。

在将DDX文档传递到Assembler服务之前，请将XML从 `org.w3c.dom.Document` 实例到 `com.adobe.idp.Document` 实例。 如果使用的是Web服务，则从用于创建XML的数据类型转换XML(例如， `XmlDocument`)到 `BLOB` 实例。

对于此讨论，假定已动态创建以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX文档可拆卸PDF文档。 建议您熟悉PDF文档的拆解。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的详细信息，请参见 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要使用动态创建的DDX文档拆分PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 创建DDX文档。
1. 转换DDX文档。
1. 设置运行时选项。
1. 拆分PDF文档。
1. 保存已拆解的PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，请先创建汇编程序服务客户端。

**创建DDX文档**

使用您正在使用的编程语言创建DDX文档。 要创建拆卸PDF文档的DDX文档，请确保它包含 `PDFsFromBookmarks` 元素。 将用于创建DDX文档的数据类型转换为 `com.adobe.idp.Document` 实例。 如果您使用的是Web服务，请将数据类型转换为 `BLOB` 实例。

**转换DDX文档**

使用创建的DDX文档 `org.w3c.dom` 类必须转换为 `com.adobe.idp.Document` 对象。 要在使用Java API时执行此任务，请使用Java XML转换类。 如果您使用的是Web服务，请将DDX文档转换为 `BLOB` 对象。

**引用要分解的PDF文档**

要拆分PDF文档，请引用表示要拆分PDF文档的PDF文件。 当传递到Assembler服务时，将为文档中的每个1级书签返回一个单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。 要设置运行时选项，请使用 `AssemblerOptionSpec` 对象。

**拆分PDF文档**

PDF通过调用 `invokeDDX` 操作。 传递动态创建的DDX文档。 Assembler服务返回集合对象中已拆解的PDF文档。

**保存已拆解的PDF文档**

所有已拆解的PDF文档都会在集合对象中返回。 循环访问收藏集对象并将每个PDF文档另存为PDF文件。

**另请参阅**

[使用Java API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用Web服务API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式拆分PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API动态创建DDX文档 {#dynamically-create-a-ddx-document-using-the-java-api}

使用Assembler服务API (Java)动态创建DDX文档并拆分PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 创建DDX文档。

   * 创建Java `DocumentBuilderFactory` 对象，方法是 `DocumentBuilderFactory` 类&#39; `newInstance` 方法。
   * 创建Java `DocumentBuilder` 对象，方法是 `DocumentBuilderFactory` 对象的 `newDocumentBuilder` 方法。
   * 调用 `DocumentBuilder` 对象的 `newDocument` 实例化的方法 `org.w3c.dom.Document` 对象。
   * 通过调用 `org.w3c.dom.Document` 对象的 `createElement` 方法。 此方法创建 `Element` 表示根元素的对象。 将表示元素名称的字符串值传递给 `createElement` 方法。 将返回值强制转换为 `Element`. 接下来，通过调用其子元素的 `setAttribute` 方法。 最后，通过调用标头元素的 `appendChild` 方法，并将子元素对象作为参数传递。 以下代码行显示此应用程序逻辑：
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 创建 `PDFsFromBookmarks` 元素，方法是调用 `Document` 对象的 `createElement` 方法。 将表示元素名称的字符串值传递给 `createElement` 方法。 将返回值强制转换为 `Element`. 为设置值 `PDFsFromBookmarks` 元素(通过调用其 `setAttribute` 方法。 附加 `PDFsFromBookmarks` 元素到 `DDX` 元素(通过调用DDX元素的 `appendChild` 方法。 传递 `PDFsFromBookmarks` 元素对象。 以下代码行显示此应用程序逻辑：

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 创建 `PDF` 元素，方法是调用 `Document` 对象的 `createElement` 方法。 传递表示元素名称的字符串值。 将返回值强制转换为 `Element`. 为设置值 `PDF` 元素(通过调用其 `setAttribute` 方法。 附加 `PDF` 元素到 `PDFsFromBookmarks` 元素，方法是调用 `PDFsFromBookmarks` 元素的 `appendChild` 方法。 传递 `PDF` 元素对象。 以下代码行显示了此应用程序逻辑：

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 转换DDX文档。

   * 创建 `javax.xml.transform.Transformer` 对象，方法是调用 `javax.xml.transform.Transformer` 对象的静态 `newInstance` 方法。
   * 创建 `Transformer` 对象，方法是调用 `TransformerFactory` 对象的 `newTransformer` 方法。
   * 创建 `ByteArrayOutputStream` 对象。
   * 创建 `javax.xml.transform.dom.DOMSource` 对象。 传递 `org.w3c.dom.Document` 表示DDX文档的对象。
   * 创建 `javax.xml.transform.dom.DOMSource` 对象，使用它的构造函数传递 `ByteArrayOutputStream` 对象。
   * 填充Java `ByteArrayOutputStream` 对象，方法是调用 `javax.xml.transform.Transformer` 对象的 `transform` 方法。 传递 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 对象。
   * 创建字节数组并分配 `ByteArrayOutputStream` 对象。
   * 通过调用 `ByteArrayOutputStream` 对象的 `toByteArray` 方法。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递字节数组。

1. 参照要拆解的PDF文档。

   * 创建 `java.util.Map` 通过使用PDF存储输入文档的对象 `HashMap` 构造函数。
   * 创建 `java.io.FileInputStream` 对象通过构造函数传递PDF文件的位置进行拆解。
   * 创建 `com.adobe.idp.Document` 对象。 传递 `java.io.FileInputStream` 包含要拆解的PDF文档的对象。
   * 将条目添加到 `java.util.Map` 对象(通过调用其 `put` 方法并传递以下参数：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的PDF源元素的值匹配。 (在动态创建的DDX文档中，值为 `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` 包含要拆解的PDF文档的对象。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象的 `setFailOnError` 方法和路径 `false`.

1. 拆分PDF文档。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法并传递以下值：

   * A `com.adobe.idp.Document` 表示动态创建的DDX文档的对象
   * A `java.util.Map` 包含要拆解的PDF文档的对象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象

   此 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已拆卸PDF文档以及发生的任何异常的对象。

1. 保存已拆解的PDF文档。

   要获取已拆解的PDF文档，请执行以下步骤：

   * 调用 `AssemblerResult` 对象的 `getDocuments` 方法。 此方法会返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果为止 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于提取PDF文档的方法。

**另请参阅**

[快速入门（SOAP模式）：使用Java API动态创建DDX文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API动态创建DDX文档 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用Assembler服务API（Web服务）动态创建DDX文档并拆分PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 在设置服务引用时，请确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象使用默认构造函数。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 创建DDX文档。

   * 创建 `System.Xml.XmlElement` 对象。
   * 通过调用 `XmlElement` 对象的 `CreateElement` 方法。 此方法创建 `Element` 表示根元素的对象。 将表示元素名称的字符串值传递给 `CreateElement` 方法。 通过调用DDX元素的 `SetAttribute` 方法。 最后，通过调用 `XmlElement` 对象的 `AppendChild` 方法。 将DDX对象作为参数传递。 以下代码行显示此应用程序逻辑：

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 创建DDX文档的 `PDFsFromBookmarks` 元素，方法是调用 `XmlElement` 对象的 `CreateElement` 方法。 将表示元素名称的字符串值传递给 `CreateElement` 方法。 接下来，通过调用元素的属性来为其设置值 `SetAttribute` 方法。 附加 `PDFsFromBookmarks` 元素到根元素，方法是调用 `DDX` 元素的 `AppendChild` 方法。 传递 `PDFsFromBookmarks` 元素对象。 以下代码行显示此应用程序逻辑：

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 创建DDX文档的 `PDF` 元素，方法是调用 `XmlElement` 对象的 `CreateElement` 方法。 将表示元素名称的字符串值传递给 `CreateElement` 方法。 接下来，通过调用其子元素的 `SetAttribute` 方法。 附加 `PDF` 元素到 `PDFsFromBookmarks` 元素，方法是调用 `PDFsFromBookmarks` 元素的 `AppendChild` 方法。 传递 `PDF` 元素对象。 以下代码行显示了此应用程序逻辑：

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 转换DDX文档。

   * 创建 `System.IO.MemoryStream` 对象。
   * 填充 `MemoryStream` 对象的DDX文档 `XmlElement` 表示DDX文档的对象。 调用 `XmlElement` 对象的 `Save` 方法并传递 `MemoryStream` 对象。
   * 创建字节数组，并在其中填充数据 `MemoryStream` 对象。 以下代码显示此应用程序逻辑：

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 创建 `BLOB` 对象。 将字节数组分配给 `BLOB` 对象的 `MTOM` 字段。

1. 参照要拆解的PDF文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储输入PDF文档。 此 `BLOB` 对象被传递到 `invokeOneDocument` 作为论据。
   * 创建 `System.IO.FileStream` 对象通过调用其构造函数。 传递一个字符串值，该值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 属性字节数组的内容。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过为属于以下对象的数据成员分配值，设置运行时选项以满足您的业务要求 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请分配 `false` 到 `AssemblerOptionSpec` 对象的 `failOnError` 数据成员。

1. 拆分PDF文档。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示动态创建的DDX文档的对象
   * 此 `mapItem` 包含输入PDF文档的数组
   * An `AssemblerOptionSpec` 指定运行时选项的对象

   此 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和发生的任何异常的对象。

1. 保存已拆解的PDF文档。

   要获取新创建的PDF文档，请执行以下步骤：

   * 访问 `AssemblerResult` 对象的 `documents` 字段，即 `Map` 包含已拆卸PDF文档的对象。
   * 循环访问 `Map` 对象以获取每个结果文档。 然后，强制转换该数组成员的 `value` 到 `BLOB`.
   * 通过访问代表PDF文档的二进制数据 `BLOB` 对象的 `MTOM` 属性。 这会返回一个字节数组，您可以将该字节写出到PDF文件中。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
