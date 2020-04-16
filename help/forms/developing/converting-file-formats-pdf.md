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
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 在文件格式和PDF之间转换 {#converting-between-file-formatsand-pdf}

**关于生成PDF服务**

“生成PDF”服务将本机文件格式转换为PDF。 它还将PDF转换为其他文件格式并优化PDF文档的大小。

“生成PDF”服务使用本机应用程序将以下文件格式转换为PDF。 除非另有说明，否则仅支持这些应用程序的德语、法语、英语和日语版本。 *仅Windows* 表示仅支持Windows Server® 2003和Windows Server 2008。

* 转换DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、PPTX、VSD、MPP、MPPX、XPS和PUB的Microsoft Office 2003和2007（仅限Windows）

>[!NOTE]
>
>需要Acrobat® 9.2或更高版本才能将Microsoft XPS格式转换为PDF。

* Autodesk AutoCAD 2005、2006、2007、2008和2009可转换DWF、DWG和DXW（仅英文版）
* 转换WPD、QPW、SHW的Corel WordPerfect 12和X4（仅英文版）
* OpenOffice 2.0、2.4、3.0.1和3.1可转换ODT、ODS、ODP、ODG、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、XLSX、 PPPSX、 PPPT、 PPPT、 PPP、 PPPtx、VSD、MPP、MPPX和PUB

>[!NOTE]
>
>“生成PDF”服务不支持64位版本的OpenOffice。

* 转换PSD的Adobe Photoshop® CS2（仅限Windows）

>[!NOTE]
>
>不支持Photoshop CS3和CS4，因为它们不支持Windows Server 2003或Windows Server 2008。

* 转换FM的Adobe FrameMaker® 7.2和8（仅限Windows）
* 用于转换PMD、PM6、P65和PM的Adobe PageMaker® 7.0（仅限Windows）
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

生成PDF服务要求您执行以下管理任务:

* 在承载AEM Forms的计算机上安装所需的本机应用程序
* 在承载AEM Forms的计算机上安装Adobe Acrobat Professional或Acrobat Pro Extended 9.2
* 执行安装后设置任务

使用JBoss Tunkly安装和部署AEM表单中介绍了这些任务。

您可以使用“生成PDF”服务完成以下任务:

* 从本机文件格式转换为PDF。
* 将HTML文档转换为PDF文档。
* 将PDF文档转换为文件格式。

>[!NOTE]
>
>有关生成PDF服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将Word文档转换为PDF文档 {#converting-word-documents-to-pdf-documents}

本节介绍如何使用“生成PDF API”以编程方式将Microsoft Word文档转换为PDF文档。

>[!NOTE]
>
>有关其他文件格式的详细信息，请参 [阅添加对其他本机文件格式的支持](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)。

>[!NOTE]
>
>有关生成PDF服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要将Microsoft Word文档转换为PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建“生成PDF”客户端。
1. 检索要转换为PDF文档的文件。
1. 将文件转换为PDF文档。
1. 检索结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建生成PDF客户端**

在以编程方式执行“生成PDF”操作之前，请先创建“生成PDF”服务客户端。 如果您使用Java API，请创建一个对 `GeneratePdfServiceClient` 象。 如果您使用Web服务API，请创建一个对 `GeneratePDFServiceService` 象。

**检索要转换为PDF文档的文件**

检索Microsoft Word文档以转换为PDF文档。

**将文件转换为PDF文档**

在创建“生成PDF”服务客户端后，可以调用该 `createPDF2` 方法。 此方法需要有关要转换的文档的信息，包括文件扩展名。

**检索结果**

将文件转换为PDF文档后，可以检索结果。 例如，将Word文件转换为PDF文档后，可以检索并保存PDF文档。

**另请参阅**

[使用Java API将Word文档转换为PDF文档](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[使用Web服务API将Word文档转换为PDF文档](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF Service API快速开始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API将Word文档转换为PDF文档 {#convert-word-documents-to-pdf-documents-using-the-java-api}

使用“生成PDF API(Java)”将Microsoft Word文档转换为PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-generatepdf-client.jar。

1. 创建“生成PDF”客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `GeneratePdfServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索要转换为PDF文档的文件。

   * 创建一 `java.io.FileInputStream` 个对象，它使用其构造函数表示要转换的Word文件。 传递指定文件位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 将文件转换为PDF文档。

   通过调用对象的方法并传递以 `GeneratePdfServiceClient` 下值，将文 `createPDF2` 件转换为PDF文档:

   * 表示 `com.adobe.idp.Document` 要转换的文件的对象。
   * 包含 `java.lang.String` 文件扩展名的对象。
   * 包含 `java.lang.String` 要在转换中使用的文件类型设置的对象。 文件类型设置为不同文件类型（如。doc或。xls）提供转换设置。
   * 包 `java.lang.String` 含要使用的PDF设置名称的对象。 For example, you can specify `Standard`.
   * 包 `java.lang.String` 含要使用的安全设置名称的对象。
   * 可选对 `com.adobe.idp.Document` 象，其中包含在生成PDF文档时要应用的设置。
   * 一个可 `com.adobe.idp.Document` 选对象，其中包含要应用于PDF文档的元数据信息。
   该方 `createPDF2` 法返回一 `CreatePDFResult` 个对象，该对象包含新的PDF文档和日志信息。 日志文件通常包含由转换请求生成的错误或警告消息。

1. 检索结果。

   要获取PDF文档，请执行以下操作：

   * 调用对 `CreatePDFResult` 象的方 `getCreatedDocument` 法，该方法返回一 `com.adobe.idp.Document` 个对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，以从在上一步中创建的对象中提取PDF文档。
   如果您使用该方 `createPDF2` 法获取日志文档（不适用于HTML转换），请执行以下操作：

   * 调用 `CreatePDFResult` 对象的方 `getLogDocument` 法。 这将返回一个 `com.adobe.idp.Document` 对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取日志文档。


**另请参阅**

[步骤摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API将Microsoft Word文档转换为PDF文档](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将Word文档转换为PDF文档 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

使用“生成PDF API（Web服务）”将Microsoft Word文档转换为PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建“生成PDF”客户端。

   * 使用对 `GeneratePDFServiceClient` 象的默认构造函数创建对象。
   * 使用构 `GeneratePDFServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.)您无需使用该属 `lc_version` 性。 但是，请指 `?blob=mtom`定。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `GeneratePDFServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换为PDF文档的文件。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储要转换为PDF文档的文件。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示要转换的文件的位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的属性分配字 `MTOM` 节数组的内容来填充对象。

1. 将文件转换为PDF文档。

   通过调用对象的方法并传递以 `GeneratePDFServiceService` 下值，将文 `CreatePDF2` 件转换为PDF文档:

   * 表示 `BLOB` 要转换的文件的对象。
   * 包含文件扩展名的字符串。
   * 包含 `java.lang.String` 要在转换中使用的文件类型设置的对象。 文件类型设置为不同文件类型（如。doc或。xls）提供转换设置。
   * 包含要使用的PDF设置的字符串对象。 您可以指定 `Standard`。
   * 包含要使用的安全设置的字符串对象。 您可以指定 `No Security`。
   * 可选对 `BLOB` 象，其中包含在生成PDF文档时要应用的设置。
   * 一个可 `BLOB` 选对象，其中包含要应用于PDF文档的元数据信息。
   * 由该方法填充 `BLOB` 的输出参数类型 `CreatePDF2` 。 该方 `CreatePDF2` 法使用转换的文档填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 由该方法填充 `BLOB` 的输出参数类型 `CreatePDF2` 。 该方 `CreatePDF2` 法使用日志文档填充此对象。 （此参数值仅对于Web服务调用是必需的）。

1. 检索结果。

   * 通过将对象的字段指定给字节数 `BLOB` 组，检索转 `MTOM` 换的PDF文档。 字节数组表示转换的PDF文档。 确保使用 `BLOB` 用作方法输出参数的对 `createPDF2` 象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个表示已转换的PDF文档的文件位置的字符串值来创建对象。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[步骤摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将HTML文档转换为PDF文档 {#converting-html-documents-to-pdf-documents}

本节介绍如何使用“生成PDF API”以编程方式将HTML文档转换为PDF文档。

>[!NOTE]
>
>有关生成PDF服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要将HTML文档转换为PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建“生成PDF”客户端。
1. 检索要转换为PDF文档的HTML内容。
1. 将HTML内容转换为PDF文档。
1. 检索结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建生成PDF客户端**

在以编程方式执行“生成PDF”操作之前，必须创建“生成PDF”服务客户端。 如果您使用Java API，请创建一个对 `GeneratePdfServiceClient` 象。 如果您使用Web服务API，请创建 `GeneratePDFServiceService`。

**检索要转换为PDF文档的HTML内容**

引用要转换为PDF文档的HTML内容。 可引用HTML内容，如HTML文件或可使用URL访问的HTML内容。

**将HTML内容转换为PDF文档**

创建服务客户端后，可以调用相应的PDF创建操作。 此操作需要有关要转换的文档的信息，包括目标文档的路径。

**检索结果**

将HTML内容转换为PDF文档后，您可以检索结果并保存PDF文档。

**另请参阅**

[使用Java API将HTML内容转换为PDF文档](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[使用Web服务API将HTML内容转换为PDF文档](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF Service API快速开始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API将HTML内容转换为PDF文档 {#convert-html-content-to-a-pdf-document-using-the-java-api}

使用“生成PDF API(Java)”将HTML文档转换为PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-generatepdf-client.jar。

1. 创建“生成PDF”客户端。

   使用对 `GeneratePdfServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 检索要转换为PDF文档的HTML内容。

   通过创建字符串变量并指定指向HTML内容的URL来检索HTML内容。

1. 将HTML内容转换为PDF文档。

   调用对 `GeneratePdfServiceClient` 象的方 `htmlToPDF2` 法并传递以下值：

   * 包 `java.lang.String` 含要转换的HTML文件URL的对象。
   * 包含 `java.lang.String` 要在转换中使用的文件类型设置的对象。 文件类型设置可以包括色阶。
   * 包 `java.lang.String` 含要使用的安全设置名称的对象。
   * 可选对 `com.adobe.idp.Document` 象，其中包含在生成PDF文档时要应用的设置。 如果未提供此信息，则根据前三个参数自动选择设置。
   * 一个可 `com.adobe.idp.Document` 选对象，其中包含要应用于PDF文档的元数据信息。

1. 检索结果。

   该方 `htmlToPDF2` 法返回一 `HtmlToPdfResult` 个对象，该对象包含已生成的新PDF文档。 要获取新创建的PDF文档，请执行以下操作：

   * 调用 `HtmlToPdfResult` 对象的方 `getCreatedDocument` 法。 这将返回一个 `com.adobe.idp.Document` 对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，以从在上一步中创建的对象中提取PDF文档。

**另请参阅**

[将HTML文档转换为PDF文档](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[快速开始（SOAP模式）:使用Java API将HTML内容转换为PDF文档](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[快速开始（SOAP模式）:使用Java API将HTML内容转换为PDF文档](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将HTML内容转换为PDF文档 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

使用“生成PDF API”（Web服务）将HTML内容转换为PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建“生成PDF”客户端。

   * 使用对 `GeneratePDFServiceClient` 象的默认构造函数创建对象。
   * 使用构 `GeneratePDFServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.)您无需使用该属 `lc_version` 性。 但是，请指 `?blob=mtom`定。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `GeneratePDFServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换为PDF文档的HTML内容。

   通过创建字符串变量并指定指向HTML内容的URL来检索HTML内容。

1. 将HTML内容转换为PDF文档。

   通过调用对象的方法将HTML内容转换为PDF文档, `GeneratePDFServiceService` 并传递 `HtmlToPDF2` 以下值：

   * 包含要转换的HTML内容的字符串。
   * 包含 `java.lang.String` 要在转换中使用的文件类型设置的对象。
   * 包含要使用的安全设置的字符串对象。
   * 可选对 `BLOB` 象，其中包含在生成PDF文档时要应用的设置。
   * 一个可 `BLOB` 选对象，其中包含要应用于PDF文档的元数据信息。
   * 由该方法填充 `BLOB` 的输出参数类型 `CreatePDF2` 。 该方 `CreatePDF2` 法使用转换的文档填充此对象。 （此参数值仅对于Web服务调用是必需的）。

1. 检索结果。

   * 通过将对象的字段指定给字节数 `BLOB` 组，检索转 `MTOM` 换的PDF文档。 字节数组表示转换的PDF文档。 确保使用 `BLOB` 用作方法输出参数的对 `HtmlToPDF2` 象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个表示已转换的PDF文档的文件位置的字符串值来创建对象。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[将HTML文档转换为PDF文档](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将PDF文档转换为非图像格式 {#converting-pdf-documents-to-non-image-formats}

本节介绍如何使用“生成PDF Java API”和“Web服务API”以编程方式将PDF文档转换为RTF文件（非图像格式的示例）。 其他非图像格式包括HTML、文本、DOC和EPS。 将PDF文档转换为RTF时，请确保PDF文档不包含表单元素，如提交按钮。 表单元素不会转换。

>[!NOTE]
>
>有关生成PDF服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要将PDF文档转换为任何支持的类型，请执行以下步骤：

1. 包括项目文件。
1. 创建“生成PDF”客户端。
1. 检索要转换的PDF文档。
1. 转换PDF文档。
1. 保存转换的文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建生成PDF客户端**

在以编程方式执行“生成PDF”操作之前，必须创建“生成PDF”服务客户端。 如果您使用Java API，请创建一个对 `GeneratePdfServiceClient` 象。 如果您使用Web服务API，请创建一个对 `GeneratePDFServiceService` 象。

**检索要转换的PDF文档**

检索PDF文档以转换为非图像格式。

**转换PDF文档**

创建服务客户端后，可以调用PDF导出操作。 此操作需要有关要转换的文档的信息，包括目标文档的路径。

**保存转换的文件**

保存转换的文件。 例如，如果将PDF文档转换为RTF文件，请将转换后的文档保存为RTF文件。

**另请参阅**

[使用Java API将PDF文档转换为RTF文件](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[使用Web服务API将PDF文档转换为RTF文件](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[生成PDF Service API快速开始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### 使用Java API将PDF文档转换为RTF文件 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

使用“生成PDF API(Java)”将PDF文档转换为RTF文件：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-generatepdf-client.jar。

1. 创建“生成PDF”客户端。

   使用对 `GeneratePdfServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 检索要转换的PDF文档。

   * 创建一 `java.io.FileInputStream` 个对象，它使用其构造函数表示要转换的PDF文档。 传递一个指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 转换PDF文档。

   调用对 `GeneratePdfServiceClient` 象的方 `exportPDF2` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` 要转换的PDF文件的对象。
   * 包 `java.lang.String` 含要转换的文件名称的对象。
   * 包 `java.lang.String` 含Adobe PDF设置名称的对象。
   * 一个 `ConvertPDFFormatType` 对象，它指定转换的目标文件类型。
   * 可选对 `com.adobe.idp.Document` 象，其中包含在生成PDF文档时要应用的设置。
   该方 `exportPDF2` 法返回一个 `ExportPDFResult` 包含已转换文件的对象。

1. 转换PDF文档。

   要获取新创建的文件，请执行以下操作：

   * 调用 `ExportPDFResult` 对象的方 `getConvertedDocument` 法。 这将返回一个 `com.adobe.idp.Document` 对象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法提取新文档。

**另请参阅**

[步骤摘要](converting-file-formats-pdf.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API将HTML内容转换为PDF文档](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PDF文档转换为RTF文件 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

使用“生成PDF API”（Web服务）将PDF文档转换为RTF文件：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Generate PDF客户端。

   * 使用对 `GeneratePDFServiceClient` 象的默认构造函数创建对象。
   * 使用构 `GeneratePDFServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.)您无需使用该属 `lc_version` 性。 但是，请指 `?blob=mtom`定。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `GeneratePDFServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `GeneratePDFServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储已转换的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的属性分配字 `MTOM` 节数组的内容来填充对象。

1. 转换PDF文档。

   调用对 `GeneratePDFServiceServiceWse` 象的方 `ExportPDF2` 法并传递以下值：

   * 表示 `BLOB` 要转换的PDF文件的对象。
   * 包含要转换的文件路径名的字符串。
   * 指定 `java.lang.String` 文件位置的对象。
   * 一个字符串对象，它指定用于转换的目标文件类型。 指定 `RTF`。
   * 可选对 `BLOB` 象，其中包含在生成PDF文档时要应用的设置。
   * 由该方法填充 `BLOB` 的输出参数类型 `ExportPDF2` 。 该方 `ExportPDF2` 法使用转换的文档填充此对象。 （此参数值仅对于Web服务调用是必需的）。

1. 保存转换的文件。

   * 通过将对象的字段指定给字 `BLOB` 节数组来检 `MTOM` 索转换的RTF文档。 字节数组表示转换的RTF文档。 确保使用 `BLOB` 用作方法输出参数的对 `ExportPDF2` 象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递表示RTF文件位置的字符串值。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字节数组的 `System.IO.BinaryWriter` 内容写 `Write` 入RTF文件。

**另请参阅**

[步骤摘要](converting-file-formats-pdf.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 添加对其他本机文件格式的支持 {#adding-support-for-additional-native-file-formats}

本节介绍如何添加对其他本机文件格式的支持。 它概述了“生成PDF”服务与本服务用于将本机文件格式转换为PDF的本机应用程序之间的交互。

本节还介绍以下内容：

* 如何修改“生成PDF”服务对本产品已用于将本机文件格式转换为PDF的本机应用程序所提供的响应
* 生成PDF服务、生成PDF服务应用程序监视器(AppMon)组件与本机应用程序（如Microsoft Word）之间的交互
* XML文法在这些交互中所扮演的角色

### 组件交互 {#component-interactions}

“生成PDF”服务通过调用与文件格式关联的应用程序，然后与应用程序交互以使用默认打印机打印文档，来转换本机文件格式。 默认打印机必须设置为Adobe PDF打印机。

此插图显示了与本机应用程序支持相关的组件和驱动程序。 它还提到影响交互的XML文法。

用于本机文件转换的组件交互

此文档使用术语 *本机应用程序* ，以指示用于生成本机文件格式的应用程序，如Microsoft Word。

*AppMon是一个企业组件，它与本机应用程序交互的方式与用户在该应用程序显示的对话框中导航的方式相同。* AppMon用来指示应用程序（如Microsoft Word）打开和打印文件的XML文法包含以下顺序任务:

1. 通过选择“文件”>“打开”打开文件
1. 确保显示“打开”对话框；如果不是，则处理错误
1. 在“文件名”字段中提供文件名，然后单击“打开”按钮
1. 确保文件实际打开
1. 通过选择“文件”>“打印”打开“打印”对话框
1. 确保显示“打印”对话框

AppMon使用标准Win32 API与第三方应用程序交互，以便传输UI事件，如按键和鼠标单击，这对于控制这些应用程序从它们生成PDF文件非常有用。

由于这些Win32 API的限制，AppMon无法将这些UI事件分派到某些特定类型的窗口，如浮动菜单栏（在某些应用程序中如TextPad）和某些类型的对话框，这些对话框的内容无法使用Win32 API检索。

可以很容易地以可视方式识别浮动菜单栏；但是，可能无法仅通过视觉检查来识别特殊类型的对话框。 您需要第三方应用程序(如Microsoft Spy++(Microsoft Visual C++开发环境的一部分)或其等效的WinID(可免费从 [https://www.dennisbabkin.com/php/download.php?what=WinID下载](https://www.dennisbabkin.com/php/download.php?what=WinID))来检查对话框以确定AppMon是否能够使用标准Win32 API与它交互。

如果WinID能够提取对话框内容，如文本、子窗口、窗口类ID等，那么AppMon也可以提取这些内容。

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
   <td><p>包括PDF设置、安全性设置和文件类型设置。 </p><p>文件类型设置将文件扩展名与相应的本机应用程序相关联。 文件类型设置还指定用于打印本机文件的本机应用程序设置。 </p></td>
   <td><p>要更改已支持的本机应用程序的设置，系统管理员可在管理控制台中设置“文件类型设置”。 </p><p>要添加对新本机文件格式的支持，必须手动编辑该文件。 (请参 <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">阅添加或修改对本机文件格式的支持</a>。) </p></td>
  </tr>
  <tr>
   <td><p>脚本 </p></td>
   <td><p>指定“生成PDF”服务与本机应用程序之间的交互。 此类交互操作通常将应用程序打印到Adobe PDF驱动程序。 </p><p>该脚本包含指示本机应用程序打开特定对话框以及向这些对话框中的字段和按钮提供特定响应的说明。 </p></td>
   <td><p>“生成PDF”服务包含所有支持的本机应用程序的脚本文件。 您可以使用XML编辑应用程序修改这些文件。</p><p>要添加对新本机应用程序的支持，必须创建新的脚本文件。 (请参 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">阅为本机应用程序创建或修改其他对话框XML文件</a>。) </p></td>
  </tr>
  <tr>
   <td><p>通用对话框说明 </p></td>
   <td><p>指定如何响应多个应用程序通用的对话框。 这些对话框由操作系统、辅助应用程序（如PDFMaker）和驱动程序生成。 </p><p>包含此信息的文件是appmon.global.en_US.xml。</p></td>
   <td><p>请勿修改此文件。 </p></td>
  </tr>
  <tr>
   <td><p>特定于应用程序的对话框说明</p></td>
   <td><p>指定如何响应特定于应用程序的对话框。 </p><p>包含此信息的文件是appmon。<i>“[appname]”“</i>.dialog。<i>“[locale]`</i>.xml（例如，appmon.word.en_US.xml）。</p></td>
   <td><p>请勿修改此文件。 </p><p>要为新的本机应用程序添加对话框说明，请参 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">阅为本机应用程序创建或修改其他对话框XML文件</a>。</p></td>
  </tr>
  <tr>
   <td><p>其他特定于应用程序的对话框说明 </p></td>
   <td><p>指定对特定于应用程序的对话框说明的覆盖和添加。 本节提供了此类信息的示例。 </p><p>包含此信息的文件是appmon。<i>“[appname]”</i>.addition。<i>“[区域设置]”</i>.xml。 一个示例是appmon.addition.en_US.xml。</p></td>
   <td><p>可以使用XML编辑应用程序创建和修改此类文件。 (请参 <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">阅为本机应用程序创建或修改其他对话框XML文件</a>。) </p><p><strong>重要说明</strong>:您必须为您的服务器将支持的每个本机应用程序创建其他特定于应用程序的对话框说明。 </p></td>
  </tr>
 </tbody>
</table>

### 关于脚本和对话框XML文件 {#about-the-script-and-dialog-xml-files}

脚本XML文件指示“生成PDF”服务在应用程序对话框中导航，就像用户在应用程序对话框中导航一样。 脚本XML文件还指示“生成PDF”服务通过执行按钮、选择或取消选择复选框或选择菜单项等操作来响应对话框。

相反，对话框XML文件只是对对话框做出响应，其操作类型与脚本XML文件中使用的操作相同。

#### 对话框和窗口元素术语 {#dialog-box-and-window-element-terminology}

本节和下一节对对话框及其包含的组件使用不同的术语，具体取决于所描述的透视图。 对话框组件是按钮、字段和组合框等项。

从用户的角度，本节和下一节介绍对话框及其组件时，会使用对 *话框*、 *button*、 *field*、 ** combobox等术语。

从对话框及其内部表示的角度来说，本部分和下一部分描述对话框及其组件时，将使 *用术语窗口元素* 。 窗口元素的内部表示是层次结构，其中每个窗口元素实例都由标签标识。 窗口元素实例还描述了其物理特性和行为。

从用户的角度看，对话框及其组件显示不同的行为，其中某些对话框元素在激活之前都是隐藏的。 从内部表示的角度来看，不存在此类行为问题。 例如，对话框的内部表示形式与其包含的组件的内部表示形式相似，但组件嵌套在对话框中除外。

本节介绍为AppMon提供说明的XML元素。 这些元素的名称如元 `dialog` 素和元 `window` 素。 此文档使用等宽字体来区分XML元素。 元 `dialog` 素标识出一个对话框，XML脚本文件可能会被有意或无意地显示。 元素 `window` 标识窗口元素（对话框或对话框的组件）。

#### 层次结构 {#hierarchy}

此图显示了脚本和对话框XML的层次结构。 脚本XML文件符合script.xsd模式，从XML意义上讲，该模式包括window.xsd。 同样，对话框XML文件符合dialogs.xsd模式，该模式还包括window.xsd。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

脚本和对话框XML的层次结构

#### 脚本XML文件 {#script-xml-files}

脚 *本XML文件指定了一系列步骤* ，这些步骤引导本机应用程序导航到某些窗口元素，然后为这些元素提供响应。 大多数响应是文本或按键，这些文本或按键与用户向相应对话框中的字段、组合框或按钮提供的输入相对应。

“生成PDF”服务对脚本XML文件的支持旨在引导本机应用程序打印本机文件。 但是，脚本XML文件可用于完成用户与本机应用程序对话框交互时可执行的任何任务。

脚本XML文件中的步骤按顺序执行，没有任何分支机会。 支持的唯一条件测试是超时／重试，如果某个步骤在特定时间段内和在特定数量的重试之后未成功完成，则会导致脚本终止。

除了顺序的步骤之外，步骤内的指令也按顺序执行。 您必须确保步骤和说明反映用户执行这些相同步骤的顺序。

脚本XML文件中的每个步骤都标识在成功执行该步骤的指令时应显示的窗口元素。 如果执行脚本步骤时出现意外对话框，“生成PDF”服务将按下一节所述搜索对话框XML文件。

#### 对话框XML文件 {#dialog-xml-files}

运行本机应用程序会显示不同的对话框，无论本机应用程序处于可见模式还是不可见模式，都会显示这些对话框。 对话框可以由操作系统或应用程序本身生成。 当本机应用程序在“生成PDF”服务的控制下运行时，系统和本机应用程序对话框显示在不可见窗口中。

对话框 *XML文件指定* “生成PDF”服务如何响应系统或本机应用程序对话框。 对话框XML文件允许“生成PDF”服务以便于转换过程的方式响应未提示的对话框。

当系统或本机应用程序显示的对话框不由当前正在执行的脚本XML文件处理时，“生成PDF”服务将按此顺序搜索对话框XML文件，当它找到匹配项时停止：

* appmon。`[appname]`.additional.`[locale]`.xml
* appmon。`[appname]`.`[locale]`.xml（请勿修改此文件。）
* appmon.global.`[locale]`.xml（请勿修改此文件。）

如果“生成PDF”服务找到对话框的匹配项，则会通过发送为对话框指定的按键或其他操作将其取消。 如果对话框的说明指定了中止消息，则“生成PDF”服务将终止当前正在执行的作业并生成错误消息。 将在脚本XML语法的元素中 `abortMessage` 指定此类中止消息。

如果“生成PDF”服务遇到一个对话框，而该对话框在以前列出的任何文件中都没有说明，则“生成PDF”服务会将该对话框的说明并入日志文件条目中。 当前执行的作业最终超时。 然后，您可以使用日志文件中的信息为本机应用程序在其他对话框XML文件中编写新说明。

### 添加或修改对本机文件格式的支持 {#adding-or-modifying-support-for-a-native-file-format}

本节介绍支持其他本机文件格式或修改对已支持的本机文件格式的支持所必须执行的任务。

在添加或修改支持之前，您必须完成以下任务。

#### 选择用于识别窗口元素的工具 {#choosing-a-tool-for-identifying-window-elements}

对话框和脚本XML文件要求您标识对话框或脚本元素所响应的窗口元素（对话框、字段或其他对话框组件）。 例如，在脚本调用本机应用程序的菜单后，该脚本必须标识该菜单上要应用按键或动作的窗口元素。

您可以通过对话框在标题栏中显示的标题轻松标识对话框。 但是，必须使用Microsoft Spy++等工具来识别低级窗口元素。 下层窗口元素可以通过各种属性来识别，这些属性并不明显。 此外，每个本机应用程序可以不同地识别其窗口元素。 因此，有多种方法可以识别窗口元素。 以下是考虑窗口要素标识的建议顺序：

1. 题注本身（如果它是唯一的）
1. 控制ID，对于给定对话框，它可能唯一，也可能不唯一
1. 类名，可能唯一，也可能不唯一

这三个属性的任何一个或组合都可以用于标识窗口。

如果属性无法识别题注，则可以通过使用窗口元素相对于其父元素的索引来识别窗口元素。 索引 *指定窗口元素* 相对于其同级窗口元素的位置。 通常，索引是识别组合框的唯一方法。

请注意以下问题：

* Microsoft Spy++通过使用&amp;符号(&amp;)来标识字幕的热键来显示字幕。 例如，Spy++将一个“打印”对话框的标题显示为， `Pri&nt`表示热键为 *n*。 脚本和对话框XML文件中的字幕标题必须忽略&amp;符号。
* 某些字幕包括换行符。 “生成PDF”服务无法识别换行符。 如果题注包含换行符，则包含足够的题注以将其与其他菜单项区分开，然后对省略的部分使用常规表达式。 例如( `^Long caption title$`)。]. (请参阅 [在题注属性中使用常规表达式](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)。)
* 对保留的XML字符使用字符实体（也称为转义序列）。 例如，对于 `&` “和”, `<` 对于“ `>` 小于”和“大于”符号， `&apos;` 对于撇号和 `&quot;` 引号。

如果您计划处理对话框或脚本XML文件，则应安装应用程序Microsoft Spy++。

#### 取消对话框和脚本文件的打包 {#unpackaging-the-dialog-and-script-files}

对话框和脚本文件位于appmondata.jar文件中。 在可以修改其中任何文件或添加新脚本或对话框文件之前，必须先取消打包此JAR文件。 例如，假设您要添加对EditPlus应用程序的支持。 可以创建两个XML文件，名为appmon.editplus.script.en_US.xml和appmon.editplus.script.addition.en_US.xml。 必须将这些XML脚本添加到adobe-appmondata.jar文件的两个位置，如下所述：

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon。 adobe-livecycle-native-jboss-x86_win32.ear文件位于的导出文件夹中 `[AEM forms install directory]\configurationManager`。 （如果AEM Forms部署在另一台J2EE应用程序服务器上，请将adobe-livecycle-native-jboss-x86_win32.ear文件替换为与您的J2EE应用程序服务器对应的EAR文件。）
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jar文件位于adobe-generatepdf-dsc.jar文件中）。 adobe-generatepdf-dsc.jar文件在文件夹中 `[AEM forms install directory]\deploy` 。

将这些XML文件添加到adobe-appmondata.jar文件后，必须重新部署GeneratePDF组件。 要将对话框和脚本XML文件添加到adobe-appmondata.jar文件，请执行以下任务:

1. 使用WinZip或WinRAR等工具，打开adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib >adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar文件。
1. 将对话框和脚本XML文件添加到appmondata.jar文件中，或修改此文件中的现有XML文件。 (请参 [阅为本机应用程序创建或修改脚本XML文](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)件和 [为本机应用程序创建或修改其他对话框XML文件](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)。)
1. 使用WinZip或WinRAR等工具，打开adobe-generatepdf-dsc.jar > adobe-appmondata.jar。
1. 将对话框和脚本XML文件添加到appmondata.jar文件中，或修改此文件中的现有XML文件。 (请参 [阅为本机应用程序创建或修改脚本XML文](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)件和 [为本机应用程序创建或修改其他对话框XML文件](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)。)在将XML文件添加到adobe-appmondata.jar文件后，将新的adobe-appmondata.jar文件放入adobe-generatepdf-dsc.jar文件中。
1. 如果添加了对其他本机文件格式的支持，请创建一个系统环境变量，它提供应用程序的路径(请参阅创建环境变量以查找本机应用程序 [](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application))。

**重新部署GeneratePDF组件**

1. 登录到Workbench。
1. 选择 **窗口** >显 **示视图** > **组件**。 此操作会将组件视图添加到工作台。
1. 右键单击“生成PDF”组件，然后选择“停 **止组件”**。
1. 当组件停止时，右键单击并选择“卸载组件”将其删除。
1. 右键单击“组件 **”图标** ，然后选择 **安装组件**。
1. 浏览并选择修改后的adobe-generatepdf-dsc.jar文件，然后单击“打开”。 请注意，“生成PDF”组件旁边会显示一个红方。
1. 展开GeneratePDF组件，选择“服务描述符”，然后右键单击“生成PDF服务”，然后选择“激活服务”。
1. 在出现的配置对话框中，输入适用的配置值。 如果将这些值留空，则使用默认配置值。
1. 右键单击“生成PDF”，然后选择“开始组件”。
1. 展开活动服务。 如果服务名称正在运行，则该服务名称旁边将显示绿色箭头。 否则，服务处于停止状态。
1. 如果服务处于停止状态，请右键单击服务名称，然后选择“开始服务”。

### 为本机应用程序创建或修改脚本XML文件 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

如果要将文件定向到新的本机应用程序，则必须为该应用程序创建一个脚本XML文件。 如果要修改生成PDF服务与已支持的本机应用程序交互的方式，则必须修改该应用程序的脚本。

该脚本包含在本机应用程序的窗口元素之间导航的说明，这些说明为这些元素提供特定的响应。 包含此信息的文件是 `appmon.`[appname]&quot; `.script.`[locale]`.xml`。 例如appmon.notepad.script.en_US.xml。

#### 确定脚本必须执行的步骤 {#identifying-steps-the-script-must-execute}

使用本机应用程序确定必须导航的窗口元素以及打印文档时必须执行的每个响应。 注意任何响应产生的对话框。 这些步骤将类似于以下步骤：

1. 选择“文件”>“打开”。
1. 指定路径，然后单击“打开”。
1. 在菜单栏上选择“文件”>“打印”。
1. 指定打印机所需的属性。
1. 选择“打印”，然后等待“另存为”对话框出现。 “生成PDF”服务需要“另存为”对话框来指定PDF文件的目标位置。

#### 标识在题注属性中指定的对话框 {#identifying-the-dialogs-specified-in-caption-attributes}

使用Microsoft Spy++获取本机应用程序中窗口元素属性的标识。 您必须具有这些身份才能编写脚本。

#### 在题注属性中使用常规表达式 {#using-regular-expressions-in-caption-attributes}

您可以在题注规范中使用常规表达式。 “生成PDF”服务使用 `java.util.regex.Matcher` 类支持常规表达式。 该实用程序支持中所述的常规表达式 `java.util.regex.Pattern`。 (请访问Java网站： [https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html)。)

**在记事本横幅中，包含前缀于记事本的文件名的常规表达式**

```as3
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**常规表达式区分打印和打印设置**

```as3
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### 对窗口和窗口排序列表元素 {#ordering-the-window-and-windowlist-elements}

您必须按如 `window` 下方式 `windowList` 订购和元素：

* 当多个 `window` 元素在某个或元素中显示为子元素时， `windowList` 请按降序顺序排列这些元素，其名称的长 `dialog``window``caption` 度表示该顺序中的位置。
* 当元素 `windowList` 中出现多个元素时， `window` 请按降序排列这些元素，第一个元素的属 `windowList` 性的长度表示该 `caption``indexes/`顺序中的位置。

**将窗口元素排序到对话框文件中**

```as3
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

```as3
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

如果为以前不支持的本机应用程序创建脚本，则还必须为该应用程序创建额外的对话框XML文件。 AppMon使用的每个本机应用程序必须只有一个额外的对话框XML文件。 即使不需要主动提供的对话框，也需要额外的对话框XML文件。 附加的对话框必须至少有一个元 `window` 素，即使该元素只是 `window` 一个占位符。

>[!NOTE]
>
>在此上下文中，术语“附加”指 `appmon.[applicationname].addition.[locale]`.xml”文件的内容。 这样的文件会指定对话框XML文件的覆盖和添加。

您还可以出于以下目的为本机应用程序修改额外的对话框XML文件：

* 用不同的响应覆盖应用程序的对话框XML文件
* 向该应用程序的对话框XML文件中未解决的对话框添加响应

标识其他dialogXML文件的文件名为 `appmon.[appname].addition.[locale].xml`。 例如appmon.excel.addition.en_US.xml。

附加对话框XML文件的名称必须使用格式 `appmon.[applicationname].addition.[locale].xml`，其中 *applicationname* 必须与XML配置文件和脚本中使用的应用程序名称完全匹配。

>[!NOTE]
>
>native2pdfconfig.xml配置文件中指定的所有通用应用程序都没有主对话框XML文件。 添加或 [修改对本机文件格式的支持部分介绍了](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) 此类规范。

您必须对元素 `windowList` 中显示为子元素的元素进行 `window` 排序。 (请参 [阅对窗口和窗口列表元素进行排序](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)。)

### 修改常规对话框XML文件 {#modifying-the-general-dialog-xml-file}

您可以修改常规对话框XML文件以响应由系统生成的对话框或响应多个应用程序通用的对话框。

#### 在XML配置文件中添加文件类型条目 {#adding-a-filetype-entry-in-the-xml-configuration-file}

此过程介绍如何更新生成PDF服务配置文件以将文件类型与本机应用程序关联。 要更新此配置文件，必须使用管理控制台将配置数据导出到文件。 配置数据的默认文件名为native2pdfconfig.xml。

**更新“生成PDF”服务配置文件**

1. 选择“ **主页** ”>“服务 **”** >“ **Adobe PDF Generator** ”>“配置文件”, ********&#x200B;然后选择“导出配置”。
1. 根据 `filetype-settings` 需要修改native2pdfconfig.xml文件中的元素。
1. 选择“ **主页** ”>“服务 **”** >“ **Adobe PDF Generator** ”>“配置文件”,********&#x200B;然后选择“导入配置”Configuration Configuration Select。 配置数据将导入到“生成PDF”服务中，替换以前的设置。

>[!NOTE]
>
>应用程序的名称被指定为元素属 `GenericApp` 性的 `name` 值。 此值必须与为该应用程序开发的脚本中指定的相应名称完全匹配。 同样，元 `GenericApp` 素的属性 `displayName` 应与相应脚本的窗口题注完全 `expectedWindow` 匹配。 在解析出现在或属性中的任何常规表达式后，将评估此 `displayName` 等价 `caption` 关系。

在此示例中，修改了随“生成PDF”服务提供的默认配置数据，以指定应使用记事本（而非Microsoft Word）处理文件扩展名为。txt的文件。 在此修改之前，将Microsoft Word指定为应处理此类文件的本机应用程序。

**将文本文件定向到记事本的修改(native2pdfconfig.xml)**

```as3
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

创建一个环境变量，它指定本机应用程序可执行文件的位置。 变量必须使用格式 `[applicationname]_PATH`，其中 *applicationname* 必须与XML配置文件和脚本中使用的应用程序名称完全匹配，并且路径包含以多次引号表示的可执行文件的路径。 这样的环境变量的示例是 `Photoshop_PATH`。

创建新的环境变量后，必须重新启动部署了“生成PDF”服务的服务器。

**在Windows XP环境中创建系统变量**

1. 选择“ **控制面板”>“系统**”。
1. 在“系统属性”对话框中，单击“高 **级** ”选项卡，然后单击“ **环境变量”**。
1. 在“环境变量”对话框的“系统变量”下，单击“新 **建”**。
1. 在“新建系统变量”对话框的“变 **量名称** ”框中，键入使用格式的名称 `[applicationname]_PATH`。
1. 在“变 **量值** ”(Variable value)框中，键入应用程序可执行文件的完整路径和文件名，然后单击“确 **定”(OK)**。 例如，类型： `c:\windows\Notepad.exe`
1. 在“环境变量”对话框中，单击“确 **定”**。

**从命令行创建系统变量**

1. 在命令行窗口中，使用以下格式键入变量定义：

   ```as3
            [applicationname]_PATH=[Full path name]
   ```

   例如，类型： `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 开始新的命令行提示，使系统变量生效。

#### XML文件 {#xml-files}

AEM Forms包含示例XML文件，这些文件导致“生成PDF”服务使用记事本处理文件扩展名为。txt的任何文件。 此代码包含在本节中。 此外，您还必须进行本条所述的其他修改。

#### 其他对话框XML文件 {#additional-dialog-xml-file}

此示例包含记事本应用程序的其他对话框。 除了“生成PDF”服务指定的对话框之外，还可以添加这些对话框。

**记事本对话框(appmon.notepad.addition.cn_US.xml)**

```as3
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### 脚本XML文件 {#script-xml-file}

此示例指定“生成PDF”服务如何与记事本交互，以便使用Adobe PDF打印机打印文件。

**记事本脚本XML文件(appmon.notepad.script.en_US.xml)**

```as3
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

