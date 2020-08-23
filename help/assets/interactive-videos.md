---
title: 交互式视频
description: 了解如何在Dynamic Media中处理交互式视频和购物视频
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '6050'
ht-degree: 25%

---


# 交互式视频{#interactive-videos}

您可以轻松创建交互式视频（也称为购物视频），从而直接推动视频转化。 客户在视频播放器一侧的面板中与视频进行交互，根据视频展示的内容，相关的服务、信息或产品缩略图会滚动到客户的视线中。客户可以点按缩略图并直接链接到相应的服务，也可以将项目添加到购物车以立即购买，或者链接到某个网页以了解更多信息。

视频结束时，所有提供项目的可视汇总会显示出来以发出行动动员。客户还有其他机会点按所需的项目。像这样的可操作特定体验能够提高客户的参与度和转化率。

另请参阅[交互式图像](/help/assets/interactive-images.md)。

## 交互式视频实际操作情况 {#interactive-video-in-action}

To see an interactive, shoppable video in action, click [Live Demos](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html), scroll to the **[!UICONTROL Shoppable Media]** heading on the page, then click the shoppable video.

* 在播放过程中，当视频中使用产品时，相同的产品以缩略图的形式显示在右侧。

* 单击缩略图以暂停视频并打开产品的概览。 例如，单击视频中的KitchenAid缩览图图像，体验混色器的360度旋转视图，或放大以查看混色器详细信息。

<!-- There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![交互式购物视频中的帧](assets/chlimage_1-126.png)*交互式购物视频中的视频帧捕获。*

>[!NOTE]
>
>如果您创建交互式视频以在用户单击缩略图时启动网页，某些设备将阻止打开弹出网页。 在这种情况下，您必须更改设备上的弹出窗口阻止程序设置。 例如，在Apple iPhone 6上，点按 **[!UICONTROL 设置]** > **Safari** > **阻止弹出窗口**，然后将控件滑 **[!UICONTROL 动到Off]**。 现在，当您播放交互式视频并单击缩略图时，如果要打开弹出窗口，将提示您。 如果您接受，则将打开网页。

### 观看如何创建交互式视频 {#watch-how-interactive-videos-are-created}

观看有关[如何创建交互式视频](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)的 7 分 30 秒视频演练[](https://outv.omniture.com?v=s4NHQ2dzqd7hIqWjeG2sIdyNWsTWyupA)。
（虽然视频演练使用 Assets（按需）进行标记，但 AEM Assets 中的交互式视频仍适用这些原则和步骤。）

### Adobe 客户成功网络研讨会 {#adobe-customer-success-webinar}

“使用AEM Assets的交互式视频、链接共享和YouTube共享”网络研讨会教您如何使用交互式视频和其他功能将转化驱动的事件绑定到视频营销内容中。

>[!NOTE]
[在 AEM 资产中使用交互式视频、链接共享和 YouTube 共享](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/).

## 快速入门：交互式视频 {#quick-start-interactive-videos}

下面的工作流分步说明旨在帮助您在 Dynamic Media 中快速设置并运行交互式视频。

请查找某些“快速入门”任务中的&#x200B;**示例**&#x200B;标题。它包含一个简短的教程，该教程基于尚未为其添加 *交互* 的此开始演示网页：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

**示例**&#x200B;有助于说明在您的网站上集成交互式视频的步骤。

完成上一个示例部分中的教程后，具有完全集成的交互式视频的最终演示网页将如下所示：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

交互式视频步骤：

1. **（可选）识别概览变量** -通过识别现有概览实施所使用的动态变量来开始。 在创建交互式视频时，可以使用变量将产品缩略图映射到相应的产品概览。 请参 [阅（可选）识别概览变量](#optional-identifying-quickview-variables)。
   *请注意，仅当以下所有情况均为真时，才需要执行此步骤*:·您希望通过触发概览来为视频添加交互性。
·您的AEM实施不 *使用* eCommerce integration framework从任何电子商务解决方案（如IBM Websphere Commerce、Elastic Path、hybris或Intershop）将产品数据拉入AEM。 请参阅 [AEM Assets的电子商务概念](/help/sites-administering/concepts.md)。

1. **（可选）创建交互式视频查看器预设** -自定义组成播放器的各种组件的外观和行为，如视频浏览条和交互式缩略图。
Creating your own Interactive Video viewer preset is not required if you intend to use the out-of-the-box Interactive Video viewer presets `Shoppable_Video_Light` or `Shoppable_Video_Dark` instead.
请参 [阅创建新查看器预设](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) （这是可选的）和创建 [交互式查看器预设的特殊注意事项](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)。

1. **上传视频及其关联的图像资产** -上传您要实现交互的视频和关联的图像。
请参阅[上传视频及其关联的缩略图资产](#uploading-a-video-and-its-associated-thumbnail-assets)。


1. **为视频添加交互性** -为视频添加一个或多个时间段。 然后，将这些时间段内的图像缩略图关联起来。 将每个图像缩略图分配给操作，如超链接、概览或体验片段。
(请注意，如果您的交互式内容包含与相对URL(尤其是指向AEM Sites页面的链接)的链接，则无法使用基于URL的链接方法。)
最后，发布交互式视频资源。 Publishing creates the embed code or URL that you will eventually copy and apply to your website landing page.See [Adding interactivity to your video](#adding-interactivity-to-your-video).
请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

1. **将交互式视频添加到您的网站或AEM中的您的网站**&#x200B;如果您使用AEM Sites、AEM电子商务，或同时使用二者，则可以通过将交互式媒体组件拖动到页面上，将交互式视频直接添加到AEM的网页。 See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)
使用嵌入代码或URL将交互式视频与您的网站体验相集成。 See [Integrating an interactive video with your website](#integrating-an-interactive-video-with-your-website).
如果您使用第三方WCM（Web内容管理器），则必须将新的交互式视频与网站上使用的现有Quickview实现相集成。 请参 [阅将交互式视频与现有Quickview集成](#integrating-an-interactive-video-with-an-existing-quickview)。
   [](/help/assets/adding-dynamic-media-assets-to-pages.md)

## （可选）识别概览变量 {#optional-identifying-quickview-variables}

>[!NOTE]
仅当满足以下条件时，才需要此任务:
* 您希望通过触发Quickviews向视频添加交互性。
* 您的AEM实施不 *使用* eCommerce integration framework将产品数据从任何电子商务解决方案（如IBM Websphere Commerce、Elastic Path、hybris或Intershop）拉入AEM。 请参阅 [AEM Assets的电子商务概念](/help/sites-administering/concepts.md)。

如果您的AEM实施使用电子商务，则可以跳过此任务并继续到下一个任务。

开始，识别现有Quickview实施所使用的动态变量，以便在交互式视频创建过程中将产品缩略图映射到相应的产品Quickview。

在将时间区段添加到视频时，您需要为添加到区段的每个缩略图分配一个 SKU 及其他任何变量。以后会使用这些变量显示正确的Quickview产品。

必须准确地识别唯一触发产品概览所需的变量，这一点很重要。

有时，可能需要向负责现有Quickview实施的IT专家咨询。 他们可能知道在系统中识别概览所需的最少数据集。 但在大多数情况下，可能只需简单地分析前端代码的现有行为即可。

大多数Quickview实施都采用以下模式：

* 用户在网站上激活用户界面元素。例如，单击“Quickview”按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* Quickview数据将转换为准备在网页上呈现的内容。
* 最后，前端代码以可视形式将这些内容呈现在屏幕上。

因此，方法是访问现有网站中实现Quickview的不同区域，触发Quickview，并捕获网页发送的用于加载Quickview数据或内容的Ajax URL。

通常情况下，您不需要使用任何专业的调试工具。现代的 Web 浏览器具备 Web 检查器，可以实现相同的功能。下面列举了一些具备 Web 检查器的 Web 浏览器：

* To see all outgoing HTTP requests in Google Chrome, press **F12** (Windows) or **Command+Options+I** (Mac) to open the Developer Tools panel, and then click the **Network** tab.

* In Firefox, you can either activate the Firebug plug-in by pressing **F12** (Windows) or **Command+Option+I** (Mac) and use its **`[Net]`** tab, or you can use the built-in Inspector tool and its Network tab.

* 在Internet Explorer中，通过按F12激活调 **试器工具**。

在浏览器中打开网络监视时，在页面上触发概览。

现在，在网络日志中找到Quickview Ajax URL，并复制记录的URL供将来分析。 在大多数情况下，当您触发Quickview时，会向服务器发出大量请求。 通常，Quickview Ajax URL是列表中最早的URL之一。 It has either a complex query string portion or path, and its response MIME type is either `text/html`, `text/xml`, or `text/javascript`.

在此过程中，访问网站的不同区域(具有不同的产品类别和类型)非常重要。 其原因是，Quickview URL可能具有特定网站类别通用的部分，但仅在您访问网站的其他区域时更改。

在最简单的情况下，Quickview URL中唯一的变量部分是产品SKU。 在这种情况下，产品SKU值是向AEM交互式视频中的某个时间段添加缩略图时唯一需要的数据。

但是，在复杂情况下，Quickview URL除了产品SKU之外还具有不同的可变元素，如类别ID、颜色代码等。 在这种情况下，AEM的缩略图数据定义中的每个此类元素都会成为单独的变量。

请考虑以下Quickview URL及其生成的缩略图变量示例：

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
    </ul> <p>The only variable part in the URL is the value of the <code>productId=</code> query string parameter, and it is clearly a SKU value. Therefore, our thumbnails only need SKU fields populated with values like <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>单个 SKU，位于 URL 路径中。</p> </td>
    <td><p>录制的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>The variable part is in the last portion of the path, and it becomes the SKU value of AEM thumbnails: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU 和类别 ID，位于查询字符串中。</p> </td>
    <td><p>录制的Quickview URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL 中有两个可变部分。The SKU is stored in the <code>prodId</code> parameter and the category ID is stored in the <code>category=</code> parameter.</p> <p>因此，缩略图定义是成对存在的。 即，一个 SKU 值对应一个额外的变量 <code>categoryId</code>。生成的各对如下所示：</p>
    <ul>
      <li>SKU is <code>305466</code> and <code>categoryId</code> is <code>1100004</code></li>
      <li>SKU is <code>310181</code> and <code>categoryId</code> is <code>1100004</code></li>
      <li>SKU is <code>308706</code> and <code>categoryId</code> is <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

将上述方法应用于我们的示例网站时，我们的网页包含许多产品缩略图，每个缩略图都有一个“SEE MORE”按钮：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

在激活页面上可用的所有产品概览后，您将获得向后端发出的概览请求的以下列表:

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

通过查看这些服务器调用，您会发现只有请求路径中存在产品特定信息。 您还注意到查询字符串根本未使用，并且涉及两种不同类型的数据：

* 第一种是蜡烛，垫子，家具，玻璃器皿。 您可以称此为“产品类别”。
* 第二种类型是产品代码，如233916597。 您可以假定它是“产品SKU”。

根据此信息，整个Quickview URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

根据此分析，您可以得出以下两个变量作为缩略图： `categoryId` 和 `SKU`。

您现在可以上传视频及其关联的缩略图资产。

## （可选）创建交互式视频查看器预设{#optional-creating-an-interactive-video-viewer-preset}

如果您打算使用默认的现成交互式视频查看器预设类型或，则可以跳过此任务并继续下一 `Shoppable_Video_dark` 步 `Shoppable_Video_light`。

在创作环境中单击缩略图时，将显示“概览”对话框的预览。

![chlimage_1-21](assets/chlimage_1-127.png)

您可以选择创建自己的自定义交互式视频查看器预设。 您可以确定视频播放器的样式、交互式缩略图以及显示在视频末尾的缩略图网格视图。

交互式视频查看器预设能够准确地呈现您添加的视频和所有时间轴区段。在预览模式下单击产品缩略图时，它还使用默认概览示例，这样您就可以在发布前测试其交互性。

保存查看器预设后，“查看器预设”页面中的查看器预设状态将自动设置为 **开**。此状态表明查看器预设在 Dynamic Media 组件中可见，预览视频时也可见。另请确保手动发布新查看器预设。

请参 [阅创建新查看器预设](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) ，以创建您自己的交互式视频查看器预设。

## 上传视频及其关联的缩略图资产 {#uploading-a-video-and-its-associated-thumbnail-assets}

If you have already uploaded your video and thumbnail assets, proceed to [Adding interactivity to your video](#adding-interactivity-to-your-video).

如果您上传了错误的视频或图像，或者您希望删除不再需要的已上传视频或图像，请参阅删 [除资产](/help/assets/managing-assets-touch-ui.md#deleting-assets)。

要上传视频及其关联的缩略图资产，请执行以下操作：

1. 将视频和关联的缩略图资产上传到一个或多个所需的文件夹。

   请参阅[上传资产](/help/assets/managing-assets-touch-ui.md)。
请参阅[使用 FTP 作业计划功能上传资产](/help/assets/managing-assets-touch-ui.md)。

   现在，可以为视频添加交互性。

## 为视频添加交互性 {#adding-interactivity-to-your-video}

您可以使用“创建交互式视频”页面上的就地可视编辑器，向视频添加时间轴区段。

在添加时间轴区段后，您可以在每个区段内添加缩略图。对于添加的每个缩略图，您可以分别应用一个操作。例如，您可以将概览应用到缩略图，也可以为其分配超链接或体验片段。

请参 [阅体验片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
请注意，在体验片段中嵌入查看器时，不支持交互式视频中的社交媒体共享工具。 要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。

>[!NOTE]
如果您的交互式内容包含与相对URL(特别是指向AEM Sites页面的链接)的链接，则无法使用基于URL的链接方法。

在当前创建／编辑会话中，页面右上角附近支持撤消和重做选项。

保存交互式视频后，视频会立即打开到预览。您可以从中选择交互式视频查看器预设并播放视频，大致了解交互式视频将如何呈现给客户。

要为视频添加交互性，请执行以下操作：

1. 在“资产”视图中，导航到您上传的要实现交互的视频。
1. 执行下列操作之一：

   * Hover on the image, then tap **[!UICONTROL Select]** (checkmark icon). On the toolbar, tap **[!UICONTROL Edit.]**

   * 将鼠标悬停在图像上，然后点 **[!UICONTROL 按更多操作]** （三个点图标） **[!UICONTROL >编辑。]**

   * 点按图像以在“详细信息”视图页中将其打开。 On the toolbar, tap **[!UICONTROL Edit.]**

1. 在“创建交互式视频”页面中，执行以下任一操作：

   * 点按&#x200B;**[!UICONTROL 播放]**&#x200B;按钮以开始播放视频。当视频中出现您要突出显示的特定产品、服务或详细信息时，点按工具栏中的&#x200B;**[!UICONTROL 添加区段]**。重复上述步骤，直到视频结束。



      对于您添加的每个时间区段，您可以向其分配一个或多个缩略图，然后将这些缩略图链接到Quickview产品页面供客户购买，或链接到网页以了解更多信息。

   * 点击“ **[!UICONTROL 播放]** ”按钮开始播放视频。当您要突出显示的特定产品、服务或详细信息进入视图时，点按 **[!UICONTROL 暂停。]** 点按 **[!UICONTROL 添加区段。]**

      继续播放视频，并在您要添加区段的时间轴点处暂停视频，直到视频结束。

1. （可选）向左拖动&#x200B;**[!UICONTROL 时间轴缩放滑块]**&#x200B;上的栏可放大（向右拖动则缩小），从而控制您看到的已添加区段的详细信息量。

   ![chlimage_1-22](assets/chlimage_1-128.png)

   根据视频的长度，“区段持续时间”默认为以下值：

   <table>
      <tbody>
        <tr>
        <td><strong>如果视频长度为……</strong></td>
        <td><strong>“区段持续时间”设置默认为……</strong></td>
        </tr>
        <tr>
        <td>3分钟或更多</td>
        <td>60秒</td>
        </tr>
        <tr>
        <td>2-3分钟</td>
        <td>30秒</td>
        </tr>
        <tr>
        <td>1-2 分钟</td>
        <td>20 seconds<br /> </td>
        </tr>
        <tr>
        <td>30-60秒</td>
        <td>10秒</td>
        </tr>
        <tr>
        <td>30秒或更短</td>
        <td>5秒</td>
        </tr>
      </tbody>
    </table>

   视频时间轴使用的屏幕空间与它可用的屏幕空间一样多。 因此，在调整浏览器大小时，您添加的区段会保持其正确的宽度。

   为了说明这一点，以下三个屏幕截图使用同一个视频。 请注意，每个区段的宽度会根据时间轴比例设置而改变。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   屏幕截图A

   以上屏幕截图A显示了29秒产品视频的默认视图。 时间轴比例设置为默认的5秒。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   屏幕截图B

   在上面的屏幕截图B中，时间轴缩放滑块从默认的5秒到3秒拖动。 请注意，单个时间轴比例时间戳现在都以3秒的间隔设置。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   屏幕截图C

   在上面的屏幕截图C中，“时间轴缩放”设置被移动到8秒。 请注意，包含产品缩略图的区段已缩小。 如果您有较长的视频并且希望能够看到通常适合页面宽度的更多区段的概述，以这种方式进行缩小很有用。

1. （可选）执行以下操作之一：

   * 调整区段的开始时间和结束时间。



      选择一个区段，然后拖动前导或尾部蓝色椭圆以分别调整开始或结束时间。 显示的视频帧会根据您的调整，移动到视频中的相应时间。时间轴区段的移动会受到时间轴中任意相邻区段的限制。最少允许区段有一秒钟的时长。



      可使用以下导航快捷方式快速地查看和微调视频区段：


      * 点按前导蓝色椭圆，将视频直接搜索到该区段的开头。
      * 点按尾部蓝色椭圆，将视频直接搜索到该段的末尾。
      * 点按整个区段，使视频播放返回到该区段的开头。

   ![chlimage_1-26](assets/chlimage_1-132.png)

   调整时间轴区段结尾的位置

   * 删除区段

      Select the last segment that is on the timeline, then on the toolbar, tap **[!UICONTROL Delete Segment.]** 如果选择了两个或多个段，则会禁用“删除段”功能。

      您只能删除最后一个区段。For example, if you wanted to delete all the segments on the timeline, you must always select the last one, then tap **[!UICONTROL Delete Segment.]**


1. 选择要将一个或多个缩略图关联到的时间区段。
1. 在视频右侧，点按&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡。
1. 在内容选项卡下，点 **[!UICONTROL 按选择资]**&#x200B;产，然后浏览并选择您要用于视频的所有图像资产。 选定的资产会添加到“内容”选项卡的“资产选择器”面板。

1. 在“内容”选项卡下的资产选择器中，执行下列任一操作：

   <table>
      <tbody>
        <tr>
        <td>将缩略图关联到选定的时间轴区段</td>
        <td><p>点按右侧资产选择器面板中的图像。</p> <p>您可以向时间轴区段中添加任意所需数量的缩略图。对于您选择的每个图像，资产选择器中相应图像的上方便会出现一个对勾标记。</p> </td>
        </tr>
        <tr>
        <td>将缩略图从选定的时间轴区段中删除</td>
        <td><p>执行以下操作之一：</p>
          <ul>
          <li>在资产选择器面板中，点按带有复选标记的图像以取消选择它。 图像资产会从时间轴区段中删除。<br /> </li>
          <li>在选定的时间轴区段中，点按一幅图像，然后点按工具栏中的<strong>删除产品</strong>。</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![资产选取器](assets/chlimage_1-133.png)

   点击资产选择器面板中的图像会将其添加到选定的时间轴区段。

1. 在某个时间轴区段内选择一个缩略图，然后点按&#x200B;**[!UICONTROL 操作]**&#x200B;选项卡。
1. 执行以下操作之一：
   <table> 
    <tbody> 
      <tr> 
      <td>将所选缩略图与概览相关联</td> 
      <td><p>在“操作类型”下，点 <strong>按概览</strong>。</p> <p>如果您是AEM Sites和电子商务客户：</p> 
       <ul> 
       <li>请注意，“SKU 值”文本字段会预先填充选定产品的 SKU（库存单位），即您提供的每个不同产品或服务的唯一标识符。当图像与AEM Commerce中的产品关联时，会自动填充该字段。</li> 
       <li>如果预填充的SKU不正确，请点按或单击产品选取器图标（放大镜）以打开选择产品页面。 点按或单击要使用的产品，然后点按页面右上角的复选标记，以返回到交互式视频编辑器。</li> 
       </ul> <p> 如果您不是 <em>AEM Sites</em> 或电子商务客户</p> 
       <ul> 
       <li>请参阅<a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">识别热点变量</a>。您需要定义这些变量。 </li> 
       <li>默认情况下，此SKU字段使用图像资产的文件名，但不带扩展名。 如果您的基于 SKU 的文件遵循标准的命名规范，则通常不需要进行任何额外的编辑。 </li> 
       <li>否则，请编辑默认值并输入正确的SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），即您优惠的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充概览模板的变量部分，以便系统能够将点击的图像与特定SKU的概览相关联。</li> 
       </ul> <p>(Optional) If there are other variables within the Quickview that you need to use to further identify a product, tap <strong>Add Generic Variable</strong>. 在文本字段中，指定其他变量。 例如，<code>category=Womens</code> 就是一个添加的变量。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>将选定的缩略图与超链接相关联</td> 
      <td><p>在“操作类型”下，点 <strong>按超链</strong>接，然后执行下列操作之一：</p> 
       <ul> 
       <li>如果您是AEM Sites客户，请点按站点选择器图标（文件夹）以导航到网页。 请注意，如果您的交互式内容包含相对URL的链接，特别是指向AEM Sites页面的链接，则无法使用基于URL的链接方法。</li> 
       <li>如果您是独立的Dynamic Media客户，请在“HREF”文本字段中指定链接网页的完整URL路径。</li> 
       </ul> <p>请确保指定是在新的浏览器选项卡还是在当前的选项卡中打开链接。</p> </td> 
      </tr> 
      <tr> 
      <td>将所选缩略图与体验片段关联</td> 
      <td><p>在操作类型下，点 <strong>按体验片</strong>段，然后执行以下操作：<p> 
       <ul> 
       <li>如果您是AEM Sites客户，请点按或单击搜索图标（放大镜）以打开体验片段页面。 点按或单击要使用的体验片段，然 <strong>后 </strong>点按页面右上角的选择，以返回到上一页上的操作面板。<br /> 请参 <a href="/help/sites-authoring/experience-fragments.md">阅体验片段</a>。</li> 
      </ul> 
       <ul> 
       <li>指定体验片段在视频中的显示方式，如同其宽度和高度一样。</li>
       </ul><strong>注意</strong>:请注意，在体验片段中嵌入查看器时，不支持交互式视频中的社交媒体共享工具。 要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。</p></tr>&lt; 
      <tr> 
      <td>编辑已分配给缩略图的操作</td> 
      <td>在某个时间轴区段内，点按其文本标签右侧带有链式链接的缩略图。该链式链接表示已向该缩略图分配操作。点按<strong>操作</strong>选项卡以进行更改。</td> 
      </tr> 
      <tr> 
      <td>更改缩略图的文本标签</td> 
      <td><p>默认情况下，文本标签使用缩略图的元数据 <code>Title</code> 字段。 If <code>Title</code> is not present, the thumbnail image's filename is used instead, but without the extension.</p> <p>To change the text label of a thumbnail image, under the <strong>Actions </strong>tab, directly below the image asset that is displayed, enter the desired text. 请参阅下面的插图。</p> <p>请注意，新文本标签仅供视频播放器本身以及时间轴区段中显示的缩略图文本使用。标签更改不会影响缩略图的“标题”元数据字段及其文件名。</p> </td> 
      </tr> 
      <tr> 
      <td>还原所做的更改</td> 
      <td>在页面的右上角附近，点按<strong>撤消</strong>或<strong>重做</strong>。</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   新文本标签会添加到缩略图。

1. 执行下列操作之一：

   * 重复第6-11步，将更多缩略图添加到视频中的时间轴区段。
   * 继续执行可选步骤13。

1. （可选）执行下列操作之一：

   * **[!UICONTROL 合并区段]** -您可以将两个相邻的区段（无论是否分配了产品缩略图）合并到一个区段中。

      在时间轴上，点按要合并到一个中的两个或多个连续段。 请注意，下图中的两个选定段上没有蓝色椭圆拖动手柄。

      点按 **[!UICONTROL 工具栏]** 上的合并区段。
   ![chlimage_1-134](assets/chlimage_1-134.png)

   将两个选定的五个第二段合并为一个十个第二段。

   * **[!UICONTROL 拆分段]** -您可以将单个段分为两个等时段的段。 如果已为区段分配了产品缩略图，则缩略图会合并到左侧区段中。

      在时间轴上，点按要分成两半的区段，然后点按工 **[!UICONTROL 具栏上的]** “拆分区段”。

      选择两个或多个段将禁用“拆 **[!UICONTROL 分段]** ”功能。
   ![chlimage_1-133](assets/chlimage_1-135.png)

   将选定的10秒段分为两段，每段5秒。

1. 在“创建交互式视频”页 **[!UICONTROL 面的右上角]** ，将显示与视频一起使用的当前选定查看器预设的名称。 点按名称以选择其他查看器预设。

   例如，`Shoppable_Video_light` 查看器预设能够让您在播放视频时，在视频旁边留出一个白色显示区域。该显示区域用于在播放视频时，显示可点击的缩略图。`Shoppable_Video_dark` 查看器预设则能够让您在播放视频时，在视频旁边留出一个黑色显示区域。


   如果您创建了自己的交互式视频查看器预设，您还会在预设列表中看到该查看器预设，您可以从中进行选择。

   完成后，点按保 **[!UICONTROL 存。]**

   >[!NOTE]
   在保存交互式视频时，会自动保存 `.vtt` 一个关联的文件。 文 `.vtt` 件将保存到位于资 `_VTT` 产根目录的文 **[!UICONTROL 件夹。]**&#x200B;要在网站上正确播放交互式视频，必须填写文件和文件夹。 因此，请勿移动、编辑或删除文件夹 `_VTT` 或其内容。

1. 发布交互式视频。发布后会创建嵌入代码或 URL，最后您需要将该嵌入代码或 URL 复制并粘贴到您的网站体验。

   如果您使用Quickviews添加交互性，则只使用嵌入代码；如果您通过超链接的网页添加了交互性，则还可以使用已发布的URL。 但是，请注意，如果您的交互式内容包含与相对URL(特别是指向AEM Sites页面的链接)的链接，则无法使用基于URL的链接方法。

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

   >[!NOTE]
   要使用Quickviews发布购物视频，请确保还从您的商务区域单独发布每个视频的相关图像资产。

   在添加时间轴区段并发布交互式视频后，您便可以将其添加到您的现有网站登录页面。See [Integrating an interactive video with your website.](#integrating-an-interactive-video-with-your-website)

## 发布交互式视频资源 {#publishing-interactive-video-assets}

See [Publishing Assets](/help/assets/publishing-dynamicmedia-assets.md) for details on how to publish interactive video assets.

## Integrating an interactive video with your website {#integrating-an-interactive-video-with-your-website}

现在，在上传视频、向视频添加时间轴区段并发布交互式视频后，您便可以将其添加到您的现有网站。

如果您是AEM Sites的客户，则可以通过将交互式媒体组件拖动到页面来添加交互式视频。 See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

如果您是独立的AEM Assets客户，则可以按本节所述手动将交互式视频添加到您的网站。

1. 复制已发布的交互式视频的嵌入代码或 URL。

请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

如果您使用Quickviews添加交互性，则只使用嵌入代码；如果您通过超链接的网页添加了交互性，则还可以使用已发布的URL。 但是，请注意，如果您的交互式内容包含与相对URL(特别是指向AEM Sites页面的链接)的链接，则无法使用基于URL的链接方法。

1. 在目标网页代码中，找到静态视频所在的位置。

1. 删除静态视频，并将其代码原封不动地替换为您从 AEM 资产中复制的嵌入代码或 URL。

由于复制的嵌入代码是为响应式环境设计的，因此该代码应该会自动地适应之前由静态视频所占用的区域。

>[!NOTE]
至此，如果您只是通过超链接的网页添加交互性，您就已经完成了所有操作。
但是，如果您为触发概览而添加了任何交互性，则交互式视频旁边的缩略图仅用于显示目的；它们尚未与您现有的Quickviews集成。 在这种情况下，您现在需要将交互式视频与网站上的现有Quickviews相集成。

**示例**

以演示网站为例：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-0.html)

请注意，它是标准视频嵌入代码：

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

集成过程很简单，只需删除视频嵌入代码并将其替换为AEM中的交互式视频嵌入代码。 您可以在以下URL查看结果。 虽然它在页面上显示交互式视频，但尚未与现有概览相集成：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-1.html)

## 将交互式视频与现有Quickview集成 {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
此任务仅在您是独立的AEM Assets客户时适用。

该过程的最后一步是将交互式视频与网站上使用的现有Quickview实现相集成。 但是，没有任何一种集成解决方案是在所有情况下都适用的。每个Quickview实施都是独一无二的。 因此，需要一种最可能需要前端IT人员协助的特定方法。

现有Quickview实现通常表示在网页上按以下顺序发生的一系列相互关联的操作：

1. 用户在网站的用户界面上触发一个元素。
1. 前端代码根据在步骤1中触发的用户界面元素获取Quickview URL。
1. 前端代码使用步骤2中获取的URL发送AJAX请求。
1. 后端逻辑将相应的概览数据或内容返回到前端代码。
1. 前端代码加载Quickview数据或内容。
1. （可选）前端代码将加载的Quickview数据转换为HTML表示形式。
1. 前端代码显示一个模态对话框或面板，并将 HTML 内容呈现在屏幕上以供最终用户查看。

这些调用并非独立的公共 API 调用（可以由网页逻辑从任意步骤进行调用）。相反，这些调用属于链式调用，即，每个后续步骤都隐藏在前一步的最后阶段（回调）。

在替换步骤1和部分步骤2的同时，当用户单击交互式视频中的缩略图时，查看器将处理此类用户交互。 查看器将返回一个事件到网页，其中包含之前添加到AEM的所有缩略图数据。

在这种事件处理程序中，前端代码执行以下操作：

* 监听交互式视频发出的事件。
* 根据缩略图数据构建概览URL。
* 触发从后端加载概览并在屏幕上显示概览的过程。

此外，交互式视频查看器支持全屏操作模式。 最终用户通过单击缩略图而不离开全屏来触发Quickview。 要实现此功能，请更改前端代码，以便将Quickview模态对话框附加到查看器的容器。 请勿添加文档BODY或查看器处于全屏模式时不可用的其他网页元素。 执行此作业的代码需要听取在页面上加载查看器后发送的另一个查看器回调。

AEM返回的嵌入代码已具有现成的事件处理程序。 它被注释掉，如下面突出显示的代码片段所示：

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

因此，只需取消上面突出显示的代码片断的注释，并将虚拟处理程序主体替换为特定网页的特定代码。

标准嵌入代码中存在两个默认回调处理函数： `quickViewActivate` 和 `initComplete`。 在查 `quickViewActivate` 看器中单击缩略图时，处理函数会触发。 使用它将查看器与Quickview激活逻辑集成。 当查 `initComplete` 看器加载到页面时，处理函数只触发一次。 此处理函数用于调整网页DOM中的Quickview对话框位置。

构建Quickview URL的过程与识别本主题前面介绍的缩略图变量的过程相反。 使用我们之前标识的Quickview URL示例，您可以了解在各种情况下如何构建Quickview URL:

<table>
  <tbody>
  <tr>
    <td><p>单个 SKU，位于查询字符串中</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>单个 SKU，位于 URL 路径中</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>SKU 和类别 ID，位于查询字符串中</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

触发Quickview URL并激活Quickview面板的最后一步很可能需要IT部门的前端IT人员的协助。 他们最了解如何通过适当的步骤准确地触发Quickview实施，并拥有现成的Quickview URL。

您可以了解如何将这些步骤应用到演示网站，以将交互式视频与概览代码完全集成。 在本主题的前面，Quickview URL的结构如下所示：

```xml
/datafeed/$CategoryId$-$SKU$.json
```

使用对象中的可用字段(通 `quickViewActivate` 过查看器的代码 `categoryId``sku``inData` 传递给该处理程序)，可以轻松地在处理程序中重建此URL，如下所示：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

The demo website is triggering the Quickview dialog box using a simple `loadQuickView()` function call. 此函数只使用一个参数，即Quickview数据URL。 So the last step needed to integrate the interactive video is to add the following line of code to the `quickViewActivate` handler:

```xml
loadQuickView(quickViewUrl);
```

最后，确保将Quickview对话框附加到查看器的容器元素。 默认嵌入代码提供实现此功能的示例步骤。 要获取对查看器容器元素的引用，可使用以下几行代码：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

其中 `inner_container` 是对查看器所管 `DIV` 理的元素的引用。 您希望该对话框是该对话框的子项 `DIV`。

实际定位模态对话框元素并将其附加到上述容器的步骤是特定的。 同样，您可以向熟悉所需Quickview实施的前端开发人员寻求帮助。

在示例网站中，Quickview模态对话框是作为直接附 `DIV` 加到文档的概览模态ID来实现的 `BODY`。 因此，将该对话框移动到查看器容器的代码与以下代码一样简单：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

完整的源代码如下：

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

具有完全集成的交互式视频的最终演示网站如下所示：

[https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-video/john-lewis/landing-3.html)

## 使用概览创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/custom-pop-ups.md).
