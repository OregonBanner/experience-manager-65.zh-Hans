---
title: 动态创建DDX文档
seo-title: 动态创建DDX文档
description: 使用Java API和Web服务API动态创建DDX文档。 动态创建DDX文档使您能够使用在运行时获取的DDX文档中的值。
seo-description: 使用Java API和Web服务API动态创建DDX文档。 动态创建DDX文档使您能够使用在运行时获取的DDX文档中的值。
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2200'
ht-degree: 0%

---


# 动态创建DDX文档{#dynamically-creating-ddx-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

您可以动态创建可用于执行Assembler操作的DDX文档。 动态创建DDX文档使您能够使用在运行时获取的DDX文档中的值。 要动态创建DDX文档，请使用属于您所使用的编程语言的类。 例如，如果您使用Java开发客户端应用程序，请使用属于`org.w3c.dom.*`包的类。 同样，如果您使用的是Microsoft .NET，则使用属于`System.Xml`命名空间的类。

在将DDX文档传递给Assembler服务之前，请将XML从`org.w3c.dom.Document`实例转换为`com.adobe.idp.Document`实例。 如果您使用Web服务，请将XML从用于创建XML的数据类型（例如`XmlDocument`）转换为`BLOB`实例。

对于此讨论，假定动态创建以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

此DDX文档拆解PDF文档。 建议您熟悉PDF文档的反汇编。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参阅[Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要使用动态创建的DDX文档反汇编PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 创建DDX文档。
1. 转换DDX文档。
1. 设置运行时选项。
1. 反汇编PDF文档。
1. 保存已拆解的PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则为必需)

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，请先创建一个Assembler服务客户端。

**创建DDX文档**

使用您所使用的编程语言创建DDX文档。 要创建分解PDF文档的DDX文档，请确保它包含`PDFsFromBookmarks`元素。 如果使用Java API，则将用于创建DDX文档的数据类型转换为`com.adobe.idp.Document`实例。 如果您使用Web服务，请将数据类型转换为`BLOB`实例。

**转换DDX文档**

使用`org.w3c.dom`类创建的DDX文档必须转换为`com.adobe.idp.Document`对象。 要在使用Java API时执行此任务，请使用Java XML转换类。 如果您使用Web服务，请将DDX文档转换为`BLOB`对象。

**参考PDF文档以反汇编**

要反汇编PDF文档，请参考表示要反汇编的PDF文档的PDF文件。 传递到Assembler服务时，将为文档中的每个1级书签返回单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，以在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 要设置运行时选项，请使用`AssemblerOptionSpec`对象。

**反汇编PDF文档**

通过调用`invokeDDX`操作拆解PDF文档。 传递动态创建的DDX文档。 Assembler服务返回集合对象中已拆解的PDF文档。

**保存已拆解的PDF文档**

所有已拆卸的PDF文档都会在集合对象中返回。 遍历集合对象，将每个PDF文档另存为PDF文件。

**另请参阅**

[使用Java API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[使用Web服务API动态创建DDX文档](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式反汇编PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API {#dynamically-create-a-ddx-document-using-the-java-api}动态创建DDX文档

使用Assembler Service API(Java)动态创建DDX文档并反汇编PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`AssemblerServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 创建DDX文档。

   * 通过调用`DocumentBuilderFactory`类`newInstance`方法创建Java `DocumentBuilderFactory`对象。
   * 通过调用`DocumentBuilderFactory`对象的`newDocumentBuilder`方法创建Java `DocumentBuilder`对象。
   * 调用`DocumentBuilder`对象的`newDocument`方法来实例化`org.w3c.dom.Document`对象。
   * 通过调用`org.w3c.dom.Document`对象的`createElement`方法创建DDX文档的根元素。 此方法创建一个表示根元素的`Element`对象。 将表示元素名称的字符串值传递给`createElement`方法。 将返回值转换为`Element`。 接下来，通过调用子元素的`setAttribute`方法为其设置值。 最后，通过调用标题元素的`appendChild`方法将元素追加到标题元素，并将子元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * 通过调用`Document`对象的`createElement`方法创建`PDFsFromBookmarks`元素。 将表示元素名称的字符串值传递给`createElement`方法。 将返回值转换为`Element`。 通过调用`setAttribute`方法为`PDFsFromBookmarks`元素设置值。 通过调用DDX元素的`appendChild`方法，将`PDFsFromBookmarks`元素追加到`DDX`元素。 将`PDFsFromBookmarks`元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * 通过调用`Document`对象的`createElement`方法创建`PDF`元素。 传递表示元素名称的字符串值。 将返回值转换为`Element`。 通过调用`setAttribute`方法为`PDF`元素设置值。 通过调用`PDFsFromBookmarks`元素的`appendChild`方法，将`PDF`元素追加到`PDFsFromBookmarks`元素。 将`PDF`元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. 转换DDX文档。

   * 通过调用`javax.xml.transform.Transformer`对象的静态`newInstance`方法创建`javax.xml.transform.Transformer`对象。
   * 通过调用`TransformerFactory`对象的`newTransformer`方法创建`Transformer`对象。
   * 使用`ByteArrayOutputStream`对象的构造函数创建对象。
   * 使用`javax.xml.transform.dom.DOMSource`对象的构造函数创建对象。 传递表示DDX文档的`org.w3c.dom.Document`对象。
   * 使用`javax.xml.transform.dom.DOMSource`对象的构造函数并传递`ByteArrayOutputStream`对象，创建对象。
   * 通过调用`javax.xml.transform.Transformer`对象的`transform`方法填充Java `ByteArrayOutputStream`对象。 传递`javax.xml.transform.dom.DOMSource`和`javax.xml.transform.stream.StreamResult`对象。
   * 创建一个字节数组，并将`ByteArrayOutputStream`对象的大小分配给字节数组。
   * 通过调用`ByteArrayOutputStream`对象的`toByteArray`方法填充字节数组。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递字节数组，创建对象。

1. 参考PDF文档以反汇编。

   * 使用`HashMap`构造函数创建用于存储输入PDF文档的`java.util.Map`对象。
   * 使用`java.io.FileInputStream`对象的构造函数并将PDF文档的位置传递给反汇编。
   * 创建`com.adobe.idp.Document`对象。 将包含PDF文档的`java.io.FileInputStream`对象传递到反汇编。
   * 通过调用`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名的字符串值。 此值必须与在DDX文档中指定的PDF源元素的值匹配。 (在动态创建的DDX文档中，值为`AssemblerResultPDF.pdf`。)
      * 一个`com.adobe.idp.Document`对象，其中包含要反汇编的PDF文档。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建存储运行时选项的对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 反汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 一个`com.adobe.idp.Document`对象，它表示动态创建的DDX文档
   * `java.util.Map`对象，其中包含要拆解的PDF文档
   * 一个`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，它指定运行时选项，包括默认字体和作业日志级别

   `invokeDDX`方法返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，其中包含已拆卸的PDF文档和发生的任何异常。

1. 保存已拆解的PDF文档。

   要获取已拆解的PDF文档，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 此方法返回`java.util.Map`对象。
   * 遍历`java.util.Map`对象，直到找到生成的`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDF文档。

**另请参阅**

[快速开始（SOAP模式）：使用Java API动态创建DDX文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#dynamically-create-a-ddx-document-using-the-web-service-api}动态创建DDX文档

使用Assembler Service API（Web服务）动态创建DDX文档并反汇编PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 请确保在设置服务引用时使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用`AssemblerServiceClient`对象的默认构造函数创建一个对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时使用此属性。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`赋给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`赋给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 创建DDX文档。

   * 使用`System.Xml.XmlElement`对象的构造函数创建对象。
   * 通过调用`XmlElement`对象的`CreateElement`方法创建DDX文档的根元素。 此方法创建一个表示根元素的`Element`对象。 将表示元素名称的字符串值传递给`CreateElement`方法。 通过调用DDX元素的`SetAttribute`方法来设置其值。 最后，通过调用`XmlElement`对象的`AppendChild`方法将元素追加到DDX文档。 将DDX对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * 通过调用`XmlElement`对象的`CreateElement`方法，创建DDX文档的`PDFsFromBookmarks`元素。 将表示元素名称的字符串值传递给`CreateElement`方法。 接下来，通过调用元素的`SetAttribute`方法为元素设置值。 通过调用`DDX`元素的`AppendChild`方法，将`PDFsFromBookmarks`元素追加到根元素。 将`PDFsFromBookmarks`元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * 通过调用`XmlElement`对象的`CreateElement`方法，创建DDX文档的`PDF`元素。 将表示元素名称的字符串值传递给`CreateElement`方法。 接下来，通过调用子元素的`SetAttribute`方法为其设置值。 通过调用`PDFsFromBookmarks`元素的`AppendChild`方法，将`PDF`元素追加到`PDFsFromBookmarks`元素。 将`PDF`元素对象作为参数传递。 以下几行代码显示此应用程序逻辑：

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. 转换DDX文档。

   * 使用`System.IO.MemoryStream`对象的构造函数创建对象。
   * 使用表示DDX文档的`XmlElement`对象，用DDX文档填充`MemoryStream`对象。 调用`XmlElement`对象的`Save`方法并传递`MemoryStream`对象。
   * 创建一个字节数组，并用位于`MemoryStream`对象中的数据填充它。 以下代码显示此应用程序逻辑：

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * 创建`BLOB`对象。 将字节数组分配给`BLOB`对象的`MTOM`字段。

1. 参考PDF文档以反汇编。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储输入的PDF文档。 此`BLOB`对象作为参数传递给`invokeOneDocument`。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，该值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的字节数组内容分配其属性来填充`BLOB`对象。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务需求。 例如，要指示Assembler服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 反汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 一个`BLOB`对象，它表示动态创建的DDX文档
   * 包含输入PDF文档的`mapItem`数组
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个`AssemblerResult`对象，其中包含作业的结果和发生的任何异常。

1. 保存已拆解的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含已拆解的PDF文档的`Map`对象。
   * 循环访问`Map`对象以获得每个生成文档。 然后，将该数组成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`属性提取表示PDF数据的二进制数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
