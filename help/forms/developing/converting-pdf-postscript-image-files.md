---
title: 将PDF转换为Postscript和Image文件
seo-title: 将PDF转换为Postscript和Image文件
description: 使用“转换PDF”服务，可以使用Java API和Web服务API将PDF文档转换为PostScript以及多种图像格式（JPEG、JPEG 2000、PNG和TIFF）。
seo-description: 使用“转换PDF”服务，可以使用Java API和Web服务API将PDF文档转换为PostScript以及多种图像格式（JPEG、JPEG 2000、PNG和TIFF）。
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '2846'
ht-degree: 0%

---


# 将PDF转换为Postscript和图像文件{#converting-pdf-to-postscript-andimage-files}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于转换PDF服务**

“转换PDF”服务会将PDF文档转换为PostScript和多种图像格式（JPEG、JPEG 2000、PNG和TIFF）。 将PDF文档转换为PostScript对于在任何PostScript打印机上基于服务器的无人参与打印都很有用。 在不支持PDF文档的内容管理系统中存档文档时，将PDF文档转换为多页TIFF文件非常实用。

您可以使用“转换PDF”服务完成以下任务:

* 将PDF文档转换为PostScript。
* 将PDF文档转换为图像格式。

>[!NOTE]
>
>有关转换PDF服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将PDF文档转换为PostScript {#converting-pdf-documents-to-postscript}

本主题介绍如何使用“转换PDF服务API（Java和Web服务）”以编程方式将PDF文档转换为PostScript文件。 转换为PostScript文件的PDF文档必须是非交互式PDF文档。 即，如果尝试将交互式PDF文档转换为PostScript文件，则会引发异常。

>[!NOTE]
>
>有关转换PDF服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要将PDF文档转换为PostScript文件，请执行以下步骤：

1. 包括项目文件。
1. 创建“转换PDF”服务客户端。
1. 引用PDF文档以转换为PostScript文件。
1. 设置转换运行时选项。
1. 将PDF文档转换为PostScript文件。
1. 保存PostScript文件。

**包括项目文件**

将必要的文件包含到开发项目中。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建转换PDF客户端**

在以编程方式执行“转换PDF”服务操作之前，必须创建“转换PDF”服务客户端。 如果您使用Java API，请创建`ConvertPdfServiceClient`对象。 如果您使用Web服务API，请创建`ConvertPDFServiceService`对象。

本节使用AEM Forms中引入的Web服务功能。 要访问新功能，必须使用`lc_version`属性构建代理对象。 (请参阅[使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)中的“使用Web服务访问新功能”。)

**引用PDF文档以转换为PostScript文件**

引用要转换为PostScript文件的PDF文档。 如本主题前面所述，PDF文档必须是非交互式PDF文档。 如果尝试将交互式PDF文档转换为PostScript文件，将引发异常。

**设置转换运行时选项**

将PDF文档转换为PostScript文件时，可以定义指定所创建的PostScript类型的运行时选项。 例如，您可以定义第3级PostScript文件。

通常，生成的PostScript文件将反映输入PDF文档的大小。 如果选择`ShrinkToFit`选项（该选项会缩小PostScript文件的输出以适合页面），您将看不到输入的PDF文档与生成的PostScript文件之间的区别。 `ShrinkToFit`选项仅在选择以比输入PDF文档小的页面大小打印时生效。 要选择较小的页面大小，请定义`PageSize`选项。 此外，建议将`RotateAndCenter`选项设置为`true`以获得正确的PostScript输出。

同样，如果您选择`ExpandToFit`选项（该选项扩展了PostScript文件的输出以适合页面），则仅当您选择以比输入PDF文档更大的页面大小打印时，才生效。 要选择较大的页面大小，请定义`PageSize`选项。 此外，建议将`RotateAndCenter`选项设置为`true`以获得正确的PostScript输出。

>[!NOTE]
>
>有关可以设置的运行时值的信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToPSOptionsSpec`类引用。

**将PDF文档转换为PostScript文件**

创建服务客户端并设置运行时选项后，可以调用PostScript转换操作。 此操作需要有关要转换的文档的信息，包括目标文档的首选PostScript级别。

**保存PostScript文件**

将PDF文档转换为PostScript后，可将输出另存为PostScript文件。

**另请参阅**

[使用Java API将PDF文档转换为PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[使用Web服务API将PDF文档转换为PS](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[转换PDF服务API快速开始](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-pdf-document-to-ps-using-the-java-api}将PDF文档转换为PS

使用“转换PDF服务API”(Java)将PDF文档转换为PostScript:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-convertpdf-client.jar。

1. 创建“转换PDF”客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`ConvertPdfServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 引用PDF文档以转换为PostScript文件。

   * 使用`java.io.FileInputStream`对象的构造函数创建一个对象，并传递一个字符串值，该字符串值指定要转换的PDF文档的位置。
   * 使用`com.adobe.idp.Document`构造函数创建存储PDF文档的`com.adobe.idp.Document`对象。 传递包含PDF文档的`java.io.FileInputStream`对象。

1. 设置转换运行时选项。

   * 通过调用其构造函数创建`ToPSOptionsSpec`对象。
   * 通过调用属于`ToPSOptionsSpec`对象的适当方法来设置运行时选项。 例如，要定义所创建的PostScript级别，请调用`ToPSOptionsSpec`对象的`setPsLevel`方法，并传递指定PostScript级别的`PSLevel`明细列表值。 有关可设置的所有运行时值的信息，请参阅[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToPSOptionsSpec`类引用。

1. 将PDF文档转换为PostScript文件。

   调用`ConvertPdfServiceClient`对象的`toPS2`方法并传递以下值：

   * 一个`com.adobe.idp.Document`对象，它表示要转换为PostScript文件的PDF文档。
   * 一个`ToPSOptionsSpec`对象，它指定PostScript运行时选项。

   `toPS2`方法返回一个`Document`对象，该对象包含新的PostScript文档。

1. 保存PostScript文件。

   * 创建一个`java.io.File`对象，并确保文件扩展名为.ps。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件（请确保使用由`toPS2`方法返回的`Document`对象）。

**另请参阅**

[步骤摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[快速开始（SOAP模式）：使用Java API将PDF文档转换为PostScript](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#convert-a-pdf-document-to-ps-using-the-web-service-api}将PDF文档转换为PS

使用“转换PDF服务API（Web服务）”将PDF文档转换为PostScript:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建“转换PDF”客户端。

   * 使用`ConvertPdfServiceClient`对象的默认构造函数创建对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`ConvertPdfServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 您无需使用`lc_version`属性。 但是，请指定`?blob=mtom`。
   * 通过获取`ConvertPdfServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 为字段`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`ConvertPdfServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`赋给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`赋给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用PDF文档以转换为PostScript文件。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储转换为PostScript文件的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示要转换的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 将`BLOB`对象的`MTOM`字段指定为字节数组的内容，从而填充该对象。

1. 设置转换运行时选项。

   * 通过调用其构造函数创建`ToPSOptionsSpec`对象。
   * 通过为`ToPSOptionsSpec`对象的数据成员分配值来设置运行时选项。 例如，要定义所创建的PostScript级别，请为`ToPSOptionsSpec`对象的`psLevel`明细列表成员分配一个`PSLevel`数据值。

1. 将PDF文档转换为PostScript文件。

   调用`GeneratePDFServiceService`对象的`toPS2`方法并传递以下值：

   * 一个`BLOB`对象，它表示要转换为PostScript文件的PDF文档
   * 指定运行时选项的`ToPSOptionsSpec`对象

   转换完成后，通过访问PostScript文档的`BLOB`对象的`MTOM`属性提取表示该数据的二进制数据。 这会返回一个字节数组，您可以将其写出到PostScript文件。

1. 保存PostScript文件。

   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它表示PS文件的文件位置。
   * 创建一个字节数组，用于存储`encryptPDFUsingPassword`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`字段的值来填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象，创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PostScript文件。

**另请参阅**

[步骤摘要](converting-pdf-postscript-image-files.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将PDF文档转换为图像格式{#converting-pdf-documents-to-image-formats}

您可以使用“转换PDF”服务以编程方式将PDF文档转换为图像格式，包括JPEG、JPEG 2000、TIFF和PNG。 通过将PDF文档转换为图像文件，您可以将PDF文档用作图像文件。 例如，可以将图像放入企业内容管理系统以进行存储。

将PDF文档转换为图像时，“转换PDF”服务会为文档中的每个页面创建单独的图像。 即，如果文档有20页，则“转换PDF”服务将创建20个图像文件。 将PDF文档转换为图像格式时，您可以为PDF文档中的每页创建单独的图像，或为整个PDF文档创建单个图像文件。

>[!NOTE]
>
>有关转换PDF服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要将PDF文档转换为任何支持的类型，请执行以下步骤：

1. 包括项目文件。
1. 创建“转换PDF”服务客户端。
1. 检索要转换的PDF文档。
1. 设置运行时选项。
1. 将PDF转换为图像。
1. 从集合中检索图像文件。

**包括项目文件**

将必要的文件包含到开发项目中。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建转换PDF客户端**

在以编程方式执行“转换PDF”服务操作之前，必须创建“转换PDF”服务客户端。 如果您使用Java API，请创建`ConvertPdfServiceClient`对象。 如果您使用Web服务API，请创建`ConvertPDFServiceService`对象。

**检索要转换的PDF文档**

必须检索PDF文档才能转换为图像。 无法将交互式PDF文档转换为图像。 如果尝试这样做，将引发异常。 要将交互式PDF文档转换为图像文件，您必须在转换PDF文档之前拼合它。 (请参阅[拼合PDF文档](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)。)

**设置运行时选项**

必须设置运行时选项，如图像格式和分辨率值。 有关运行时值的信息，请参阅[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`ToImageOptionsSpec`类引用。

**将PDF转换为图像**

在创建服务客户端并设置运行时选项后，可以将PDF文档转换为图像。 将返回包含图像的集合对象。

**从集合检索图像文件**

您可以从转换PDF服务返回的集合对象中检索图像文件。 集合中的每个元素都是一个`com.adobe.idp.Document`实例（如果您使用Web服务，则为一个`BLOB`实例），可以将其另存为图像文件，如JPG文件。

图像文件的格式取决于`ImageConvertFormat`运行时选项。 即，如果将`ImageConvertFormat`运行时选项设置为`ImageConvertFormat.JPEG`，则可以将图像文件另存为JPG文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[转换PDF服务API快速开始](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### 使用Java API {#convert-a-pdf-document-to-image-files-using-the-java-api}将PDF文档转换为图像文件

使用“转换PDF服务API(Java)”将PDF文档转换为图像格式：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-convertpdf-client.jar。

1. 创建“转换PDF”客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`ConvertPdfServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 检索要转换的PDF文档。

   * 创建一个`java.io.FileInputStream`对象，它使用其构造函数并传递一个指定PDF文档位置的字符串值来表示要转换的PDF文档。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建对象。

1. 设置运行时选项。

   * 使用`ToImageOptionsSpec`对象的构造函数创建对象。
   * 根据需要调用属于此对象的方法。 例如，通过调用`setImageConvertFormat`方法并传递指定格式类型的`ImageConvertFormat`枚举值来设置图像类型。

   >[!NOTE]
   >
   >必须设置`ImageConvertFormat`明细列表值。

1. 将PDF转换为图像。

   调用`ConvertPdfServiceClient`对象的`toImage2`方法并传递以下值：

   * 表示要转换的PDF文件的`com.adobe.idp.Document`对象。
   * 一个`com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec`对象，其中包含有关目标图像格式的各种首选项。

   `toImage2`方法返回包含图像的`java.util.List`对象。 集合中的每个元素都是`com.adobe.idp.Document`实例。

1. 从集合中检索图像文件。

   对`java.util.List`对象进行迭代以确定是否存在图像。 每个元素都是`com.adobe.idp.Document`实例。 通过调用`com.adobe.idp.Document`对象的`copyToFile`方法并传递`java.io.File`对象来保存图像。

**另请参阅**

[快速开始（SOAP模式）：使用Java API将PDF文档转换为JPEG文件](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### 使用Web服务API {#convert-a-pdf-document-to-image-files-using-the-web-service-api}将PDF文档转换为图像文件

使用“转换PDF服务API（Web服务）”将PDF文档转换为图像格式：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建转换PDF客户端。

   * 使用`ConvertPdfServiceClient`对象的默认构造函数创建对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`ConvertPdfServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 您无需使用`lc_version`属性。 但是，请指定`?blob=mtom`。
   * 通过获取`ConvertPdfServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 为字段`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`ConvertPdfServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`赋给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`赋给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索要转换的PDF文档。

   * 使用`BLOB`对象的构造函数创建对象。 此`BLOB`对象用于存储PDF表单。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它指定PDF表单的位置以及在中打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 通过获取`System.IO.FileStream`对象的`Length`属性，确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、起始位置和流长度。
   * 将`BLOB`对象的`MTOM`字段指定为字节数组的内容，从而填充该对象。

1. 设置运行时选项。

   * 使用`ToImageOptionsSpec`对象的构造函数创建对象。
   * 根据需要调用属于此对象的方法。 例如，通过调用`setImageConvertFormat`方法并传递指定格式类型的`ImageConvertFormat`明细列表值来设置图像类型。

   >[!NOTE]
   >
   >必须设置`ImageConvertFormat`明细列表值。

1. 将PDF转换为图像。

   调用`ConvertPDFServiceService`对象的`toImage2`方法并传递以下值：

   * 表示要转换的文件的`BLOB`对象
   * `ToImageOptionsSpec`对象，其中包含有关目标图像格式的各种首选项

   `toImage2`方法返回一个`MyArrayOfBLOB`对象，该对象包含新创建的图像文件。

1. 从集合中检索图像文件。

   * 通过获取`Count`字段的值，确定`MyArrayOfBLOB`对象中元素的数量。 每个元素都是包含图像的`BLOB`对象。
   * 遍历`MyArrayOfBLOB`对象并保存每个图像文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
