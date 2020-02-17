---
title: 使用PDF/A文档
seo-title: 使用PDF/A文档
description: 'null'
seo-description: 'null'
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用PDF/A文档 {#working-with-pdf-a-documents}

**关于DocConverter服务**

DocConverter服务可将PDF文档转换为PDF/A文档。 您可以使用此服务完成以下任务：

* 将PDF文档转换为PDF/A文档。 (请参 [阅将文档转换为PDF/A文档](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。)
* 确定PDF文档是否为PDF/A文档。 (请参 [阅以编程方式确定PDF/A规范](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。)

>[!NOTE]
>
>有关DocConverter服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将文档转换为PDF/A文档 {#converting-documents-to-pdf-a-documents}

可以使用DocConverter服务将PDF文档转换为PDF/A文档。 由于PDF/A是用于长期保留文档内容的存档格式，因此嵌入了所有字体并且文件未压缩。 因此，PDF/A文档通常大于标准PDF文档。 此外，PDF/A文档不包含音频和视频内容。 在将PDF文档转换为PDF/A文档之前，请确保PDF文档不是PDF/A文档。

PDF/A-1规范由A和B两个符合性级别组成。两者的主要区别在于逻辑结构（辅助功能）支持，而符合性级别B不需要这些支持。无论符合性级别如何，PDF/A-1都规定所有字体都嵌入到生成的PDF/A文档中。 目前，验证（和转换）只支持PDF/A-1b。

虽然PDF/A是归档PDF文档的标准，但如果标准PDF文档满足您公司的要求，则不必将PDF/A用于归档。 PDF/A标准的目的是建立一个PDF文件，用于满足长期存档和文档保存需求。

>[!NOTE]
>
>有关DocConverter服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要将PDF文档转换为PDF/A文档，请执行以下步骤：

1. 包括项目文件。
1. 创建DocConvert客户端
1. 引用PDF文档以转换为PDF/A文档。
1. 设置跟踪信息。
1. 转换文档。
1. 保存PDF/A文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar（在JBoss Application server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建DocConvert客户端**

在以编程方式执行DocConverter操作之前，必须先创建DocConverter客户端。 如果您使用Java API，请创建一个对 `DocConverterServiceClient` 象。 如果您使用DocConverter web服务API，请创建一个对 `DocConverterServiceService` 象。

**引用PDF文档以转换为PDF/A文档**

检索PDF文档以转换为PDF/A文档。 如果尝试将PDF文档（如Acrobat表单）转换为PDF/A文档，则会引起异常。

**设置跟踪信息**

您可以设置运行时选项，以确定在转换过程中跟踪的信息量。 即，您可以设置九个不同级别，以指定DocConverter服务在将PDF文档转换为PDF/A文档时跟踪的信息量。

**转换文档**

在创建DocConverter服务客户端后，引用PDF文档进行转换并设置指定跟踪多少信息的运行时选项，您可以将PDF文档转换为PDF/A文档。

**保存PDF/A文档**

可将PDF/A文档另存为PDF文件。

**另请参阅**

[使用Java API将文档转换为PDF/A文档](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[使用Web服务API将文档转换为PDF/A文档](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式确定PDF/A兼容性](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### 使用Java API将文档转换为PDF/A文档 {#convert-documents-to-pdf-a-documents-using-the-java-api}

使用Java API将PDF文档转换为PDF/A文档：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-docconverter-client.jar。

1. 创建DocConvert客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DocConverterServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 引用PDF文档以转换为PDF/A文档

   * 创建一 `java.io.FileInputStream` 个对象，该对象使用其构造函数并传递一个指定PDF文件位置的字符串值来表示要转换的PDF文档。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 设置跟踪信息

   * 使用对 `PDFAConversionOptionSpec` 象的构造函数创建对象。
   * 通过调用对象的方法并传递 `PDFAConversionOptionSpec` 指定跟踪级 `setLogLevel` 别的字符串值来设置信息跟踪级别。 例如，传递值 `FINE`。 有关不同值的信息，请参阅 `setLogLevel` 《 [AEM Forms API参考》中的方法](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 转换文档

   通过调用对象的方法并传递以下值，将PDF文 `DocConverterServiceClient` 档转换 `toPDFA` 为PDF/A文档：

   * 包 `com.adobe.idp.Document` 含要转换的PDF文档的对象
   * 指定 `PDFAConversionOptionSpec` 跟踪信息的对象
   该方 `toPDFA` 法返回一 `PDFAConversionResult` 个包含PDF/A文档的对象。

1. 保存PDF/A文档

   * 通过调用对象的方法检索PDF/ `PDFAConversionResult` A文 `getPDFA` 档。 此方法返回 `com.adobe.idp.Document` 一个表示PDF/A文档的对象。
   * 创建 `java.io.File` 表示PDF/A文件的对象。 确保文件扩展名为。pdf。
   * 通过调用对象的方法并传递对象， `com.adobe.idp.Document` 用PDF/A `copyToFile` 数据填充文 `java.io.File` 件。

**另请参阅**

[使用PDF/A文档](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入门（SOAP模式）:使用Java API将文档转换为PDF/A文档](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将文档转换为PDF/A文档 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

使用DocConverter API（Web服务）将PDF文档转换为PDF/A文档：

1. 包括项目文件

   * 创建一个使用DocConverter WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建DocConvert客户端

   * 使用Microsoft .NET客户端程序集，通过调用 `DocConverterServiceService` 其默认构造函数创建对象。
   * 使用指 `DocConverterServiceService` 定用户名 `Credentials` 和口令值的值设置 `System.Net.NetworkCredential` 对象的数据成员。

1. 引用PDF文档以转换为PDF/A文档

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储转换为PDF/A文档的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `binaryData` 为字节数组的内容来填充对象。

1. 设置跟踪信息

   * 使用对 `PDFAConversionOptionSpec` 象的构造函数创建对象。
   * 通过为对象的数据成员分配一个指定跟踪级别的值来设 `PDFAConversionOptionSpec` 置信息跟 `logLevel` 踪级别。 例如，将值分配 `FINE` 给此数据成员。

1. 转换文档

   通过调用对象的方法并传递以下值，将PDF文 `DocConverterServiceService` 档转换 `toPDFA` 为PDF/A文档：

   * 包 `BLOB` 含要转换的PDF文档的对象
   * 指定 `PDFAConversionOptionSpec` 跟踪信息的对象
   该方 `toPDFA` 法返回一 `PDFAConversionResult` 个包含PDF/A文档的对象。

1. 保存PDF/A文档

   * 通过 `BLOB` 获取对象数据成员的值，创建存储PDF/A文 `PDFAConversionResult` 档的 `PDFADocument` 对象。
   * 创建一个字节数组，它存储使用对 `BLOB` 象返回的对象的内 `PDFAConversionResult` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `binaryData` 数组。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个表示PDF/A文档文件位置的字符串值来创建对象。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[使用PDF/A文档](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的。NET客户端组件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 以编程方式确定PDF/A兼容性 {#programmatically-determining-pdf-a-compliancy}

您可以使用DocConverter服务确定PDF文档是否符合PDF/A规范。 有关PDF/A文档以及如何将PDF文档转换为PDF/A文档的信息，请参阅将 [文档转换为PDF/A文档](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。

>[!NOTE]
>
>有关DocConverter服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要确定PDF/A规范，请执行以下步骤：

1. 包括项目文件。
1. 创建DocConvert客户端
1. 引用用于确定PDF/A规范的PDF文档。
1. 设置运行时选项。
1. 检索有关PDF文档的信息。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar（在JBoss Application server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application server上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建DocConvert客户端**

在以编程方式执行DocConverter操作之前，必须先创建DocConverter客户端。 如果您使用Java API，请创建一个对 `DocConverterServiceClient` 象。 如果您使用DocConverter web服务API，请创建一个对 `DocConverterServiceService` 象。

**引用用于确定PDF/A规范的PDF文档**

PDF文档必须被引用并传递给DocConverter服务，才能确定PDF文档是否符合PDF/A规范。

**设置运行时选项**

您可以设置运行时选项，以确定在转换过程中跟踪的信息量。 即，您可以设置9个不同级别，以指定DocConverter服务在将PDF文档转换为PDF/A文档时跟踪的信息量。

**检索有关PDF文档的信息**

在创建DocConverter服务客户端、引用PDF文档并设置运行时选项后，您可以确定PDF文档是否符合PDF/A规范。

**另请参阅**

[使用Java API确定PDF/A规范](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[使用Web服务API确定PDF/A规范](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API确定PDF/A规范 {#determine-pdf-a-compliancy-using-the-java-api}

使用Java API确定PDF/A规范：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-docconverter-client.jar。

1. 创建DocConvert客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `DocConverterServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 引用用于确定PDF/A规范的PDF文档

   * 创建一 `java.io.FileInputStream` 个对象，该对象使用其构造函数并传递一个指定PDF文件位置的字符串值来表示要转换的PDF文档。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 设置运行时选项

   * 使用对 `PDFAValidationOptionSpec` 象的构造函数创建对象。
   * 通过调用对象的方法并 `PDFAValidationOptionSpec` 传递来设置 `setCompliance` 规范级别 `PDFAValidationOptionSpec.Compliance.PDFA_1B`。
   * 通过调用对象的方法并传递 `PDFAValidationOptionSpec` 指定跟踪级 `setLogLevel` 别的字符串值来设置信息跟踪级别。 例如，传递值 `FINE`。 有关不同值的信息，请参阅 `setLogLevel` 《 [AEM Forms API参考》中的方法](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 检索有关PDF文档的信息

   通过调用对象的方法并传递 `DocConverterServiceClient` 以下值来确 `isPDFA` 定PDF/A规范：

   * 包 `com.adobe.idp.Document` 含PDF文档的对象。
   * 指定 `PDFAValidationOptionSpec` 运行时选项的对象。
   该方 `isPDFA` 法返回一 `PDFAValidationResult` 个包含此操作结果的对象。

**另请参阅**

[使用PDF/A文档](pdf-a-documents.md#working-with-pdf-a-documents)

[快速入门（SOAP模式）:使用Java API确定PDF/A规范](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API确定PDF/A规范 {#determine-pdf-a-compliancy-using-the-web-service-api}

使用Web服务API确定PDF/A规范：

1. 包括项目文件

   * 创建一个使用DocConverter WSDL的Microsoft .NET客户端组件。
   * 参考Microsoft .NET客户端程序集。

1. 创建DocConvert客户端

   * 使用Microsoft .NET客户端程序集，通过调用 `DocConverterServiceService` 其默认构造函数创建对象。
   * 使用指 `DocConverterServiceService` 定用户名 `Credentials` 和口令值的值设置 `System.Net.NetworkCredential` 对象的数据成员。

1. 引用用于确定PDF/A规范的PDF文档

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储转换为PDF/A文档的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `binaryData` 为字节数组的内容来填充对象。

1. 设置运行时选项

   * 使用对 `PDFAValidationOptionSpec` 象的构造函数创建对象。
   * 通过将对象的数据成员 `PDFAValidationOptionSpec` 赋值来设 `compliance` 置规范级别 `PDFAConversionOptionSpec_Compliance.PDFA_1B`。
   * 通过为对象的数据成员分配 `PDFAValidationOptionSpec` 值来设置 `resultLevel` 信息跟踪级别 `PDFAValidationOptionSpec_ResultLevel.DETAILED`。

1. 检索有关PDF文档的信息

   通过调用对象的方法并传递 `DocConverterServiceService` 以下值来确 `isPDFA` 定PDF/A规范：

   * 包 `BLOB` 含PDF文档的对象。
   * 包 `PDFAValidationOptionSpec` 含运行时选项的对象。
   该方 `isPDFA` 法返回一 `PDFAValidationResult` 个包含此操作结果的对象。

**另请参阅**

[使用PDF/A文档](pdf-a-documents.md#working-with-pdf-a-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的。NET客户端组件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
