---
title: 将PDF转换为Postscript和图像文件
seo-title: Converting PDF to Postscript andImage Files
description: 使用“转换PDF”服务，通过Java API和Web服务API，将PDF文档转换为PostScript和多种图像格式(JPEG、JPEG2000、PNG和TIFF)。
seo-description: Use the Convert PDF service to convert PDF documents to PostScript and to a number of image formats (JPEG, JPEG 2000, PNG, and TIFF) using the Java API and Web Service API.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2809'
ht-degree: 0%

---

# 将PDF转换为Postscript和图像文件 {#converting-pdf-to-postscript-andimage-files}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

**关于转换PDF服务**

“转换PDF”服务将PDF文档转换为PostScript和多种图像格式(JPEG、JPEG2000、PNG和TIFF)。 将PDF文档转换为PostScript对于在任何PostScript打印机上进行基于服务器的无人值守打印非常有用。 当在不支持PDF文档的内容管理系统中归档文档时，将TIFF文档转换为多页PDF文件是非常实用的。

您可以使用转换PDF服务完成以下任务：

* 将PDF文档转换为PostScript。
* 将PDF文档转换为图像格式。

>[!NOTE]
>
>有关转换PDF服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 将PDF文档转换为PostScript {#converting-pdf-documents-to-postscript}

本主题介绍如何使用转换PDF服务API（Java和Web服务）以编程方式将PDF文档转换为PostScript文件。 转换为PostScript文件的PDF文档必须是非交互式PDF文档。 也就是说，如果尝试将交互式PDF文档转换为PostScript文件，则会引发异常。

>[!NOTE]
>
>有关转换PDF服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要将PDF文档转换为PostScript文件，请执行以下步骤：

1. 包括项目文件。
1. 创建转换PDF服务客户端。
1. 引用PDF文档以转换为PostScript文件。
1. 设置转化运行时选项。
1. 将PDF文档转换为PostScript文件。
1. 保存PostScript文件。

**包含项目文件**

将必需的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建转换PDF客户端**

在以编程方式执行转换PDF服务操作之前，必须创建转换PDF服务客户端。 如果您使用的是Java API，请创建 `ConvertPdfServiceClient` 对象。 如果您使用的是Web服务API，请创建 `ConvertPDFServiceService` 对象。

本节使用AEM Forms中引入的Web服务功能。 要访问新功能，您必须使用 `lc_version` 属性。 (请参阅 [使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**引用PDF文档以转换为PostScript文件**

引用要转换为PostScript文件的PDF文档。 如本主题前面所述，PDF文档必须是非交互式PDF文档。 如果尝试将交互式PDF文档转换为PostScript文件，则会引发异常。

**设置转化运行时选项**

在将PDF文档转换为PostScript文件时，您可以定义运行时选项，以指定所创建的PostScript类型。 例如，您可以定义第3级PostScript文件。

通常，生成的PostScript文件将反映输入PDF文档的大小。 如果您选择 `ShrinkToFit` 选项（该选项可缩小PostScript文件的输出以适合页面），则不会看到输入PDF文档与生成的PostScript文件之间的差异。 的 `ShrinkToFit` 仅当您选择在比输入PDF文档小的页面大小上打印时，选项才生效。 要选择较小的页面大小，请定义 `PageSize` 选项。 此外，建议您将 `RotateAndCenter` 选项 `true` 以获取正确的PostScript输出。

同样，如果您选择 `ExpandToFit` 选项（该选项将扩展PostScript文件的输出以适合页面大小），只有在选择打印的页面大于输入PDF文档时，该选项才会生效。 要选择更大的页面大小，请定义 `PageSize` 选项。 此外，建议您将 `RotateAndCenter` 选项 `true` 以获取正确的PostScript输出。

>[!NOTE]
>
>有关可设置的运行时值的信息，请参阅 `ToPSOptionsSpec` 类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**将PDF文档转换为PostScript文件**

在创建服务客户端并设置运行时选项后，可以调用PostScript转换操作。 此操作需要有关要转换的文档的信息，包括目标文档的首选PostScript级别。

**保存PostScript文件**

将PDF文档转换为PostScript后，可以将输出另存为PostScript文件。

**另请参阅**

[使用Java API将PDF文档转换为PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用Web服务API将PDF文档转换为PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[转换PDF服务API快速入门](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API将PDF文档转换为PS {#convert-a-pdf-document-to-ps-using-the-java-api}

使用转换PDF服务API(Java)将PDF文档转换为PostScript:

1. 包括项目文件。

   将客户端JAR文件（如adobe-convertpdf-client.jar）包含在您Java项目的类路径中。

1. 创建转换PDF客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `ConvertPdfServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用PDF文档以转换为PostScript文件。

   * 创建 `java.io.FileInputStream` 对象，并传递一个字符串值，该字符串值指定要转换的PDF文档的位置。
   * 创建 `com.adobe.idp.Document` 用于存储PDF文档的对象 `com.adobe.idp.Document` 构造函数。 传递 `java.io.FileInputStream` 包含PDF文档的对象。

1. 设置转化运行时选项。

   * 创建 `ToPSOptionsSpec` 对象。
   * 通过调用属于 `ToPSOptionsSpec` 对象。 例如，要定义所创建的PostScript级别，请调用 `ToPSOptionsSpec` 对象 `setPsLevel` 方法和通过 `PSLevel` 指定PostScript级别的枚举值。 有关可设置的所有运行时值的信息，请参阅 `ToPSOptionsSpec` 类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 将PDF文档转换为PostScript文件。

   调用 `ConvertPdfServiceClient`对象 `toPS2` 方法并传递以下值：

   * A `com.adobe.idp.Document` 表示要转换为PostScript文件的PDF文档的对象。
   * A `ToPSOptionsSpec` 指定PostScript运行时选项的对象。

   的 `toPS2` 方法返回 `Document` 包含新PostScript文档的对象。

1. 保存PostScript文件。

   * 创建 `java.io.File` 对象，并确保文件扩展名为.ps。
   * 调用 `Document` 对象 `copyToFile` 复制内容的方法 `Document` 对象到文件(确保使用 `Document` 由返回的对象 `toPS2` 方法)。

**另请参阅**

[步骤摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API将PDF文档转换为PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PDF文档转换为PS {#convert-a-pdf-document-to-ps-using-the-web-service-api}

使用转换PDF服务API（Web服务）将PDF文档转换为PostScript:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建转换PDF客户端。

   * 创建 `ConvertPdfServiceClient` 对象。
   * 创建 `ConvertPdfServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) 您无需使用 `lc_version` 属性。 但是，请指定 `?blob=mtom`.
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `ConvertPdfServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用PDF文档以转换为PostScript文件。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储转换为PostScript文件的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要转换的PDF文档的文件位置以及在中打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递字节数组、起始位置及流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 设置转化运行时选项。

   * 创建 `ToPSOptionsSpec` 对象。
   * 通过为 `ToPSOptionsSpec` 对象的数据成员。 例如，要定义所创建的PostScript级别，请分配 `PSLevel` 枚举值 `ToPSOptionsSpec` 对象 `psLevel` 数据成员。

1. 将PDF文档转换为PostScript文件。

   调用 `GeneratePDFServiceService` 对象 `toPS2` 方法并传递以下值：

   * A `BLOB` 表示要转换为PostScript文件的PDF文档的对象
   * A `ToPSOptionsSpec` 指定运行时选项的对象

   转换完成后，通过访问代表PostScript文档的二进制数据 `BLOB` 对象 `MTOM` 属性。 这会返回一个字节数组，您可以将其写出到PostScript文件。

1. 保存PostScript文件。

   * 创建 `System.IO.FileStream` 对象。 传递表示PS文件位置的字符串值。
   * 创建用于存储 `BLOB` 由返回的对象 `encryptPDFUsingPassword` 方法。 通过获取 `BLOB` 对象 `MTOM` 字段。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将PDF文档转换为图像格式 {#converting-pdf-documents-to-image-formats}

您可以使用“转换PDF”服务以编程方式将PDF文档转换为图像格式，包括JPEG、JPEG2000、TIFF和PNG。 通过将PDF文档转换为图像文件，可以将PDF文档用作图像文件。 例如，您可以将映像放入企业内容管理系统中进行存储。

在将PDF文档转换为图像时，“转换PDF”服务会为文档中的每个页面创建单独的图像。 即，如果文档有20页，则转换PDF服务将创建20个图像文件。 在将PDF文档转换为图像格式时，您可以为PDF文档中的每个页面创建单个图像，或为整个PDF文档创建单个图像文件。

>[!NOTE]
>
>有关转换PDF服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-1}

要将PDF文档转换为任何受支持的类型，请执行以下步骤：

1. 包括项目文件。
1. 创建转换PDF服务客户端。
1. 检索要转换的PDF文档。
1. 设置运行时选项。
1. 将PDF转换为图像。
1. 从集合中检索图像文件。

**包含项目文件**

将必需的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建转换PDF客户端**

在以编程方式执行转换PDF服务操作之前，必须创建转换PDF服务客户端。 如果您使用的是Java API，请创建 `ConvertPdfServiceClient` 对象。 如果您使用的是Web服务API，请创建 `ConvertPDFServiceService` 对象。

**检索要转换的PDF文档**

必须检索PDF文档才能转换为图像。 无法将交互式PDF文档转换为图像。 如果尝试执行此操作，则会引发异常。 要将交互式PDF文档转换为图像文件，必须先拼合PDF文档，然后再转换。 (请参阅 [拼合PDF文档](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**设置运行时选项**

您必须设置运行时选项，如图像格式和分辨率值。 有关运行时值的信息，请参阅 `ToImageOptionsSpec` 类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**将PDF转换为图像**

在创建服务客户端并设置运行时选项后，可以将PDF文档转换为图像。 将返回包含图像的集合对象。

**从集合中检索图像文件**

您可以从转换PDF服务返回的集合对象中检索图像文件。 集合中的每个元素都是 `com.adobe.idp.Document` 实例(或 `BLOB` 实例（如果您使用的是web服务），可将其另存为图像文件，如JPG文件。

图像文件的格式取决于 `ImageConvertFormat` 运行时选项。 即，如果您将 `ImageConvertFormat` 运行时选项 `ImageConvertFormat.JPEG`，您可以将图像文件另存为JPG文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[转换PDF服务API快速入门](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API将PDF文档转换为图像文件 {#convert-a-pdf-document-to-image-files-using-the-java-api}

使用转换PDF服务API(Java)将PDF文档转换为图像格式：

1. 包括项目文件。

   将客户端JAR文件（如adobe-convertpdf-client.jar）包含在您Java项目的类路径中。

1. 创建转换PDF客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `ConvertPdfServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 检索要转换的PDF文档。

   * 创建 `java.io.FileInputStream` 表示要转换的PDF文档的对象，方法是使用其构造函数并传递指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置运行时选项。

   * 创建 `ToImageOptionsSpec` 对象。
   * 根据需要调用属于此对象的方法。 例如，通过调用 `setImageConvertFormat` 方法和通过 `ImageConvertFormat` 指定格式类型的枚举值。

   >[!NOTE]
   >
   >设置 `ImageConvertFormat` 枚举值是必选项。

1. 将PDF转换为图像。

   调用 `ConvertPdfServiceClient` 对象 `toImage2` 方法并传递以下值：

   * A `com.adobe.idp.Document` 表示要转换的PDF文件的对象。
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` 包含有关目标图像格式的各种首选项的对象。

   的 `toImage2` 方法返回 `java.util.List` 包含图像的对象。 集合中的每个元素都是 `com.adobe.idp.Document` 实例。

1. 从集合中检索图像文件。

   循环访问 `java.util.List` 用于确定图像是否存在的对象。 每个元素都是 `com.adobe.idp.Document` 实例。 通过调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法和通过 `java.io.File` 对象。

**另请参阅**

[快速入门（SOAP模式）：使用Java API将PDF文档转换为JPEG文件](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用Web服务API将PDF文档转换为图像文件 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

使用转换PDF服务API（Web服务）将PDF文档转换为图像格式：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建转换PDF客户端。

   * 创建 `ConvertPdfServiceClient` 对象。
   * 创建 `ConvertPdfServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) 您无需使用 `lc_version` 属性。 但是，请指定 `?blob=mtom`.
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `ConvertPdfServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 检索要转换的PDF文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储PDF表单。
   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，以指定PDF表单的位置以及在其中打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法。 传递字节数组、开始位置和流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 设置运行时选项。

   * 创建 `ToImageOptionsSpec` 对象。
   * 根据需要调用属于此对象的方法。 例如，通过调用 `setImageConvertFormat` 方法和通过 `ImageConvertFormat` 指定格式类型的枚举值。

   >[!NOTE]
   >
   >设置 `ImageConvertFormat` 枚举值是必选项。

1. 将PDF转换为图像。

   调用 `ConvertPDFServiceService` 对象 `toImage2` 方法并传递以下值：

   * A `BLOB` 表示要转换的文件的对象
   * A `ToImageOptionsSpec` 包含有关目标图像格式的各种首选项的对象

   的 `toImage2` 方法返回 `MyArrayOfBLOB` 包含新创建图像文件的对象。

1. 从集合中检索图像文件。

   * 确定 `MyArrayOfBLOB` 对象，方法是获取 `Count` 字段。 每个元素都是 `BLOB` 包含图像的对象。
   * 循环访问 `MyArrayOfBLOB` 对象，并保存每个图像文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
