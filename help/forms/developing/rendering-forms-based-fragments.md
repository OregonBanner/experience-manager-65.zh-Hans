---
title: 根据片段渲染Forms
seo-title: Rendering Forms Based on Fragments
description: 使用Forms服务渲染基于使用Designer创建的片段的表单。
seo-description: Use the Forms service to render forms that are based on fragments created using Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 0%

---

# 根据片段渲染Forms {#rendering-forms-based-on-fragments}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

## 根据片段渲染Forms {#rendering-forms-based-on-fragments-inner}

Forms服务可以渲染基于您使用Designer创建的片段的表单。 A *片段* 是表单的可重用部分，并另存为可插入到多个表单设计中的单独XDP文件。 例如，片段可以包含地址块或合法文本。

使用片段可简化并加速大量表单的创建和维护。 创建新表单时，插入对所需片段的引用，片段将显示在表单中。 片段引用包含指向物理XDP文件的子表单。 有关基于片段创建表单设计的信息，请参阅 [Forms设计器](https://www.adobe.com/go/learn_aemforms_designer_63)

一个片段可以包含多个包在选择子表单集中的子表单。 选择子表单集根据来自数据连接的数据流控制子表单的显示。 可使用条件语句确定集合中的哪个子表单出现在交付的表单中。 例如，集合中的每个子表单可以包含特定地理位置的信息，并且显示的子表单可以根据用户的位置确定。

A *脚本片段* 包含可重复使用的JavaScript函数或与任何特定对象（如日期解析器或Web服务调用）分开存储的值。 这些片段包括一个脚本对象，该对象在层次结构面板中显示为变量的子项。 无法从作为其他对象属性的脚本（如验证、计算或初始化等事件脚本）创建片段。

使用片段的优点如下：

* **内容重用**：您可以使用片段在多个表单设计中重用内容。 当您需要以多个表单使用某些相同的内容时，使用片段比复制或重新创建内容更快、更简单。 使用片段还可以确保表单设计中经常使用的部分在所有引用表单中具有一致的内容和外观。
* **全局更新**：您可以使用片段仅在一个文件中对多个表单进行一次全局更改。 您可以更改片段中的内容、脚本对象、数据绑定、布局或样式，并且引用片段的所有XDP表单都将反映这些更改。
* 例如，许多表单中的一个通用元素可能是一个地址块，其中包含国家/地区的下拉列表对象。 如果需要更新下拉列表对象的值，则必须打开多个表单进行更改。 如果您在片段中包含地址块，则只需打开一个片段文件即可进行更改。
* 要更新PDF表单中的片段，必须在设计器中重新保存表单。
* **共享表单创建**：您可以使用片段在多种资源中共享表单的创建。 具有脚本或Designer其他高级功能专业知识的表单开发人员可以开发和共享利用脚本和动态属性的片段。 表单设计人员可以使用这些片段来布局表单设计，并确保表单的所有部分在多人设计的多个表单中都具有一致的外观和功能。

### 组装使用片段组装的造型设计 {#assembling-a-form-design-assembled-using-fragments}

您可以组合表单设计，以基于多个片段传递到Forms服务。 要组装多个片段，请使用Assembler服务。 要查看使用Assemble服务创建其他Forms服务（Output服务）使用的表单设计的示例，请参阅 [使用片段创建PDF文档](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). 您可以使用Forms服务执行相同的工作流，而不是使用输出服务。

使用Assembler服务时，传递使用片段装配的表单设计。 创建的表单设计未引用其他片段。 相反，本主题讨论将引用其他片段的表单设计传递到Forms服务。 然而，Assembler没有组装表单设计。 它是在Designer中创建的。

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关创建基于片段渲染表单的基于Web的应用程序的信息，请参阅 [创建渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md).

### 步骤摘要 {#summary-of-steps}

要呈现基于片段的表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 指定URI值。
1. 渲染表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建Forms服务客户端，然后才能以编程方式执行Forms服务客户端API操作。

**指定URI值**

要成功渲染基于片段的表单，您必须确保Forms服务能够找到表单和表单设计引用的片段（XDP文件）。 例如，假设表单名为PO.xdp，并且此表单使用名为FooterUS.xdp和FooterCanada.xdp的两个片段。 在这种情况下，Forms服务必须能够找到所有三个XDP文件。

您可以将表单放置在一个位置，将片段放置在另一个位置，来组织表单及其片段，也可以将所有XDP文件放置在同一位置。 在本节中，假设所有XDP文件都位于AEM Forms存储库中。 有关将XDP文件放入AEM Forms存储库的信息，请参阅 [写入资源](/help/forms/developing/aem-forms-repository.md#writing-resources).

呈现基于片段的表单时，必须仅引用表单本身，而不引用片段。 例如，您必须引用PO.xdp，而不是FooterUS.xdp或FooterCanada.xdp。 确保将片段放置在Forms服务可以找到它们的位置。

**渲染表单**

基于片段的表单可以按与非片段表单相同的方式呈现。 也就是说，您可以将表单渲染为PDF、HTML或表单参考线（已弃用）。 本节中的示例将基于片段的表单渲染为交互式PDF表单。 (请参阅 [渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**将表单数据流写入客户端Web浏览器**

Forms服务渲染表单时，会返回一个您必须写入客户端Web浏览器的表单数据流。 在写入客户端Web浏览器时，该表单对用户可见。

**另请参阅**

[使用Java API根据片段渲染表单](#render-forms-based-on-fragments-using-the-java-api)

[使用Web服务API根据片段渲染表单](#render-forms-based-on-fragments-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[创建渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API根据片段渲染表单 {#render-forms-based-on-fragments-using-the-java-api}

使用Forms API (Java)呈现基于片段的表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 指定URI值

   * 创建 `URLSpec` 使用其构造函数存储URI值的对象。
   * 调用 `URLSpec` 对象的 `setApplicationWebRoot` 方法，并传递一个表示应用程序的Web根目录的字符串值。
   * 调用 `URLSpec` 对象的 `setContentRootURI` 方法，并传递一个指定内容根URI值的字符串值。 确保表单设计和片段位于内容根URI中。 如果不存在，则Forms服务会引发异常。 要引用存储库，请指定 `repository://`.
   * 调用 `URLSpec` 对象的 `setTargetURL` 方法，并传递一个字符串值，该值指定将表单数据发布到的目标URL值。 如果您在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL，以执行计算。

1. 渲染表单

   调用 `FormsServiceClient` 对象的 `renderPDFForm` 方法，并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递一个空值 `com.adobe.idp.Document` 对象。
   * A `PDFFormRenderSpec` 存储运行时选项的对象。
   * A `URLSpec` 包含Forms服务根据片段呈现表单所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   此 `renderPDFForm` 方法返回 `FormsResult` 包含必须写入客户端Web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `com.adobe.idp.Document` 对象 `FormsResult` 对象 `getOutputContent` 方法。
   * 获取的内容类型 `com.adobe.idp.Document` 对象，调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用其 `setContentType` 方法和传递的内容类型 `com.adobe.idp.Document` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建 `java.io.InputStream` 对象 `com.adobe.idp.Document` 对象的 `getInputStream` 方法。
   * 创建一个字节数组，通过调用 `InputStream` 对象的 `read`方法，并将字节数组作为参数传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象的 `write` 方法将表单数据流发送到客户端Web浏览器。 将字节数组传递到 `write` 方法。

**另请参阅**

[根据片段渲染Forms](#rendering-forms-based-on-fragments)

[快速入门（SOAP模式）：使用Java API基于片段呈现表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API根据片段渲染表单 {#render-forms-based-on-fragments-using-the-web-service-api}

使用Forms API（Web服务）根据片段渲染表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建 `FormsService` 对象并设置身份验证值。

1. 指定URI值

   * 创建 `URLSpec` 使用其构造函数存储URI值的对象。
   * 调用 `URLSpec` 对象的 `setApplicationWebRoot` 方法，并传递一个表示应用程序的Web根目录的字符串值。
   * 调用 `URLSpec` 对象的 `setContentRootURI` 方法，并传递一个指定内容根URI值的字符串值。 确保表单设计位于内容根URI中。 如果不存在，则Forms服务会引发异常。 要引用存储库，请指定 `repository://`.
   * 调用 `URLSpec` 对象的 `setTargetURL` 方法，并传递一个字符串值，该值指定将表单数据发布到的目标URL值。 如果您在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL，以执行计算。

1. 渲染表单

   调用 `FormsService` 对象的 `renderPDFForm` 方法，并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递 `null`.
   * A `PDFFormRenderSpec` 存储运行时选项的对象。 请注意，如果输入文档是PDFPDF，则无法设置标记文档选项。 如果输入文件是XDP文件，则可以设置标记的PDF选项。
   * A `URLSpec` 包含Forms服务所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的对象。 此参数用于存储渲染的表单。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的对象。 此参数将存储表单中的页数。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的对象。 此参数将存储区域设置值。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 将包含此操作结果的对象。

   此 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值（具有必须写入客户端Web浏览器的表单数据流）传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象的 `value` 数据成员。
   * 创建 `BLOB` 通过调用 `FormsResult` 对象的 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 对象，调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用其 `setContentType` 方法和传递的内容类型 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建一个字节数组，并通过调用 `BLOB` 对象的 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象的 `write` 方法将表单数据流发送到客户端Web浏览器。 将字节数组传递到 `write` 方法。

**另请参阅**

[根据片段渲染Forms](#rendering-forms-based-on-fragments)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
