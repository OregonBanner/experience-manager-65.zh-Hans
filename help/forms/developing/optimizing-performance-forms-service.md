---
title: 优化Forms服务的性能
seo-title: 优化Forms服务的性能
description: 'null'
seo-description: 'null'
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 优化Forms服务的性能 {#optimizing-the-performance-of-theforms-service}

## 优化Forms服务的性能 {#optimizing-the-performance-of-the-forms-service}

在呈现表单时，您可以设置运行时选项以优化Forms服务的性能。 可以执行的另一个任务是将XDP文件存储在存储库中，以提高Forms服务的性能。 但是，本节不介绍如何执行此任务。 (请参 [阅使用Java客户端库调用服务](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)。)

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要在呈现表单时优化表单服务的性能，请执行以下任务：

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 设置性能运行时选项。
1. 渲染表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式执行Forms服务客户端API操作之前，必须先创建Forms服务客户端。 如果您使用Java API，请创建一个对 `FormsServiceClient` 象。 如果您使用的是Forms web服务API，请创建一个对 `FormsService` 象。

**设置性能运行时选项**

您可以设置以下性能运行时选项来改进Forms服务的性能：

* **表单缓存**:您可以在服务器缓存中缓存呈现为PDF的表单。 每个表单在首次生成后都会缓存。 在随后的渲染中，如果缓存的表单比表单设计的时间戳新，则从缓存检索表单。 通过缓存表单，可以提高Forms服务的性能，因为它不必从存储库检索表单设计。
* 表单参考线（已弃用）的渲染时间可能比其他转换类型更长。 建议您缓存表单指南（已弃用）以提高性能。
* **独立选项**:如果不需要Forms服务执行服务器端计算，可以将“独立”选项设置为 `true`，这会导致表单呈现时没有状态信息。 如果要向最终用户呈现交互式表单，然后在表单中输入信息并将表单提交回表单服务，则需要状态信息。 然后，表单服务执行计算操作并将表单呈现回用户，结果显示在表单中。 如果将没有状态信息的表单提交回Forms服务，则只有XML数据可用，且不执行服务器端计算。
* **线性化PDF**:线性化的PDF文件经过组织，可在网络环境中实现高效的增量访问。 PDF文件在所有方面都是有效的PDF，并且与所有现有查看器和其他PDF应用程序兼容。 即，可在下载线性化的PDF时查看它。
* 在客户端上渲染PDF表单时，此选项不会提高性能。
* **GuideRSL选项**:启用使用运行时共享库生成表单指南（已弃用）。 这意味着第一个请求将下载较小的SWF文件以及存储在浏览器缓存中的较大的共享库。 有关详细信息，请参阅Flex文档中的RSL。
* 您还可以通过在客户端上渲染表单来提高Forms服务的性能。 (请参阅 [在客户端渲染表单](/help/forms/developing/rendering-forms-client.md)。)

**渲染表单**

要在设置性能选项后渲染表单，请使用与渲染没有性能选项的表单相同的应用程序逻辑。

**将表单数据流写入客户端Web浏览器**

在表单服务呈现表单后，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器。 当写入到客户端Web浏览器时，用户可看到表单。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF表单](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将表单渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建呈现表单的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API优化性能 {#optimize-the-performance-using-the-java-api}

使用Forms API(Java)渲染性能优化的表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 设置性能运行时选项

   * 使用对 `PDFFormRenderSpec` 象的构造函数创建对象。
   * 通过调用对象的方法并传递 `PDFFormRenderSpec` 来设置表 `setCacheEnabled` 单缓存选项 `true`。
   * 通过调用对象的方法并 `PDFFormRenderSpec` 传递来设置线 `setLinearizedPDF` 性化选项 `true.`

1. 渲染表单

   调用对 `FormsServiceClient` 象的方 `renderPDFForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。
   * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象。 如果不想合并数据，请传递空对 `com.adobe.idp.Document` 象。
   * 存储 `PDFFormRenderSpec` 运行时选项以提高性能的对象。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   该方 `renderPDFForm` 法返回一个对 `FormsResult` 象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 创建一 `javax.servlet.ServletOutputStream` 个对象，用于将表单数据流发送到客户端Web浏览器。
   * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
   * 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
   * 创建一个字节数组，并通过调用对象的方法并将字 `InputStream` 节数组作 `read`为参数传递，用表单数据流填充它。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[快速入门（SOAP模式）:使用Java API优化性能](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API优化性能 {#optimize-the-performance-using-the-web-service-api}

使用Forms API（Web服务）渲染性能优化的表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建对 `FormsService` 象并设置身份验证值。

1. 设置性能运行时选项

   * 使用对 `PDFFormRenderSpec` 象的构造函数创建对象。
   * 通过调用对象的方法并传递true `PDFFormRenderSpec` 来设置表 `setCacheEnabled` 单缓存选项。
   * 通过调用对象的方法并传 `PDFFormRenderSpec` 递true来设置 `setStandAlone` 独立选项。
   * 通过调用对象的方法并传递 `PDFFormRenderSpec` true来设置线 `setLinearizedPDF` 性化选项。

1. 渲染表单

   调用对 `FormsService` 象的方 `renderPDFForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。
   * 包含 `BLOB` 要与表单合并的数据的对象。 如果您不想合并数据，请传递 `null`。
   * 存 `PDFFormRenderSpecc` 储运行时选项的对象。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空对象。 它用于存储渲染的PDF表单。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空对象。 （此参数将存储表单中的页数）。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对象。 （此参数将存储区域设置值）。
   * 将包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作结果的空对象。
   该方 `renderPDFForm` 法使用必 `com.adobe.idp.services.holders.FormsResultHolder` 须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `FormResult` 获取对象数据成员的 `com.adobe.idp.services.holders.FormsResultHolder` 值来创建 `value` 对象。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，用于将表单数据流发送到客户端Web浏览器。
   * 通过调 `BLOB` 用对象的方法创建包含表 `FormsResult` 单数据的对 `getOutputContent` 象。
   * 创建一个字节数组，并通过调用对象的 `BLOB` 方法填充该 `getBinaryData` 数组。 此任务将对象的内 `FormsResult` 容分配给字节数组。
   * 调用对 `javax.servlet.http.HttpServletResponse` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
