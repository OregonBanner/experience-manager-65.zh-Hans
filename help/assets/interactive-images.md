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
feature: 交互式图像
role: Business Practitioner, Administrator
exl-id: 8a609024-e9e6-4805-8306-48d095110eb6
source-git-commit: c59ec6e2429095c07c9b2d6bb83dad6ab4f80aa0
workflow-type: tm+mt
source-wordcount: '4286'
ht-degree: 18%

---

# 交互式图像{#interactive-images}

通过将“购物”热点拖放到图像上，您可以轻松地为客户打造出丰富且引人入胜的静态图像体验。购物热点将有关产品或服务的其他信息与直接的销售点“添加到购物车”或“购买”功能相结合。客户可以点按或单击这些热点，并直接链接到产品或服务、将其添加到购物车或链接到网页。 诸如此类的直接体验可以提高您网站上的客户参与度和转化率。

下面是一个带有概览弹出窗口的购物横幅。 用户通过点按模型上的圆或“热点”来激活概览。

![chlimage_1-152](assets/chlimage_1-368.png)

通过转到以下内容，查看上述网页上的交互式图像的实际操作情况：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html)

## 观看如何创建交互式图像横幅 {#watch-how-interactive-image-banners-are-created}

播放有关如何创建交互式图像横幅的演练](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)（10分33秒）。 [您还可以了解如何预览、编辑和传送交互式图像横幅。

## 快速入门：交互式图像 {#quick-start-interactive-images}

以下工作流分步描述旨在帮助您快速启动并运行Adobe Experience Manager Assets中的交互式图像。

请查找某些“快速入门”任务中的&#x200B;**示例**&#x200B;标题。本指南包含一个简短教程，该教程基于以下尚未添加交互式图像的网页示例：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

本教程有助于说明在您的网站上集成交互式图像的步骤。

交互式图像步骤：

1. **（可选）识别热点变量**  — 如果您使用Experience Manager资产和Dynamic Media独立版，请首先识别现有概览实施中使用的动态变量。然后，您可以在创建交互式图像时输入热点数据。 请参阅[（可选）识别热点变量](#optional-identifying-hotspot-variables)。
但是，如果您使用Adobe Experience Manager Sites、Adobe Experience Manager eCommerce或两者，则无需执行此步骤。
请参阅Experience Manager资产](/help/commerce/cif-classic/administering/concepts.md)中的[电子商务概念。

1. **（可选）创建交互式图像查看器预设**  — 自定义用于表示热点的图形图像。如果您打算改用名为`Shoppable_Banner`的现成交互式图像查看器预设，则无需创建您自己的交互式图像查看器预设。
请参阅[（可选）创建交互式图像查看器预设](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)。

1. **上传图像横幅**  — 上传要进行交互的图像横幅。请参阅[上传图像横幅](#uploading-an-image-banner)。

1. **将热点添加到图像横幅**  — 向图像横幅添加一个或多个热点，并将每个热点与操作（如超链接、概览或体验片段）相关联。添加热点后，您将通过发布交互式图像来完成此任务。

   * 请参阅[将热点添加到图像横幅](#adding-hotspots-to-an-image-banner)。
   * 请参阅[预览交互式图像](#optional-previewing-interactive-images) — 可选。 如果需要，您可以查看购物横幅的呈现形式并测试其交互性。

   * 有关如何发布交互式图像资产的详细信息，请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

1. **将交互式图像添加到您的网站**  — 如果您使用Experience Manager站点或电子商务，或者同时使用这两者，则可以将交互式图像添加到Experience Manager中的网页。将交互式媒体组件拖动到页面上。 请参阅[将Dynamic Media Assets添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

   如果您使用Experience Manager资产和Dynamic Media独立版，则必须复制您网站上的嵌入代码，然后将其与现有概览相集成。 请参阅[将交互式图像与您的网站集成](#integrating-an-interactive-image-with-your-website)。

   如果您使用的是第三方WCM（Web内容管理器），则必须将新的交互式视频与您网站上使用的现有概览实施相集成。 请参阅[将交互式图像与现有Quickview](#integrating-an-interactive-image-with-an-existing-quickview)集成。

## （可选）识别热点变量 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>仅当满足以下条件时，才需要执行此任务：
>
>* 要通过触发概览来为图像添加交互性。
>* 您的Experience Manager实施&#x200B;*not*&#x200B;使用电子商务集成框架将产品数据从任何电子商务解决方案(如IBM® WebSphere® Commerce、Elastic Path、hybris或Intershop)拉入Experience Manager。 请参阅Experience Manager资产](/help/commerce/cif-classic/administering/concepts.md)中的[电子商务概念。

>
>
如果您的Experience Manager实施使用电子商务，则可以跳过此任务并继续执行下一项任务。

首先，识别现有概览实施所使用的动态变量，以便您输入热点数据以创建交互式图像。

在Experience Manager资产中向横幅图像添加热点时，必须为每个热点分配一个SKU（库存单位和可选的其他变量）。 此类热点变量稍后会用于将热点与概览内容进行匹配。

必须准确地识别要与热点数据相关联的变量数量及类型，这一点很重要。而且，添加到横幅图像的每个热点都必须附带足够的信息，以便能够在现有的后端系统中明确地识别产品。

有多种不同的方法可以识别用于热点数据的变量集。

有时，只需咨询负责现有概览实施的IT专家即可。 IT专家可能会知道在系统中识别概览所需的最少数据集。 但是，也可以简单地分析前端代码的现有行为。

大多数概览实施都使用以下范例：

* 用户在网站上激活用户界面元素。例如，单击“概览”按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* 概览数据会转换为内容，以准备在网页上渲染。
* 最后，前端代码以可视形式将这些内容呈现在屏幕上。

然后，方法是访问现有网站中实施了概览功能的不同区域。 然后，您触发概览并捕获由网页发送的用于加载概览数据或内容的Ajax URL。

通常情况下，您不需要使用任何专业的调试工具。现代的 Web 浏览器具备 Web 检查器，可以实现相同的功能。下面列举了一些具备 Web 检查器的 Web 浏览器：

* 要在 Google Chrome 中查看发出的所有 HTTP 请求，请按 F12 键以打开“开发人员工具”面板，然后单击“网络”选项卡。在Mac上，按Command+Option+I打开“开发人员工具”面板，然后单击“网络”选项卡。

* 在 Firefox 中，您既可以按 F12 键并使用其“网络”选项卡来激活 Firebug 插件，也可以使用内置的检查器工具及其“网络”选项卡。在Mac上，按Command+Option+I打开“开发人员工具”面板，然后单击“检查器”选项卡。

在浏览器中打开网络监控时，会触发页面上的概览。

现在，在网络日志中找到Quickview Ajax URL，并复制记录的URL以供将来分析。 通常，在触发概览时，会向服务器发送大量请求。 通常，Quickview Ajax URL是列表中最先使用的URL之一。 它具有复杂的查询字符串部分或路径，其响应MIME类型为`text/html`、`text/xml`或`text/javascript`。

在此过程中，访问网站中具有不同产品类别和类型的不同区域非常重要。 原因是概览URL可能包含给定网站类别的通用部分，但仅当您访问网站的其他区域时才会发生更改。

在最简单的情况下，概览URL中唯一的变量部分是产品SKU。 在这种情况下，SKU 值就是您将热点添加到横幅图像时唯一需要提供的数据。

但是，在复杂的情况下，除SKU之外，快速视图URL还具有不同的可变元素，例如类别ID、颜色代码和大小代码。 在这种情况下，在Experience Manager资产的交互式购物图像功能中，每个元素都是热点数据定义中的一个单独变量。

请考虑以下概览URL及其生成的热点变量示例：

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
    </ul> <p>URL 中唯一的变量部分是 productId= 查询字符串参数的值，很明显它就是 SKU 值。因此，您的热点只需在SKU字段中填充<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong>等值即可。</p> </td>
  </tr>
  <tr>
    <td><p>单个 SKU，位于 URL 路径中。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>变量部分位于路径的最后一部分，它将成为热点的SKU值：<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>。</p> </td>
  </tr>
  <tr>
    <td><p>SKU 和类别 ID，位于查询字符串中。</p> </td>
    <td><p>记录的概览URL包括：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL 中有两个可变部分。SKU存储在<code>prodId</code>参数中，类别ID<code></code>存储在<code>category=</code>参数中。</p> <p>因此，热点定义是成对存在的，即，SKU值和一个名为<code>categoryId</code>的额外变量。 生成的各对如下所示：</p>
    <ul>
      <li><p>SKU为<strong><code>305466</code></strong>, <code>categoryId</code>为<code>1100004</code>。</p> </li>
      <li><p>SKU为<strong><code>310181</code></strong>, <code>categoryId</code>为<strong><code>1100004</code></strong>。</p> </li>
      <li><p>SKU为<strong><code>308706</code></strong>, <code>categoryId</code>为<strong><code>1740148</code></strong>。</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**示例**

您可以将上述三个示例中所用的方法运用到演示网页：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

演示网页包含多个产品缩略图，每个缩略图都有一个标有“查看更多”的“概览”按钮。 如果Web浏览器的调试工具仍处于激活状态，请单击每个按钮并记下记录的概览URL。 激活页面上所有四个可用的产品概览后，您会向后端发出以下概览请求列表：

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

查看服务器调用时，您会看到特定于产品的信息仅存在于请求路径中。 您还注意到查询字符串根本不被使用，并且涉及两种不同类型的数据段：

* 第一种类型是“男”或“女”。 您可以将此类别称为“产品”。
* 第二种类型是产品名称，如CamoPullover。 您可以假定此信息是产品SKU。

根据此信息，整个概览URL具有以下模式：

`/datafeed/$categoryId$-$SKU$.json`

依据上述分析，您可以在热点中使用 `categoryId` 和 `SKU`。

现在，您可以使用Experience Manager资产中的交互式购物图像功能，上传图像横幅并向其添加热点。

## （可选）创建交互式图像查看器预设 {#optional-creating-an-interactive-image-viewer-preset}

您可以选择使用默认的名为`Shoppable_Banner`且随Experience Manager资产一起提供的现成交互式图像查看器预设。 或者，您也可以创建自己的自定义查看器预设，以用于交互式图像。

创建自定义交互式图像查看器预设时，您可以确定图像横幅上热点的外观。 在创建查看器预设的过程中，您可以选择使用预定义图像库中提供的热点图形。

在保存查看器预设后，查看器预设会在“Experience Manager资产”的“查看器预设”列表页面上自动激活（打开）。 此功能意味着无论您何时查看资产，都可以在交互式媒体组件中看到该内容。 但是，要使用此查看器预设交付&#x200B;**&#x200B;交互式横幅，您还必须&#x200B;*发布*&#x200B;您的查看器预设。 对于自定义或现成查看器预设，此规则为true。

**要创建交互式图像查看器预设，请执行以下操作：**

1. 在左边栏中，点按&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**。
1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 创建]**。
1. 在“新查看器预设”对话框中，键入一个用于描述该交互式横幅查看器预设的名称。


   保存后，标题会显示在“查看器预设”列表页面中。

1. 在“富媒体类型”下拉菜单中，选择&#x200B;**[!UICONTROL 交互式图像]**。
1. 点按&#x200B;**[!UICONTROL 创建]**。
1. 在“编辑查看器预设”页面中，点按&#x200B;**[!UICONTROL 外观]**&#x200B;选项卡。
1. 执行下列操作之一：

   * 要上传您自己的热点图像以在图像上使用，请点按“资产选取器”图标。在“选择内容”页面上，导航到您要使用的热点图像，将其选中，然后点按右上角的对勾标记图标。
   * 要选择预定义的热点图像，请点按“热点图库”图标。在热点图库面板上，点按您要使用的热点图像。

1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 保存]**。

   请确保您发布了新查看器预设。

   请参阅[发布已添加的查看器预设](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)。

   现在，您便可以上传图像横幅。

## 上传图像横幅 {#uploading-an-image-banner}

如果您已上传要使用的图像，请前进到下一步[将热点添加到图像横幅](#adding-hotspots-to-an-image-banner)。

**要上传图像横幅，请执行以下操作：**

1. 上传您要实现交互的图像横幅。

   请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。


   现在，您可以向图像横幅中添加热点；请参阅下面的下一项任务。

## 将热点添加到图像横幅 {#adding-hotspots-to-an-image-banner}

您可以使用热点管理页面上的编辑器将热点添加到图像横幅。

添加热点时，您可以将热点定义为“概览”弹出显示、超链接或体验片段。

请参阅[体验片段](/help/sites-authoring/experience-fragments.md)。

>[!NOTE]
>
>在体验片段中嵌入查看器时，不支持交互式图像中的社交媒体共享工具。 要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。

在当前创建/编辑会话期间，支持页面右上角附近的撤消和重做选项。

创建完交互式图像后，您可以使用“预览”来查看交互式图像在客户中的显示方式。

请参阅[（可选）预览交互式图像](#optional-previewing-interactive-images)。

>[!NOTE]
>
>在交互式图像或轮播横幅中向图像添加热点时，热点信息会存储在同一元数据位置。 该位置是相对于图像位置的，无论它是交互式图像还是轮播横幅。 此功能意味着您可以在任意查看器中轻松重复使用同一图像及其定义的热点数据。
传送横幅支持图像上的图像映射，图像上也可以包含热点；交互式图像不会。 如果您打算创建使用相同图像的交互式图像或轮播横幅，请记住此规则。 您可以使用同一图像的不同副本来创建交互式图像和传送横幅。
另请参阅[传送横幅](/help/assets/carousel-banners.md)。

>[!NOTE]
如果您正在使用热点编辑交互式图像并裁剪图像，则热点会被删除。

**要将热点添加到图像横幅，请执行以下操作：**

1. 在“资产”视图中，导航到要进行交互的图像横幅。
1. 执行下列操作之一：

   * 将鼠标悬停在图像上，然后点按&#x200B;**[!UICONTROL 选择]**（复选标记图标）。 在工具栏中，点按&#x200B;**[!UICONTROL 编辑]**。

   * 将鼠标悬停在图像上，然后点按&#x200B;**[!UICONTROL 更多操作]**（三个圆点图标）**[!UICONTROL 编辑]**。

   * 点按图像，以便在“详细信息视图”页面中将其打开。 在工具栏中，点按&#x200B;**[!UICONTROL 编辑]**。

1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL 添加热点]**（手指点按图标）以打开热点管理页面。
1. 在页面的左上角附近，点按&#x200B;**[!UICONTROL 热点]**。

   1. 在“热点管理”页面的左上角附近，点按&#x200B;**[!UICONTROL 热点]**。
   1. 在图像上，点按您希望显示热点的位置。如有必要，可拖动热点以调整其位置。
   1. 重复步骤a和b，根据需要添加其他热点。
   1. （可选）要删除热点，请在图像上将其选中，然后点按&#x200B;**[!UICONTROL 热点]**&#x200B;标题下的&#x200B;**[!UICONTROL 删除]**（垃圾桶图标）。

1. 在“名称”文本字段中，键入热点的名称。此名称也会显示在“选定的热点”下拉列表中。
1. 执行下列操作之一：

   * 点按&#x200B;**[!UICONTROL Quickview]**。

      * 如果您是Experience Manager站点或电子商务客户，请点按或单击产品选取器图标（放大镜）以打开选择产品页面。 点按或单击要使用的产品，然后点按页面右上角的&#x200B;**[!UICONTROL 选择]**，以便您可以返回到热点管理页面。
      * 如果您是&#x200B;*not* Experience Manager站点或电子商务客户

         * 请参阅[识别热点变量](#optional-identifying-hotspot-variables);您必须定义这些变量。
         * 然后，手动输入SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），即您提供的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充概览模板的变量部分，以便系统能够将点按的热点与特定SKU的概览相关联。
         * （可选）如果快速视图中存在其他必须用来进一步标识产品的变量，请点按&#x200B;**[!UICONTROL 添加常规变量]**。 在文本字段中，指定一个额外的变量。 例如，`category=Males` 就是一个添加的变量。
   * 点按&#x200B;**[!UICONTROL 超链接]**。

      * 如果您是Experience Manager站点客户，请点按或单击站点选择器图标（文件夹）以导航到URL。 如果您的交互式内容具有包含相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。
      * 如果您是独立客户，请在“HREF”文本字段中，指定链接网页的完整URL路径。

   请确保指定是在新的浏览器选项卡（推荐为默认选项卡）还是在同一选项卡中打开链接。

   有关更多信息，请参阅[使用选择器](/help/assets/working-with-selectors.md)。

   * 点按&#x200B;**[!UICONTROL 体验片段]**。

      * 如果您是Experience Manager站点客户，请点按或单击搜索图标（放大镜）以打开体验片段页面。 点按要使用的体验片段，然后点按页面右上角的&#x200B;**[!UICONTROL 选择]**，以便您可以返回到热点管理页面。
请参阅[体验片段](/help/sites-authoring/experience-fragments.md)。

      * 指定您希望在横幅上显示的体验片段的宽度和高度。

         >[!NOTE]
         在体验片段中嵌入查看器时，不支持交互式图像中的社交媒体共享工具。 要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功将其嵌入到体验片段中。



1. 点按&#x200B;**[!UICONTROL Save]**&#x200B;以保存您的工作并返回到浏览页面。
1. 发布交互式图像。 发布后，横幅可通过云进行交付，如果您需要与第三方网站集成，则还会生成嵌入代码。

   请参阅[发布资产](/help/assets/manage-assets.md#publishing-assets)。

   添加热点并发布交互式图像后，您现在可以将其添加到现有网站。

   请参阅[将交互式图像与您的网站集成](#integrating-an-interactive-image-with-your-website)。

   >[!NOTE]
   如果您正在使用热点编辑交互式图像并裁剪图像，则热点会被删除。

### （可选）预览交互式图像 {#optional-previewing-interactive-images}

您可以使用“预览”来查看交互式图像在客户中的显示方式，并测试图像的热点以确保它们按预期行为。

如果您对交互式图像满意，可以发布该图像。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。
请参阅[将URL关联到您的Web应用程序](/help/assets/linking-urls-to-yourwebapplication.md)。 如果您的交互式内容具有包含相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。
请参阅[将Dynamic Media Assets添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

**要预览交互式图像，请执行以下操作：**

1. 在“资产”视图中，导航到您创建的现有交互式图像，然后点按以在预览中打开该图像。
1. 在“预览”页面的左上角附近，在“内容”下拉列表中，点按&#x200B;**[!UICONTROL 查看器]**。
1. 在“查看器”列表中，点按&#x200B;**[!UICONTROL Shoppable_Banner]**&#x200B;或您创建的交互式图像查看器预设的名称。
1. 如果要测试图像上的热点关联操作，请点按该图像上的热点。

## 发布交互式图像资产 {#publishing-interactive-image-assets}

有关如何发布交互式图像资产的详细信息，请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

## 将交互式图像与您的网站集成 {#integrating-an-interactive-image-with-your-website}

现在，在上传横幅图像、将热点添加到图像并发布交互式图像后，您便可以将其添加到您的网站页面。

如果您是Experience Manager站点客户，则可以通过将交互式媒体组件拖动到您的页面上来添加交互式图像。 请参阅[将Dynamic Media Assets添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

如果您是独立的Experience Manager资产客户，则可以按照此部分中的所述，手动将交互式图像添加到您的网站。

1. 复制已发布的交互式图像的嵌入代码。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

1. 将复制的嵌入代码添加到网页中的所需位置。
复制的嵌入代码是为响应式环境设置的，以便自动适合分配的区域。

**示例**

以演示网站为例：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html)

请注意，这三个雄性的图片是一个静态`IMG`标记：

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

集成过程很简单，只需删除`IMG`标记并将其替换为从Experience Manager资产中复制的嵌入代码即可。 您可以通过下面的 URL 查看最终效果，即页面上会显示带有三个圆形热点的交互式购物图像：

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html)

>[!NOTE]
因此，演示网站交互式购物图像上的热点仅用于显示目的；它们尚未与现有概览集成。

要为响应式环境对交互式购物图像应用“裁剪”，您可以将交互式图像配置属性`ZoomView.iscommand`包含到路径中。 组件`ZoomView`被调用，`iscommand`是您应用的“裁剪”图像服务命令。

请参阅 [ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html) 配置属性。

请参阅[裁剪](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html)图像服务命令。

现在，您可以将交互式图像与网站上的现有概览相集成。

## 将交互式图像与现有概览相集成 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
此任务仅在您是独立Experience Manager资产客户时才适用。

此过程的最后一步是，将交互式图像与您网站上的现有概览实施相集成。 但是，没有任何一种集成解决方案是在所有情况下都适用的。每个概览实施都是独一无二的，需要一种特定的方法。 这可能需要前端IT人员的协助。

现有的概览实施通常表示在网页上发生的一系列相互关联的操作，这些操作按以下顺序发生：

1. 用户在网站的用户界面上触发一个元素。
1. 前端代码根据在步骤1中触发的用户界面元素来获取概览URL。
1. 前端代码使用在第 2 步获取的 URL 发送一个 Ajax 请求。
1. 后端逻辑会将相应的概览数据或内容返回到前端代码。
1. 前端代码加载概览数据或内容。
1. 或者，前端代码会将加载的概览数据转换为HTML表示形式。
1. 前端代码显示一个模态对话框或面板，并将 HTML 内容呈现在屏幕上以供最终用户查看。

这些调用不表示独立的公共API调用，网页逻辑可从任意步骤中调用这些调用。 相反，这些调用属于链式调用，即，每个后续步骤都隐藏在前一步的最后阶段（回调）。

如果用交互式购物图像来替换第 1 步的操作以及第 2 步的部分操作，则与此同时，当用户单击购物图像中的热点时，查看器就会处理此类用户交互。查看器会向网页返回一个事件，其中包含之前添加到Experience Manager资产的所有热点数据。

在此类事件处理程序中，前端代码会执行下列操作：

* 监听交互式购物图像发出的事件。
* 根据热点数据构建概览URL。
* 触发从后端加载概览并在屏幕上呈现概览以供显示的过程。

由Experience Manager资产返回的嵌入代码已经具有一个可供使用的事件处理程序，该处理程序已被注释掉，如以下高亮显示的代码片段所示：

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

构建概览URL的过程与识别前面介绍的热点变量的过程相反。

请参阅[识别热点变量](#optional-identifying-hotspot-variables)。

使用前面的概览URL示例，您可以在以下示例中看到如何在每种情况下构建概览URL:

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

触发概览URL并激活概览面板的最后一步，很可能需要IT部门的前端IT人员的协助。 他们深知如何通过正确的步骤准确触发概览实施，从而拥有现成的概览URL。

您可以了解如何将这些步骤应用到演示网站，以便将交互式购物图像与概览代码完全集成。 以前，概览URL的结构如下所示：

```xml
/datafeed/$categoryId$-$SKU$.json
```

要在`quickViewActivate`处理程序中重建此URL，可以使用`inData`对象中可用的`categoryId`和`SKU`字段，该对象通过查看器代码传递到处理程序：

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

演示网站使用简单的`loadQuickView()`函数调用触发“概览”对话框。 此函数仅采用一个参数，即概览数据URL。 因此，集成交互式购物图像的最后一步是将下面一行代码添加到`quickViewActivate`处理程序：

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

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html)

## 使用概览创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

请参阅[使用概览](/help/assets/custom-pop-ups.md)创建自定义弹出窗口。
