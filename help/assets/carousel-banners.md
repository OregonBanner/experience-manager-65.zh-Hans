---
title: 轮播横幅
description: 了解如何在Dynamic Media中使用轮播横幅
uuid: 73684a08-d84d-4665-ab89-3a1bf88ac5dd
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e26c7f7f-bdd7-421a-8614-ba48abf381d2
docset: aem65
feature: Carousel Banners
role: User, Admin
exl-id: 53d34d3a-ecb6-4fa0-9665-60d21f48021e
source-git-commit: 5192a284c38eb10c214c67a8727de0f7dd4d1ee2
workflow-type: tm+mt
source-wordcount: '4730'
ht-degree: 7%

---

# 轮播横幅{#carousel-banners}

轮播横幅通过轻松创建交互式轮播促销内容并将其交付到任何屏幕，使营销人员能够推动转化。

创建和修改促销横幅中的特色内容可能非常耗时，从而限制您快速发布新内容或使其更具针对性的能力。 轮播横幅允许您快速创建或修改旋转横幅。 您可以添加交互功能（如链接到产品详细信息或相关资源的热点），并将它们交付到任何屏幕，从而更快地向市场推出新的促销内容。

轮播横幅由带有单词的横幅指定 **[!UICONTROL CAROUSELSET]**

![chlimage_1-438](assets/chlimage_1-438.png)

在您的网站上，轮播横幅可以如下所示：

![chlimage_1-439](assets/chlimage_1-439.png)

您可以在此处浏览图像（通过单击数字）。 此外，幻灯片会根据您可以自定义的时间间隔自动旋转。 您在轮播横幅中添加的图像同时支持热点和图像映射，用户可以在其中选择或转到超链接或访问概览窗口。

在此示例中，用户点按或单击了图像映射，并访问了“概览”窗口以获取手套：

![chlimage_1-440](assets/chlimage_1-440.png)

## 观看如何创建轮播横幅 {#watch-how-carousel-banners-are-created}

演练 [如何创建轮播横幅](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)（10分33秒）。 您还将了解如何预览、编辑和投放轮播横幅。

>[!NOTE]
>
>必须将非管理用户添加到 **[!UICONTROL dam-users]** 组才能创建或编辑轮播横幅。 如果您在创建或编辑时遇到问题，请咨询您的系统管理员，以便他们将您添加到 **[!UICONTROL dam-users]** 组。

## 快速入门：轮播横幅 {#quick-start-carousel-banners}

使用轮播横幅快速启动并运行：

1. [识别热点和图像映射变量](#identifying-hotspot-and-image-map-variables) (仅适用于使用Experience Manager Assets + Dynamic Media的客户)

   首先，标识现有“快速视图”实施使用的动态变量，以便您可以在Adobe Experience Manager Assets中的轮播横幅创建过程中正确输入热点和图像映射数据。

   >[!NOTE]
   >
   >如果您是Experience Manager Sites或电子商务客户，则可以使用内置功能导航到产品页面并在产品目录中查找现有SKU（库存单位）。 您无需手动输入热点或图像映射变量。 查看以下信息 [设置电子商务](/help/commerce/cif-classic/administering/generic.md).
   >
   >
   >如果您是Experience Manager Assets和Dynamic Media客户，请手动输入热点和图像映射的数据，然后将发布的URL或嵌入代码与第三方内容管理系统集成。

1. 可选：根据需要[创建轮播集查看器预设](/help/assets/managing-viewer-presets.md)。

   如果您是管理员，则可以通过创建自己的轮盘查看器预设来自定义轮盘的行为和外观。 主要好处是，您可以对多个轮播重用此自定义查看器预设。 但是，用户可以选择在创作轮播时直接自定义轮播的行为和外观。 当您希望为给定的轮播进行特定设计时，此方法是首选方法。

1. [上传图像横幅](#uploading-image-banners).

   上传您要实现交互的图像横幅。

1. [创建轮播集](#creating-carousel-sets).

   在轮播集中，用户浏览横幅图像并选择热点或图像映射以访问相关内容。

   要在Assets中创建轮播集，请选择 **[!UICONTROL 创建]**，然后选择 **[!UICONTROL 轮播集]**. 将资源添加到幻灯片并选择 **[!UICONTROL 保存]**. 您还可以直接在编辑器中编辑轮播集的外观和行为。

1. [将热点或图像映射添加到图像横幅](#adding-hotspots-or-image-maps-to-an-image-banner).

   将一个或多个热点或图像映射添加到图像横幅，并将每个热点或图像映射与链接、概览或体验片段等操作相关联。 添加热点或图像映射后，您可以通过发布轮播集来完成此任务。 发布操作将创建可用于复制并应用于您的网站登陆页面的嵌入代码。

   参见 [（可选）预览轮播横幅](#optional-previewing-carousel-banners)  — 可选。 如果需要，您可以查看轮播集的表示形式并测试其交互性。

1. [发布轮播横幅](#publishing-carousel-banners).

   您可以像发布任何资源一样发布传送集。 在Assets中，导航到轮播集并将其选定，然后选择 **[!UICONTROL Publish]**. 发布轮播集将激活URL和嵌入字符串。

1. 执行下列操作之一：

   * [向您的网站页面添加轮播横幅](#adding-a-carousel-banner-to-your-website-page) 您可以将复制的轮播横幅URL或嵌入代码添加到网站页面。

      * [将轮播横幅与现有概览集成](#integrating-the-carousel-banner-with-an-existing-quickview). 如果您使用第三方Web内容管理系统，则必须将新的轮播横幅与网站上现有的概览实施集成。
   * [在Experience Manager中将轮播横幅添加到您的网站](/help/assets/adding-dynamic-media-assets-to-pages.md) 如果您是Experience Manager Sites客户，则可以使用交互式媒体组件，直接将轮播集添加到Experience Manager中的页面。


要编辑传送集，请参阅 [编辑轮播集](#editing-carousel-sets). 此外，您还可以查看和编辑 [轮播集属性](manage-assets.md#editing-properties).

## 识别热点和图像映射变量 {#identifying-hotspot-and-image-map-variables}

首先，标识现有“快速视图”实施使用的动态变量，以便您可以在Experience Manager Assets中的轮播集创建过程中正确输入热点或图像映射数据。

在Experience Manager Assets中将热点或图像映射添加到横幅图像时，请为每个热点或图像映射分配一个SKU和可选的其他变量。 此类变量稍后用于匹配热点或图像映射与概览内容。

>[!NOTE]
>
>如果您是Experience Manager Sites和/或Experience Manager电子商务客户，请跳过此步骤。 您无需手动标识热点或图像映射变量；您可以将与电子商务的集成用于产品集成。 查看以下信息 [设置电子商务](/help/commerce/cif-classic/administering/generic.md). 此外，您还可以使用交互式组件并将其添加到网页。
>
>如果您是Experience Manager Assets或媒体客户，请发布URL或嵌入代码，然后与第三方内容管理系统集成，并手动识别热点和图像映射。

正确标识要与热点或图像映射数据关联的变量的数量和类型非常重要。 添加到横幅图像的每个热点或图像映射都必须包含足够的信息，才能明确识别现有后端系统中的产品。 同时，每个热点或图像映射所包含的数据不能超过所需数量。 这是因为这会使数据录入过程过于复杂，并且不断的热点或图像映射管理更加容易出错。

有多种不同的方法可标识一组用于热点或图像映射数据的变量。

有时，咨询负责现有Quickview实施的IT专家就足够了。 他们可能会知道在系统中标识概览所需的最小数据集。 但是，通常也可以简单地分析前端代码的现有行为。

大多数概览实施都使用以下范例：

* 用户在网站上激活用户界面元素。例如，点按 **[!UICONTROL 概览]** 按钮。
* 如果需要，网站会向后端发送Ajax请求以加载概览数据或内容。
* 概览数据将转换为内容，以便在网页上呈现。
* 最后，前端代码以可视形式将这些内容呈现在屏幕上。

然后，方法是访问实施概览功能的现有网站的不同区域。 触发概观，并捕获网页发送的Ajax URL，以加载概观数据或内容。

通常情况下，您不需要使用任何专业的调试工具。现代的 Web 浏览器具备 Web 检查器，可以实现相同的功能。下面列举了一些具备 Web 检查器的 Web 浏览器：

* 要在Google Chrome中查看所有传出的HTTP请求，请按F12 (Windows)或Command-Option-I (Mac)打开“开发人员工具”面板，然后选择“网络”选项卡。
* 在Firefox中，您可以通过按F12 (Windows)或Command-Option-I (Mac)并使用其“网络”选项卡来激活Firebug插件，也可以使用内置的检查器工具及其“网络”选项卡。

在浏览器中打开网络监视功能时，会在页面上触发概览。

现在，请在网络日志中找到Quickview Ajax URL，并复制记录的URL以供将来分析。 通常，在触发概览时，会向服务器发送大量请求。 通常，快速视图Ajax URL是列表中的前几个之一。 它具有复杂的查询字符串部分或路径，并且其响应MIME类型为 `text/html`， `text/xml`，或 `text/javascript`.

在此过程中，请务必访问网站的不同区域，以及不同的产品类别和类型。 原因是概观URL具有给定网站类别共有的部分，但只有在访问网站的其他区域时才更改。

最简单的情况是，概览URL中的唯一变量部分是产品SKU。 在这种情况下，将“热点”或“图像映射”添加到横幅图像时，SKU值是唯一需要的数据块。

但是，在复杂的情况下，除了SKU之外，概览URL还有不同的变化元素，例如类别ID、颜色代码和大小代码。 在这种情况下，每个元素在热点或轮播横幅功能中的图像映射数据定义中都是单独的变量。

请考虑以下概观URL示例及其生成的热点或图像映射变量：

<table>
 <tbody>
  <tr>
   <td>单个 SKU，位于查询字符串中。</td>
   <td><p>记录的概览URL包括：</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>URL中的唯一变量部分是 <code>productId=</code> 查询字符串参数，它显然是一个SKU值。 因此，热点或图像映射只需要使用如下值填充的SKU字段 <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>单个 SKU，位于 URL 路径中。</td>
   <td><p>记录的概览URL包括：</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>变量部分位于路径的最后一部分，它成为热点/图像映射的SKU值：<strong><code>6422350843</code>， <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU 和类别 ID，位于查询字符串中。</td>
   <td><p>记录的概览URL包括：</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>在这种情况下，URL 中有两个可变部分。SKU存储在 <code>prodId</code> 参数和类别ID存储在 <code>category=</code>参数。</p> <p>因此，热点/图像映射定义是对。 即，一个SKU值和一个名为的额外变量 <code>categoryId</code>. 生成的各对如下所示：</p>
    <ul>
     <li><p>SKU是 <strong><code>305466</code></strong> 和 <code>categoryId</code> 是 <code>1100004</code>.</p> </li>
     <li><p>SKU是 <strong><code>310181</code></strong> 和 <code>categoryId</code> 是 <strong><code>1100004</code></strong>.</p> </li>
     <li><p>SKU是 <strong><code>308706</code></strong> 和 <code>categoryId</code> 是 <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 上传图像横幅 {#uploading-image-banners}

如果您已上传要使用的图像，请前进到下一步， [创建轮播集](#creating-carousel-sets). 请注意，在启用Dynamic Media后，必须上传轮播中使用的图像。

要上传图像横幅，请参阅 [上传资产](/help/assets/manage-assets.md).

## 创建轮播集 {#creating-carousel-sets}

>[!NOTE]
>
>必须将非管理用户添加到 **[!UICONTROL dam-users]** 组才能创建或编辑轮播横幅。 如果您在创建或编辑时遇到问题，请咨询您的系统管理员，以便他们将您添加到 **[!UICONTROL dam-users]** 组。

**要创建传送集，请执行以下操作：**

1. 在Assets中，导航到要创建轮播集的文件夹，然后转到 **[!UICONTROL 创建]** > **[!UICONTROL 轮播集]**.
1. 在轮播横幅编辑器页面上，选择 **[!UICONTROL 点按以打开资产选择器]** 以选择第一张幻灯片的图像。

   在轮播横幅编辑器页面上，执行以下任一操作：

   * 在页面的左上角附近，选择 **[!UICONTROL 添加幻灯片]** 图标。

   * 在页面中间附近，选择 **[!UICONTROL 点按以打开资产选择器]**.
   选择以选择要包含在轮播集中的资源。 选定资产上有一个复选标记图标。完成后，在页面的右上角附近，选择 **[!UICONTROL 选择]**.

   借助资产选择器，您可以通过键入关键字并点按或单击&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后选择 **[!UICONTROL 筛选条件]** 图标。 点按“视图”图标并选择&#x200B;**[!UICONTROL 列视图]**、**[!UICONTROL 卡片视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;可更改视图。

   参见 [使用选择器](/help/assets/working-with-selectors.md) 了解更多信息。

1. 继续添加幻灯片，直到在轮播集中添加了所有要旋转的图像为止。
1. （可选）执行以下操作之一：

   * 如有必要，请拖动幻灯片以重新排序集合列表中的图像。
   * 要删除图像，请选择该图像，然后选择 **[!UICONTROL 删除幻灯片]** 工具栏上。

   * 要应用预设，请在页面右上角附近选择预设下拉列表，然后选择要应用于设置的预设。
   要删除幻灯片，请选择幻灯片，然后在工具栏上选择 **[!UICONTROL 删除幻灯片]**. 要移动幻灯片，请选择重新排序图标，然后按住并移动到所需位置。

1. 在幻灯片中添加图像后，您可以向图像添加热点、图像映射，或同时添加这两者。 参见 [将热点或图像映射添加到图像横幅](#adding-hotspots-or-image-maps-to-an-image-banner).
1. 您可以更改轮播集的视觉设计和行为。 选择 **[!UICONTROL 行为]** 和 **[!UICONTROL 外观]** 选项卡并调整轮播横幅的显示方式或特定组件的行为。 参见 [管理查看器预设](/help/assets/viewer-presets.md) 有关如何使用查看器编辑器的更多信息。

   >[!NOTE]
   >
   >对于轮播横幅，您可以调整以下内容：
   >
   >    * 图像显示的持续时间。 默认情况下，每个图像会显示9秒。
   >    * 动画. 默认情况下，每个幻灯片过渡都是淡入淡出。 您可以将其更改为幻灯片过渡。
   >    * 按钮的样式。 用户可以通过点按每个点或数字来旋转横幅。 您可以更改设置指示器按钮的显示位置（如果是数字或点状样式，则更改其大小）。
   >    * 更改图像映射的高亮样式或用于热点的图标。
   >    * 在编辑查看器预设之前，请选择要使预设基于的样式。 如果未选择样式，则在开始编辑查看器预设时，如果决定更改为其他预设，则会丢失所有更改。

   >
   >参见 [轮播横幅的特殊注意事项](/help/assets/managing-viewer-presets.md#special-considerations-for-creating-a-carousel-banner-viewer-preset) 有关查看器编辑器的详细说明和详细信息。

   您还可以预览轮播横幅的显示方式。 参见 [（可选）预览轮播横幅](#optional-previewing-carousel-banners).

1. 选择 **[!UICONTROL 保存]** 完成后。

## 将热点或图像映射添加到图像横幅 {#adding-hotspots-or-image-maps-to-an-image-banner}

您可以使用轮播集编辑器将热点或图像映射添加到横幅中。

添加热点或图像映射时，可以将它们定义为概览弹出显示、超链接或体验片段。

参见 [体验片段](/help/sites-authoring/experience-fragments.md).

>[!NOTE]
>
>将查看器嵌入体验片段时，不支持轮播横幅中的社交媒体共享工具。
>
>要解决此问题，您可以使用或创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功地将其嵌入体验片段中。

在向图像添加热点或图像映射时，请记住保存所做的工作。 在当前创建/编辑会话期间，支持页面右上角附近的“撤消”和“重做”选项。

创建完轮播横幅后，您可以选择使用“预览”来查看向客户显示的轮播横幅的显示方式。

参见 [（可选）预览轮播横幅](#optional-previewing-carousel-banners).

>[!NOTE]
>
>将热点添加到中的图像时 [交互式图像](/help/assets/interactive-images.md) 对于轮播横幅，热点信息存储在相同的元数据位置。 该位置相对于图像的位置，无论图像是交互式图像还是轮播横幅。 这项功能意味着您可以轻松地在任一查看器中重用相同的图像及其定义的热点数据。
但是，请注意，轮播横幅支持图像映射，这些图像也可能包含热点；而交互式图像则不支持。 如果您打算创建使用同一图像的交互式图像或轮播横幅，请记住此规则。 请考虑改用同一图像的单独副本来创建交互式图像和轮播横幅。

>[!NOTE]
如果您正在编辑具有热点的交互式图像并裁切图像，则您的热点会被删除。

另请参阅 [添加图像映射](/help/assets/image-maps.md).

**要将热点或图像映射添加到图像横幅，请执行以下操作：**

1. 在Assets中，导航到要使其成为交互式内容的轮播集。
1. 选择轮播集并选择 **[!UICONTROL 编辑]**. 此时将打开“轮盘查看器编辑器”。
1. 选择要使其成为交互式幻灯片。
1. 在页面的左上角附近，选择 **[!UICONTROL 热点]** 或 **[!UICONTROL 图像映射]**.
1. 执行以下任一操作：

   * 对于热点：在图像上，选择要显示热点的位置。
   * 对于图像映射：在图像上，选择，然后从左上角拖动到右下角，以创建图像映射区域。 您可以通过拖动角来调整图像映射的大小。

   如有必要，请将热点或图像映射拖动到新位置。 根据需要添加其他热点或图像映射。

   要删除热点或图像映射，请选择 **[!UICONTROL 操作]** 选项卡。 在&#x200B;**[!UICONTROL 映射和热点]**&#x200B;标题下，从&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉菜单中，选择要删除的热点或图像映射的名称。选择 **[!UICONTROL 垃圾桶]** 图标，然后选择 **[!UICONTROL 删除]**.

1. 在“名称”文本字段中，键入热点或图像映射的名称。 此名称也会出现在 **[!UICONTROL 映射和热点]** 下拉列表。 提供名称可让您在决定将来更改热点或图像映射时轻松识别它。
1. 在中执行以下操作之一 **[!UICONTROL 操作]** 选项卡：

   * 选择 **[!UICONTROL 概览]**.

      * 如果您是Experience Manager Sites和电子商务客户，请选择产品选取器图标（放大镜）以打开“选择产品”页面。 选择要使用的产品，然后选择页面右上角的复选标记，以便您可以返回到轮盘横幅编辑器。
      * 如果您不是Experience Manager Sites或电子商务客户

         * 参见 [识别热点变量](#identifying-hotspot-and-image-map-variables) （如果要定义这些变量）。
         * 然后，手动输入SKU值。 在“SKU值”文本字段中，键入产品的SKU（库存单位），它是您提供的每个不同产品或服务的唯一标识符。 输入的SKU值会自动填充概览模板的变量部分，以便系统知道将点按的热点与特定SKU的概览相关联。
         * （可选）如果概览中还有其他必须用来进一步标识产品的变量，请选择 **[!UICONTROL 添加通用变量]**. 在文本字段中，指定一个额外的变量。 例如， category=Mens是一个添加的变量。

         * 参见 [使用选择器](/help/assets/working-with-selectors.md) 了解更多信息。
   * 选择 **[!UICONTROL 超链接]**.

      * 如果您是Experience Manager Sites客户，请选择站点选择器图标（文件夹）以导航到某个URL。
         >[!NOTE]
         如果您的交互式内容具有带相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL的链接方法。

      * 如果您是独立客户，请在HREF文本字段中指定链接网页的完整URL路径。

   请确保指定是在新的浏览器选项卡（推荐的默认值）中还是同一选项卡中打开链接。

   参见 [使用选择器](/help/assets/working-with-selectors.md) 了解更多信息。

   * 选择 **[!UICONTROL 体验片段]**.

      * 如果您是Experience Manager Sites客户，请选择“搜索”图标（放大镜）以打开“体验片段”页面。 选择要使用的体验片段，然后选择 **[!UICONTROL 选择]** ，以便可以返回热点管理页面。
参见 [体验片段](/help/sites-authoring/experience-fragments.md).

      * 指定体验片段在横幅上显示的宽度和高度。

         >[!NOTE]
         将查看器嵌入体验片段时，不支持轮播横幅中的社交媒体共享工具。
         要解决此问题，请创建没有社交媒体共享工具的查看器预设。 通过此类查看器预设，您可以成功地将其嵌入体验片段中。
   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   您还可以预览轮播横幅的显示方式。 参见 [（可选）预览轮播横幅](#optional-previewing-carousel-banners).

1. 选择&#x200B;**[!UICONTROL 保存]**。
1. 发布轮播集。 发布会创建可在网站页面上使用的嵌入代码或URL。 如果您是Experience Manager Sites客户，则可以直接将轮播集添加到网页。

   请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

   参见 [向网站登陆页面添加轮播集](#adding-a-carousel-banner-to-your-website-page)

## 编辑轮播集 {#editing-carousel-sets}

>[!NOTE]
必须将非管理用户添加到 **[!UICONTROL dam-users]** 组才能创建或编辑轮播横幅。 如果您在创建或编辑时遇到问题，请咨询您的系统管理员，以便他们将您添加到 **[!UICONTROL dam-users]** 组。

您可以对轮播集执行各种编辑任务，如下所示：

* 将幻灯片添加到轮播集。 另请参阅 [使用选择器](/help/assets/working-with-selectors.md).
* 重新排序轮播集中的幻灯片。
* 删除轮播集中的资源。
* 应用查看器预设。
* 删除轮播集。
* 添加或编辑热点和图像映射。 另请参阅 [使用选择器](/help/assets/working-with-selectors.md).

**要编辑传送集，请执行以下操作：**

1. 执行以下任一操作：

   * 将鼠标悬停在轮播集资源上，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。
   * 将鼠标悬停在轮播集资源上，选择 **[!UICONTROL 选择]** （复选标记图标），然后选择 **[!UICONTROL 编辑]** 工具栏上。

   * 选择一个轮播集资源，然后在页面的左上角选择 **[!UICONTROL 编辑]** （铅笔图标）。

1. 要编辑轮播集，请执行以下任一操作：

   * 要添加幻灯片，请选择 **[!UICONTROL 添加幻灯片]** 图标，然后导航到要添加到该幻灯片的资源并选中复选标记。
   * 要重新排序幻灯片，请将幻灯片拖到新位置（选择重新排序图标以移动项目）。
   * 要添加热点或图像映射，请选择热点或图像映射图标并参见 [添加热点和图像映射](#adding-hotspots-or-image-maps-to-an-image-banner).
   * 要编辑轮播集的外观或行为，请选择 **[!UICONTROL 外观]** 选项卡或 **[!UICONTROL 行为]** 选项卡，然后设置所需的选项。
   * 要编辑热点或图像映射，请在相应的幻灯片上选择一个热点或图像映射，然后根据需要在 **[!UICONTROL 操作]** 选项卡。
   * 要删除幻灯片，请选择它，然后选择 **[!UICONTROL 删除幻灯片]** 工具栏上。
   * 要应用预设，请在页面的右上角附近，选择 **[!UICONTROL 预设]** 下拉列表，然后选择查看器预设。
   * 要删除整个轮播集，请导航到轮播集，选择它，然后选择 **[!UICONTROL 删除]**.

   >[!NOTE]
   如果您正在编辑具有热点的交互式图像并裁切图像，则您的热点会被删除。

## （可选）预览轮播横幅 {#optional-previewing-carousel-banners}

您可以使用“预览”来查看轮播横幅向客户显示的方式，并测试轮播横幅热点和图像映射，以确保它们按预期运行。

如果您对轮播横幅满意，则可以发布它。
请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。请参阅[将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)。如果您的交互式内容具有带相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则无法基于URL的链接方法。
参见 [将Dynamic Media资源添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md).

您可以从轮播编辑器（首选方法）预览轮播横幅，也可以从 **[!UICONTROL 查看器]** 列表。

**要预览轮播横幅，请执行以下操作：**

1. In **[!UICONTROL 资产]**，导航到您创建的现有轮播横幅，然后选择以将其打开。
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 在工具栏右上角的查看器预设列表中，选择一个查看器以预览轮播横幅。

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. 选择&#x200B;**[!UICONTROL 预览]**。
1. 选择图像上的热点或图像映射，以便测试其关联的操作。

**要从查看器列表中预览轮播横幅，请执行以下操作：**

1. In **[!UICONTROL 资产]**，导航到您创建的现有轮播横幅，然后选择以将其打开。
1. 在“预览”页面的左上角附近，选择“内容”图标。
1. 在 **[!UICONTROL 查看器]** 在页面左侧的面板中，选择要使用的轮播横幅查看器预设的名称。
1. 选择图像上的热点或图像映射，以便测试其关联的操作。

## 发布轮播横幅 {#publishing-carousel-banners}

发布轮播以便您可以使用。 发布轮播集将激活URL和嵌入代码。 它还将轮播发布到与CDN集成的Dynamic Media云，以进行可扩展和性能良好的交付。

>[!NOTE]
如果为轮播横幅使用带热点的现有交互式图像，则必须在发布轮播横幅后单独发布交互式图像。
此外，如果您修改了转盘横幅中正在使用的预先存在的已发布交互式图像，则必须先发布该交互式图像，然后这些更改才会反映在转盘横幅中。

参见 [发布Dynamic Media资源](/help/assets/publishing-dynamicmedia-assets.md) 了解有关如何发布轮播横幅的信息。

## 向您的网站页面添加轮播横幅 {#adding-a-carousel-banner-to-your-website-page}

在上传横幅图像以创建轮播、将热点和/或图像映射添加到横幅并发布轮播集后，您现在可以将其添加到现有网站页面。

>[!NOTE]
如果您是Experience Manager Sites客户，则可以通过将交互式媒体组件拖动到页面来将轮播横幅直接添加到页面。 参见 [将Dynamic Media资源添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md).

但是，如果您是独立的Experience Managerassets客户，则可以手动将轮播横幅添加到网站登陆页面，如本节所述。

1. 复制已发布的轮播集的嵌入代码。
参见 [将视频或图像查看器嵌入网页](/help/assets/embed-code.md).

1. 将您从Experience Manager Assets复制的嵌入代码添加到您的网页。
复制的嵌入代码是响应式的，因此它必须自动适合页面的嵌入区域。

## 将轮播横幅与现有概览集成 {#integrating-the-carousel-banner-with-an-existing-quickview}

>[!NOTE]
此步骤仅适用于Experience Manager Assets独立客户。

此流程的最后一步是将轮播横幅与网站上现有的概览实施集成。 每个概览实施都是独一无二的，需要涉及前端IT人员帮助的特定方法。

现有的概览实施通常表示在网页上发生的一系列相互关联的操作，顺序如下：

1. 用户在网站的用户界面上触发一个元素。
1. 前端代码基于在步骤1中触发的用户界面元素获取概览URL。
1. 前端代码使用在第 2 步获取的 URL 发送一个 Ajax 请求。
1. 后端逻辑将相应的概览数据或内容返回到前端代码。
1. 前端代码加载概览数据或内容。
1. 前端代码可以选择将加载的概览数据转换为HTML表示形式。
1. 前端代码显示一个模态对话框或面板，并将 HTML 内容呈现在屏幕上以供最终用户查看。

这些调用不表示独立的公共API调用，网页逻辑可以从任意步骤调用这些API调用。 相反，这些调用属于链式调用，即，每个后续步骤都隐藏在前一步的最后阶段（回调）。

在轮播横幅替换步骤1和部分步骤2的同时，当用户点按轮播横幅内的热点或图像映射时，此类交互由查看器处理。 查看器会向包含之前添加的所有热点或图像映射数据的网页返回一个事件。

在此类事件处理程序中，前端代码会执行下列操作：

* 侦听轮播横幅发出的事件。
* 根据热点或图像映射数据构建概览URL。
* 触发从后端加载概览并在屏幕上呈现以进行显示的过程。

Experience Manager Assets返回的嵌入代码已具有现成的事件处理程序，该处理程序已被注释掉。

因此，只需取消对该代码的注释，并用针对特定网页的代码来替换虚拟处理程序主体即可。

构建概观URL的过程与用于标识先前覆盖的热点和图像映射变量的过程相反。

参见 [识别热点和图像映射变量](#identifying-hotspot-and-image-map-variables).

触发概观URL和激活概览面板的最后一步很可能需要您IT部门的前端IT人员的协助。 他们最清楚如何从适当的步骤准确触发概览实施，拥有一个现成的概观URL。

## 使用 Quickview 创建自定义弹出窗口 {#using-quickviews-to-create-custom-pop-ups}

参见 [使用Quickview创建自定义弹出窗口](/help/assets/custom-pop-ups.md).
