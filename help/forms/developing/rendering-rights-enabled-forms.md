---
title: 启用渲染权限的Forms
seo-title: 启用渲染权限的Forms
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
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---


# 启用渲染权限的Forms{#rendering-rights-enabled-forms}

Forms服务可以呈现对其应用了使用权的表单。 使用权限与默认在Acrobat但在Adobe Reader不可用的功能有关，如向表单添加注释或填写表单字段并保存表单的功能。 对其应用使用权限的Forms称为启用权限的表单。 在Adobe Reader打开启用权限的表单的用户可以执行为该表单启用的操作。

要对表单应用使用权，Acrobat Reader DC扩展服务必须是AEM表单安装的一部分。 此外，您必须具有有效的凭据，才能对PDF文档应用使用权限。 也就是说，必须正确配置Acrobat Reader DC扩展服务，然后才能渲染启用权限的表单。 (请参阅[关于Acrobat Reader DC扩展服务](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)。)

>[!NOTE]
>
>要渲染包含使用权限的表单，必须使用XDP文件作为输入，而不是PDF文件。 如果您使用PDF文件作为输入，表单仍会呈现；但是，它不是启用权限的表单。

>[!NOTE]
>
>在指定以下使用权限时，不能用XML数据预填充表单：`enableComments`、`enableCommentsOnline`、`enableEmbeddedFiles`或`enableDigitalSignatures`。 (请参阅[使用可流动布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)

>[!NOTE]
>
>有关Forms服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤{#summary-of-steps}的摘要

要渲染启用权限的表单，请执行以下任务:

1. 包括项目文件。
1. 创建一个Forms客户端API对象。
1. 设置使用权限运行时选项。
1. 渲染启用权限的表单。
1. 将启用权限的表单写入客户端Web浏览器。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

在以编程方式执行Forms服务客户端API操作之前，必须创建Forms服务客户端。

**设置使用权限运行时选项**

您必须设置使用权限运行时选项才能呈现启用权限的表单。 还必须指定用于将使用权限应用于表单的凭据别名。 在指定别名值后，您可以指定每个用于表单的权限。

**渲染启用权限的表单**

要渲染启用权限的表单，请使用与渲染没有使用权限的表单相同的应用程序逻辑。 唯一的区别是必须确保应用程序逻辑中包含使用权限运行时选项。

>[!NOTE]
>
>使用FormsWeb服务API渲染启用权限的表单时，无法将文件附加到表单。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现一个启用权限的表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器。 一旦写入到客户端Web浏览器，用户就可以看到表单。 在Adobe Reader查看启用权限的表单的用户能够执行为该表单启用的操作。

**另请参阅**

[使用Java API呈现支持权限的表单](#render-rights-enabled-forms-using-the-java-api)

[使用Web服务API渲染支持权限的表单](#render-rights-enabled-forms-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[创建呈现Forms的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#render-rights-enabled-forms-using-the-java-api}呈现启用权限的表单

使用FormsAPI(Java)渲染启用权限的表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormsServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 设置使用权限运行时选项

   * 使用`ReaderExtensionSpec`对象的构造函数创建&lt;a0/>对象。
   * 通过调用`ReaderExtensionSpec`对象的`setReCredentialAlias`方法指定凭据的别名，并指定表示别名值的字符串值。
   * 通过调用属于`ReaderExtensionSpec`对象的相应方法来设置每个使用权限。 但是，只有在引用的凭据允许您设置使用权限时，才可设置此权限。 也就是说，如果凭据不允许您设置，则无法设置使用权限。 例如。 要设置允许用户填写表单字段并保存表单的使用权限，请调用`ReaderExtensionSpec`对象的`setReFillIn`方法并传递`true`。

   >[!NOTE]
   >
   >无需调用`ReaderExtensionSpec`对象的`setReCredentialPassword`方法。 Forms服务不使用此方法。

1. 渲染启用权限的表单

   调用`FormsServiceClient`对象的`renderPDFFormWithUsageRights`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递一个空`com.adobe.idp.Document`对象。
   * 存储运行时选项的`PDFFormRenderSpec`对象。
   * 存储使用权限运行时选项的`ReaderExtensionSpec`对象。
   * 一个`URLSpec`对象，它包含Forms服务所需的URI值。

   `renderPDFFormWithUsageRights`方法返回一个`FormsResult`对象，该对象包含一个必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象“s `getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数进行传递，创建一个用表单数据流填充它的字节数组。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[快速开始（SOAP模式）:使用Java API渲染支持权限的表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#render-rights-enabled-forms-using-the-web-service-api}呈现启用权限的表单

使用FormsAPI（Web服务）渲染启用权限的表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms客户端API对象

   创建`FormsService`对象并设置身份验证值。

1. 设置使用权限运行时选项

   * 使用`ReaderExtensionSpec`对象的构造函数创建&lt;a0/>对象。
   * 通过调用`ReaderExtensionSpec`对象的`setReCredentialAlias`方法指定凭据的别名，并指定表示别名值的字符串值。
   * 通过调用属于`ReaderExtensionSpec`对象的相应方法来设置每个使用权限。 但是，只有在引用的凭据允许您设置使用权限时，才可设置此权限。 也就是说，如果凭据不允许您设置，则无法设置使用权限。 要设置允许用户填写表单字段并保存表单的使用权限，请调用`ReaderExtensionSpec`对象的`setReFillIn`方法并传递`true`。

1. 渲染启用权限的表单

   调用`FormsService`对象的`renderPDFFormWithUsageRights`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想将数据与表单合并，则必须传递一个基于空XML数据源的`BLOB`对象。 不能传递`BLOB`对象为null;否则，将引发异常。
   * 存储运行时选项的`PDFFormRenderSpec`对象。
   * 存储使用权限运行时选项的`ReaderExtensionSpec`对象。
   * 一个`URLSpec`对象，它包含Forms服务所需的URI值。

   `renderPDFFormWithUsageRights`方法返回一个`FormsResult`对象，该对象包含一个必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 通过调用`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用`setContentType`方法并传递`BLOB`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充它。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[启用渲染权限的Forms](#rendering-rights-enabled-forms)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
