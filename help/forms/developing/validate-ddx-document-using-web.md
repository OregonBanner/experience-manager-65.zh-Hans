---
title: 使用Web服务API验证DDX文档
seo-title: Validate a DDX document using theweb service API
description: 使用汇编程序服务API验证DDX文档。
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 使用Web服务API验证DDX文档 {#validate-a-ddx-document-using-theweb-service-api}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

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

[验证DX文档](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
