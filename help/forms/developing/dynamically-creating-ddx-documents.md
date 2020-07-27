---
title: 动态创建DDX文档
seo-title: 动态创建DDX文档
description: 'null'
seo-description: 'null'
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 0%

---


# 动态创建DDX文档 {#dynamically-creating-ddx-documents}

您可以动态创建DDX文档，它可用于执行Assembler操作。 动态创建DDX文档使您能够在DDX文档中使用在运行时获得的值。 要动态创建DDX文档，请使用属于您所使用的编程语言的类。 例如，如果您使用Java开发客户端应用程序，请使用属于该包的 `org.w3c.dom.*`类。 同样，如果您使用的是Microsoft .NET，则使用属于该命名空间的 `System.Xml` 类。

在将DDX文档传递到Assembler服务之前，请将XML从实例 `org.w3c.dom.Document` 转换为实 `com.adobe.idp.Document` 例。 如果您使用Web服务，请将XML从用于创建XML（例如）的数据类型转 `XmlDocument`换为实 `BLOB` 例。

对于此讨论，假定动态创建以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX文档拆解PDF文档。 建议您熟悉反汇编PDF文档。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参 [阅Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要使用动态创建的DDX文档反汇编PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 创建DDX文档。
1. 转换DDX文档。
1. 设置运行时选项。
1. 反汇编PDF文档。
1. 保存已拆解的PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时需要)

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，请先创建Assembler服务客户端。

**创建DDX文档**

使用您所使用的编程语言创建DDX文档。 要创建分解PDF文档的DDX文档，请确保它包含该元 `PDFsFromBookmarks` 素。 如果您使用Java API，则将用于创建DDX文档 `com.adobe.idp.Document` 的类型转换为实例。 如果您使用Web服务，请将数据类型转换为实 `BLOB` 例。

**转换DDX文档**

必须使用类创建的DDX文档 `org.w3c.dom` 必须转换为对 `com.adobe.idp.Document` 象。 要在使用Java API时执行此任务，请使用Java XML转换类。 如果您使用Web服务，请将DDX文档转换为对 `BLOB` 象。

**参考PDF文档进行反汇编**

要反汇编PDF文档，请参考表示要反汇编的PDF文档的PDF文件。 传递到Assembler服务时，将为文档中的每个1级书签返回单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 要设置运行时选项，请使用对 `AssemblerOptionSpec` 象。

**反汇编PDF文档**

通过调用操作反汇编PDF `invokeDDX` 文档。 传递动态创建的DDX文档。 Assembler服务在集合对象中返回已拆解的PDF文档。

**保存已拆卸的PDF文档**

所有已拆卸的PDF文档都会在集合对象中返回。 对集合对象进行迭代，并将每个PDF文档另存为PDF文件。

**另请参阅**

[使用Java API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用Web服务API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式反汇编PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API动态创建DDX文档 {#dynamically-create-a-ddx-document-using-the-java-api}

使用Assembler Service API(Java)动态创建DDX文档并反汇编PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 创建DDX文档。

   * 通过调 `DocumentBuilderFactory` 用类的方法 `DocumentBuilderFactory` 创建Java `newInstance` 对象。
   * 通过调 `DocumentBuilder` 用对象的方 `DocumentBuilderFactory` 法创建Java `newDocumentBuilder` 对象。
   * 调用 `DocumentBuilder` 对象的方 `newDocument` 法来实例化 `org.w3c.dom.Document` 对象。
   * 通过调用对象的方法创建DDX文档 `org.w3c.dom.Document` 的根元 `createElement` 素。 此方法创建 `Element` 一个表示根元素的对象。 将表示元素名称的字符串值传递给该 `createElement` 方法。 将返回值转换为 `Element`。 然后，通过调用子元素的方法为其设置 `setAttribute` 值。 最后，通过调用标题元素的方法将元素追加到标 `appendChild` 题元素，并将子元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 通过 `PDFsFromBookmarks` 调用对象的方 `Document` 法创建元 `createElement` 素。 将表示元素名称的字符串值传递给该 `createElement` 方法。 将返回值转换为 `Element`。 通过调用元素 `PDFsFromBookmarks` 的方法来设置 `setAttribute` 值。 通过 `PDFsFromBookmarks` 调用DDX元 `DDX` 素的方法将元素追加到元 `appendChild` 素。 将元素 `PDFsFromBookmarks` 对象作为参数进行传递。 以下几行代码显示此应用程序逻辑：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 通过 `PDF` 调用对象的方 `Document` 法创建元 `createElement` 素。 传递表示元素名称的字符串值。 将返回值转换为 `Element`。 通过调用元素 `PDF` 的方法来设置 `setAttribute` 值。 通过调 `PDF` 用元素 `PDFsFromBookmarks` 的方法将元 `PDFsFromBookmarks` 素追加到元 `appendChild` 素。 将元素 `PDF` 对象作为参数进行传递。 以下几行代码显示此应用程序逻辑：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 转换DDX文档。

   * 通过 `javax.xml.transform.Transformer` 调用对象的 `javax.xml.transform.Transformer` 静态方法创建 `newInstance` 对象。
   * 通过 `Transformer` 调用对象的 `TransformerFactory` 方法创建 `newTransformer` 对象。
   * 使用对 `ByteArrayOutputStream` 象的构造函数创建对象。
   * 使用对 `javax.xml.transform.dom.DOMSource` 象的构造函数创建对象。 传递 `org.w3c.dom.Document` 表示DDX文档的对象。
   * 使用对 `javax.xml.transform.dom.DOMSource` 象的构造函数并传递该对 `ByteArrayOutputStream` 象。
   * 通过调 `ByteArrayOutputStream` 用对象的方 `javax.xml.transform.Transformer` 法填充Java `transform` 对象。 传递 `javax.xml.transform.dom.DOMSource` 和对 `javax.xml.transform.stream.StreamResult` 象。
   * 创建一个字节数组，并将对象的大 `ByteArrayOutputStream` 小分配给字节数组。
   * 通过调用对象的方 `ByteArrayOutputStream` 法填充字节 `toByteArray` 数组。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递字节数组来创建对象。

1. 参考PDF文档进行反汇编。

   * 使用构 `java.util.Map` 造函数创建用于存储输入PDF文档的对 `HashMap` 象。
   * 通过使用 `java.io.FileInputStream` 其构造函数并将PDF文档的位置传递给反汇编，从而创建对象。
   * 创建对 `com.adobe.idp.Document` 象。 将包含 `java.io.FileInputStream` PDF文档的对象传递到反汇编。
   * 通过调用对象的方 `java.util.Map` 法并传递以 `put` 下参数，向对象添加一个条目：

      * 表示键名称的字符串值。 此值必须与在DDX文档中指定的PDF源元素值匹配。 (在动态创建的DDX文档中，值为 `AssemblerResultPDF.pdf`。)
      * 包 `com.adobe.idp.Document` 含要反汇编的PDF文档的对象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调 `AssemblerOptionSpec` 用对象的 `setFailOnError` 方法并传递 `false`。

1. 反汇编PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` 动态创建的DDX文档的对象
   * 包含 `java.util.Map` 要反汇编的PDF文档的对象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象

   该方 `invokeDDX` 法返回一 `com.adobe.livecycle.assembler.client.AssemblerResult` 个对象，其中包含已分解的PDF文档和发生的任何例外。

1. 保存已拆解的PDF文档。

   要获取已分解的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 此方法返回一个 `java.util.Map` 对象。
   * 遍历对象 `java.util.Map` ，直到找到生成的对 `com.adobe.idp.Document` 象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。

**另请参阅**

[快速开始（SOAP模式）: 使用Java API动态创建DDX文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API动态创建DDX文档 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用Assembler Service API（Web服务）动态创建DDX文档并反汇编PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 请确保在设置服务引用时使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用对象 `AssemblerServiceClient` 的默认构造函数创建对象。
   * 使用构 `AssemblerServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `AssemblerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 创建DDX文档。

   * 使用对 `System.Xml.XmlElement` 象的构造函数创建对象。
   * 通过调用对象的方法创建DDX文档 `XmlElement` 的根元 `CreateElement` 素。 此方法创建 `Element` 一个表示根元素的对象。 将表示元素名称的字符串值传递给该 `CreateElement` 方法。 通过调用DDX元素的方法为其设置 `SetAttribute` 值。 最后，通过调用对象的方法将元素追加 `XmlElement` 到DDX文档 `AppendChild` 中。 将DDX对象作为参数进行传递。 以下几行代码显示此应用程序逻辑：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 通过调用对 `PDFsFromBookmarks` 象的方法创 `XmlElement` 建DDX文档的 `CreateElement` 元素。 将表示元素名称的字符串值传递给该 `CreateElement` 方法。 接下来，通过调用元素的方法来设置该元素 `SetAttribute` 的值。 通过 `PDFsFromBookmarks` 调用元素的方法，将元素 `DDX` 追加到根元 `AppendChild` 素。 将元素 `PDFsFromBookmarks` 对象作为参数进行传递。 以下几行代码显示此应用程序逻辑：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 通过调用对 `PDF` 象的方法创 `XmlElement` 建DDX文档的 `CreateElement` 元素。 将表示元素名称的字符串值传递给该 `CreateElement` 方法。 然后，通过调用子元素的方法为其设置 `SetAttribute` 值。 通过调 `PDF` 用元素 `PDFsFromBookmarks` 的方法将元 `PDFsFromBookmarks` 素追加到元 `AppendChild` 素。 将元素 `PDF` 对象作为参数进行传递。 以下几行代码显示此应用程序逻辑：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 转换DDX文档。

   * 使用对 `System.IO.MemoryStream` 象的构造函数创建对象。
   * 使用 `MemoryStream` 表示DDX文档的对象， `XmlElement` 用DDX文档填充对象。 调用 `XmlElement` 对象的方 `Save` 法并传递对 `MemoryStream` 象。
   * 创建一个字节数组，并用该对象中的数据填充 `MemoryStream` 它。 以下代码显示此应用程序逻辑：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 创建对 `BLOB` 象。 将字节数组指 `BLOB` 定给对象的 `MTOM` 字段。

1. 参考PDF文档进行反汇编。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储输入的PDF文档。 此 `BLOB` 对象作为参 `invokeOneDocument` 数传递给。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取 `System.IO.FileStream` 的字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的属性 `MTOM` 指定字节数组的内容来填充对象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请 `false` 指定 `AssemblerOptionSpec` 对象的数据 `failOnError` 成员。

1. 反汇编PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `BLOB` 动态创建的DDX文档的对象
   * 包 `mapItem` 含输入PDF文档的数组
   * 指定 `AssemblerOptionSpec` 运行时选项的对象

   方 `invokeDDX` 法返回一 `AssemblerResult` 个对象，其中包含作业的结果和发生的任何异常。

1. 保存已拆解的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含已 `Map` 拆解的PDF文档的对象。
   * 对对象进行 `Map` 迭代以获得每个生成文档。 然后，将该阵列成员 `value` 转换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示PDF `BLOB` 的二进制 `MTOM` 数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
