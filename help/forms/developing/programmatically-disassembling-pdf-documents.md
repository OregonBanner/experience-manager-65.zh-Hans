---
title: 以编程方式拆分PDF文档
description: 使用Assembler服务通过Java API和Web服务API将单个PDF文档拆分为多个PDF文档。
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 0%

---

# 以编程方式拆分PDF文档 {#programmatically-disassembling-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

通过将PDF文档传递给Assembler服务，可以分解文档。 通常，当PDF文档最初由许多单个文档（如语句集合）创建时，此任务非常有用。 在下图中，DocA被划分为多个结果文档，其中页面上的第一个级别1书签标识了新结果文档的开始。

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

要拆卸PDF文档，请确保 `PDFsFromBookmarks` 元素位于DDX文档中。 此 `PDFsFromBookmarks` 元素是生成的元素，并且只能是 `DDX` 元素。 它没有 `result` 属性，因为它可能导致生成多个文档。

此 `PDFsFromBookmarks` 元素导致为源文档中的每个1级书签生成单个文档。

为了进行此讨论，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务组合PDF文档。 (请参阅 [以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>将单个PDF文档传递给Assembler服务并取回单个文档时，您可以调用 `invokeOneDocument` 操作。 但是，要拆分PDF文档，请使用 `invokeDDX` 操作的原因是，虽然一个输入PDF文档被传递到Assembler服务，但Assembler服务返回包含一个或多个文档的集合对象。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的详细信息，请参见 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要拆分PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 参照要拆解的PDF文档。
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

如果将AEM Forms部署在受支持的J2EE应用程序服务器（不是JBoss）上，则必须将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF汇编程序客户端**

您必须先创建一个Assembler服务客户端，然后才能以编程方式执行Assembler操作。

**引用现有DDX文档**

要拆分PDF文档，必须引用DDX文档。 此DDX文档必须包含 `PDFsFromBookmarks` 元素。

**引用要分解的PDF文档**

要拆分PDF文档，请引用表示要拆分PDF文档的PDF文件。 当传递到Assembler服务时，将为文档中的每个1级书签返回一个单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。

**拆分PDF文档**

在创建Assembler服务客户端、引用DDX文档、引用PDFPDF文档进行分解并设置运行时选项之后，可以通过调用 `invokeDDX` 方法。 只要DDX文档包含拆卸PDF文档的指令，Assembler服务就会返回收集对象中的拆卸PDF文档。

**保存已拆解的PDF文档**

所有已拆解的PDF文档都会在集合对象中返回。 循环访问收藏集对象并将每个PDF文档另存为PDF文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API拆分PDF文档 {#disassemble-a-pdf-document-using-the-java-api}

使用Assembler服务API (Java)拆分PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 通过使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 参照要拆解的PDF文档。

   * 创建 `java.util.Map` 通过使用PDF存储输入文档的对象 `HashMap` 构造函数。
   * 创建 `java.io.FileInputStream` 对象通过构造函数传递PDF文件的位置进行拆解。
   * 创建 `com.adobe.idp.Document` 对象并传递 `java.io.FileInputStream` 包含要拆解的PDF文档的对象。
   * 将条目添加到 `java.util.Map` 对象(通过调用其 `put` 方法并传递以下参数：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 包含要拆解的PDF文档的对象。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象的 `setFailOnError` 方法和路径 `false`.

1. 拆分PDF文档。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象
   * A `java.util.Map` 包含要拆解的PDF文档的对象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象

   此 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已拆卸PDF文档以及发生的任何异常的对象。

1. 保存已拆解的PDF文档。

   要获取已拆解的PDF文档，请执行以下步骤：

   * 调用 `AssemblerResult` 对象的 `getDocuments` 方法。 这会返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果为止 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于提取PDF文档的方法。

**另请参阅**

[以编程方式拆分PDF文档](#programmatically-disassembling-pdf-documents)

[快速入门（SOAP模式）：使用Java API拆分PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API拆分PDF文档 {#disassemble-a-pdf-document-using-the-web-service-api}

使用Assembler服务API（Web服务）拆分PDF文档：

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

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象通过调用其构造函数。 传递一个字符串值，该值表示DDX文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 属性与字节数组的内容。

1. 参照要拆解的PDF文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储输入PDF文档。 此 `BLOB` 对象被传递到 `invokeOneDocument` 作为论据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 字段字节数组的内容。
   * 创建 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 此集合对象用于存储要拆解的PDF。
   * 创建 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 将代表键名的字符串值分配给 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象的 `key` 字段。 此值必须与DDX文档中指定的PDF源元素的值匹配。
   * 分配 `BLOB` 将PDF文档存储到的对象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象的 `value` 字段。
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象 `Add` 方法并传递 `MyMapOf_xsd_string_To_xsd_anyType` 对象。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过为属于以下对象的数据成员分配值，设置运行时选项以满足您的业务要求 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请分配 `false` 到 `AssemblerOptionSpec` 对象的 `failOnError` 字段。

1. 拆分PDF文档。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示拆卸PDF文档的DDX文档的对象
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含要拆解的PDF文档的对象
   * An `AssemblerOptionSpec` 指定运行时选项的对象

   此 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和发生的任何异常的对象。

1. 保存已拆解的PDF文档。

   要获取新创建的PDF文档，请执行以下步骤：

   * 访问 `AssemblerResult` 对象的 `documents` 字段，即 `Map` 包含已拆卸PDF文档的对象。
   * 循环访问 `Map` 对象以获取每个结果文档。 然后，强制转换该数组成员的 `value` 到 `BLOB`.
   * 通过访问代表PDF文档的二进制数据 `BLOB` 对象的 `MTOM` 属性。 这会返回一个字节数组，您可以将该字节写出到PDF文件中。

**另请参阅**

[以编程方式拆分PDF文档](#programmatically-disassembling-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
