---
title: 将Forms渲染为HTML
seo-title: Rendering Forms as HTML
description: 使用Forms服务将表单渲染为HTML，以响应来自Web浏览器的HTTP请求。 您可以使用Java API和Web服务API将表单渲染为HTML。
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4150'
ht-degree: 0%

---

# 将Forms渲染为HTML {#rendering-forms-as-html}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

Forms服务将表单渲染为HTML，以响应来自Web浏览器的HTTP请求。 将表单渲染为HTML的好处是，客户端Web浏览器所在的计算机不需要Adobe Reader、Acrobat或Flash Player(对于表单指南（已弃用）)。

要将表单渲染为HTML，必须将表单设计另存为XDP文件。 保存为PDF文件的表单设计无法呈现为HTML。 在Designer中开发将渲染为HTML的表单设计时，请考虑以下条件：

* 请勿使用对象的边框属性在表单上绘制线条、框或网格。 某些浏览器可能不会将边框与预览中显示的边框完全对齐。 对象可能显示为分层或可能将其他对象推离其预期位置。
* 可使用直线、矩形和圆定义背景。
* 绘制文本的大小略大于容纳文本所需的大小。 某些Web浏览器无法清晰地显示文本。

>[!NOTE]
>
>在渲染包含TIFF图像的表单时，使用 `FormServiceClient` 对象的 `(Deprecated) renderHTMLForm` 和 `renderHTMLForm2` 方法，则TIFF图像在Internet Explorer或Mozilla Firefox浏览器中显示的渲染HTML表单中不可见。 这些浏览器不为TIFF图像提供本机支持。

## HTML页面 {#html-pages}

当窗体设计呈现为HTML窗体时，每个二级子窗体呈现为HTML页（面板）。 可以在Designer中查看子表单的层次结构。 属于根子表单的子表单（根子表单的默认名称为form1）是面板子表单。 以下示例显示了表单设计的子表单。

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

将表单设计渲染为HTML表单时，面板不受任何特定页面大小的限制。 如果您有动态子表单，则应将它们嵌套在面板子表单中。 动态子表单能够扩展到无限数量的HTML页。

当表单呈现为HTML表单时，页面大小(对呈现为PDF的表单进行分页所必需的)没有任何意义。 由于具有可流动布局的表单可展开至无限数量的HTML页，因此务必要避免主控页上的页脚。 主控页面上内容区域下方的页脚可能会覆盖流经页面边界的HTML内容。

您必须使用 `xfa.host.pageUp` 和 `xfa.host.pageDown` 方法。 您可以通过向Forms服务发送表单并让Forms服务将表单渲染回客户端设备（通常是Web浏览器）来更改页面。

>[!NOTE]
>
>将表单发送到Forms服务，然后让Forms服务将表单渲染回客户端设备的过程称为将数据轮跳到服务器。

>[!NOTE]
>
>如果要自定义HTML表单上“HTML数字签名”按钮的外观，则必须在fscdigsig.css文件（在adobe-forms-ds.ear > adobe-forms-ds.war文件中）中更改以下属性：

**.fsc-ds-ssb**：此样式表适用于符号字段为空白的情况。

**.fsc-ds-ssv**：此样式表适用于有效符号字段的情况。

**.fsc-ds-ssc**：此样式表适用于符号字段有效但数据已更改的情况。

**.fsc-ds-ssi**：此样式表适用于符号字段无效的情况。

**.fsc-ds-popup-bg**：未使用此样式表属性。

**.fsc-ds-popup-btn**：未使用此样式表属性。

## 运行脚本 {#running-scripts}

表单作者指定脚本是在服务器或客户端上执行。 Forms服务会创建一个分布式的事件处理环境，用于执行可通过使用的在客户端和服务器之间分发的表单智能 `runAt` 属性。 有关此属性或在表单设计中创建脚本的信息，请参阅 [Forms设计器](https://www.adobe.com/go/learn_aemforms_designer_63_cn)

Forms服务可以在渲染表单时执行脚本。 因此，您可以通过连接到数据库或连接到客户端上可能不可用的Web服务来预填充包含数据的表单。 您还可以设置按钮的 `Click` 事件在服务器上运行，以便客户端将数据往返到服务器。 这允许客户端在用户与表单交互时运行可能需要服务器资源的脚本，例如企业数据库。 对于HTML表单，formcalc脚本只能在服务器上执行。 因此，您必须标记这些脚本以在 `server` 或 `both`.

您可以通过调用来设计在页面（面板）之间移动的表单 `xfa.host.pageUp` 和 `xfa.host.pageDown` 方法。 此脚本放置在按钮的 `Click` 事件和 `runAt` 属性设置为 `Both`. 您选择的原因 `Both` 是这样，Adobe Reader或Acrobat(适用于呈现为PDF的表单)无需转至服务器即可更改页面，而HTML表单可以通过向服务器舍入检索数据来更改页面。 也就是说，表单将发送到Forms服务，并且表单将呈现为HTML，同时显示新页面。

建议不要为脚本变量和表单字段指定相同的名称，例如项目。 某些Web浏览器（如Internet Explorer）可能不会初始化与表单字段同名的变量，从而导致出现脚本错误。 为表单字段和脚本变量指定不同的名称是一种好的做法。

在渲染包含页面导航功能和表单脚本的HTML表单时（例如，假设脚本在每次渲染表单时都从数据库中检索字段数据），请确保表单脚本位于form：calculate事件中，而不是form：readyevent中。

位于form：ready事件中的表单脚本在表单的初始渲染期间只执行一次，而不会在后续页面检索中执行。 相反，对于渲染表单的每个页面导航执行form：calculate事件。

>[!NOTE]
在多页面表单中，如果您移动到其他页面，JavaScript对页面所做的更改将不会保留。

您可以在提交表单之前调用自定义脚本。 此功能在所有可用的浏览器上均可使用。 但是，它只能在用户渲染具有它的HTML表单时使用 `Output Type` 属性设置为 `Form Body`. 当 `Output Type` 是 `Full HTML`. 有关配置此功能的步骤，请参阅管理帮助中的配置表单。

必须先定义在提交表单之前调用的回调函数，该函数的名称为 `_user_onsubmit`. 假定函数不会引发任何异常，或者如果引发异常，则将忽略该异常。 建议将JavaScript函数放置在html的head部分中；但是，您可以在脚本标记的结尾之前的任何位置声明该函数，这些标记包括 `xfasubset.js`.

在表单服务器渲染包含下拉列表的XDP时，除了创建下拉列表之外，还会创建两个隐藏的文本字段。 这些文本字段存储下拉列表的数据（一个字段存储选项的显示名称，另一个字段存储选项的值）。 因此，每次用户提交表单时，都会提交下拉列表的整个数据。 假设您不希望每次都提交那么多的数据，则可以编写自定义脚本来禁用它。 例如：下拉列表的名称为 `drpOrderedByStateProv` 并将其包装在子表单标题下。 HTML输入元素的名称将为 `header[0].drpOrderedByStateProv[0]`. 存储和提交下拉列表数据的隐藏字段的名称具有以下名称： `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

如果不想发布数据，可以通过以下方式禁用这些输入元素。 `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA子集 {#xfa-subsets}

在创建要呈现为HTML的表单设计时，必须将脚本限制为JavaScript语言脚本的XFA子集。

在客户端上运行或在客户端和服务器上运行的脚本必须写入XFA子集中。 在服务器上运行的脚本可以使用完整的XFA脚本模型，也可以使用FormCalc。 有关使用JavaScript的信息，请参见 [Forms设计器](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

在客户端上运行脚本时，只有显示的当前面板可以使用脚本；例如，当显示面板B时，您无法针对面板A中的字段编写脚本。 在服务器上运行脚本时，可以访问所有面板。

在客户端上运行的脚本中使用脚本对象模型(SOM)表达式时，也必须小心。 在客户端上运行的脚本仅支持SOM表达式的简化子集。

## 事件计时 {#event-timing}

XFA子集定义映射到HTML事件的XFA事件。 计算事件和验证事件的时间在行为上略有不同。 在Web浏览器中，退出字段时会执行完全计算事件。 当您对字段值做出更改时，计算事件不会自动执行。 您可以通过调用 `xfa.form.execCalculate` 方法。

在Web浏览器中，仅在退出字段或提交表单时执行验证事件。 您可以使用强制验证事件 `xfa.form.execValidate` 方法。

在Web浏览器中显示的Forms(与Adobe Reader或Acrobat不同)符合必填字段的XFA空值测试（错误或警告）。

* 如果空值测试产生错误，并且您退出字段时未指定值，则会显示一个消息框，您将在单击“确定”后重新定位到该字段。
* 如果空值测试产生警告，并且您退出字段时未指定值，系统将提示您单击“确定”或“取消”，从而为您提供继续操作但不指定值或返回字段输入值的选项。

有关null测试的详细信息，请参见 [Forms设计器](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

## 表单按钮 {#form-buttons}

单击提交按钮可将表单数据发送到Forms服务，并代表表单处理的结束。 此 `preSubmit` 事件可以设置为在客户端或服务器上运行。 此 `preSubmit` 如果将事件配置为在客户端上运行，则该事件会在提交表单之前运行。 否则， `preSubmit` 事件在提交表单期间在服务器上运行。 欲知关于 `preSubmit` 事件，请参见 [Forms设计器](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

如果按钮没有关联的客户端脚本，则会将数据提交到服务器，在服务器上执行计算，并重新生成HTML表单。 如果按钮包含客户端脚本，则不会将数据发送到服务器，并且客户端脚本会在Web浏览器中执行。

## HTML4.0 Web浏览器 {#html-4-0-web-browser}

仅支持HTML4.0的Web浏览器无法支持XFA子集客户端脚本模型。 在创建同时适用于HTML4.0和MSDHTML或CSS2HTML的表单设计时，标记为在客户端运行的脚本实际上将在服务器上运行。 例如，假设用户单击了位于HTML4.0 Web浏览器中显示的表单上的按钮。 在这种情况下，表单数据将发送到执行客户端脚本的服务器。

建议您将表单逻辑放置在HTML4.0版本的服务器上运行的计算事件中，以及在MSDHTML或CSS2HTML的客户端上运行的计算事件中。

## 维护演示文稿更改 {#maintaining-presentation-changes}

在HTML页面（面板）之间移动时，只会保留数据的状态。 不会维护背景颜色或必填字段设置等设置（如果与初始设置不同）。 要保持表示状态，您必须创建表示字段表示状态的字段（通常为隐藏字段）。 如果将脚本添加到字段的 `Calculate` 根据隐藏字段值更改演示文稿的事件，在HTML页面（面板）之间来回移动时，可以保留演示文稿状态。

以下脚本将维护 `fillColor` 基于的值的ID为 `hiddenField`. 假定此脚本位于字段的 `Calculate` 事件。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
嵌套在表单元格内时，静态对象不会显示在渲染的HTML表单中。 例如，嵌套在表格单元格中的圆和矩形不会显示在渲染HTML表单中。 但是，当这些相同的静态对象位于表外部时，它们会正确显示。

## 对HTML表单进行数字签名 {#digitally-signing-html-forms}

如果包含数字签名字段的HTML表单呈现为以下HTML转换之一，则无法对该表单进行签名：

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

有关对文档进行数字签名的信息，请参见 [数字签名和认证文档](/help/forms/developing/digitally-signing-certifying-documents.md)

## 渲染符合辅助功能准则的XHTML表单 {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

您可以渲染符合无障碍准则的完整HTML表单。 也就是说，表单在完整HTML标签中呈现，而不是在body标签中呈现HTML表单(不是完整的HTML页面)。

## 验证表单数据 {#validating-form-data}

在将表单渲染为HTML表单时，建议您限制对表单字段使用验证规则。 HTML表单可能不支持某些验证规则。 例如，将MM-DD-YYYY验证模式应用于 `Date/Time` 字段位于呈现为HTML表单的表单设计中，即使正确键入了日期，该字段也无法正常工作。 但是，此验证模式适用于呈现为PDF的表单。

>[!NOTE]
有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步骤摘要 {#summary-of-steps}

要渲染HTML表单，请执行以下步骤：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 设置HTML运行时选项。
1. 渲染HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建表单数据集成服务客户端，然后才能以编程方式将数据导入PDF表单客户端API。 创建服务客户端时，您可以定义调用服务所需的连接设置。

**设置HTML运行时选项**

在渲染HTML表单时，可以设置HTML运行时选项。 例如，您可以将工具栏添加到HTML表单，使用户能够选择位于客户端计算机上的文件附件，或检索使用HTML表单呈现的文件附件。 默认情况下，HTML工具栏处于禁用状态。 要将工具栏添加到HTML表单，必须以编程方式设置运行时选项。 默认情况下，HTML工具栏包含以下按钮：

* `Home`：提供指向应用程序Web根目录的链接。
* `Upload`：提供用户界面，以选择要附加到当前表单的文件。
* `Download`：提供用于显示附加文件的用户界面。

当HTML表单上出现HTML工具栏时，用户可以选择最多十个要与表单数据一起提交的文件。 提交文件后，Forms服务即可检索文件。

将表单渲染为HTML时，您可以指定用户代理值。 用户代理值提供浏览器和系统信息。 这是一个可选值，您可以传递一个空字符串值。 “使用Java API渲染HTML表单”快速入门说明了如何获取用户代理值并将其用于将表单渲染为HTML。

要向其中发布表单数据的HTTP URL，可以通过使用Forms服务客户端API设置目标URL来指定，也可以在XDP表单设计中包含的“提交”按钮中指定。 如果在表单设计中指定了目标URL，则请不要使用Forms服务客户端API设置值。

>[!NOTE]
使用工具栏呈现HTML表单是可选的。

>[!NOTE]
如果渲染AHTML表单，建议不要向表单添加工具栏。

**渲染HTML表单**

要呈现HTML表单，必须指定在Designer中创建并另存为XDP文件的表单设计。 还必须选择HTML转换类型。 例如，您可以指定用于渲染Internet Explorer 5.0或更高版本的动态HTML的HTML转换类型。

呈现HTML表单还需要值，例如呈现其他表单类型所需的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务渲染HTML表单时，它会返回您必须写入客户端Web浏览器的表单数据流。 在写入客户端Web浏览器时，用户可看到HTML表单。

**另请参阅**

[使用Java API将表单渲染为HTML](#render-a-form-as-html-using-the-java-api)

[使用Web服务API将表单渲染为HTML](#render-a-form-as-html-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[使用自定义工具栏渲染HTMLForms](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[创建渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API将表单渲染为HTML {#render-a-form-as-html-using-the-java-api}

使用Forms API (Java)渲染HTML表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 设置HTML运行时选项

   * 创建 `HTMLRenderSpec` 对象。
   * 要使用工具栏渲染HTML表单，请调用 `HTMLRenderSpec` 对象的 `setHTMLToolbar` 方法和传递 `HTMLToolbar` 枚举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`.
   * 要设置HTML表单的区域设置值，请调用 `HTMLRenderSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。 （这是一个可选设置。）
   * 要在完整HTML标签中呈现HTML表单，请调用 `HTMLRenderSpec` 对象的 `setOutputType` 方法和路径 `OutputType.FullHTMLTags`. （这是一个可选设置。）

   >[!NOTE]
   当Forms处于以下状态时，无法在HTML中成功呈现 `StandAlone` 选项为 `true` 和 `ApplicationWebRoot` 引用除托管AEM Forms的J2EE应用程序服务器之外的其他服务器( `ApplicationWebRoot` 值是使用 `URLSpec` 传递到的对象 `FormsServiceClient` 对象的 `(Deprecated) renderHTMLForm` 方法)。 当 `ApplicationWebRoot` 是来自托管AEM Forms的服务器，管理控制台中的Web根URI值需要设置为表单的Web应用程序URI值。 要执行此操作，请登录到管理控制台，单击服务> Forms，然后将Web根URI设置为https://server-name:port/FormServer。 然后，保存您的设置。

1. 渲染HTML表单

   调用 `FormsServiceClient` 对象的 `(Deprecated) renderHTMLForm` 方法，并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML首选项类型的枚举值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递一个空值 `com.adobe.idp.Document` 对象。
   * 此 `HTMLRenderSpec` 存储HTML运行时选项的对象。
   * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` 存储呈现HTML表单所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   此 `(Deprecated) renderHTMLForm` 方法返回 `FormsResult` 包含可写入客户端Web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `com.adobe.idp.Document` 对象 `FormsResult` 对象 `getOutputContent` 方法。
   * 获取的内容类型 `com.adobe.idp.Document` 对象，调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用其 `setContentType` 方法和传递的内容类型 `com.adobe.idp.Document` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建 `java.io.InputStream` 对象 `com.adobe.idp.Document` 对象的 `getInputStream` 方法。
   * 创建一个字节数组，并通过调用 `InputStream` 对象的 `read` 方法，并将字节数组作为参数传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象的 `write` 方法将表单数据流发送到客户端Web浏览器。 将字节数组传递到 `write` 方法。

**另请参阅**

[将Forms渲染为HTML](#rendering-forms-as-html)

[快速入门（SOAP模式）：使用Java API渲染HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API将表单渲染为HTML {#render-a-form-as-html-using-the-web-service-api}

使用Forms API（Web服务）渲染HTML表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建 `FormsService` 对象并设置身份验证值。

1. 设置HTML运行时选项

   * 创建 `HTMLRenderSpec` 对象。
   * 要使用工具栏渲染HTML表单，请调用 `HTMLRenderSpec` 对象的 `setHTMLToolbar` 方法和传递 `HTMLToolbar` 枚举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`.
   * 要设置HTML表单的区域设置值，请调用 `HTMLRenderSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。 有关更多信息，请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 要在完整HTML标签中呈现HTML表单，请调用 `HTMLRenderSpec` 对象的 `setOutputType` 方法和路径 `OutputType.FullHTMLTags`.

   >[!NOTE]
   当Forms处于以下状态时，无法在HTML中成功呈现 `StandAlone` 选项为 `true` 和 `ApplicationWebRoot` 引用除托管AEM Forms的J2EE应用程序服务器之外的其他服务器( `ApplicationWebRoot` 值是使用 `URLSpec` 传递到的对象 `FormsServiceClient` 对象的 `(Deprecated) renderHTMLForm` 方法)。 当 `ApplicationWebRoot` 是来自托管AEM Forms的服务器，管理控制台中的Web根URI值需要设置为表单的Web应用程序URI值。 要执行此操作，请登录到管理控制台，单击服务> Forms，然后将Web根URI设置为https://server-name:port/FormServer。 然后，保存您的设置。

1. 渲染HTML表单

   调用 `FormsService` 对象的 `(Deprecated) renderHTMLForm` 方法，并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML首选项类型的枚举值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`.
   * A `BLOB` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递 `null`. (请参阅 [使用可流布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * 此 `HTMLRenderSpec` 存储HTML运行时选项的对象。
   * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 如果您不想设置此值，可以传递空字符串。
   * A `URLSpec` 存储呈现HTML表单所需的URI值的对象。 (请参阅 [指定URI值](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。 (请参阅 [将文件附加到表单](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的对象。 此参数值存储渲染的表单。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的对象。 此参数将存储输出XML数据。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的对象。 此参数将存储表单中的页数。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的对象。 此参数将存储区域设置值。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的对象。 此参数将存储使用的HTML渲染值。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 将包含此操作结果的对象。

   此 `(Deprecated) renderHTMLForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值（具有必须写入客户端Web浏览器的表单数据流）传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象的 `value` 数据成员。
   * 创建 `BLOB` 通过调用 `FormsResult` 对象的 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 对象，调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用其 `setContentType` 方法和传递的内容类型 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建一个字节数组，并通过调用 `BLOB` 对象的 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象的 `write` 方法将表单数据流发送到客户端Web浏览器。 将字节数组传递到 `write` 方法。

**另请参阅**

[将Forms渲染为HTML](#rendering-forms-as-html)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
