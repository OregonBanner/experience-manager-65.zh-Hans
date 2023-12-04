---
title: 使用自定义CSS文件渲染HTMLForms
description: 使用Forms服务引用自定义CSS文件来呈现HTML表单，以响应来自Web浏览器的HTTP请求。 您可以使用Java API和Web服务API呈现使用CSS文件的HTML表单。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 0%

---

# 使用自定义CSS文件渲染HTMLForms {#rendering-html-forms-using-custom-css-files}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

Forms服务会呈现HTML表单，以响应来自Web浏览器的HTTP请求。 呈现HTML表单时，Forms服务可以引用自定义CSS文件。 您可以创建一个自定义CSS文件以满足您的业务要求，并在使用Forms服务渲染HTML表单时引用该CSS文件。

Forms服务可静默解析自定义CSS文件。 也就是说，Forms服务不会报告在自定义CSS文件不符合CSS标准时可能遇到的错误。 在这种情况下，Forms服务会忽略样式，继续处理CSS文件中的其余样式。

以下列表指定了自定义CSS文件中支持的样式：

* **类级别选择器样式对**：如果存在于自定义CSS文件中，则会使用在HTML表单中用作类样式的选择器。 未使用的类样式将被忽略。
* **标识符级别选择器样式对**：如果在HTML表单中使用了所有标识符样式，则使用这些样式。
* **元素级别选择器样式对**：如果在HTML表单中使用了所有元素样式，则使用这些样式。
* **样式优先级**：支持样式优先级（例如重要），并可在自定义CSS文件中使用。
* **媒体类型**：一个或多个选择器样式对可以封装在@media样式中来定义媒体类型。 Forms服务不检查指定的媒体类型是否受支持。 自定义CSS文件中指定的媒体类型将合并到HTML表单中。

您可以使用FormsIVS应用程序检索示例CSS文件。 上传表单，在“测试表单设计”页面中选择它，然后单击“生成CSS”。 在单击该按钮之前，您不需要设置HTML转换类型。 接下来，选择“保存”。 您可以编辑此CSS文件以满足您的业务要求。

>[!NOTE]
>
>在呈现使用自定义CSS文件的HTML表单之前，请务必充分了解如何呈现HTML表单。 (请参阅 [将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步骤摘要 {#summary-of-steps}

要呈现使用CSS文件的HTML表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms Java API对象。
1. 引用CSS文件。
1. 呈现HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms Java API对象**

您必须先创建Forms客户端对象，然后才能以编程方式执行Forms服务支持的操作。

**引用CSS文件**

要呈现使用自定义CSS文件的HTML表单，请确保引用现有的CSS文件。

**呈现HTML表单**

要呈现HTML表单，请指定在Designer中创建并保存为XDP文件的表单设计。 选择HTML转换类型。 例如，您可以指定用于呈现Internet Explorer 5.0或更高版本的动态HTML的HTML转换类型。

呈现HTML表单还需要值，例如呈现其他表单类型所需的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务渲染HTML表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器，才能使用户看到HTML表单。

**另请参阅**

[渲染使用CSS文件的HTML表单（使用Java API）](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 渲染使用CSS文件的HTML表单（使用Java API） {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

使用Forms API (Java)呈现使用自定义CSS文件的HTML表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。

1. 创建Forms Java API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用CSS文件

   * 创建 `HTMLRenderSpec` 对象。
   * 要呈现使用自定义CSS文件的HTML表单，请调用 `HTMLRenderSpec` 对象的 `setCustomCSSURI` 方法，并传递一个指定CSS文件位置和名称的字符串值。

1. 呈现HTML表单

   调用 `FormsServiceClient` 对象的 `(Deprecated) (Deprecated) renderHTMLForm` 方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保您指定完整的路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 用于指定HTML首选项类型的枚举值。 例如，要呈现与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递一个空值 `com.adobe.idp.Document` 对象。
   * 此 `HTMLRenderSpec` 存储HTML运行时选项的对象。
   * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` 用于存储呈现HTML表单所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   此 `(Deprecated) renderHTMLForm` 方法返回 `FormsResult` 包含必须写入客户端Web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `com.adobe.idp.Document` 对象，方法是调用 `FormsResult` 对象 `getOutputContent` 方法。
   * 获取的内容类型 `com.adobe.idp.Document` 对象(通过调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 通过调用对象的内容类型 `setContentType` 方法和传递的内容类型 `com.adobe.idp.Document` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.h\ttp.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建 `java.io.InputStream` 对象，方法是调用 `com.adobe.idp.Document` 对象的 `getInputStream` 方法。
   * 创建字节数组，并通过调用 `InputStream` 对象的 `read` 方法并将字节数组作为参数传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象的 `write` 将表单数据流发送到客户端Web浏览器的方法。 将字节数组传递给 `write` 方法。

**另请参阅**

[使用自定义CSS文件渲染HTMLForms](#rendering-html-forms-using-custom-css-files)

[快速入门（SOAP模式）：呈现使用CSS文件的HTML表单（使用Java API）](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 渲染使用CSS文件的HTML表单（使用Web服务API） {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

使用Forms API（Web服务）呈现使用自定义CSS文件的HTML表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 在类路径中包含Java代理类。

1. 创建Forms Java API对象

   创建 `FormsService` 对象并设置身份验证值。

1. 引用CSS文件

   * 创建 `HTMLRenderSpec` 对象。
   * 要呈现使用自定义CSS文件的HTML表单，请调用 `HTMLRenderSpec` 对象的 `setCustomCSSURI` 方法，并传递一个指定CSS文件位置和名称的字符串值。

1. 呈现HTML表单

   调用 `FormsService` 对象的 `(Deprecated) renderHTMLForm` 方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保您指定完整的路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 用于指定HTML首选项类型的枚举值。 例如，要呈现与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`.
   * A `BLOB` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递 `null`. (请参阅 [使用可流布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * 此 `HTMLRenderSpec` 存储HTML运行时选项的对象。
   * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 如果您不想设置此值，则可以传递空字符串。
   * A `URLSpec` 用于存储呈现HTML表单所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。
   * 空的 `com.adobe.idp.services.holders.BLOBHolder` 由填充的对象 `(Deprecated) renderHTMLForm` 方法。 此参数值存储渲染的表单。
   * 空的 `com.adobe.idp.services.holders.BLOBHolder` 由填充的对象 `(Deprecated) renderHTMLForm` 方法。 此参数存储输出XML数据。
   * 空的 `javax.xml.rpc.holders.LongHolder` 由填充的对象 `(Deprecated) renderHTMLForm` 方法。 此参数存储表单中的页数。
   * 空的 `javax.xml.rpc.holders.StringHolder` 由填充的对象 `(Deprecated) renderHTMLForm` 方法。 此参数存储区域设置值。
   * 空的 `javax.xml.rpc.holders.StringHolder` 由填充的对象 `(Deprecated) renderHTMLForm` 方法。 此参数用于存储使用的HTML渲染值。
   * 空的 `com.adobe.idp.services.holders.FormsResultHolder` 将包含此操作结果的对象。

   此 `(Deprecated) renderHTMLForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值传递的对象，该对象具有必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象的 `value` 数据成员。
   * 创建 `BLOB` 通过调用 `FormsResult` 对象的 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 对象(通过调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 通过调用对象的内容类型 `setContentType` 方法和传递的内容类型 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建字节数组，并通过调用 `BLOB` 对象的 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象的 `write` 将表单数据流发送到客户端Web浏览器的方法。 将字节数组传递给 `write` 方法。

**另请参阅**

[使用自定义CSS文件渲染HTMLForms](#rendering-html-forms-using-custom-css-files)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
