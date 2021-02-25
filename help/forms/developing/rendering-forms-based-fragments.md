---
title: 渲染基于片段的Forms
seo-title: 渲染基于片段的Forms
description: 使用Forms服务渲染基于使用Designer创建的片段的表单。
seo-description: 使用Forms服务渲染基于使用Designer创建的片段的表单。
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '2229'
ht-degree: 0%

---


# 基于片段渲染Forms{#rendering-forms-based-on-fragments}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 基于片段渲染Forms{#rendering-forms-based-on-fragments-inner}

Forms服务可以渲染基于您使用Designer创建的片段的表单。 *fragment*&#x200B;是表单的可重用部分，将其保存为可插入到多个表单设计中的单独XDP文件。 例如，片段可以包括地址块或合法文本。

使用片段可简化和加快大量表单的创建和维护。 创建新表单时，您插入对所需片段的引用，该片段将显示在表单中。 片段引用包含指向物理XDP文件的子表单。 有关创建基于片段的表单设计的信息，请参阅[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

片段可以包括多个子表单，这些子表单包装在所选子表单集中。 选择子表单集基于来自数据连接的数据流来控制子表单的显示。 您使用条件语句确定集合中显示的子表单在已提交表单中。 例如，集合中的每个子表单可以包括特定地理位置的信息，并且所显示的子表单可以基于用户的位置来确定。

*脚本片段*&#x200B;包含可重用的JavaScript函数或值，这些函数或值与任何特定对象（如日期分析器或Web服务调用）分开存储。 这些片段包括单个脚本对象，该对象在“层次结构”调板中显示为变量的子对象。 不能从其他对象(如验证、计算或初始化等事件脚本)的属性脚本创建片段。

以下是使用片段的优势：

* **内容重用**:您可以使用片段在多个表单设计中重复使用内容。当您需要在多个表单中使用某些相同的内容时，使用片段比复制或重新创建内容更快、更简单。 使用片段还可确保表单设计中经常使用的部分在所有引用表单中具有一致的内容和外观。
* **全局更新**:您只能使用片段对一个文件中的多个表单进行一次全局更改。您可以更改片段中的内容、脚本对象、数据绑定、布局或样式，引用片段的所有XDP表单都将反映更改。
* 例如，跨多种形式的公用元素可能是一个地址块，其中包含国家/地区的下拉列表对象。 如果需要更新下拉式列表对象的值，则必须打开多个表单才能进行更改。 如果将地址块包含在片段中，则只需打开一个片段文件即可进行更改。
* 要更新PDF表单中的片段，您必须在Designer中重新保存表单。
* **共享表单创建**:您可以使用片段在多个资源之间共享表单的创建。具备脚本或其他高级功能的表单开发人员可以开发和共享利用脚本和动态属性的片段。 表单设计人员可以使用这些片段对表单设计进行布局，并确保表单的所有部分在由多人设计的多个表单上具有一致的外观和功能。

### 使用片段{#assembling-a-form-design-assembled-using-fragments}组装表单设计

您可以组合一个表单设计，以基于多个片段传递到Forms服务。 要组合多个片段，请使用Assembler服务。 要查看使用Assemble服务创建供其他Forms服务（Output服务）使用的表单设计的示例，请参阅[使用片段创建PDF文档](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)。 您可以使用Forms服务执行相同的工作流，而不是使用输出服务。

使用Assembler服务时，您正在传递使用片段组合的表单设计。 创建的表单设计不引用其他片段。 与此相反，本主题讨论如何传递引用其他片段到Forms服务的表单设计。 但是，表单设计不是由Assembler装配的。 它是在Designer中创建的。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅[AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)的服务参考。

>[!NOTE]
>
>有关创建基于Web的应用程序以根据片段呈现表单的信息，请参阅[创建呈现Forms的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)。

### 步骤{#summary-of-steps}的摘要

要渲染基于片段的表单，请执行以下任务:

1. 包括项目文件。
1. 创建Forms Client API对象。
1. 指定URI值。
1. 渲染表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Forms Client API对象**

在以编程方式执行Forms服务客户端API操作之前，必须创建Forms服务客户端。

**指定URI值**

要成功呈现基于片段的表单，必须确保Forms服务可以找到表单设计引用的表单和片段（XDP文件）。 例如，假定表单名为PO.xdp，并且此表单使用两个名为FooterUS.xdp和FooterCanada.xdp的片段。 在这种情况下，Forms服务必须能够找到所有三个XDP文件。

您可以将表单放在一个位置，将片段放在另一个位置，从而组织表单及其片段，也可以将所有XDP文件放在同一位置。 为本节的目的，假定所有XDP文件都位于AEM Forms存储库中。 有关将XDP文件放入AEM Forms存储库的信息，请参阅[编写资源](/help/forms/developing/aem-forms-repository.md#writing-resources)。

在基于片段呈现表单时，您必须只引用表单本身，而不引用片段。 例如，必须引用PO.xdp，而不是FooterUS.xdp或FooterCanada.xdp。 请确保将片段放在Forms服务可以找到它们的位置。

**渲染表单**

基于片段的表单可以以与非碎片表单相同的方式呈现。 也就是说，您可以以PDF、HTML或表单参考线（已弃用）形式呈现表单。 本节中的示例将基于片段的表单渲染为交互式PDF表单。 (请参阅[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)。)

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现表单时，它返回一个必须写入客户端Web浏览器的表单数据流。 写入到客户端Web浏览器时，用户可以看到表单。

**另请参阅**

[使用Java API根据片段渲染表单](#render-forms-based-on-fragments-using-the-java-api)

[使用Web服务API根据片段渲染表单](#render-forms-based-on-fragments-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[创建渲染Forms的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#render-forms-based-on-fragments-using-the-java-api}根据片段渲染表单

使用Forms API(Java)渲染基于片段的表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Client API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormsServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 指定URI值

   * 创建一个`URLSpec`对象，该对象使用其构造函数存储URI值。
   * 调用`URLSpec`对象的`setApplicationWebRoot`方法并传递一个字符串值，该值表示应用程序的Web根目录。
   * 调用`URLSpec`对象的`setContentRootURI`方法并传递一个指定内容根URI值的字符串值。 确保表单设计和片段位于内容根URI中。 否则，Forms服务将引发异常。 要引用存储库，请指定`repository://`。
   * 调用`URLSpec`对象的`setTargetURL`方法并传递一个字符串值，该字符串值指定将表单目标发布到的位置。 如果在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL以执行计算。

1. 渲染表单

   调用`FormsServiceClient`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递空`com.adobe.idp.Document`对象。
   * 存储运行时选项的`PDFFormRenderSpec`对象。
   * 一个`URLSpec`对象，其中包含Forms服务根据片段呈现表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。

   `renderPDFForm`方法返回一个`FormsResult`对象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象&#39;s `getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数传递，创建一个用表单数据流填充它的字节数组。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[渲染基于片段的Forms](#rendering-forms-based-on-fragments)

[快速开始（SOAP模式）：使用Java API渲染基于片段的表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#render-forms-based-on-fragments-using-the-web-service-api}基于片段渲染表单

使用Forms API（Web服务）渲染基于片段的表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms Client API对象

   创建`FormsService`对象并设置身份验证值。

1. 指定URI值

   * 使用其构造函数创建存储URI值的`URLSpec`对象。
   * 调用`URLSpec`对象的`setApplicationWebRoot`方法并传递一个字符串值，该值表示应用程序的Web根目录。
   * 调用`URLSpec`对象的`setContentRootURI`方法并传递一个指定内容根URI值的字符串值。 确保表单设计位于内容根URI中。 否则，Forms服务将引发异常。 要引用存储库，请指定`repository://`。
   * 调用`URLSpec`对象的`setTargetURL`方法并传递一个字符串值，该字符串值指定将表单目标发布到的位置。 如果在表单设计中定义目标URL，则可以传递空字符串。 您还可以指定将表单发送到的URL以执行计算。

1. 渲染表单

   调用`FormsService`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递`null`。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 请注意，如果输入文档是PDF文档，则无法设置加标签的PDF选项。 如果输入文件是XDP文件，则可以设置加标签的PDF选项。
   * 一个`URLSpec`对象，其中包含Forms服务所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数用于存储呈现的表单。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 此参数将存储表单中的页数。
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数将存储区域设置值。
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `renderPDFForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值，创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建一个包含表单数据的`BLOB`对象。
   * 通过调用`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用`setContentType`方法并传递`BLOB`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充它。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[渲染基于片段的Forms](#rendering-forms-based-on-fragments)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
