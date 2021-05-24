---
title: 网页响应式设计
seo-title: 网页响应式设计
description: 通过响应式设计，可以在多个设备上以多个方向有效地显示相同的页面
seo-description: 通过响应式设计，可以在多个设备上以多个方向有效地显示相同的页面
uuid: 3d324557-e7ff-4c82-920f-9b5a906925e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 532544b0-1932-419a-b6bd-ecf57a926fef
legacypath: /content/docs/en/aem/6-0/develop/mobile/responsive
exl-id: c705710b-a94a-4f4f-affa-ddd4fc6cb0ec
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5339'
ht-degree: 0%

---

# 网页响应式设计{#responsive-design-for-web-pages}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染的项目（例如&#x200B;_React_）使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。


设计网页，使其适应显示网页的客户端视区。 通过响应式设计，可以在多个设备上以两种方向有效地显示相同的页面。 下图演示了页面对视区大小更改做出响应的一些方式：

* 布局：对较小的视区使用单列布局，对较大的视区使用多列布局。
* 文本大小：在较大的视区中使用较大的文本大小（如果适用，如标题）。
* 内容：在较小的设备上显示时，仅包含最重要的内容。
* 导航：提供了用于访问其他页面的设备特定工具。
* 图像：提供适用于客户端视区的图像演绎版。 根据窗口尺寸。

![chlimage_1-4](assets/chlimage_1-4a.png)

开发Adobe Experience Manager(AEM)应用程序，以生成可适应多种窗口大小和方向的HTML5页面。 例如，以下视区宽度范围与各种设备类型和方向相对应

* 最大宽度为480像素（手机、纵向）
* 最大宽度767像素（手机、横向）
* 宽度介于768像素和979像素（平板电脑、纵向）之间
* 宽度介于980像素和1199像素之间（平板电脑、横向）
* 宽度为1200像素或更大（桌面）

有关实施响应式设计行为的信息，请参阅以下主题：

* [媒体查询](/help/sites-developing/responsive.md#using-media-queries)
* [流体网格](/help/sites-developing/responsive.md#developing-a-fluid-grid)
* [自适应图像](/help/sites-developing/responsive.md#using-adaptive-images)

在设计时，请使用&#x200B;**[!UICONTROL Sidekick]**&#x200B;来预览不同屏幕大小的页面。

## 在开发{#before-you-develop}之前

在开发支持网页的AEM应用程序之前，应先做出一些设计决策。 例如，您需要具有以下信息：

* 您定位的设备。
* 目标视区大小。
* 每个目标视区大小的页面布局。

### 应用程序结构{#application-structure}

典型的AEM应用程序结构支持所有响应式设计实施：

* 页面组件位于/apps/*application_name*/components下
* 模板位于/apps/*application_name*/templates下
* 设计位于/etc/designs下

## 使用媒体查询{#using-media-queries}

媒体查询允许选择性地使用CSS样式进行页面渲染。 AEM开发工具和功能使您能够高效地在应用程序中实施媒体查询。

W3C组提供了描述此CSS3功能和语法的[媒体查询](https://www.w3.org/TR/css3-mediaqueries/)推荐。

### 创建CSS文件{#creating-the-css-file}

在CSS文件中，根据定向设备的属性定义媒体查询。 以下实施策略对于管理每个媒体查询的样式非常有效：

* 使用ClientLibraryFolder定义呈现页面时组装的CSS。
* 在单独的CSS文件中定义每个媒体查询和关联的样式。 使用表示媒体查询设备功能的文件名时，此方法非常有用。
* 在单独的CSS文件中定义所有设备通用的样式。
* 在ClientLibraryFolder的css.txt文件中，按照组装的CSS文件中的要求对列表CSS文件进行排序。

We.Retail Media示例使用此策略来定义网站设计中的样式。 We.Retail使用的CSS文件位于`*/apps/weretail/clientlibs/clientlib-site/less/grid.less`。

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
   <td>常用样式。</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>bootstrap.css</td>
   <td>通用样式，由TwitterBootstrap定义。</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td>responsive-1200px.css</td>
   <td>所有宽或宽1200像素的媒体的样式。</td>
   <td><p>@media(最小宽度：1200px){<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-980px-1199px.css</td>
   <td>介于980像素和1199像素宽之间的媒体样式。</td>
   <td><p>@media(最小宽度：980px)和(最大宽度：1199px){<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-768px-979px.css</td>
   <td>介质的样式，宽度介于768像素和979像素之间。 </td>
   <td><p>@media(最小宽度：768px)和(最大宽度：979px){<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-767px-max.css</td>
   <td>所有媒体的样式宽度小于768像素。</td>
   <td><p>@media(最大宽度：767px){<br /> ...<br /> }</p> </td>
  </tr>
  <tr>
   <td>responsive-480px.css</td>
   <td>所有媒体的样式宽度小于481像素。</td>
   <td>@media(最大宽度：480){<br /> ...<br /> }</td>
  </tr>
 </tbody>
</table>

`/etc/designs/weretail/clientlibs`文件夹中的css.txt文件列出了客户端库文件夹包含的CSS文件。 文件的顺序实现样式优先级。 当设备大小减小时，样式会更加具体。

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

**提示**:使用描述性文件名可以轻松识别目标视区大小。

### 对AEM页面{#using-media-queries-with-aem-pages}使用媒体查询

将客户端库文件夹包含在页面组件的JSP脚本中，以生成包含媒体查询的CSS文件，并引用该文件。

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

>[!NOTE]
>
>`apps.weretail.all`客户端库文件夹嵌入了clientlibs库。

JSP脚本生成引用样式表的以下HTML代码：

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## 预览特定设备{#previewing-for-specific-devices}

以不同视区大小查看页面的预览，以测试响应式设计的行为。 在&#x200B;**[!UICONTROL 预览]**&#x200B;模式下， **[!UICONTROL Sidekick]**&#x200B;包含用于选择设备的&#x200B;**[!UICONTROL 设备]**&#x200B;下拉菜单。 当您选择设备时，页面会发生更改以适应视区大小。

![chlimage_1-5](assets/chlimage_1-5a.png)

要在&#x200B;**[!UICONTROL Sidekick]**&#x200B;中启用设备预览，必须配置页面和&#x200B;**[!UICONTROL MobileEmulatorProvider]**&#x200B;服务。 另一个页面配置控制显示在&#x200B;**[!UICONTROL Devices]**&#x200B;列表中的设备列表。

### 添加设备列表{#adding-the-devices-list}

当您的页面包含呈现&#x200B;**[!UICONTROL 设备]**&#x200B;列表的JSP脚本时，**[!UICONTROL 设备]**&#x200B;列表会显示在&#x200B;**[!UICONTROL Sidekick]**&#x200B;中。 要将&#x200B;**[!UICONTROL Devices]**&#x200B;列表添加到&#x200B;**[!UICONTROL Sidekick]**，请在页面的`head`部分包含`/libs/wcm/mobile/components/simulator/simulator.jsp`脚本。

在定义`head`部分的JSP中包含以下代码：

`<cq:include script="/libs/wcm/mobile/components/simulator/simulator.jsp"/>`

要查看示例，请以CRXDE Lite打开`/apps/weretail/components/page/head.jsp`文件。

### 注册页面组件以进行模拟{#registering-page-components-for-simulation}

要启用设备模拟器以支持您的页面，请使用MobileEmulatorProvider工厂服务注册您的页面组件，并定义`mobile.resourceTypes`属性。

使用AEM时，可通过多种方法来管理此类服务的配置设置；有关完整的详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

例如，要在应用程序中创建` [sling:OsgiConfig](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)`节点，请执行以下操作：

* 父文件夹：`/apps/application_name/config`
* 名称: `com.day.cq.wcm.mobile.core.impl.MobileEmulatorProvider-*alias*`

   - `*alias*`后缀是必需的，因为MobileEmulatorProvider服务是工厂服务。 使用此工厂特有的任何别名。

* jcr:primaryType: `sling:OsgiConfig`

添加以下节点属性：

* 名称: `mobile.resourceTypes`
* 类型: `String[]`
* 值：呈现网页的页面组件的路径。 例如，geometrixx-media应用程序使用以下值：

   ```
   geometrixx-media/components/page
    geometrixx-unlimited/components/pages/page
    geometrixx-unlimited/components/pages/coverpage
    geometrixx-unlimited/components/pages/issue
   ```

### 指定设备组{#specifying-the-device-groups}

要指定“设备”列表中显示的设备组，请将`cq:deviceGroups`属性添加到站点根页面的`jcr:content`节点。 属性的值是指向设备组节点的路径数组。

设备组节点位于`/etc/mobile/groups`文件夹中。

例如，Geometrixx Media站点的根页面为`/content/geometrixx-media`。 `/content/geometrixx-media/jcr:content`节点包含以下属性：

* 名称: `cq:deviceGroups`
* 类型: `String[]`
* 值: `/etc/mobile/groups/responsive`

使用“工具”控制台创建和编辑设备组](/help/sites-developing/groupfilters.md)。[

>[!NOTE]
>
>对于用于响应式设计的设备组，请编辑设备组，然后在“常规”选项卡中选择禁用模拟器。 此选项可防止显示模拟器轮播，这与响应式设计无关。


## 使用自适应图像{#using-adaptive-images}

您可以使用媒体查询选择要在页面中显示的图像资源。 但是，使用媒体查询条件化其使用的每个资源都会下载到客户端。 媒体查询仅确定是否显示下载的资源。

对于图像等大型资源，下载所有资源并不能有效地使用客户端的数据管道。 要有选择地下载资源，请在媒体查询执行选择后使用javascript启动资源请求。

以下策略会加载使用媒体查询选择的单个资源：

1. 为资源的每个版本添加一个DIV元素。 将资源的URI作为属性值包含在内。 浏览器不会将属性解释为资源。
1. 向每个适合该资源的DIV元素添加媒体查询。
1. 当文档加载或窗口大小调整时，javascript代码会测试每个DIV元素的媒体查询。
1. 根据查询结果确定要包含的资源。
1. 在引用资源的DOM中插入一个HTML元素。

### 使用Javascript {#evaluating-media-queries-using-javascript}评估媒体查询

通过W3C定义的[MediaQueryList界面](https://dev.w3.org/csswg/cssom-view/#the-mediaquerylist-interface)的实施，您可以使用Javascript评估媒体查询。 您可以将逻辑应用于媒体查询结果并执行针对当前窗口的脚本：

* 实施MediaQueryList接口的浏览器支持`window.matchMedia()`函数。 此函数针对给定字符串测试媒体查询。 函数返回一个`MediaQueryList`对象，用于提供对查询结果的访问。

* 对于不实施该界面的浏览器，您可以使用`matchMedia()`多填充，如[matchMedia.js](https://github.com/paulirish/matchMedia.js)，这是一个可免费使用的Javascript库。

#### 选择特定于媒体的资源{#selecting-media-specific-resources}

W3C建议的[图片元素](https://picture.responsiveimages.org/)使用媒体查询来确定要用于图像元素的源。 图片元素使用元素属性将媒体查询与图像路径关联。

可免费使用的[picturel.js库](https://github.com/scottjehl/picturefill)提供与建议的`picture`元素类似的功能，并且使用类似的策略。 picturepill.js库调用`window.matchMedia`以评估为一组`div`元素定义的媒体查询。 每个`div`元素还指定一个图像源。 当`div`元素的媒体查询返回`true`时，将使用源。

`picturefill.js`库需要与以下示例类似的HTML代码：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
</div>
```

呈现页面时，picturefull.js会插入一个`img`元素作为`<div data-picture>`元素的最后一个子元素：

```xml
<div data-picture>
    <div data-src='path to default image'></div>
    <div data-src='path to small image'    data-media="(media query for phone)"></div>
    <div data-src='path to medium image'   data-media="(media query for tablet)"></div>
    <div data-src='path to large image'     data-media="(media query for monitor)"></div>
    <img src="path to medium image">
</div>
```

在AEM页面中，`data-src`属性的值是存储库中资源的路径。

### 在AEM {#implementing-adaptive-images-in-aem}中实施自适应图像

要在AEM应用程序中实施自适应图像，您需要添加所需的javascript库，并在页面中包含所需的HTML标记。

**库**

获取以下javascript库并将其包含在客户端库文件夹中：

* [matchMedia.js](https://github.com/paulirish/matchMedia.js) （适用于不实施MediaQueryList界面的浏览器）
* [picturepircl.js](https://github.com/scottjehl/picturefill)
* jquery.js(可通过`/etc/clientlibs/granite/jquery`客户端库文件夹(category = jquery)启用
* [jquery.debouncedresize.js](https://github.com/louisremi/jquery-smartresize) （一个在调整窗口大小后发生一次的jquery事件）

**提示：** 您可以通过嵌入来自动连接多个客户端库 [文件夹](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries)。

**HTML**

创建一个组件，以生成picturepirl.js代码所需的必需div元素。 在AEM页面中，data-src属性的值是存储库中资源的路径。 例如，页面组件可以在DAM中对媒体查询和图像呈现的关联路径进行硬编码。 或者，创建一个自定义图像组件，使作者能够选择图像演绎版或指定运行时渲染选项。

以下示例HTML从同一图像的2个DAM演绎版中进行选择。

```xml
<div data-picture>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png'></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.319.319.png'    data-media="(min-width: 769px)"></div>
    <div data-src='/content/dam/geometrixx-media/articles/meridien.png/jcr:content/renditions/cq5dam.thumbnail.140.100.png'   data-media="(min-width: 481px)"></div>
</div>
```

>[!NOTE]
>
>自适应图像基础组件可实施自适应图像：
>
>* 客户端库文件夹：`/libs/foundation/components/adaptiveimage/clientlibs`
>* 生成HTML的脚本：`/libs/foundation/components/adaptiveimage/adaptiveimage.jsp`

>
>
后续部分提供有关此组件的详细信息。


### 了解AEM {#understanding-image-rendering-in-aem}中的图像渲染

要自定义图像渲染，您应该了解默认的AEM静态图像渲染实施。 AEM提供了图像组件和图像渲染servlet，这两个组件可一起为网页渲染图像。 在页面的段落系统中包含图像组件时，会发生以下一系列事件：

1. 创作：作者编辑图像组件以指定要包含在HTML页面中的图像文件。 文件路径将存储为图像组件节点的属性值。
1. 页面请求：页面组件的JSP生成HTML代码。 图像组件的JSP会生成一个img元素并将其添加到该页面。
1. 图像请求：Web浏览器加载页面，并根据img元素的src属性请求图像。
1. 图像渲染：图像渲染Servlet将图像返回到Web浏览器。

![chlimage_1-6](assets/chlimage_1-6a.png)

例如，图像组件的JSP会生成以下HTML元素：

`<img title="My Image" alt="My Image" class="cq-dd-image" src="/content/mywebsite/en/_jcr_content/par/image_0.img.jpg/1358372073597.jpg">`

浏览器加载页面时，会使用src属性的值作为URL来请求图像。 Sling解构URL:

* 资源: `/content/mywebsite/en/_jcr_content/par/image_0`
* 文件扩展名：`.jpg`
* 选择器: `img`
* 后缀: `1358372073597.jpg`

`image_0`节点的`jcr:resourceType`值为`foundation/components/image`,`sling:resourceSuperType`值为`foundation/components/parbase`。 Parbase组件包含img.GET.java脚本，该脚本与请求URL的选择器和文件扩展名匹配。 CQ使用此脚本(servlet)呈现图像。

要查看脚本的源代码，请使用CRXDE Lite打开`/libs/foundation/components/parbase/img.GET.java`
文件。

## 按当前视区大小{#scaling-images-for-the-current-viewport-size}缩放图像

根据客户端视区的特性在运行时缩放图像，以提供符合响应式设计原则的图像。 使用与静态图像渲染相同的设计模式，即使用Servlet和创作组件。

组件需要执行以下任务：

* 将图像资源的路径和所需维度存储为属性值。
* 生成`div`元素，其中包含用于呈现图像的媒体选择器和服务调用。

>[!NOTE]
>
>Web客户端使用matchMedia和Picturerjavascript库（或类似库）来评估媒体选择器。


处理图像请求的Servlet需要执行以下任务：

* 从组件属性中检索图像的路径和尺寸。
* 根据属性缩放图像并返回图像。

**可用的解决方案**

AEM会安装以下可使用或扩展的实施。

* 可生成媒体查询的自适应图像基础组件，以及对可缩放图像的自适应图像组件Servlet的HTTP请求。
* Geometrixx共用包会安装可更改图像分辨率的图像引用修改Servlet示例Servlet。

### 了解自适应图像组件{#understanding-the-adaptive-image-component}

自适应图像组件生成对自适应图像组件Servlet的调用，以渲染根据设备屏幕大小调整的图像。 该组件包括以下资源：

* JSP:添加将媒体查询与对自适应图像组件Servlet的调用关联的div元素。
* 客户端库：clientlibs文件夹是一个`cq:ClientLibraryFolder`文件夹，用于组合matchMedia polyfill javascript库和修改后的Picturel javascript库。
* 编辑对话框：`cq:editConfig`节点会覆盖CQ基础图像组件，以便放置目标创建自适应图像组件，而不是基础图像组件。

#### 添加DIV元素{#adding-the-div-elements}

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

`path`变量包含当前资源的路径（自适应图像组件节点）。 该代码会生成一系列具有以下结构的`div`元素：

`<div data-scr = "*path-to-parent-node*.adaptive-image.adapt.*width*.*quality*.jpg" data-media="*media query*"></div>`

`data-scr`属性的值是一个URL，Sling会解析为可呈现图像的自适应图像组件Servlet。 data-media属性包含针对客户端属性评估的媒体查询。

以下HTML代码是JSP生成的`div`元素的一个示例：

```xml
<div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.low.jpg'></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.320.medium.jpg'    data-media="(min-width: 320px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.480.medium.jpg'    data-media="(min-width: 321px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.476.high.jpg'     data-media="(min-width: 481px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.620.high.jpg'     data-media="(min-width: 769px)"></div>
    <div data-src='/content/geometrixx-media/en/events/the-lineup-you-ve-been-waiting-for/jcr:content/article-content-par/adaptive_image.adapt.full.high.jpg'     data-media="(min-width: 1025px)"></div>
```

#### 更改图像大小选择器{#changing-the-image-size-selectors}

如果自定义自适应图像组件并更改宽度选择器，则还必须配置自适应图像组件Servlet以支持宽度。

### 了解自适应图像组件Servlet {#understanding-the-adaptive-image-component-servlet}

自适应图像组件Servlet根据指定的宽度调整JPEG图像的大小，并设置JPEG质量。

#### 自适应图像组件Servlet的接口{#the-interface-of-the-adaptive-image-component-servlet}

自适应图像组件Servlet绑定到默认的Sling Servlet，并支持.jpg、.jpeg、.gif和.png文件扩展名。 Servlet选择器是img。

>[!CAUTION]
>
>AEM不支持.gif动画文件进行自适应呈现。

因此，Sling会将以下格式的HTTP请求URL解析为此Servlet:

`*path-to-node*.img.*extension*`

例如，Sling会将URL为`http://localhost:4502/content/geometrixx/adaptiveImage.img.jpg`的HTTP请求转发到自适应图像组件Servlet。

另外两个选择器可指定请求的图像宽度和JPEG质量。 以下示例请求宽度为480像素且中等质量的图像：

`http://localhost:4502/content/geometrixx/adaptiveImage.adapt.480.MEDIUM.jpg`

**支持的图像属性**

Servlet接受有限数量的图像宽度和质量。 默认支持以下宽度（以像素为单位）：

* 全部
* 320
* 480
* 476
* 620

完整值表示无缩放。

支持JPEG质量的以下值：

* 低
* 中
* 高

数值分别为0.4、0.82和1.0。

**更改默认支持的宽度**

使用Web控制台([http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))或sling:OsgiConfig节点配置Adobe CQ自适应图像组件Servlet支持的宽度。

有关如何配置AEM服务的信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

<table>
 <tbody>
  <tr>
   <th> </th>
   <th>Web控制台</th>
   <th>sling:OsgiConfig</th>
  </tr>
  <tr>
   <th>服务或节点名称</th>
   <td>“配置”选项卡上的服务名称是Adobe CQ自适应图像组件Servlet</td>
   <td>com.day.cq.wcm.foundation.impl。 AdaptiveImageComponentServlet</td>
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
     <li>该属性是一个多值字符串值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

#### 实施详细信息{#implementation-details}

`com.day.cq.wcm.foundation.impl.AdaptiveImageComponentServlet`类扩展[AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html)类。 AdaptiveImageComponentServlet源代码位于`/libs/foundation/src/impl/src/com/day/cq/wcm/foundation/impl`文件夹中。

类使用Felix SCR注释配置Servlet关联的资源类型和文件扩展名以及第一个选择器的名称。

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

Servlet使用属性SCR注释设置默认支持的图像质量和尺寸。

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

`AbstractImageServlet`类提供处理HTTP请求的`doGet`方法。 此方法可确定与请求关联的资源，从存储库中检索资源属性，并在[ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html)对象中返回它们。

>[!NOTE]
>
>[com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html)类提供`getFileReference method`，用于检索资源`fileReference`属性的值。

`AdaptiveImageComponentServlet`类覆盖`createLayer`方法。 该方法从`ImageContext`对象中获取图像资源的路径和请求的图像宽度。 然后，它调用`info.geometrixx.commons.impl.AdaptiveImageHelper`类的方法，该类执行实际的图像缩放。

AdaptiveImageComponentServlet类也覆盖writeLayer方法。 此方法将JPEG质量应用于图像。

### 图像引用修改Servlet(Geometrixx常用){#image-reference-modification-servlet-geometrixx-common}

示例图像引用修改Servlet为img元素生成大小属性，以在网页上缩放图像。

#### 调用servlet {#calling-the-servlet}

Servlet绑定到`cq:page`资源，并支持.jpg文件扩展名。 Servlet选择器为`image`。 因此，Sling会将以下格式的HTTP请求URL解析为此Servlet:

`path-to-page-node.image.jpg`

例如，Sling会将URL为`http://localhost:4502/content/geometrixx/en.image.jpg`的HTTP请求转发到图像引用修改Servlet。

另外三个选择器指定请求的图像宽度、高度和（可选）质量。 以下示例请求的图像宽度为770像素、高度为360像素，且质量中等。

`http://localhost:4502/content/geometrixx/en.image.770.360.MEDIUM.jpg`

**支持的图像属性**

Servlet接受有限数量的图像尺寸和质量值。

默认支持以下值（宽xheight）：

* 256x192
* 370x150
* 480x200
* 127x127
* 770 x 360
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

使用AEM时，可通过多种方法来管理此类服务的配置设置；有关完整的详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

#### 指定图像资源{#specifying-the-image-resource}

图像路径、维度和质量值必须作为存储库中节点的属性进行存储：

* 节点名称为`image`。
* 父节点是`cq:page`资源的`jcr:content`节点。

* 图像路径将存储为名为`fileReference`的属性的值。

在创作页面时，请使用&#x200B;**Sidekick**&#x200B;指定图像，并将`image`节点添加到页面属性中：

1. 在&#x200B;**Sidekick**&#x200B;中，单击&#x200B;**页面**&#x200B;选项卡，然后单击&#x200B;**页面属性**。
1. 单击&#x200B;**Image**&#x200B;选项卡并指定图像。
1. 单击&#x200B;**确定**。

#### 实施详细信息{#implementation-details-1}

info.geometrixx.commons.impl.servlets.ImageReferenceModificationServlet类扩展[AbstractImageServlet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.html)类。 如果已安装cq-geometrixx-commons-pkg包，则ImageReferenceModificationServlet源代码位于`/apps/geometrixx-commons/src/core/src/main/java/info/geometrixx/commons/impl/servlets`文件夹中。

类使用Felix SCR注释配置Servlet关联的资源类型和文件扩展名以及第一个选择器的名称。

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

Servlet使用属性SCR注释设置默认支持的图像质量和尺寸。

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

`AbstractImageServlet`类提供处理HTTP请求的`doGet`方法。 此方法可确定与调用关联的资源，从存储库中检索资源属性，并将它们保存在[ImageContext](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/commons/AbstractImageServlet.ImageContext.html)对象中。

`ImageReferenceModificationServlet`类覆盖`createLayer`方法并实现确定要渲染的图像资源的逻辑。 方法将检索名为`image`的页面`jcr:content`节点的子节点。 从此`image`节点创建[Image](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/Image.html)对象，`getFileReference`方法从图像节点的`fileReference`属性返回到图像文件的路径。

>[!NOTE]
>[com.day.cq.commons.DownloadResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/DownloadResource.html)类提供getFileReferencemethod。


## 开发流体网格{#developing-a-fluid-grid}

AEM使您能够高效地实施流体网格。 本页介绍如何将流式网格或现有网格实施(如[Bootstrap](https://twitter.github.com/bootstrap/))集成到AEM应用程序中。

如果您不熟悉流体网格，请参阅本页底部的[流体网格简介](/help/sites-developing/responsive.md#developing-a-fluid-grid)部分。 本文概述了流体网格及其设计方法。

### 使用页面组件{#defining-the-grid-using-a-page-component}定义网格

使用页面组件生成用于定义页面内容块的HTML元素。 页面引用的ClientLibraryFolder提供了控制内容块布局的CSS:

* 页面组件：添加表示内容块行的div元素。 表示内容块的div元素包括作者在其中添加内容的parsys组件。
* 客户端库文件夹：提供包含div元素的媒体查询和样式的CSS文件。

例如，示例geometrixx-media应用程序包含media-home组件。 此页面组件插入两个脚本，它们生成类`row-fluid`的两个`div`元素：

* 第一行包含类`span12`的`div`元素（内容跨越12列）。 `div`元素包含parsys组件。

* 第二行包含两个`div`元素，一个是类`span8`，另一个是类`span4`。 每个`div`元素都包含parsys组件。

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
>当组件包含多个引用Parsys组件的`cq:include`元素时，每个`path`属性必须具有不同的值。


#### 缩放页面组件网格{#scaling-the-page-component-grid}

与geometrixx-media页面组件(`/etc/designs/geometrixx-media`)关联的设计包含`clientlibs` ClientLibraryFolder。 此ClientLibraryFolder为`row-fluid`类、`span*`类和`span*`类定义CSS样式，这些类是`row-fluid`类的子类。 媒体查询允许根据不同视区大小重新定义样式。

以下示例CSS是这些样式的子集。 此子集重点关注`span12`、`span8`和`span4`类，以及两种视区大小的媒体查询。 请注意CSS的以下特性：

* `.span`样式使用绝对数字定义元素宽度。
* `.row-fluid .span*`样式将元素宽度定义为父项的百分比。 百分比是使用绝对宽度计算的。
* 对于较大视区的媒体查询，会分配较大的绝对宽度。

>[!NOTE]
>
>Geometrixx Media示例将[Bootstrap](https://twitter.github.com/bootstrap/javascript.html) javascript框架集成到其流式网格实现中。 Bootstrap框架提供bootstrap.css文件。

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

#### 重新定位页面组件网格{#repositioning-content-in-the-page-component-grid}中的内容

示例Geometrixx Media应用程序的页面在宽视区中水平分布内容块行。 在较小的视区中，垂直分布相同的块。 以下示例CSS显示用于为媒体主页组件生成的HTML代码实施此行为的样式：

* media-welcome页面的默认CSS为`row-fluid`类内的`span*`类分配`float:left`样式。

* 对于较小视区的媒体查询，为相同类分配`float:none`样式。

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

#### 模块化页面组件{#tip-modularize-your-page-components}

将组件模块化以有效使用代码。 您的网站可能使用多种不同类型的页面，如欢迎页面、文章页面或产品页面。 每种类型的页面都包含不同类型的内容，并且可能使用不同的布局。 但是，当每个布局的某些元素在多个页面中是通用的时，您可以重复使用用于实现该部分布局的代码。

**使用页面组件叠加**

创建一个主页组件，该组件提供用于生成页面各个部分的脚本，例如主体中的`head`和`body`部分，以及`header`、`content`和`footer`部分。

创建其他使用主页组件作为`cq:resourceSuperType`的页面组件。 这些组件包括可根据需要覆盖主页脚本的脚本。

例如， goemetrixx-media应用程序包含页面组件（`sling:resourceSuperType`是基础页面组件）。 多个子组件（如文章、类别和媒体主页）使用此页面组件作为`sling:resourceSuperType`。 每个子组件都包括一个content.jsp文件，该文件将覆盖页面组件的content.jsp文件。

**重复使用脚本**

创建多个JSP脚本，这些脚本生成多个页面组件通用的行和列组合。 例如，文章的`content.jsp`脚本和media-home组件都引用了`8x4col.jsp`脚本。

**按目标视区大小组织CSS样式**

在单独的文件中包含不同视区大小的CSS样式和媒体查询。 使用客户端库文件夹将它们连接在一起。

### 将组件插入页面网格{#inserting-components-into-the-page-grid}

当组件生成单个内容块时，通常由页面组件建立的网格控制内容的放置。

作者应该注意，内容块可以以各种大小和相对位置呈现。 内容文本不应使用相对方向来引用其他内容块。

如有必要，组件应提供其生成的HTML代码所需的任何CSS或Javascript库。 在组件中使用客户端库文件夹生成CSS和JS文件。 要公开文件，请[创建依赖项或将库](/help/sites-developing/clientlibs.md#creating-client-library-folders)嵌入到/etc文件夹下的其他客户端库文件夹中。

**子网格**

如果组件包含多个内容块，请在行中添加内容块，以在页面上建立子网格：

* 使用与包含页面组件相同的类名称，将div元素表示为行和内容块。
* 要覆盖页面设计的CSS实施的行为，请为行div元素使用第二个类名称，并在客户端库文件夹中提供关联的CSS。

例如，`/apps/geometrixx-media/components/2-col-article-summary`组件生成两列内容。 它生成的HTML具有以下结构：

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

页面CSS的`.row-fluid .span6`选择器适用于此HTML中相同类和结构的`div`元素。 但是，该组件还包含/apps/geometrixx-media/components/2-col-article-summary/clientlibs客户端库文件夹：

* CSS使用与页面组件相同的媒体查询来在相同的离散页面宽度下建立布局更改。
* 选择器使用行`div`元素的`multi-col-article-summary`类来覆盖页面`row-fluid`类的行为。

例如，`/apps/geometrixx-media/components/2-col-article-summary/clientlibs/css/responsive-480px.css`文件中包含以下样式：

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

## 流体网格简介{#introduction-to-fluid-grids}

流式网格使页面布局能够适应客户端视区的尺寸。 网格由逻辑列和行组成，这些列和行在页面上放置内容块。

* 列可确定内容块的水平位置和宽度。
* 行决定内容块的相对垂直位置。

使用HTML5技术，您可以实施并处理网格以根据不同的视区大小调整页面布局：

* HTML `div`元素包含跨越特定列数的内容块。
* 这些div元素中的一个或多个在共享公共父维度时构成一行。

### 使用离散宽度{#using-discrete-widths}

对于您定位的每个视区宽度范围，请使用静态页面宽度和内容块的恒定宽度。 手动调整浏览器窗口大小时，内容大小会在不同的窗口宽度（也称为断点）发生更改。 因此，页面设计得到了更紧密的遵守，从而最大化了用户体验。

#### 缩放网格{#scaling-the-grid}

使用网格来缩放内容块以适应不同的视区大小。 内容块跨越特定数量的列。 当列宽度增加或减小以适合不同视区大小时，内容块的宽度会相应地增大或减小。 缩放可以同时支持大型和中型视区，这些视区足够宽，可以并排放置内容块。

![](do-not-localize/chlimage_1-1a.png)

#### 重新定位网格中的内容{#repositioning-content-in-the-grid}

内容块的大小可以受到最小宽度的约束，超出该宽度，缩放不再有效。 对于较小的视区，可使用网格垂直分发内容块，而不是水平分发。

![](do-not-localize/chlimage_1-2a.png)

### 设计网格{#designing-the-grid}

确定在页面上放置内容块时需要使用的列和行。 页面布局决定了跨网格的列和行数。

**列数**

包括足够的列，以便根据所有视区大小在所有布局中水平放置内容块。 您应使用当前所需的列数，以适应将来的页面设计。

**行内容**

使用行控制内容块的垂直位置。 确定共享同一行的内容块：

* 任何布局中水平相邻的内容块都位于同一行中。
* 水平（较宽的视区）和垂直（较小的视区）相邻的内容块位于同一行中。

### 网格实现{#grid-implementations}

创建CSS类和样式以控制页面上内容块的布局。 页面设计通常基于视区中内容块的相对大小和位置。 视区可确定内容块的实际大小。 CSS需要考虑相对大小和绝对大小。 您可以使用三种类型的CSS类实施流体网格：

* `div`元素的类，该元素是所有行的容器。 此类设置网格的绝对宽度。
* 表示行的`div`元素的类。 此类控制其包含的内容块的水平或垂直位置。
* 表示不同宽度的内容块的`div`元素的类。 宽度以父项（行）的百分比表示。

目标视区宽度（及其关联的媒体查询）可划分用于页面布局的离散宽度。

#### 内容块的宽度{#widths-of-content-blocks}

通常，内容块类的`width`样式基于页面和网格的以下特征：

* 您为每个目标视区大小使用的绝对页面宽度。 这些是已知值。
* 每个页面宽度的网格列的绝对宽度。 由您确定这些值。
* 每列的相对宽度占页面总宽度的百分比。 您可以计算这些值。

CSS包含使用以下结构的一系列媒体查询：

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

使用以下算法作为开发页面元素类和CSS样式的起点。

1. 为包含所有行的div元素定义类名称，例如`content.`
1. 为表示行的div元素（如`row-fluid`）定义CSS类。
1. 为内容块元素定义类名称。 对于所有可能的宽度（以列跨度计），都需要一个类。 例如，对于跨3列的`div`元素，使用`span3`类；对于跨4列的`span4`类。 定义网格中列数的类。

1. 针对您定位的每个视区大小，将相应的媒体查询添加到CSS文件中。 在每个媒体查询中添加以下项：

   * `content`类的选择器，例如`.content{}`。
   * 每个span类的选择器，例如`.span3{ }`。
   * `row-fluid`类的选择器，例如`.row-fluid{ }`
   * 行流式类内跨类的选择器，例如`.row-fluid span3 { }`。

1. 为每个选择器添加宽度样式：

   1. 将`content`选择器的宽度设置为页面的绝对大小，例如`width:480px`。
   1. 将所有行式选择器的宽度设置为100%。
   1. 将所有范围选择器的宽度设置为内容块的绝对宽度。 琐碎的网格使用相同宽度的均匀分布列：`(absolute width of page)/(number of columns)`。
   1. 将`.row-fluid .span`选择器的宽度设置为总宽度的百分比。 使用`(absolute span width)/(absolute page width)*100`公式计算此宽度。

#### 在行{#positioning-content-blocks-in-rows}中定位内容块

使用`.row-fluid`类的浮点样式控制行中的内容块是水平排列还是垂直排列。

* `float:left`或`float:right`样式导致子元素（内容块）的水平分布。

* `float:none`样式导致子元素的垂直分布。

将样式添加到每个媒体查询内的`.row-fluid`选择器中。 根据用于媒体查询的页面布局设置值。 例如，下图说明了一行内容在宽视区中水平分发，在窄视区中垂直分发。

![](do-not-localize/chlimage_1-3a.png)

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

#### 将类分配给内容块{#assigning-classes-to-content-blocks}

对于您定位的每个视区大小的页面布局，请确定每个内容块跨越的列数。 然后，确定用于这些内容块的div元素的类。

在建立div类后，您可以使用AEM应用程序实施网格。
