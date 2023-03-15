---
title: 使用CustomToolbars渲染HTMLForms
seo-title: Rendering HTML Forms with CustomToolbars
description: 使用Forms服务可自定义通过HTML表单呈现的工具栏。 您可以使用Java API和Web服务API通过自定义工具栏呈现HTML表单。
seo-description: Use the Forms service to customize a toolbar that is rendered with an HTML form. You can render an HTML Form with a custom toolbar using the Java API and a Web Service API.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# 使用CustomToolbars渲染HTMLForms {#rendering-html-forms-with-customtoolbars}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

## 使用自定义工具栏渲染HTMLForms {#rendering-html-forms-with-custom-toolbars}

Forms服务允许您自定义使用HTML表单呈现的工具栏。 可以自定义工具栏，以通过覆盖默认CSS样式来更改其外观，并通过覆盖Java脚本来添加动态行为。 使用名为fscmenu.xml的XML文件自定义工具栏。 默认情况下，Forms服务从内部指定的URI位置检索此文件。

>[!NOTE]
>
>此URI位置位于adobe-forms-core.jar文件中，该文件位于adobe-forms-dsc.jar文件中。 adobe-forms-dsc.jar文件位于C:\Adobe\Adobe_Experience_Manager_forms\文件夹中(C:\是安装目录)。 您可以使用文件提取工具（如Win RAR）打开Adobe。

您可以从此位置复制fscmenu.xml，修改它以满足您的要求，然后将其置于自定义URI位置。 接下来，使用Forms服务API从指定位置使用fscmenu.xml文件设置导致Forms服务的运行时选项。 这些操作会导致Forms服务呈现具有自定义工具栏的HTML表单。

除了fscmenu.xml文件外，还需要获取以下文件：

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS是与每个节点关联的Java脚本。 必须为以下项提供一个 `div#fscmenu` 节点和（可选） `ul#fscmenuItem` 节点。 JS文件实施核心工具栏功能，默认文件工作。

fscCSS是与特定节点关联的样式表。 CSS文件中的样式指定工具栏外观。 *fscVCSS* 是垂直工具栏的样式表，显示在渲染的HTML表单的左侧。 *fscIECSS* 是一个样式表，用于HTML在Internet Explorer中渲染的表单。

确保上述所有文件都在fscmenu.xml文件中被引用。 也就是说，在fscmenu.xml文件中，指定指向这些文件的URI位置，以便Forms服务能够找到它们。 默认情况下，这些文件在URI位置可用，以内部关键字开头 `FSWebRoot` 或 `ApplicationWebRoot`.

要自定义工具栏，请使用外部关键字替换关键字 `FSToolBarURI`. 此关键字表示在运行时传递到Forms服务的URI（本章稍后部分将显示此方法）。

您还可以指定这些JS和CSS文件的绝对位置，如https://www.mycompany.com/scripts/misc/fscmenu.js。 在这种情况下，您无需使用 `FSToolBarURI` 关键字。

>[!NOTE]
>
>不建议混合使用这些文件的引用方式。 也就是说，所有URI都应该使用 `FSToolBarURI` 关键字或绝对位置。

您可以通过打开adobe-forms-&lt;appserver>.ear文件。 在此文件中，打开adobe-forms-res.war。 所有这些文件都位于WAR文件中。 adobe-forms-&lt;appserver>.ear文件位于AEM forms安装文件夹中(C:\是安装目录)。 您可以打开adobe-forms-&lt;appserver>.ear使用文件提取工具，如WinRAR。

以下XML语法显示了一个fscmenu.xml文件的示例。

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>粗体文本表示必须引用的CSS和JS文件的URI。

以下项目介绍了自定义工具栏的方法：

* 更改以下项的值： `fscJS`， `fscCSS`， `fscVCSS`， `fscIECSS` 属性（在fscmenu.xml文件中），以使用本节中介绍的方法之一来反映所引用文件的自定义位置(例如， `fscJS="FSToolBarURI/scripts/fscmenu.js"`)。
* 必须指定所有CSS和JS文件。 如果未修改任何文件，请在自定义位置提供默认文件。 通过打开本节中介绍的各种文件，可以获得默认文件。
* 允许为任何文件提供绝对引用(例如，https://www.example.com/scripts/custom-vertical-fscmenu.css)。
* 符合以下条件的JS和CSS文件： `div#fscmenu` 节点要求是工具栏功能所必需的。 个人 `ul#fscmenuItem` 节点可能具有支持JS或CSS文件，也可能不具有这些文件。

**更改本地值**

在自定义工具栏时，您可以更改工具栏的区域设置值。 也就是说，可以用另一种语言显示它。 下图显示了一个以法语显示的自定义工具栏。

>[!NOTE]
>
>无法创建采用多种语言的自定义工具栏。 工具栏不能根据区域设置使用不同的XML文件。

要更改工具栏的区域设置值，请确保fscmenu.xml文件包含要显示的语言。 以下XML语法显示了用于显示法语工具栏的fscmenu.xml文件。

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>与此部分关联的“快速入门”使用此XML文件来显示法语自定义工具栏，如上图所示。

此外，通过调用 `HTMLRenderSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。 例如，通过 `fr_FR` 指定法语。 Forms服务与本地化的工具栏捆绑在一起。

>[!NOTE]
>
>在渲染使用自定义工具栏的HTML表单之前，您必须了解HTML表单的渲染方式。 (请参阅 [将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md).)

有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要渲染包含自定义工具栏的HTML表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms Java API对象。
1. 引用自定义fscmenu XML文件。
1. 渲染HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请包含代理文件。

**创建Forms Java API对象**

在以编程方式执行Forms服务支持的操作之前，您必须创建Forms客户端对象。

**引用自定义fscmenu XML文件**

要呈现包含自定义工具栏的HTML表单，请引用描述工具栏的fscmenu XML文件。 （本节提供了fscmenu XML文件的两个示例。） 此外，请确保fscmenu.xml文件正确指定所有引用文件的位置。 如本节前面所述，请确保所有文件都被 `FSToolBarURI` 关键字或其绝对位置。

**渲染HTML表单**

要呈现HTML表单，请指定在Designer中创建并另存为XDP文件的表单设计。 另外，选择HTML转换类型。 例如，您可以指定用于渲染Internet Explorer 5.0或更高版本的动态HTML的HTML转换类型。

呈现HTML表单还需要值，例如用于呈现其他表单类型的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务渲染HTML表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器，才能使用户看到HTML表单。

**另请参阅**

[使用Java API通过自定义工具栏渲染HTML表单](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[使用Web服务API通过自定义工具栏呈现HTML表单](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API通过自定义工具栏渲染HTML表单 {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

使用Forms服务API (Java)呈现包含自定义工具栏的HTML表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Java API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用自定义fscmenu XML文件

   * 创建 `HTMLRenderSpec` 对象。
   * 要使用工具栏渲染HTML表单，请调用 `HTMLRenderSpec` 对象的 `setHTMLToolbar` 方法和传递 `HTMLToolbar` 枚举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`.
   * 通过调用 `HTMLRenderSpec` 对象的 `setToolbarURI` 方法，并传递一个指定XML文件的URI位置的字符串值。
   * 如果适用，通过调用 `HTMLRenderSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。 默认值为English。

   >[!NOTE]
   >
   >与此部分关联的“快速入门”会将此值设置为 `fr_FR`*.*

1. 渲染HTML表单

   调用 `FormsServiceClient` 对象的 `renderHTMLForm` 方法，并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML首选项类型的枚举值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递一个空值 `com.adobe.idp.Document` 对象。
   * 此 `HTMLRenderSpec` 存储HTML运行时选项的对象。
   * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` 存储呈现HTML表单所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   此 `renderHTMLForm` 方法返回 `FormsResult` 包含必须写入客户端Web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `com.adobe.idp.Document` 对象 `FormsResult` 对象 `getOutputContent` 方法。
   * 获取的内容类型 `com.adobe.idp.Document` 对象，调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用其 `setContentType` 方法和传递的内容类型 `com.adobe.idp.Document` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建 `java.io.InputStream` 对象 `com.adobe.idp.Document` 对象的 `getInputStream` 方法。
   * 创建一个字节数组，并通过调用 `InputStream` 对象的 `read` 方法，并将字节数组作为参数传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象的 `write` 方法将表单数据流发送到客户端Web浏览器。 将字节数组传递到 `write` 方法。

**另请参阅**

[快速入门（SOAP模式）：使用Java API通过自定义工具栏呈现HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API通过自定义工具栏呈现HTML表单 {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

使用Forms服务API （Web服务）呈现包含自定义工具栏的HTML表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 在类路径中包含Java代理类。

1. 创建Forms Java API对象

   创建 `FormsService` 对象并设置身份验证值。

1. 引用自定义fscmenu XML文件

   * 创建 `HTMLRenderSpec` 对象。
   * 要使用工具栏渲染HTML表单，请调用 `HTMLRenderSpec` 对象的 `setHTMLToolbar` 方法和传递 `HTMLToolbar` 枚举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`.
   * 通过调用 `HTMLRenderSpec` 对象的 `setToolbarURI` 方法，并传递一个指定XML文件的URI位置的字符串值。
   * 如果适用，通过调用 `HTMLRenderSpec` 对象的 `setLocale` 方法，并传递一个指定区域设置值的字符串值。 默认值为English。

   >[!NOTE]
   >
   >与此部分关联的“快速入门”会将此值设置为 `fr_FR`*.*

1. 渲染HTML表单

   调用 `FormsService` 对象的 `renderHTMLForm` 方法，并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML首选项类型的枚举值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`.
   * A `BLOB` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递 `null`.
   * 此 `HTMLRenderSpec` 存储HTML运行时选项的对象。
   * 一个字符串值，它指定 `HTTP_USER_AGENT` 标头值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`)。 如果您不想设置此值，可以传递空字符串。
   * A `URLSpec` 存储呈现HTML表单所需的URI值的对象。
   * A `java.util.HashMap` 存储文件附件的对象。 此参数是可选的，您可以指定 `null` 如果您不打算将文件附加到表单。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由填充的对象 `renderHTMLForm` 方法。 此参数值存储渲染的表单。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由填充的对象 `renderHTMLForm` 方法。 此参数存储输出XML数据。
   * 空 `javax.xml.rpc.holders.LongHolder` 由填充的对象 `renderHTMLForm` 方法。 此参数存储表单中的页数。
   * 空 `javax.xml.rpc.holders.StringHolder` 由填充的对象 `renderHTMLForm` 方法。 此参数存储区域设置值。
   * 空 `javax.xml.rpc.holders.StringHolder` 由填充的对象 `renderHTMLForm` 方法。 此参数存储使用的HTML渲染值。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 将包含此操作结果的对象。

   此 `renderHTMLForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值（具有必须写入客户端Web浏览器的表单数据流）传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象的 `value` 数据成员。
   * 创建 `BLOB` 通过调用 `FormsResult` 对象的 `getOutputContent` 方法。
   * 获取的内容类型 `BLOB` 对象，调用其 `getContentType` 方法。
   * 设置 `javax.servlet.http.HttpServletResponse` 对象的内容类型(通过调用其 `setContentType` 方法和传递的内容类型 `BLOB` 对象。
   * 创建 `javax.servlet.ServletOutputStream` 用于通过调用 `javax.servlet.http.HttpServletResponse` 对象的 `getOutputStream` 方法。
   * 创建一个字节数组，并通过调用 `BLOB` 对象的 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象的 `write` 方法将表单数据流发送到客户端Web浏览器。 将字节数组传递到 `write` 方法。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
