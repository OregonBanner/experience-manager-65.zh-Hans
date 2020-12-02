---
title: 为登陆页扩展和配置设计导入程序
seo-title: 为登陆页扩展和配置设计导入程序
description: 了解如何为登陆页配置设计导入程序。
seo-description: 了解如何为登陆页配置设计导入程序。
uuid: a2dd0c30-03e4-4e52-ba01-6b0b306c90fc
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e02f5484-fbc2-40dc-8d06-ddb53fd9afc2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '3522'
ht-degree: 59%

---


# 扩展和配置登陆页的设计导入程序{#extending-and-configuring-the-design-importer-for-landing-pages}

此部分介绍如何针对登录页面配置和扩展（如果需要）设计导入程序。[登陆页中涵盖导入后使用登陆页。](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)

**使设计导入程序提取自定义组件**

以下是使设计导入程序识别自定义组件的逻辑步骤

1. 创建TagHandler

   * 标记处理程序是处理特定类型 HTML 标记的 POJO。TagHandler 可处理的 HTML 标记类型通过 TagHandlerFactory 的 OSGi 属性“tagpattern.name”来定义。此 OSGi 属性实质上是应与要处理的输入 HTML 标记匹配的正则表达式。所有嵌套的标记都会交由标记处理程序进行处理。例如，如果注册一个包含嵌套&lt;p>标记的div,&lt;p>标记也会被抛出到您的TagHandler中，具体由您如何处理它。
   * 标记处理程序的界面与 SAX 内容处理程序的界面类似。它接收每个 HTML 标记的 SAX 事件。作为标记处理程序提供者，您需要实施设计导入程序框架自动调用的特定生命周期方法。

1. 创建其对应的TagHandlerFactory。

   * 标记处理程序工厂是 OSGi 组件 (singleton)，负责生成标记处理程序的实例。
   * 您的标记处理程序工厂必须公开一个名为“tagpattern.name”的 OSGi 属性，其值将针对输入 HTML 标记进行匹配。
   * 如果有多个标记处理函数与输入html标记匹配，则选取级别较高的标记处理函数。 排名本身作为OSGi属性&#x200B;**service.ranking**&#x200B;公开。
   * TagHandlerFactory 是一个 OSGi 组件。要提供给 TagHandler 的任何引用都必须通过此工厂提供。

1. 如果要覆盖默认值，请确保TagHandlerFactory具有更好的等级。

>[!CAUTION]
>
>[AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features) 弃用了用于导入登陆页面的设计导入程序。

## 准备要导入的 HTML {#preparing-the-html-for-import}

创建导入程序页面后，可以导入完整的HTML登陆页。 要导入 HTML 登录页面，需要首先将其内容压缩到设计包中。设计包包含 HTML 登录页面以及引用的资产（图像、css、图标、脚本，等等）。

以下备忘录提供了如何准备导入 HTML 的示例：

登陆页备忘单

[获取文件](assets/cheatsheet.zip)

### Zip 文件布局和要求 {#zip-file-layout-and-requirements}

>[!NOTE]
>
>目前，ZIP 文件只包含一个 HTML 页面或页面的一部分。

zip 文件的示例布局如下所示：

* /index.html ->登陆页HTML文件
* /css ->添加到CSS clientlib中
* /img ->所有图像和资产
* /js ->添加到JS clientlib中

该布局基于 HTML5 Boilerplate 最佳实践布局。请访问[https://html5boilerplate.com/](https://html5boilerplate.com/)阅读更多信息

>[!NOTE]
>
>设计包&#x200B;**至少必须**&#x200B;在根级别包含&#x200B;**index.html**&#x200B;文件。 如果要导入的登陆页也包含移动版本，则zip必须在根级别包含&#x200B;**mobile.index.html**&#x200B;和&#x200B;**index.html**。

### 准备登录页面 HTML {#preparing-the-landing-page-html}

为了能够导入 HTML，需要向登录页面 HTML 添加画布 div。

画布div是一个带有`id="cqcanvas"`的html **div**，必须在HTML `<body>`标签中插入，并且必须包含要转换的内容。

添加画布 div 后的登录页面 HTML 示例代码片段如下所示：

```xml
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
  <meta name="description" content="">
</head>
<body>
 <div id="cqcanvas">
  <!-- HTML content intended for conversion -->
 </div>
</body>
</html>
```

### 准备 HTML 以包含可编辑的 AEM 组件  {#preparing-the-html-to-include-editable-aem-components}

导入登录页面时，可以选择按原样导入页面，这意味着导入登录页面之后，无法在 AEM 中编辑任何导入的项目（但仍可以在页面上添加其他 AEM 组件）。

导入登录页面之前，您可能要转换登录页面的某些部分，以便它们成为可编辑的 AEM 组件。这允许您快速编辑登陆页的各个部分，即使在导入登陆页设计后也是如此。

通过将 `data-cq-component` 添加到导入 HTML 文件中的相应组件，可完成此操作。

以下部分介绍如何编辑 HTML 文件，以便可以将登录页面的某些部分转换为可编辑的不同 AEM 组件。组件在[登陆页组件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)中有详细说明。

>[!NOTE]
>
>用于将登录页面的各部分转换为 AEM 组件的 HTML 标记同时具有长格式和短标记声明。将分别介绍每个组件的这两种形式。

### 限制 {#limitations}

导入之前，请注意以下限制：

### 在标记上应用的任何属性（如类或 id） &amp;lt;body>标记未保留{#any-attribute-like-class-or-id-applied-on-the-amp-lt-body-tag-is-not-preserved}

如果在body标签上应用了id或类等任何属性（例如`<body id="container">`），则导入后不会保留它。 因此，要导入的设计不应与`<body>`标签上应用的属性有任何依赖关系。

### 拖放 zip {#drag-and-drop-zip}

Internet Explorer和Firefox版本3.6及更早版本不支持拖放zip上传。 要在使用这些浏览器时上传设计，请单击放置文件区域，打开文件上传对话框，然后使用该框上传您的设计。

支持设计zip文件“拖放”的浏览器为Chrome、Safari5.x、Firefox 4及更高版本。

### 不支持 Modernizr。{#modernizr-is-not-supported}

`Modernizr.js` 是一个基于 javascript 的工具，它检测浏览器的本机功能，还检测这些功能是否适用于 html5 元素。使用 Modernizr 增强各种旧版浏览器支持的设计可能会导致登录页面解决方案中出现导入错误。设计导入程序不支持 `Modernizr.js` 脚本。

### 导入设计包时不保留页面属性 {#page-properties-are-not-preserved-at-the-time-of-importing-design-package}

导入设计包前为页面（使用空白登录页面模板）设置的任何页面属性（例如，自定义域、强制 HTTPS，等等）在导入设计之后都会丢失。因此，推荐的做法是在导入设计包后设置页面属性。

### 仅采用HTML标记{#html-only-markup-assumed}

导入时，出于安全原因会对标记进行清理，以避免导入和发布无效标记。这种情况会假定只有 HTML 标记；所有其他形式的元素，例如内联 SVG 或 Web 组件等，都会被筛选掉。

### 文本 {#text}

用于在设计包内的 HTML 中插入文本组件 (`foundation/components/text`) 的 HTML 标记：

```xml
<div data-cq-component="text"> <p>This is some editable text</p> </div>
```

要在 HTML 中包含以上标记，请执行以下操作：

* 在导入设计包后创建的登陆页中创建可编辑的AEM文本组件(`sling:resourceType=foundation/components/text`)。
* 将创建的文本组件的`text`属性设置为`div`中包含的HTML。

**短组件标记声明**：

```xml
<p data-cq-component="text">Text component shorthand</p>
```

**包含列表的文本**

添加包含列表的文本：

* 1st
* 2nd

可在 RTE 编辑器中进行编辑：

```xml
<div data-cq-component="text"><p>This is text with a list:</p><ul><li>1st</li><li>2nd</li></ul><p>It can be edited with the RTE editor</p></div>
```

**具有颜色的文本**

添加可在 RTE 编辑器中进行编辑的具有颜色（粉红色）的文本：

```xml
<div class="pink" data-cq-component="text"><p>This is pink text.</p><p>It can be edited with the RTE editor</p></div>
```

### 标题 {#title}

用于在设计包内的HTML中插入标题组件(`wcm/landingpage/components/title`)的HTML标记：

```xml
<div data-cq-component="title"> <h1>This is some editable title text</h1> </div>
```

要在 HTML 中包含以上标记，请执行以下操作：

* 在导入设计包后创建的登陆页中创建可编辑的AEM标题组件(`sling:resourceType=wcm/landingpage/components/title`)。
* 将创建的标题组件的 `jcr:title` 属性设置为标题标记内 div 中包含的文本。
* 将`type`属性设置为标题标记，在本例中为`h1`。

标题组件支持7种类型- `h1, h2, h3, h4, h5, h6`和`default`。

**短组件标记声明**：

```xml
<h1 data-cq-component="title">Title component shorthand</h1>
```

### 图像 {#image}

用于在设计包内的 HTML 中插入图像组件 (foundation/components/image) 的 HTML 标记：

```xml
<div data-cq-component="image">
<img src="img/video1.png" alt="Video about Polar Brake Goggles in action" title="Polar Brake Goggles" width="300" height="200" />
</div>
```

要在 HTML 中包含以上标记，请执行以下操作：

* 在导入设计包后创建的登陆页中创建可编辑的AEM图像组件(`sling:resourceType=foundation/components/image`)。
* 将创建的图像组件的 `fileReference` 属性设置为导入的 src 属性中指定的图像路径。
* 将`alt`属性设置为img标记中alt属性的值。
* 将`title`属性设置为img标记中标题属性的值。
* 将`width`属性设置为img标记中width属性的值。
* 将`height`属性设置为img标记中高度属性的值。

**短组件标记声明：**

```xml
<img data-cq-component="image" src="test.png" alt="Image component shorthand"/>
```

#### 图像组件 Div 内不支持绝对 URL img src {#absolute-url-img-src-not-supported-within-image-component-div}

如果尝试使用具有绝对url src的`<img>`标记进行组件转换，则会引发相应的&#x200B;**UnsupportedTagContentException**。 例如，不支持以下内容：

`<div data-cq-component="image">`

`<img src="https://cdn.printfriendly.com/pf-button.gif" alt="Print Friendly and PDF"/>`

`</div>`

但是，不属于图像组件 div 的 img 标记支持绝对 URL 图像。

### 行动动员组件  {#call-to-action-components}

您可以标记登陆页的一部分以导入为“可编辑的行动动员组件”-这样导入的行动动员组件可以在导入登陆页后进行编辑。 AEM 包含以下 CTA 组件：

* 点进率链接 - 允许您添加一个文本链接，当访客单击这个链接时即被引向目标 URL。
* 图像链接 - 允许您添加一个图像链接，当访客单击这个链接时即被引向目标 URL。

#### 点进率链接  {#click-through-link}

该 CTA 组件可用于在登录页面上添加文本链接。

支持的属性

* 标签，具有粗体、斜体和下划线选项
* 目标 URL，支持第三方和 AEM URL
* 页面渲染选项（同一窗口、新窗口等）

用于在导入的 zip 文件中包含点进组件的 HTML 标记。此处的href映射到目标url,“视图产品详细信息”映射到标签，依此类推。

```xml
<div id="cqcanvas">
.
.
                <div data-cq-component="clickThroughLink">
        <a href="/content/we-retail/us/en/products/equipment/snow-sports/flying-snowboard.html">View Product Details  ></a>
  </div>
.
.
</div>
```

此组件既可以在任何独立应用程序中使用，也可以从 zip 中导入。

**短组件标记声明**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughLink">Click Through Link shorthand</a>
```

#### 图形链接 {#graphical-link}

该 CTA 组件可用于在登陆页面上添加任何带链接的图像。该图像可以是一个简单的按钮，也可以是任何用作背景的图像。用户单击图像时，将转到组件属性中指定的目标 URL。它是“行动动员”组的一部分。

支持的属性

* 图像裁剪、旋转
* 悬停文本、说明、大小（像素）
* 目标 URL，支持第三方和 AEM URL
* 页面渲染选项（同一窗口、新窗口等）

用于在导入的 zip 文件中包含图形链接组件的 HTML 标记。此处的href将映射到目标url,img src将是渲染图像，“标题”将被用作悬停文本，依此类推。

```xml
<div id="cqcanvas">
  <div data-cq-component="clickThroughGraphicalLink"><a href="https://www.adobe.com/go/wem"><img src="img/call-to-action-button.png" title="Click Here to Learn More" /></a></div>
</div>
```

**短组件标记声明**：

```xml
<a href="/somelink.html" data-cq-component="clickThroughGraphicalLink"><img src="linkimage.png" alt="Click Through Graphical Link shorthand"/></a>
```

>[!NOTE]
>
>要创建clickthroughgraphical链接，您需要在具有`data-cq-component="clickthroughgraphicallink"`属性的div中包含锚点标签和图像标签。
>
>例如`<div data-cq-component="clickthroughlink"> <a href="https://myURLhere/"><img src="image source here"></a> </div>`
>
>使用 CSS 时，不支持通过其他方式将图像与锚点标记相关联，例如，以下标记将无法使用：
>
>`<div data-cq-component="clickthroughgraphicallink">`
>
>`<a class="hasBackground" href="https://myURLhere/"></a>`
>
>`</div>`
>
>与关联的`css .hasbackground { background-image: pathtoimage }`


### 潜在客户表单 {#lead-form}

潜在客户表单是一种用于搜集访客/潜在客户个人资料信息的表单。这类信息可被存储起来，以供以后进行有针对性的营销活动。此信息通常包括标题、名称、电子邮件、出生日期、地址、关注，等等。它是“CTA潜在客户表单”组的一部分。

**支持的功能**

* 预定义的潜在客户字段——名字、姓氏、地址、Dob、性别、关于、userId、emailId、提交按钮在Sidekick中可用。 只需将所需的组件拖放到您的潜在客户表单即可。
* 借助于这些组件，作者可以设计独立的潜在客户表单，这些字段与潜在客户表单字段相对应。在独立或导入的zip应用程序中，用户可以使用cq:form或cta潜在客户表单字段添加其他字段，并根据要求命名和设计这些字段。
* 使用CTA潜在客户表单的特定预定义名称映射潜在客户表单字段，例如，firstName用于潜在客户表单中的名字，依此类推。
* 未映射到潜在客户表单的字段将映射到 cq:form 组件 - 文本、单选按钮、复选框、下拉框、隐藏、密码。
* 用户可以使用“标签”标记提供标题，使用样式属性“类”提供样式（仅适用于 CTA 潜在客户表单组件）。
* 感谢页面和订阅列表可以作为表单的隐藏参数提供（在index.htm中提供），也可以从“潜在客户表单的开始”的编辑栏中添加／编辑

   &lt;input type=&quot;hidden&quot; name=&quot;redirectUrl&quot; value=&quot;/content/we-retail/en/user/register/thank_you&quot; />

   &lt;input type=&quot;hidden&quot; name=&quot;groupName&quot; value=&quot;leadForm&quot; />

* 约束（如——必需）可以通过每个组件的编辑配置提供。

用于在导入的 zip 文件中包含图形链接组件的 HTML 标记。此处的“firstName”将映射到潜在客户表单的firstName等，但复选框除外——这两个复选框将映射到cq:form下拉组件。

```xml
<div id="cqcanvas">
   <div id="form_wrapper">
    <h2>NEWSLETTER SIGN UP</h2>
       <div data-cq-component="leadFormGeneration">
       <form method="post" action="#" onsubmit="return popupBox()">
       <label for="firstName" class="checkText">
        FIRST NAME
       </label><br />
       <input name="firstName" class="text pink" type="text" /><br />
       <label for="lastName" class="checkText">
        LAST NAME
       </label><br />
       <input name="lastName" class="text pink" type="text" /><br />
       <label for="emailId" class="checkText">
        EMAIL ADDRESS
       </label><br />
       <input name="emailId" class="text pink" type="text" /><br />

       <div class="checkboxes">
       <input type="checkbox" class="check" name="send_news" /> <label for="send_news" class="checkText">Send me the latest We.Retail news and announcements.</label><br />
       <input type="checkbox" class="check" name="send_offers" /> <label for="send_offers" class="checkText">Send me We.Retail deals and special offers.</label><br />
       </div>
       <input type="submit" name="submit" class="submit pink" value="Sign Up >" />
       </form>
     </div>
   </div>
```

### Parsys {#parsys}

AEM parsys 组件是可包含其他 AEM 组件的容器组件。可以在导入的 HTML 中添加 parsys 组件。这样，即使在导入之后，用户仍可以向登录页面添加可编辑的 AEM 组件，或从中删除可编辑的 AEM 组件。

段落系统为用户提供了使用 Sidekick 添加组件的功能。

用于在设计包内的 HTML 中插入 parsys 组件 (`foundation/components/parsys`) 的 HTML 标记：

```xml
<div data-cq-component="parsys">
   <div data-cq-component="title"><h2>ULTIMATE PROTECTION</h2></div>
        <div data-cq-component="title"><h3>ON SALE</h3></div>
</div>
```

要在 HTML 中包含以上标记，请执行以下操作：

* 在导入设计包后创建的登录页面中插入 AEM parsys 组件 (foundation/components/parsys)。
* 使用默认组件初始化 Sidekick。通过将 Sidekick 中的组件拖动到 Parsys 组件上，可将新组件添加到登录页面。
* parsys 还包含两个标题组件。

### 目标  {#target}

目标组件在页面上显示体验的内容。营销活动中可能创建了多个体验，目标组件可以向访问页面的各个用户动态显示不同体验的内容。

用于插入目标组件和在营销活动中创建不同体验的 HTML 标记：

```xml
<div data-cq-component="target">
 <section data-cq-component="experience" data-cq-experience="default">
  <p data-cq-component="text">Default content. Select this campaign in client context to view other experiences</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="over-30">
  <p data-cq-component="text">Content for Over 30</p>
 </section>

 <section data-cq-component="experience" data-cq-segment="under-30">
  <p data-cq-component="text">Content for Under 30</p>
 </section>
</div>
```

## 其他导入选项 {#additional-importing-options}

除指定导入的组件是否为可编辑的 AEM 组件之外，还可以在导入设计包之前配置以下内容：

* 通过提取导入 HTML 中定义的元数据设置页面属性。
* 指定 HTML 中的字符集编码。
* 覆盖导入程序页面模板。

### 通过提取导入 HTML 中定义的元数据设置页面属性 {#setting-page-properties-by-extracting-metadata-defined-in-imported-html}

设计导入程序将提取并保留导入的HTML标题中声明的以下元数据作为属性“jcr:description”:

* &lt;meta name=&quot;description&quot; content=&quot;&quot;>

设计导入程序将提取并保留HTML标记中设置的Lang属性作为属性“jcr:language”

* &lt;html lang=&quot;en&quot;>

### 指定 HTML 中的字符集编码 {#specifying-the-charset-encoding-in-the-html}

设计导入程序读取导入 HTML 中指定的编码。可按如下方式指定编码：

`<meta charset="UTF-8">`

*或者*

`<meta http-equiv="content-type" content="text/html;charset=utf-8">`

如果导入 HTML 中未指定编码，则设计导入程序设置的默认编码为 UTF-8。

### 覆盖模板  {#overlaying-template}

可通过在以下位置创建新登陆页模板来覆盖空白模板：`/apps/<appName>/designimporter/templates/<templateName>`

有关在AEM中创建新模板的步骤，请参见[此处](/help/sites-developing/templates.md)。

### 从登录页面引用组件 {#referring-a-component-from-landing-page}

假定您有一个组件，想要在 HTML 中使用 data-cq-component 属性加以引用，以便设计导入程序渲染此处包含的组件。例如，您要引用表组件(`resourceType = /libs/foundation/components/table`)。 需要在 HTML 中添加以下内容：

`<div data-cq-component="/libs/foundation/components/table">foundation table</div>`

data-cq-component 中的路径应为 resourceType 组件。

### 最佳实践 {#best-practices}

对于标记为导入时进行组件转换的元素，不建议使用类似下列选择器的 CSS 选择器。

| E > F | E 元素的子元素 F 元素 | [子组合器](https://www.w3.org/TR/css3-selectors/#child-combinators) |
|---|---|---|
| E + F | 紧贴在 E 元素之后的 F 元素 | [相邻兄弟组合器](https://www.w3.org/TR/css3-selectors/#adjacent-sibling-combinators) |
| E ~ F | E 元素之后的 F 元素 | [一般兄弟组合器](https://www.w3.org/TR/css3-selectors/#general-sibling-combinators) |
| E:root | E 元素，文档的根元素 | [结构伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-child(n) | E 元素，其父元素的第 n 个子元素 | [结构伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-child(n) | E 元素，从最后一个元素算起，其父元素的第 n 个子元素 | [结构伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-of-type(n) | E 元素，同类型的第 n 个兄弟元素 | [结构伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |
| E:nth-last-of-type(n) | E 元素，从最后一个元素算起，同类型的第 n 个兄弟元素 | [结构伪类](https://www.w3.org/TR/css3-selectors/#structural-pseudos) |

这是由于导入后向生成的Html中添加了其他HTML元素（如&lt;div>标签）。

* 对于已标记为转换到 AEM 组件的元素，也不建议使用依赖于类似上文结构的脚本。
* 不建议在用于组件转换的标记（如&lt;div data-cq-component=&quot;&amp;ast;&quot;>）上使用样式。
* 设计布局应遵循 HTML5 Boilerplate 中的最佳实践。阅读更多信息：[https://html5boilerplate.com/](https://html5boilerplate.com/)。

## 配置 OSGI 模块 {#configuring-osgi-modules}

公开可通过OSGI控制台配置的属性的组件如下：

* 登录页面设计导入程序
* 登录页面生成器
* 移动登录页面生成器
* 登录页面条目处理器

下表简要说明了这些属性：

<table>
 <tbody>
  <tr>
   <td><strong>组件</strong></td>
   <td><strong>属性名称</strong></td>
   <td><strong>属性描述 </strong></td>
  </tr>
  <tr>
   <td>登录页面设计导入程序</td>
   <td>提取过滤器</td>
   <td>用于从提取中过滤文件的正则表达式列表。<br /> 与任一指定模式匹配的 Zip 条目将从提取中排除</td>
  </tr>
  <tr>
   <td>登录页面生成器</td>
   <td>文件模式</td>
   <td>登陆页构建器可配置为处理与由文件模式定义的常规表达式匹配的HTML文件。</td>
  </tr>
  <tr>
   <td>移动登录页面生成器</td>
   <td>文件模式</td>
   <td>登陆页构建器可配置为处理与由文件模式定义的常规表达式匹配的HTML文件。</td>
  </tr>
  <tr>
   <td> </td>
   <td>设备组</td>
   <td>要提供支持的设备组列表。</td>
  </tr>
  <tr>
   <td>登录页面条目处理器</td>
   <td>搜索模式 </td>
   <td>用于在归档条目内容中进行搜索的模式。此常规表达式与条目内容逐行匹配。 匹配后，匹配文本将替换为指定的替换模式。<br /><br />请参阅下方有关登录页面条目处理器当前限制的注释。</td>
  </tr>
  <tr>
   <td> </td>
   <td>替换模式</td>
   <td>替换找到的匹配项的模式。您可以使用正则表达式组引用，如$1、$2。 此外，此模式还支持在导入过程中用实际值解析的关键字，如{designPath}。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>**登录页面条目处理器的当前限制：**
>如果需要对搜索模式做任何更改，则在打开 felix 属性编辑器时，需要手动添加反斜杠字符，以对正则表达式元字符进行转义。如果未手动添加反斜杠字符，正则表达式将被视为无效，而不会替换旧的正则表达式。
>
>例如，如果默认配置为
>`/\* *CQ_DESIGN_PATH *\*/ *(['"])`
>
>而且你需要 >`CQ_DESIGN_PATH` 在搜索模式下，搜索模式应当如下：`VIPURL`
`/\* *VIPURL *\*/ *(['"])`

## 疑难解答 {#troubleshooting}

导入设计包时，可能会遇到此部分介绍的若干错误。

### 使用登录页面相关的组件初始化 Sidekick  {#initialization-of-sidekick-with-landing-page-relevant-components}

如果设计包包含 parsys 组件标记，则在导入后，Sidekick 开始显示登录页面相关的组件。您可以将新组件拖放到登录页面内的 parsys 组件上。还可以转到设计模式，将新组件添加到 Sidekick。

### 导入过程中显示的错误消息 {#error-messages-displayed-during-import}

如果出现任何错误（例如，导入的包不是有效的zip文件），设计导入将不会导入包，而是在页面顶部的拖放框正上方显示错误消息。 下面描述了一些错误情况的示例。更正错误之后，可以将更新的 zip 重新导入到同一空白登录页面上。引发错误的各种情况如下：

* 导入的设计包不是有效的 zip 归档。
* 导入的设计包顶级不包含index.html。

### 导入后显示警告 {#warnings-displayed-after-import}

如果出现任何警告（例如，HTML引用包中不存在的图像），设计导入程序将导入zip文件，但同时在结果窗格上显示一列表问题／警告，单击问题链接，将显示一列表警告，指出设计包中的任何问题。 设计导入程序捕获并显示警告的不同情况如下：

* HTML引用包中不存在的图像。
* HTML引用包中不存在的脚本。
* HTML引用包中不存在的样式。

### ZIP文件的文件存储在AEM中的哪些位置？{#where-are-the-files-of-the-zip-file-being-stored-in-aem}

登录页面导入之后，设计包中的文件（图像、css、js，等等）存储在AEM的以下位置：

`/etc/designs/default/canvas/content/campaigns/<name of brand>/<name of campaign>/<name of landing page>`

假定登陆页是在活动We.Retail下创建的，登陆页的名称为&#x200B;**myBlankLandingPage**，则存储Zip文件的位置如下：

`/etc/designs/default/canvas/content/campaigns/geometrixx/myBlankLandingPage`

### 格式设置无法保留 {#formatting-not-preserved}

创建 CSS 时，请注意以下限制：

如果文本和（可编辑）图像类似于以下内容：

```xml
<div class="box">
<p><div data-cq-component="image"><img src="assets/image.jpg" width="115"
height="116" /></div>Some Text </p>
</div>
```

对类`box`应用CSS，如下所示：

```xml
.box

{ width: 450px; padding:10px; border: 1px #C5DBE7 solid; margin: 0px auto 0 auto; background-image:url(assets/box.gif); background-repeat:repeat-x,y; font-family:Verdana, Arial, Helvetica, sans-serif; font-size:12px; color:#6D6D6D; }
```

然后，设计导入程序中使用`box img`，结果登陆页似乎未保留格式。 要解决该问题，请注意，AEM 在 CSS 中添加了 div 标记，请相应地重写代码。否则，有些 CSS 规则将无效。

```xml
.box img

{ float:right; margin: 0 0 5px 5px; border: 1px #343434 solid; }
```

>[!NOTE]
此外，设计人员应注意，导入程序只识别&#x200B;**id=cqcanvas**&#x200B;标记内的代码，否则不会保留设计。

