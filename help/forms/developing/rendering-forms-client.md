---
title: 在客户端呈现Forms
seo-title: 在客户端呈现Forms
description: 通过使用Acrobat或Adobe Reader的客户端渲染功能，优化PDF内容的投放并改进Forms服务处理网络负载的能力
seo-description: 通过使用Acrobat或Adobe Reader的客户端渲染功能，优化PDF内容的投放并改进Forms服务处理网络负载的能力
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# 在客户端{#rendering-forms-at-the-client}处呈现Forms

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 在客户端{#rendering-forms-at-the-client-inner}处呈现Forms

您可以使用Acrobat或Adobe Reader的客户端渲染功能优化PDF内容的投放并改进Forms服务处理网络负载的能力。 此过程称为在客户端渲染表单。 要在客户端渲染表单，客户端设备（通常是Web浏览器）必须使用Acrobat 7.0或Adobe Reader 7.0或更高版本。

服务器端脚本执行对表单所做的更改不会反映在客户端呈现的表单中，除非根子表单包含设置为`auto`的`restoreState`属性。 有关此属性的详细信息，请参阅[Forms Designer。](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅[AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)的服务参考。

### 步骤{#summary-of-steps}的摘要

要在客户端渲染表单，请执行以下任务:

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 设置客户端渲染运行时选项。
1. 在客户端渲染表单。
1. 将表单写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式执行Forms服务客户端API操作之前，必须创建Forms服务客户端。 如果您使用Java API，请创建`FormsServiceClient`对象。 如果您使用Forms Web服务API，请创建`FormsService`对象。

**设置客户端渲染运行时选项**

您必须设置客户端渲染运行时选项，以通过将`RenderAtClient`运行时选项设置为`true`在客户端渲染表单。 这会导致表单被传送到呈现表单的客户端设备。 如果`RenderAtClient`为`auto`（默认值），则表单设计将确定表单是否在客户端呈现。 表单设计必须是具有可流动布局的表单设计。

可以设置的可选运行时选项是`SeedPDF`选项。 `SeedPDF`选项将PDF容器(种子PDF文档)与表单设计和XML数据相结合。 表单设计和XML数据都会交付到Acrobat或Adobe Reader，在那里可以呈现表单。 当客户端计算机中没有表单中使用的字体时（例如，当最终用户未获得使用表单所有者有权使用的字体的许可时），可以使用`SeedPDF`选项。

您可以使用设计器创建简单的动态PDF文件，以用作种子PDF文件。 执行此任务需要执行以下步骤：

1. 确定是否需要在种子PDF文件中嵌入任何字体。 种子PDF文件需要包含要渲染的表单所需的其他字体。 在将字体嵌入种子PDF文件时，请确保您没有违反任何字体许可协议。 在Designer中，您可以确定是否可以合法嵌入字体。 在保存时，如果存在无法嵌入到表单中的字体，Designer会显示一条消息，其中列出了您无法嵌入的字体。 对于静态PDF文档，此消息不在Designer中显示。
1. 如果您是在Designer中创建种子PDF文件，建议至少添加一个包含消息的文本字段。 此消息应针对Adobe Reader早期版本的用户，这些用户声明他们需要Acrobat 7.0或更高版本，或Adobe Reader 7.0或更高版本才能视图文档。
1. 将种子PDF文件另存为具有PDF文件扩展名的动态PDF文件。

>[!NOTE]
>
>您无需定义种子PDF运行时选项即可在客户端上渲染表单。 如果未指定种子PDF，Forms服务将创建一个外壳pdf，它将不包含COS对象，但将包含一个PDF包装器，实际XDP内容嵌入其中。 本节中的步骤不会设置种子PDF运行时选项。 有关COS对象的信息，请参阅《Adobe PDF参考指南》。

**在客户端上呈现表单**

要在客户端渲染表单，必须确保在渲染表单时应用程序逻辑中包含客户端渲染运行时选项。

**将表单数据流写入客户端Web浏览器**

Forms服务会创建一个表单数据流，您必须将其写入客户端Web浏览器。 当写入到客户端Web浏览器时，表单由Acrobat 7.0或Adobe Reader 7.0或更高版本渲染，并且对用户可见。

**另请参阅**

[使用Java API在客户端渲染表单](#render-a-form-at-the-client-using-the-java-api)

[使用Web服务API在客户端渲染表单](#render-a-form-at-the-client-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建渲染Forms的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#render-a-form-at-the-client-using-the-java-api}在客户端渲染表单

使用Forms API(Java)在客户端渲染表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormsServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 设置客户端渲染运行时选项

   * 使用`PDFFormRenderSpec`对象的构造函数创建对象。
   * 通过调用`PDFFormRenderSpec`对象的`setRenderAtClient`方法并传递枚举值`RenderAtClient.Yes`来设置`RenderAtClient`运行时选项。

1. 在客户端上呈现表单

   调用`FormsServiceClient`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是AEM Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递空`com.adobe.idp.Document`对象。
   * 一个`PDFFormRenderSpec`对象，用于存储在客户端呈现表单所需的运行时选项。
   * 一个`URLSpec`对象，其中包含Forms服务渲染表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。

   `renderPDFForm`方法返回一个`FormsResult`对象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象&#39;s `getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数传递，创建一个字节数组并将其填充为表单数据流。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[快速开始（SOAP模式）：使用Java API在客户端呈现表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#render-a-form-at-the-client-using-the-web-service-api}在客户端渲染表单

使用Forms API（Web服务）在客户端渲染表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建`FormsService`对象并设置身份验证值。

1. 设置客户端渲染运行时选项

   * 使用`PDFFormRenderSpec`对象的构造函数创建对象。
   * 通过调用`PDFFormRenderSpec`对象的`setRenderAtClient`方法并传递字符串值`RenderAtClient.Yes`来设置`RenderAtClient`运行时选项。

1. 在客户端上呈现表单

   调用`FormsService`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递`null`。 (请参阅[使用可流式布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * 一个`PDFFormRenderSpec`对象，用于存储在客户端呈现表单所需的运行时选项。
   * `URLSpec`对象，其中包含Forms服务所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数用于存储呈现的PDF表单。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 （此参数将存储表单中的页数）。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 （此参数将存储区域设置值）。
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `renderPDFForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值，创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建一个包含表单数据的`BLOB`对象。
   * 通过调用`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用`setContentType`方法并传递`BLOB`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充它。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[在客户端呈现Forms](#rendering-forms-at-the-client)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
