---
title: 网页的响应式设计
description: 通过响应式设计，可以在多个设备上以多个方向有效地显示相同的页面。
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '5375'
ht-degree: 0%

---

# 网页的响应式设计{#responsive-design-for-web-pages}

>[!NOTE]
>
>AdobeSPA建议对需要基于单页应用程序框架的客户端渲染(例如 _React_)。 [了解详情](/help/sites-developing/spa-overview.md).
>

>[!NOTE]
>
>各种示例都基于Geometrixx示例内容，AEM (Adobe Experience Manager)不再附带该内容，已被We.Retail取代。 查看文档 [We.Retail参考实施](/help/sites-developing/we-retail.md#we-retail-geometrixx) 了解如何下载和安装Geometrixx。

设计网页，使其适应显示它们的客户端视区。 通过响应式设计，可以在多个设备上在两个方向上有效地显示相同的页面。 下图演示了页面响应视区大小更改的一些方式：

* 布局：对较小的视区使用单列布局，对较大的视区使用多列布局。
* 文本大小：在较大的视区中使用较大的文本大小（如果适用，例如标题）。
* 内容：在较小的设备上显示时，仅包含最重要的内容。
* 导航：提供了特定于设备的工具来访问其他页面。
* 图像：提供适用于客户端视区的图像演绎版。 视窗尺寸而定。

![chlimage_1-4](assets/chlimage_1-4a.png)

开发可生成适应多种窗口大小和方向的HTML5页面的Adobe Experience Manager (AEM)应用程序。 例如，以下视区宽度范围对应于各种设备类型和方向

* 最大宽度480像素（手机、纵向）
* 最大宽度767像素（手机、横向）
* 宽度在768像素和979像素之间（平板电脑、纵向）
* 宽度在980像素和1199像素之间（平板电脑、横向）
* 宽度1200像素或更高（桌面）

有关实施响应式设计行为的信息，请参阅以下主题：

* [媒体查询](/help/sites-developing/responsive.md#using-media-queries)
* [流式网格](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [自适应图像](/help/sites-developing/responsive.md#using-adaptive-images)

在设计时，使用 **[!UICONTROL Sidekick]** 以预览各种屏幕大小的页面。

## 在开发之前 {#before-you-develop}

在开发支持网页的AEM应用程序之前，需要做出一些设计决策。 例如，您必须具有以下信息：

* 您定位的设备。
* 目标视区大小。
* 每个目标视区大小的页面布局。

### 应用程序结构 {#application-structure}

典型的AEM应用程序结构支持所有响应式设计实施：

* 页面组件位于/apps/下&#x200B;*application_name*/components
* 模板位于/apps/下&#x200B;*application_name*/templates
* 设计位于/etc/designs之下

## 使用媒体查询 {#using-media-queries}

媒体查询允许选择性地使用CSS样式进行页面渲染。 AEM开发工具和功能使您能够有效、高效地在应用程序中实施媒体查询。

W3C组提供 [媒体查询](https://www.w3.org/TR/mediaqueries-3/) 介绍此CSS3功能和语法的建议。

### 创建CSS文件 {#creating-the-css-file}

在CSS文件中，根据所定位设备的属性定义媒体查询。 以下实施策略可以有效地管理每个媒体查询的样式：

* 使用ClientLibraryFolder定义在渲染页面时汇编的CSS。
* 在单独的CSS文件中定义每个媒体查询和相关样式。 使用表示媒体查询的设备功能的文件名很有用。
* 在单独的CSS文件中定义所有设备通用的样式。
* 在ClientLibraryFolder的css.txt文件中，按照汇编的CSS文件中的要求对CSS文件列表进行排序。

此 `We.Retail` 媒体示例使用此策略来定义网站设计中的样式。 使用的CSS文件 `We.Retail` 位于 `*/apps/weretail/clientlibs/clientlib-site/less/grid.less`.

下表列出了css子文件夹中的文件。

<table>
 <tbody>
  <tr>
   <th>文件名</th>
   <th>描述</th>
   <th>媒体查询</th>
  </tr>
  <tr>
   <td>style.css</td>
   <td>通用样式。</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>通用样式，由TwitterBootstrap定义。</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>所有宽度或宽度为1200像素的媒体的样式。</td>
   <td><p>@media （最小宽度：1200像素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>宽度在980像素和1199像素之间的媒体的样式。</td>
   <td><p>@media （最小宽度：980像素）和（最大宽度：1199像素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>宽度在768像素和979像素之间的媒体的样式。 </td>
   <td><p>@media （最小宽度：768像素）和（最大宽度：979像素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>宽度小于768像素的所有媒体的样式。</td>
   <td><p>@media （max-width： 767像素） {<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>宽度小于481像素的所有媒体的样式。</td>
   <td>@media （max-width： 480像素） {<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

中的css.txt文件 `/etc/designs/weretail/clientlibs` 文件夹列出客户端库文件夹中包含的CSS文件。 文件的顺序实施样式优先级。 随着设备大小的减小，样式会更加具体。

`#base=css`

```
style.css
 bootstrap.css
```

```
responsive-1200px.css
 responsive-980px-1199px.css
 responsive-768px-979px.css
 responsive-767px-max.css
 responsive-480px.css
```

**笔尖**：通过描述性文件名，可轻松识别目标视区大小。

### 在AEM页面中使用媒体查询 {#using-media-queries-with-aem-pages}

在页面组件的JSP脚本中包含客户端库文件夹。 这样做有助于生成包含媒体查询并引用文件的CSS文件。

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>此 `apps.weretail.all` client library文件夹嵌入了clientlibs库。

JSP脚本生成引用样式表的以下HTML代码：

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## 预览特定设备 {#previewing-for-specific-devices}

查看不同视区大小的页面预览，以便测试响应式设计的行为。 In **[!UICONTROL 预览]** 模式， **[!UICONTROL Sidekick]** 包括 **[!UICONTROL 设备]** 用于选择设备的下拉菜单。 选择设备后，页面会根据视区大小进行相应更改。

![chlimage_1-5](assets/chlimage_1-5a.png)

在中启用设备预览 **[!UICONTROL Sidekick]**，您必须配置页面和 **[!UICONTROL MobileEmulatorProvider]** 服务。 另一个页面配置控制 **[!UICONTROL 设备]** 列表。

### 添加设备列表 {#adding-the-devices-list}

此 **[!UICONTROL 设备]** 列表显示于 **[!UICONTROL Sidekick]** 页面中包含的JSP脚本将渲染 **[!UICONTROL 设备]** 列表。 添加 **[!UICONTROL 设备]** 列表至 **[!UICONTROL Sidekick]**，包括 `/libs/wcm/mobile/components/simulator/simulator.jsp` 中的脚本 `head` 部分。

在JSP中包含以下代码，它定义 `head` 部分：

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

要查看示例，请打开 `/apps/weretail/components/page/head.jsp` 文件CRXDE Lite。

### 注册用于模拟的页面组件 {#registering-page-components-for-simulation}

要启用设备模拟器来支持页面，请使用MobileEmulatorProvider工厂服务注册页面组件，并定义 `mobile.resourceTypes` 属性。

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解完整的详细信息。

例如，创建 ` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)` 节点的位置：

* 父文件夹： `/apps/application_name/config`
* 名称: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

  此 —  `*alias*` 后缀是必需的，因为MobileEmulatorProvider服务是工厂服务。 使用对此工厂唯一的任何别名。

* jcr:primaryType: `sling:OsgiConfig`

添加以下节点属性：

* 名称: `mobile.resourceTypes`
* 类型: `String[]`
* 值：呈现网页的页面组件的路径。 例如， geometrixx-media应用程序使用以下值：

  ```
  geometrixx-media/components/page
   geometrixx-unlimited/components/pages/page
   geometrixx-unlimited/components/pages/coverpage
   geometrixx-unlimited/components/pages/issue
  ```

### 指定设备组 {#specifying-the-device-groups}

要指定显示在“设备”列表中的设备组，请添加 `cq:deviceGroups` 属性到 `jcr:content` 站点的根页面的节点。 属性的值是设备组节点的路径数组。

设备组节点位于 `/etc/mobile/groups` 文件夹。

例如，Geometrixx Media站点的根页面为 `/content/geometrixx-media`. 此 `/content/geometrixx-media/jcr:content` 节点包括以下属性：

* 名称: `cq:deviceGroups`
* 类型: `String[]`
* 价值: `/etc/mobile/groups/responsive`

使用“工具”控制台可以 [创建和编辑设备组](/help/sites-developing/groupfilters.md).

>[!NOTE]
>
>对于用于响应式设计的设备组，请编辑设备组，然后在“常规”选项卡上选择“禁用模拟器”。 此选项可防止出现与响应式设计无关的模拟器轮播。
>

## 使用自适应图像 {#using-adaptive-images}

您可以使用媒体查询来选择要显示在页面中的图像资源。 但是，使用媒体查询条件化其使用的每个资源都下载到客户端。 媒体查询仅确定是否显示下载的资源。

对于大型资源（如图像），下载所有资源不是有效使用客户端的数据管道。 要有选择地下载资源，请在媒体查询执行选择后使用JavaScript启动资源请求。

以下策略加载使用媒体查询选择的单个资源：

1. 为资源的每个版本添加一个DIV元素。 包括资源的URI作为属性值。 浏览器不会将属性解释为资源。
1. 向每个适用于资源的DIV元素添加媒体查询。
1. 当文档加载或窗口调整大小时，JavaScript代码测试每个DIV元素的媒体查询。
1. 根据查询结果，确定要包括的资源。
1. 在引用资源的DOM中插入一个HTML元素。

### 使用JavaScript评估媒体查询 {#evaluating-media-queries-using-javascript}

实施 [MediaQueryList接口](https://drafts.csswg.org/cssom-view/#the-mediaquerylist-interface) W3C定义的区域，使您能够使用JavaScript评估媒体查询。 您可以将逻辑应用于媒体查询结果，并执行针对当前窗口的脚本：

* 实施MediaQueryList接口的浏览器支持 `window.matchMedia()` 函数。 此函数针对给定的字符串测试媒体查询。 此函数返回 `MediaQueryList` 提供对查询结果的访问权限的对象。

* 对于未实施接口的浏览器，您可以使用 `matchMedia()` 多边形填充，例如 [matchmedia.js](https://github.com/paulirish/matchMedia.js)，这是一个免费提供的JavaScript库。

#### 选择特定于媒体的资源 {#selecting-media-specific-resources}

W3C [图片元素](https://html.spec.whatwg.org/multipage/embedded-content.html#the-picture-element) 使用媒体查询来确定用于图像元素的源。 图片元素使用元素属性将媒体查询与图像路径相关联。

免费提供 [picturefill.js库](https://github.com/scottjehl/picturefill) 提供与建议类似的功能 `picture` 元素，并使用类似的策略。 picturefill.js库调用 `window.matchMedia` 评估为一组媒体查询定义的媒体查询 `div` 元素。 每个 `div` element还指定图像源。 当的媒体查询时 `div` 元素返回 `true`.

此 `picturefill.js` 库需要类似于以下示例的HTML代码：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

渲染页面时，picturefull.js插入 `img` 元素作为的最后一个子项 `<div data-picture>` 元素：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

在AEM页面中， `data-src` attribute是存储库中资源的路径。

### 在AEM中实施自适应图像 {#implementing-adaptive-images-in-aem}

要在AEM应用程序中实施自适应图像，您必须添加所需的JavaScript库，并在页面中包含所需的HTML标记。

**库**

获取以下JavaScript库，并将其包含在客户端库文件夹中：

* [matchmedia.js](https://github.com/paulirish/matchMedia.js) （适用于未实施MediaQueryList接口的浏览器）
* [picturefill.js](https://github.com/scottjehl/picturefill)
* jquery.js(可通过 `/etc/clientlibs/granite/jquery` 客户端库文件夹（类别= jquery）
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) （调整窗口大小后出现一次的jquery事件）

**提示：** 您可以通过以下方式自动连接多个客户端库文件夹 [嵌入](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries).

**HTML**

创建一个组件，用于生成picturefill.js代码所需的所需div元素。 在AEM页中，data-src属性的值是存储库中资源的路径。 例如，页面组件可以硬编码媒体查询以及DAM中图像演绎版的相关路径。 或者，创建一个自定义图像组件，让作者可以选择图像演绎版或指定运行时渲染选项。

以下示例HTML从同一图像的两个DAM演绎版中进行选择。

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>自适应图像基础组件实施自适应图像：
>
>* 客户端库文件夹： `/libs/foundation/components/adaptiveimage/clientlibs`
>* 生成HTML的脚本： `/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`
>
>后续部分提供了有关此组件的详细信息。
>

### 了解AEM中的图像渲染 {#understanding-image-rendering-in-aem}

要自定义图像渲染，您应该了解默认的AEM静态图像渲染实施。 AEM提供图像组件和图像渲染servlet，二者可一起渲染网页的图像。 将图像组件包含在页面的段落系统中时，会发生以下事件序列：

1. 创作：作者可编辑图像组件，以指定要包含在HTML页中的图像文件。 文件路径将存储为图像组件节点的属性值。
1. Page request：Page组件的JSP生成HTML代码。 图像组件的JSP生成一个img元素并将其添加到页面中。
1. 图像请求：Web浏览器加载页面，并根据img元素的src属性请求图像。
1. 图像渲染：图像渲染servlet将图像返回到Web浏览器。

![chlimage_1-6](assets/chlimage_1-6a.png)

例如，图像组件的JSP生成以下HTML元素：

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

浏览器加载页面时，会使用src属性的值作为URL来请求图像。 Sling会解压缩URL：

* 资源: `/content/mywebsite/en/_jcr_content/par/image_0`
* 文件扩展名： `.jpg`
* 选择器: `img`
* 后缀: `1358372073597.jpg`

此 `image_0` 节点具有 `jcr:resourceType` 值 `foundation/components/image`，它具有 `sling:resourceSuperType` 值 `foundation/components/parbase`. parbase组件包含与请求URL的选择器和文件扩展名匹配的img.request.javaGET。 CQ使用此脚本(servlet)渲染图像。

要查看脚本的源代码，请使用CRXDE Lite打开 `/libs/foundation/components/parbase/img.GET.java`
文件。

## 根据当前视区大小缩放图像 {#scaling-images-for-the-current-viewport-size}

在运行时根据客户端视区的特性缩放图像，以提供符合响应式设计原则的图像。 使用与静态图像渲染相同的设计模式，使用servlet和创作组件。

该组件必须执行以下任务：

* 将图像资源的路径和所需尺寸存储为属性值。
* 生成 `div` 包含用于渲染图像的媒体选择器和服务调用的元素。

>[!NOTE]
>
>Web客户端使用matchMedia和Picturefill JavaScript库（或类似的库）来评估媒体选择器。
>

处理图像请求的servlet必须执行以下任务：

* 从组件属性中检索图像的路径和尺寸。
* 根据属性缩放图像并返回图像。

**可用的解决方案**

AEM将安装以下实施，您可以使用或扩展这些实施。

* 生成媒体查询的自适应图像基础组件，以及对缩放图像的自适应图像组件Servlet的HTTP请求。
* GeometrixxCommons软件包安装可改变图像分辨率的图像引用修改Servlet示例servlet。

### 了解自适应图像组件 {#understanding-the-adaptive-image-component}

自适应图像组件生成对自适应图像组件Servlet的调用，以渲染根据设备屏幕调整大小的图像。 该组件包括以下资源：

* JSP：添加将媒体查询与对自适应图像组件Servlet的调用关联的div元素。
* 客户端库： clientlibs文件夹是 `cq:ClientLibraryFolder` 用于组合matchMedia polyfill JavaScript库和修改后的Picturefill JavaScript库。
* “编辑”对话框： `cq:editConfig` 节点覆盖CQ foundation图像组件，以便放置目标创建自适应图像组件，而不是基础图像组件。

#### 添加DIV元素 {#adding-the-div-elements}

adaptive-image.jsp脚本包含以下用于生成div元素和媒体查询的代码：

```
<div data-picture data-alt='<%= alt %>'>
    <div data-src='<%= path + ".img.320.low." + extension + suffix %>'       data-media="(min-width: 1px)"></div>                                        <%-- Small mobile --%>
    <div data-src='<%= path + ".img.320.medium." + extension + suffix %>'    data-media="(min-width: 320px)"></div>  <%-- Portrait mobile --%>
    <div data-src='<%= path + ".img.480.medium." + extension + suffix %>'    data-media="(min-width: 321px)"></div>  <%-- Landscape mobile --%>
    <div data-src='<%= path + ".img.476.high." + extension + suffix %>'      data-media="(min-width: 481px)"></div>   <%-- Portrait iPad --%>
    <div data-src='<%= path + ".img.620.high." + extension + suffix %>'      data-media="(min-width: 769px)"></div>  <%-- Landscape iPad --%>
    <div data-src='<%= path + ".img.full.high." + extension + suffix %>'     data-media="(min-width: 1025px)"></div> <%-- Desktop --%>

    <%-- Fallback content for non-JS browsers. Same img src as the initial, unqualified source element. --%>
    <noscript>
        <img src='<%= path + ".img.320.low." + extension + suffix %>' alt='<%= alt %>'>
    </noscript>
</div>
```

此 `path` 变量包含当前资源的路径（自适应图像组件节点）。 该代码会生成一系列 `div` 元素具有以下结构：

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

的值 `data-scr` 属性是Sling解析为渲染图像的自适应图像组件Servlet的URL。 data-media属性包含根据客户端属性评估的媒体查询。

以下HTML代码是 `div` jsp生成的元素：

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### 更改图像大小选择器 {#changing-the-image-size-selectors}

如果自定义自适应图像组件并更改宽度选择器，则还必须配置自适应图像组件Servlet以支持宽度。

### 了解自适应图像组件Servlet {#understanding-the-adaptive-image-component-servlet}

自适应图像组件Servlet根据指定的宽度调整JPEG图像的大小，并设置JPEG质量。

#### 自适应图像组件Servlet的界面 {#the-interface-of-the-adaptive-image-component-servlet}

自适应图像组件Servlet绑定到默认的Sling servlet，并支持.jpg、.jpeg、.gif和.png文件扩展名。 servlet选择器为img。

>[!CAUTION]
>
>AEM for adaptive renditions不支持动画.gif文件。

因此，Sling将以下格式的HTTP请求URL解析为此servlet：

`*path-to-node*.img.*extension*`

例如，Sling使用URL转发HTTP请求 `http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg` 到自适应图像组件Servlet。

另外两个选择器指定请求的图像宽度和JPEG质量。 以下示例请求的图像宽度为480像素，质量适中：

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**支持的图像属性**

此servlet接受有限数量的图像宽度和品质。 默认支持以下宽度（以像素为单位）：

* 全部
* 320
* 480
* 476
* 620

完整值表示无缩放。

支持以下JPEG质量值：

* 低
* 中
* 高

数值分别为0.4、0.82和1.0。

**更改默认支持的宽度**

使用Web控制台([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))或sling：OsgiConfig节点，以配置Adobe CQ自适应图像组件Servlet支持的宽度。

有关如何配置AEM服务的信息，请参见 [配置OSGi](/help/sites-deploying/configuring-osgi.md).

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Web控制台</th>
   <th>sling：OsgiConfig</th>
  </tr>
  <tr>
   <th>服务或节点名称</th>
   <td>“配置”选项卡上的服务名称为Adobe CQ自适应图像组件Servlet</td>
   <td>com.day.cq.wcm.foundation.impl. AdaptiveImageComponentServlet</td>
  </tr>
  <tr>
   <th>属性</th>
   <td><p>支持的宽度</p>
    <ul>
     <li>要添加支持的宽度，请单击+按钮并输入正整数。</li>
     <li>要删除支持的宽度，请单击关联的 — 按钮。</li>
     <li>要修改支持的宽度，请编辑字段值。</li>
    </ul> </td>
   <td><p>adapt.supported.widths</p>
    <ul>
     <li>属性是一个多值字符串值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 实施详细信息 {#implementation-details}

此 `com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet` 类扩展 [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 类。 AdaptiveImageComponentServlet源代码位于 `/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl` 文件夹。

类使用Felix SCR注释来配置与servlet关联的资源类型和文件扩展名，以及第一个选择器的名称。

```java
@Component(metatype = true, label = "Adobe CQ Adaptive Image Component Servlet",
        description = "Render adaptive images in a variety of qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = "foundation/components/adaptiveimage", propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "img", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value ={
            "jpg",
            "jpeg",
            "png",
            "gif"
    }, propertyPrivate = true)
})
```

此servlet使用属性SCR注释来设置默认支持的图像质量和尺寸。

```java
@Property(value = {
            "320", // iPhone portrait
            "480", // iPhone landscape
            "476", // iPad portrait
            "620" // iPad landscape
    },
            label = "Supported Widths",
            description = "List of widths this component is permitted to generate.")
```

此 `AbstractImageServlet` 类提供 `doGet` 处理HTTP请求的方法。 此方法确定与请求关联的资源，从存储库中检索资源属性，并将它们返回到 [Imagecontext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 对象。

>[!NOTE]
>
>此 [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) 类提供 `getFileReference method`，以检索资源的 `fileReference` 属性。

此 `AdaptiveImageComponentServlet` 类覆盖 `createLayer` 方法。 该方法从获取图像资源的路径和请求的图像宽度 `ImageContext` 对象。 然后，它会调用 `info.geometrixx.commons.impl.AdaptiveImageHelper` 类执行实际的图像缩放。

AdaptiveImageComponentServlet类也会覆盖writeLayer方法。 此方法将JPEG质量应用于图像。

### 图像引用修改Servlet(常用Geometrixx) {#image-reference-modification-servlet-geometrixx-common}

示例图像引用修改Servlet生成图像元素的大小属性，以缩放网页上的图像。

#### 调用servlet {#calling-the-servlet}

此servlet绑定到 `cq:page` 资源和支持.jpg文件扩展名。 servlet选择器为 `image`. 因此，Sling将以下格式的HTTP请求URL解析为此servlet：

`path-to-page-node.image.jpg`

例如，Sling使用URL转发HTTP请求 `http://localhost:4502/content/geometrixx/en.image.jpg` 到图像引用修改Servlet。

另外三个选择器指定请求的图像宽度、高度和（可选）质量。 以下示例请求宽度770像素、高度360像素和中等质量的图像。

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**支持的图像属性**

此servlet接受有限数量的图像维度和质量值。

默认情况下，支持以下值(widthxheight)：

* 256x192
* 370x150
* 480x200
* 127x127
* 770x360
* 620x290
* 480x225
* 320x150
* 375x175
* 303x142
* 1170x400
* 940x340
* 770x300
* 480x190

支持以下图像质量值：

* 低
* 中
* 高

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解完整的详细信息。

#### 指定图像资源 {#specifying-the-image-resource}

图像路径、尺寸和质量值必须作为存储库中节点的属性存储：

* 节点名称为 `image`.
* 父节点为 `jcr:content` 节点 `cq:page` 资源。

* 图像路径存储为名为的属性的值 `fileReference`.

创作页面时，使用 **Sidekick** 以指定图像并添加 `image` 节点到页面属性：

1. In **Sidekick**，单击 **页面** 选项卡，然后单击 **页面属性**.
1. 单击 **图像** 制表符并指定图像。
1. 单击&#x200B;**确定**。

#### 实施详细信息 {#implementation-details-1}

info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet类扩展 [AbstractImageServlet](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html) 类。 如果您安装了cq-geometrixx-commons-pkg软件包，则ImageReferenceModificationServlet源代码位于 `/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets` 文件夹。

类使用Felix SCR注释来配置与servlet关联的资源类型和文件扩展名，以及第一个选择器的名称。

```java
@Component(metatype = true, label = "Adobe CQ Image Reference Modification Servlet",
        description = "Render the image associated with a page in a variety of dimensions and qualities")
@Service
@Properties(value = {
    @Property(name = "sling.servlet.resourceTypes", value = NameConstants.NT_PAGE, propertyPrivate = true),
    @Property(name = "sling.servlet.selectors", value = "image", propertyPrivate = true),
    @Property(name = "sling.servlet.extensions", value = "jpg", propertyPrivate = true)
})
```

此servlet使用属性SCR注释来设置默认支持的图像质量和尺寸。

```java
@Property(label = "Image Quality",
            description = "Quality must be a double between 0.0 and 1.0", value = "0.82")
@Property(value = {
                "256x192", // Category page article list images
                "370x150", // "Most popular" desktop & iPad & carousel min-width: 1px
                "480x200", // "Most popular" phone
                "127x127", // article summary phone square images
                "770x360", // article summary, desktop
                "620x290", // article summary, tablet
                "480x225", // article summary, phone (landscape)
                "320x150", // article summary, phone (portrait) and fallback
                "375x175", // 2-column article summary, desktop
                "303x142", // 2-column article summary, tablet
                "1170x400", // carousel, full
                "940x340",  // carousel min-width: 980px
                "770x300",  // carousel min-width: 768px
                "480x190"   // carousel min-width: 480px
            },
            label = "Supported Resolutions",
            description = "List of resolutions this component is permitted to generate.")
```

此 `AbstractImageServlet` 类提供 `doGet` 处理HTTP请求的方法。 此方法确定与调用关联的资源，从存储库中检索资源属性，并将它们保存在 [Imagecontext](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html) 对象。

此 `ImageReferenceModificationServlet` 类覆盖 `createLayer` 方法和实现了确定要渲染的图像资源的逻辑。 方法检索页面的子节点 `jcr:content` 节点已命名 `image`. An [图像](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/Image.html) 对象是从此处创建的 `image` 节点，以及 `getFileReference` 方法返回图像文件的路径，从 `fileReference` 图像节点的属性。

>[!NOTE]
>此 [com.day.cq.commons.DownloadResource](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/DownloadResource.html) 类提供getFileReferencemethod。
>

## 开发流体网格 {#developing-a-fluid-grid}

AEM使您能够高效实施流式网格。 本页说明如何集成流动网格或现有网格实施(例如 [Bootstrap](https://github.com/topics/twitter-bootstrap?l=css))添加到您的AEM应用程序。

如果您不熟悉流体网格，请参阅 [流式网格简介](/help/sites-developing/responsive.md#developing-a-fluid-grid) 部分（位于本页底部）。 本文对流体网格进行了概述，为流体网格的设计提供了指导。

### 使用页面组件定义网格 {#defining-the-grid-using-a-page-component}

使用页面组件可生成定义页面的HTML块的内容元素。 页面引用的ClientLibraryFolder提供了控制内容块布局的CSS：

* 页面组件：添加表示内容块行的div元素。 表示内容块的div元素包括一个parsys组件，作者可在其中添加内容。
* 客户端库文件夹：提供CSS文件，该文件包含div元素的媒体查询和样式。

例如，示例geometrixx-media应用程序包含media-home组件。 此页面组件插入两个脚本，这两个脚本将生成两个 `div` 类的元素 `row-fluid`：

* 第一行包含 `div` 类的元素 `span12` （内容跨越12列）。 此 `div` 元素包含parsys组件。

* 第二行包含两个 `div` 元素，类之一 `span8` 和班上的另一个 `span4`. 每个 `div` 元素包含parsys组件。

```xml
<div class="page-content">
    <div class="row-fluid">
        <div class="span12">
            <cq:include path="grid-12-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
    <div class="row-fluid">
        <div class="span8">
            <cq:include path="grid-8-par" resourceType="foundation/components/parsys" />
        </div>
        <div class="span4">
            <cq:include path="grid-4-par" resourceType="foundation/components/parsys" />
        </div>
    </div>
</div>
```

>[!NOTE]
>
>当组件包含多个时 `cq:include` 引用parsys组件的元素，每个 `path` 特性必须具有不同的值。
>

#### 缩放页面组件网格 {#scaling-the-page-component-grid}

与geometrixx-media页面组件关联的设计(`/etc/designs/geometrixx-media`)包含 `clientlibs` ClientLibraryFolder。 此ClientLibraryFolder定义 `row-fluid` 类， `span*` 类，以及 `span*` 作为子项的类 `row-fluid` 类。 通过媒体查询，可以为不同的视区大小重新定义样式。

以下示例CSS是这些样式的子集。 此子集侧重于 `span12`， `span8`、和 `span4` 类以及两种视区大小的媒体查询。 请注意CSS的以下特征：

* 此 `.span` 样式使用绝对数字定义元素宽度。
* 此 `.row-fluid .span*` 样式将元素宽度定义为父项的百分比。 百分比由绝对宽度计算。
* 较大视区的媒体查询分配较大的绝对宽度。

>[!NOTE]
>
>Geometrixx Media示例集成了 [Bootstrap](https://getbootstrap.com/2.0.2/) 将JavaScript框架融入到其流网格中实现。 Bootstrap框架提供bootstrap.css文件。

```xml
/* default styles (no media queries) */
 .span12 { width: 940px }
 .span8 { width: 620px }
 .span4 { width: 300px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.95744680851064% }
 .row-fluid .span4 { width: 31.914893617021278% }

@media (min-width: 768px) and (max-width: 979px) {
 .span12 { width: 724px; }
 .span8 {     width: 476px; }
 .span4 {     width: 228px; }
 .row-fluid .span12 {     width: 100%;}
 .row-fluid .span8 {     width: 65.74585635359117%; }
 .row-fluid .span4 {     width: 31.491712707182323%; }
}

@media (min-width: 1200px) {
 .span12 { width: 1170px }
 .span8 { width: 770px }
 .span4 { width: 370px }
 .row-fluid .span12 { width: 100% }
 .row-fluid .span8 { width: 65.81196581196582% }
 .row-fluid .span4 { width: 31.623931623931625% }
}
```

#### 在页面组件网格中重新定位内容 {#repositioning-content-in-the-page-component-grid}

示例Geometrixx Media应用程序的页面在宽视区中水平分布内容块行。 在较小的视区中，相同的块垂直分布。 以下示例CSS显示了为media-home页面组件生成的HTML代码实施此行为的样式：

* media-welcome页面的默认CSS分配 `float:left` 样式 `span*` 类位于内部 `row-fluid` 类。

* 较小视区的媒体查询分配 `float:none` 相同类的样式。

```xml
/* default styles (no media queries) */
    .row-fluid [class*="span"] {
        width: 100%;
        float: left;
}

@media (max-width: 767px) {
    [class*="span"], .row-fluid [class*="span"] {
        float: none;
        width: 100%;
    }
}
```

#### 将页面组件模块化 {#tip-modularize-your-page-components}

将组件模块化，以便高效地使用代码。 您的网站可能会使用多种不同类型的页面，例如欢迎页面、文章页面或产品页面。 每种类型的页面包含不同类型的内容，并且可能使用不同的布局。 但是，当每个布局的某些元素在多个页面中很共有时，您可以重用实施该部分布局的代码。

**使用页面组件叠加图**

创建一个主页组件，该组件提供用于生成页面的各个部分的脚本，例如 `head` 和 `body` 部分，和 `header`， `content`、和 `footer` 部分。

创建使用主页组件作为的其他页面组件 `cq:resourceSuperType`. 这些组件包括根据需要覆盖主页的脚本的脚本。

例如，goemetrixx-media应用程序包含页面组件( `sling:resourceSuperType` 是基础页面组件)。 多个子组件（例如article、category和media-home）使用此页面组件作为 `sling:resourceSuperType`. 每个子组件都包含一个content.jsp文件，该文件会覆盖页面组件的content.jsp文件。

**重用脚本**

创建多个JSP脚本，这些脚本可生成多个页面组件通用的行和列组合。 例如， `content.jsp` 文章的脚本和media-home组件都引用 `8x4col.jsp` 脚本。

**按目标视区大小组织CSS样式**

在单独的文件中包含不同视区大小的CSS样式和媒体查询。 使用客户端库文件夹连接它们。

### 将组件插入页面网格 {#inserting-components-into-the-page-grid}

当组件生成单个内容块时，通常页面组件建立的网格控制内容的放置。

作为作者，内容块可以呈现为各种大小和相对位置。 内容文本不应使用相对方向来引用其他内容块。

如有必要，组件应提供其生成的HTML代码所需的任何CSS或JavaScript库。 在组件内使用客户端库文件夹，以便生成CSS和JS文件。 要公开这些文件， [创建依赖项或嵌入库](/help/sites-developing/clientlibs.md#creating-client-library-folders) /etc文件夹下的另一个客户端库文件夹中。

**子网格**

如果组件包含多个内容块，请在行中添加内容块以在页面上建立子网格：

* 使用与包含页面组件相同的类名，以便您可以将div元素表示为行和内容块。
* 要覆盖页面设计CSS实施的行为，请为row div元素使用第二个类名称，并在客户端库文件夹中提供关联的CSS。

例如， `/apps/geometrixx-media/components/2-col-article-summary` 组件生成两列内容。 它生成的HTML具有以下结构：

```xml
<div class="row-fluid mutli-col-article-summary">
    <div class="span6">
        <article>
            <div class="article-summary-image">...</div>
            <div class="social-header">...</div>
            <div class="article-summary-description">...</div>
            <div class="social">...</div>
        </article>
    </div>
</div>
```

此 `.row-fluid .span6` 页面CSS的选择器适用于 `div` 此HTML中相同类和结构的元素。 但是，该组件还包括/apps/geometrixx-media/components/2-col-article-summary/clientlibs客户端库文件夹：

* CSS使用与页面组件相同的媒体查询，以在相同的离散页面宽度处建立布局更改。
* 选择器使用 `multi-col-article-summary` 行的类 `div` 元素覆盖页面的 `row-fluid` 类。

例如，以下样式包含在 `/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css` 文件：

```xml
@media (max-width: 480px) {
    .mutli-col-article-summary .article-summary-image {
        float: left;
        width: 127px;
    }
    .mutli-col-article-summary .article-summary-description {
        width: auto;
        margin-left: 127px;
    }
    .mutli-col-article-summary .article-summary-description h4 {
        padding-left: 10px;
    }
    .mutli-col-article-summary .article-summary-text {
        margin-left: 127px;
        min-height: 122px;
        top: 0;
    }
}
```

## 流式网格简介 {#introduction-to-fluid-grids}

流式网格使页面布局能够适应客户端视区的维度。 网格由逻辑列和在页面上放置内容块的行组成。

* 列确定内容块的水平位置和宽度。
* 行确定内容块的相对垂直位置。

使用HTML5技术，您可以实施网格并操作它以根据不同的视区大小调整页面布局：

* HTML `div` 元素包含跨越某些列的内容块。
* 当这些div元素中的一个或多个共享公共的父div元素时，它们构成一行。

### 使用离散宽度 {#using-discrete-widths}

对于要定位的每个视区宽度范围，请使用静态页面宽度和固定宽度的内容块。 手动调整浏览器窗口大小时，内容大小的更改发生在离散的窗口宽度（也称为断点）。 因此，页面设计将更紧密地粘合，从而最大化用户体验。

#### 缩放网格 {#scaling-the-grid}

使用网格来缩放内容块，以适应不同的视区大小。 内容块跨越特定数量的列。 随着列宽度的增加或减少以适合不同的视区大小，内容块的宽度将相应地增加或减少。 缩放功能可以支持宽到足以容纳并排放置内容块的大中型视区。

![两个网格的图像，一个网格的缩放比例小于另一个网格。](do-not-localize/chlimage_1-1a.png)

#### 在网格中重新定位内容 {#repositioning-content-in-the-grid}

内容块的大小可以通过最小宽度来限制，超过该宽度缩放不再有效。 对于较小的视区，可以使用网格垂直分布内容块，而不是水平分布。

![两个网格的图像，其中一个网格被重新定位得小于另一个网格。](do-not-localize/chlimage_1-2a.png)

### 设计网格 {#designing-the-grid}

确定必须在页面上放置内容块的列和行。 页面布局决定了网格中跨越的列数和行数。

**列数**

包含足够的列，以便在所有版面中水平放置内容块（对于所有视区大小）。 使用的列数超过当前所需的列数，以便适应未来的页面设计。

**行内容**

使用行控制内容块的垂直位置。 确定共享同一行的内容块：

* 在任何布局中，水平放置彼此相邻的内容块位于同一行中。
* 水平（较宽的视区）和垂直（较小的视区）彼此相邻的内容块位于同一行中。

### 网格实施 {#grid-implementations}

创建CSS类和样式，以便您可以控制页面上内容块的布局。 页面设计通常基于视区中内容块的相对大小和位置。 视区确定内容块的实际大小。 CSS必须考虑相对大小和绝对大小。 您可以使用三种类型的CSS类实施流式网格：

* 一个类 `div` 元素作为所有行的容器。 此类设置网格的绝对宽度。
* 的类 `div` 表示行的元素。 此类控制其包含的内容块的水平或垂直位置。
* 类别 `div` 表示不同宽度内容块的元素。 宽度以父项（行）的百分比表示。

目标视区宽度（及其相关媒体查询）可区分用于页面布局的离散宽度。

#### 内容块的宽度 {#widths-of-content-blocks}

一般而言， `width` 内容块类的样式基于页面和网格的以下特征：

* 您对每个目标视区大小使用的绝对页面宽度。 已知值。
* 每个页面宽度的网格列的绝对宽度。 您可以确定这些值。
* 每列的相对宽度，以总页面宽度的百分比表示。 您可以计算这些值。

CSS包含一系列使用以下结构的媒体查询：

```xml
@media(query_for_targeted_viewport){

  .class_for_container{ width:absolute_page_width }
  .class_for_row { width:100%}

  /* several selectors for content blocks   */
  .class_for_content_block1 { width:absolute_block_width1 }
  .class_for_content_block2 { width:absolute_block_width2 }
  ...

  /* several selectors for content blocks inside rows */
  .class_for_row .class_for_content_block1 { width:relative_block_width1 }
  .class_for_row .class_for_content_block2 { width:relative_block_width2 }
  ...
}
```

使用以下算法作为开发页面的元素类和CSS样式的起点。

1. 为包含所有行的div元素定义类名称，例如 `content.`
1. 为表示行的div元素定义CSS类，例如 `row-fluid`.
1. 定义内容块元素的类名。 所有可能的宽度（以列跨度为单位）都需要一个类。 例如，使用 `span3` 类 `div` 跨三列的元素，使用 `span4` 跨度为四列的类。 定义网格中列数的类数。

1. 对于要定位的每个视区大小，将相应的媒体查询添加到CSS文件中。 在每个媒体查询中添加以下项目：

   * 的选择器 `content` 类，例如 `.content{}`.
   * 每个span类的选择器，例如 `.span3{ }`.
   * 的选择器 `row-fluid` 类，例如 `.row-fluid{ }`
   * 位于行流类内部的跨类选择器，例如 `.row-fluid span3 { }`.

1. 为每个选择器添加宽度样式：

   1. 设置宽度 `content` 页面绝对大小的选择器，例如 `width:480px`.
   1. 将所有行流体选择器的宽度设置为100%。
   1. 将所有范围选择器的宽度设置为内容块的绝对宽度。 普通网格使用具有相同宽度的均匀分布的列： `(absolute width of page)/(number of columns)`.
   1. 设置宽度 `.row-fluid .span` 选择器占总宽度的百分比。 使用以下方式计算此宽度 `(absolute span width)/(absolute page width)*100` 公式。

#### 将内容块定位在行中 {#positioning-content-blocks-in-rows}

使用浮动样式 `.row-fluid` 类，以便您可以控制行中的内容块是水平排列还是垂直排列。

* 此 `float:left` 或 `float:right` style导致子元素（内容块）的水平分布。

* 此 `float:none` style导致子元素的垂直分布。

将样式添加到 `.row-fluid` 每个媒体查询中的选择器。 根据用于该媒体查询的页面布局设置值。 例如，下图说明了一个行，该行将宽视区水平分发内容，窄视区垂直分发内容。

![一行中有两个内容块的图像，第二张显示行的图像已重新定位。](do-not-localize/chlimage_1-3a.png)

以下CSS可以实施此行为：

```xml
@media (min-width: 768px) and (max-width: 979px) {
   .row-fluid {
       width:100%;
       float:left
   }
}

@media (max-width:480px){
    .row-fluid {
       width:100%;
       float:none
   }
}
```

#### 将类分配给内容块 {#assigning-classes-to-content-blocks}

对于要定位的每个视区大小的页面布局，请确定每个内容块跨越的列数。 然后，确定要用于这些内容块的div元素的类。

建立div类后，可以使用AEM应用程序实施网格。
