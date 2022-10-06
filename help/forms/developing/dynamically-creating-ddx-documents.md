---
title: 动态创建DDX文档
seo-title: Dynamically Creating DDX Documents
description: 使用Java API和Web服务API动态创建DDX文档。 通过动态创建DDX文档，可以使用在运行时获取的DDX文档值。
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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# 动态创建DDX文档 {#dynamically-creating-ddx-documents}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以动态创建可用于执行汇编程序操作的DDX文档。 通过动态创建DDX文档，可以使用在运行时获取的DDX文档值。 要动态创建DDX文档，请使用属于您所使用的编程语言的类。 例如，如果您使用Java开发客户端应用程序，则使用属于 `org.w3c.dom.*`包。 同样，如果您使用的是Microsoft .NET，则使用属于 `System.Xml` 命名空间。

在将DDX文档传递到汇编程序服务之前，请先将XML从 `org.w3c.dom.Document` 实例 `com.adobe.idp.Document` 实例。 如果您使用Web服务，请从用于创建XML的数据类型转换XML(例如， `XmlDocument`) `BLOB` 实例。

对于此讨论，假定已动态创建以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX文档将分解PDF文档。 建议您熟悉拆分PDF文档。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要使用动态创建的DDX文档来拆解PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 创建DDX文档。
1. 转换DDX文档。
1. 设置运行时选项。
1. 拆解PDF文档。
1. 保存已拆卸的PDF文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，请创建汇编程序服务客户端。

**创建DDX文档**

使用您使用的编程语言创建DDX文档。 要创建分解PDF文档的DDX文档，请确保它包含 `PDFsFromBookmarks` 元素。 将用于创建DDX文档的数据类型转换为 `com.adobe.idp.Document` 实例。 如果您使用Web服务，请将数据类型转换为 `BLOB` 实例。

**转换DDX文档**

使用 `org.w3c.dom` 类必须转换为 `com.adobe.idp.Document` 对象。 要在使用Java API时执行此任务，请使用Java XML转换类。 如果您使用Web服务，请将DDX文档转换为 `BLOB` 对象。

**引用PDF文档以拆解**

要拆解PDF文档，请引用表示要拆解的PDF文档的PDF文件。 当传递到汇编程序服务时，将为文档中的每个1级书签返回单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。 要设置运行时选项，请使用 `AssemblerOptionSpec` 对象。

**拆解PDF文档**

通过调用 `invokeDDX` 操作。 传递动态创建的DDX文档。 汇编程序服务返回集合对象中的已拆卸PDF文档。

**保存已拆卸的PDF文档**

所有已拆卸的PDF文档都在收集对象中返回。 遍历收集对象，并将每个PDF文档另存为PDF文件。

**另请参阅**

[使用Java API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用Web服务API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式拆分PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API动态创建DDX文档 {#dynamically-create-a-ddx-document-using-the-java-api}

使用汇编程序服务API(Java)动态创建DDX文档并反汇编PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 创建DDX文档。

   * 创建Java `DocumentBuilderFactory` 对象 `DocumentBuilderFactory` class&#39; `newInstance` 方法。
   * 创建Java `DocumentBuilder` 对象 `DocumentBuilderFactory` 对象 `newDocumentBuilder` 方法。
   * 调用 `DocumentBuilder` 对象 `newDocument` 实例化方法 `org.w3c.dom.Document` 对象。
   * 通过调用 `org.w3c.dom.Document` 对象 `createElement` 方法。 此方法将创建 `Element` 表示根元素的对象。 将表示元素名称的字符串值传递到 `createElement` 方法。 将返回值转换为 `Element`. 接下来，通过调用子元素的 `setAttribute` 方法。 最后，通过调用标头元素的 `appendChild` 方法，并将子元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 创建 `PDFsFromBookmarks` 元素 `Document` 对象 `createElement` 方法。 将表示元素名称的字符串值传递到 `createElement` 方法。 将返回值转换为 `Element`. 为 `PDFsFromBookmarks` 元素 `setAttribute` 方法。 附加 `PDFsFromBookmarks` 元素 `DDX` 元素(通过调用 `appendChild` 方法。 传递 `PDFsFromBookmarks` 元素对象。 以下几行代码显示此应用程序逻辑：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 创建 `PDF` 元素 `Document` 对象 `createElement` 方法。 传递表示元素名称的字符串值。 将返回值转换为 `Element`. 为 `PDF` 元素 `setAttribute` 方法。 附加 `PDF` 元素 `PDFsFromBookmarks` 元素 `PDFsFromBookmarks` 元素 `appendChild` 方法。 传递 `PDF` 元素对象。 下面几行代码显示此应用程序逻辑：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 转换DDX文档。

   * 创建 `javax.xml.transform.Transformer` 对象 `javax.xml.transform.Transformer` 对象的静态 `newInstance` 方法。
   * 创建 `Transformer` 对象 `TransformerFactory` 对象 `newTransformer` 方法。
   * 创建 `ByteArrayOutputStream` 对象。
   * 创建 `javax.xml.transform.dom.DOMSource` 对象。 传递 `org.w3c.dom.Document` 表示DDX文档的对象。
   * 创建 `javax.xml.transform.dom.DOMSource` 对象，并使用其构造函数进行传递 `ByteArrayOutputStream` 对象。
   * 填充Java `ByteArrayOutputStream` 对象 `javax.xml.transform.Transformer` 对象 `transform` 方法。 传递 `javax.xml.transform.dom.DOMSource` 和 `javax.xml.transform.stream.StreamResult` 对象。
   * 创建字节数组并分配 `ByteArrayOutputStream` 对象。
   * 通过调用 `ByteArrayOutputStream` 对象 `toByteArray` 方法。
   * 创建 `com.adobe.idp.Document` 对象。

1. 引用要拆解的PDF文档。

   * 创建 `java.util.Map` 用于通过使用 `HashMap` 构造函数。
   * 创建 `java.io.FileInputStream` 对象，并将PDF文档的位置传递到反汇编。
   * 创建 `com.adobe.idp.Document` 对象。 传递 `java.io.FileInputStream` 包含要拆解的PDF文档的对象。
   * 在 `java.util.Map` 通过调用对象 `put` 方法和传递以下参数：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。 (在动态创建的DDX文档中，值为 `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` 包含要拆解的PDF文档的对象。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象 `setFailOnError` 方法和传递 `false`.

1. 拆解PDF文档。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法并传递以下值：

   * A `com.adobe.idp.Document` 表示动态创建的DDX文档的对象
   * A `java.util.Map` 包含要拆解的PDF文档的对象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已拆卸PDF文档和发生的任何例外的对象。

1. 保存已拆卸的PDF文档。

   要获取已拆卸的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象 `getDocuments` 方法。 此方法将返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法提取PDF文档。

**另请参阅**

[快速入门（SOAP模式）：使用Java API动态创建DDX文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API动态创建DDX文档 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用汇编程序服务API（Web服务）动态创建DDX文档并拆解PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 在设置服务引用时，请确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 创建DDX文档。

   * 创建 `System.Xml.XmlElement` 对象。
   * 通过调用 `XmlElement` 对象 `CreateElement` 方法。 此方法将创建 `Element` 表示根元素的对象。 将表示元素名称的字符串值传递到 `CreateElement` 方法。 通过调用DDX元素的 `SetAttribute` 方法。 最后，通过调用 `XmlElement` 对象 `AppendChild` 方法。 将DDX对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 创建DDX文档的 `PDFsFromBookmarks` 元素 `XmlElement` 对象 `CreateElement` 方法。 将表示元素名称的字符串值传递到 `CreateElement` 方法。 接下来，通过调用 `SetAttribute` 方法。 附加 `PDFsFromBookmarks` 元素到根元素，方法是通过调用 `DDX` 元素 `AppendChild` 方法。 传递 `PDFsFromBookmarks` 元素对象。 以下几行代码显示此应用程序逻辑：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 创建DDX文档的 `PDF` 元素 `XmlElement` 对象 `CreateElement` 方法。 将表示元素名称的字符串值传递到 `CreateElement` 方法。 接下来，通过调用子元素的 `SetAttribute` 方法。 附加 `PDF` 元素 `PDFsFromBookmarks` 元素 `PDFsFromBookmarks` 元素 `AppendChild` 方法。 传递 `PDF` 元素对象。 下面几行代码显示此应用程序逻辑：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 转换DDX文档。

   * 创建 `System.IO.MemoryStream` 对象。
   * 填充 `MemoryStream` 对象与DDX文档的对象(使用 `XmlElement` 表示DDX文档的对象。 调用 `XmlElement` 对象 `Save` 方法和通过 `MemoryStream` 对象。
   * 创建一个字节数组，并使用位于 `MemoryStream` 对象。 以下代码显示此应用程序逻辑：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 创建 `BLOB` 对象。 将字节数组分配给 `BLOB` 对象 `MTOM` 字段。

1. 引用要拆解的PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储输入PDF文档。 此 `BLOB` 对象被传递到 `invokeOneDocument` 作为参数。
   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，该值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性字节数组的内容。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过为属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请指定 `false` 到 `AssemblerOptionSpec` 对象 `failOnError` 数据成员。

1. 拆解PDF文档。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示动态创建的DDX文档的对象
   * 的 `mapItem` 包含输入PDF文档的数组
   * 安 `AssemblerOptionSpec` 指定运行时选项的对象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和发生的任何例外的对象。

1. 保存已拆卸的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问 `AssemblerResult` 对象 `documents` 字段， `Map` 包含已拆卸的PDF文档的对象。
   * 循环访问 `Map` 对象来获取每个生成文档。 然后，将该阵列成员的 `value` 至 `BLOB`.
   * 通过访问表示PDF文档的二进制数据 `BLOB` 对象 `MTOM` 属性。 这会返回一个字节数组，您可以将其写出到PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
