---
title: 将Postscript转换为PDF文档
seo-title: Converting Postscript to PDF Documents
description: 使用Distiller服务将PostScript®、封装的PostScript(EPS)和PRN文件转换为通过网络压缩、可靠和更安全的PDF文件。 Distiller服务使用Java API和Web服务API将大量打印文档转换为电子文档，如发票和报表。
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---

# 将Postscript转换为PDF文档 {#converting-postscript-to-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

## 关于Distiller服务 {#about-the-distiller-service}

Distiller®服务可将PostScript®、封装的PostScript(EPS)和PRN文件转换为通过网络压缩、可靠和更安全的PDF文件。 Distiller服务经常用于将大量打印文件转换为电子文件，如发票和报表。 将文档转换为PDF还允许企业向其客户发送文档的纸质版本和电子版本。

>[!NOTE]
>
>有关Distiller服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 将PostScript转换为PDF文档 {#converting-postscript-to-pdf-documents-inner}

本主题介绍如何使用Distiller服务API（Java和Web服务）以编程方式将PostScript(PS)、封装的PostScript(EPS)和PRN文件转换为PDF文档。

>[!NOTE]
>
>有关Distiller服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>要将PostScript文件转换为PDF文档，需要在托管AEM Forms的服务器上安装以下任一内容：Acrobat 9或Microsoft Visual C++ 2005可再发行包。

### 步骤摘要 {#summary-of-steps}

要将任何受支持的类型转换为PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Distiller服务客户端。
1. 检索要转换的文件。
1. 调用PDF创建操作。
1. 保存PDF文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Distiller服务客户端**

您必须先创建Distiller服务客户端，然后才能以编程方式执行Distiller服务操作。 如果您使用的是Java API，请创建 `DistillerServiceClient` 对象。 如果您使用的是Web服务API，请创建 `DistillerServiceService` 对象。

**检索要转换的文件**

必须检索要转换的文件。 例如，要将PS文件转换为PDF文档，必须检索PS文件。

**调用PDF创建操作**

创建服务客户端后，可以调用PDF创建操作。 此操作需要有关要转换的文档的信息，包括目标文档的路径。

**保存PDF文档**

您可以将PDF文档另存为PDF文件。

**另请参阅**

[使用Java API将PostScript文件转换为PDF](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[使用Web服务API将PostScript文件转换为PDF](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API将PostScript文件转换为PDF {#convert-a-postscript-file-to-pdf-using-the-java-api}

使用Distiller服务API(Java)将PostScript文件转换为PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-distiller-client.jar。

1. 创建Distiller服务客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `DistillerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 检索要转换的文件。

   * 创建 `java.io.FileInputStream` 对象，该对象表示使用其构造函数进行转换，并传递指定文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 调用PDF创建操作。

   调用 `DistillerServiceClient` 对象 `createPDF` 方法并传递以下值：

   * 的 `com.adobe.idp.Document` 表示要转换的PS、EPS或PRN文件的对象
   * A `java.lang.String` 包含要转换的文件名称的对象
   * A `java.lang.String` 包含要使用的Adobe PDF设置名称的对象
   * A `java.lang.String` 包含要使用的安全设置名称的对象
   * 可选 `com.adobe.idp.Document` 包含要在生成PDF文档时应用的设置的对象
   * 可选 `com.adobe.idp.Document` 包含要应用于PDF文档的元数据信息的对象

   的 `createPDF` 方法返回 `CreatePDFResult` 包含新PDF文档和可能生成的日志文件的对象。 日志文件通常包含由转换请求生成的错误或警告消息。

1. 保存PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `CreatePDFResult` 对象 `getCreatedDocument` 方法。 这会返回 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法提取PDF文档。

   同样，要获取日志文档，请执行以下操作。

   * 调用 `CreatePDFResult` 对象 `getLogDocument` 方法。 这会返回 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法提取日志文档。


**另请参阅**

[步骤摘要](converting-postscript-pdf-documents.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API将PostScript文件转换为PDF文档](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PostScript文件转换为PDF {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

使用Distiller服务API（Web服务）将PostScript文件转换为PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建Distiller服务客户端。

   * 创建 `DistillerServiceClient` 对象。
   * 创建 `DistillerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `DistillerServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 检索要转换的文件。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储要转换为PDF文档的文件。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示文件位置和在中打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 调用PDF创建操作。

   调用 `DistillerServiceService` 对象 `CreatePDF2` 方法，并传递以下必需值：

   * 的 `BLOB` 表示要转换的PS文件的对象
   * 包含要转换的文件的路径名的字符串
   * 包含要使用的Adobe PDF设置的字符串对象(例如， `Standard`)
   * 一个字符串对象，其中包含要使用的安全设置(例如， `No Securit`y)
   * 可选 `BLOB` 包含要在生成PDF文档时应用的设置的对象
   * 可选 `BLOB` 包含要应用于PDF文档的元数据信息的对象
   * A `BLOB` 用于存储PDF文档的输出参数
   * A `BLOB` 用于存储日志的输出参数

1. 保存PDF文档。

   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，该值表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `BLOB` 由返回的对象 `CreatePDF2` 方法（输出参数）。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
