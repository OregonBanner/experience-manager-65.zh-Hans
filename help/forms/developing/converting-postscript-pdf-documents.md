---
title: 将Postscript转换为PDF文档
seo-title: 将Postscript转换为PDF文档
description: 'null'
seo-description: 'null'
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 0%

---


# 将Postscript转换为PDF文档{#converting-postscript-to-pdf-documents}

## 关于Distiller服务{#about-the-distiller-service}

Distiller®服务将PostScript®、封装的PostScript(EPS)和PRN文件转换为网络上紧凑、可靠和更安全的PDF文件。 Distiller服务经常用于将大量印刷文档转换为电子文档，如发票和报表。 将文档转换为PDF还允许企业向其客户发送纸质版本和电子版文档。

>[!NOTE]
>
>有关Distiller服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将PostScript转换为PDF文档{#converting-postscript-to-pdf-documents-inner}

本主题介绍如何使用Distiller服务API（Java和Web服务）以编程方式将PostScript(PS)、封装的PostScript(EPS)和PRN文件转换为PDF文档。

>[!NOTE]
>
>有关Distiller服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>要将PostScript文件转换为PDF文档，在承载AEM Forms的服务器上需要安装以下某项：Acrobat 9或Microsoft Visual C++ 2005可再发行包。

### 步骤{#summary-of-steps}的摘要

要将任何支持的类型转换为PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Distiller服务客户端。
1. 检索要转换的文件。
1. 调用PDF创建操作。
1. 保存PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Distiller服务客户端**

在以编程方式执行Distiller服务操作之前，必须创建Distiller服务客户端。 如果您使用Java API，请创建`DistillerServiceClient`对象。 如果您使用Web服务API，请创建`DistillerServiceService`对象。

**检索要转换的文件**

必须检索要转换的文件。 例如，要将PS文件转换为PDF文档，必须检索PS文件。

**调用PDF创建操作**

创建服务客户端后，您可以调用PDF创建操作。 此操作需要有关要转换的文档的信息，包括目标文档的路径。

**保存PDF文档**

可将PDF文档另存为PDF文件。

**另请参阅**

[使用Java API将PostScript文件转换为PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用Web服务API将PostScript文件转换为PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-postscript-file-to-pdf-using-the-java-api}将PostScript文件转换为PDF

使用Distiller服务API(Java)将PostScript文件转换为PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-distiller-client.jar。

1. 创建Distiller服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`DistillerServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 检索要转换的文件。

   * 创建一个`java.io.FileInputStream`对象，该对象使用其构造函数并传递一个指定文件位置的字符串值来表示要转换的文件。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 调用PDF创建操作。

   调用`DistillerServiceClient`对象的`createPDF`方法并传递以下值：

   * 表示要转换的PS、EPS或PRN文件的`com.adobe.idp.Document`对象
   * `java.lang.String`对象，其中包含要转换的文件的名称
   * `java.lang.String`对象，其中包含要使用的Adobe PDF设置的名称
   * `java.lang.String`对象，其中包含要使用的安全设置的名称
   * 可选`com.adobe.idp.Document`对象，包含在生成PDF文档时要应用的设置
   * 可选`com.adobe.idp.Document`对象，其中包含要应用于PDF文档的元数据信息

   `createPDF`方法返回一个`CreatePDFResult`对象，该对象包含新的PDF文档和可能生成的日志文件。 日志文件通常包含转换请求生成的错误或警告消息。

1. 保存PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用`CreatePDFResult`对象的`getCreatedDocument`方法。 这将返回`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDF文档。

   同样，要获取日志文档，请执行以下操作。

   * 调用`CreatePDFResult`对象的`getLogDocument`方法。 这将返回`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取日志文档。


**另请参阅**

[步骤摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API将PostScript文件转换为PDF文档](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#converting-a-postscript-file-to-pdf-using-the-web-service-api}将PostScript文件转换为PDF

使用Distiller服务API（Web服务）将PostScript文件转换为PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Distiller服务客户端。

   * 使用其默认构造函数创建`DistillerServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`DistillerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/DistillerService?blob=mtom`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。 但是，指定`?blob=mtom`以使用MTOM。
   * 通过获取`DistillerServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`DistillerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`DistillerServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换的文件。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 此`BLOB`对象用于存储要转换为PDF文档的文件。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示文件位置和在中打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。

1. 调用PDF创建操作。

   调用`DistillerServiceService`对象的`CreatePDF2`方法并传递以下必需值：

   * 表示要转换的PS文件的`BLOB`对象
   * 包含要转换的文件的路径名的字符串
   * 包含要使用的Adobe PDF设置的字符串对象（例如，`Standard`）
   * 包含要使用的安全设置的字符串对象（例如，`No Securit`y）
   * 可选`BLOB`对象，包含在生成PDF文档时要应用的设置
   * 可选`BLOB`对象，其中包含要应用于PDF文档的元数据信息
   * 用于存储PDF文档的`BLOB`输出参数
   * 用于存储日志的`BLOB`输出参数

1. 保存PDF文档。

   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`CreatePDF2`方法返回的`BLOB`对象的内容（输出参数）。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
