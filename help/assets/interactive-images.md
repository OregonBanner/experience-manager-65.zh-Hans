---
title: 交互式图像
description: 了解如何在Dynamic Media中处理交互式图像
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '4334'
ht-degree: 23%

---


# 交互式图像{#interactive-images}

通过将“购物”热点拖放到图像上，您可以轻松地为客户打造出丰富多彩、引人入胜的静态图像体验。购物热点将有关产品或服务的附加信息与直接的、销售点“添加到购物车”或“购买”功能相结合。客户可以点按或单击这些热点，直接链接到产品或服务，将其添加到购物车，或链接到网页。此类直接体验能够提高客户在您网站上的参与度和转化率。

下面是带有概览弹出窗口的购物横幅。 用户点按模型上的圆圈或“热点”以激活概览。

![chlimage_1-152](assets/chlimage_1-368.png)

通过转到以下内容，在上面的网页上查看交互式图像的实际操作情况：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## 观看如何创建交互式图像横幅 {#watch-how-interactive-image-banners-are-created}

Watch a 10 minute and 33 second walkthrough on [how interactive image banners are created](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). 您还将学习如何预览、编辑和投放交互式图像横幅。

## Quick Start: Interactive Images {#quick-start-interactive-images}

以下工作流分步说明旨在帮助您在AEM Assets快速设置和运行交互式图像。

请查找某些“快速入门”任务中的&#x200B;**示例**&#x200B;标题。它包含一个简短的教程，该教程基于尚未添加交互式图像的以下网页示例：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

本教程有助于说明在您自己的网站上集成交互式图像的步骤。

交互式图像步骤：

1. **（可选）识别热点变量** -如果您使用AEM Assets和Dynamic Media独立版本，可通过识别现有Quickview实施中使用的动态变量来开始，以便您在创建交互式图像时输入热点数据。 See [(Optional) Identifying hotspot variables](#optional-identifying-hotspot-variables).
但是，如果您使用AEM Sites、AEM eCommerce或二者，则不必执行此步骤。
请参阅 [AEM Assets的电子商务概念](/help/sites-administering/concepts.md)。

1. **（可选）创建交互式图像查看器预设** -自定义用于表示热点的图形图像。 如果您打算使用现成的名为的交互式图像查看器预设，则无需创建您自己的交互式图像查看器预 `Shoppable_Banner` 设。
See [(Optional) Creating an Interactive Image viewer preset](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **上传图像横幅** -上传要实现交互的图像横幅。请参 [阅上传图像横幅](#uploading-an-image-banner)。

1. **将热点添加到图像横幅** -将一个或多个热点添加到图像横幅，并将每个热点与操作（如超链接、概览或体验片段）关联。 添加热点后，您将通过发布交互式图像来完成此任务。

   * See [Adding hotspots to an image banner](#adding-hotspots-to-an-image-banner).
   * 请参 [阅预览交互式图](#optional-previewing-interactive-images) 像——可选。 如果需要，您可以查看购物横幅的呈现形式并测试其交互性。

   * See [Publishing Assets](/help/assets/publishing-dynamicmedia-assets.md) for details on how to publish interactive image assets.

1. **将交互式图像添加到您的网站或AEM中的您的**&#x200B;网站如果您使用AEM Sites、AEM电子商务或两者，则可以通过将交互式媒体组件拖动到页面上，将交互式图像直接添加到AEM的网页。 See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)
如果您使用AEM Assets和Dynamic Media独立版本，则必须将嵌入代码复制到您的网站上，然后将其与现有Quickview集成。 See [Integrating an interactive image with your website](#integrating-an-interactive-image-with-your-website).
如果您使用第三方WCM（Web内容管理器），则必须将新的交互式视频与网站上使用的现有Quickview实现相集成。 请参 [阅将交互式图像与现有概览相集成](#integrating-an-interactive-image-with-an-existing-quickview)。

## （可选）识别热点变量 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>仅当满足以下条件时，才需要此任务:
>
>* 您希望通过触发Quickviews向图像添加交互性。
>* 您的AEM实施不 *使用* eCommerce integration framework将产品数据从任何电子商务解决方案（如IBM Websphere Commerce、Elastic Path、hybris或Intershop）拉入AEM。 请参阅 [AEM Assets的电子商务概念](/help/sites-administering/concepts.md)。

>
>
如果您的AEM实施使用电子商务，则可以跳过此任务并继续到下一个任务。

开始，识别现有Quickview实现所使用的动态变量，以便输入热点数据以创建交互式图像。

在AEM Assets向横幅图像添加热点时，您需要分配SKU(库存单位；您所优惠的每个不同产品或服务的唯一标识符)以及每个热点的可选附加变量。 以后会使用这些热点变量将热点与概览内容相匹配。

必须准确地识别要与热点数据相关联的变量数量及类型，这一点很重要。而且，添加到横幅图像的每个热点都必须附带足够的信息，以便能够在现有的后端系统中明确地识别产品。

有多种不同的方法可以识别用于热点数据的变量集。

有时可能需要向负责现有Quickview实施的IT专家咨询，因为他们可能了解在系统中识别Quickview所需的最少数据集。 但在大多数情况下，可能只需简单地分析前端代码的现有行为即可。

大多数Quickview实施都采用以下模式：

* 用户在网站上激活用户界面元素。例如，单击“Quickview”按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* Quickview数据将转换为准备在网页上呈现的内容。
* 最后，前端代码以可视形式将这些内容呈现在屏幕上。

然后，该方法是访问实现Quickview功能的现有网站的不同区域，触发Quickview并捕获由网页发送的Ajax URL，以加载Quickview数据或内容。

通常情况下，您不需要使用任何专业的调试工具。现代的 Web 浏览器具备 Web 检查器，可以实现相同的功能。下面列举了一些具备 Web 检查器的 Web 浏览器：

* 要在 Google Chrome 中查看发出的所有 HTTP 请求，请按 F12 键以打开“开发人员工具”面板，然后单击“网络”选项卡。在Mac上，按Command+Option+I打开“开发人员工具”面板，然后单击“网络”选项卡。

* 在 Firefox 中，您既可以按 F12 键并使用其“网络”选项卡来激活 Firebug 插件，也可以使用内置的检查器工具及其“网络”选项卡。在Mac上，按Command+Option+I打开“Developer Tools”（开发人员工具）面板，然后单击“Inspector”（检查器）选项卡。

在浏览器中打开网络监视时，在页面上触发概览。

现在，在网络日志中找到Quickview Ajax URL，并复制记录的URL供将来分析。 在大多数情况下，当您触发Quickview时，会向服务器发出大量请求。 通常，Quickview Ajax URL是列表中最早的URL之一。 It has either a complex query string portion or path, and its response MIME type is either `text/html`, `text/xml`, or `text/javascript`.

在此过程中，访问网站的不同区域(具有不同的产品类别和类型)非常重要。 其原因是，Quickview URL可能具有特定网站类别通用的部分，但仅在您访问网站的其他区域时更改。

在最简单的情况下，Quickview URL中唯一的变量部分是产品SKU。 在这种情况下，SKU 值就是您将热点添加到横幅图像时唯一需要提供的数据。

但是，在复杂情况下，除SKU外，Quickview URL还具有不同的可变元素，如类别ID、颜色代码、大小代码等。 在这种情况下，在 AEM 资产的交互式购物图像功能中，每个元素都是热点数据定义中的一个独立变量。

请考虑以下Quickview URL示例及其生成的热点变量：

<table>
  <tbody>
  <tr>
    <td><p>单个 SKU，位于查询字符串中。</p> </td>
    <td><p>录制的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL 中唯一的变量部分是 productId= 查询字符串参数的值，很明显它就是 SKU 值。Therefore, our hotspots only need SKU fields populated with values like <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>单个 SKU，位于 URL 路径中。</p> </td>
    <td><p>录制的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>The variable part is in the last portion of the path, and it becomes the SKU value of the hotspots: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU 和类别 ID，位于查询字符串中。</p> </td>
    <td><p>录制的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL 中有两个可变部分。The SKU is stored in the <code>prodId</code> parameter and the category ID<code></code> is stored in the <code>category=</code> parameter.</p> <p>因此，热点定义是成对存在的，即，一个 SKU 值对应一个额外的变量 <code>categoryId</code>。生成的各对如下所示：</p>
    <ul>
      <li><p>SKU is <strong><code>305466</code></strong> and <code>categoryId</code> is <code>1100004</code>.</p> </li>
      <li><p>SKU is <strong><code>310181</code></strong> and <code>categoryId</code> is <strong><code>1100004</code></strong>.</p> </li>
      <li><p>SKU is <strong><code>308706</code></strong> and <code>categoryId</code> is <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

您可以将上述三个示例中所用的方法运用到演示网页：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

演示网页有多个产品缩略图，每个缩略图都有一个标有“查看更多”的概览按钮。 在Web浏览器的调试工具仍处于激活状态时，单击每个按钮并记下录制的Quickview URL。 在激活页面上所有四个可用的产品概览后，您会对向后端发出的概览请求产生以下列表:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

通过查看这些服务器调用，您会发现只有请求路径中存在产品特定信息。 您还注意到，查询字符串根本不被使用，并且涉及两种不同类型的数据：

* 第一类是男性或女性。 您可以称此为“产品类别”。
* 第二种类型是产品名称，如CamoPullover。 您可以假定这是产品SKU。

根据此信息，整个Quickview URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

依据上述分析，您可以在热点中使用 `categoryId` 和 `SKU`。

现在，您便可以使用 AEM 资产中的交互式购物图像功能，上传图像横幅并向其添加热点。

## (Optional) Creating an Interactive Image viewer preset {#optional-creating-an-interactive-image-viewer-preset}

您可以选择使用 AEM 资产默认附带的名为 `Shoppable_Banner` 的现成交互式图像查看器预设。或者，您也可以创建自己的自定义查看器预设，以便与交互式图像配合使用。

在创建自定义交互式图像查看器预设时，您可以确定图像横幅上热点的外观。 在创建查看器预设的过程中，您可以选择使用预定义图像库中提供的热点图形。

在保存查看器预设后，查看器预设会在AEM Assets的“查看器预设”列表页面上自动激活（打开）。 此功能意味着无论您何时视图资产，都可以在交互式媒体组件中看到该内容。 但是，要*提供具有此查看器预设的*交互式横幅，您还必须*发布*您的查看器预设（对于自定义或现成的查看器预设，情况也是如此）。

**创建交互式图像查看器预设的步骤**

1. 在左边栏中，点按工 **[!UICONTROL 具>资产>查看器预设。]**
1. Near the upper-right corner of the page, tap **[!UICONTROL Create.]**
1. 在“新查看器预设”对话框中，键入一个用于描述该交互式横幅查看器预设的名称。


   这是保存后将在“查看器预设”列表页面中显示的标题。

1. In the Rich Media Type pull-down menu, select **[!UICONTROL Interactive Image.]**
1. Tap **[!UICONTROL Create.]**
1. 在“编辑查看器预设”页面中，点按&#x200B;**[!UICONTROL 外观]**&#x200B;选项卡。
1. 执行下列操作之一：

   * 要上传您自己的热点图像以在图像上使用，请点按“资产选取器”图标。在“选择内容”页面上，导航到您要使用的热点图像，将其选中，然后点按右上角的对勾标记图标。
   * 要选择预定义的热点图像，请点按“热点图库”图标。在热点图库画板上，点按您要使用的热点图像。

1. Near the upper-right corner of the page, tap **[!UICONTROL Save.]**

   请确保您发布了新查看器预设。

   请参阅[发布已添加的查看器预设](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)。

   现在，您便可以上传图像横幅。

## 上传图像横幅 {#uploading-an-image-banner}

If you have already uploaded the images that you want to use, advance to the next step, [Adding hotspots to an image banner](#adding-hotspots-to-an-image-banner).

**上传图像横幅**

1. 上传您要实现交互的图像横幅。

   请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。


   您现在可以向图像横幅添加热点；请参阅下面的下一个任务。

## 将热点添加到图像横幅 {#adding-hotspots-to-an-image-banner}

您可以使用“热点管理”页面上的编辑器将热点添加到图像横幅。

添加热点时，您可以将热点定义为概览弹出显示、超链接或体验片段。

请参 [阅体验片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
>
>请注意，在体验片段中嵌入查看器时，不支持交互式图像中的社交媒体共享工具。 要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。

在当前创建／编辑会话中，页面右上角附近支持撤消和重做选项。

创建完交互式图像后，您可以使用预览来查看交互式图像将如何呈现给客户。

请参 [阅（可选）预览交互式图像](#optional-previewing-interactive-images)。

>[!NOTE]
>
>当您在交互式图像或传送横幅中向图像添加热点时，无论热点是交互式图像还是传送横幅，热点信息都会存储在与图像位置相关的同一元数据位置。 此功能意味着您可以在任一查看器中轻松重复使用同一图像及其定义的热点数据。
>
>但是，请注意，传送横幅支持图像上的图像地图，这些图像上也可能包含热点；交互式图像则不会。 如果要创建使用同一图像的交互式图像或传送横幅，请牢记这一点。 您可能希望改为使用同一图像的单独副本创建交互式图像和传送横幅。
>
>另请参阅 [传送横幅](/help/assets/carousel-banners.md)。

>[!NOTE]
>
>如果您正在使用热点编辑交互式图像并裁剪图像，则您的热点将被删除。

**向图像横幅添加热点**

1. 在“资产”视图中，导航到要进行交互的图像横幅。
1. 执行下列操作之一：

   * Hover on the image, then tap **[!UICONTROL Select]** (checkmark icon). On the toolbar, tap **[!UICONTROL Edit.]**

   * 将鼠标悬停在图像上，然后点 **[!UICONTROL 按更多操作]** （三个点图标） **[!UICONTROL >编辑。]**

   * 点按图像以在“详细信息”视图页中将其打开。 On the toolbar, tap **[!UICONTROL Edit.]**

1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL 添加热点]**（手指点按图标）以打开热点管理页面。
1. Near the upper-left corner of the page, tap **[!UICONTROL Hotspot.]**

1. Near the upper-left corner of the Hotspot Management page, tap **[!UICONTROL Hotspot.]**
1. 在图像上，点按您希望显示热点的位置。如有必要，可拖动热点以调整其位置。
1. 重复步骤a和b，根据需要添加其他热点。
1. （可选）要删除热点，请在图像上选择该热点，然后点按“热 **[!UICONTROL 点]** ”标题下的删除 **[!UICONTROL (垃圾桶图]** 标)。

1. 在“名称”文本字段中，键入热点的名称。此名称也会显示在“选定的热点”下拉列表中。
1. 执行下列操作之一：

   * 点按 **[!UICONTROL 概览。]**

      * 如果您是AEM Sites或电子商务客户，请点按或单击产品选取器图标（放大镜）以打开“选择产品”页面。 点按或单击要使用的产品，然后点按页面右上角的**选择**以返回到热点管理页面。
      * 如果您不是 *AEM Sites* 或电子商务客户

         * 请参阅 [识别热点变量](#optional-identifying-hotspot-variables);您需要定义这些变量。
         * 然后，手动输入SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），即您优惠的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充概览模板的变量部分，以便系统能够将点按的热点与特定SKU的概览相关联。
         * (Optional) If there are other variables within the Quickview that you need to use to further identify a product, tap **[!UICONTROL Add Generic Variable.]** 在文本字段中，指定其他变量。 例如，`category=Mens` 就是一个添加的变量。
   * Tap **[!UICONTROL Hyperlink.]**

      * 如果您是AEM Sites客户，请点按或单击站点选择器图标（文件夹）以导航到URL。 请注意，如果您的交互式内容包含相对URL的链接，特别是指向AEM Sites页面的链接，则无法使用基于URL的链接方法。
      * 如果您是独立客户，请在“HREF”文本字段中指定链接网页的完整URL路径。

   请确保指定是在新的浏览器选项卡（建议使用默认选项卡）还是在同一选项卡中打开链接。

   有关更 [多信息，请参](/help/assets/working-with-selectors.md) 阅使用选择器。

   * Tap **[!UICONTROL Experience Fragment.]**

      * 如果您是AEM Sites客户，请点按或单击搜索图标（放大镜）以打开体验片段页面。 点按或单击要使用的体验片段，然后点按页面右上角的选择以返回到热点管理页面。
请参 [阅体验片段](/help/sites-authoring/experience-fragments.md)。

      * 指定体验片段在横幅上的显示方式，如同其宽度和高度一样。

         >[!NOTE]
         >
         >请注意，在体验片段中嵌入查看器时，不支持交互式图像中的社交媒体共享工具。 要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。



1. Tap **[!UICONTROL Save]** to save your work and return to the Browse page.
1. 发布交互式图像。 通过发布，横幅可通过云传送，如果需要与第三方网站集成，还可生成嵌入代码。

   请参阅[发布资产](/help/assets/manage-assets.md#publishing-assets)。

   添加热点并发布交互式图像后，您现在可以将其添加到现有网站。

   See [Integrating an interactive image with your website](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   >
   >如果您正在编辑具有热点的交互式图像并裁剪图像，则您的热点将被删除。

### (Optional) Previewing interactive images {#optional-previewing-interactive-images}

您可以使用预览来查看交互式图像对客户的呈现效果，并测试图像的热点以确保它们的行为符合预期。

当您对交互式图像感到满意时，您可以发布该图像。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。请参阅[将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)。请注意，如果您的交互式内容包含相对URL的链接，特别是指向AEM Sites页面的链接，则无法使用基于URL的链接方法。
See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

**预览交互式图像**

1. 在“资产”视图中，导航到您创建的现有交互式图像，然后点按以预览打开它。
1. 在预览页面的左上角附近，在内容下拉列表中，点按查看 **[!UICONTROL 器。]**
1. 在“查看器”列表 **[!UICONTROL 中，点按]** Shoppable_Banner，或点按您创建的交互式图像查看器预设的名称。
1. 点按图像上的热点以测试其关联的操作。

## 发布交互式图像资源 {#publishing-interactive-image-assets}

See [Publishing Assets](/help/assets/publishing-dynamicmedia-assets.md) for details on how to publish interactive image assets.

## 将交互式图像与您的网站集成 {#integrating-an-interactive-image-with-your-website}

在上传横幅图像、将热点添加到图像并发布交互式图像后，您现在可以将其添加到网站页面。

如果您是AEM Sites的客户，则可以通过将交互式媒体组件拖到页面上来添加交互式图像。 See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

如果您是独立的AEM Assets客户，则可以按本节所述手动将交互式图像添加到您的网站。

1. 复制已发布的交互式图像的嵌入代码。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

1. 将复制的嵌入代码添加到网页中的所需位置。
复制的嵌入代码已设置为响应式环境，因此应自动适应分配的区域。

**示例**

以演示网站为例：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html)

请注意，三位男士的照片是静态的 `IMG` 标记：

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

集成过程很简单，只需删除 `IMG` 标记并将其替换为从 AEM 资产中复制的嵌入代码即可。您可以通过下面的 URL 查看最终效果，即页面上会显示带有三个圆形热点的交互式购物图像：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
>
>至此，演示网站交互式购物图像上的热点仅用于显示目的；它们尚未与现有Quickviews集成。

要面向交互式环境对购物交互式图像进行“裁剪”，您可以将交互式图像配置属性 `ZoomView.iscommand` 添加到路径中 － 其中 `ZoomView` 是要调用的组件，而 `iscommand` 是您所应用的“裁剪”图像服务命令。

请参阅 [ZoomView.iscommand](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) 配置属性。

请参阅[裁剪](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html)图像服务命令。

您现在可以将交互式图像与网站上的现有概览相集成。

## 将交互式图像与现有Quickview集成 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
>
>此任务仅在您是独立的AEM Assets客户时适用。

该过程的最后一步是将交互式图像与网站上现有的Quickview实施相集成。 但是，没有任何一种集成解决方案是在所有情况下都适用的。每个Quickview实施都是独一无二的，需要一种特定的方法，最可能需要前端IT人员的协助。

现有Quickview实现通常表示在网页上按以下顺序发生的一系列相互关联的操作：

1. 用户在网站的用户界面上触发一个元素。
1. 前端代码根据在步骤1中触发的用户界面元素获取Quickview URL。
1. 前端代码使用在第 2 步获取的 URL 发送一个 Ajax 请求。
1. 后端逻辑将相应的概览数据或内容返回到前端代码。
1. 前端代码加载Quickview数据或内容。
1. （可选）前端代码将加载的Quickview数据转换为HTML表示形式。
1. 前端代码显示一个模态对话框或面板，并将 HTML 内容呈现在屏幕上以供最终用户查看。

这些调用并非独立的公共 API 调用（可以由网页逻辑从任意步骤进行调用）。相反，这些调用属于链式调用，即，每个后续步骤都隐藏在前一步的最后阶段（回调）。

如果用交互式购物图像来替换第 1 步的操作以及第 2 步的部分操作，则与此同时，当用户单击购物图像中的热点时，查看器就会处理此类用户交互。查看器会向网页返回一个事件，其中包含之前添加到 AEM 资产中的所有热点数据。

在此类事件处理程序中，前端代码会执行下列操作：

* 监听交互式购物图像发出的事件。
* 根据热点数据构建概览URL。
* 触发从后端加载概览并在屏幕上显示概览的过程。

AEM Assets返回的嵌入代码已经有一个可用的事件处理程序被注释掉，如下面突出显示的代码片断所示：

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

因此，只需取消对该代码的注释，并用针对特定网页的代码来替换虚拟处理程序主体即可。

构建Quickview URL的过程与之前介绍的用于识别热点变量的过程基本相反。

请参阅[识别热点变量](#optional-identifying-hotspot-variables)。

使用我们以前的Quickview URL示例，您可以在以下示例中看到在各种情况下如何构建Quickview URL:

<table>
 <tbody>
  <tr>
   <td><p>单个 SKU，位于查询字符串中</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>单个 SKU，位于 URL 路径中</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU 和类别 ID，位于查询字符串中</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

触发Quickview URL并激活Quickview面板的最后一步很可能需要IT部门的前端IT人员的协助。 他们最了解如何通过适当的步骤准确地触发Quickview实施，并拥有现成的Quickview URL。

您可以了解如何将这些步骤应用到演示网站，以将交互式购物图像与概览代码完全集成。 以前，Quickview URL的结构如下所示：

```xml
/datafeed/$categoryId$-$SKU$.json
```

To reconstruct this URL inside the `quickViewActivate` handler, you can use the `categoryId` and `SKU` fields available in the `inData` object that is passed to the handler by the viewer&#39;s code:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

The demo website is triggering the Quickview dialog box using a simple `loadQuickView()` function call. 此函数只使用一个参数，即Quickview数据URL。 As such, the last step needed to integrate the shoppable interactive image is to add the following line of code to the `quickViewActivate` handler:

```xml
loadQuickView(quickViewUrl);
```

下面是完整的源代码：

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

具有完全集成的交互式图像的最终演示网站如下所示：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html)

## 使用概览创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/custom-pop-ups.md).
