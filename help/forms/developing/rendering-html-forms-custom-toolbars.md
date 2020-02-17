---
title: 使用自定义工具栏渲染HTML表单
seo-title: 使用自定义工具栏渲染HTML表单
description: 'null'
seo-description: 'null'
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用自定义工具栏渲染HTML表单 {#rendering-html-forms-with-customtoolbars}

## 使用自定义工具栏渲染HTML表单 {#rendering-html-forms-with-custom-toolbars}

Forms服务允许您自定义使用HTML表单呈现的工具栏。 可以通过覆盖默认的CSS样式来自定义工具栏以更改其外观，并通过覆盖Java脚本来添加动态行为。 使用名为fscmenu.xml的XML文件自定义工具栏。 默认情况下，Forms服务从内部指定的URI位置检索此文件。

>[!NOTE]
>
>此URI位置位于adobe-forms-core.jar文件中，该文件位于adobe-forms-dsc.jar文件中。 adobe-forms-dsc.jar文件位于C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)中。 您可以使用文件提取工具（如Win RAR）打开adobe。

您可以从此位置复制fscmenu.xml，根据您的要求修改它，然后将它放在自定义URI位置。 然后，使用Forms Service API，从指定位置设置导致使用fscmenu.xml文件生成Forms服务的运行时选项。 这些操作导致Forms服务渲染具有自定义工具栏的HTML表单。

除了fscmenu.xml文件外，您还需要获得以下文件：

* fscmenu.js
* fscattamments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS是与每个节点关联的Java脚本。 必须为节点提供一个，并 `div#fscmenu` 为节点提供可选 `ul#fscmenuItem` 的。 JS文件实现核心工具栏功能，默认文件可正常使用。

fscCSS是与特定节点关联的样式表。 CSS文件中的样式指定工具栏外观。 *fscVCSS* 是垂直工具栏的样式表，它显示在渲染的HTML表单的左侧。 *fscIECSS* 是用于在Internet explorer中呈现的HTML表单的样式表。

确保上述所有文件在fscmenu.xml文件中都被引用。 即，在fscmenu.xml文件中，指定指向这些文件的URI位置，以便Forms服务能够找到它们。 默认情况下，这些文件位于以内部关键字或开头的URI `FSWebRoot` 位置 `ApplicationWebRoot`。

要自定义工具栏，请使用外部关键字替换关键字 `FSToolBarURI`。 此关键字表示在运行时传递到Forms服务的URI（此方法在本节后面显示）。

您还可以指定这些JS和CSS文件的绝对位置，如https://www.mycompany.com/scripts/misc/fscmenu.js。 在这种情况下，您无需使用关 `FSToolBarURI` 键字。

>[!NOTE]
>
>建议不要混合这些文件的引用方式。 即，所有URI都应通过使用关键字或绝 `FSToolBarURI` 对位置来引用。

您可以通过打开adobe-forms-&lt;appserver>.ear文件获取JS和CSS文件。 在此文件中，打开adobe-forms-res.war。 所有这些文件都位于WAR文件中。 adobe-forms-&lt;appserver>.ear文件位于AEM Forms安装文件夹(C:\ is the installation directory)中。 您可以使用文件提取工具（如WinRAR）打开adobe-forms-&lt;appserver>.ear。

以下XML语法显示了一个fscmenu.xml文件的示例。

```as3
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

以下项目介绍了如何自定义工具栏：

* 更改、、 `fscJS`、、属性的值（在fscmenu.xml文件中），以反映引用文件的自定义位置，方法是使用本节中介绍的方法之一(例如， `fscCSS``fscVCSS``fscIECSS``fscJS="FSToolBarURI/scripts/fscmenu.js"`)。
* 必须指定所有CSS和JS文件。 如果没有修改任何文件，请在自定义位置提供默认文件。 您可以按本节所述打开各种文件来获取默认文件。
* 允许为任何文件提供绝对引用(例如，https://www.example.com/scripts/custom-vertical-fscmenu.css)。
* 节点需要的JS和CSS文 `div#fscmenu` 件是工具栏功能的必备工具。 单个 `ul#fscmenuItem` 节点可能或可能没有支持JS或CSS文件。

**更改本地值**

在自定义工具栏时，您可以更改工具栏的区域设置值。 即，可以用其他语言显示它。 下图显示了一个以法语显示的自定义工具栏。

>[!NOTE]
>
>无法使用多种语言创建自定义工具栏。 工具栏不能根据区域设置使用不同的XML文件。

要更改工具栏的区域设置值，请确保fscmenu.xml文件包含要显示的语言。 以下XML语法显示了fscmenu.xml文件，该文件用于显示法语工具栏。

```as3
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
>与此部分关联的快速入门使用此XML文件显示法语自定义工具栏，如上图所示。

此外，通过调用对象的方法并传递指定区 `HTMLRenderSpec` 域设置值的 `setLocale` 字符串值来指定有效的区域设置值。 例如，传递以 `fr_FR` 指定法语。 表单服务与本地化的工具栏捆绑在一起。

>[!NOTE]
>
>在渲染使用自定义工具栏的HTML表单之前，您必须了解HTML表单的呈现方式。 (请参阅 [将表单渲染为HTML](/help/forms/developing/rendering-forms-html.md)。)

有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要渲染包含自定义工具栏的HTML表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms Java API对象。
1. 引用自定义fscmenu XML文件。
1. 渲染HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建Forms Java API对象**

在以编程方式执行Forms服务支持的操作之前，必须先创建一个Forms客户端对象。

**引用自定义fscmenu XML文件**

要渲染包含自定义工具栏的HTML表单，请引用描述工具栏的fscmenu XML文件。 （本节提供fscmenu XML文件的两个示例。）另外，确保fscmenu.xml文件正确指定所有引用文件的位置。 如本节前面所述，确保所有文件都被关键字或其绝 `FSToolBarURI` 对位置引用。

**渲染HTML表单**

要渲染HTML表单，请指定在Designer中创建并另存为XDP文件的表单设计。 还可选择HTML转换类型。 例如，可指定用于为Internet Explorer 5.0或更高版本渲染动态HTML的HTML转换类型。

渲染HTML表单还需要值，如用于渲染其他表单类型的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现HTML表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器才能使HTML表单对用户可见。

**另请参阅**

[使用Java API使用自定义工具栏渲染HTML表单](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[使用Web服务API使用自定义工具栏渲染HTML表单](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF表单](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将表单渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建呈现表单的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API使用自定义工具栏渲染HTML表单 {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

使用Forms Service API(Java)渲染包含自定义工具栏的HTML表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms Java API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 引用自定义fscmenu XML文件

   * 使用对 `HTMLRenderSpec` 象的构造函数创建对象。
   * 要使用工具栏渲染HTML表单，请调 `HTMLRenderSpec` 用对象的方 `setHTMLToolbar` 法并传递枚 `HTMLToolbar` 举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`。
   * 通过调用对象的方法并传递一个指定XML文 `HTMLRenderSpec` 件的URI `setToolbarURI` 位置的字符串值，指定fscmenu XML文件的位置。
   * 如果适用，请通过调用对象的方法并传 `HTMLRenderSpec` 递指定区 `setLocale` 域设置值的字符串值来设置区域设置值。 默认值为英语。
   >[!NOTE]
   >
   >与此部分关联的“快速入门”将此值设置为 `fr_FR`*。*

1. 渲染HTML表单

   调用对 `FormsServiceClient` 象的方 `renderHTMLForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是表单应用程序的一部分，请确保指定完整路径，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首选项类型的enum值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`。
   * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象。 如果不想合并数据，请传递空对 `com.adobe.idp.Document` 象。
   * 存 `HTMLRenderSpec` 储HTML运行时选项的对象。
   * 指定标题值的 `HTTP_USER_AGENT` 字符串值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * 存 `URLSpec` 储呈现HTML表单所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可以指 `null` 定是否不想将文件附加到表单。
   该方 `renderHTMLForm` 法返回一个对 `FormsResult` 象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
   * 通过调用对象的方 `com.adobe.idp.Document` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `com.adobe.idp.Document` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象用于通过调用对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
   * 创建一个字节数组，并通过调用对象的方法并将字节数 `InputStream` 组作为参数传 `read` 递，用表单数据流填充它。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[快速入门（SOAP模式）:使用Java API使用自定义工具栏渲染HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API使用自定义工具栏渲染HTML表单 {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

使用Forms Service API（Web服务）渲染包含自定义工具栏的HTML表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 在类路径中包含Java代理类。

1. 创建Forms Java API对象

   创建对 `FormsService` 象并设置身份验证值。

1. 引用自定义fscmenu XML文件

   * 使用对 `HTMLRenderSpec` 象的构造函数创建对象。
   * 要使用工具栏渲染HTML表单，请调 `HTMLRenderSpec` 用对象的方 `setHTMLToolbar` 法并传递枚 `HTMLToolbar` 举值。 例如，要显示垂直HTML工具栏，请传递 `HTMLToolbar.Vertical`。
   * 通过调用对象的方法并传递一个指定XML文 `HTMLRenderSpec` 件的URI `setToolbarURI` 位置的字符串值，指定fscmenu XML文件的位置。
   * 如果适用，请通过调用对象的方法并传 `HTMLRenderSpec` 递指定区 `setLocale` 域设置值的字符串值来设置区域设置值。 默认值为英语。
   >[!NOTE]
   >
   >与此部分关联的“快速入门”将此值设置为 `fr_FR`*。*

1. 渲染HTML表单

   调用对 `FormsService` 象的方 `renderHTMLForm` 法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果引用的表单设计是表单应用程序的一部分，请确保指定完整路径，如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定 `TransformTo` HTML首选项类型的enum值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定 `TransformTo.MSDHTML`。
   * 包含 `BLOB` 要与表单合并的数据的对象。 如果您不想合并数据，请传递 `null`。
   * 存 `HTMLRenderSpec` 储HTML运行时选项的对象。
   * 一个字符串值，它指 `HTTP_USER_AGENT` 定标题值，如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`)。 如果不想设置此值，可以传递空字符串。
   * 存 `URLSpec` 储呈现HTML表单所需的URI值的对象。
   * 存储 `java.util.HashMap` 文件附件的对象。 此参数是可选的，您可以指 `null` 定是否不想将文件附加到表单。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空对 `renderHTMLForm` 象。 此参数值存储呈现的表单。
   * 由方 `com.adobe.idp.services.holders.BLOBHolder` 法填充的空对 `renderHTMLForm` 象。 此参数存储输出XML数据。
   * 由方 `javax.xml.rpc.holders.LongHolder` 法填充的空对 `renderHTMLForm` 象。 此参数存储表单中的页数。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对 `renderHTMLForm` 象。 此参数存储区域设置值。
   * 由方 `javax.xml.rpc.holders.StringHolder` 法填充的空对 `renderHTMLForm` 象。 此参数存储所使用的HTML呈现值。
   * 将包含 `com.adobe.idp.services.holders.FormsResultHolder` 此操作结果的空对象。
   该方 `renderHTMLForm` 法使用必 `com.adobe.idp.services.holders.FormsResultHolder` 须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过 `FormResult` 获取对象数据成员的 `com.adobe.idp.services.holders.FormsResultHolder` 值来创建 `value` 对象。
   * 通过调 `BLOB` 用对象的方法创建包含表 `FormsResult` 单数据的对 `getOutputContent` 象。
   * 通过调用对象的方 `BLOB` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `BLOB` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象用于通过调用对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 创建一个字节数组，并通过调用对象的 `BLOB` 方法填充该 `getBinaryData` 数组。 此任务将对象的内 `FormsResult` 容分配给字节数组。
   * 调用对 `javax.servlet.http.HttpServletResponse` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
