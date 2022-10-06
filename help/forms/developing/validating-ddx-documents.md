---
title: 验证DX文档
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

# 验证DX文档 {#validating-ddx-documents}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以以编程方式验证汇编程序服务使用的DDX文档。 即，使用汇编程序服务API，可以确定DDX文档是否有效。 例如，如果您从以前的AEM Forms版本升级，并且希望确保DDX文档有效，则可以使用汇编程序服务API验证它。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要验证DDX文档，请执行以下任务：

1. 包括项目文件。
1. 创建汇编程序客户端。
1. 引用现有DDX文档。
1. 设置运行时选项以验证DDX文档。
1. 执行验证。
1. 将验证结果保存在日志文件中。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms所部署的J2EE应用程序服务器的JAR文件。

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

要验证DDX文档，必须引用现有DDX文档。

**设置运行时选项以验证DDX文档**

验证DDX文档时，必须设置特定的运行时选项，这些选项指示汇编程序服务验证DDX文档，而不是执行它。 此外，您还可以增加汇编程序服务写入日志文件的信息量。

**执行验证**

在创建汇编程序服务客户端、引用DDX文档并设置运行时选项后，可以调用 `invokeDDX` 操作来验证DDX文档。 验证DX文档时，您可以通过 `null` 作为映射参数(此参数通常存储汇编程序执行DDX文档中指定的操作所需的PDF文档)。

如果验证失败，则会引发异常，并且日志文件包含详细信息，说明DDX文档无效的原因，可从 `OperationException` 实例。 在经过基本XML解析和模式检查后，将执行针对DDX规范的验证。 位于DDX文档中的所有错误都在日志中指定。

**将验证结果保存在日志文件中**

汇编程序服务返回可写入XML日志文件的验证结果。 汇编程序服务写入日志文件的详细信息量取决于您设置的运行时选项。

**另请参阅**

[使用Java API验证DDX文档](#validate-a-ddx-document-using-the-java-api)

[使用Web服务API验证DDX文档](#validate-a-ddx-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API验证DDX文档 {#validate-a-ddx-document-using-the-java-api}

使用汇编程序服务API(Java)验证DDX文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置运行时选项以验证DDX文档。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 设置运行时选项，该选项指示汇编程序服务通过调用 `AssemblerOptionSpec` 对象的setValidateOnly方法和传递 `true`.
   * 通过调用 `AssemblerOptionSpec` 对象 `getLogLevel` 方法和传递字符串值符合您的要求。 验证DDX文档时，您希望将更多信息写入日志文件，以协助验证过程。 因此，您可以传递值 `FINE` 或 `FINER`.

1. 执行验证。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法并传递以下值：

   * A `com.adobe.idp.Document` 表示DDX文档的对象。
   * 值 `null` 用于通常存储PDF文档的java.io.Map对象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项的对象。

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含指定DDX文档是否有效的信息的对象。

1. 将验证结果保存在日志文件中。

   * 创建 `java.io.File` 对象，并确保文件扩展名为.xml。
   * 调用 `AssemblerResult` 对象 `getJobLog` 方法。 此方法将返回 `com.adobe.idp.Document` 包含验证信息的实例。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象。

   >[!NOTE]
   >
   >如果DDX文档无效，则 `OperationException` 的次数。 在catch语句中，您可以调用 `OperationException` 对象 `getJobLog` 方法。

**另请参阅**

[验证DX文档](#validating-ddx-documents)

[快速入门（SOAP模式）：使用Java API验证DDX文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAP模式）

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API验证DDX文档 {#validate-a-ddx-document-using-the-web-service-api}

使用汇编程序服务API（Web服务）验证DDX文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >将localhost替换为Forms服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及在中打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 设置运行时选项以验证DDX文档。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 设置运行时选项，该选项指示汇编程序服务通过将值true赋予 `AssemblerOptionSpec` 对象 `validateOnly` 数据成员。
   * 通过将字符串值分配给 `AssemblerOptionSpec` 对象 `logLevel` 数据成员。 方法验证DDX文档时，您希望将更多信息写入日志文件，以协助验证过程。 因此，您可以指定值 `FINE` 或 `FINER`. 有关可设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` 类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 执行验证。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象。
   * 值 `null` 对于 `Map` 通常存储PDF文档的对象。
   * 安 `AssemblerOptionSpec` 指定运行时选项的对象。

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含指定DDX文档是否有效的信息的对象。

1. 将验证结果保存在日志文件中。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示日志文件的文件位置以及在中打开文件的模式。 确保文件扩展名为.xml。
   * 创建 `BLOB` 用于通过获取 `AssemblerResult` 对象 `jobLog` 数据成员。
   * 创建用于存储 `BLOB` 对象。 通过获取 `BLOB` 对象 `MTOM` 字段。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

   >[!NOTE]
   >
   >如果DDX文档无效，则 `OperationException` 的次数。 在catch语句中，您可以获取 `OperationException` 对象 `jobLog` 成员。

**另请参阅**

[验证DX文档](#validating-ddx-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
