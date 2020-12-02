---
title: 汇编非交互式PDF文档
seo-title: 汇编非交互式PDF文档
description: 'null'
seo-description: 'null'
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 0%

---


# 汇编非交互式PDF文档{#assembling-non-interactive-pdf-documents}

在将交互式PDF表单用作输入时，您可以组合非交互式PDF文档。 也就是说，假定您有一个表单，用户可以使用它在其字段中输入数据。 您可以将该表单传递给Assembler服务，导致Assembler服务返回一个PDF文档，阻止用户在其字段中输入数据。 此文档是非交互式PDF表单。 例如，下图显示了一个表示交互式表单的按揭贷款应用程序。

在本讨论中，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

在此DDX文档中，请注意为源属性分配了值`inDoc`。 如果只将一个输入的PDF文档传递给Assembler服务并返回一个PDF文档，并调用`invokeOneDocument`操作，则将值`inDoc`指定给PDF源属性。 调用`invokeOneDocument`操作时，`inDoc`值是预定义的键，必须在DDX文档中指定。

相反，将两个或两个以上输入的PDF文档传递给Assembler服务时，可以调用`invokeDDX`操作。 在这种情况下，将输入PDF文档的文件名指定为`source`属性。

此DDX文档包含`NoXFA`元素，它指示Assembler服务返回非交互式PDF文档。

如果输入的PDF文档基于Acrobat表单或静态XFA表单，则Assembler服务可以组合非交互式PDF文档，而不将输出服务作为AEM表单安装的一部分。 但是，如果输入PDF文档是动态XFA表单，则输出服务必须是AEM表单安装的一部分。 如果组装动态XFA表单时，输出服务不是AEM表单安装的一部分，则会引发异常。 请参阅[创建文档输出流](/help/forms/developing/creating-document-output-streams.md)。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务汇编PDF文档。 本节不讨论概念，如创建包含输入文档的集合对象，或学习如何从返回的集合对象中提取结果。 (请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参阅[Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要组合非交互式PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 参考交互式PDF文档。
1. 设置运行时选项。
1. 组合PDF文档。
1. 保存非交互式PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，则为必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必需)

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms部署的J2EE应用程序服务器的JAR文件。

**创建Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 此DDX文档必须包含`NoXFA`元素，该元素指示Assembler服务返回非交互式PDF文档。

**参考交互式PDF文档**

交互式PDF文档必须被引用并传递给Assembler服务才能返回非交互式PDF文档。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。

**组合PDF文档**

在创建Assembler服务客户端、引用DDX文档、引用交互式PDF文档并设置运行时选项后，可以调用`invokeOneDocument`操作。 由于只有一个输入的PDF文档传递给Assembler服务并返回一个文档，因此您可以使用`invokeOneDocument`操作，而不是使用`invokeDDX`操作。

**保存非交互式PDF文档**

如果只有一个PDF文档传递给Assembler服务，Assembler服务将返回一个文档而不是集合对象。 即，在调用`invokeOneDocument`操作时，返回单个文档。 由于本节中引用的DDX文档包含创建非交互式PDF文档的说明，Assembler服务返回可另存为PDF文件的非交互式PDF文档。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}组合非交互式PDF文档

使用Assembler Service API(Java)汇编非交互式PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建Assembler客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`AssemblerServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 通过使用DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示DDX文件的`java.io.FileInputStream`对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 参考交互式PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数并传递交互式PDF文档的位置，创建&lt;a0/>对象。
   * 创建`com.adobe.idp.Document`对象，并传递包含PDF文档的`java.io.FileInputStream`对象。 此`com.adobe.idp.Document`对象将传递给`invokeOneDocument`方法。

1. 设置运行时选项。

   * 使用其构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足业务要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合PDF文档。

   调用`AssemblerServiceClient`对象的`invokeOneDocument`方法并传递以下值：

   * 表示DDX文档的`com.adobe.idp.Document`对象。 确保此DDX文档包含PDF源元素的值`inDoc`。
   * 一个`com.adobe.idp.Document`对象，它包含交互式PDF文档。
   * 一个`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，它指定运行时选项，包括默认字体和作业日志级别。

   `invokeOneDocument`方法返回一个`com.adobe.idp.Document`对象，该对象包含非交互式PDF文档。

1. 保存非交互式PDF文档。

   * 创建`java.io.File`对象，并确保文件扩展名为。pdf。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件。 确保使用`invokeOneDocument`方法返回的`Document`对象。

* &quot;快速开始（SOAP模式）:使用Java API汇编非交互式PDF文档”

## 使用Web服务API {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}组合非交互式PDF文档

使用Assembler Service API（Web服务）汇编非交互式PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Assembler客户端。

   * 使用其默认构造函数创建`AssemblerServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及在中打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 参考交互式PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储输入的PDF文档。 此`BLOB`对象作为参数传递给`invokeOneDocument`。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及在中打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 设置运行时选项。

   * 使用其构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合PDF文档。

   调用`AssemblerServiceClient`对象的`invokeOneDocument`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 表示交互式PDF文档的`BLOB`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeOneDocument`方法返回一个`BLOB`对象，该对象包含非交互式PDF文档。

1. 保存非交互式PDF文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示非交互式PDF文档的文件位置以及在中打开文件的模式。
   * 创建一个字节数组，用于存储`invokeOneDocument`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`字段的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

* “快速开始(MTOM):使用Web服务API汇编非交互式PDF文档”。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
