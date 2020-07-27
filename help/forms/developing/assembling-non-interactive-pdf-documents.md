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


# 汇编非交互式PDF文档 {#assembling-non-interactive-pdf-documents}

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

在此DDX文档中，请注意为源属性分配了值 `inDoc`。 如果仅将一个输入的PDF文档传递给Assembler服务，并返回一个PDF文档，并调用该操作， `invokeOneDocument` 则将该值指 `inDoc` 定给PDF源属性。 调用操 `invokeOneDocument` 作时， `inDoc` 值是预定义的键，必须在DDX文档中指定。

相反，将两个或两个以上输入的PDF文档传递给Assembler服务时，可以调用该操 `invokeDDX` 作。 在这种情况下，将输入PDF文档的文件名指定到属 `source` 性。

此DDX文档包 `NoXFA` 含元素，该元素指示Assembler服务返回非交互式PDF文档。

如果输入的PDF文档基于Acrobat表单或静态XFA表单，则Assembler服务可以组合非交互式PDF文档，而不将输出服务作为AEM表单安装的一部分。 但是，如果输入PDF文档是动态XFA表单，则输出服务必须是AEM表单安装的一部分。 如果在组装动态XFA表单时，输出服务不是AEM表单安装的一部分，则会引发异常。 请参 [阅创建文档输出流](/help/forms/developing/creating-document-output-streams.md)。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务汇编PDF文档。 本节不讨论概念，如创建包含输入文档的集合对象，或学习如何从返回的集合对象中提取结果。 (请参 [阅以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>有关Assembler服务的详细信息，请参 [阅Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

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
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时需要)

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms部署在其上的J2EE应用程序服务器的JAR文件。

**创建Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 此DDX文档必须包 `NoXFA` 含元素，该元素指示Assembler服务返回非交互式PDF文档。

**参考交互式PDF文档**

交互式PDF文档必须被引用并传递给Assembler服务才能返回非交互式PDF文档。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。

**组合PDF文档**

在创建Assembler服务客户端、引用DDX文档、引用交互式PDF文档并设置运行时选项后，可以调用该操 `invokeOneDocument` 作。 由于只有一个输入的PDF文档传递给Assembler服务并返回一个文档，因此您可以使用该操 `invokeOneDocument` 作而不是该操 `invokeDDX` 作。

**保存非交互式PDF文档**

如果只有一个PDF文档传递给Assembler服务，Assembler服务将返回一个文档而不是集合对象。 即，在调用操作时 `invokeOneDocument` ，将返回单个文档。 由于本节中引用的DDX文档包含创建非交互式PDF文档的说明，Assembler服务返回可另存为PDF文件的非交互式PDF文档。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API组合非交互式PDF文档 {#assemble-a-non-interactive-pdf-document-using-the-java-api}

使用Assembler Service API(Java)汇编非交互式PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 通过 `java.io.FileInputStream` 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该DDX文件的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 参考交互式PDF文档。

   * 通过使用 `java.io.FileInputStream` 其构造函数并传递交互式PDF文档的位置来创建对象。
   * 创建一 `com.adobe.idp.Document` 个对象，并传 `java.io.FileInputStream` 递包含PDF文档的对象。 此 `com.adobe.idp.Document` 对象将传递给方 `invokeOneDocument` 法。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调 `AssemblerOptionSpec` 用对象的 `setFailOnError` 方法并传递 `false`。

1. 组合PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeOneDocument` 法并传递以下值：

   * 表 `com.adobe.idp.Document` 示DDX文档的对象。 确保此DDX文档包含PDF `inDoc` 源元素的值。
   * 包 `com.adobe.idp.Document` 含交互式PDF文档的对象。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象。

   该 `invokeOneDocument` 方法返回 `com.adobe.idp.Document` 一个包含非交互式PDF文档的对象。

1. 保存非交互式PDF文档。

   * 创建对 `java.io.File` 象，并确保文件扩展名为。pdf。
   * 调用 `Document` 对象的方 `copyToFile` 法，将对象的内容 `Document` 复制到文件。 确保使用方 `Document` 法返回的 `invokeOneDocument` 对象。

* &quot;快速开始（SOAP模式）: 使用Java API汇编非交互式PDF文档”

## 使用Web服务API组合非交互式PDF文档 {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

使用Assembler Service API（Web服务）汇编非交互式PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Assembler客户端。

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
   * 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及在中打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 参考交互式PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储输入的PDF文档。 此 `BLOB` 对象作为参 `invokeOneDocument` 数传递给。
   * 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及在中打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请 `false` 指定 `AssemblerOptionSpec` 对象的数据 `failOnError` 成员。

1. 组合PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeOneDocument` 法并传递以下值：

   * 表 `BLOB` 示DDX文档的对象
   * 表示 `BLOB` 交互式PDF文档的对象
   * 指定 `AssemblerOptionSpec` 运行时选项的对象

   该 `invokeOneDocument` 方法返回 `BLOB` 一个包含非交互式PDF文档的对象。

1. 保存非交互式PDF文档。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示非交互式PDF文档的文件位置以及在中打开文件的模式。
   * 创建一个字节数组，用于存储方 `BLOB` 法返回的对 `invokeOneDocument` 象的内容。 通过获取对象字段的值 `BLOB` 填充字节数 `MTOM` 组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入PDF文件。

* “快速开始(MTOM): 使用Web服务API汇编非交互式PDF文档”。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
