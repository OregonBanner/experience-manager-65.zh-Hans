---
title: 渲染启用了权限的表单
seo-title: 渲染启用了权限的表单
description: 'null'
seo-description: 'null'
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 渲染启用了权限的表单 {#rendering-rights-enabled-forms}

Forms服务可以呈现对其应用了使用权限的表单。 使用权限与Acrobat默认提供但Adobe reader不提供的功能有关，例如向表单添加注释或填写表单字段并保存表单的功能。 对其应用了使用权限的表单称为启用权限的表单。 在Adobe Reader中打开启用了权限的表单的用户可以执行为该表单启用的操作。

要对表单应用使用权限，Acrobat Reader DC扩展服务必须是AEM表单安装的一部分。 此外，您必须拥有有效的凭据，才能对PDF文档应用使用权限。 也就是说，必须正确配置Acrobat Reader DC扩展服务，才能渲染启用了权限的表单。 (请参 [阅关于Acrobat Reader DC扩展服务](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)。)

>[!NOTE]
>
>要渲染包含使用权限的表单，必须使用XDP文件作为输入，而不是PDF文件。 如果您使用PDF文件作为输入，表单仍会呈现；但是，它不是启用权限的表单。

>[!NOTE]
>
>在指定以下使用权限时，不能用XML数据预填充表单： `enableComments`、 `enableCommentsOnline`、 `enableEmbeddedFiles`或 `enableDigitalSignatures`。 (请参阅 [使用可流式布局预填充表单](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要渲染启用了权限的表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 设置使用权限运行时选项。
1. 渲染启用了权限的表单。
1. 将启用权限的表单写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式执行Forms服务客户端API操作之前，必须先创建Forms服务客户端。

**设置使用权限运行时选项**

您必须设置使用权限运行时选项才能渲染启用了权限的表单。 您还必须指定用于将使用权限应用于表单的凭证别名。 在指定别名值后，您指定每个用于表单的权限。

**渲染启用了权限的表单**

要渲染启用了权限的表单，请使用与渲染没有使用权限的表单相同的应用程序逻辑。 唯一的区别是必须确保应用程序逻辑中包含使用权限运行时选项。

>[!NOTE]
>
>使用Forms web服务API渲染具有权限的表单时，无法将文件附加到表单。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现一个启用权限的表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器。 一旦写入客户端Web浏览器，用户就可以看到表单。 在Adobe reader中查看已启用权限的表单的用户可以执行为该表单启用的操作。

**另请参阅**

[使用Java API渲染支持权限的表单](#render-rights-enabled-forms-using-the-java-api)

[使用Web服务API渲染支持权限的表单](#render-rights-enabled-forms-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF表单](/help/forms/developing/rendering-interactive-pdf-forms.md)

[创建呈现表单的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API渲染支持权限的表单 {#render-rights-enabled-forms-using-the-java-api}

使用Forms API(Java)渲染支持权限的表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 设置使用权限运行时选项

   * 使用对 `ReaderExtensionSpec` 象的构造函数创建对象。
   * 通过调用对象的方法指定凭据的 `ReaderExtensionSpec` 别名，并 `setReCredentialAlias` 指定表示别名值的字符串值。
   * 通过调用属于该对象的相应方法来设置每个使用 `ReaderExtensionSpec` 权限。 但是，只有在引用的凭证允许您设置使用权限时，才可以设置此权限。 也就是说，如果凭证不允许您设置使用权限，则不能设置此权限。 例如。 要设置使用户能够填写表单字段并保存表单的使用权限，请调用对 `ReaderExtensionSpec` 象的方法并 `setReFillIn` 传递 `true`。
   >[!NOTE]
   >
   >无需调用对象 `ReaderExtensionSpec` 的方 `setReCredentialPassword` 法。 Forms服务不使用此方法。

1. 渲染启用了权限的表单

   调用对 `FormsServiceClient` 象的方 `renderPDFFormWithUsageRights` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是表单应用程序的一部分，请确保指定完整路径，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象。 如果不想合并数据，请传递空对 `com.adobe.idp.Document` 象。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。
   * 存储 `ReaderExtensionSpec` 使用权限运行时选项的对象。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   该方 `renderPDFFormWithUsageRights` 法返回一个对 `FormsResult` 象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
   * 通过调用对象的方 `com.adobe.idp.Document` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `com.adobe.idp.Document` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
   * 通过调用对象的方法并将字节数组作为参数传递，创 `InputStream` 建一个用 `read` 表单数据流填充它的字节数组。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[快速入门（SOAP模式）:使用Java API渲染支持权限的表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API渲染支持权限的表单 {#render-rights-enabled-forms-using-the-web-service-api}

使用Forms API（Web服务）渲染支持权限的表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建对 `FormsService` 象并设置身份验证值。

1. 设置使用权限运行时选项

   * 使用对 `ReaderExtensionSpec` 象的构造函数创建对象。
   * 通过调用对象的方法指定凭据的 `ReaderExtensionSpec` 别名，并 `setReCredentialAlias` 指定表示别名值的字符串值。
   * 通过调用属于该对象的相应方法来设置每个使用 `ReaderExtensionSpec` 权限。 但是，只有在引用的凭证允许您设置使用权限时，才可以设置此权限。 也就是说，如果凭证不允许您设置使用权限，则不能设置此权限。 要设置使用户能够填写表单字段并保存表单的使用权限，请调用对 `ReaderExtensionSpec` 象的方法并 `setReFillIn` 传递 `true`。

1. 渲染启用了权限的表单

   调用对 `FormsService` 象的方 `renderPDFFormWithUsageRights` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是表单应用程序的一部分，请确保指定完整路径，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包含 `BLOB` 要与表单合并的数据的对象。 如果不希望将数据与表单合并，则必须传 `BLOB` 递基于空XML数据源的对象。 不能传递 `BLOB` 为null的对象；否则，将引发异常。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。
   * 存储 `ReaderExtensionSpec` 使用权限运行时选项的对象。
   * 包 `URLSpec` 含Forms服务所需的URI值的对象。
   该方 `renderPDFFormWithUsageRights` 法返回一个对 `FormsResult` 象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调 `BLOB` 用对象的方法创建包含表 `FormsResult` 单数据的对 `getOutputContent` 象。
   * 通过调用对象的方 `BLOB` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `BLOB` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 创建一个字节数组，并通过调用对象的 `BLOB` 方法填充该 `getBinaryData` 数组。 此任务将对象的内 `FormsResult` 容分配给字节数组。
   * 调用对 `javax.servlet.http.HttpServletResponse` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[渲染启用了权限的表单](#rendering-rights-enabled-forms)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
