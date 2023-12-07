---
title: 使用Web服务API验证DDX文档
description: 使用Assembler服务API验证DDX文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# 使用Web服务API验证DDX文档 {#validate-a-ddx-document-using-theweb-service-api}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

使用Assembler服务API（Web服务）验证DDX文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >将localhost替换为Forms服务器的IP地址。

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
   * 创建 `System.IO.FileStream` 对象，方法是：调用其构造函数，并传递一个字符串值，该值表示DDX文档的文件位置以及用于打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 属性与字节数组的内容。

1. 设置运行时选项以验证DDX文档。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过将值true赋给，设置运行时选项，指示Assembler服务验证DDX文档 `AssemblerOptionSpec` 对象的 `validateOnly` 数据成员。
   * 通过为指定字符串值，设置Assembler服务写入日志文件的信息量 `AssemblerOptionSpec` 对象的 `logLevel` 数据成员。 方法验证DDX文档时，您需要将更多信息写入日志文件，以帮助验证过程。 因此，您可以指定值 `FINE` 或 `FINER`. 有关可设置的运行时选项的信息，请参见 `AssemblerOptionSpec` 中的类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 执行验证。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象。
   * 值 `null` 对于 `Map` 通常存储PDF文档的对象。
   * An `AssemblerOptionSpec` 指定运行时选项的对象。

   此 `invokeDDX` 方法返回 `AssemblerResult` 包含指定DDX文档是否有效的信息的对象。

1. 将验证结果保存在日志文件中。

   * 创建 `System.IO.FileStream` 对象，方法是：调用其构造函数，并传递一个字符串值，该值表示日志文件的文件位置以及用于在中打开文件的模式。 确保文件扩展名为.xml。
   * 创建 `BLOB` 对象，通过获取 `AssemblerResult` 对象的 `jobLog` 数据成员。
   * 创建一个字节数组，用于存储 `BLOB` 对象。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 字段。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

   >[!NOTE]
   >
   >如果DDX文档无效， `OperationException` 被抛出。 在catch语句中，您可以获取 `OperationException` 对象的 `jobLog` 成员。

**另请参阅**

[验证DDX文档](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
