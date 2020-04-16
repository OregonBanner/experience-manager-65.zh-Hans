---
title: 将PDF转换为Postscript和图像文件
seo-title: 将PDF转换为Postscript和图像文件
description: 'null'
seo-description: 'null'
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 将PDF转换为Postscript和图像文件 {#converting-pdf-to-postscript-andimage-files}

**关于转换PDF服务**

“转换PDF”服务将PDF文档转换为PostScript和多种图像格式（JPEG、JPEG 2000、PNG和TIFF）。 将PDF文档转换为PostScript对于在任何PostScript打印机上进行基于服务器的无人值守打印都很有用。 将PDF文档转换为多页TIFF文件在不支持PDF文档的内容管理系统中归档文档时非常实用。

您可以使用“转换PDF”服务完成以下任务:

* 将PDF文档转换为PostScript。
* 将PDF文档转换为图像格式。

>[!NOTE]
>
>有关转换PDF服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将PDF文档转换为PostScript {#converting-pdf-documents-to-postscript}

本主题介绍如何使用转换PDF服务API（Java和Web服务）以编程方式将PDF文档转换为PostScript文件。 转换为PostScript文件的PDF文档必须是非交互式PDF文档。 即，如果尝试将交互式PDF文档转换为PostScript文件，则会引发异常。

>[!NOTE]
>
>有关转换PDF服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要将PDF文档转换为PostScript文件，请执行以下步骤：

1. 包括项目文件。
1. 创建“转换PDF”服务客户端。
1. 引用PDF文档以转换为PostScript文件。
1. 设置转换运行时选项。
1. 将PDF文档转换为PostScript文件。
1. 保存PostScript文件。

**包括项目文件**

将必要的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建转换PDF客户端**

在以编程方式执行“转换PDF”服务操作之前，必须创建“转换PDF”服务客户端。 如果您使用Java API，请创建一个对 `ConvertPdfServiceClient` 象。 如果您使用Web服务API，请创建一个对 `ConvertPDFServiceService` 象。

本节使用AEM Forms中引入的Web服务功能。 要访问新功能，您必须使用属性构建代理对 `lc_version` 象。 (请参阅使用Web服务调用AEM表单中的“ [使用Web服务访问新功能](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)”。)

**引用PDF文档以转换为PostScript文件**

引用要转换为PostScript文件的PDF文档。 如本主题前面所述，PDF文档必须是非交互式PDF文档。 如果尝试将交互式PDF文档转换为PostScript文件，则会引发异常。

**设置转换运行时选项**

将PDF文档转换为PostScript文件时，可以定义运行时选项，这些选项指定所创建的PostScript类型。 例如，可以定义级别3的PostScript文件。

通常，生成的PostScript文件将反映输入PDF文档的大小。 如果选择 `ShrinkToFit` 选项（该选项会缩小PostScript文件的输出以适合页面），您将看不到输入PDF文档与生成的PostScript文件之间的区别。 仅当 `ShrinkToFit` 您选择以比输入PDF文档小的页面大小打印时，此选项才生效。 要选择较小的页面大小，请定义选 `PageSize` 项。 此外，建议您设置选项以 `RotateAndCenter` 获得 `true` 正确的PostScript输出。

同样，如果您选择 `ExpandToFit` 选项（该选项会扩展PostScript文件的输出以适合页面），则只有在选择打印的页面大于输入的PDF文档时，该选项才生效。 要选择较大的页面大小，请定义选 `PageSize` 项。 此外，建议您设置选项以 `RotateAndCenter` 获得 `true` 正确的PostScript输出。

>[!NOTE]
>
>有关可以设置的运行时值的信息，请参阅 `ToPSOptionsSpec` AEM Forms API Reference中的类引用 [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**将PDF文档转换为PostScript文件**

在创建服务客户端并设置运行时选项后，可以调用PostScript转换操作。 此操作需要有关要转换的文档的信息，包括目标文档的首选PostScript级别。

**保存PostScript文件**

将PDF文档转换为PostScript后，可将输出另存为PostScript文件。

**另请参阅**

[使用Java API将PDF文档转换为PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用Web服务API将PDF文档转换为PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[转换PDF Service API快速开始](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API将PDF文档转换为PS {#convert-a-pdf-document-to-ps-using-the-java-api}

使用“转换PDF服务API”(Java)将PDF文档转换为PostScript:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-convertpdf-client.jar。

1. 创建“转换PDF”客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `ConvertPdfServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 引用PDF文档以转换为PostScript文件。

   * 使用对 `java.io.FileInputStream` 象的构造函数创建一个对象，并传递一个指定要转换的PDF文档位置的字符串值。
   * 使用构 `com.adobe.idp.Document` 造函数创建存储PDF文档的对 `com.adobe.idp.Document` 象。 传递 `java.io.FileInputStream` 包含PDF文档的对象。

1. 设置转换运行时选项。

   * 通过调 `ToPSOptionsSpec` 用对象的构造函数创建对象。
   * 通过调用属于对象的相应方法来设置运行时选 `ToPSOptionsSpec` 项。 例如，要定义所创建的PostScript级别，请调 `ToPSOptionsSpec` 用对象的方 `setPsLevel` 法并传递指定PostScript `PSLevel` 级别的明细列表值。 有关可设置的所有运行时值的信息，请参阅 `ToPSOptionsSpec` AEM Forms API参考中的类引用 [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 将PDF文档转换为PostScript文件。

   调用 `ConvertPdfServiceClient`对象的方 `toPS2` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` 要转换为PostScript文件的PDF文档的对象。
   * 指定 `ToPSOptionsSpec` PostScript运行时选项的对象。
   该方 `toPS2` 法返回一 `Document` 个包含新PostScript文档的对象。

1. 保存PostScript文件。

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。ps。
   * 调用对 `Document` 象的方 `copyToFile` 法，将对象的内容复制到文件中(确保使用由 `Document` 该方法返回的对 `Document``toPS2` 象)。

**另请参阅**

[步骤摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API将PDF文档转换为PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PDF文档转换为PS {#convert-a-pdf-document-to-ps-using-the-web-service-api}

使用“转换PDF服务API（Web服务）”将PDF文档转换为PostScript:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建“转换PDF”客户端。

   * 使用对 `ConvertPdfServiceClient` 象的默认构造函数创建对象。
   * 使用构 `ConvertPdfServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.)您无需使用该属 `lc_version` 性。 但是，请指 `?blob=mtom`定。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `ConvertPdfServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF文档以转换为PostScript文件。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储转换为PostScript文件的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示要转换的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并将字节数组、开始位 `System.IO.FileStream` 置和流长度传递 `Read` 给读取，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 设置转换运行时选项。

   * 通过调 `ToPSOptionsSpec` 用对象的构造函数创建对象。
   * 通过为对象的数据成员分配一个值来 `ToPSOptionsSpec` 设置运行时选项。 例如，要定义所创建的PostScript级别，请为对象的 `PSLevel` 数据成员分 `ToPSOptionsSpec` 配一个 `psLevel` 明细列表值。

1. 将PDF文档转换为PostScript文件。

   调用对 `GeneratePDFServiceService` 象的方 `toPS2` 法并传递以下值：

   * 表示 `BLOB` 要转换为PostScript文件的PDF文档的对象
   * 指定 `ToPSOptionsSpec` 运行时选项的对象
   转换完成后，通过访问PostScript文档的对象属性提取表示PostScript `BLOB` 的二进制数 `MTOM` 据。 这会返回一个字节数组，您可以将其写出到PostScript文件。

1. 保存PostScript文件。

   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递表示PS文件的文件位置的字符串值。
   * 创建一个字节数组，它存储由方法返 `BLOB` 回的对象的数据内 `encryptPDFUsingPassword` 容。 通过获取对象字段的值来填 `BLOB` 充字节数 `MTOM` 组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字节数组的 `System.IO.BinaryWriter` 内容写 `Write` 入PostScript文件。

**另请参阅**

[步骤摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将PDF文档转换为图像格式 {#converting-pdf-documents-to-image-formats}

您可以使用“转换PDF”服务以编程方式将PDF文档转换为图像格式，包括JPEG、JPEG 2000、TIFF和PNG。 通过将PDF文档转换为图像文件，您可以将PDF文档用作图像文件。 例如，您可以将图像放在企业内容管理系统中进行存储。

将PDF文档转换为图像时，“转换PDF”服务会为文档中的每页创建单独的图像。 即，如果文档有20页，“转换PDF”服务将创建20个图像文件。 将PDF文档转换为图像格式时，您可以为PDF文档中的每页创建单独的图像，或为整个PDF文档创建单个图像文件。

>[!NOTE]
>
>有关转换PDF服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要将PDF文档转换为任何支持的类型，请执行以下步骤：

1. 包括项目文件。
1. 创建“转换PDF”服务客户端。
1. 检索要转换的PDF文档。
1. 设置运行时选项。
1. 将PDF转换为图像。
1. 从集合中检索图像文件。

**包括项目文件**

将必要的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建转换PDF客户端**

在以编程方式执行“转换PDF”服务操作之前，必须创建“转换PDF”服务客户端。 如果您使用Java API，请创建一个对 `ConvertPdfServiceClient` 象。 如果您使用Web服务API，请创建一个对 `ConvertPDFServiceService` 象。

**检索要转换的PDF文档**

您必须检索PDF文档才能转换为图像。 无法将交互式PDF文档转换为图像。 如果尝试这样做，则会引发异常。 要将交互式PDF文档转换为图像文件，您必须先拼合PDF文档，然后再转换。 (请参阅 [拼合PDF文档](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)。)

**设置运行时选项**

必须设置运行时选项，如图像格式和分辨率值。 有关运行时值的信息，请参阅 `ToImageOptionsSpec` AEM Forms API Reference中的类引用 [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**将PDF转换为图像**

在创建服务客户端并设置运行时选项后，您可以将PDF文档转换为图像。 将返回包含图像的集合对象。

**从集合中检索图像文件**

您可以从转换PDF服务返回的集合对象中检索图像文件。 集合中的每个元素都是 `com.adobe.idp.Document` 一个实例(或者，如果您使用Web服务， `BLOB` 则是一个实例)，您可以将其另存为图像文件，如JPG文件。

图像文件的格式取决于运 `ImageConvertFormat` 行时选项。 即，如果将运行时选 `ImageConvertFormat` 项设置为，则可 `ImageConvertFormat.JPEG`将图像文件另存为JPG文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[转换PDF Service API快速开始](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API将PDF文档转换为图像文件 {#convert-a-pdf-document-to-image-files-using-the-java-api}

使用“转换PDF服务API”(Java)将PDF文档转换为图像格式：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-convertpdf-client.jar。

1. 创建“转换PDF”客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `ConvertPdfServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 检索要转换的PDF文档。

   * 创建一 `java.io.FileInputStream` 个对象，它表示要转换的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 设置运行时选项。

   * 使用对 `ToImageOptionsSpec` 象的构造函数创建对象。
   * 根据需要调用属于此对象的方法。 例如，通过调用方法并传递指定格 `setImageConvertFormat` 式类型的enum `ImageConvertFormat` 值来设置图像类型。
   >[!NOTE]
   >
   >必须 `ImageConvertFormat` 设置明细列表值。

1. 将PDF转换为图像。

   调用对 `ConvertPdfServiceClient` 象的方 `toImage2` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` 要转换的PDF文件的对象。
   * 包含 `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` 有关目标图像格式的各种首选项的对象。
   该方 `toImage2` 法返回包含 `java.util.List` 图像的对象。 集合中的每个元素都是一个 `com.adobe.idp.Document` 实例。

1. 从集合中检索图像文件。

   遍历对 `java.util.List` 象以确定是否存在图像。 每个元素都是一个 `com.adobe.idp.Document` 实例。 通过调用对象的方 `com.adobe.idp.Document` 法并传递对 `copyToFile` 象来保存图 `java.io.File` 像。

**另请参阅**

[快速开始（SOAP模式）:使用Java API将PDF文档转换为JPEG文件](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用Web服务API将PDF文档转换为图像文件 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

使用“转换PDF服务API（Web服务）”将PDF文档转换为图像格式：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建转换PDF客户端。

   * 使用对 `ConvertPdfServiceClient` 象的默认构造函数创建对象。
   * 使用构 `ConvertPdfServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.)您无需使用该属 `lc_version` 性。 但是，请指 `?blob=mtom`定。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `ConvertPdfServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `ConvertPdfServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 此 `BLOB` 对象用于存储PDF表单。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它指定PDF表单的位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 通过获取对象的属性确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 设置运行时选项。

   * 使用对 `ToImageOptionsSpec` 象的构造函数创建对象。
   * 根据需要调用属于此对象的方法。 例如，通过调用方法并传递指定格 `setImageConvertFormat` 式类型的明细列表 `ImageConvertFormat` 值来设置图像类型。
   >[!NOTE]
   >
   >必须 `ImageConvertFormat` 设置明细列表值。

1. 将PDF转换为图像。

   调用对 `ConvertPDFServiceService` 象的方 `toImage2` 法并传递以下值：

   * 表示 `BLOB` 要转换的文件的对象
   * 包含 `ToImageOptionsSpec` 有关目标图像格式的各种首选项的对象
   该方 `toImage2` 法返回一个 `MyArrayOfBLOB` 包含新创建的图像文件的对象。

1. 从集合中检索图像文件。

   * 通过获取对象字段 `MyArrayOfBLOB` 的值，确定对象中的元素 `Count` 数。 每个元素都是 `BLOB` 一个包含图像的对象。
   * 遍历对象并 `MyArrayOfBLOB` 保存每个图像文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
