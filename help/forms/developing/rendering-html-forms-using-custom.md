---
title: 使用自定义CSS文件渲染HTMLForms
seo-title: 使用自定义CSS文件渲染HTMLForms
description: 'null'
seo-description: 'null'
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: fcbe1d860410e215cb7c438f94579e0b14d262a5
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 0%

---


# 使用自定义CSS文件{#rendering-html-forms-using-custom-css-files}渲染HTMLForms

Forms服务响应来自Web浏览器的HTTP请求来呈现HTML表单。 呈现HTML表单时，Forms服务可引用自定义CSS文件。 您可以创建自定义CSS文件以满足您的业务要求，并在使用Forms服务渲染HTML表单时引用该CSS文件。

Forms服务以静默方式解析自定义CSS文件。 即，Forms服务不会报告在自定义CSS文件不符合CSS标准时可能遇到的错误。 在这种情况下，Forms服务将忽略该样式，并继续保留CSS文件中的其余样式。

以下列表指定自定义CSS文件中支持的样式：

* **类级选择器——样式对**:如果自定义CSS文件中存在，则使用HTML表单中用作类样式的选择器。将忽略未使用的类样式。
* **标识符级别选择器——样式对**:如果在HTML表单中使用所有标识符样式，则会使用这些样式。
* **元素级选择器样式对**:如果在HTML表单中使用所有元素样式，则会使用这些样式。
* **样式优先级**:支持样式优先级（如重要内容），并可在自定义CSS文件中使用。
* **媒体类型**:一个或多个选择器样式对可以打包在@media样式中以定义媒体类型。Forms服务不检查是否支持指定的媒体类型。 在自定义CSS文件中指定的媒体类型将合并到HTML表单中。

您可以使用FormsIVS应用程序检索示例CSS文件。 上传表单，在“测试表单设计”页面中选择它，然后单击“生成CSS”。 单击按钮之前，无需设置HTML转换类型。 下一步选择保存。 您可以编辑此CSS文件以满足您的业务需求。

>[!NOTE]
>
>在渲染使用自定义CSS文件的HTML表单之前，您必须对渲染HTML表单有深入的了解。 (请参阅[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)。)

>[!NOTE]
>
>有关Forms服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤{#summary-of-steps}的摘要

要渲染使用CSS文件的HTML表单，请执行以下任务:

1. 包括项目文件。
1. 创建一个FormsJava API对象。
1. 引用CSS文件。
1. 渲染HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建FormsJava API对象**

在以编程方式执行Forms服务支持的操作之前，必须创建Forms客户端对象。

**引用CSS文件**

要渲染使用自定义CSS文件的HTML表单，请确保引用现有CSS文件。

**渲染HTML表单**

要渲染HTML表单，必须指定在Designer中创建并另存为XDP文件的表单设计。 还必须选择HTML转换类型。 例如，可指定用于为Internet Explorer 5.0或更高版本渲染动态HTML的HTML转换类型。

渲染HTML表单还需要值，如渲染其他表单类型所需的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现HTML表单时，它返回一个表单数据流，您必须将该数据流写入客户端Web浏览器，以使用户可以看到该HTML表单。

**另请参阅**

[使用Java API渲染使用CSS文件的HTML表单](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建呈现Forms的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#render-an-html-form-that-uses-a-css-file-using-the-java-api}渲染使用CSS文件的HTML表单

使用FormsAPI(Java)渲染使用自定义CSS文件的HTML表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建FormsJava API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormsServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 引用CSS文件

   * 使用`HTMLRenderSpec`对象的构造函数创建&lt;a0/>对象。
   * 要呈现使用自定义CSS文件的HTML表单，请调用`HTMLRenderSpec`对象的`setCustomCSSURI`方法并传递一个字符串值，它指定CSS文件的位置和名称。

1. 渲染HTML表单

   调用`FormsServiceClient`对象的`(Deprecated) (Deprecated) renderHTMLForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 一个`TransformTo`枚举值，它指定HTML首选项类型。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定`TransformTo.MSDHTML`。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递一个空`com.adobe.idp.Document`对象。
   * 存储HTML运行时选项的`HTMLRenderSpec`对象。
   * 指定`HTTP_USER_AGENT`头值的字符串值，如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * 一个`URLSpec`对象，用于存储呈现HTML表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。

   `(Deprecated) renderHTMLForm`方法返回一个`FormsResult`对象，该对象包含一个必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象“s `getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.h\ttp.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数进行传递，创建一个字节数组并将其填充为表单数据流。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[使用自定义CSS文件渲染HTMLForms](#rendering-html-forms-using-custom-css-files)

[快速开始（SOAP模式）:使用Java API渲染使用CSS文件的HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}渲染使用CSS文件的HTML表单

使用FormsAPI（Web服务）渲染使用自定义CSS文件的HTML表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 在类路径中包含Java代理类。

1. 创建FormsJava API对象

   创建`FormsService`对象并设置身份验证值。

1. 引用CSS文件

   * 使用`HTMLRenderSpec`对象的构造函数创建&lt;a0/>对象。
   * 要呈现使用自定义CSS文件的HTML表单，请调用`HTMLRenderSpec`对象的`setCustomCSSURI`方法并传递一个字符串值，它指定CSS文件的位置和名称。

1. 渲染HTML表单

   调用`FormsService`对象的`(Deprecated) renderHTMLForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 一个`TransformTo`枚举值，它指定HTML首选项类型。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定`TransformTo.MSDHTML`。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递`null`。 (请参阅[使用可流动布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * 存储HTML运行时选项的`HTMLRenderSpec`对象。
   * 指定`HTTP_USER_AGENT`头值的字符串值，如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果不想设置此值，可以传递空字符串。
   * 一个`URLSpec`对象，用于存储呈现HTML表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数值存储呈现的表单。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数存储输出XML数据。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 此参数存储表单中的页数。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数存储区域设置值。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数存储所使用的HTML呈现值。
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `(Deprecated) renderHTMLForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值，创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 通过调用`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用`setContentType`方法并传递`BLOB`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充它。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[使用自定义CSS文件渲染HTMLForms](#rendering-html-forms-using-custom-css-files)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
