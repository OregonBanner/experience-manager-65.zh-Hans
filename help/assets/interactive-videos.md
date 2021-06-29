---
title: 交互式视频
description: 了解如何在Dynamic Media中使用交互式视频和购物视频
uuid: c3ff6839-fff5-4709-8163-5c4245b80e6d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 04be55f2-c7d8-45ef-89e5-58856b971de5
docset: aem65
feature: 交互式视频
role: Business Practitioner, Administrator
exl-id: d118879d-c17b-43f3-9cc8-0405531b4d9f
source-git-commit: c59ec6e2429095c07c9b2d6bb83dad6ab4f80aa0
workflow-type: tm+mt
source-wordcount: '6015'
ht-degree: 19%

---

# 交互式视频{#interactive-videos}

您可以轻松创建交互式视频（也称为购物视频），以直接从视频促进转化。 客户在视频播放器一侧的面板中与视频进行交互，根据视频展示的内容，相关的服务、信息或产品缩略图会滚动到客户的视线中。客户可以点按缩略图并直接链接到相应的服务，也可以将项目添加到购物车以立即购买，或者链接到某个网页以了解更多信息。

视频结束时，所有提供项目的可视汇总会显示出来以发出行动动员。客户还有其他机会点按所需的项目。诸如此类的可操作和特定体验可以提高客户参与度和转化率。

另请参阅[交互式图像](/help/assets/interactive-images.md)。

## 交互式视频的实际操作情况 {#interactive-video-in-action}

要查看交互式购物视频的实际操作情况，请单击[实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html)，滚动到页面上的&#x200B;**[!UICONTROL 购物视频]**&#x200B;标题，然后单击购物视频。

* 在播放过程中，由于视频中使用了产品，因此相同的产品会以缩略图的形式显示在右侧。

* 如果要暂停视频并打开产品概览，请单击缩略图。 例如，单击视频中的KitchenAid缩略图图像可体验混合器的360度旋转视图，或放大以查看混合器详细信息。

<!-- There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This now needs to call a new interactive video-->

![交互式购物视频中的帧](assets/chlimage_1-126.png) *从交互式购物视频中捕获视频帧。*

>[!NOTE]
>
>如果创建交互式视频以在用户单击缩略图时启动网页，则某些设备会阻止弹出网页打开。 在这种情况下，您必须更改设备上的弹出窗口阻止程序设置。 例如，在Apple iPhone 6上，点按&#x200B;**[!UICONTROL 设置]** > **Safari** > **阻止弹出窗口**，然后将控件滑动到&#x200B;**[!UICONTROL 关闭]**。 现在，当您播放交互式视频并单击缩略图时，如果要打开弹出窗口，系统会提示您。 如果接受，则会打开网页。

### 观看如何创建交互式视频 {#watch-how-interactive-videos-are-created}

播放有关如何创建交互式视频的演练](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)（7分30秒）。
[尽管视频演练使用Assets（按需）进行标记，但Adobe Experience Manager Assets中的交互式视频仍适用这些原则和步骤。

### Adobe 客户成功网络研讨会 {#adobe-customer-success-webinar}

“在Experience Manager资产中使用交互式视频、链接共享和YouTube共享”网络研讨会将向您讲授如何使用交互式视频和其他功能，将转化驱动的事件绑定到您的视频营销内容中。

>[!NOTE]
>
>[在Experience Manager资产中使用交互式视频、链接共享和YouTube共享](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/)。

## 快速入门：交互式视频 {#quick-start-interactive-videos}

下面的工作流分步说明旨在帮助您在 Dynamic Media 中快速设置并运行交互式视频。

请查找某些“快速入门”任务中的&#x200B;**示例**&#x200B;标题。它包含一个简短教程，该教程基于&#x200B;*尚未*&#x200B;添加交互性的此起始演示网页：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

**示例**&#x200B;有助于说明在您的网站上集成交互式视频的步骤。

当您完成上一个示例部分中的教程后，具有完全集成的交互式视频的最终演示网页如下所示：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

交互式视频步骤：

1. **（可选）识别概览变量**  — 首先，识别现有概览实施所使用的动态变量。在创建交互式视频时，您可以使用变量将产品缩略图映射到其相应的产品概览。 请参阅[（可选）识别概览变量](#optional-identifying-quickview-variables)。
   *仅当满足以下所有条件时，才需要执行此步骤*:·您希望通过触发概览来为视频添加交互性。·您的Experience Manager实施&#x200B;*not*&#x200B;使用电子商务集成框架将产品数据从任何电子商务解决方案(如IBM® WebSphere® Commerce、Elastic Path、Hybris或Intershop)提取到Experience Manager中。 请参阅Experience Manager资产](/help/commerce/cif-classic/administering/concepts.md)中的[电子商务概念。

1. **（可选）创建交互式视频查看器预设**  — 自定义构成播放器的各种组件的外观和行为，如视频清理器和交互式缩略图。如果您打算改用现成的交互式视频查看器预设`Shoppable_Video_Light`或`Shoppable_Video_Dark`，则无需创建您自己的交互式视频查看器预设。
请参阅[创建查看器预设](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)（可选）和[创建交互式查看器预设的特殊注意事项](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset)。

1. **上传视频及其关联的图像资产**  — 上传您要进行交互的视频和关联的图像。请参阅[上传视频及其关联的缩略图资产](#uploading-a-video-and-its-associated-thumbnail-assets)。

1. **为视频添加交互性**  — 向视频添加一个或多个时间区段。然后，关联这些时间区段中的图像缩略图。 将每个图像缩略图分配给操作，如超链接、概览或体验片段。
(如果您的交互式内容具有包含相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。)
最后，发布交互式视频资产。 发布后会创建嵌入代码或URL，您最终会将该嵌入代码或URL复制并应用到您的网站登录页面。 请参阅[为视频添加交互性](#adding-interactivity-to-your-video)。
请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

1. **在Experience Manager中将交互式视频添加到您的网站或您的网站**  — 如果您使用Experience Manager站点或电子商务，或者同时使用这两者，则可以将交互式视频添加到网页。将交互式媒体组件拖动到页面上的Experience Manager。 请参阅[将Dynamic Media Assets添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md)。
使用嵌入代码或URL将交互式视频与您的网站体验相集成。 请参阅[将交互式视频与您的网站集成](#integrating-an-interactive-video-with-your-website)。
如果您使用的是第三方WCM（Web内容管理器），则必须将新的交互式视频与您网站上使用的现有概览实施相集成。 请参阅[将交互式视频与现有概览](#integrating-an-interactive-video-with-an-existing-quickview)集成。
   [将Dynamic Media Assets添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md)

## （可选）识别概览变量 {#optional-identifying-quickview-variables}

>[!NOTE]
>
>仅当满足以下条件时，才需要执行此任务：
>
>* 要通过触发概览来为视频添加交互性。
>* 您的Experience Manager实施&#x200B;*not*&#x200B;使用电子商务集成框架将产品数据从任何电子商务解决方案(如IBM® WebSphere® Commerce、Elastic Path、Hybris或Intershop)拉入Experience Manager。 请参阅Experience Manager资产](/help/commerce/cif-classic/administering/concepts.md)中的[电子商务概念。

>
>
如果您的Experience Manager实施使用电子商务，则可以跳过此任务并继续执行下一项任务。

首先，识别现有概览实施所使用的动态变量，以便您能够在交互式视频创建过程中将产品缩略图映射到其相应产品概览。

在向视频添加时间区段时，您需要为添加到区段的每个缩略图分配一个SKU（库存单位）和任何其他变量。 此类变量稍后用于显示正确的概览产品。

必须准确地识别唯一触发产品概览所需的变量，这一点很重要。

有时，只需咨询负责现有概览实施的IT专家即可。 他们可能知道系统中用于标识概览的最少数据集。 但是，也可以简单地分析前端代码的现有行为。

大多数概览实施都使用以下范例：

* 用户在网站上激活用户界面元素。例如，单击“概览”按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* 概览数据会转换为内容，以准备在网页上渲染。
* 最后，前端代码以可视形式将这些内容呈现在屏幕上。

因此，方法是访问现有网站中实施了快速视图的不同区域，触发快速视图，并捕获网页发送的用于加载快速视图数据或内容的Ajax URL。

通常情况下，您不需要使用任何专业的调试工具。现代的 Web 浏览器具备 Web 检查器，可以实现相同的功能。下面列举了一些具备 Web 检查器的 Web 浏览器：

* 要在Google Chrome中查看所有传出的HTTP请求，请按&#x200B;**F12**(Windows)或&#x200B;**Command+Options+I**(Mac)以打开“开发人员工具”面板，然后单击&#x200B;**Network**&#x200B;选项卡。

* 在Firefox中，您可以通过按&#x200B;**F12**(Windows)或&#x200B;**Command+Option+I**(Mac)并使用其&#x200B;**`[Net]`**&#x200B;选项卡来激活Firebug插件，也可以使用内置的检查器工具及其“网络”选项卡。

* 在Internet Explorer中，通过按&#x200B;**F12**&#x200B;激活调试器工具。

在浏览器中打开网络监控时，会触发页面上的概览。

现在，在网络日志中找到Quickview Ajax URL，并复制记录的URL以供将来分析。 通常，触发概览时，会向服务器发送大量请求。 通常，Quickview Ajax URL是列表中最先使用的URL之一。 它具有复杂的查询字符串部分或路径，其响应MIME类型为`text/html`、`text/xml`或`text/javascript`。

在此过程中，访问网站中具有不同产品类别和类型的不同区域非常重要。 原因是概览URL可能包含给定网站类别的通用部分，但仅当您访问网站的其他区域时才会发生更改。

在最简单的情况下，概览URL中唯一的变量部分是产品SKU。 在这种情况下，产品SKU值是向交互式视频中的时间区段添加缩略图所需的唯一数据段，该Experience Manager中包含缩略图。

但是，在复杂的情况下，除了产品SKU之外，概览URL还具有不同的可变元素，例如类别ID、颜色代码和大小代码。 在这种情况下，每个此类元素都会在Experience Manager的缩略图数据定义中成为单独的变量。

请考虑以下概览URL及其生成的缩略图变量示例：

<table>
  <tbody>
  <tr>
    <td><p>单个 SKU，位于查询字符串中。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中唯一的变量部分是<code>productId=</code>查询字符串参数的值，很明显它是SKU值。 因此，您的缩略图只需在SKU字段中填充<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>等值即可。</p> </td>
  </tr>
  <tr>
    <td><p>单个 SKU，位于 URL 路径中。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>变量部分位于路径的最后一部分，它变为Experience Manager缩略图的SKU值：<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>SKU 和类别 ID，位于查询字符串中。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL 中有两个可变部分。SKU存储在<code>prodId</code>参数中，类别ID存储在<code>category=</code>参数中。</p> <p>因此，缩略图定义是成对存在的。 即，SKU值和一个名为<code>categoryId</code>的额外变量。 生成的各对如下所示：</p>
    <ul>
      <li>SKU为<code>305466</code>, <code>categoryId</code>为 <code>1100004</code></li>
      <li>SKU为<code>310181</code>, <code>categoryId</code>为 <code>1100004</code></li>
      <li>SKU为<code>308706</code>, <code>categoryId</code>为 <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

将上述方法应用于示例网站后，您的网页中会包含多个产品缩略图，每个缩略图中都有一个“查看更多”按钮：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

激活页面上所有可用的产品概览后，您会收到向后端发出的概览请求列表：

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

查看服务器调用时，您会看到特定于产品的信息仅存在于请求路径中。 您还会注意到查询字符串根本不被使用，并且涉及两种不同类型的数据段：

* 第一种是蜡烛、垫子、家具和玻璃器皿。 您可以将此类别称为“产品”。
* 第二种类型是产品代码，如233916597。 您可以假定它是“产品SKU”。

根据此信息，整个概览URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

根据这种分析，您可以得出结论，将以下两个变量用于缩略图：`categoryId`和`SKU`。

您现在可以上传视频及其关联的缩略图资产。

## （可选）创建交互式视频查看器预设 {#optional-creating-an-interactive-video-viewer-preset}

如果您打算使用默认的现成交互式视频查看器预设类型`Shoppable_Video_dark`或`Shoppable_Video_light`中的任一类型，则可以跳过此任务并继续下一步。

在创作环境中单击缩略图时，将显示“快速查看”对话框的预览。

![chlimage_1-21](assets/chlimage_1-127.png)

您可以选择创建自己的自定义交互式视频查看器预设。 您可以确定视频播放器的样式、交互式缩略图以及在视频末尾显示的缩略图网格视图等内容。

交互式视频查看器预设能够准确地呈现您添加的视频和所有时间轴区段。当您在“预览”模式下单击产品缩略图时，它还使用默认概览示例，以便您能够在发布之前测试其交互性。

在保存查看器预设后，查看器预设的状态会在“查看器预设”页面中自动设置为&#x200B;**开启**。此状态表明查看器预设在 Dynamic Media 组件中可见，预览视频时也可见。另请确保手动发布新查看器预设。

请参阅[创建新查看器预设](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)以创建您自己的交互式视频查看器预设。

## 上传视频及其关联的缩略图资产 {#uploading-a-video-and-its-associated-thumbnail-assets}

如果您已上传视频和缩略图资产，请继续执行[为视频添加交互性](#adding-interactivity-to-your-video)。

如果您上传了错误的视频或图像，或者想要删除您不再需要的已上传视频或图像，请参阅[删除资产](/help/assets/manage-assets.md#deleting-assets)。

要上传视频及其关联的缩略图资产，请执行以下操作：

1. 将视频和关联的缩略图资产上传到一个或多个所需的文件夹。

   请参阅[上传资产](/help/assets/manage-assets.md)。
请参阅[使用 FTP 作业计划功能上传资产](/help/assets/manage-assets.md)。

   现在，可以为视频添加交互性。

## 为视频添加交互性 {#adding-interactivity-to-your-video}

您可以使用“创建交互式视频”页面上的就地可视编辑器，向视频添加时间轴区段。

在添加时间轴区段后，您可以在每个区段内添加缩略图。对于添加的每个缩略图，您可以分别应用一个操作。例如，您可以将概览应用到缩略图，也可以为其分配超链接或体验片段。

请参阅[体验片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
>
>在体验片段中嵌入查看器时，不支持交互式视频中的社交媒体共享工具。 要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。

>[!NOTE]
>
>如果您的交互式内容具有包含相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。

在当前创建/编辑会话期间，支持页面右上角附近的撤消和重做选项。

在保存交互式视频后，视频会立即在“预览”中打开。从此处，您可以选择交互式视频查看器预设并播放视频，以大致了解它如何显示给客户。

**为视频添加交互性：**

1. 在“资产”视图中，导航到您上传的要实现交互的视频。
1. 执行下列操作之一：

   * 将鼠标悬停在图像上，然后点按&#x200B;**[!UICONTROL 选择]**（复选标记图标）。 在工具栏中，点按&#x200B;**[!UICONTROL 编辑]**。

   * 将鼠标悬停在图像上，然后点按&#x200B;**[!UICONTROL 更多操作]**（三个圆点图标）**[!UICONTROL >编辑]**。

   * 点按图像，以便在“详细信息视图”页面中将其打开。 在工具栏中，点按&#x200B;**[!UICONTROL 编辑]**。

1. 在“创建交互式视频”页面中，执行以下任一操作：

   * 要开始播放视频，请点按&#x200B;**[!UICONTROL 播放]**&#x200B;按钮。 当视频中出现您要突出显示的特定产品、服务或详细信息时，点按工具栏中的&#x200B;**[!UICONTROL 添加区段]**。重复上述步骤，直到视频结束。



      对于您添加的每个时间区段，向其分配一个或多个缩略图，然后将这些缩略图关联到概览产品页面以供客户购买，或关联到网页以了解更多信息。

   * 要开始播放视频，请点按&#x200B;**[!UICONTROL 播放]**&#x200B;按钮。 当视频中出现您要突出显示的特定产品、服务或详细信息时，点按&#x200B;**[!UICONTROL 暂停]**。点按&#x200B;**[!UICONTROL 添加区段]**。



      继续播放视频，并在您要添加区段的时间轴点处暂停视频，直到视频结束。

1. （可选）向左拖动&#x200B;**[!UICONTROL 时间轴缩放滑块]**&#x200B;上的栏可放大（向右拖动则缩小），以便控制已添加区段的显示详细信息量。

   ![chlimage_1-22](assets/chlimage_1-128.png)

   根据视频的长度，区段持续时间默认为以下值：

   <table>
      <tbody>
        <tr>
        <td><strong>如果视频长度为……</strong></td>
        <td><strong>区段持续时间设置默认为……</strong></td>
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
        <td>20秒<br /> </td>
        </tr>
        <tr>
        <td>30-60秒</td>
        <td>10秒</td>
        </tr>
        <tr>
        <td>30秒或更少</td>
        <td>5秒</td>
        </tr>
      </tbody>
    </table>

   视频时间轴使用的屏幕空间与其可用的空间大小相同。 因此，在调整浏览器大小时，您添加的区段会保持其正确的宽度。

   为了说明这一点，以下三个屏幕截图使用的是同一视频。 请注意，每个区段的宽度会根据时间轴缩放设置而发生更改。

   ![chlimage_1-23](assets/chlimage_1-129.png)

   屏幕截图A

   屏幕截图上方的A显示了29秒产品视频的默认视图。 时间轴比例在默认5秒处设置。

   ![chlimage_1-130](assets/chlimage_1-130.png)

   屏幕截图B

   在上面的屏幕截图B中，将时间轴缩放滑块从默认的5秒拖到3秒。 请注意，单个时间轴刻度时间戳现在都以3秒为间隔设置。

   ![chlimage_1-25](assets/chlimage_1-131.png)

   屏幕截图C

   在上面的屏幕截图C中，时间轴缩放设置已移至8秒。 请注意包含产品缩略图的区段是如何缩小的。 如果您的视频较长，并且希望能够看到通常适合页面宽度的更多区段的概述，则以这种方式缩小会非常有用。

1. （可选）执行以下操作之一：

   * 调整区段的开始时间和结束时间。



      选择一个区段，然后拖动前导或尾随的蓝色椭圆以分别调整开始或结束时间。 显示的视频帧会根据您的调整，移动到视频中的相应时间。时间轴区段的移动会受到时间轴中任意相邻区段的限制。最少允许区段有一秒钟的时长。



      可使用以下导航快捷方式快速地查看和微调视频区段：


      * 要直接将视频搜寻到该区段的开头，请点按前导的蓝色椭圆。
      * 要直接将视频搜寻到该区段的结尾，请点按尾随的蓝色椭圆。
      * 要将视频播放返回到该区段的开头，请点按整个区段。

   ![chlimage_1-26](assets/chlimage_1-132.png)

   调整时间轴区段结尾的位置

   * 删除区段

      选择时间轴上的最后一个区段，然后点按工具栏上的&#x200B;**[!UICONTROL 删除区段]**。 如果选择了两个或更多区段，则删除区段功能会被禁用。

      您只能删除最后一个区段。例如，如果要删除时间轴上的所有区段，则必须始终选择最后一个区段，然后点按&#x200B;**[!UICONTROL 删除区段]**。


1. 选择您要为其关联一个或多个缩略图的时间区段。
1. 在视频右侧，点按&#x200B;**[!UICONTROL 内容]**&#x200B;选项卡。
1. 在内容选项卡下，点按&#x200B;**[!UICONTROL 选择资产]**，然后浏览并选择您要在视频中使用的所有图像资产。 选定的资产将会添加到内容选项卡的资产选择器面板。

1. 在“内容”选项卡下方的资产选择器中，执行以下任一操作：

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
          <li>在资产选择器面板中，点按带有复选标记的图像以取消选择该图像。 图像资产将从时间轴区段中删除。<br /> </li>
          <li>在选定的时间轴区段中，点按一幅图像，然后点按工具栏中的<strong>删除产品</strong>。</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![资产选取器](assets/chlimage_1-133.png)

   点按资产选择器面板中的图像，会将其添加到选定的时间轴区段。

1. 在某个时间轴区段内选择一个缩略图，然后点按&#x200B;**[!UICONTROL 操作]**&#x200B;选项卡。
1. 执行以下操作之一：
   <table> 
    <tbody> 
      <tr> 
      <td>将选定的缩略图图像与概览相关联</td> 
      <td><p>在操作类型下，点按<strong>Quickview</strong>。</p> <p>如果您是Experience Manager站点和电子商务客户：</p> 
       <ul> 
       <li>请注意，“SKU 值”文本字段会预先填充选定产品的 SKU（库存单位），即您提供的每个不同产品或服务的唯一标识符。当图像与Experience Manager商务中的产品关联时，将自动填充此值。</li> 
       <li>如果预填充的SKU不正确，请点按或单击产品选取器图标（放大镜）以打开选择产品页面。 点按或单击要使用的产品，然后点按页面右上角的复选标记，以便您可以返回到交互式视频编辑器。</li> 
       </ul> <p> 如果您是<em>not</em>Experience Manager站点或电子商务客户</p> 
       <ul> 
       <li>请参阅<a href="/help/assets/carousel-banners.md#identifying-hotspot-and-image-map-variables">识别热点变量</a>。必须定义变量。  </li> 
       <li>默认情况下，此SKU字段会使用图像资产的文件名（不带扩展名）。 如果您基于SKU的文件遵循标准命名约定，则此文件名通常不需要进行任何其他编辑。 </li> 
       <li>否则，请编辑默认值并输入正确的SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），即您提供的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充概览模板的变量部分，以便系统能够将点按的图像与特定SKU的概览相关联。</li> 
       </ul> <p>（可选）如果快速视图中存在其他必须用来进一步标识产品的变量，请点按<strong>添加常规变量</strong>。 在文本字段中，指定一个额外的变量。 例如，<code>category=Womens</code> 就是一个添加的变量。</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>将选定的缩略图与超链接相关联</td> 
      <td><p>在操作类型下，点按<strong>超链接</strong>，然后执行下列操作之一：</p> 
       <ul> 
       <li>如果您是Experience Manager站点客户，请点按站点选择器图标（文件夹）以导航到网页。 如果您的交互式内容具有包含相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。</li> 
       <li>如果您是独立的Dynamic Media客户，请在“HREF”文本字段中，指定链接网页的完整URL路径。</li> 
       </ul> <p>请确保指定是在新的浏览器选项卡还是在当前的选项卡中打开链接。</p> </td> 
      </tr> 
      <tr> 
      <td>将选定的缩略图图像与体验片段关联</td> 
      <td><p>在操作类型下，点按<strong>体验片段</strong>，然后执行以下操作：<p> 
       <ul> 
       <li>如果您是Experience Manager站点客户，请点按或单击搜索图标（放大镜）以打开体验片段页面。 点按或单击要使用的体验片段，然后点按页面右上角的<strong>选择</strong>，以返回到上一页面上的“操作”面板。<br /> 请参阅 <a href="/help/sites-authoring/experience-fragments.md">体验片段</a>。</li> 
      </ul> 
       <ul> 
       <li>指定您希望在视频中显示的体验片段的宽度和高度。</li>
       </ul><strong>注意</strong>:在体验片段中嵌入查看器时，不支持交互式视频中的社交媒体共享工具。要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。</p></tr>&lt;&gt; 
      <tr> 
      <td>编辑已分配给缩略图的操作</td> 
      <td>在某个时间轴区段内，点按其文本标签右侧带有链式链接的缩略图。该链式链接表示已向该缩略图分配操作。点按<strong>操作</strong>选项卡，以便进行更改。</td> 
      </tr> 
      <tr> 
      <td>更改缩略图的文本标签</td> 
      <td><p>默认情况下，文本标签使用缩略图的<code>Title</code>元数据字段。 如果<code>Title</code>不存在，则会使用缩略图的文件名，但不使用扩展名。</p> <p>要更改缩略图的文本标签，请在<strong>操作</strong>选项卡的显示图像资产的正下方，输入所需的文本。 请参阅下面的屏幕截图。</p> <p>新文本标签仅供视频播放器本身以及时间轴区段中显示的缩略图文本使用。 标签更改不会影响缩略图的标题元数据字段及其文件名。</p> </td> 
      </tr> 
      <tr> 
      <td>还原更改：</td> 
      <td>在页面的右上角附近，点按<strong>撤消</strong>或<strong>重做</strong>。</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   新文本标签会添加到缩略图。

1. 执行下列操作之一：

   * 重复步骤6-11，向视频中的时间轴区段添加更多缩略图。
   * 继续执行可选步骤13。

1. （可选）执行以下任一操作：

   * **[!UICONTROL 合并区段]**  — 您可以将两个相邻的区段（无论是否分配了产品缩略图）合并到一个区段中。

      在时间轴上，点按要合并到一个中的两个或多个连续区段。 下面屏幕截图中的两个选定区段上没有蓝色的椭圆拖动手柄。

      点按工具栏上的&#x200B;**[!UICONTROL 合并区段]** 。
   ![chlimage_1-134](assets/chlimage_1-134.png)

   将两个选定的五秒区段合并为一个十秒区段。

   * **[!UICONTROL 拆分区段]**  — 您可以将一个区段划分为两个等时的区段。如果已将产品缩略图分配给区段，则缩略图会合并到左侧区段中。

      在时间轴上，点按要分成两半的区段，然后点按工具栏上的&#x200B;**[!UICONTROL 拆分区段]** 。

      选择两个或更多区段会禁用&#x200B;**[!UICONTROL 拆分区段]**&#x200B;功能。
   ![chlimage_1-135](assets/chlimage_1-135.png)

   将选定的10秒区段拆分为两个区段，每个区段为5秒。

1. 在&#x200B;**[!UICONTROL 创建交互式视频]**&#x200B;页面的右上角附近，将显示当前选定的与视频一起使用的查看器预设的名称。 如果要选择其他查看器预设，请点按名称。

   例如，`Shoppable_Video_light`查看器预设允许您在视频旁边播放一个白色显示区域的视频。 该显示区域用于在播放视频时，显示可点击的缩略图。`Shoppable_Video_dark`查看器预设允许您在视频旁边播放带有黑色显示区域的视频。

   如果您创建了自己的交互式视频查看器预设，则会在可供选择的预设列表中看到该预设。

   完成后，点按&#x200B;**[!UICONTROL Save]**。

   >[!NOTE]
   >
   >在保存交互式视频时，会自动保存 `.vtt` 一个关联的文件。 `.vtt`文件将保存到&#x200B;**[!UICONTROL Assets]**&#x200B;根目录的`_VTT`文件夹中。 要在网站上正确播放交互式视频，必须填写文件和文件夹。 因此，请勿移动、编辑或删除文件夹 `_VTT` 或其内容。

1. 发布交互式视频。发布后会创建嵌入代码或URL，您最终会将该嵌入代码或URL复制并粘贴到您的网站体验中。

   如果您是通过概览添加交互性的，则仅使用嵌入代码；如果您通过超链接的网页添加了交互性，则还可以使用已发布的URL。 但是，请注意，如果您的交互式内容具有链接相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

   >[!NOTE]
   >
   >要通过概览发布购物视频，请确保您还会从商务区域单独发布每个视频的相关图像资产。

   在添加时间轴区段并发布交互式视频后，您便可以将其添加到您的现有网站登录页面。请参阅[将交互式视频与您的网站集成](#integrating-an-interactive-video-with-your-website)。

## 发布交互式视频资产 {#publishing-interactive-video-assets}

有关如何发布交互式视频资产的详细信息，请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

## 将交互式视频与您的网站集成 {#integrating-an-interactive-video-with-your-website}

现在，在上传视频、向视频添加时间轴区段并发布交互式视频后，您便可以将其添加到您的现有网站。

如果您是Experience Manager站点客户，则可以通过将交互式媒体组件拖动到您的页面来添加交互式视频。 请参阅[将Dynamic Media资产添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

如果您是独立的Experience Manager资产客户，则可以按照此部分中的所述，手动将交互式视频添加到您的网站。

1. 复制已发布的交互式视频的嵌入代码或URL。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。
如果您是通过概览添加交互性的，则仅使用嵌入代码；如果您通过超链接的网页添加了交互性，则还可以使用已发布的URL。 但是，请注意，如果您的交互式内容具有链接相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。

1. 在目标网页代码中，找到静态视频所在的位置。

1. 删除静态视频，并将该代码原样替换为您从Experience Manager资产中复制的嵌入代码或URL。
复制的嵌入代码是为响应式环境设置的，以便自动适应之前由静态视频占用的区域。

>[!NOTE]
>
>至此，如果您只是通过超链接的网页添加交互性，您就已经完成了所有操作。
>
>但是，如果您为触发概览而添加了任何交互性，则交互式视频旁边的缩略图仅用于显示目的；它们尚未与您现有的概览相集成。 在这种情况下，您现在必须将交互式视频与网站上的现有概览相集成。

**示例**

以演示网站为例：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

请注意，嵌入代码是标准代码：

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

集成过程很简单，只需删除视频嵌入代码并将其替换为从Experience Manager中插入的交互式视频嵌入代码即可。 您可以在以下URL上查看结果。 虽然该视频在页面上显示交互式视频，但尚未与现有概览相集成：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html)

## 将交互式视频与现有概览相集成 {#integrating-an-interactive-video-with-an-existing-quickview}

>[!NOTE]
>
>此任务仅在您是独立Experience Manager资产客户时才适用。

此过程的最后一步是将交互式视频与网站上使用的现有概览实施相集成。 但是，没有任何一种集成解决方案是在所有情况下都适用的。每个概览实施都是唯一的。 因此，需要一种具体的方法，需要前端IT人员的协助。

现有的概览实施通常表示在网页上发生的一系列相互关联的操作，这些操作按以下顺序发生：

1. 用户在网站的用户界面上触发一个元素。
1. 前端代码根据在步骤1中触发的用户界面元素来获取概览URL。
1. 前端代码使用步骤2中获取的URL发送AJAX请求。
1. 后端逻辑会将相应的概览数据或内容返回到前端代码。
1. 前端代码加载概览数据或内容。
1. 或者，前端代码会将加载的概览数据转换为HTML表示形式。
1. 前端代码显示一个模态对话框或面板，并将 HTML 内容呈现在屏幕上以供最终用户查看。

这些调用不表示独立的公共API调用，网页逻辑可从任意步骤中调用这些调用。 相反，这些调用属于链式调用，即，每个后续步骤都隐藏在前一步的最后阶段（回调）。

在交互式视频替换步骤1和部分步骤2的同时，当用户单击交互式视频内的缩略图时，此类用户交互由查看者处理。 查看器会向网页返回一个事件，其中包含之前添加到Experience Manager的所有缩略图数据。

在此类事件处理程序中，前端代码会执行以下操作：

* 监听交互式视频发出的事件。
* 根据缩略图数据构建概览URL。
* 触发从后端加载概览并在屏幕上呈现概览以供显示的过程。

此外，交互式视频查看器支持全屏操作模式。 最终用户通过单击缩略图而不离开全屏来触发概览。 要实现此功能，请更改前端代码，以便将“快速查看”模式对话框附加到查看器的容器。 请勿添加文档BODY或查看器处于全屏模式时不可用的其他网页元素。 执行此作业的代码必须监听在页面上加载的查看器之后发送的一个或多个查看器回调。

由Experience Manager返回的嵌入代码已拥有一个现成的事件处理程序。 如以下高亮显示的代码片段所示，该代码片段被注释掉：

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

因此，只需取消对上面突出显示的代码片段的注释，并将虚拟处理程序主体替换为特定网页的特定代码即可。

标准嵌入代码中存在两个默认回调处理程序：`quickViewActivate`和`initComplete`。 在查看器中单击缩略图时，将触发`quickViewActivate`处理程序。 使用它将查看器与概览激活逻辑集成。 当查看器加载到页面时，`initComplete`处理程序只触发一次。 此处理程序用于调整网页DOM中的“快速查看”对话框位置。

构建概览URL的过程与识别本主题前面介绍的缩略图变量的过程相反。 使用之前已识别的概览URL示例，您可以了解在每种情况下如何构建概览URL:

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

触发概览URL并激活概览面板的最后一步，很可能需要IT部门的前端IT人员的协助。 他们深知如何通过正确的步骤准确触发概览实施，从而拥有现成的概览URL。

您可以了解如何将这些步骤应用到演示网站，以便将交互式视频与概览代码完全集成。 在本主题的前面，快速视图URL的结构如下所示：

```xml
/datafeed/$CategoryId$-$SKU$.json
```

使用`categoryId`和`sku`对象中可用的`inData`字段，轻松地在`quickViewActivate`处理程序中重建此URL，如下所示：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

演示网站使用简单的`loadQuickView()`函数调用触发“概览”对话框。 此函数仅采用一个参数，即概览数据URL。 因此，集成交互式视频的最后一步是将下面一行代码添加到`quickViewActivate`处理程序：

```xml
loadQuickView(quickViewUrl);
```

最后，确保将“快速查看”对话框附加到查看器的容器元素。 默认嵌入代码提供了实现此功能的示例步骤。 要获取对查看器容器元素的引用，可以使用以下代码行：

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

其中，`inner_container`是对查看器管理的`DIV`元素的引用。 您希望该对话框是该`DIV`的子项。

实际找到模态对话框元素并将其附加到上述容器的步骤具体因大小写而异。 再次重申，您可以向熟悉所需Quickview实施的前端开发人员寻求帮助。

如果您使用示例网站，则“快速视图”模式对话框将实施为`DIV` ，并且该快速视图模式ID直接附加到文档`BODY`。 因此，将该对话框移动到查看器容器的代码与以下代码一样简单：

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

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

## 使用概览创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

请参阅[使用概览](/help/assets/custom-pop-ups.md)创建自定义弹出窗口。
