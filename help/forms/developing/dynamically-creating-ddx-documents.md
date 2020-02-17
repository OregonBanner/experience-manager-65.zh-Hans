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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 动态创建DDX文档 {#dynamically-creating-ddx-documents}

您可以动态创建可用于执行汇编程序操作的DDX文档。 动态创建DDX文档使您能够在DDX文档中使用在运行时获取的值。 要动态创建DDX文档，请使用属于您所使用的编程语言的类。 例如，如果您使用Java开发客户端应用程序，请使用属于该包的 `org.w3c.dom.*`类。 同样，如果您使用的是Microsoft .NET，则使用属于命名空间的 `System.Xml` 类。

在将DDX文档传递到Assembler服务之前，请将XML从实例转 `org.w3c.dom.Document` 换为实 `com.adobe.idp.Document` 例。 如果您使用Web服务，请将XML从用于创建XML的数据类型(例如， `XmlDocument`)转换为实 `BLOB` 例。

对于此讨论，假定以下DDX文档是动态创建的。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX文档拆分了PDF文档。 建议您熟悉PDF文档的拆解。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要使用动态创建的DDX文档反汇编PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 创建DDX文档。
1. 转换DDX文档。
1. 设置运行时选项。
1. 反汇编PDF文档。
1. 保存已拆卸的PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，请先创建Assembler服务客户端。

**创建DDX文档**

使用您所使用的编程语言创建DDX文档。 要创建拆分PDF文档的DDX文档，请确保它包含该元 `PDFsFromBookmarks` 素。 如果您使用Java API，则将用于创建DDX文档的 `com.adobe.idp.Document` 数据类型转换为实例。 如果您使用Web服务，请将数据类型转换为实 `BLOB` 例。

**转换DDX文档**

必须使用类创建的DDX文 `org.w3c.dom` 档必须转换为对 `com.adobe.idp.Document` 象。 要在使用Java API时执行此任务，请使用Java XML转换类。 如果您使用Web服务，请将DDX文档转换为对 `BLOB` 象。

**引用PDF文档进行反汇编**

要反汇编PDF文档，请引用表示要反汇编的PDF文档的PDF文件。 当传递给Assembler服务时，文档中每个1级书签将返回一个单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，这些选项控制Assembler服务在执行作业时的行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 要设置运行时选项，请使用对 `AssemblerOptionSpec` 象。

**反汇编PDF文档**

通过调用操作反汇编PDF文 `invokeDDX` 档。 传递动态创建的DDX文档。 Assembler服务返回集合对象中已拆解的PDF文档。

**保存已拆卸的PDF文档**

所有已拆卸的PDF文档都会返回到一个集合对象中。 遍历集合对象并将每个PDF文档另存为PDF文件。

**另请参阅**

[使用Java API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用Web服务API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式拆解PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API动态创建DDX文档 {#dynamically-create-a-ddx-document-using-the-java-api}

使用Assembler Service API(Java)动态创建DDX文档并反汇编PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 创建DDX文档。

   * 通过调用 `DocumentBuilderFactory` 类的方法创建 `DocumentBuilderFactory` 一个Java `newInstance` 对象。
   * 通过调 `DocumentBuilder` 用对象的方 `DocumentBuilderFactory` 法创建Java对 `newDocumentBuilder` 象。
   * 调用对 `DocumentBuilder` 象的方 `newDocument` 法来实例化对 `org.w3c.dom.Document` 象。
   * 通过调用对象的方法创建DDX文档 `org.w3c.dom.Document` 的根元 `createElement` 素。 此方法创建 `Element` 一个表示根元素的对象。 将表示元素名称的字符串值传递给方 `createElement` 法。 将返回值转换为 `Element`。 接下来，通过调用子元素的方法为其设置 `setAttribute` 值。 最后，通过调用标题元素的方法将元素追加到标题元素 `appendChild` ，并将子元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 通过 `PDFsFromBookmarks` 调用对象的方 `Document` 法创建元 `createElement` 素。 将表示元素名称的字符串值传递给方 `createElement` 法。 将返回值转换为 `Element`。 通过调用元素 `PDFsFromBookmarks` 的方法来设置元 `setAttribute` 素值。 通过调 `PDFsFromBookmarks` 用DDX元素 `DDX` 的方法将元素追加到元素 `appendChild` 后。 将元素 `PDFsFromBookmarks` 对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 通过 `PDF` 调用对象的方 `Document` 法创建元 `createElement` 素。 传递表示元素名称的字符串值。 将返回值转换为 `Element`。 通过调用元素 `PDF` 的方法来设置元 `setAttribute` 素值。 通过调 `PDF` 用元素的 `PDFsFromBookmarks` 方法将元素 `PDFsFromBookmarks` 追加到元 `appendChild` 素。 将元素 `PDF` 对象作为参数传递。 下面几行代码显示了此应用程序逻辑：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 转换DDX文档。

   * 通过 `javax.xml.transform.Transformer` 调用对象的静态 `javax.xml.transform.Transformer` 方法创建对 `newInstance` 象。
   * 通过 `Transformer` 调用对象的方 `TransformerFactory` 法创建对 `newTransformer` 象。
   * 使用对 `ByteArrayOutputStream` 象的构造函数创建对象。
   * 使用对 `javax.xml.transform.dom.DOMSource` 象的构造函数创建对象。 传递 `org.w3c.dom.Document` 表示DDX文档的对象。
   * 使用对 `javax.xml.transform.dom.DOMSource` 象的构造函数并传递该对 `ByteArrayOutputStream` 象。
   * 通过调 `ByteArrayOutputStream` 用对象的方 `javax.xml.transform.Transformer` 法填充Java对 `transform` 象。 传递 `javax.xml.transform.dom.DOMSource` 和对 `javax.xml.transform.stream.StreamResult` 象。
   * 创建一个字节数组，并将对象的大 `ByteArrayOutputStream` 小分配给该字节数组。
   * 通过调用对象的方法 `ByteArrayOutputStream` 填充字节数 `toByteArray` 组。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递字节数组来创建对象。

1. 引用PDF文档进行反汇编。

   * 使用构 `java.util.Map` 造函数创建用于存储输入PDF文档的对 `HashMap` 象。
   * 通过使用 `java.io.FileInputStream` 其构造函数并传递PDF文档的位置以反汇编来创建对象。
   * 创建对 `com.adobe.idp.Document` 象。 将包含 `java.io.FileInputStream` PDF文档的对象传递给反汇编。
   * 通过调用对象的方 `java.util.Map` 法并传递以下参数， `put` 向对象添加一个条目：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的PDF源元素的值匹配。 (在动态创建的DDX文档中，该值为 `AssemblerResultPDF.pdf`。)
      * 包含 `com.adobe.idp.Document` 要反汇编的PDF文档的对象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用对 `AssemblerOptionSpec` 象的方 `setFailOnError` 法并传递 `false`。

1. 反汇编PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` 动态创建的DDX文档的对象
   * 包含 `java.util.Map` 要反汇编的PDF文档的对象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象
   该方 `invokeDDX` 法返回一个对 `com.adobe.livecycle.assembler.client.AssemblerResult` 象，其中包含已拆解的PDF文档和发生的任何例外。

1. 保存已拆卸的PDF文档。

   要获取已拆卸的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 此方法返回一个 `java.util.Map` 对象。
   * 遍历对象， `java.util.Map` 直到找到生成的对 `com.adobe.idp.Document` 象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。

**另请参阅**

[快速入门（SOAP模式）:使用Java API动态创建DDX文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API动态创建DDX文档 {#dynamically-create-a-ddx-document-using-the-web-service-api}

使用Assembler Service API（Web服务）动态创建DDX文档并反汇编PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保在设置服务引用时使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用对 `AssemblerServiceClient` 象的默认构造函数创建对象。
   * 使用构 `AssemblerServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `AssemblerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 创建DDX文档。

   * 使用对 `System.Xml.XmlElement` 象的构造函数创建对象。
   * 通过调用对象的方法创建DDX文档 `XmlElement` 的根元 `CreateElement` 素。 此方法创建 `Element` 一个表示根元素的对象。 将表示元素名称的字符串值传递给方 `CreateElement` 法。 通过调用DDX元素的方法为其设置 `SetAttribute` 值。 最后，通过调用对象的方法将元素追加 `XmlElement` 到DDX文 `AppendChild` 档。 将DDX对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 通过调用对象的 `PDFsFromBookmarks` 方法创建DDX文 `XmlElement` 档的元 `CreateElement` 素。 将表示元素名称的字符串值传递给方 `CreateElement` 法。 接下来，通过调用元素的方法为元素设置 `SetAttribute` 值。 通过调 `PDFsFromBookmarks` 用元素的方法，将元素追加 `DDX` 到根元素 `AppendChild` 后。 将元素 `PDFsFromBookmarks` 对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 通过调用对象的 `PDF` 方法创建DDX文 `XmlElement` 档的元 `CreateElement` 素。 将表示元素名称的字符串值传递给方 `CreateElement` 法。 接下来，通过调用子元素的方法为其设置 `SetAttribute` 值。 通过调 `PDF` 用元素的 `PDFsFromBookmarks` 方法将元素 `PDFsFromBookmarks` 追加到元 `AppendChild` 素。 将元素 `PDF` 对象作为参数传递。 下面几行代码显示了此应用程序逻辑：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 转换DDX文档。

   * 使用对 `System.IO.MemoryStream` 象的构造函数创建对象。
   * 使用 `MemoryStream` 表示DDX文档的对象，用DDX `XmlElement` 文档填充对象。 调用对 `XmlElement` 象的方 `Save` 法并传递对 `MemoryStream` 象。
   * 创建一个字节数组，并用位于对象中的数据填充该 `MemoryStream` 数组。 以下代码显示此应用程序逻辑：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 创建对 `BLOB` 象。 将字节数组指定 `BLOB` 给对象的字 `MTOM` 段。

1. 引用PDF文档进行反汇编。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储输入的PDF文档。 此对 `BLOB` 象作为参数传递给 `invokeOneDocument` 该对象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指 `MTOM` 定到字节数组的内容来填充对象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请为对 `false` 象的数 `AssemblerOptionSpec` 据成员分 `failOnError` 配。

1. 反汇编PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `BLOB` 动态创建的DDX文档的对象
   * 包 `mapItem` 含输入PDF文档的数组
   * 指定 `AssemblerOptionSpec` 运行时选项的对象
   该方 `invokeDDX` 法返回一个对 `AssemblerResult` 象，该对象包含作业的结果和发生的任何例外。

1. 保存已拆卸的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含已拆 `Map` 卸的PDF文档的对象。
   * 遍历对象 `Map` 以获得每个生成的文档。 然后，将该阵列成员转 `value` 换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示该PDF文 `BLOB` 档的二进制数 `MTOM` 据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
