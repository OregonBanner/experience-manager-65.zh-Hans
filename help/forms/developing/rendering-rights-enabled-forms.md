---
title: 渲染启用权限的Forms
description: 使用Forms服务呈现应用了使用权限的表单。 您可以使用Java API和Web服务API呈现启用权限的表单。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 0%

---

# 渲染启用权限的Forms {#rendering-rights-enabled-forms}

Forms服务可以呈现已应用了使用权限的表单。 使用权限与Acrobat中默认提供的功能有关，但在Adobe Reader中不可用，例如向表单添加注释或填写表单字段并保存表单的功能。 对其应用了使用权限的Forms称为启用权限的表单。 在Adobe Reader中打开启用了权限的表单的用户可以执行为该表单启用的操作。

要对表单应用使用权限，AEM表单安装中必须包含Acrobat Reader DC扩展服务。 此外，您必须具有有效的凭据，以便能够对PDF文档应用使用权限。 也就是说，在渲染启用权限的表单之前，必须正确配置Acrobat Reader DC扩展服务。 (请参阅 [关于Acrobat Reader DC扩展服务](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>要呈现包含使用权限的表单，必须使用XDP文件作为输入，而非PDF文件。 如果您使用PDF文件作为输入，则表单仍会呈现；但是，它不会是启用权限的表单。

>[!NOTE]
>
>指定以下使用权限时，不能使用XML数据预填充表单： `enableComments`， `enableCommentsOnline`， `enableEmbeddedFiles`，或 `enableDigitalSignatures`. (请参阅 [使用可流布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步骤摘要 {#summary-of-steps}

要呈现启用权限的表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 设置使用权限运行时选项。
1. 呈现启用权限的表单。
1. 将启用权限的表单写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建Forms服务客户端，然后才能以编程方式执行Forms服务客户端API操作。

**设置使用权限运行时选项**

设置使用权限运行时选项以呈现启用权限的表单。 指定用于向表单应用使用权限的凭据的别名。 指定别名值后，指定应用于表单的每个使用权限。

**呈现启用权限的表单**

要呈现启用了权限的表单，请使用与呈现没有使用权限的表单相同的应用程序逻辑。 唯一的区别是，必须确保应用程序逻辑中包含使用权限运行时选项。

>[!NOTE]
>
>使用Forms Web服务API呈现启用权限的表单时，无法将文件附加到表单。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现启用权限的表单时，它会返回一个您必须写入客户端Web浏览器的表单数据流。 将表单写入客户端Web浏览器后，该表单对用户可见。 查看Adobe Reader中启用了权限的表单的用户能够执行为该表单启用的操作。

**另请参阅**

[使用Java API渲染启用权限的表单](#render-rights-enabled-forms-using-the-java-api)

[使用Web服务API呈现启用权限的表单](#render-rights-enabled-forms-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API渲染启用权限的表单 {#render-rights-enabled-forms-using-the-java-api}

使用Forms API (Java)呈现启用权限的表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 设置使用权限运行时选项

   * 创建 `ReaderExtensionSpec` 对象。
   * 通过调用 `ReaderExtensionSpec` 对象的 `setReCredentialAlias` 方法，并指定表示别名值的字符串值。
   * 通过调用属于 `ReaderExtensionSpec` 对象。 但是，只有引用凭据允许您设置使用权限，您才能设置使用权限。 也就是说，如果凭据不允许设置使用权限，则无法设置该权限。 例如。 要设置使用户能够填写表单字段并保存表单的使用权限，请调用 `ReaderExtensionSpec` 对象的 `setReFillIn` 方法和路径 `true`.

   >[!NOTE]
   >
   >无需调用 `ReaderExtensionSpec` 对象的 `setReCredentialPassword` 方法。 Forms服务不使用此方法。

1. 呈现启用权限的表单

   调用 `FormsServiceClient` 对象的 `renderPDFFormWithUsageRights` 方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保您指定完整的路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递一个空值 `com.adobe.idp.Document` 对象。
   * A `PDFFormRenderSpec` 存储运行时选项的对象。
   * A `ReaderExtensionSpec` 存储使用权限运行时选项的对象。
   * A `URLSpec` 包含Forms服务所需的URI值的对象。

   此 `renderPDFFormWithUsageRights` 方法返回 `FormsResult` 包含必须写入客户端Web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `com.adobe.idp.Document` 对象，方法是调用 `FormsResult` 对象 `getOutputContent` 方法。
   * 获取的内容类型 `com.adobe.idp.Document` 对象(通过调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 通过调用对象的内容类型 `setContentType` 方法和传递的内容类型 `com.adobe.idp.Document` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建 `java.io.InputStream` 对象，方法是调用 `com.adobe.idp.Document` 对象的 `getInputStream` 方法。
   * 创建一个字节数组，通过调用 `InputStream` 对象的 `read` 方法并将字节数组作为参数传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象的 `write` 将表单数据流发送到客户端Web浏览器的方法。 将字节数组传递给 `write` 方法。

**另请参阅**

[快速入门（SOAP模式）：使用Java API呈现启用权限的表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API呈现启用权限的表单 {#render-rights-enabled-forms-using-the-web-service-api}

使用Forms API（Web服务）呈现启用权限的表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建 `FormsService` 对象并设置身份验证值。

1. 设置使用权限运行时选项

   * 创建 `ReaderExtensionSpec` 对象。
   * 通过调用 `ReaderExtensionSpec` 对象的 `setReCredentialAlias` 方法，并指定表示别名值的字符串值。
   * 通过调用属于 `ReaderExtensionSpec` 对象。 但是，只有引用凭据允许您设置使用权限，您才能设置使用权限。 也就是说，如果凭据不允许设置使用权限，则无法设置该权限。 要设置使用户能够填写表单字段并保存表单的使用权限，请调用 `ReaderExtensionSpec` 对象的 `setReFillIn` 方法和路径 `true`.

1. 呈现启用权限的表单

   调用 `FormsService` 对象的 `renderPDFFormWithUsageRights` 方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保您指定完整的路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要与表单合并的数据的对象。 如果不想将数据与表单合并，则必须传递 `BLOB` 基于空XML数据源的对象。 您无法传递 `BLOB` 空的对象；否则，将引发异常。
   * A `PDFFormRenderSpec` 存储运行时选项的对象。
   * A `ReaderExtensionSpec` 存储使用权限运行时选项的对象。
   * A `URLSpec` 包含Forms服务所需的URI值的对象。

   此 `renderPDFFormWithUsageRights` 方法返回 `FormsResult` 包含必须写入客户端Web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `BLOB` 通过调用 `FormsResult` 对象的 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 对象(通过调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 通过调用对象的内容类型 `setContentType` 方法和传递的内容类型 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建字节数组，并通过调用 `BLOB` 对象的 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象的 `write` 将表单数据流发送到客户端Web浏览器的方法。 将字节数组传递给 `write` 方法。

**另请参阅**

[渲染启用权限的Forms](#rendering-rights-enabled-forms)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
