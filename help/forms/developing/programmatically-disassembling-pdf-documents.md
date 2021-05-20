---
title: 以编程方式拆解PDF文档
seo-title: 以编程方式拆解PDF文档
description: 使用汇编程序服务，使用Java API和Web服务API将单个PDF文档拆解为多个PDF文档。
seo-description: 使用汇编程序服务，使用Java API和Web服务API将单个PDF文档拆解为多个PDF文档。
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 0%

---

# 以编程方式拆解PDF文档{#programmatically-disassembling-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以通过将PDF文档传递到汇编程序服务来拆解该文档。 通常，当PDF文档最初是从许多单独的文档（如语句集合）创建时，此任务会很有用。 在下图中，文档A被分为多个生成文档，其中页面上的第一级书签标识新生成文档的开始。

![pd_pd_pdf从书签](assets/pd_pd_pdfsfrombookmarks.png)

要拆解PDF文档，请确保`PDFsFromBookmarks`元素位于DDX文档中。 `PDFsFromBookmarks`元素是生成元素，只能是`DDX`元素的子元素。 它没有`result`属性，因为它可能导致生成多个文档。

`PDFsFromBookmarks`元素会为源文档中的每个1级书签生成一个文档。

在本讨论中，假定使用了以下DDX文档。

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
>在阅读本节之前，建议您熟悉使用汇编程序服务来汇编PDF文档。 （请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>将单个PDF文档传递到汇编程序服务并返回单个文档时，可以调用`invokeOneDocument`操作。 但是，要拆解PDF文档，请使用`invokeDDX`操作，因为尽管一个输入的PDF文档被传递到汇编程序服务，汇编程序服务会返回一个包含一个或多个文档的集合对象。

>[!NOTE]
>
>有关汇编程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要拆解PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用PDF文档进行反汇编。
1. 设置运行时选项。
1. 反汇编PDF文档。
1. 保存已拆卸的PDF文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档以反汇编PDF文档。 此DDX文档必须包含`PDFsFromBookmarks`元素。

**引用PDF文档进行反汇编**

要反汇编PDF文档，请引用表示要反汇编的PDF文档的PDF文件。 当传递到汇编程序服务时，将为文档中的每个1级书签返回一个单独的PDF文档。

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。

**反汇编PDF文档**

在创建汇编程序服务客户端、引用DDX文档、引用要反汇编的PDF文档并设置运行时选项后，可以通过调用`invokeDDX`方法来反汇编PDF文档。 如果DDX文档包含反汇编PDF文档的说明，汇编程序服务会在收集对象中返回已拆解的PDF文档。

**保存已拆卸的PDF文档**

所有已拆卸的PDF文档都会在收藏对象中返回。 遍历收藏集对象，并将每个PDF文档另存为PDF文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#disassemble-a-pdf-document-using-the-java-api}反汇编PDF文档

使用汇编程序服务API(Java)反汇编PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`AssemblerServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该文档的`java.io.FileInputStream`对象。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 引用PDF文档进行反汇编。

   * 使用`HashMap`构造函数创建一个`java.util.Map`对象，用于存储输入的PDF文档。
   * 使用`java.io.FileInputStream`对象的构造函数创建一个对象，并将PDF文档的位置传递到反汇编。
   * 创建`com.adobe.idp.Document`对象，并将包含PDF文档的`java.io.FileInputStream`对象传递到反汇编。
   * 通过调用`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。
      * `com.adobe.idp.Document`对象，其中包含要拆解的PDF文档。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法来设置运行时选项以满足您的业务要求。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 反汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 表示要使用的DDX文档的`com.adobe.idp.Document`对象
   * `java.util.Map`对象，其中包含要拆解的PDF文档
   * 一个`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，用于指定运行时选项，包括默认字体和作业日志级别

   `invokeDDX`方法会返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，其中包含已拆卸的PDF文档以及发生的任何例外。

1. 保存已拆卸的PDF文档。

   要获取已拆卸的PDF文档，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 这会返回`java.util.Map`对象。
   * 遍历`java.util.Map`对象，直到找到结果`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDF文档。

**另请参阅**

[以编程方式拆解PDF文档](#programmatically-disassembling-pdf-documents)

[快速入门（SOAP模式）：使用Java API反汇编PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#disassemble-a-pdf-document-using-the-web-service-api}反汇编PDF文档

使用汇编程序服务API（Web服务）对PDF文档进行反汇编：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 在设置服务引用时，请确保使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 使用`AssemblerServiceClient`对象的默认构造函数创建对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用`System.IO.FileStream`对象的构造函数创建对象。 传递一个字符串值，该值表示DDX文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`BLOB`对象的`MTOM`属性分配字节数组的内容来填充该对象。

1. 引用PDF文档进行反汇编。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储输入的PDF文档。 此`BLOB`对象将作为参数传递到`invokeOneDocument`。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段分配字节数组的内容来填充`BLOB`对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此收集对象用于存储要反汇编的PDF。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段分配表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。
   * 将存储PDF文档的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象“ `Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务要求。 例如，要指示汇编程序服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`字段。

1. 反汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * `BLOB`对象，表示分解PDF文档的DDX文档
   * 包含要反汇编的PDF文档的`MyMapOf_xsd_string_To_xsd_anyType`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个`AssemblerResult`对象，其中包含作业结果和发生的任何异常。

1. 保存已拆卸的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含已拆卸的PDF文档的`Map`对象。
   * 遍历`Map`对象以获取每个生成文档。 然后，将该阵列成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`属性，提取表示该文档的二进制数据。 这会返回一个字节数组，您可以将其写出到PDF文件。

**另请参阅**

[以编程方式拆解PDF文档](#programmatically-disassembling-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
