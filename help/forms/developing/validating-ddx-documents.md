---
title: 验证DDX文档
seo-title: 验证DDX文档
description: 'null'
seo-description: 'null'
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 验证DDX文档 {#validating-ddx-documents}

您可以通过编程方式验证Assembler服务使用的DDX文档。 即，使用Assembler服务API，您可以确定DDX文档是否有效。 例如，如果您从先前的AEM Forms版本升级，并且要确保DDX文档有效，则可以使用Assembler服务API验证它。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要验证DDX文档，请执行以下任务：

1. 包括项目文件。
1. 创建Assembler客户端。
1. 引用现有DDX文档。
1. 设置运行时选项以验证DDX文档。
1. 执行验证。
1. 将验证结果保存在日志文件中。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms部署在上的J2EE应用程序服务器的JAR文件。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

要验证DDX文档，必须引用现有DDX文档。

**设置运行时选项以验证DDX文档**

验证DDX文档时，必须设置特定的运行时选项，这些选项指示Assembler服务验证DDX文档，而不是执行它。 此外，您还可以增加Assembler服务写入日志文件的信息量。

**执行验证**

在创建Assembler服务客户端、引用DDX文档并设置运行时选项后，可以调用操 `invokeDDX` 作验证DDX文档。 验证DDX文档时，可以作为映射参数传递(此参数通常存储 `null` PDF文档，汇编程序需要这些PDF文档执行DDX文档中指定的操作)。

如果验证失败，则会引发异常，并且日志文件包含解释DDX文档无效原因的详细信 `OperationException` 息。 一旦通过基本XML解析和架构检查，就会针对DDX规范执行验证。 DDX文档中的所有错误都在日志中指定。

**将验证结果保存在日志文件中**

Assembler服务返回可写入XML日志文件的验证结果。 Assembler服务写入日志文件的详细信息量取决于您设置的运行时选项。

**另请参阅**

[使用Java API验证DDX文档](#validate-a-ddx-document-using-the-java-api)

[使用Web服务API验证DDX文档](#validate-a-ddx-document-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API验证DDX文档 {#validate-a-ddx-document-using-the-java-api}

使用Assembler Service API(Java)验证DDX文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 使用 `java.io.FileInputStream` DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示该文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 设置运行时选项以验证DDX文档。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 设置运行时选项，该选项指示Assembler服务通过调用对象的setValidateOnly方法并 `AssemblerOptionSpec` 传递来验证DDX文档 `true`。
   * 通过调用对象的方法并传递符合您要求的字符串值，设置Assembler服务 `AssemblerOptionSpec` 写入日志 `getLogLevel` 文件的信息量。 验证DDX文档时，您希望将更多信息写入日志文件，以协助验证过程。 因此，您可以传递值 `FINE` 或 `FINER`。

1. 执行验证。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` DDX文档的对象。
   * 通常存 `null` 储PDF文档的java.io.Map对象的值。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项的对象。
   该方 `invokeDDX` 法返回一个对 `AssemblerResult` 象，该对象包含指定DDX文档是否有效的信息。

1. 将验证结果保存在日志文件中。

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。xml。
   * 调用 `AssemblerResult` 对象的方 `getJobLog` 法。 此方法返回包 `com.adobe.idp.Document` 含验证信息的实例。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复 `com.adobe.idp.Document` 制到文件。
   >[!NOTE]
   >
   >如果DDX文档无效，则会 `OperationException` 引发。 在catch语句中，可以调用对 `OperationException` 象的方 `getJobLog` 法。

**另请参阅**

[验证DDX文档](#validating-ddx-documents)

[快速入门（SOAP模式）:使用Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）验证DDX文档

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API验证DDX文档 {#validate-a-ddx-document-using-the-web-service-api}

使用Assembler Service API（Web服务）验证DDX文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >将localhost替换为表单服务器的IP地址。

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

1. 引用现有DDX文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储DDX文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `MTOM` 为字节数组的内容来填充对象。

1. 设置运行时选项以验证DDX文档。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 设置运行时选项，该选项指示Assembler服务通过为对象的数据成员指定值true来验 `AssemblerOptionSpec` 证DDX `validateOnly` 文档。
   * 通过为对象的数据成员分配一个字符串值，设置汇编服务写入日志文 `AssemblerOptionSpec` 件的信 `logLevel` 息量。 方法验证DDX文档时，您希望将更多信息写入日志文件，以协助验证过程。 因此，您可以指定值 `FINE` 或 `FINER`。 有关可设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` AEM Forms API参考 [中的类引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 执行验证。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `BLOB` DDX文档的对象。
   * 通常存 `null` 储PDF文 `Map` 档的对象的值。
   * 指定 `AssemblerOptionSpec` 运行时选项的对象。
   该方 `invokeDDX` 法返回一个对 `AssemblerResult` 象，该对象包含指定DDX文档是否有效的信息。

1. 将验证结果保存在日志文件中。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示日志文件的文件位置以及在中打开文件的模式。 确保文件扩展名为。xml。
   * 创建一 `BLOB` 个对象，该对象通过获取对象数据成员的值 `AssemblerResult` 来存储日 `jobLog` 志信息。
   * 创建存储对象内容的字节数 `BLOB` 组。 通过获取对象字段的值来填 `BLOB` 充字节数 `MTOM` 组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。
   >[!NOTE]
   >
   >如果DDX文档无效，则会 `OperationException` 引发。 在catch语句中，您可以获取对象成 `OperationException` 员的值 `jobLog` 。

**另请参阅**

[验证DDX文档](#validating-ddx-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
