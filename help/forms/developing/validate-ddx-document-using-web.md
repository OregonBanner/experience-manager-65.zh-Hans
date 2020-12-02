---
title: 使用Web服务API验证DDX文档
seo-title: 使用Web服务API验证DDX文档
description: 'null'
seo-description: 'null'
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---


# 使用Web服务API {#validate-a-ddx-document-using-theweb-service-api}验证DDX文档

使用Assembler Service API（Web服务）验证DDX文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将localhost替换为表单服务器的IP地址。

1. 创建PDF Assembler客户端。

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
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。

1. 设置运行时选项以验证DDX文档。

   * 使用其构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 设置运行时选项，该选项指示Assembler服务通过将值true指定给`AssemblerOptionSpec`对象的`validateOnly`文档成员来验证DDX。
   * 通过为`AssemblerOptionSpec`对象的`logLevel`数据成员分配字符串值，设置Assembler服务写入日志文件的信息量。 方法验证DDX文档时，您希望将更多信息写入日志文件，以协助验证过程。 因此，可以指定值`FINE`或`FINER`。 有关可以设置的运行时选项的信息，请参见[AEM FormsAPI参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`类引用。

1. 执行验证。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象。
   * 通常存储PDF文档的`Map`对象的值`null`。
   * 指定运行时选项的`AssemblerOptionSpec`对象。

   `invokeDDX`方法返回一个`AssemblerResult`对象，该对象包含指定DDX文档是否有效的信息。

1. 将验证结果保存在日志文件中。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建一个&lt;a0/>对象，该字符串值表示日志文件的文件位置以及在中打开文件的模式。 确保文件扩展名为。xml。
   * 通过获取`AssemblerResult`对象的`jobLog`数据成员的值，创建存储日志信息的`BLOB`对象。
   * 创建存储`BLOB`对象内容的字节数组。 通过获取`BLOB`对象的`MTOM`字段的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

   >[!NOTE]
   >
   >如果DDX文档无效，则引发`OperationException`。 在catch语句中，可以获取`OperationException`对象的`jobLog`成员的值。

**另请参阅**

[验证DDX文档](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
