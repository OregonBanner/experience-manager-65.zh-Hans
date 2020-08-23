---
title: 在文件格式和PDF之间转换
seo-title: 在文件格式和PDF之间转换
description: 'null'
seo-description: 'null'
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '7842'
ht-degree: 0%

---


# 在文件格式和PDF之间转换 {#converting-between-file-formatsand-pdf}

**关于生成PDF服务**

“生成PDF”服务将本机文件格式转换为PDF。 它还将PDF转换为其他文件格式并优化PDF文档的大小。

“生成PDF”服务使用本机应用程序将以下文件格式转换为PDF。 除非另有说明，否则仅支持这些应用程序的德语、法语、英语和日语版本。 *仅Windows* 表示仅支持Windows Server® 2003和Windows Server 2008。

* 转换DOC、DOCX、RTF、TXT、XLS、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX、XPS和PUB（仅限Windows）

>[!NOTE]
>
>Acrobat® 9.2或更高版本才能将Microsoft XPS格式转换为PDF。

* Autodesk AutoCAD 2005、2006、2007、2008和2009可转换DWF、DWG和DXW（仅英文版）
* 转换WPD、QPW、SHW的Corel WordPerfect 12和X4（仅英文版）
* OpenOffice 2.0、2.4、3.0.1和3.1可转换ODT、ODS、ODP、ODG、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、XLSX、 PPT、 PPT、 PPPT、 PPPTtx、VSD、MPP、MPPX和PUB

>[!NOTE]
>
>“生成PDF”服务不支持64位版本的OpenOffice。

* Adobe Photoshop® CS2转换PSD（仅限Windows）

>[!NOTE]
>
>PhotoshopCS3和CS4不受支持，因为它们不支持Windows Server 2003或Windows Server 2008。

* Adobe FrameMaker® 7.2和8转换FM（仅限Windows）
* AdobePageMaker® 7.0转换PMD、PM6、P65和PM（仅限Windows）
* 第三方应用程序支持的本机格式（需要开发特定于该应用程序的设置文件）（仅限Windows）

“生成PDF”服务将以下基于标准的文件格式转换为PDF。

* 视频格式：SWF、FLV（仅限Windows）
* 图像格式：JPEG、JPG、JP2、J2Kí、JPC、J2C、GIF、BMP、TIFF、TIF、PNG、JPF
* HTML（Windows、Sun™ Solaris™和Linux®）

“生成PDF”服务将PDF转换为以下文件格式（仅限Windows）:

* 封装的PostScript(EPS)
* HTML3.2
* 带CSS 1.0的HTML 4.01
* DOC（Microsoft Word格式）
* RTF
* 文本（可访问和纯文本）
* XML
* 仅使用DeviceRGB色彩空间的PDF/A-1a
* 仅使用DeviceRGB色彩空间的PDF/A-1b

“生成PDF”服务要求您执行以下管理任务:

* 在承载AEM Forms的计算机上安装所需的本机应用程序
* 在承载Adobe Acrobat的计算机上安装AEM Forms专业版或Acrobat Pro扩展版9.2
* 执行安装后设置任务

使用JBoss Turnkey安装和部署AEM表单中介绍了这些任务。

您可以使用“生成PDF”服务完成以下任务:

* 从本机文件格式转换为PDF。
* 将HTML文档转换为PDF文档。
* 将PDF文档转换为文件格式。

>[!NOTE]
>
>有关生成PDF服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将Word文档转换为PDF文档 {#converting-word-documents-to-pdf-documents}

本节介绍如何使用“生成PDF API”以编程方式将Microsoft Word文档转换为PDF文档。

>[!NOTE]
>
>有关其他文件格式的详细信息，请参 [阅添加对其他本机文件格式的支持](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)。

>[!NOTE]
>
>有关生成PDF服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要将Microsoft Word文档转换为PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建“生成PDF”客户端。
1. 检索要转换为PDF文档的文件。
1. 将文件转换为PDF文档。
1. 检索结果。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建生成PDF客户端**

在以编程方式执行“生成PDF”操作之前，请先创建“生成PDF”服务客户端。 如果您使用Java API，请创建一个 `GeneratePdfServiceClient` 对象。 如果您使用Web服务API，请创建一个 `GeneratePDFServiceService` 对象。

**检索要转换为PDF文档的文件**

检索Microsoft Word文档以转换为PDF文档。

**将文件转换为PDF文档**

创建“生成PDF”服务客户端后，可以调用该 `createPDF2` 方法。 此方法需要有关要转换的文档的信息，包括文件扩展名。

**检索结果**

将文件转换为PDF文档后，可以检索结果。 例如，将Word文件转换为PDF文档后，可以检索并保存PDF文档。

**另请参阅**

[使用Java API将Word文档转换为PDF文档](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[使用Web服务API将Word文档转换为PDF文档](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF服务API快速开始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API将Word文档转换为PDF文档 {#convert-word-documents-to-pdf-documents-using-the-java-api}

使用“生成PDF API(Java)”将Microsoft Word文档转换为PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-generatepdf-client.jar。

1. 创建“生成PDF”客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `GeneratePdfServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索要转换为PDF文档的文件。

   * 使用构 `java.io.FileInputStream` 造函数创建一个表示要转换的Word文件的对象。 传递指定文件位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 将文件转换为PDF文档。

   通过调用对象的方法并传递以 `GeneratePdfServiceClient` 下值， `createPDF2` 将文件转换为PDF文档:

   * 表示 `com.adobe.idp.Document` 要转换的文件的对象。
   * 包 `java.lang.String` 含文件扩展名的对象。
   * 包含 `java.lang.String` 要在转换中使用的文件类型设置的对象。 文件类型设置提供不同文件类型（如。doc或。xls）的转换设置。
   * 包 `java.lang.String` 含要使用的PDF设置名称的对象。 For example, you can specify `Standard`.
   * 包 `java.lang.String` 含要使用的安全设置名称的对象。
   * 一个可 `com.adobe.idp.Document` 选对象，包含在生成PDF文档时要应用的设置。
   * 一个可 `com.adobe.idp.Document` 选对象，其中包含要应用于PDF文档的元数据信息。

   该方 `createPDF2` 法返回一 `CreatePDFResult` 个对象，该对象包含新的PDF文档和日志信息。 日志文件通常包含转换请求生成的错误或警告消息。

1. 检索结果。

   要获取PDF文档，请执行以下操作：

   * 调用对 `CreatePDFResult` 象的方 `getCreatedDocument` 法，该方法返回 `com.adobe.idp.Document` 对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，从上一步创建的对象中提取PDF文档。

   如果您使用 `createPDF2` 该方法获取日志文档（不适用于HTML转换），请执行以下操作：

   * 调用 `CreatePDFResult` 对象的方 `getLogDocument` 法。 这将返回一个 `com.adobe.idp.Document` 对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取日志文档。


**另请参阅**

[步骤摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API将Microsoft Word文档转换为PDF文档](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将Word文档转换为PDF文档 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

使用“生成PDF API（Web服务）”将Microsoft Word文档转换为PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替 `localhost` 换为承载AEM Forms的服务器的IP地址。

1. 创建“生成PDF”客户端。

   * 使用对象 `GeneratePDFServiceClient` 的默认构造函数创建对象。
   * 使用构 `GeneratePDFServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 但是，请指 `?blob=mtom`定。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `GeneratePDFServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段指定AEM表单用户名 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换为PDF文档的文件。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储要转换为PDF文档的文件。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示要转换的文件的位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取 `System.IO.FileStream` 的字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的属性 `MTOM` 分配字节数组的内容来填充对象。

1. 将文件转换为PDF文档。

   通过调用对象的方法并传递以 `GeneratePDFServiceService` 下值， `CreatePDF2` 将文件转换为PDF文档:

   * 表示 `BLOB` 要转换的文件的对象。
   * 包含文件扩展名的字符串。
   * 包含 `java.lang.String` 要在转换中使用的文件类型设置的对象。 文件类型设置提供不同文件类型（如。doc或。xls）的转换设置。
   * 包含要使用的PDF设置的字符串对象。 您可以指 `Standard`定。
   * 包含要使用的安全设置的字符串对象。 您可以指 `No Security`定。
   * 一个可 `BLOB` 选对象，包含在生成PDF文档时要应用的设置。
   * 一个可 `BLOB` 选对象，其中包含要应用于PDF文档的元数据信息。
   * 由该方法填 `BLOB` 充的输出参数 `CreatePDF2` 类型。 该方 `CreatePDF2` 法使用转换的文档填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 由该方法填 `BLOB` 充的输出参数 `CreatePDF2` 类型。 方 `CreatePDF2` 法使用日志文档填充此对象。 （此参数值仅对于Web服务调用是必需的）。

1. 检索结果。

   * 通过将对象的字段指定给字 `BLOB` 节数组来检 `MTOM` 索已转换的PDF文档。 字节数组表示转换的PDF文档。 确保使用 `BLOB` 用作方法输出参数的对 `createPDF2` 象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示已转换的PDF文档的文件位置。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入PDF文件。

**另请参阅**

[步骤摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将HTML文档转换为PDF文档 {#converting-html-documents-to-pdf-documents}

本节介绍如何使用“生成PDF API”以编程方式将HTML文档转换为PDF文档。

>[!NOTE]
>
>有关生成PDF服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要将HTML文档转换为PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建“生成PDF”客户端。
1. 检索要转换为PDF文档的HTML内容。
1. 将HTML内容转换为PDF文档。
1. 检索结果。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建生成PDF客户端**

在以编程方式执行“生成PDF”操作之前，必须创建“生成PDF”服务客户端。 如果您使用Java API，请创建一个 `GeneratePdfServiceClient` 对象。 如果您使用Web服务API，请创建 `GeneratePDFServiceService`。

**检索要转换为PDF文档的HTML内容**

引用要转换为PDF文档的HTML内容。 可引用HTML内容，如HTML文件或可通过URL访问的HTML内容。

**将HTML内容转换为PDF文档**

创建服务客户端后，可以调用相应的PDF创建操作。 此操作需要有关要转换的文档的信息，包括目标文档的路径。

**检索结果**

将HTML内容转换为PDF文档后，您可以检索结果并保存PDF文档。

**另请参阅**

[使用Java API将HTML内容转换为PDF文档](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[使用Web服务API将HTML内容转换为PDF文档](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF服务API快速开始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API将HTML内容转换为PDF文档 {#convert-html-content-to-a-pdf-document-using-the-java-api}

使用“生成PDF API(Java)”将HTML文档转换为PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-generatepdf-client.jar。

1. 创建“生成PDF”客户端。

   使用对 `GeneratePdfServiceClient` 象的构造函数并传递包含连接属 `ServiceClientFactory` 性的对象，创建对象。

1. 检索要转换为PDF文档的HTML内容。

   通过创建字符串变量并指定指向HTML内容的URL来检索HTML内容。

1. 将HTML内容转换为PDF文档。

   调用对 `GeneratePdfServiceClient` 象的方 `htmlToPDF2` 法并传递以下值：

   * 包 `java.lang.String` 含要转换的HTML文件URL的对象。
   * 包含 `java.lang.String` 要在转换中使用的文件类型设置的对象。 文件类型设置可以包括蜘蛛程度。
   * 包 `java.lang.String` 含要使用的安全设置名称的对象。
   * 一个可 `com.adobe.idp.Document` 选对象，包含在生成PDF文档时要应用的设置。 如果未提供此信息，则根据前三个参数自动选择设置。
   * 一个可 `com.adobe.idp.Document` 选对象，其中包含要应用于PDF文档的元数据信息。

1. 检索结果。

   该方 `htmlToPDF2` 法返回 `HtmlToPdfResult` 一个对象，该对象包含已生成的新PDF文档。 要获取新创建的PDF文档，请执行以下操作：

   * 调用 `HtmlToPdfResult` 对象的方 `getCreatedDocument` 法。 这将返回一个 `com.adobe.idp.Document` 对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，从上一步创建的对象中提取PDF文档。

**另请参阅**

[将HTML文档转换为PDF文档](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[快速开始（SOAP模式）:使用Java API将HTML内容转换为PDF文档](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[快速开始（SOAP模式）:使用Java API将HTML内容转换为PDF文档](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将HTML内容转换为PDF文档 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

使用“生成PDF API”（Web服务）将HTML内容转换为PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替 `localhost` 换为承载AEM Forms的服务器的IP地址。

1. 创建“生成PDF”客户端。

   * 使用对象 `GeneratePDFServiceClient` 的默认构造函数创建对象。
   * 使用构 `GeneratePDFServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 但是，请指 `?blob=mtom`定。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `GeneratePDFServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段指定AEM表单用户名 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换为PDF文档的HTML内容。

   通过创建字符串变量并指定指向HTML内容的URL来检索HTML内容。

1. 将HTML内容转换为PDF文档。

   通过调用对象的方法将HTML内容转 `GeneratePDFServiceService` 换为PDF文档 `HtmlToPDF2` 并传递以下值：

   * 包含要转换的HTML内容的字符串。
   * 包含 `java.lang.String` 要在转换中使用的文件类型设置的对象。
   * 包含要使用的安全设置的字符串对象。
   * 一个可 `BLOB` 选对象，包含在生成PDF文档时要应用的设置。
   * 一个可 `BLOB` 选对象，其中包含要应用于PDF文档的元数据信息。
   * 由该方法填 `BLOB` 充的输出参数 `CreatePDF2` 类型。 该方 `CreatePDF2` 法使用转换的文档填充此对象。 （此参数值仅对于Web服务调用是必需的）。

1. 检索结果。

   * 通过将对象的字段指定给字 `BLOB` 节数组来检 `MTOM` 索已转换的PDF文档。 字节数组表示转换的PDF文档。 确保使用 `BLOB` 用作方法输出参数的对 `HtmlToPDF2` 象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示已转换的PDF文档的文件位置。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入PDF文件。

**另请参阅**

[将HTML文档转换为PDF文档](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将PDF文档转换为非图像格式 {#converting-pdf-documents-to-non-image-formats}

本节介绍如何使用“生成PDF Java API”和“Web服务API”以编程方式将PDF文档转换为RTF文件（非图像格式的示例）。 其他非图像格式包括HTML、文本、DOC和EPS。 将PDF文档转换为RTF时，请确保PDF文档不包含表单元素，如提交按钮。 表单元素不会转换。

>[!NOTE]
>
>有关生成PDF服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要将PDF文档转换为任何支持的类型，请执行以下步骤：

1. 包括项目文件。
1. 创建“生成PDF”客户端。
1. 检索要转换的PDF文档。
1. 转换PDF文档。
1. 保存转换的文件。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建生成PDF客户端**

在以编程方式执行“生成PDF”操作之前，必须创建“生成PDF”服务客户端。 如果您使用Java API，请创建一个 `GeneratePdfServiceClient` 对象。 如果您使用Web服务API，请创建一个 `GeneratePDFServiceService` 对象。

**检索要转换的PDF文档**

检索PDF文档以转换为非图像格式。

**转换PDF文档**

创建服务客户端后，可以调用PDF导出操作。 此操作需要有关要转换的文档的信息，包括目标文档的路径。

**保存转换的文件**

保存转换的文件。 例如，如果将PDF文档转换为RTF文件，请将转换后的文档保存为RTF文件。

**另请参阅**

[使用Java API将PDF文档转换为RTF文件](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[使用Web服务API将PDF文档转换为RTF文件](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF服务API快速开始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API将PDF文档转换为RTF文件 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

使用“生成PDF API(Java)”将PDF文档转换为RTF文件：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-generatepdf-client.jar。

1. 创建“生成PDF”客户端。

   使用对 `GeneratePdfServiceClient` 象的构造函数并传递包含连接属 `ServiceClientFactory` 性的对象，创建对象。

1. 检索要转换的PDF文档。

   * 使用构 `java.io.FileInputStream` 造函数创建表示要转换的PDF文档的对象。 传递一个指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 转换PDF文档。

   调用对 `GeneratePdfServiceClient` 象的方 `exportPDF2` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` 要转换的PDF文件的对象。
   * 包 `java.lang.String` 含要转换的文件名称的对象。
   * 包 `java.lang.String` 含Adobe PDF设置名称的对象。
   * 一个 `ConvertPDFFormatType` 对象，它指定用于转换的目标文件类型。
   * 一个可 `com.adobe.idp.Document` 选对象，包含在生成PDF文档时要应用的设置。

   该方 `exportPDF2` 法返回 `ExportPDFResult` 包含已转换文件的对象。

1. 转换PDF文档。

   要获取新创建的文件，请执行以下操作：

   * 调用 `ExportPDFResult` 对象的方 `getConvertedDocument` 法。 这将返回一个 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法以提取新文档。

**另请参阅**

[步骤摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API将HTML内容转换为PDF文档](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PDF文档转换为RTF文件 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

使用“生成PDF API”（Web服务）将PDF文档转换为RTF文件：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替 `localhost` 换为承载AEM Forms的服务器的IP地址。

1. 创建Generate PDF客户端。

   * 使用对象 `GeneratePDFServiceClient` 的默认构造函数创建对象。
   * 使用构 `GeneratePDFServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 但是，请指 `?blob=mtom`定。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `GeneratePDFServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段指定AEM表单用户名 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储已转换的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取 `System.IO.FileStream` 的字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的属性 `MTOM` 分配字节数组的内容来填充对象。

1. 转换PDF文档。

   调用对 `GeneratePDFServiceServiceWse` 象的方 `ExportPDF2` 法并传递以下值：

   * 表示 `BLOB` 要转换的PDF文件的对象。
   * 包含要转换的文件的路径名的字符串。
   * 指定 `java.lang.String` 文件位置的对象。
   * 一个字符串对象，它指定用于转换的目标文件类型。 Specify `RTF`.
   * 一个可 `BLOB` 选对象，包含在生成PDF文档时要应用的设置。
   * 由该方法填 `BLOB` 充的输出参数 `ExportPDF2` 类型。 该方 `ExportPDF2` 法使用转换的文档填充此对象。 （此参数值仅对于Web服务调用是必需的）。

1. 保存转换的文件。

   * 将对象字段指定给字节数 `BLOB` 组，以检 `MTOM` 索转换的RTF文档。 字节数组表示转换的RTF文档。 确保使用 `BLOB` 用作方法输出参数的对 `ExportPDF2` 象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递表示RTF文件位置的字符串值。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入RTF文件。

**另请参阅**

[步骤摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 添加对其他本机文件格式的支持 {#adding-support-for-additional-native-file-formats}

本节介绍如何添加对其他本机文件格式的支持。 它概述了“生成PDF”服务与本服务用于将本机文件格式转换为PDF的本机应用程序之间的交互。

本节还介绍以下内容：

* 如何修改“生成PDF”服务对本产品已用于将本机文件格式转换为PDF的本机应用程序所提供的响应
* “生成PDF”服务、“生成PDF服务应用程序监视器”(AppMon)组件与本机应用程序（如Microsoft Word）之间的交互
* XML文法在这些交互中的作用

### 组件交互 {#component-interactions}

“生成PDF”服务通过调用与文件格式关联的应用程序，然后与应用程序交互以使用默认打印机打印文档，来转换本机文件格式。 默认打印机必须设置为Adobe PDF打印机。

此插图显示了与本机应用程序支持相关的组件和驱动程序。 还提到影响交互的XML文法。

用于本机文件转换的组件交互

此文档使用术语 *本机应用* ，以指示用于生成本机文件格式（如Microsoft Word）的应用程序。

*AppMon是* 一个企业组件，它与本机应用程序交互的方式与用户在该应用程序显示的对话框中导航的方式相同。 AppMon用来指示应用程序（如Microsoft Word）打开和打印文件的XML文法包含下列顺序任务:

1. 通过选择“文件”>“打开”打开文件
1. 确保显示“打开”对话框；如果不是，则处理错误
1. 在“文件名”字段中提供文件名，然后单击“打开”按钮
1. 确保文件实际打开
1. 通过选择“文件”>“打印”打开“打印”对话框
1. 确保显示“打印”对话框

AppMon使用标准Win32 API与第三方应用程序交互，以便传输UI事件，如按键和鼠标单击，这对于控制这些应用程序以从它们生成PDF文件非常有用。

由于这些Win32 API的限制，AppMon无法将这些UI事件分派到某些特定类型的窗口，如浮动菜单栏（在TextPad等某些应用程序中可找到）和某些类型的对话框，这些对话框的内容无法使用Win32 API检索。

可以很容易地以可视方式识别浮动菜单栏；但是，可能无法仅通过视觉检查来识别特殊类型的对话。 您需要第三方应用程序(如Microsoft Spy++(Microsoft Visual C++开发环境的一部分)或其等效的WinID(可从https://www.dennisbabkin.com/php/download.php?what=WinID免费下载 [](https://www.dennisbabkin.com/php/download.php?what=WinID))来检查对话框，以确定AppMon是否能够使用标准Win32 API与它交互。

如果WinID能够提取对话框内容，如文本、子窗口、窗口类ID等，则AppMon也能够提取。

此表列表了打印本机文件格式时使用的信息类型。

<table>
 <thead>
  <tr>
   <th><p>信息类型</p></th>
   <th><p>描述</p></th>
   <th><p>修改／创建与本机文件相关的条目 </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>管理设置 </p></td>
   <td><p>包括PDF设置、安全设置和文件类型设置。 </p><p>文件类型设置将文件扩展名与相应的本机应用程序相关联。 文件类型设置还指定用于打印本机文件的本机应用程序设置。 </p></td>
   <td><p>要更改已支持的本机应用程序的设置，系统管理员在管理控制台中设置“文件类型设置”。 </p><p>要添加对新本机文件格式的支持，必须手动编辑文件。 (请参 <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">阅添加或修改对本机文件格式的支持</a>。) </p></td>
  </tr>
  <tr>
   <td><p>脚本 </p></td>
   <td><p>指定“生成PDF”服务与本机应用程序之间的交互。 此类交互通常将应用程序打印到Adobe PDF驱动程序。 </p><p>该脚本包含指示本机应用程序打开特定对话框的说明，这些说明为这些对话框中的字段和按钮提供特定响应。 </p></td>
   <td><p>“生成PDF”服务包括所有支持的本机应用程序的脚本文件。 您可以使用XML编辑应用程序修改这些文件。</p><p>要添加对新本机应用程序的支持，必须创建新的脚本文件。 (请参 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">阅为本机应用程序创建或修改其他对话框XML文件</a>。) </p></td>
  </tr>
  <tr>
   <td><p>通用对话框说明 </p></td>
   <td><p>指定如何响应多个应用程序通用的对话框。 这些对话框由操作系统、帮助程序（如PDFMaker）和驱动程序生成。 </p><p>包含此信息的文件为appmon.global.en_US.xml。</p></td>
   <td><p>请勿修改此文件。 </p></td>
  </tr>
  <tr>
   <td><p>特定于应用程序的对话框说明</p></td>
   <td><p>指定如何响应特定于应用程序的对话框。 </p><p>包含此信息的文件为appmon。<i>“[appname]”</i>.dialog。<i>“[locale]</i>`.xml（例如，appmon.word.en_US.xml）。</p></td>
   <td><p>请勿修改此文件。 </p><p>要为新的本机应用程序添加对话框说明，请参 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">阅为本机应用程序创建或修改其他对话框XML文件</a>。</p></td>
  </tr>
  <tr>
   <td><p>其他特定于应用程序的对话框说明 </p></td>
   <td><p>指定对特定于应用程序的对话框说明的覆盖和添加。 本节介绍了此类信息的示例。 </p><p>包含此信息的文件为appmon。<i>“[appname]”</i>.addition。<i>“[locale]”</i>.xml。 一个示例是appmon.addition.en_US.xml。</p></td>
   <td><p>可以使用XML编辑应用程序创建和修改此类文件。 (请参 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">阅为本机应用程序创建或修改其他对话框XML文件</a>。) </p><p><strong>重要说明</strong>:必须为服务器将支持的每个本机应用程序创建其他特定于应用程序的对话框说明。 </p></td>
  </tr>
 </tbody>
</table>

### 关于脚本和对话框XML文件 {#about-the-script-and-dialog-xml-files}

脚本XML文件指示“生成PDF”服务以用户在应用程序对话框中导航的方式浏览应用程序对话框。 脚本XML文件还指示“生成PDF”服务通过执行按钮、选择或取消选择复选框或选择菜单项等操作来响应对话框。

相反，对话框XML文件只对对话框做出响应，其操作类型与脚本XML文件中使用的操作类型相同。

#### 对话框和窗口元素术语 {#dialog-box-and-window-element-terminology}

本节和下一节对对话框及其包含的组件使用不同的术语，具体取决于所描述的透视图。 对话框组件包括按钮、字段和组合框等项。

当本节和下一节从用户的角度描述对话框及其组件时，将使用 *对话框*、 *按钮*、 *字段*** 、组合框。

当此部分和下一部分从其内部表示的角度描述对话框及其组件时，将使 *用术语* “窗口”元素。 窗口元素的内部表示是层次结构，其中每个窗口元素实例都由标签标识。 窗口元素实例还描述其物理特性和行为。

从用户的角度来看，对话框及其组件显示不同的行为，其中某些对话框元素在激活前处于隐藏状态。 从内部代表性的角度来看，不存在此类行为问题。 例如，对话框的内部表示形式与其包含的组件的内部表示形式相似，但是组件嵌套在对话框中。

本节介绍提供AppMon的XML元素及说明。 这些元素具有元素 `dialog` 和元素等名 `window` 称。 此文档使用等宽字体来区分XML元素。 元 `dialog` 素标识出XML脚本文件可能导致有意或无意显示的对话框。 元 `window` 素标识窗口元素（对话框或对话框的组件）。

#### 层次结构 {#hierarchy}

此图显示了脚本和对话框XML的层次结构。 脚本XML文件符合script.xsd模式，它包括（在XML意义上）window.xsd模式。 同样，对话框XML文件符合dialogs.xsd模式，该模式还包括window.xsd。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

脚本和对话框XML的层次结构

#### 脚本XML文件 {#script-xml-files}

脚 *本XML文件* ，指定一系列步骤，这些步骤引导本机应用程序导航到某些窗口元素，然后向这些元素提供响应。 大多数响应是文本或按键，与用户向相应对话框中的字段、组合框或按钮提供的输入相对应。

“生成PDF”服务对脚本XML文件的支持旨在引导本机应用程序打印本机文件。 但是，脚本XML文件可用于完成用户在与本机应用程序对话框交互时可以执行的任何任务。

脚本XML文件中的步骤按顺序执行，无需任何分支机会。 支持的唯一条件测试是超时／重试，如果某个步骤在特定时间段内和特定数量的重试后未成功完成，则会导致脚本终止。

除了按顺序执行的步骤之外，步骤中的指令也按顺序执行。 您必须确保步骤和说明反映用户执行这些相同步骤的顺序。

脚本XML文件中的每个步骤都标识在成功执行该步骤的指令时应显示的窗口元素。 如果在执行脚本步骤时出现意外的对话框，“生成PDF”服务将按下一节所述搜索对话框XML文件。

#### 对话框XML文件 {#dialog-xml-files}

运行本机应用程序会显示不同的对话框，无论本机应用程序处于可见模式还是不可见模式，都会显示这些对话框。 对话框可以由操作系统或应用程序本身生成。 当本机应用程序在“生成PDF”服务的控制下运行时，系统和本机应用程序对话框显示在不可见窗口中。

对 *话框XML文件* ，指定“生成PDF”服务对系统或本机应用程序对话框的响应方式。 对话框XML文件允许“生成PDF”服务以方便转换过程的方式响应未提示的对话框。

当系统或本机应用程序显示当前执行的脚本XML文件未处理的对话框时，“生成PDF”服务将按此顺序搜索对话框XML文件，当它找到匹配项时停止：

* appmon。`[appname]`.additional.`[locale]`.xml
* appmon。`[appname]`。`[locale]`.xml（请勿修改此文件。）
* appmon.global.`[locale]`.xml（请勿修改此文件。）

如果“生成PDF”服务找到对话框的匹配项，则会通过发送为对话框指定的按键或其他操作将其取消。 如果对话框的说明指定了中止消息，则“生成PDF”服务将终止当前正在执行的作业并生成错误消息。 将在脚本XML语法的元素 `abortMessage` 中指定此类中止消息。

如果“生成PDF”服务遇到任何先前列出的文件中未描述的对话框，则“生成PDF”服务会将该对话框的标题并入日志文件条目中。 当前执行的作业最终超时。 然后，您可以使用日志文件中的信息在其他对话框XML文件中为本机应用程序编写新说明。

### 添加或修改对本机文件格式的支持 {#adding-or-modifying-support-for-a-native-file-format}

本节介绍支持其他本机文件格式或修改对已受支持的本机文件格式的支持时必须执行的任务。

在添加或修改支持之前，您必须完成以下任务。

#### 选择用于识别窗口元素的工具 {#choosing-a-tool-for-identifying-window-elements}

对话框和脚本XML文件要求您标识对话框或脚本元素所响应的窗口元素（对话框、字段或其他对话框组件）。 例如，在脚本调用本机应用程序的菜单后，脚本必须标识该菜单上要应用按键或动作的窗口元素。

您可以通过对话框在标题栏中显示的标题轻松标识对话框。 但是，必须使用Microsoft Spy++等工具来识别低级窗口元素。 低层窗口元素可以通过各种属性进行识别，这些属性并不明显。 此外，每个本机应用程序可以不同地标识其窗口元素。 因此，有多种方法可以识别窗口元素。 以下是考虑窗口要素标识的建议顺序：

1. 如果题注是唯一的
1. 控制ID，对于给定对话框，它可能唯一，也可能不唯一
1. 类名，可能唯一，也可能不唯一

这三个属性中的任何一个或一个组合都可以用于标识窗口。

如果属性无法标识题注，则可以通过使用窗口元素相对于其父元素的索引来标识窗口元素。 索 *引指* 定窗口元素相对于其同级窗口元素的位置。 索引通常是识别组合框的唯一方法。

请注意以下问题：

* Microsoft Spy++使用&amp;符号(&amp;)来标识字幕的热键，从而显示字幕。 例如，Spy++将一个“打印”对话框的描 `Pri&nt`述显示为，表示热键 *为n*。 脚本和对话框XML文件中的字幕标题必须忽略&amp;符号。
* 某些字幕包含换行符。 “生成PDF”服务无法识别换行。 如果题注包含换行符，则包含足够的题注以将其与其他菜单项区分开，然后对省略的部分使用常规表达式。 例如( `^Long caption title$`)。 (请参 [阅在题注属性中使用常规表达式](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)。)
* 对保留的XML字符使用字符实体（也称为转义序列）。 例如，对 `&` 于和号 `<` 、小 `>` 于和大于符号、 `&apos;` 撇号和 `&quot;` 引号使用。

如果您计划使用对话框或编写XML文件脚本，应安装应用程序Microsoft Spy++。

#### 取消对话框和脚本文件的打包 {#unpackaging-the-dialog-and-script-files}

对话框和脚本文件驻留在appmondata.jar文件中。 必须先取消打包此JAR文件，然后才能修改其中的任何文件或添加新的脚本或对话框文件。 例如，假定您要添加对EditPlus应用程序的支持。 创建两个XML文件，名为appmon.editplus.script.en_US.xml和appmon.editplus.script.addition.en_US.xml。 必须在以下两个位置将这些XML脚本添加到adobe-appmondata.jar文件中：

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon。 adobe-livecycle-native-jboss-x86_win32.ear文件位于的导出文件夹中 `[AEM forms install directory]\configurationManager`。 (如果AEM Forms部署在另一台J2EE应用程序服务器上，请用与您的J2EE应用程序服务器对应的EAR文件替换adobe-livecycle-native-jboss-x86_win32.ear文件。)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jar文件在adobe-generatepdf-dsc.jar文件中）。 adobe-generatepdf-dsc.jar文件在文件夹中 `[AEM forms install directory]\deploy` 。

将这些XML文件添加到adobe-appmondata.jar文件后，必须重新部署GeneratePDF组件。 要向adobe-appmondata.jar文件添加对话框和脚本XML文件，请执行以下任务:

1. 使用WinZip或WinRAR等工具，打开adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar文件。
1. 将对话框和脚本XML文件添加到appmondata.jar文件，或修改此文件中的现有XML文件。 (请参 [阅为本机应用程序创建或修改脚本XML文](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)件， [以及为本机应用程序创建或修改其他对话框XML文件](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)。)
1. 使用WinZip或WinRAR等工具，打开adobe-generatepdf-dsc.jar > adobe-appmondata.jar。
1. 将对话框和脚本XML文件添加到appmondata.jar文件，或修改此文件中的现有XML文件。 (请参 [阅为本机应用程序创建或修改脚本XML文](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)件， [以及为本机应用程序创建或修改其他对话框XML文件](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)。) 将XML文件添加到adobe-appmondata.jar文件后，将新的adobe-appmondata.jar文件放入adobe-generatepdf-dsc.jar文件中。
1. 如果添加了对其他本机文件格式的支持，请创建一个系统环境变量，它提供应用程序的路径(请参 [阅创建环境变量以查找本机应用程序](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)。)

**重新部署GeneratePDF组件**

1. 登录Workbench。
1. 选择 **窗口** >显 **示视图** > **组**&#x200B;件。 此操作会将“组件”视图添加到Workbench。
1. 右键单击“生成PDF”组件，然后选择“停 **止组件”**。
1. 组件停止后，右键单击并选择“卸载组件”以删除它。
1. 右键单击“组件 **”图标** ，然后选择 **安装组件**。
1. 浏览并选择修改后的adobe-generatepdf-dsc.jar文件，然后单击“打开”。 请注意，GeneratePDF组件旁边会显示一个红方。
1. 展开GeneratePDF组件，选择“服务描述符”，然后右键单击“生成PDF服务”，然后选择“激活服务”。
1. 在出现的配置对话框中，输入适用的配置值。 如果将这些值留空，则使用默认配置值。
1. 右键单击“生成PDF”，然后选择“开始组件”。
1. 扩展活动服务。 如果服务名称正在运行，则该服务名称旁边将显示绿色箭头。 否则，服务处于停止状态。
1. 如果服务处于停止状态，请右键单击服务名称，然后选择开始服务。

### 为本机应用程序创建或修改脚本XML文件 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

如果要将文件定向到新的本机应用程序，则必须为该应用程序创建一个脚本XML文件。 如果要修改生成PDF服务与已支持的本机应用程序交互的方式，则必须修改该应用程序的脚本。

该脚本包含在本机应用程序的窗口元素之间导航的说明，这些说明为这些元素提供特定响应。 包含此信息的文件为 `appmon.`[appname]&quot; `.script.`[locale]`.xml`。 一个示例是appmon.notepad.script.en_US.xml。

#### 确定脚本必须执行的步骤 {#identifying-steps-the-script-must-execute}

使用本机应用程序确定必须导航的窗口元素以及打印文档时必须执行的每个响应。 请注意任何响应产生的对话框。 这些步骤将类似于以下步骤：

1. 选择“文件”>“打开”。
1. 指定路径，然后单击“打开”。
1. 在菜单栏上选择“文件”>“打印”。
1. 指定打印机所需的属性。
1. 选择“打印”，然后等待“另存为”对话框出现。 “生成PDF”服务需要“另存为”对话框来指定PDF文件的目标。

#### 标识在题注属性中指定的对话框 {#identifying-the-dialogs-specified-in-caption-attributes}

使用Microsoft Spy++获取本机应用程序中窗口元素属性的标识。 您必须具有这些身份才能编写脚本。

#### 在字幕属性中使用常规表达式 {#using-regular-expressions-in-caption-attributes}

您可以在字幕规范中使用常规表达式。 “生成PDF”服务使用 `java.util.regex.Matcher` 类支持常规表达式。 该实用程序支持中所述的常规表达式 `java.util.regex.Pattern`。 (请访问Java网 [站](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html)https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html。)

**在记事本横幅中，将文件名放在记事本前面的常规表达式**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**常规表达式区分打印和打印设置**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### 对窗口和窗口排序列表元素 {#ordering-the-window-and-windowlist-elements}

您必须按如 `window` 下方 `windowList` 式订购和元素：

* 当多个 `window` 元素在某个或元素中显 `windowList` 示为子元素时， `dialog` 按降序排列这些元素，其名称长度 `window``caption` 表示该顺序中的位置。
* 当元素 `windowList` 中出现多个元素 `window` 时，按降序排列这些元素 `windowList` ，其中第一个元素的属性的长 `caption` 度表示该 `indexes/`顺序中的位置。

**将窗口元素排序到对话框文件中**

```xml
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**对windowList元素中的窗口元素进行排序**

```xml
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### 为本机应用程序创建或修改其他对话框XML文件 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

如果为以前不支持的本机应用程序创建脚本，则还必须为该应用程序创建一个额外的对话框XML文件。 AppMon使用的每个本机应用程序都必须只有一个额外的对话框XML文件。 即使不需要主动提供的对话框，也需要额外的对话框XML文件。 附加对话框必须至少包含一个元 `window` 素，即使该元素 `window` 只是占位符。

>[!NOTE]
>
>在此上下文中，术语“附加”指。xml `appmon.[applicationname].addition.[locale]`“文件的内容。 这样的文件会指定对话框XML文件的覆盖和添加。

您还可以出于以下目的修改本机应用程序的附加对话框XML文件：

* 用其他响应覆盖应用程序的对话框XML文件
* 添加对该应用程序对话框XML文件中未解决的对话框的响应

标识其他dialogXML文件的文件名为 `appmon.[appname].addition.[locale].xml`。 一个示例为appmon.excel.addition.en_US.xml。

附加对话框XML文件的名称必须使用格式， `appmon.[applicationname].addition.[locale].xml`其中 *applicationname* 必须与XML配置文件和脚本中使用的应用程序名称完全匹配。

>[!NOTE]
>
>native2pdfconfig.xml配置文件中指定的所有通用应用程序都没有主对话框XML文件。 添加或 [修改对本机文件格式的支持一节介绍](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) 此类规范。

您必须对元 `windowList` 素中显示为子元素的元 `window` 素进行排序。 (请参 [阅对窗口和窗口列表元素进行排序](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)。)

### 修改常规对话框XML文件 {#modifying-the-general-dialog-xml-file}

您可以修改常规对话框XML文件以响应由系统生成的对话框或响应多个应用程序通用的对话框。

#### 在XML配置文件中添加文件类型条目 {#adding-a-filetype-entry-in-the-xml-configuration-file}

此过程说明如何更新“生成PDF”服务配置文件，将文件类型与本机应用程序关联。 要更新此配置文件，必须使用管理控制台将配置数据导出到文件。 配置数据的默认文件名为native2pdfconfig.xml。

**更新“生成PDF”服务配置文件**

1. 选择 **“主页** ”>“ **服务** ” **>“Adobe PDF** 生成器 **”>“配置**&#x200B;文件”，然后选 ****&#x200B;择“配置”。
1. 根据需要 `filetype-settings` 修改native2pdfconfig.xml文件中的元素。
1. 选择 **“主页** ”>“ **服务** ” **>“Adobe PDF** 生成器&#x200B;**”>“配置**&#x200B;文件”，然后选 ****&#x200B;择配置文件。 配置数据将导入到“生成PDF”服务中，替换以前的设置。

>[!NOTE]
>
>应用程序的名称指定为元素属 `GenericApp` 性的 `name` 值。 此值必须与为该应用程序开发的脚本中指定的相应名称完全匹配。 同样，元 `GenericApp` 素的属 `displayName` 性应与相应脚本的窗口标题完 `expectedWindow` 全匹配。 在解析出现在或属性中的任何常规表达式后，将评估此 `displayName` 等价 `caption` 关系。

在此示例中，修改了随“生成PDF”服务提供的默认配置数据，以指定应使用记事本（而非Microsoft Word）处理文件扩展名为。txt的文件。 在进行此修改之前，将Microsoft Word指定为应处理此类文件的本机应用程序。

**将文本文件定向到记事本(native2pdfconfig.xml)的修改**

```xml
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### 创建环境变量以定位本机应用程序 {#creating-an-environment-variable-to-locate-the-native-application}

创建一个环境变量，它指定本机应用程序可执行文件的位置。 变量必须使用格式 `[applicationname]_PATH`，其中 *applicationname* 必须与XML配置文件和脚本中使用的应用程序名称完全匹配，并且路径包含多次引号中可执行文件的路径。 这样的环境变量的示例是 `Photoshop_PATH`。

创建新环境变量后，必须重新启动部署了“生成PDF”服务的服务器。

**在Windows XP环境中创建系统变量**

1. 选择 **控制面板>系统**。
1. 在“系统属性”对话框中，单击“高 **级** ”选项卡，然后单 **击“环境变量”**。
1. 在“环境变量”对话框的“系统变量”下，单击“ **新建**”。
1. 在“新建系统变量”对话框的“变 **量名称** ”框中，键入使用格式的名称 `[applicationname]_PATH`。
1. 在“变 **量值** ”框中，键入应用程序可执行文件的完整路径和文件名，然后单击“确 **定”**。 例如，类型： `c:\windows\Notepad.exe`
1. 在“环境变量”对话框中，单击“ **确定**”。

**从命令行创建系统变量**

1. 在命令行窗口中，使用以下格式键入变量定义：

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   例如，类型： `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 开始新的命令行提示符，使系统变量生效。

#### XML文件 {#xml-files}

AEM Forms包含示例XML文件，这些文件导致“生成PDF”服务使用记事本处理文件扩展名为。txt的任何文件。 此代码包含在本节中。 此外，您还必须进行本条所述的其他修改。

#### 附加对话框XML文件 {#additional-dialog-xml-file}

此示例包含记事本应用程序的其他对话框。 这些对话框可以是“生成PDF”服务指定的对话框的补充。

**记事本对话框(appmon.notepad.addition.en_US.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### 脚本XML文件 {#script-xml-file}

此示例指定Generate PDF服务如何与记事本交互，以使用Adobe PDF打印机打印文件。

**记事本脚本XML文件(appmon.notepad.script.en_US.xml)**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```

