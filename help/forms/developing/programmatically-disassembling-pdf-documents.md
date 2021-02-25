---
title: 以编程方式反汇编PDF文档
seo-title: 以编程方式反汇编PDF文档
description: 使用Assembler服务，使用Java API和Web服务API将单个PDF文档拆解为多个PDF文档。
seo-description: 使用Assembler服务，使用Java API和Web服务API将单个PDF文档拆解为多个PDF文档。
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 0%

---


# 以编程方式反汇编PDF文档{#programmatically-disassembling-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

您可以将PDF文档反汇编，方法是将其传递给Assembler服务。 通常，当PDF文档最初是从许多单个文档（如语句集合）创建时，此任务很有用。 在下图中，DocA被划分为多个生成文档，其中页面上的第一级书签标识新生成文档的开始。

![pd_pd_pdf从书签](assets/pd_pd_pdfsfrombookmarks.png)

要反汇编PDF文档，请确保`PDFsFromBookmarks`元素位于DDX文档中。 `PDFsFromBookmarks`元素是生成元素，只能是`DDX`元素的子元素。 它没有`result`属性，因为它可能导致生成多个文档。

`PDFsFromBookmarks`元素使源文档中每个1级书签生成一个文档。

在此讨论中，假定使用以下DDX文档。

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
>在阅读本节之前，建议您熟悉使用Assembler服务汇编PDF文档。 (请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>将单个PDF文档传递到Assembler服务并返回单个文档时，可以调用`invokeOneDocument`操作。 但是，要反汇编PDF文档，请使用`invokeDDX`操作，因为尽管将一个输入的PDF文档传递给Assembler服务，但Assembler服务返回一个包含一个或多个文档的集合对象。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参阅[Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要反汇编PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 参考PDF文档以反汇编。
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

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档以反汇编PDF文档。 此DDX文档必须包含`PDFsFromBookmarks`元素。

**参考PDF文档以反汇编**

要反汇编PDF文档，请参考表示要反汇编的PDF文档的PDF文件。 传递到Assembler服务时，将为文档中的每个1级书签返回单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，以在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。

**反汇编PDF文档**

在创建Assembler服务客户端后，请参考DDX文档，引用PDF文档以反汇编，并设置运行时选项，您可以通过调用`invokeDDX`方法反汇编PDF文档。 如果DDX文档包含反汇编PDF文档的说明，则Assembler服务会在集合对象中返回已分解的PDF文档。

**保存已拆解的PDF文档**

所有已拆卸的PDF文档都会在集合对象中返回。 遍历集合对象，将每个PDF文档另存为PDF文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#disassemble-a-pdf-document-using-the-java-api}拆解PDF文档

使用Assembler Service API(Java)反汇编PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`AssemblerServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示DDX文件的`java.io.FileInputStream`对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建对象。

1. 参考PDF文档以反汇编。

   * 使用`HashMap`构造函数创建用于存储输入PDF文档的`java.util.Map`对象。
   * 使用`java.io.FileInputStream`对象的构造函数并将PDF文档的位置传递给反汇编。
   * 创建`com.adobe.idp.Document`对象，并将包含PDF文档的`java.io.FileInputStream`对象传递给反汇编。
   * 通过调用`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名的字符串值。 此值必须与在DDX文档中指定的PDF源元素的值匹配。
      * 一个`com.adobe.idp.Document`对象，其中包含要反汇编的PDF文档。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建存储运行时选项的对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 反汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 一个`com.adobe.idp.Document`对象，它表示要使用的DDX文档
   * `java.util.Map`对象，其中包含要拆解的PDF文档
   * 一个`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，它指定运行时选项，包括默认字体和作业日志级别

   `invokeDDX`方法返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，其中包含已拆卸的PDF文档和发生的任何异常。

1. 保存已拆解的PDF文档。

   要获取已拆解的PDF文档，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 这返回一个`java.util.Map`对象。
   * 遍历`java.util.Map`对象，直到找到生成的`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDF文档。

**另请参阅**

[以编程方式反汇编PDF文档](#programmatically-disassembling-pdf-documents)

[快速开始（SOAP模式）：使用Java API反汇编PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#disassemble-a-pdf-document-using-the-web-service-api}拆解PDF文档

使用Assembler Service API（Web服务）反汇编PDF文档:

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

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它表示DDX文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过将`MTOM`属性赋予字节数组的内容，填充`BLOB`对象。

1. 参考PDF文档以反汇编。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储输入的PDF文档。 此`BLOB`对象作为参数传递给`invokeOneDocument`。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段指定字节数组的内容来填充`BLOB`对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储要反汇编的PDF。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段指定表示键名的字符串值。 此值必须与在DDX文档中指定的PDF源元素的值匹配。
   * 将存储PDF文档的`BLOB`对象指定到`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象&#39; `Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务需求。 例如，要指示Assembler服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`字段。

1. 反汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 一个`BLOB`对象，它表示分解PDF文档的DDX文档
   * 包含要反汇编的PDF文档的`MyMapOf_xsd_string_To_xsd_anyType`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个`AssemblerResult`对象，其中包含作业结果和发生的任何异常。

1. 保存已拆解的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含已拆解的PDF文档的`Map`对象。
   * 循环访问`Map`对象以获得每个生成文档。 然后，将该数组成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`属性提取表示PDF数据的二进制数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[以编程方式反汇编PDF文档](#programmatically-disassembling-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
