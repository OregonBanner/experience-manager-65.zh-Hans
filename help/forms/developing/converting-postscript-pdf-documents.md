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

---


# 将Postscript转换为PDF文档 {#converting-postscript-to-pdf-documents}

## 关于Distiller服务 {#about-the-distiller-service}

Distiller®服务将PostScript®、封装的PostScript(EPS)和PRN文件转换为网络上紧凑、可靠和更安全的PDF文件。 Distiller服务经常用于将大量打印文档转换为电子文档，如发票和报表。 将文档转换为PDF还允许企业向客户发送文档的纸质版本和电子版本。

>[!NOTE]
>
>有关Distiller服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将PostScript转换为PDF文档 {#converting-postscript-to-pdf-documents-inner}

本主题介绍如何使用Distiller Service API（Java和Web服务）以编程方式将PostScript(PS)、封装的PostScript(EPS)和PRN文件转换为PDF文档。

>[!NOTE]
>
>有关Distiller服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>要将PostScript文件转换为PDF文档，需要在承载AEM Forms的服务器上安装以下任一内容：Acrobat 9或Microsoft Visual C++ 2005可再分发包。

### 步骤摘要 {#summary-of-steps}

要将任何支持的类型转换为PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Distiller服务客户端。
1. 检索要转换的文件。
1. 调用PDF创建操作。
1. 保存PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Distiller服务客户端**

在以编程方式执行Distiller服务操作之前，必须创建Distiller服务客户端。 如果您使用Java API，请创建一个对 `DistillerServiceClient` 象。 如果您使用Web服务API，请创建一个对 `DistillerServiceService` 象。

**检索要转换的文件**

必须检索要转换的文件。 例如，要将PS文件转换为PDF文档，必须检索PS文件。

**调用PDF创建操作**

在创建服务客户端后，可以调用PDF创建操作。 此操作需要有关要转换的文档的信息，包括目标文档的路径。

**保存PDF文档**

可将PDF文档另存为PDF文件。

**另请参阅**

[使用Java API将PostScript文件转换为PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用Web服务API将PostScript文件转换为PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API将PostScript文件转换为PDF {#convert-a-postscript-file-to-pdf-using-the-java-api}

使用Distiller Service API(Java)将PostScript文件转换为PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-distiller-client.jar。

1. 创建Distiller服务客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DistillerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索要转换的文件。

   * 创建一 `java.io.FileInputStream` 个对象，该对象使用其构造函数并传递一个指定文件位置的字符串值来表示要转换的文件。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 调用PDF创建操作。

   调用对 `DistillerServiceClient` 象的方 `createPDF` 法并传递以下值：

   * 表 `com.adobe.idp.Document` 示要转换的PS、EPS或PRN文件的对象
   * 包 `java.lang.String` 含要转换的文件名称的对象
   * 包 `java.lang.String` 含要使用的Adobe PDF设置名称的对象
   * 包 `java.lang.String` 含要使用的安全设置名称的对象
   * 一个可 `com.adobe.idp.Document` 选对象，其中包含在生成PDF文档时要应用的设置
   * 包含要 `com.adobe.idp.Document` 应用于PDF文档的元数据信息的可选对象
   该方 `createPDF` 法返回一个 `CreatePDFResult` 对象，该对象包含新的PDF文档和可能生成的日志文件。 日志文件通常包含由转换请求生成的错误或警告消息。

1. 保存PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `CreatePDFResult` 对象的方 `getCreatedDocument` 法。 这将返回一个 `com.adobe.idp.Document` 对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。
   同样，要获取日志文档，请执行以下操作。

   * 调用 `CreatePDFResult` 对象的方 `getLogDocument` 法。 这将返回一个 `com.adobe.idp.Document` 对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法提取日志文档。


**另请参阅**

[步骤摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速入门（SOAP模式）:使用Java API将PostScript文件转换为PDF文档](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PostScript文件转换为PDF {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

使用Distiller Service API（Web服务）将PostScript文件转换为PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Distiller服务客户端。

   * 使用对 `DistillerServiceClient` 象的默认构造函数创建对象。
   * 使用构 `DistillerServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/DistillerService?blob=mtom`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `DistillerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DistillerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `DistillerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换的文件。

   * 使用对 `BLOB` 象的构造函数创建对象。 此对 `BLOB` 象用于存储要转换为PDF文档的文件。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示文件位置以及在中打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `MTOM` 为字节数组的内容来填充对象。

1. 调用PDF创建操作。

   调用对 `DistillerServiceService` 象的方 `CreatePDF2` 法并传递以下所需值：

   * 表示 `BLOB` 要转换的PS文件的对象
   * 包含要转换的文件的路径名的字符串
   * 包含要使用的Adobe PDF设置的字符串对象(例如， `Standard`)
   * 包含要使用的安全设置的字符串对象(例如， `No Securit`y)
   * 一个可 `BLOB` 选对象，其中包含在生成PDF文档时要应用的设置
   * 包含要 `BLOB` 应用于PDF文档的元数据信息的可选对象
   * 用于 `BLOB` 存储PDF文档的输出参数
   * 用于 `BLOB` 存储日志的输出参数

1. 保存PDF文档。

   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，它存储由方 `BLOB` 法（输出参数）返 `CreatePDF2` 回的对象的内容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[步骤摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
