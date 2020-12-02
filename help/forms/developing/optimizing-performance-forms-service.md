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
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 0%

---


# 优化Forms服务的性能{#optimizing-the-performance-of-theforms-service}

## 优化Forms服务的性能{#optimizing-the-performance-of-the-forms-service}

呈现表单时，您可以设置运行时选项，以优化Forms服务的性能。 您可以执行的另一个任务是将XDP文件存储在存储库中，以提高Forms服务的性能。 但是，本节不介绍如何执行此任务。 （请参阅[使用Java客户端库调用服务](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)。）

>[!NOTE]
>
>有关Forms服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要在呈现表单时优化Forms服务的性能，请执行以下任务:

1. 包括项目文件。
1. 创建一个Forms客户端API对象。
1. 设置性能运行时选项。
1. 渲染表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

在以编程方式执行Forms服务客户端API操作之前，必须创建Forms服务客户端。 如果您使用Java API，请创建`FormsServiceClient`对象。 如果您使用的是FormsWeb服务API，请创建一个`FormsService`对象。

**设置性能运行时选项**

您可以设置以下性能运行时选项来改进Forms服务的性能：

* **表单缓存**:可以在服务器缓存中缓存呈现为PDF的表单。每个表单在首次生成后缓存。 在随后的渲染中，如果缓存的表单比表单设计的时间戳新，则从缓存检索表单。 通过缓存表单，您可以提高Forms服务的性能，因为它不必从存储库中检索表单设计。
* 表单参考线（已弃用）的渲染时间可能比其他转换类型要长。 建议您缓存表单指南（已弃用）以提高性能。
* **独立选项**:如果您不需要Forms服务执行服务器端计算，可以将“独立”选项设置为，这 `true`会导致表单呈现时没有状态信息。如果要向最终用户呈现交互式表单，并将该表单输入到表单中并将其提交回Forms服务，则状态信息是必需的。 然后，Forms服务执行计算操作并将表单呈现回用户，结果显示在表单中。 如果将没有状态信息的表单提交回Forms服务，则只有XML数据可用，且不执行服务器端计算。
* **线性化的PDF**:组织线性化的PDF文件，以在网络环境中实现有效的增量访问。PDF文件在所有方面都是有效的PDF，并且与所有现有查看器和其他PDF应用程序兼容。 即，可在下载线性化的PDF时查看它。
* 当在客户端上渲染PDF表单时，此选项不会提高性能。
* **GuideRSL选项**:启用使用运行时共享库生成表单指南（已弃用）。这意味着第一个请求将下载较小的SWF文件以及存储在浏览器缓存中的较大共享库。 有关详细信息，请参阅Flex文档中的RSL。
* 您还可以通过在客户端上呈现表单来改进Forms服务的性能。 (请参阅[在客户端渲染Forms](/help/forms/developing/rendering-forms-client.md)。)

**渲染表单**

要在设置性能选项后渲染表单，请使用与渲染没有性能选项的表单相同的应用程序逻辑。

**将表单数据流写入客户端Web浏览器**

在Forms服务呈现表单后，它返回一个表单数据流，您必须将该数据流写入客户端Web浏览器。 写入客户端Web浏览器时，用户可以看到表单。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建呈现Forms的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#optimize-the-performance-using-the-java-api}优化性能

使用FormsAPI(Java)渲染性能优化的表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormsServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 设置性能运行时选项

   * 使用`PDFFormRenderSpec`对象的构造函数创建&lt;a0/>对象。
   * 通过调用`PDFFormRenderSpec`对象的`setCacheEnabled`方法并传递`true`来设置表单缓存选项。
   * 通过调用`PDFFormRenderSpec`对象的`setLinearizedPDF`方法并传递`true.`来设置线性化选项

1. 渲染表单

   调用`FormsServiceClient`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递一个空`com.adobe.idp.Document`对象。
   * 一个`PDFFormRenderSpec`对象，它存储运行时选项以提高性能。
   * 一个`URLSpec`对象，它包含Forms服务所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。

   `renderPDFForm`方法返回一个`FormsResult`对象，该对象包含一个必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流发送到客户端Web浏览器。
   * 通过调用`FormsResult`对象“s `getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数进行传递，创建一个字节数组并将其填充为表单数据流。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[快速开始（SOAP模式）:使用Java API优化性能](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#optimize-the-performance-using-the-web-service-api}优化性能

使用FormsAPI（Web服务）渲染性能优化的表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms客户端API对象

   创建`FormsService`对象并设置身份验证值。

1. 设置性能运行时选项

   * 使用`PDFFormRenderSpec`对象的构造函数创建&lt;a0/>对象。
   * 通过调用`PDFFormRenderSpec`对象的`setCacheEnabled`方法并传递true来设置表单缓存选项。
   * 通过调用`PDFFormRenderSpec`对象的`setStandAlone`方法并传递true来设置独立选项。
   * 通过调用`PDFFormRenderSpec`对象的`setLinearizedPDF`方法并传递true来设置线性化选项。

1. 渲染表单

   调用`FormsService`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递`null`。
   * 存储运行时选项的`PDFFormRenderSpecc`对象。
   * 一个`URLSpec`对象，它包含Forms服务所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 它用于存储呈现的PDF表单。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 （此参数将存储表单中的页数）。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 （此参数将存储区域设置值）。
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `renderPDFForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值，创建`FormResult`对象。
   * 创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流发送到客户端Web浏览器。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充它。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
