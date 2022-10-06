---
title: 按值呈现Forms
seo-title: Rendering Forms By Value
description: 使用Forms API(Java)通过Java API和Web服务API来按值呈现表单。
seo-description: Use the Forms API (Java) to render a form by value using the Java API and Web Service API.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 0%

---

# 按值呈现Forms {#rendering-forms-by-value}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

通常，在Designer中创建的表单设计会通过引用Forms服务来传递。 表单设计可能较大，因此，通过引用传递它们更为有效，从而避免必须按值封送表单设计字节。 Forms服务还可以缓存表单设计，以便在缓存时，不必持续读取表单设计。

如果表单设计包含UUID属性，则会缓存该属性。 对于所有表单设计，UUID值都是唯一的，可用于唯一标识表单。 按值呈现表单时，只有在表单重复使用时才应缓存该表单。 但是，如果表单没有重复使用且必须是唯一的，则可以避免使用使用使用AEM Forms API设置的缓存选项来缓存表单。

Forms服务还可以解析表单设计中链接内容的位置。 例如，从表单设计中引用的链接图像是相对URL。 链接的内容始终被假定为相对于表单设计位置。 因此，解析链接内容是通过将相对路径应用到绝对表单设计位置来确定其位置的问题。

您可以按值传递表单设计，而不是按引用传递表单设计。 在动态创建表单设计时，按值传递表单设计非常有效；也就是说，当客户端应用程序在运行时生成创建表单设计的XML时。 在这种情况下，表单设计不会存储在物理存储库中，因为它存储在内存中。 在运行时动态创建表单设计并按值传递该设计时，您可以缓存该表单并提高Forms服务的性能。

**按值传递表单的限制**

按值传递表单设计时，将受到以下限制：

* 表单设计中不能包含任何相对链接的内容。 所有图像和片段必须嵌入到表单设计中，或绝对引用。
* 表单呈现后，无法执行服务器端计算。 如果表单已提交回Forms服务，则无需任何服务器端计算，即可提取并返回数据。
* 由于HTML在运行时只能使用链接的图像，因此无法生成包含嵌入图像的HTML。 这是因为Forms服务通过从引用的表单设计中检索图像来支持具有HTML的嵌入图像。 由于按值传递的表单设计没有引用位置，因此在显示HTML页面时无法提取嵌入的图像。 因此，图像引用必须是要在HTML中呈现的绝对路径。

>[!NOTE]
>
>尽管您可以按值呈现不同类型的表单(例如，HTML表单或包含使用权限的表单)，但本节将讨论渲染交互式PDF forms。

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步骤摘要 {#summary-of-steps}

要按值渲染表单，请执行以下步骤：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 引用表单设计。
1. 按值呈现表单。
1. 将表单数据流写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

在以编程方式将数据导入PDF表单客户端API之前，您必须创建数据集成服务客户端。 在创建服务客户端时，您可以定义调用服务所需的连接设置。

**引用表单设计**

按值渲染表单时，必须创建 `com.adobe.idp.Document` 包含要渲染的表单设计的对象。 您可以引用现有的XDP文件，也可以在运行时动态创建表单设计并填充 `com.adobe.idp.Document` 数据。

>[!NOTE]
>
>此部分和相应的快速启动会引用现有的XDP文件。

**按值呈现表单**

要按值呈现表单，请传递 `com.adobe.idp.Document` 将表单设计包含到呈现方法的实例 `inDataDoc` 参数(可以是 `FormsServiceClient` 对象的呈现方法，如 `renderPDFForm`, `(Deprecated) renderHTMLForm`，等等)。 此参数值通常为与表单合并的数据保留。 同样，将空字符串值传递到 `formQuery` 参数。 通常，此参数需要一个字符串值来指定表单设计的名称。

>[!NOTE]
>
>如果要在表单中显示数据，必须在 `xfa:datasets` 元素。 有关XFA架构的信息，请转到 [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**将表单数据流写入客户端Web浏览器**

当Forms服务按值呈现表单时，它会返回一个必须写入客户端Web浏览器的表单数据流。 写入客户端Web浏览器时，用户可以看到该表单。

**另请参阅**

[使用Java API按值呈现表单](#render-a-form-by-value-using-the-java-api)

[使用Web服务API按值呈现表单](#render-a-form-by-value-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API按值呈现表单 {#render-a-form-by-value-using-the-java-api}

使用Forms API(Java)按值呈现表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用表单设计

   * 创建 `java.io.FileInputStream` 表示要使用其构造函数呈现的表单设计的对象，并传递指定XDP文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 按值呈现表单

   调用 `FormsServiceClient` 对象 `renderPDFForm` 方法并传递以下值：

   * 空字符串值。 （通常，此参数需要一个指定表单设计名称的字符串值。）
   * A `com.adobe.idp.Document` 包含表单设计的对象。 通常，此参数值是为与表单合并的数据保留的。
   * A `PDFFormRenderSpec` 用于存储运行时选项的对象。 这是一个可选参数，您可以指定 `null` 如果您不想指定运行时选项，请执行以下操作：
   * A `URLSpec` 包含Forms服务所需URI值的对象。
   * A `java.util.HashMap` 用于存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含可写入客户端web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `com.adobe.idp.Document` 对象 `FormsResult` 对象s `getOutputContent` 方法。
   * 获取的内容类型 `com.adobe.idp.Document` 通过调用对象 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用 `setContentType` 方法和传递 `com.adobe.idp.Document` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用将表单数据流写入客户端web浏览器的对象 `javax.servlet.http.HttpServletResponse` 对象 `getOutputStream` 方法。
   * 创建 `java.io.InputStream` 对象 `com.adobe.idp.Document` 对象 `getInputStream` 方法。
   * 创建字节数组并分配 `InputStream` 对象。 调用 `InputStream` 对象 `available` 获取 `InputStream` 对象。
   * 通过调用 `InputStream` 对象 `read`方法并将字节数组作为参数进行传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象 `write` 将表单数据流发送到客户端web浏览器的方法。 将字节数组传递到 `write` 方法。

**另请参阅**

[按值呈现Forms](/help/forms/developing/rendering-forms.md)

[快速入门（SOAP模式）：使用Java API按值呈现](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API按值呈现表单 {#render-a-form-by-value-using-the-web-service-api}

使用Forms API（Web服务）按值呈现表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms客户端API对象

   创建 `FormsService` 对象，并设置身份验证值。

1. 引用表单设计

   * 创建 `java.io.FileInputStream` 对象。 传递指定XDP文件位置的字符串值。
   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储使用密码加密的PDF文档。
   * 创建用于存储 `java.io.FileInputStream` 对象。 您可以通过获取 `java.io.FileInputStream` 对象的大小使用其 `available` 方法。
   * 通过调用 `java.io.FileInputStream` 对象 `read` 方法和传递字节数组。
   * 填充 `BLOB` 通过调用对象 `setBinaryData` 方法和传递字节数组。

1. 按值呈现表单

   调用 `FormsService` 对象 `renderPDFForm` 方法并传递以下值：

   * 空字符串值。 （通常，此参数需要一个指定表单设计名称的字符串值。）
   * A `BLOB` 包含表单设计的对象。 通常，此参数值是为与表单合并的数据保留的。
   * A `PDFFormRenderSpec` 用于存储运行时选项的对象。 这是一个可选参数，您可以指定 `null` 如果您不想指定运行时选项，请执行以下操作：
   * A `URLSpec` 包含Forms服务所需URI值的对象。
   * A `java.util.HashMap` 用于存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的对象。 用于存储呈现的PDF表单。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的对象。 （此参数以表单形式存储页数。）
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的对象。 （此参数存储区域设置值。）
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作结果的对象。

   的 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值传递的对象，表单数据流必须写入客户端web浏览器。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象 `value` 数据成员。
   * 创建 `BLOB` 通过调用包含表单数据的对象 `FormsResult` 对象 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 通过调用对象 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用 `setContentType` 方法和传递 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用将表单数据流写入客户端web浏览器的对象 `javax.servlet.http.HttpServletResponse` 对象 `getOutputStream` 方法。
   * 创建一个字节数组，并通过调用 `BLOB` 对象 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象 `write` 将表单数据流发送到客户端web浏览器的方法。 将字节数组传递到 `write` 方法。

**另请参阅**

[按值呈现Forms](#rendering-forms-by-value)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
