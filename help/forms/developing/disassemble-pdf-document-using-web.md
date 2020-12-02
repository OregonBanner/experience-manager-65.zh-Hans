---
title: 使用Web服务API反汇编PDF文档
seo-title: 使用Web服务API反汇编PDF文档
description: 'null'
seo-description: 'null'
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# 使用Web服务API {#disassemble-a-pdf-document-usingthe-web-service-api}反汇编PDF文档

使用Assembler Service API（Web服务）反汇编PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 请确保在设置服务引用时使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

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
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。

1. 参考PDF文档进行反汇编。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储输入的PDF文档。 此`BLOB`对象作为参数传递给`invokeOneDocument`。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段分配字节数组的内容，填充`BLOB`对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储要反汇编的PDF。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段指定表示键名的字符串值。 此值必须与在DDX文档中指定的PDF源元素值匹配。
   * 将存储PDF文档的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。

1. 设置运行时选项。

   * 使用其构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`字段。

1. 反汇编PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 一个`BLOB`对象，它表示分解PDF文档的DDX文档
   * 包含要反汇编的PDF文档的`MyMapOf_xsd_string_To_xsd_anyType`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个`AssemblerResult`对象，该对象包含作业结果和发生的任何异常。

1. 保存已拆解的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是一个`Map`对象，包含已拆解的PDF文档。
   * 对`Map`对象进行迭代以获得每个生成文档。 然后，将该数组成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`属性，提取表示PDF数据的二进制数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[以编程方式反汇编PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
