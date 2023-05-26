---
title: 验证DDX文档
seo-title: Validating DDX Documents
description: 使用Java API和Web服务API以编程方式验证DDX文档。
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 0%

---

# 验证DDX文档 {#validating-ddx-documents}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

您可以通过编程方式验证汇编程序服务使用的DDX文档。 即，使用Assembler服务API，您可以确定DDX文档是否有效。 例如，如果您从以前的AEM Forms版本升级，并且想要确保DDX文档有效，则可以使用汇编程序服务API来验证它。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的详细信息，请参见 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要验证DDX文档，请执行以下任务：

1. 包括项目文件。
1. 创建汇编程序客户端。
1. 引用现有DDX文档。
1. 设置运行时选项以验证DDX文档。
1. 执行验证。
1. 将验证结果保存在日志文件中。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果将AEM Forms部署在除JBoss之外受支持的J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF汇编程序客户端**

必须先创建一个Assembler服务客户端，然后才能以编程方式执行Assembler操作。

**引用现有DDX文档**

要验证DDX文档，必须引用现有的DDX文档。

**设置运行时选项以验证DDX文档**

验证DDX文档时，必须设置特定的运行时选项，以指示Assembler服务验证DDX文档，而不是执行文档。 此外，您还可以增加Assembler服务写入日志文件的信息量。

**执行验证**

创建Assembler服务客户端、引用DDX文档并设置运行时选项后，可以调用 `invokeDDX` 验证DDX文档的操作。 验证DDX文档时，您可以通过 `null` 作为map参数(此参数通常存储汇编程序执行DDX文档中指定的操作所需的PDF文档)。

如果验证失败，则会引发异常，并且日志文件包含详细说明，解释为什么DDX文档无效，该详细信息可从 `OperationException` 实例。 一旦通过了基本的XML解析和模式检查，则执行针对DDX规范的验证。 DDX文档中的所有错误都在日志中指定。

**将验证结果保存在日志文件中**

Assembler服务返回可以写入XML日志文件的验证结果。 汇编程序服务写入日志文件的详细信息量取决于您设置的运行时选项。

**另请参阅**

[使用Java API验证DDX文档](#validate-a-ddx-document-using-the-java-api)

[使用Web服务API验证DDX文档](#validate-a-ddx-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API验证DDX文档 {#validate-a-ddx-document-using-the-java-api}

使用Assembler服务API (Java)验证DDX文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 对象，通过使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 设置运行时选项以验证DDX文档。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过调用，设置指示汇编程序服务验证DDX文档的运行时选项 `AssemblerOptionSpec` 对象的setValidateOnly方法和传递 `true`.
   * 通过调用 `AssemblerOptionSpec` 对象的 `getLogLevel` 方法和传递字符串值符合您的要求。 验证DDX文档时，您需要将更多信息写入日志文件以帮助进行验证过程。 因此，您可以传递值 `FINE` 或 `FINER`.

1. 执行验证。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法，并传递以下值：

   * A `com.adobe.idp.Document` 表示DDX文档的对象。
   * 值 `null` java.io.Map对象，通常存储PDF文档。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项的对象。

   此 `invokeDDX` 方法返回 `AssemblerResult` 包含指定DDX文档是否有效的信息的对象。

1. 将验证结果保存在日志文件中。

   * 创建 `java.io.File` 对象并确保文件扩展名为.xml。
   * 调用 `AssemblerResult` 对象的 `getJobLog` 方法。 此方法会返回 `com.adobe.idp.Document` 包含验证信息的实例。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制目录内容的方法 `com.adobe.idp.Document` 对象到文件。

   >[!NOTE]
   >
   >如果DDX文档无效，则 `OperationException` 被抛出。 在catch语句中，您可以调用 `OperationException` 对象的 `getJobLog` 方法。

**另请参阅**

[验证DDX文档](#validating-ddx-documents)

[快速入门（SOAP模式）：使用Java API验证DDX文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API验证DDX文档 {#validate-a-ddx-document-using-the-web-service-api}

使用Assembler服务API （Web服务）验证DDX文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >将localhost替换为表单服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及用于打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性与字节数组的内容。

1. 设置运行时选项以验证DDX文档。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过将值true赋给，设置指示Assembler服务验证DDX文档的运行时选项 `AssemblerOptionSpec` 对象的 `validateOnly` 数据成员。
   * 通过为指定字符串值，设置Assembler服务写入日志文件的信息量 `AssemblerOptionSpec` 对象的 `logLevel` 数据成员。 方法验证DDX文档时，您需要将更多信息写入日志文件，以协助进行验证过程。 因此，您可以指定值 `FINE` 或 `FINER`. 有关可设置的运行时选项的信息，请参见 `AssemblerOptionSpec` 中的类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 执行验证。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法，并传递以下值：

   * A `BLOB` 表示DDX文档的对象。
   * 值 `null` 对于 `Map` 通常存储PDF文档的对象。
   * An `AssemblerOptionSpec` 指定运行时选项的对象。

   此 `invokeDDX` 方法返回 `AssemblerResult` 包含指定DDX文档是否有效的信息的对象。

1. 将验证结果保存在日志文件中。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示日志文件的文件位置以及用于打开文件的模式。 确保文件扩展名为.xml。
   * 创建 `BLOB` 通过获取的值，存储日志信息的对象 `AssemblerResult` 对象的 `jobLog` 数据成员。
   * 创建一个字节数组，用于存储 `BLOB` 对象。 通过获取的值填充字节数组 `BLOB` 对象的 `MTOM` 字段。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 方法和传递字节数组。

   >[!NOTE]
   >
   >如果DDX文档无效，则 `OperationException` 被抛出。 在catch语句中，您可以获取 `OperationException` 对象的 `jobLog` 会员。

**另请参阅**

[验证DDX文档](#validating-ddx-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
