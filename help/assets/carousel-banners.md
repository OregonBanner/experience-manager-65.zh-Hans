---
title: 传送横幅
description: 了解如何在Dynamic Media中使用传送横幅
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '4813'
ht-degree: 20%

---


# 传送横幅{#carousel-banners}

传送横幅使营销人员能够轻松创建交互式旋转促销内容并将其交付到任何屏幕，从而推动转化。

创建和修改促销横幅中特有的内容可能非常耗时，从而限制您快速发布新内容或使其更具针对性的能力。 旋转横幅使您能够快速创建或修改旋转横幅，添加与产品详细信息或相关资源链接的热点等交互性，并将它们交付到任何屏幕——从而更快地将新的促销内容推向市场。

传送横幅由带有CAROUSELSET字样的横幅 **[!UICONTROL 指定]**:

![chlimage_1-438](assets/chlimage_1-438.png)

在您的网站上，传送横幅可以如下所示：

![chlimage_1-439](assets/chlimage_1-439.png)

您可以在此浏览图像（通过单击数字）。 此外，幻灯片会根据可自定义的时间间隔自动旋转。 您在旋转横幅中添加的图像支持热点和图像映射，用户可以点按或转到超链接或访问快速视图窗口。

在此示例中，用户已点击或单击图像映射，并访问手套的快速视图窗口：

![chlimage_1-440](assets/chlimage_1-440.png)

## 观看如何创建传送横幅 {#watch-how-carousel-banners-are-created}

观看10分钟33秒的演练，了解如 [何创建传送横幅](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)。 您还将学习如何预览、编辑和传送传送横幅。

>[!NOTE]
>
>必须将非管理用户添加到 **[!UICONTROL dam-users组]** ，才能创建或编辑传送横幅。 如果您在创建或编辑时遇到问题，请咨询系统管理员，他可以将您添 **[!UICONTROL 加到dam用户组]** 。

## 快速开始:传送横幅 {#quick-start-carousel-banners}

要快速设置并运行图像集，请执行以下操作：

1. [识别热点和图像映射变量](#identifying-hotspot-and-image-map-variables) (仅适用于使用AEM Assets+ Dynamic Media的客户)

   开始，识别现有快速视图实施所使用的动态变量，以便在AEM Assets的传送横幅创建过程中输入适当的热点和图像映射数据。

   >[!NOTE]
   >
   >如果您是AEM Sites或电子商务客户，则可以使用内置功能导航到产品页面并查找产品目录中的现有外观。 您无需手动输入热点或图像映射变量。 请参阅有关设 [置电子商务的信息](/help/sites-administering/generic.md)。
   >
   >
   >如果您是AEM Assets和Dynamic Media的客户，您将手动输入热点和图像地图的数据，然后将已发布的URL或嵌入代码集成到您的第三方内容管理系统中。

1. 可选：根据需要[创建轮播集查看器预设](/help/assets/managing-viewer-presets.md)。

   如果您是管理员，则可以通过创建自己的传送查看器预设来自定义传送的行为和外观。 主要优点是，您可以为多个轮盘重复使用此自定义查看器预设。 但是，用户还可以选择在创作传送时直接自定义传送的行为和外观。 当您希望为给定传送设计非常具体时，这是首选方法。

1. [上传图像横幅](#uploading-image-banners)。

   上传您要实现交互的图像横幅。

1. [创建传送集](#creating-carousel-sets)。

   在轮盘集中，用户在横幅图像之间导航，并点按热点或图像地图以访问相关内容。

   要在 Assets 中创建轮播集，请点按&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 轮播集。]**&#x200B;将资产添加到幻灯片，然后点按&#x200B;**[!UICONTROL 保存。]**&#x200B;您还可以直接在编辑器中编辑轮播集的外观和行为。

1. [将热点或图像映射添加到图像横幅。](#adding-hotspots-or-image-maps-to-an-image-banner)

   将一个或多个热点或图像映射添加到图像横幅，并将每个热点或图像映射与链接、概览或体验片段等操作相关联。 添加热点或图像地图后，通过发布传送集来完成此任务。 发布后会创建可用于复制并应用于网站登陆页的嵌入代码。

   请参 [阅（可选）预览传送横幅](#optional-previewing-carousel-banners) -可选。 如果需要，您可以视图轮盘集的表示并测试其交互性。

1. [发布传送横幅。](#publishing-carousel-banners)

   您可以像发布任何资产一样发布传送集。 在资产中，导航到传送集，然后选择它并点按发 **[!UICONTROL 布。]** 发布传送集时，将激活URL和嵌入字符串。

1. 执行下列操作之一：

   * [将传送横幅添加到您的网站页面](#adding-a-carousel-banner-to-your-website-page) 。您可以添加已复制到网站页面上的传送横幅URL或嵌入代码。

      * [将轮盘横幅与现有概览相集成](#integrating-the-carousel-banner-with-an-existing-quickview)。 如果您使用的是第三方Web内容管理系统，则需要将新的传送横幅与网站上现有的Quickview实现相集成。
   * [在AEM中向网站添加传送横幅](/help/assets/adding-dynamic-media-assets-to-pages.md) 如果您是AEM Sites客户，可以使用交互式媒体组件将传送集直接添加到AEM的页面。


If you need to edit Carousel Sets, see [editing Carousel Sets.](#editing-carousel-sets) 此外，您还可以视图和编 [辑传送集属性](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/managing-assets-touch-ui.html#editing-properties)。

## 识别热点和图像映射变量 {#identifying-hotspot-and-image-map-variables}

开始，通过识别现有快速视图实施所使用的动态变量，以便在AEM Assets的传送集创建过程中输入热点或图像映射数据。

在AEM Assets向横幅图像添加热点或图像映射时，您需要为每个热点或图像映射分配一个SKU和可选的其他变量。 以后会使用这些变量将热点或图像地图与快速视图内容进行匹配。

>[!NOTE]
>
>如果您是AEM Sites和／或AEM电子商务客户，请跳过此步骤。 无需手动识别热点或图像映射变量；您可以使用与Ecommerce的集成进行产品集成。 请参阅有关设 [置电子商务的信息](/help/sites-administering/generic.md)。 此外，您可以使用交互式组件并将其添加到网页。
>
>如果您是AEM Assets或媒体客户，则应发布URL或嵌入代码，然后与第三方内容管理系统集成，并手动识别热点和图像地图。

必须正确识别要与热点或图像地图数据关联的变量的数量和类型。 添加到横幅图像的每个热点或图像映射都必须包含足够的信息，以便在现有的后端系统中明确地识别产品。 同时，每个热点或图像映射不应包含超出必要范围的数据。 其原因在于，这会使数据输入过程变得过于复杂，并且持续的热点或图像映射管理更容易出错。

有不同的方法可识别用于热点或图像地图数据的一组变量。

有时可能需要向负责现有概览实施的 IT 专家进行咨询，因为他们可能了解要在系统中识别概览所需的最少数据集。但在大多数情况下，可能只需简单地分析前端代码的现有行为即可。

大部分概览实施采用以下模式：

* 用户在网站上激活用户界面元素。例如，点按&#x200B;**[!UICONTROL 快速查看]**&#x200B;按钮。
* 网站根据需要向后端发送 Ajax 请求来加载概览数据或内容。
* 概览数据转换成准备在网页上呈现的内容。
* 最后，前端代码以可视形式将这些内容呈现在屏幕上。

因此，采用的方法是访问现有网站上实施了概览功能的不同区域，触发概览，并且捕获由网页发出的用于加载概览数据或内容的 Ajax URL。

通常情况下，您不需要使用任何专业的调试工具。现代的 Web 浏览器具备 Web 检查器，可以实现相同的功能。下面列举了一些具备 Web 检查器的 Web 浏览器：

* 要在Google Chrome中查看所有传出HTTP请求，请按F12(Windows)或Command-Option-I(Mac)打开“Developer Tools”（开发人员工具）面板，然后点击“Network”（网络）选项卡。
* 在Firefox中，您可以通过按F12(Windows)或Command-Option-I(Mac)并使用其“网络”选项卡来激活Firebug插件，也可以使用内置的检查器工具及其“网络”选项卡。

在浏览器中开启网络监控功能后，页面上便会触发概览。

现在，从网络日志中找到概览 Ajax URL，然后复制记录的 URL 以供将来分析时使用。在大多数情况下，当您触发概览时，会有大量请求发出到服务器。通常，概览 Ajax URL 排在列表的首位。It has either a complex query string portion or path, and its response MIME type is either `text/html`, `text/xml`, or `text/javascript`.

在这个过程中，您需要访问网站中具有不同产品类别和类型的不同区域，这一点很重要。这是因为，对于特定的网站类别，概览 URL 的某些部分可能是通用的，只有在您访问网站的不同区域时才会发生更改。

在最简单的情况下，产品 SKU 是概览 URL 中唯一的变量部分。在这种情况下，SKU值是您向横幅图像添加热点或图像映射时唯一需要的数据。

但是，在复杂的情况下，概览 URL 除了 SKU 之外还有一些不同的可变元素，例如类别 ID、颜色代码、大小代码，等等。在这种情况下，每个元素都是热点或旋转横幅功能中图像映射数据定义中的单独变量。

请考虑以下快速视图URL及其生成的热点或图像映射变量示例：

<table>
 <tbody>
  <tr>
   <td>单个 SKU，位于查询字符串中。</td>
   <td><p>记录的概览 URL 包括：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>The only variable part in the URL is the value of the <code>productId=</code> query string parameter, and it is clearly a SKU value. 因此，我们的热点或图像映射只需要填充值(如 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>单个 SKU，位于 URL 路径中。</td>
   <td><p>记录的概览 URL 包括：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>The variable part is in the last portion of the path, and it becomes the SKU value of the hotspots/image maps:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU 和类别 ID，位于查询字符串中。</td>
   <td><p>记录的概览 URL 包括：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL 中有两个可变部分。The SKU is stored in the <code>prodId</code> parameter and the category ID is stored in the <code>category=</code>parameter.</p> <p>因此，热点／图像映射定义是成对存在的。 即，一个 SKU 值对应一个额外的变量 <code>categoryId</code>。生成的各对如下所示：</p>
    <ul>
     <li><p>SKU is <strong><code>305466</code></strong> and <code>categoryId</code> is <code>1100004</code>.</p> </li>
     <li><p>SKU is <strong><code>310181</code></strong> and <code>categoryId</code> is <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU is <strong><code>308706</code></strong> and <code>categoryId</code> is <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 上传图像横幅 {#uploading-image-banners}

如果已上传要使用的图像，请前进到下一步创建传送 [集](#creating-carousel-sets)。 请注意，在启用Dynamic Media后，必须上传传送中使用的图像。

要上传图像横幅，请参阅 [上传资产](/help/assets/managing-assets-touch-ui.md)。

## 创建传送集 {#creating-carousel-sets}

>[!NOTE]
>
>必须将非管理用户添加到 **[!UICONTROL dam-users组]** ，才能创建或编辑传送横幅。 如果您在创建或编辑时遇到问题，请咨询系统管理员，他可以将您添 **[!UICONTROL 加到dam用户组]** 。

**创建传送集**

1. 在资产中，导航到要创建传送集的文件夹，然后点按创 **[!UICONTROL 建>传送集。]**
1. 在传送横幅编辑器页面上，点按 **[!UICONTROL 点按以打开资产选择器]** ，为您的第一张幻灯片选择图像。

   在“传送横幅编辑器”页面上，执行下列操作之一：

   * Near the upper-left corner of the page, tap **[!UICONTROL Add Slide]** icon.

   * 在页面中间附近，点按 **[!UICONTROL 以打开资产选择器。]**
   点按以选择要包含在轮播集中的资产。选定资产上有一个复选标记图标。When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Select]**.

   借助资产选择器，您可以通过键入关键字并点按或单击&#x200B;**[!UICONTROL 返回来搜索资产。]**&#x200B;您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后点按工具栏上的&#x200B;**[!UICONTROL 过滤器]**&#x200B;图标。Change the view by tapping the View icon and selecting **[!UICONTROL Column View]**, **[!UICONTROL Card View]**, or **[!UICONTROL List View.]**

   有关更 [多信息，请参](/help/assets/working-with-selectors.md) 阅使用选择器。

1. 继续添加幻灯片，直到添加了要在旋转集中旋转的所有图像。
1. （可选）执行以下操作之一：

   * 如有必要，请拖动幻灯片以在这些列表中重新排序图像。
   * 要删除图像，请选择图像，然后点按工 **[!UICONTROL 具栏上的]** “删除幻灯片”。

   * 要应用预设，请点按页面右上角附近的预设下拉列表，然后选择要一次应用到该预设集的预设。
   要删除幻灯片，请点按或单击幻灯片，然后点按或单 **[!UICONTROL 击工具栏中]** 的删除幻灯片。 要移动幻灯片，请点按重排器图标，按住并移至所需位置。

1. 在幻灯片中添加图像后，您可以向图像添加热点和／或图像映射。 请参 [阅添加热点或图像地图](#adding-hotspots-or-image-maps-to-an-image-banner)。
1. 通过点按或单击“行为和外观”选项卡，并调整传送横幅的外观或特定组件的行为，可以更改传送集的可视设计和行为。 有关 [如何使用查看器编辑](/help/assets/viewer-presets.md) 器的更多信息，请参阅管理查看器预设。

   >[!NOTE]
   >
   >对于传送横幅，您可能需要调整以下内容：
   >    * 图像显示的持续时间。 默认情况下，每幅图像显示9秒。
   >    * 动画. 默认情况下，每个幻灯片过渡都是淡入淡出。 您可以将其更改为幻灯片过渡。
   >    * 按钮的样式。 用户点击每个点或数字即可在横幅中旋转。 您可以更改设置指示符按钮的显示位置（如果它们是数字或虚线样式）以及它们的大小。
   >    * 更改图像映射的高亮样式或用于热点的图标。
   >    * 在编辑查看器预设之前，请选择要将该预设作为基础的样式。 如果不这样做，则在您开始编辑查看器预设时，如果您决定更改其他预设，您将丢失所有更改。
   >
   >有关 [查看器编辑器的详细说明](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset) 和详细信息，请参阅传送横幅的特殊注意事项。

   您还可以预览传送横幅的外观。 请参 [阅（可选）预览传送横幅](#optional-previewing-carousel-banners)。

1. 完成后 **[!UICONTROL 点按]** “保存”。

## 向图像横幅添加热点或图像映射 {#adding-hotspots-or-image-maps-to-an-image-banner}

您可以使用传送集编辑器将热点或图像映射添加到横幅。

添加热点或图像映射时，可以将热点或图像映射定义为概览弹出显示、超链接或体验片段。

请参阅 [体验片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
>
>请注意，在体验片段中嵌入查看器时，轮盘横幅中不支持社交媒体共享工具。
>
>要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。

在向图像添加热点或图像映射时，切记保存您的工作。 在当前创建／编辑会话中，页面右上角附近支持撤消和重做选项。

创建完传送横幅后，您可以选择使用预览来查看传送横幅对客户的显示方式。

请参 [阅（可选）预览传送横幅。](#optional-previewing-carousel-banners)

>[!NOTE]
>
>当您在交互式图像或传送横幅 [中向图像](/help/assets/interactive-images.md) 添加热点时，热点信息会存储在相同的元数据位置——相对于图像的位置和控制板，而不管该位置是交互式图像还是传送横幅。 此功能意味着您可以在任一查看器中轻松重复使用同一图像及其定义的热点数据。

>但是，请注意，传送横幅支持图像上的图像地图，这些图像上也可能包含热点；交互式图像则不会。 如果要创建使用同一图像的交互式图像或传送横幅，请牢记这一点。 您可能希望改为使用同一图像的单独副本创建交互式图像和传送横幅。

>[!NOTE]
>
>如果您正在使用热点编辑交互式图像并裁剪图像，则您的热点将被删除。

另请参阅[添加图像映射](/help/assets/image-maps.md)。

**向图像横幅添加热点或图像映射**

1. 从资产中，导航到要进行交互的传送集。
1. 选择传送集，然后点按 **[!UICONTROL 编辑。]** 将打开传送查看器编辑器。
1. 选择要进行交互的幻灯片。
1. Near the upper-left corner of the page, tap **[!UICONTROL Hotspot]** or **[!UICONTROL Image Map.]**
1. 执行下列操作之一：

   * 对于热点：在图像上，点按您希望显示热点的位置。
   * 对于图像映射：在图像上，单击，然后从左上角拖动到右下角以创建图像映射区域。 您可以通过拖动角来调整图像映射的大小。

   如有必要，请将热点或图像映射拖到新位置。 根据需要添加其他热点或图像地图。

   要删除热点或图像映射，请点按&#x200B;**[!UICONTROL 操作]**&#x200B;选项卡。在&#x200B;**[!UICONTROL 映射和热点]**&#x200B;标题下，从&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉菜单中，选择要删除的热点或图像映射的名称。Tap the **[!UICONTROL Trash]** icon next to the menu, then tap **[!UICONTROL Delete.]**

1. 在“名称”文本字段中，键入热点或图像映射的名称。 This name also appears in the **[!UICONTROL Maps &amp; Hotspot]** drop-down list. 如果您决定在将来对热点或图像地图进行更改，提供名称可让您轻松识别该热点或图像地图。
1. 在“操作”选项卡中执行下列 **[!UICONTROL 操作]** 之一：

   * 点按 **[!UICONTROL 概览。]**

      * 如果您是AEM Sites和电子商务客户，请点按产品选取器图标（放大镜）以打开“选择产品”页面。 点按要使用的产品，然后点按页面右上角的复选标记，以返回到传送横幅编辑器。
      * 如果您不是AEM Sites或电子商务客户

         * 请参 [阅识别热点](#identifying-hotspot-and-image-map-variables) 变量，就像您想要定义这些变量一样。
         * 然后，手动输入SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），即您优惠的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充快速视图模板的变量部分，以便系统能够将点按的热点与特定SKU的快速视图关联。
         * (Optional) If there are other variables within the quick view that you need to use to further identify a product, tap **[!UICONTROL Add Generic Variable.]** In the text field, specify an additional variable. 例如，类别=Mens是添加的变量。

         * 有关更 [多信息，请参](/help/assets/working-with-selectors.md) 阅使用选择器。
   * Tap **[!UICONTROL Hyperlink.]**

      * 如果您是AEM Sites客户，请点按站点选择器图标（文件夹）以导航到URL。
         >[!NOTE]
         >
         >如果您的交互式内容包含与相对URL(特别是指向AEM Sites页面的链接)的链接，则无法使用基于URL的链接方法。

      * 如果您是独立客户，请在“HREF”文本字段中指定链接网页的完整URL路径。

   请确保指定是在新的浏览器选项卡（建议使用默认选项卡）还是在同一选项卡中打开链接。

   有关更 [多信息，请参](/help/assets/working-with-selectors.md) 阅使用选择器。

   * Tap **[!UICONTROL Experience Fragment.]**

      * 如果您是AEM Sites客户，请点击搜索图标（放大镜）以打开体验片段页面。 点按或单击要使用的体验片段，然后点按页面右上角的选择以返回到热点管理页面。
请参 [阅体验片段](/help/sites-authoring/experience-fragments.md)。

      * 指定体验片段在横幅上的显示方式，如同其宽度和高度一样。

         >[!NOTE]
         >
         >请注意，在体验片段中嵌入查看器时，轮盘横幅中不支持社交媒体共享工具。
         >要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。

   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   您还可以预览传送横幅的外观。 请参 [阅（可选）预览传送横幅](#optional-previewing-carousel-banners)。

1. Tap **[!UICONTROL Save.]**
1. 发布传送集。 发布会创建可在网站页面上使用的嵌入代码或URL。 如果您是AEM Sites客户，可以直接将传送集添加到网页。

   请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

   请参 [阅将传送集添加到网站登陆页](#adding-a-carousel-banner-to-your-website-page)

## 编辑传送集 {#editing-carousel-sets}

>[!NOTE]
>
>必须将非管理用户添加到 **[!UICONTROL dam-users组]** ，才能创建或编辑传送横幅。 如果您在创建或编辑时遇到问题，请咨询系统管理员，他可以将您添 **[!UICONTROL 加到dam用户组]** 。

您可以对传送集执行各种编辑任务，如：

* 向传送集添加幻灯片。 另请参阅 [使用选择器](/help/assets/working-with-selectors.md)。
* 在传送集中对幻灯片重新排序。
* 删除传送集中的资产。
* 应用查看器预设。
* 删除传送集。
* 添加或编辑热点和图像地图。 另请参阅 [使用选择器](/help/assets/working-with-selectors.md)。

**编辑传送集**

1. 执行下列任一操作：

   * 将鼠标悬停在旋转集资产上，然后点按 **[!UICONTROL 编辑]** （铅笔图标）。
   * 将鼠标悬停在传送集资产上，点按 **[!UICONTROL 选择]** （复选标记图标），然后点 **[!UICONTROL 按工具栏]** 上的编辑。

   * Tap on a Carousel Set asset, then in the upper-left corner of the page tap **[!UICONTROL Edit]** (pencil icon).

1. 要编辑传送集，请执行下列任一操作：

   * To add a slide, tap the **[!UICONTROL Add Slide]** icon then navigate to the asset you want to add to that slide and tap or click the checkmark.
   * 要对幻灯片重新排序，请将幻灯片拖到新位置（选择重新排序图标以移动项目）。
   * 要添加热点或图像映射，请单击热点或图像映射图标，请参阅添 [加热点和图像映射](#adding-hotspots-or-image-maps-to-an-image-banner)。
   * To edit the appearance or behavior of the carousel set, tap the **[!UICONTROL Appearance]** tab or **[!UICONTROL Behavior]** tab, then set the options you want.
   * 要编辑热点或图像映射，请在相应的幻灯片上选择热点或图像映射，然后根据需要在“操作”选项卡下 **[!UICONTROL 进行]** 更改。
   * 要删除幻灯片，请选择它，然后点按工 **[!UICONTROL 具栏上的]** “删除幻灯片”。
   * To apply a preset, near the upper-right corner of the page, tap the **[!UICONTROL Preset]** drop-down list, then select a viewer preset.
   * 要删除整个传送集，请导航到传送集，将其选中，然后点按删 **[!UICONTROL 除。]**

   >[!NOTE]
   >
   >如果您正在使用热点编辑交互式图像并裁剪图像，则您的热点将被删除。

## （可选）预览传送横幅 {#optional-previewing-carousel-banners}

您可以使用预览来查看传送横幅对客户的外观，并测试传送横幅热点和图像映射以确保它们按预期的方式显示。

当您对传送横幅感到满意时，可以发布它。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。请参阅[将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)。请注意，如果您的交互式内容包含相对URL的链接，特别是指向AEM Sites页面的链接，则无法使用基于URL的链接方法。
See [Adding Dynamic Media Assets to pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

您可以从传送编辑器（首选方法）或查看器预览传送 **[!UICONTROL 横幅]** 。

**预览传送横幅**

1. 在资 **[!UICONTROL 产中]**，导航到您已创建的现有传送横幅，然后点按以将其打开。
1. 点按 **[!UICONTROL 编辑。]**
1. 在工具栏右角的查看器预设列表中，选择一个查看器以预览传送横幅。

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. 点按 **[预览。]**
1. 点按图像上的热点或图像映射，以测试其关联的操作。

**从“查看器”预览传送横幅列表**

1. 在资 **[!UICONTROL 产中]**，导航到您已创建的现有传送横幅，然后点按以将其打开。
1. 在预览页面的左上角附近，单击内容图标。
1. 在页 **[!UICONTROL 面左侧]** “查看器”列表卡中，点按要使用的传送横幅查看器预设的名称。
1. 点按图像上的热点或图像映射，以测试其关联的操作。

## 发布传送横幅 {#publishing-carousel-banners}

您需要发布传送才能使用它。 发布传送集时，将激活URL和嵌入代码。 它还将传送发布到Dynamic Media云，该云与CDN集成，可进行可扩展且高性能的投放。

>[!NOTE]
>
>如果您将现有的带热点的交互式图像用于传送横幅，则必须在发布传送横幅后单独发布该交互式图像。
>此外，如果您修改了在传送横幅中使用的预先存在的已发布交互式图像，则必须先发布交互式图像，然后才能将这些更改反映到传送横幅中。

有关 [如何发布传送横幅](/help/assets/publishing-dynamicmedia-assets.md) ，请参阅发布Dynamic Media资产。

## 将传送横幅添加到网站页面 {#adding-a-carousel-banner-to-your-website-page}

在上传横幅图像以创建传送、向横幅添加热点和／或图像映射并发布传送集后，您现在可以将其添加到现有网站页面。

>[!NOTE]
>
>如果您是AEM Sites的客户，则可以通过将交互式媒体组件拖动到页面，将传送横幅直接添加到您的页面。 See [Adding Dynamic Media Assets to Pages.](/help/assets/adding-dynamic-media-assets-to-pages.md)

但是，如果您是独立的AEM assets客户，则可以按本节所述手动将传送横幅添加到您的网站登陆页。

1. 复制已发布的传送集的嵌入代码。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

1. 将您从AEM Assets复制的嵌入代码添加到您的网页。
复制的嵌入代码是响应式的，因此它应自动适合页面的嵌入区域。

## 将传送横幅与现有概览相集成 {#integrating-the-carousel-banner-with-an-existing-quickview}

注意：此步骤仅在您是独立的AEM Assets客户时适用。

此过程的最后一步是将传送横幅与网站上的现有快速视图实施相集成。 每个概览实施都是独一无二的，都需要特定的方法，并且极有可能需要前端 IT 人员的协助。

通常情况下，现有的概览实施表示按照下列顺序，在网页上发生的一系列相互关联的操作：

1. 用户在网站的用户界面上触发一个元素。
1. 前端代码根据在第 1 步触发的用户界面元素，获取一个概览 URL。
1. 前端代码使用在第 2 步获取的 URL 发送一个 Ajax 请求。
1. 后端逻辑向前端代码返回相应的概览数据或内容。
1. 前端代码加载概览数据或内容。
1. （可选）前端代码将加载的概览数据转换为 HTML 表现形式。
1. 前端代码显示一个模态对话框或面板，并将 HTML 内容呈现在屏幕上以供最终用户查看。

这些调用并非独立的公共 API 调用（可以由网页逻辑从任意步骤进行调用）。相反，这些调用属于链式调用，即，每个后续步骤都隐藏在前一步的最后阶段（回调）。

在轮盘横幅替换步骤1和部分步骤2的同时，当用户单击轮盘横幅中的热点或图像映射时，查看器将处理此类用户交互。 查看器将返回一个事件，该网页包含之前添加的所有热点或图像映射数据。

在此类事件处理程序中，前端代码会执行下列操作：

* 监听轮盘横幅发出的事件。
* 根据热点或图像映射数据构建快速视图URL。
* 触发从后端加载概览并将概览呈现在显示屏幕上的进程。

AEM Assets返回的嵌入代码已经有一个现成的事件处理程序，它已被注释掉。

因此，只需取消对该代码的注释，并用针对特定网页的代码来替换虚拟处理程序主体即可。

构建快速视图URL的过程与之前介绍的用于识别热点和图像映射变量的过程基本相反。

请参 [阅识别热点和图像映射变量](#identifying-hotspot-and-image-map-variables)。

触发概览 URL 并激活概览面板的最后一步操作，极有可能需要 IT 部门的前端 IT 人员提供协助。他们最了解在拥有可用的概览 URL 之后，如何采取正确的步骤来准确地触发概览实施。

## 使用概览创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

See [Using Quickviews to create custom pop-ups](/help/assets/custom-pop-ups.md).
