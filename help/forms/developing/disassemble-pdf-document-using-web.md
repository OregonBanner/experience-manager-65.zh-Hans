---
title: 使用Web服务API拆解PDF文档
seo-title: 使用Web服务API拆解PDF文档
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

---


# 使用Web服务API拆解PDF文档 {#disassemble-a-pdf-document-usingthe-web-service-api}

使用Assembler Service API（Web服务）拆解PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保在设置服务引用时使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

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
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示DDX文档的文件位置和打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `MTOM` 为字节数组的内容来填充对象。

1. 引用PDF文档进行反汇编。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储输入的PDF文档。 此对 `BLOB` 象作为参数传递给 `invokeOneDocument` 该对象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过为 `BLOB` 对象的字段分配字 `MTOM` 节数组的内容来填充对象。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储要反汇编的PDF。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与DDX文档中指定的PDF源元素的值匹配。
   * 将存 `BLOB` 储PDF文档的对象指定到该对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象的字 `value` 段。
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用对 `MyMapOf_xsd_string_To_xsd_anyType` 象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请为对 `false` 象的字 `AssemblerOptionSpec` 段赋值 `failOnError` 。

1. 反汇编PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表示 `BLOB` 拆分PDF文档的DDX文档的对象
   * 包含 `MyMapOf_xsd_string_To_xsd_anyType` 要反汇编的PDF文档的对象
   * 指定 `AssemblerOptionSpec` 运行时选项的对象
   该方 `invokeDDX` 法返回一个对 `AssemblerResult` 象，其中包含作业结果和发生的任何例外。

1. 保存已拆卸的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含已拆 `Map` 卸的PDF文档的对象。
   * 遍历对象 `Map` 以获得每个生成的文档。 然后，将该阵列成员转 `value` 换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示该PDF文 `BLOB` 档的二进制数 `MTOM` 据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[以编程方式拆解PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
