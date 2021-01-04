---
title: 使用CustomToolbars渲染HTMLForms
seo-title: 使用CustomToolbars渲染HTMLForms
description: 使用Forms服务自定义使用HTML表单呈现的工具栏。 您可以使用Java API和Web服务API呈现具有自定义工具栏的HTML表单。
seo-description: 使用Forms服务自定义使用HTML表单呈现的工具栏。 您可以使用Java API和Web服务API呈现具有自定义工具栏的HTML表单。
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2370'
ht-degree: 0%

---


# 使用CustomToolbars {#rendering-html-forms-with-customtoolbars}渲染HTMLForms

## 使用自定义工具栏{#rendering-html-forms-with-custom-toolbars}渲染HTMLForms

Forms服务允许您自定义使用HTML表单呈现的工具栏。 可以通过覆盖默认的CSS样式来自定义工具栏以更改其外观，并通过覆盖Java脚本来添加动态行为。 使用名为fscmenu.xml的XML文件自定义工具栏。 默认情况下，Forms服务从内部指定的URI位置检索此文件。

>[!NOTE]
>
>此URI位置位于adobe-forms-core.jar文件中，该文件位于adobe-forms-dsc.jar文件中。 adobe-forms-dsc.jar文件位于C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)中。 您可以使用文件提取工具（如Win RAR）打开adobe。

您可以从此位置复制fscmenu.xml，修改它以满足您的要求，然后将它放在自定义URI位置。 然后，使用Forms服务API，使用您的fscmenu.xml文件从指定位置设置导致Forms服务的运行时选项。 这些操作导致Forms服务渲染具有自定义工具栏的HTML表单。

除了fscmenu.xml文件外，您还需要获得以下文件：

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS是与每个节点关联的Java脚本。 必须为`div#fscmenu`节点提供一个，也可以为`ul#fscmenuItem`节点提供一个。 JS文件实现核心工具栏功能，默认文件正常工作。

fscCSS是与特定节点关联的样式表。 CSS文件中的样式指定工具栏外观。 ** fscVCSS是垂直工具栏的样式表，显示在呈现的HTML表单的左侧。** fscIECSS是用于在Internet Explorer中呈现的HTML表单的样式表。

确保fscmenu.xml文件中引用了上述所有文件。 即，在fscmenu.xml文件中，指定URI位置以指向这些文件，以便Forms服务能够找到它们。 默认情况下，这些文件位于以内部关键字`FSWebRoot`或`ApplicationWebRoot`开头的URI位置。

要自定义工具栏，请使用外部关键字`FSToolBarURI`替换关键字。 此关键字表示在运行时传递到Forms服务的URI（此方法在本节后面显示）。

您还可以指定这些JS和CSS文件的绝对位置，如https://www.mycompany.com/scripts/misc/fscmenu.js。 在这种情况下，您无需使用`FSToolBarURI`关键字。

>[!NOTE]
>
>建议不要混合引用这些文件的方式。 也就是说，应使用`FSToolBarURI`关键字或绝对位置引用所有URI。

打开adobe-forms-&lt;appserver>.ear文件即可获取JS和CSS文件。 在此文件中，打开adobe-forms-res.war。 所有这些文件都位于WAR文件中。 adobe-forms-&lt;appserver>.ear文件位于AEM forms安装文件夹(C:\ is the installation directory)中。 您可以使用文件提取工具（如WinRAR）打开adobe-forms-&lt;appserver>.ear。

以下XML语法显示一个fscmenu.xml文件示例。

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

以下项目介绍了如何自定义工具栏：

* 更改`fscJS`、`fscCSS`、`fscVCSS`、`fscIECSS`属性（在fscmenu.xml文件中）的值，以通过使用本节中介绍的方法之一（例如`fscJS="FSToolBarURI/scripts/fscmenu.js"`）反映引用文件的自定义位置。
* 必须指定所有CSS和JS文件。 如果没有修改任何文件，请在自定义位置提供默认文件。 打开各种文件（如本节所述）即可获得默认文件。
* 允许为任何文件提供绝对引用(例如，https://www.example.com/scripts/custom-vertical-fscmenu.css)。
* `div#fscmenu`节点需要的JS和CSS文件是工具栏功能的必备工具。 单个`ul#fscmenuItem`节点可能有或可能没有支持JS或CSS文件。

**更改本地值**

在自定义工具栏时，可以更改工具栏的区域设置值。 即，可以用其他语言显示。 下图显示了一个以法语显示的自定义工具栏。

>[!NOTE]
>
>无法使用多种语言创建自定义工具栏。 工具栏无法根据区域设置使用不同的XML文件。

要更改工具栏的区域设置值，请确保fscmenu.xml文件包含要显示的语言。 以下XML语法显示了fscmenu.xml文件，该文件用于显示法语工具栏。

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
>与此部分关联的快速开始使用此XML文件显示法语自定义工具栏，如上图所示。

另外，通过调用`HTMLRenderSpec`对象的`setLocale`方法并传递指定区域设置值的字符串值来指定有效的区域设置值。 例如，传递`fr_FR`以指定法语。 Forms服务与本地化的工具栏捆绑在一起。

>[!NOTE]
>
>在渲染使用自定义工具栏的HTML表单之前，您必须了解HTML表单的渲染方式。 (请参阅[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)。)

有关Forms服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要呈现包含自定义工具栏的HTML表单，请执行以下任务:

1. 包括项目文件。
1. 创建一个FormsJava API对象。
1. 引用自定义fscmenu XML文件。
1. 渲染HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建FormsJava API对象**

在以编程方式执行Forms服务支持的操作之前，必须创建Forms客户端对象。

**引用自定义fscmenu XML文件**

要呈现包含自定义工具栏的HTML表单，请引用描述工具栏的fscmenu XML文件。 （本节提供fscmenu XML文件的两个示例。） 另外，确保fscmenu.xml文件正确指定所有引用文件的位置。 如本节前面所述，确保所有文件都由`FSToolBarURI`关键字或其绝对位置引用。

**渲染HTML表单**

要渲染HTML表单，请指定在Designer中创建并另存为XDP文件的表单设计。 还选择HTML转换类型。 例如，可指定用于为Internet Explorer 5.0或更高版本渲染动态HTML的HTML转换类型。

渲染HTML表单还需要值，如用于渲染其他表单类型的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务呈现HTML表单时，它返回一个表单数据流，您必须将该数据流写入客户端Web浏览器，以使用户可以看到该HTML表单。

**另请参阅**

[使用Java API使用自定义工具栏渲染HTML表单](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[使用Web服务API使用自定义工具栏渲染HTML表单](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[渲染交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建呈现Forms的Web 应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}使用自定义工具栏渲染HTML表单

使用Forms服务API(Java)渲染包含自定义工具栏的HTML表单：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建FormsJava API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`FormsServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 引用自定义fscmenu XML文件

   * 使用`HTMLRenderSpec`对象的构造函数创建&lt;a0/>对象。
   * 要呈现带有工具栏的HTML表单，请调用`HTMLRenderSpec`对象的`setHTMLToolbar`方法并传递`HTMLToolbar`枚举值。 例如，要显示垂直HTML工具栏，请传递`HTMLToolbar.Vertical`。
   * 通过调用`HTMLRenderSpec`对象的`setToolbarURI`方法并传递指定XML文件URI位置的字符串值，指定fscmenu XML文件的位置。
   * 如果适用，请通过调用`HTMLRenderSpec`对象的`setLocale`方法并传递指定区域设置值的字符串值来设置区域设置值。 默认值为英语。

   >[!NOTE]
   >
   >与此部分关联的快速开始将此值设置为&#x200B;`fr_FR`*。*

1. 渲染HTML表单

   调用`FormsServiceClient`对象的`renderHTMLForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 一个`TransformTo`枚举值，它指定HTML首选项类型。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定`TransformTo.MSDHTML`。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递一个空`com.adobe.idp.Document`对象。
   * 存储HTML运行时选项的`HTMLRenderSpec`对象。
   * 指定`HTTP_USER_AGENT`头值的字符串值，如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * 一个`URLSpec`对象，用于存储呈现HTML表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是可选参数，如果不想将文件附加到表单，可以指定`null`。

   `renderHTMLForm`方法返回一个`FormsResult`对象，该对象包含一个必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象“s `getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 创建一个`javax.servlet.ServletOutputStream`对象，该对象通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法将表单数据流写入客户端Web浏览器。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数进行传递，创建一个字节数组并将其填充为表单数据流。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[快速开始（SOAP模式）:使用Java API使用自定义工具栏渲染HTML表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}使用自定义工具栏渲染HTML表单

使用Forms服务API（Web服务）渲染包含自定义工具栏的HTML表单：

1. 包括项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 在类路径中包含Java代理类。

1. 创建FormsJava API对象

   创建`FormsService`对象并设置身份验证值。

1. 引用自定义fscmenu XML文件

   * 使用`HTMLRenderSpec`对象的构造函数创建&lt;a0/>对象。
   * 要呈现带有工具栏的HTML表单，请调用`HTMLRenderSpec`对象的`setHTMLToolbar`方法并传递`HTMLToolbar`枚举值。 例如，要显示垂直HTML工具栏，请传递`HTMLToolbar.Vertical`。
   * 通过调用`HTMLRenderSpec`对象的`setToolbarURI`方法并传递指定XML文件URI位置的字符串值，指定fscmenu XML文件的位置。
   * 如果适用，请通过调用`HTMLRenderSpec`对象的`setLocale`方法并传递指定区域设置值的字符串值来设置区域设置值。 默认值为英语。

   >[!NOTE]
   >
   >与此部分关联的快速开始将此值设置为&#x200B;`fr_FR`*。*

1. 渲染HTML表单

   调用`FormsService`对象的`renderHTMLForm`方法并传递以下值：

   * 一个字符串值，它指定表单设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 一个`TransformTo`枚举值，它指定HTML首选项类型。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定`TransformTo.MSDHTML`。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递`null`。
   * 存储HTML运行时选项的`HTMLRenderSpec`对象。
   * 指定`HTTP_USER_AGENT`头值的字符串值，如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`。 如果不想设置此值，可以传递空字符串。
   * 一个`URLSpec`对象，用于存储呈现HTML表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 此参数是可选的，如果不想将文件附加到表单，可以指定`null`。
   * 由`renderHTMLForm`方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数值存储呈现的表单。
   * 由`renderHTMLForm`方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数存储输出XML数据。
   * 由`renderHTMLForm`方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 此参数存储表单中的页数。
   * 由`renderHTMLForm`方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数存储区域设置值。
   * 由`renderHTMLForm`方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数存储所使用的HTML呈现值。
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `renderHTMLForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值，创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 通过调用`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用`setContentType`方法并传递`BLOB`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 创建一个`javax.servlet.ServletOutputStream`对象，该对象通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法将表单数据流写入客户端Web浏览器。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充它。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
