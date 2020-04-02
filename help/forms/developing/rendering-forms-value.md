---
title: 按值呈现表单
seo-title: 按值呈现表单
description: 'null'
seo-description: 'null'
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: 66bfd6870b4c09dc2ca1b66058e0b9e040a71507

---


# 按值呈现表单 {#rendering-forms-by-value}

通常，在Designer中创建的表单设计会通过引用Forms服务来传递。 表单设计可能很大，因此，通过引用传递表单设计会更加有效，从而避免必须按值调整表单设计字节。 Forms服务还可以缓存表单设计，以便缓存表单设计时，它不必持续读取表单设计。

如果表单设计包含UUID属性，则会缓存该属性。 UUID值对于所有表单设计都是唯一的，用于唯一标识表单。 按值呈现表单时，仅应在重复使用表单时缓存表单。 但是，如果表单不重复使用且必须是唯一的，则可以避免使用使用使用AEM Forms API设置的缓存选项来缓存表单。

表单服务还可以解析在表单设计中链接内容的位置。 例如，从表单设计中引用的链接图像是相对URL。 链接的内容始终假定为相对于表单设计位置。 因此，解析链接内容是通过将相对路径应用到绝对表单设计位置来确定其位置的问题。

您可以按值传递表单设计，而不是按引用传递表单设计。 在动态创建表单设计时，按值传递表单设计是有效的；即，当客户端应用程序在运行时生成创建表单设计的XML时。 在这种情况下，表单设计不会存储在物理存储库中，因为它存储在内存中。 在运行时动态创建表单设计并按值传递它时，您可以缓存表单并提高Forms服务的性能。

**按值传递表单的限制**

按值传递表单设计时，以下限制适用：

* 表单设计中不能包含任何相对链接的内容。 所有图像和片段必须嵌入到表单设计中或绝对引用。
* 无法在呈现表单后执行服务器端计算。 如果将表单提交回表单服务，则数据将提取并返回，而无需任何服务器端计算。
* 由于HTML在运行时只能使用链接的图像，因此无法生成包含嵌入图像的HTML。 这是因为Forms服务通过从引用的表单设计检索图像来支持嵌入的HTML图像。 由于按值传递的表单设计没有引用的位置，因此在显示HTML页面时无法提取嵌入的图像。 因此，图像引用必须是要在HTML中呈现的绝对路径。

>[!NOTE]
>
>虽然您可以按值呈现不同类型的表单（例如，包含使用权限的HTML表单或表单），但本节将讨论呈现交互式PDF表单。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要按值呈现表单，请执行以下步骤：

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 参考表单设计。
1. 按值渲染表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式将数据导入PDF表单客户端API之前，必须创建数据集成服务客户端。 创建服务客户端时，您定义调用服务所需的连接设置。

**参考表单设计**

按值呈现表单时，必须创建包含要呈 `com.adobe.idp.Document` 现的表单设计的对象。 您可以引用现有XDP文件，也可以在运行时动态创建表单设计并用该数 `com.adobe.idp.Document` 据填充表单。

>[!NOTE]
>
>此部分和相应的快速开始引用现有XDP文件。

**按值渲染表单**

要按值呈现表单，请将包含表单设计的实例传递到呈现方法的 `com.adobe.idp.Document` 参数(可以是对象的任何呈现方 `inDataDoc` 法， `FormsServiceClient``renderPDFForm``(Deprecated) renderHTMLForm`等等)。 此参数值通常为与表单合并的数据保留。 同样，将空字符串值传递给该参 `formQuery` 数。 通常，此参数需要一个指定表单设计名称的字符串值。

>[!NOTE]
>
>如果要在表单中显示数据，则必须在元素中指定数 `xfa:datasets` 据。 有关XFA体系结构的信息，请访 [问https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html)。

**将表单数据流写入客户端Web浏览器**

当Forms服务按值呈现表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器。 当写入到客户端Web浏览器时，用户可看到表单。

**另请参阅**

[使用Java API按值呈现表单](#render-a-form-by-value-using-the-java-api)

[使用Web服务API按值渲染表单](#render-a-form-by-value-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建呈现表单的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API按值呈现表单 {#render-a-form-by-value-using-the-java-api}

使用Forms API(Java)按值呈现表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 参考表单设计

   * 创建一 `java.io.FileInputStream` 个对象，该对象通过使用其构造函数并传递指定XDP文件位置的字符串值来表示要渲染的表单设计。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 按值渲染表单

   调用对 `FormsServiceClient` 象的方 `renderPDFForm` 法并传递以下值：

   * 空字符串值。 （通常情况下，此参数需要一个指定表单设计名称的字符串值。）
   * 包 `com.adobe.idp.Document` 含表单设计的对象。 通常，此参数值是为与表单合并的数据保留的。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。 这是一个可选参数，您可 `null` 以指定是否不想指定运行时选项。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   该方 `renderPDFForm` 法返回一个对 `FormsResult` 象，该对象包含可写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
   * 通过调用对象的方 `com.adobe.idp.Document` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `com.adobe.idp.Document` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
   * 创建一个字节数组并分配对象的大 `InputStream` 小。 调用对 `InputStream` 象的方 `available` 法以获取对象的大 `InputStream` 小。
   * 通过调用对象的方法并将字节数组作为参数传 `InputStream` 递，用表 `read`单数据流填充字节数组。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[按值呈现表单](/help/forms/developing/rendering-forms.md)

[快速开始（SOAP模式）:使用Java API按值呈现](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API按值渲染表单 {#render-a-form-by-value-using-the-web-service-api}

使用Forms API（Web服务）按值呈现表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建对 `FormsService` 象并设置身份验证值。

1. 参考表单设计

   * 使用对 `java.io.FileInputStream` 象的构造函数创建对象。 传递一个指定XDP文件位置的字符串值。
   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储使用密码加密的PDF文档。
   * 创建存储对象内容的字节数 `java.io.FileInputStream` 组。 您可以通过使用对象的方法获取该对象的大 `java.io.FileInputStream` 小来确定字节数组的大 `available` 小。
   * 通过调用对象的方法并传递字节数组， `java.io.FileInputStream` 用流数 `read` 据填充字节数组。
   * 通过调 `BLOB` 用对象的方法并传 `setBinaryData` 递字节数组来填充对象。

1. 按值渲染表单

   调用对 `FormsService` 象的方 `renderPDFForm` 法并传递以下值：

   * 空字符串值。 （通常情况下，此参数需要一个指定表单设计名称的字符串值。）
   * 包 `BLOB` 含表单设计的对象。 通常，此参数值是为与表单合并的数据保留的。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。 这是一个可选参数，您可 `null` 以指定是否不想指定运行时选项。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空对象。 它用于存储渲染的PDF表单。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空对象。 （此参数存储表单中的页数。）
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对象。 （此参数存储区域设置值。）
   * 将包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作结果的空对象。
   该方 `renderPDFForm` 法使用必 `com.adobe.idp.services.holders.FormsResultHolder` 须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `FormResult` 获取对象数据成员的 `com.adobe.idp.services.holders.FormsResultHolder` 值来创建 `value` 对象。
   * 通过调 `BLOB` 用对象的方法创建包含表 `FormsResult` 单数据的对 `getOutputContent` 象。
   * 通过调用对象的方 `BLOB` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `BLOB` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 创建一个字节数组，并通过调用对象的 `BLOB` 方法填充该 `getBinaryData` 数组。 此任务将对象的内 `FormsResult` 容指定给字节数组。
   * 调用对 `javax.servlet.http.HttpServletResponse` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[按值呈现表单](#rendering-forms-by-value)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
