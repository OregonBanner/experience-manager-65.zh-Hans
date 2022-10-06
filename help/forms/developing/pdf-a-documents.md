---
title: 使用PDF/A文档
seo-title: Working with PDF/A Documents
description: 使用DocConverter服务确定PDF文档是否为PDF/A文档，并将PDF文档转换为PDF/A文档。
seo-description: Use the  DocConverter service to determine if a PDF document is a PDF/A document and convert PDF documents to PDF/A documents.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 0%

---

# 使用PDF/A文档 {#working-with-pdf-a-documents}

**关于DocConverter服务**

DocConverter服务可将PDF文档转换为PDA/A文档。 您可以使用此服务完成以下任务：

* 将PDF文档转换为PDF/A文档。 (请参阅 [将文档转换为PDF/A文档](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* 确定PDF文档是否为PDF/A文档。 (请参阅 [以编程方式确定PDF/符合性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>有关DocConverter服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 将文档转换为PDF/A文档 {#converting-documents-to-pdf-a-documents}

可以使用DocConverter服务将PDF文档转换为PDF/文档。 由于PDF/A是用于长期保留文档内容的存档格式，因此所有字体都会被嵌入并且文件未压缩。 因此，PDF/A文档通常比标准PDF文档大。 此外，PDF/文档不包含音频和视频内容。 在将PDF文档转换为PDF/A文档之前，请确保PDF文档不是PDF/A文档。

PDF/A-1规范由两个符合性级别组成，即A和B。二者的主要区别在于逻辑结构（无障碍）支持，这是符合性级别B不需要的。无论符合性级别如何，PDF/A-1都指示所有字体都嵌入在生成的PDF/A文档中。 目前，验证（和转换）仅支持PDF/A-1b。

虽然PDF/A是归档PDF文档的标准，但如果标准PDF文档符合您公司的要求，则不必强制使用PDF/A进行归档。 PDF/A标准旨在建立一个PDF文件，用于满足长期归档和文档保存需求。

>[!NOTE]
>
>有关DocConverter服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要将PDF文档转换为PDF/文档，请执行以下步骤：

1. 包括项目文件。
1. 创建DocConvert客户端
1. 引用PDF文档以转换为PDF/文档。
1. 设置跟踪信息。
1. 转换文档。
1. 保存PDF/文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此变量为必需变量)
* jbossall-client.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此为必需字段)

有关这些JAR文件的位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建DocConvert客户端**

在以编程方式执行DocConverter操作之前，必须创建DocConverter客户端。 如果您使用的是Java API，请创建 `DocConverterServiceClient` 对象。 如果您使用的是DocConverter Web服务API，请创建 `DocConverterServiceService` 对象。

**引用PDF文档以转换为PDF/文档**

检索PDF文档以转换为PDF/文档。 如果尝试将PDF文档(如Acrobat表单)转换为PDF/A文档，则会引发异常。

**设置跟踪信息**

您可以设置一个运行时选项，以确定在转化过程中跟踪的信息量。 也就是说，您可以设置9个不同级别，以指定DocConverter服务在将PDF文档转换为PDF/文档时跟踪的信息量。

**转换文档**

在创建DocConverter服务客户端后，引用要转换的PDF文档并设置指定跟踪信息量的运行时选项，您可以将PDF文档转换为PDF/A文档。

**保存PDF/文档**

您可以将PDF/A文档另存为PDF文件。

**另请参阅**

[使用Java API将文档转换为PDF/A文档](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[使用Web服务API将文档转换为PDF/A文档](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式确定PDF/符合性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### 使用Java API将文档转换为PDF/A文档 {#convert-documents-to-pdf-a-documents-using-the-java-api}

使用Java API将PDF文档转换为PDF/文档：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-docconverter-client.jar。

1. 创建DocConvert客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `DocConverterServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用PDF文档以转换为PDF/文档

   * 创建 `java.io.FileInputStream` 对象，该对象表示要通过使用其构造函数进行转换的PDF文档，并传递指定PDF文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置跟踪信息

   * 创建 `PDFAConversionOptionSpec` 对象。
   * 通过调用 `PDFAConversionOptionSpec` 对象 `setLogLevel` 方法和传递指定跟踪级别的字符串值。 例如，传递值 `FINE`. 有关不同值的信息，请参阅 `setLogLevel` 方法 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 转换文档

   通过调用 `DocConverterServiceClient` 对象 `toPDFA` 方法和传递以下值：

   * 的 `com.adobe.idp.Document` 包含要转换的PDF文档的对象
   * 的 `PDFAConversionOptionSpec` 指定跟踪信息的对象

   的 `toPDFA` 方法返回 `PDFAConversionResult` 包含PDF/A文档的对象。

1. 保存PDF/文档

   * 通过调用 `PDFAConversionResult` 对象 `getPDFA` 方法。 此方法将返回 `com.adobe.idp.Document` 表示PDF/A文档的对象。
   * 创建 `java.io.File` 表示PDF/A文件的对象。 确保文件扩展名为.pdf。
   * 通过调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法和通过 `java.io.File` 对象。

**另请参阅**

[使用PDF/A文档](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入门（SOAP模式）：使用Java API将文档转换为PDF/文档](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将文档转换为PDF/A文档 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

使用DocConverter API（Web服务）将PDF文档转换为PDF/A文档：

1. 包含项目文件

   * 创建使用DocConverter WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建DocConvert客户端

   * 使用Microsoft .NET客户端程序集，创建 `DocConverterServiceService` 对象。
   * 设置 `DocConverterServiceService` 对象 `Credentials` 具有 `System.Net.NetworkCredential` 指定用户名和密码值的值。

1. 引用PDF文档以转换为PDF/文档

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储转换为PDF/A文档的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及在中打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `binaryData` 属性。

1. 设置跟踪信息

   * 创建 `PDFAConversionOptionSpec` 对象。
   * 通过为 `PDFAConversionOptionSpec` 对象 `logLevel` 数据成员。 例如，分配值 `FINE` 到此数据成员。

1. 转换文档

   通过调用 `DocConverterServiceService` 对象 `toPDFA` 方法和传递以下值：

   * 的 `BLOB` 包含要转换的PDF文档的对象
   * 的 `PDFAConversionOptionSpec` 指定跟踪信息的对象

   的 `toPDFA` 方法返回 `PDFAConversionResult` 包含PDF/A文档的对象。

1. 保存PDF/文档

   * 创建 `BLOB` 用于通过获取PDF `PDFAConversionResult` 对象 `PDFADocument` 数据成员。
   * 创建用于存储 `BLOB` 使用 `PDFAConversionResult` 对象。 通过获取 `BLOB` 对象 `binaryData` 数据成员。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个表示PDF/A文档文件位置的字符串值。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[使用PDF/A文档](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以编程方式确定PDF/符合性 {#programmatically-determining-pdf-a-compliancy}

可以使用DocConverter服务确定PDF文档是否符合PDF/A。 有关PDF/A文档以及如何将PDF文档转换为PDF/A文档的信息，请参阅 [将文档转换为PDF/A文档](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>有关DocConverter服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-1}

要确定PDF/A合规性，请执行以下步骤：

1. 包括项目文件。
1. 创建DocConvert客户端
1. 引用用于确定PDF/A符合性的PDF文档。
1. 设置运行时选项。
1. 检索有关PDF文档的信息。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此变量为必需变量)
* jbossall-client.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此为必需字段)

有关这些JAR文件的位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建DocConvert客户端**

在以编程方式执行DocConverter操作之前，必须创建DocConverter客户端。 如果您使用的是Java API，请创建 `DocConverterServiceClient` 对象。 如果您使用的是DocConverter Web服务API，请创建 `DocConverterServiceService` 对象。

**引用用于确定PDF/A符合性的PDF文档**

必须引用PDF文档并将其传递到DocConverter服务，以确定PDF文档是否符合PDF/A。

**设置运行时选项**

您可以设置一个运行时选项，以确定在转化过程中跟踪的信息量。 也就是说，您可以设置9个不同级别，以指定DocConverter服务在将PDF文档转换为PDF/文档时跟踪的信息量。

**检索有关PDF文档的信息**

在创建DocConverter服务客户端、引用PDF文档并设置运行时选项后，可以确定PDF文档是否与PDF/A兼容。

**另请参阅**

[使用Java API确定PDF/A合规性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用Web服务API确定PDF/A合规性](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API确定PDF/A合规性 {#determine-pdf-a-compliancy-using-the-java-api}

使用Java API确定PDF/A合规性：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-docconverter-client.jar。

1. 创建DocConvert客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `DocConverterServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用用于确定PDF/A符合性的PDF文档

   * 创建 `java.io.FileInputStream` 对象，该对象表示要通过使用其构造函数进行转换的PDF文档，并传递指定PDF文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置运行时选项

   * 创建 `PDFAValidationOptionSpec` 对象。
   * 通过调用 `PDFAValidationOptionSpec` 对象 `setCompliance` 方法和传递 `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * 通过调用 `PDFAValidationOptionSpec` 对象 `setLogLevel` 方法和传递指定跟踪级别的字符串值。 例如，传递值 `FINE`. 有关不同值的信息，请参阅 `setLogLevel` 方法 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 检索有关PDF文档的信息

   通过调用 `DocConverterServiceClient` 对象 `isPDFA` 方法和传递以下值：

   * 的 `com.adobe.idp.Document` 包含PDF文档的对象。
   * 的 `PDFAValidationOptionSpec` 指定运行时选项的对象。

   的 `isPDFA` 方法返回 `PDFAValidationResult` 包含此操作结果的对象。

**另请参阅**

[使用PDF/A文档](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入门（SOAP模式）：使用Java API确定PDF/A合规性](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API确定PDF/A合规性 {#determine-pdf-a-compliancy-using-the-web-service-api}

使用Web服务API确定PDF/A合规性：

1. 包含项目文件

   * 创建使用DocConverter WSDL的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建DocConvert客户端

   * 使用Microsoft .NET客户端程序集，创建 `DocConverterServiceService` 对象。
   * 设置 `DocConverterServiceService` 对象 `Credentials` 具有 `System.Net.NetworkCredential` 指定用户名和密码值的值。

1. 引用用于确定PDF/A符合性的PDF文档

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储转换为PDF/A文档的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及在中打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `binaryData` 属性。

1. 设置运行时选项

   * 创建 `PDFAValidationOptionSpec` 对象。
   * 通过为 `PDFAValidationOptionSpec` 对象 `compliance` 具有值的数据成员 `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * 通过分配 `PDFAValidationOptionSpec` 对象 `resultLevel` 具有值的数据成员 `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. 检索有关PDF文档的信息

   通过调用 `DocConverterServiceService` 对象 `isPDFA` 方法和传递以下值：

   * 的 `BLOB` 包含PDF文档的对象。
   * 的 `PDFAValidationOptionSpec` 包含运行时选项的对象。

   的 `isPDFA` 方法返回 `PDFAValidationResult` 包含此操作结果的对象。

**另请参阅**

[使用PDF/A文档](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
