---
title: 以编程方式反汇编PDF文档
seo-title: 以编程方式反汇编PDF文档
description: 'null'
seo-description: 'null'
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 0%

---


# 以编程方式反汇编PDF文档 {#programmatically-disassembling-pdf-documents}

您可以将PDF文档反汇编到Assembler服务。 通常，当PDF任务最初是从许多单独的文档（如语句集合）创建时，此文档很有用。 在下图中，DocA被划分为多个生成文档，其中页面上的第一级书签标识新生成文档的开始。

![pd_pd_pdf从书签](assets/pd_pd_pdfsfrombookmarks.png)

要反汇编PDF文档，请确 `PDFsFromBookmarks` 保元素位于DDX文档中。 元 `PDFsFromBookmarks` 素是生成元素，只能是元素的子元 `DDX` 素。 它没有属性， `result` 因为它可能导致生成多个文档。

元 `PDFsFromBookmarks` 素导致为源文档中的每个1级书签生成单个文档。

在本讨论中，假定使用以下DDX文档。

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
>在阅读本节之前，建议您熟悉使用Assembler服务来汇编PDF文档。 (请参 [阅以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>将单个PDF文档传递到Assembler服务并返回单个文档时，可以调用该操 `invokeOneDocument` 作。 但是，要反汇编PDF文档，请使 `invokeDDX` 用该操作，因为尽管一个输入的PDF文档被传递给Assembler服务，Assembler服务返回一个包含一个或多个文档的集合对象。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参 [阅Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要反汇编PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 参考PDF文档进行反汇编。
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

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档以反汇编PDF文档。 此DDX文档必须包含 `PDFsFromBookmarks` 元素。

**参考PDF文档进行反汇编**

要反汇编PDF文档，请参考表示要反汇编的PDF文档的PDF文件。 传递到Assembler服务时，将为文档中的每个1级书签返回单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。

**反汇编PDF文档**

在创建Assembler服务客户端、引用DDX文档、引用PDF文档进行反汇编并设置运行时选项后，可以通过调用方法来反汇编PDF文档 `invokeDDX` 。 如果DDX文档包含反汇编PDF文档的说明，则汇编服务会在集合对象中返回已分解的PDF文档。

**保存已拆卸的PDF文档**

所有已拆卸的PDF文档都会在集合对象中返回。 对集合对象进行迭代，并将每个PDF文档另存为PDF文件。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API反汇编PDF文档 {#disassemble-a-pdf-document-using-the-java-api}

使用Assembler Service API(Java)反汇编PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 通过 `java.io.FileInputStream` 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该DDX文件的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 参考PDF文档进行反汇编。

   * 使用构 `java.util.Map` 造函数创建用于存储输入PDF文档的对 `HashMap` 象。
   * 通过使用 `java.io.FileInputStream` 其构造函数并将PDF文档的位置传递给反汇编，从而创建对象。
   * 创建对 `com.adobe.idp.Document` 象，并将包 `java.io.FileInputStream` 含PDF文档的对象传递给反汇编。
   * 通过调用对象的方 `java.util.Map` 法并传递以 `put` 下参数，向对象添加一个条目：

      * 表示键名称的字符串值。 此值必须与在DDX文档中指定的PDF源元素值匹配。
      * 包 `com.adobe.idp.Document` 含要反汇编的PDF文档的对象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调 `AssemblerOptionSpec` 用对象的 `setFailOnError` 方法并传递 `false`。

1. 反汇编PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下必需值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文档的对象
   * 包含 `java.util.Map` 要反汇编的PDF文档的对象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象

   该方 `invokeDDX` 法返回一 `com.adobe.livecycle.assembler.client.AssemblerResult` 个对象，其中包含已分解的PDF文档和发生的任何例外。

1. 保存已拆解的PDF文档。

   要获取已分解的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 这将返回一个 `java.util.Map` 对象。
   * 遍历对象 `java.util.Map` ，直到找到生成的对 `com.adobe.idp.Document` 象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。

**另请参阅**

[以编程方式反汇编PDF文档](#programmatically-disassembling-pdf-documents)

[快速开始（SOAP模式）: 使用Java API反汇编PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API反汇编PDF文档 {#disassemble-a-pdf-document-using-the-web-service-api}

使用Assembler Service API（Web服务）反汇编PDF文档:

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

1. 引用现有DDX文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储DDX文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取 `System.IO.FileStream` 的字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象属性 `MTOM` 赋予字节数组的内容来填充对象。

1. 参考PDF文档进行反汇编。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储输入的PDF文档。 此 `BLOB` 对象作为参 `invokeOneDocument` 数传递给。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象字段指 `MTOM` 定字节数组的内容来填充对象。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储要反汇编的PDF。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与在DDX文档中指定的PDF源元素值匹配。
   * 将存 `BLOB` 储PDF文档的对象指 `MyMapOf_xsd_string_To_xsd_anyType_Item` 定到对象的字 `value` 段。
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用对 `MyMapOf_xsd_string_To_xsd_anyType` 象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请 `false` 指定 `AssemblerOptionSpec` 对象的字 `failOnError` 段。

1. 反汇编PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `BLOB` 分解PDF文档的DDX文档的对象
   * 包含 `MyMapOf_xsd_string_To_xsd_anyType` 要反汇编的PDF文档的对象
   * 指定 `AssemblerOptionSpec` 运行时选项的对象

   该方 `invokeDDX` 法返回一 `AssemblerResult` 个对象，其中包含作业结果和发生的任何异常。

1. 保存已拆解的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含已 `Map` 拆解的PDF文档的对象。
   * 对对象进行 `Map` 迭代以获得每个生成文档。 然后，将该阵列成员 `value` 转换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示PDF `BLOB` 的二进制 `MTOM` 数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[以编程方式反汇编PDF文档](#programmatically-disassembling-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
