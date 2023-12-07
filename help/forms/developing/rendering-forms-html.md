---
title: 将Forms渲染为HTML
description: 使用Forms服务将表单渲染为HTML，以响应来自Web浏览器的HTTP请求。 您可以使用Java API和Web服务API将表单渲染为HTML。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '4102'
ht-degree: 0%

---

# 将Forms渲染为HTML {#rendering-forms-as-html}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

Forms服务将表单渲染为HTML，以响应来自Web浏览器的HTTP请求。 将表单渲染为HTML的好处是，客户端Web浏览器所在的计算机不需要Adobe Reader、Acrobat或Flash Player(适用于表单指南（已弃用）)。

要将表单渲染为HTML，必须将表单设计另存为XDP文件。 保存为PDF文件的表单设计无法呈现为HTML。 在Designer中开发将渲染为HTML的表单设计时，请考虑以下条件：

* 请勿使用对象的边框属性在表单上绘制线条、框或网格。 某些浏览器可能不会将边框与预览中显示的边框完全对齐。 对象可能显示为分层，也可能将其他对象推离其预期位置。
* 可以使用直线、矩形和圆定义背景。
* 绘制文本的大小略大于容纳文本所需的大小。 某些Web浏览器无法清楚地显示文本。

>[!NOTE]
>
>在渲染包含TIFF图像的表单时，使用 `FormServiceClient` 对象的 `(Deprecated) renderHTMLForm` 和 `renderHTMLForm2` 方法，则TIFF图像在Internet Explorer或Mozilla Firefox浏览器中显示的渲染HTML表单中不可见。 这些浏览器不提供对TIFF图像的本机支持。

## HTML页面 {#html-pages}

当窗体设计呈现为HTML窗体时，每个第二级子窗体呈现为HTML页（面板）。 可以在Designer中查看子表单的层次结构。 属于根子表单的子表单（根子表单的默认名称为form1）是面板子表单。 以下示例显示了窗体设计的子窗体。

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

当窗体设计呈现为HTML窗体时，面板不受任何特定页面大小的限制。 如果您有动态子表单，则应将它们嵌套在面板子表单中。 动态子表单能够扩展到无限数量的HTML页。

当表单呈现为HTML表单时，页面大小(对呈现为PDF的表单进行分页所必需的)没有任何意义。 由于具有流式布局的表单可以扩展到无限数量的HTML页，因此请务必避免在母版页上使用页脚。 母版页上HTML区域下面的页脚可能会覆盖流过页面边界的内容内容。

您必须使用 `xfa.host.pageUp` 和 `xfa.host.pageDown` 方法。 您可以通过向Forms服务发送表单并让Forms服务将表单渲染回客户端设备（通常是Web浏览器）来更改页面。

>[!NOTE]
>
>将表单发送到Forms服务，然后让Forms服务将表单渲染回客户端设备的过程称为将数据轮跳到服务器。

>[!NOTE]
>
>如果要自定义HTML表单上“HTML数字签名”按钮的外观，则必须更改fscdigsig.css文件（在adobe-forms-ds.ear > adobe-forms-ds.war文件中）中的以下属性：

**.fsc-ds-ssb**：此样式表适用于符号字段为空的情况。

**.fsc-ds-ssv**：此样式表适用于存在有效签名字段的情况。

**.fsc-ds-ssc**：此样式表适用于存在有效符号字段但数据已更改的情况。

**.fsc-ds-ssi**：此样式表适用于符号字段无效的情况。

**.fsc-ds-popup-bg**：未使用此样式表属性。

**.fsc-ds-popup-btn**：未使用此样式表属性。

## 正在运行脚本 {#running-scripts}

表单作者指定脚本是在服务器上还是客户端上执行。 Forms服务会创建一个分布式事件处理环境，用于执行可通过使用 `runAt` 属性。 有关此属性或在表单设计中创建脚本的信息，请参阅 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Forms服务可以在渲染表单时执行脚本。 因此，您可以通过连接到数据库或客户端上可能没有的Web服务来预填充包含数据的表单。 您还可以设置按钮的 `Click` 在服务器上运行的事件，以便客户端将数据往返到服务器。 这允许客户端在用户与表单交互时运行可能需要服务器资源的脚本，例如企业数据库。 对于HTML表单，formcalc脚本只能在服务器上执行。 因此，您必须将这些脚本标记为在 `server` 或 `both`.

您可以通过调用来设计在页面（面板）之间移动的表单 `xfa.host.pageUp` 和 `xfa.host.pageDown` 方法。 此脚本放置在按钮的 `Click` 事件和 `runAt` 属性设置为 `Both`. 您选择的原因 `Both` 因此，Adobe Reader或Acrobat(适用于呈现为PDF的表单)可以在不访问服务器的情况下更改页面，并且HTML表单可以通过将数据循环到服务器来更改页面。 即，将表单发送到Forms服务，并将表单呈现为HTML，同时显示新页面。

建议不要为脚本变量和表单字段指定相同的名称，例如项目。 某些Web浏览器（如Internet Explorer）可能无法初始化与表单字段同名的变量，从而导致出现脚本错误。 为表单字段和脚本变量指定不同的名称是一种好的做法。

在呈现包含页面导航功能和表单脚本的HTML表单时（例如，假设脚本在每次呈现表单时都从数据库中检索字段数据），请确保表单脚本采用form：calculate事件，而不是form：readyevent。

form：ready事件形式的表单脚本在表单的初始渲染期间只执行一次，而不会在后续页面检索中执行。 相反，对于渲染表单的每个页面导航执行form：calculate事件。

>[!NOTE]
>
在多页面表单中，如果您移动到其他页面，JavaScript对页面所做的更改将不会保留。

您可以在提交表单之前调用自定义脚本。 此功能在所有可用的浏览器上运行。 但是，它只能在用户呈现具有它的HTML表单时使用 `Output Type` 属性设置为 `Form Body`. 当 `Output Type` 是 `Full HTML`. 有关配置此功能的步骤，请参阅管理帮助中的配置表单。

首先，定义在提交表单之前调用的回调函数，该函数的名称为 `_user_onsubmit`. 假定函数不会引发任何异常，或者如果引发异常，将忽略该异常。 建议将JavaScript函数放置在html的head部分中；但是，您可以在脚本标记(包括 `xfasubset.js`.

当表单服务器呈现包含下拉列表的XDP时，除了创建下拉列表之外，还会创建两个隐藏的文本字段。 这些文本字段存储下拉列表的数据（一个字段存储选项的显示名称，另一个字段存储选项的值）。 因此，每次用户提交表单时，都会提交下拉列表的整个数据。 假设您不希望每次都提交那么多的数据，则可以编写自定义脚本来禁用它。 例如：下拉列表的名称为 `drpOrderedByStateProv` 并将其包装在子表单标题下。 HTML输入元素的名称将 `header[0].drpOrderedByStateProv[0]`. 存储和提交下拉列表数据的隐藏字段的名称具有以下名称： `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

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

在客户端上运行或在客户端和服务器上运行的脚本必须写入到XFA子集中。 在服务器上运行的脚本可以使用完整的XFA脚本模型，也可以使用FormCalc。 有关使用JavaScript的信息，请参见 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

在客户端上运行脚本时，只有正在显示的当前面板可以使用脚本；例如，当显示面板B时，您无法针对面板A中的字段编写脚本。 在服务器上运行脚本时，可以访问所有面板。

在客户端上运行的脚本中使用脚本对象模型(SOM)表达式时要小心。 在客户端上运行的脚本仅支持SOM表达式的简化子集。

## 事件计时 {#event-timing}

XFA子集定义映射到HTML事件的XFA事件。 计算事件和验证事件的时间在行为上略有差异。 在Web浏览器中，退出字段时会执行完全计算事件。 当您对字段值做出更改时，计算事件不会自动执行。 您可以通过调用 `xfa.form.execCalculate` 方法。

在Web浏览器中，验证事件仅在退出字段或提交表单时执行。 您可以使用强制验证事件 `xfa.form.execValidate` 方法。

在Web浏览器中显示的Forms(与Adobe Reader或Acrobat不同)符合必填字段的XFA null测试（错误或警告）。

* 如果空测试产生错误，并且您退出字段时未指定值，则会显示一个消息框，您将在单击“确定”后重新定位到该字段。
* 如果空测试生成警告，并且您退出字段时未指定值，则系统将提示您单击“确定”或“取消”，从而使您可以选择继续操作而不指定值，或者返回字段输入值。

有关null测试的详细信息，请参见 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## 表单按钮 {#form-buttons}

单击提交按钮会将表单数据发送到Forms服务，并显示表单处理过程的结束。 此 `preSubmit` 事件可以设置为在客户端或服务器上运行。 此 `preSubmit` 如果配置为在客户端运行，则事件在提交表单之前运行。 否则， `preSubmit` 事件在提交表单期间在服务器上运行。 欲知关于 `preSubmit` 事件，请参见 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

如果按钮没有与其关联的客户端脚本，则会将数据提交到服务器，在服务器上执行计算，并重新生成HTML表单。 如果按钮包含客户端脚本，则不会将数据发送到服务器，并且客户端脚本将在Web浏览器中执行。

## HTML4.0 Web浏览器 {#html-4-0-web-browser}

仅支持HTML4.0的Web浏览器无法支持XFA子集客户端脚本模型。 在创建可在HTML4.0和MSDHTML或CSS2HTML中运行的表单设计时，标记为在客户端运行的脚本实际上将在服务器上运行。 例如，假设用户单击了位于HTML4.0 Web浏览器中显示的表单上的按钮。 在这种情况下，表单数据将发送到执行客户端脚本的服务器。

建议您将表单逻辑放置在计算事件中，这些计算事件在HTML为4.0的服务器以及用于MSDHTML或CSS2HTML的客户端上运行。

## 维护演示文稿更改 {#maintaining-presentation-changes}

在HTML页面（面板）之间移动时，只会保留数据的状态。 不会维护诸如背景颜色或必填字段设置之类的设置（如果与初始设置不同）。 要保持表示状态，您必须创建表示字段表示状态的字段（通常为隐藏字段）。 如果将脚本添加到字段的 `Calculate` 根据隐藏字段值更改表示法的事件，在HTML页面（面板）之间来回移动时，可以保留表示法状态。

以下脚本将维护 `fillColor` 的某个字段的值作为前缀 `hiddenField`. 假定此脚本位于字段的 `Calculate` 事件。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
>
嵌套在表单元格内时，静态对象不会显示在呈现的HTML表单中。 例如，嵌套在表格单元格中的圆形和矩形不会显示在渲染HTML表单中。 但是，当这些相同的静态对象位于表外部时，它们会正确显示。

## 对HTML表单进行数字签名 {#digitally-signing-html-forms}

如果包含数字签名字段的HTML表单呈现为以下HTML转换之一，则无法对该表单进行签名：

* AHTML
* HTML4
* 静态HTML
* NoScriptXHTML

有关对文档进行数字签名的信息，请参阅 [数字签名和认证文档](/help/forms/developing/digitally-signing-certifying-documents.md)

## 呈现符合辅助功能准则的XHTML表单 {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

您可以渲染符合辅助功能准则的完整HTML表单。 也就是说，表单在完整HTML标签中呈现，而不是在body标签中呈现HTML表单(不是完整的HTML页面)。

## 验证表单数据 {#validating-form-data}

在将表单渲染为HTML表单时，建议您限制对表单字段使用验证规则。 HTML表单可能不支持某些验证规则。 例如，当将MM-DD-YYYY验证模式应用于 `Date/Time` 表单设计中呈现为HTML表单的字段，即使正确键入了日期，该字段也不会正常工作。 但是，此验证模式可正确用于呈现为PDF的表单。

>[!NOTE]
>
有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步骤摘要 {#summary-of-steps}

要呈现HTML表单，请执行以下步骤：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 设置HTML运行时选项。
1. 呈现HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建表单数据集成服务客户端，然后才能以编程方式将数据导入PDF表单客户端API。 创建服务客户端时，您可以定义调用服务所需的连接设置。

**设置HTML运行时选项**

在渲染HTML表单时，您可以设置HTML运行时选项。 例如，您可以将工具栏添加到HTML表单，以使用户能够选择位于客户端计算机上的文件附件，或检索使用HTML表单呈现的文件附件。 默认情况下，HTML工具栏处于禁用状态。 要将工具栏添加到HTML表单，必须以编程方式设置运行时选项。 默认情况下，HTML工具栏由以下按钮组成：

* `Home`：提供指向应用程序Web根目录的链接。
* `Upload`：提供用户界面，以选择要附加到当前表单的文件。
* `Download`：提供用于显示附加文件的用户界面。

当HTML表单上出现HTML工具栏时，用户可以选择最多十个文件与表单数据一起提交。 提交文件后，Forms服务即可检索文件。

将表单渲染为HTML时，您可以指定用户代理值。 用户代理值提供浏览器和系统信息。 这是一个可选值，您可以传递空字符串值。 使用Java API快速入门呈现HTML表单展示了如何获取用户代理值并将其用于HTML呈现表单。

要发布表单数据的HTTP URL，可以通过使用Forms服务客户端API设置目标URL来指定，也可以在XDP表单设计中包含的提交按钮中指定。 如果在表单设计中指定了目标URL，请不要使用Forms服务客户端API设置值。

>[!NOTE]
>
使用工具栏呈现HTML表单是可选的。

>[!NOTE]
>
如果渲染AHTML表单，建议不要在该表单中添加工具栏。

**呈现HTML表单**

要呈现HTML表单，请指定在Designer中创建并保存为XDP文件的表单设计。 选择HTML转换类型。 例如，您可以指定用于呈现Internet Explorer 5.0或更高版本的动态HTML的HTML转换类型。

呈现HTML表单还需要值，例如呈现其他表单类型所需的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务渲染HTML表单时，它会返回一个您必须写入客户端Web浏览器的表单数据流。 在写入客户端Web浏览器时，HTML表单对用户可见。

**另请参阅**

[使用Java API将表单渲染为HTML](#render-a-form-as-html-using-the-java-api)

[使用Web服务API将表单渲染为HTML](#render-a-form-as-html-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[使用自定义工具栏呈现HTMLForms](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API将表单渲染为HTML {#render-a-form-as-html-using-the-java-api}

使用Forms API (Java)渲染HTML表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 设置HTML运行时选项

   * 创建 `HTMLRenderSpec` 对象。
   * 要使用工具栏呈现HTML表单，请调用 `HTMLRenderSpec` 对象的 `setHTMLToolbar` 方法和传递 `HTMLToolbar` 枚举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`.
   * 要设置HTML表单的区域设置值，请调用 `HTMLRenderSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。 （这是可选设置。）
   * 要在完整的HTML标签中呈现HTML表单，请调用 `HTMLRenderSpec` 对象的 `setOutputType` 方法和路径 `OutputType.FullHTMLTags`. （这是可选设置。）

   >[!NOTE]
   >
   在以下情况下，Forms无法在HTML中成功呈现： `StandAlone` 选项为 `true` 和 `ApplicationWebRoot` 引用除托管AEM Forms的J2EE应用程序服务器之外的服务器( `ApplicationWebRoot` 值是使用 `URLSpec` 传递给的对象 `FormsServiceClient` 对象的 `(Deprecated) renderHTMLForm` 方法)。 当 `ApplicationWebRoot` 是托管AEM Forms的服务器中的另一台服务器，管理控制台中的Web根URI值需要设置为表单的Web应用程序URI值。 可以通过登录到管理控制台，单击服务> Forms，并将Web根URI设置为https://server-name:port/FormServer来完成此操作。 然后，保存您的设置。

1. 呈现HTML表单

   调用 `FormsServiceClient` 对象的 `(Deprecated) renderHTMLForm` 方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保您指定完整的路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 用于指定HTML首选项类型的枚举值。 例如，要呈现与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递一个空值 `com.adobe.idp.Document` 对象。
   * 此 `HTMLRenderSpec` 存储HTML运行时选项的对象。
   * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` 用于存储呈现HTML表单所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   此 `(Deprecated) renderHTMLForm` 方法返回 `FormsResult` 包含可写入客户端Web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `com.adobe.idp.Document` 对象，方法是调用 `FormsResult` 对象 `getOutputContent` 方法。
   * 获取的内容类型 `com.adobe.idp.Document` 对象(通过调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 通过调用对象的内容类型 `setContentType` 方法和传递的内容类型 `com.adobe.idp.Document` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建 `java.io.InputStream` 对象，方法是调用 `com.adobe.idp.Document` 对象的 `getInputStream` 方法。
   * 创建字节数组，并通过调用 `InputStream` 对象的 `read` 方法并将字节数组作为参数传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象的 `write` 将表单数据流发送到客户端Web浏览器的方法。 将字节数组传递给 `write` 方法。

**另请参阅**

[将Forms渲染为HTML](#rendering-forms-as-html)

[快速入门（SOAP模式）：使用Java API呈现HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API将表单渲染为HTML {#render-a-form-as-html-using-the-web-service-api}

使用Forms API（Web服务）渲染HTML表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建 `FormsService` 对象并设置身份验证值。

1. 设置HTML运行时选项

   * 创建 `HTMLRenderSpec` 对象。
   * 要使用工具栏呈现HTML表单，请调用 `HTMLRenderSpec` 对象的 `setHTMLToolbar` 方法和传递 `HTMLToolbar` 枚举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`.
   * 要设置HTML表单的区域设置值，请调用 `HTMLRenderSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。 有关更多信息，请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 要在完整的HTML标签中呈现HTML表单，请调用 `HTMLRenderSpec` 对象的 `setOutputType` 方法和路径 `OutputType.FullHTMLTags`.

   >[!NOTE]
   >
   在以下情况下，Forms无法在HTML中成功呈现： `StandAlone` 选项为 `true` 和 `ApplicationWebRoot` 引用除托管AEM Forms的J2EE应用程序服务器之外的服务器( `ApplicationWebRoot` 值是使用 `URLSpec` 传递给的对象 `FormsServiceClient` 对象的 `(Deprecated) renderHTMLForm` 方法)。 当 `ApplicationWebRoot` 是托管AEM Forms的服务器中的另一台服务器，管理控制台中的Web根URI值需要设置为表单的Web应用程序URI值。 可以通过登录到管理控制台，单击服务> Forms，并将Web根URI设置为https://server-name:port/FormServer来完成此操作。 然后，保存您的设置。

1. 呈现HTML表单

   调用 `FormsService` 对象的 `(Deprecated) renderHTMLForm` 方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保您指定完整的路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 用于指定HTML首选项类型的枚举值。 例如，要呈现与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`.
   * A `BLOB` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递 `null`. (请参阅 [使用可流布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * 此 `HTMLRenderSpec` 存储HTML运行时选项的对象。
   * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 如果您不想设置此值，则可以传递空字符串。
   * A `URLSpec` 用于存储呈现HTML表单所需的URI值的对象。 (请参阅 [指定URI值](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。 (请参阅 [将文件附加到表单](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * 空的 `com.adobe.idp.services.holders.BLOBHolder` 方法填充的对象。 此参数值存储渲染的表单。
   * 空的 `com.adobe.idp.services.holders.BLOBHolder` 方法填充的对象。 此参数将存储输出XML数据。
   * 空的 `javax.xml.rpc.holders.LongHolder` 方法填充的对象。 此参数将存储表单中的页数。
   * 空的 `javax.xml.rpc.holders.StringHolder` 方法填充的对象。 此参数将存储区域设置值。
   * 空的 `javax.xml.rpc.holders.StringHolder` 方法填充的对象。 此参数将存储使用的HTML渲染值。
   * 空的 `com.adobe.idp.services.holders.FormsResultHolder` 将包含此操作结果的对象。

   此 `(Deprecated) renderHTMLForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值传递的对象，该对象具有必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象的 `value` 数据成员。
   * 创建 `BLOB` 通过调用 `FormsResult` 对象的 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 对象(通过调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 通过调用对象的内容类型 `setContentType` 方法和传递的内容类型 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建字节数组，并通过调用 `BLOB` 对象的 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象的 `write` 将表单数据流发送到客户端Web浏览器的方法。 将字节数组传递给 `write` 方法。

**另请参阅**

[将Forms渲染为HTML](#rendering-forms-as-html)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
