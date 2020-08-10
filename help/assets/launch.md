---
title: 将 Dynamic Media 查看器与 Adobe Analytics 和 Adobe Launch 集成
description: 用于 Adobe Launch 的 Dynamic Media 查看器扩展以及 Dynamic Media 查看器 5.13 版允许 Dynamic Media 客户、Adobe Analytics 客户和 Adobe Launch 客户在其 Adobe Launch 配置中使用特定于 Dynamic Media 查看器的事件和数据。
uuid: d218ee1c-cd2c-40c3-a3d4-b95719ae8e98
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: f4051767-182e-4cfd-9dfc-8f516378e0b6
docset: aem65
translation-type: tm+mt
source-git-commit: 8bdb019855edd08ef3d8ef58e627c91a092bc29f
workflow-type: tm+mt
source-wordcount: '6623'
ht-degree: 17%

---


# 将 Dynamic Media 查看器与 Adobe Analytics 和 Adobe Launch 集成 {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## 什么是Dynamic Media Viewers与Adobe Analytics和AdobeLaunch集成？ {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

The new *Dynamic Media Viewers* extension for Adobe Launch, along with the recent release of Dynamic Media Viewers 5.13, lets customers of Dynamic Media, Adobe Analytics, and Adobe Launch to use events and data specific for the Dynamic Media Viewers in their Adobe Launch configuration.

此集成意味着您可以跟踪Dynamic Media查看器在您与Adobe Analytics的网站上的使用情况。 同时，您可以将查看者公开的事件和数据与来自Adobe或第三方的任何其他启动扩展一起使用。

请参 [阅《Adobe](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/overview.html) 用户指南》中的“Experience Platform Launch扩展”，以了解有关扩展的更多信息。

**谁应阅读此文档：** AEM 平台及操作中的站点管理员、开发人员。

### 集成限制 {#limitations-of-the-integration}

* Adobe启动与Dynamic Media查看器的集成在AEM作者节点中不起作用。 在WCM页面发布之前，您无法看到任何跟踪。
* “弹出”操作模式不支持Adobe启动Dynamic Media查看器的集成，在该模式下，查看器URL是使用“资产详细信息”页面上的“URL”按钮获取的。
* Adobe启动集成不能与传统查看器分析集成（通过参数）同时 `config2=` 使用。
* 视频跟踪支持仅限于核心回放跟踪，如跟踪概述 [中所述](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html)。 特别是，不支持QoS、广告、章节／段或错误跟踪。
* 使用Dynamic Media Viewer扩展的存储元素不支持元素的 *持续时间* 配置。 存储持续时间必须设置为 **[!UICONTROL 无]**。

### 集成用例 {#use-cases-for-the-integration}

与AdobeLaunch集成的主要用例是同时使用AEM Assets和AEM Sites的客户。 在这种情况下，您可以在AEM作者节点和Adobe启动之间设置标准集成，然后将您的站点实例与Adobe启动属性相关联。 之后，添加到“站点”页面的任何Dynamic Media WCM组件都将跟踪查看者的数据和事件。

请参 [阅关于跟踪AEM Sites的Dynamic Media查看器](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersinAEMSites)。

集成支持的次要用例是那些仅使用AEM Assets或Dynamic Media Classic的客户。 在这种情况下，您将获得查看器的嵌入代码并将其添加到网站页面。 然后，从Adobe启动中获取Adobe启动库生产URL，然后手动将其添加到网页代码。

请参 [阅关于使用嵌入代码跟踪Dynamic Media查看器](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode)。

## 数据和事件跟踪如何在集成中工作 {#how-data-and-event-tracking-works-in-the-integration}

该集成利用两种独立类型的Dynamic Media查看器跟踪： *Adobe Analytics* 和 *Adobe Analytics音频和视频部*。

### 关于使用Adobe Analytics跟踪  {#about-tracking-using-adobe-analytics}

Adobe Analytics允许您跟踪最终用户在您网站上与Dynamic Media查看器交互时执行的操作。 Adobe Analytics还允许您跟踪特定于查看器的数据。 例如，您可以跟踪和记录视图加载事件以及资产名称、发生的任何缩放操作、视频播放操作等。

在Adobe启动中，数据元 *素和规则**的概念协同工* 作，实现Adobe Analytics跟踪。

#### 关于Adobe启动中的数据元素 {#about-data-elements-in-adobe-launch}

Adobe启动中的数据元素是已命名的属性，其值是静态定义的，或根据网页或Dynamic Media查看器数据的状态动态计算的。

可用于数据元素定义的选项取决于Adobe启动属性中安装的扩展的列表。 “核心”扩展已预装，可在任何配置中开箱即用。 此“核心”扩展允许定义一个数据元素，该数据元素的值来自cookie、JavaScript代码、查询字符串和许多其他源。

Adobe Analytics跟踪需要安装多个附加扩展，如安装和 [设置扩展中所述](#installing-and-setup-of-extensions)。 Dynamic Media Viewers扩展添加了定义数据元素的功能，该数据元素值是Dynamic Viewer事件的参数。 例如，可以引用查看器类型或查看器在加载时报告的资产名称、最终用户缩放时报告的缩放级别等。

Dynamic Media Viewer扩展可自动使其数据元素的值保持最新。

定义数据元素后，可以使用Adobe元素选取器构件在数据启动UI的其他位置使用数据元素。 尤其是，为了Dynamic Media查看器跟踪而定义的数据元素将由规则中Adobe Analytics扩展的设置变量操作引用（请参阅下文）。

请参 [阅《Experience Platform Launch](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/manage-resources/data-elements.html) 用户指南》中的数据元素了解更多信息。

#### 关于Adobe启动中的规则 {#about-rules-in-adobe-launch}

Adobe启动中的规则是一种不可知配置，它定义构成规则的三个区域： *事件*、 *条件*&#x200B;和 *操作*:

* *事件* （如果）告诉Adobe启动何时触发规则。
* *条件* （如果）告知Adobe启动在触发规则时允许或禁止的附加限制。
* *操作* （然后）告诉Adobe启动在触发规则时要执行的操作。

“事件”、“条件”和“操作”部分提供的选项取决于Adobe启动属性中安装的扩展。 已 *预装* “核心扩展”，并可在任何配置中开箱即用。 该扩展为事件提供了多个选项，如基本的浏览器级操作，包括焦点更改、按键、表单提交等。 它还包含Conditions选项，如cookie值、浏览器类型等。 对于“操作”，仅“自定义代码”选项可用。

要进行Adobe Analytics跟踪，必须安装多个附加扩展，如安装和 [设置扩展中所述](#installing-and-setup-of-extensions)。 具体而言：

* Dynamic Media Viewers扩展将受支持事件的列表扩展到特定于Dynamic Media查看器的事件，如查看器加载、资产交换、放大和视频播放。
* Adobe Analytics扩展通过向跟踪服务器发送数据所需的两个操作扩展了受支持操作的列表: *设置变量* 和 *发送信标*。

要跟踪Dynamic Media查看器，可以使用以下任何类型：

* 来自Dynamic Media Viewers扩展、核心扩展或任何其他扩展的事件。
* 规则定义中的条件。 或者，可以将条件区域留空。

在“操作”部分，需要执行“设置变 *量”操作* 。 此操作告诉Adobe Analytics如何用数据填充跟踪变量。 同时，“设置变 *量* ”动作不会向跟踪服务器发送任何内容。

“设 *置变量* ”动作后面必须有“发送 *信标”动作* 。 “发 *送信标* ”操作实际会向分析跟踪服务器发送数据。 “设置变 *量* ”和“ *发送信标*”操作均来自Adobe Analytics扩展。

请参 [阅《Experience Platform Launch](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/manage-resources/rules.html) 用户指南》中的规则，了解更多信息。

#### 示例配置 {#sample-configuration}

Adobe启动中的以下示例配置演示了如何在加载查看器时跟踪资产名称。

1. 在“数 **[!UICONTROL 据元素]** ”选项卡中，定义一个从Dynamic `AssetName` Media Viewers扩展中引 `asset` 用事件 `LOAD` 参数的数据元素。

   ![image2019-11](assets/image2019-11.png)

1. 在“规 **[!UICONTROL 则]** ”选项卡中，定义 *规则TrackAssetOnLoad*。

   在此规则中， **[!UICONTROL 事件]** 字段使 **[!UICONTROL 用]** Dynamic Media Viewer扩展中的LOAD事件。

   ![image2019-22](assets/image2019-22.png)

1. “操作”配置有来自Adobe Analytics扩展的两种“操作”类型：

   *设置变量*，将您选择的分析变量映射到数据元素 `AssetName` 的值。

   *发送信标*，将跟踪信息发送给Adobe Analytics。

   ![image2019-3](assets/image2019-3.png)

1. 生成的规则配置如下所示：

   ![image2019-4](assets/image2019-4.png)

### 关于Adobe Analytics音频和视频 {#about-adobe-analytics-for-audio-and-video}

订阅Experience Cloud帐户以使用Adobe Analytics音频和视频时，就足以在Dynamic Media查看器扩展设置中启 *用视频* 跟踪。 视频指标在Adobe Analytics可用。 视频跟踪取决于是否存在用于音频和视频扩展的Adobe媒体分析。

请参 [阅扩展的安装和设置](#installing-and-setup-of-extensions)。

目前，对视频跟踪的支持仅限于“核心播放”跟踪，如跟踪概述中 [所述](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html)。 特别是，不支持QoS、广告、章节／段或错误跟踪。

## 使用Dynamic Media Viewers扩展 {#using-the-dynamic-media-viewers-extension}

如集成 [的使用案例中所述](#use%20cases%20for%20the%20integration)，可以通过AEM Sites的新Adobe启动集成和使用嵌入代码跟踪Dynamic Media查看器。

### 跟踪AEM Sites的Dynamic Media查看器 {#tracking-dynamic-media-viewers-in-aem-sites}

要跟踪AEM Sites的Dynamic Media查看器，必须执行配置所 [有集成部分下列出的所](#configuring-all-the-integration-pieces) 有步骤。 具体而言，您必须创建IMS配置和Adobe启动云配置。

在进行正确配置后，您使用Dynamic Media支持的WCM组件将添加到“站点”页面的任何Dynamic Media查看器自动跟踪到Adobe Analytics或Adobe Analytics的视频数据，或同时跟踪到这两个数据。

<!-- To be reviewed and updated:
See [Adding Dynamic Media Assets to Pages using Adobe Sites](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html).
-->

### 使用嵌入代码跟踪Dynamic Media查看器 {#tracking-dynamic-media-viewers-using-embed-code}

未使用AEM Sites或将Dynamic Media查看器嵌入AEM Sites以外网页或两者的客户仍可使用AdobeLaunch集成。

您必须完成[配置 Adobe Analytics](#configuringadobeanalytics) 和[配置 Adobe Launch](#configuringadobelaunch) 部分中的配置步骤。但是，不需要执行与 AEM 相关的配置步骤。

在进行正确配置后，您可以使用Dynamic Media查看器向网页添加Adobe启动支持。

请参 [阅添加启动项嵌入代码](https://docs.adobe.com/content/help/en/launch/using/implement/configure/implement-the-launch-install-code.html) ，进一步了解如何使用Adobe启动库嵌入代码。

<!-- To be reviewed and updated:
See [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) to learn more about how to use the embed code feature of AEM Dynamic Media.
-->

**要使用嵌入代码跟踪Dynamic Media查看器**:

1. 为嵌入Dynamic Media查看器准备网页。
1. 首先登录Adobe启动，获取Adobe启动库的嵌入代码(请参 [阅配置Adobe启动](#configuringadobelaunch))。
1. 单击 **[!UICONTROL 属性]**，然后单击 **[!UICONTROL 环境]** 选项卡。
1. 提取与网页环境相关的环境级别。 然后，在“安 **[!UICONTROL 装]** ”列中，单击框图标。
1. **[!UICONTROL 在“Web安装说明]** ”对话框中，复制完整的Adobe启动库嵌入代码以及周围的 `<script/>` 标记。

## Dynamic Media查看器扩展的参考指南 {#reference-guide-for-the-dynamic-media-viewers-extension}

### 关于Dynamic Media查看器配置 {#about-the-dynamic-media-viewers-configuration}

如果满足以下所有条件，Dynamic Media Viewer扩展将自动与Adobe启动库集成：

* Adobe启动库全 `_satellite`局对象()在页面上。
* Dynamic Media Viewers扩展功能 `_dmviewers_v001()` 在上定 `_satellite`义。

* `config2=` 未指定查看器参数，这意味着查看器不使用传统Analytics集成。

此外，还有一个选项，可通过在查看器的配置中指定参数，在查看器 `launch=0` 中显式禁用Adobe启动集成。 此参数的默认值为 `1`。

### 配置Dynamic Media Viewer扩展 {#configuring-the-dynamic-media-viewers-extension}

Dynamic Media Viewers扩展的唯一配置选项是为音 **[!UICONTROL 频和视频启用Adobe媒体分析]**。

当您选中（启用或“开启”）此选项，并且如果安装并正确配置了Adobe媒体分析音频和视频扩展，则视频回放指标将发送到Adobe Analytics音频和视频解决方案。 禁用此选项将关闭视频跟踪。

请注意，如果启用此选 *项时* ，未安装Adobe媒体分析的音频和视频扩展，则此选项无效。

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### 关于Dynamic Media Viewers扩展中的数据元素 {#about-data-elements-in-the-dynamic-media-viewers-extension}

Dynamic Media Viewers 扩展提供的唯一数据元素类型是&#x200B;**[!UICONTROL 数据元素类型]**&#x200B;下拉列表中的&#x200B;**[!UICONTROL 查看器事件]**。

选中后，数据元素编辑器将呈现一个包含两个字段的表单：

* **[!UICONTROL DM 查看器事件数据类型]** - 一个下拉列表，标识了 Dynamic Media 查看器扩展支持的所有查看器事件（具有参数）以及特殊的 **[!UICONTROL COMMON]** 项目。**[!UICONTROL COMMON]** 项目表示事件参数列表，这些事件参数对查看器发送的所有类型事件都是通用的。
* **[!UICONTROL 跟踪参数]** -选定Dynamic Media查看器事件的参数。

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

有关按每 [种查看器类型列表受支持事件的信息](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html) ，请参阅Dynamic Media查看器参考指南；转到特定查看器部分，然后单击“支持Adobe Analytics跟踪”子部分。 目前，Dynamic Media查看器参考指南不文档事件参数。

现在，我们来考虑Dynamic Media查看器数据元素的 *生命周期*。 在页面上发生相应的Dynamic Media查看器事件后，将填充此类数据元素的值。 例如，如果数据元素指向 **[!UICONTROL LOAD]** 事件及其“asset”参数，则此类数据元素的值将在查看器首次运行LOAD事件后接收有效数据。 如果数据元素指向 **[!UICONTROL ZOOM]** 事件及其“scale”参数，则此类数据元素的值将保持为空，直到查看器首次发送 **[!UICONTROL ZOOM]** 事件。

同样，当查看器在页面上发送相应事件时，数据元素的值也会自动更新。即使在规则配置中未指定特定事件，也会发生值更新。例如，如果为 ZOOM 事件的“scale”参数定义了数据元素 **[!UICONTROL ZoomScale]**，但“规则”配置中唯一存在的规则由 **[!UICONTROL LOAD]** 事件触发，则每当用户在查看器中运行缩放时，**[!UICONTROL ZoomScale]** 的值仍会更新。

任何Dynamic media查看器在网页上都有唯一标识符。 数据元素会跟踪值本身以及已填充该值的查看器。 这意味着，如果同一页面上有多个查看器，并且有一个指向 **[!UICONTROL LOAD]** 事件及其“asset”参数的 **[!UICONTROL AssetName]** Data Element，则 **[!UICONTROL AssetName]** Data Element将保留与页面上加载的每个查看器关联的资产名称集合。

数据元素返回的确切值取决于上下文。 如果在由Dynamic Media查看器事件触发的规则中请求数据元素，则为启动该规则的查看器返回数据元素值。 而且，如果在由事件从某些其他Adobe启动扩展触发的规则中请求数据元素，则数据元素的值是查看器中最后一个更新此数据元素的值。

**请考虑以下示例设置**:

* 具有两个Dynamic Media缩放查看器的网页；我们将它们称为 *viewer1* 和 *viewer2*。

* **[!UICONTROL ZoomScale]** Data Element指向 **[!UICONTROL ZOOM]** 事件及其“scale”参数。
* **[!UICONTROL TrackPan]** 规则，包含以下项：

   * 使用Dynamic Media Viewer PAN **[!UICONTROL 事件]** 作为触发器。
   * 将ZoomScale数据元 **[!UICONTROL 素的值]** 发送到Adobe Analytics。

* 
   * **[!UICONTROL TrackKey]** Rule with the follow:

   * 使用核心事件启动扩展的按键Adobe作为触发器。
   * 将ZoomScale数据元 **[!UICONTROL 素的值]** 发送到Adobe Analytics。

现在，假定最终用户加载包含两个查看器的网页。 在 *viewer1*&#x200B;中，它们放大到50%;然后，在 *viewer2中*，它们放大到25%缩放。 在 *viewer1*&#x200B;中，它们四处平移图像，最后按下键盘上的键。

最终用户的活动导致向Adobe Analytics发出以下两个跟踪调用：

* 第一次调用是因 **[!UICONTROL 为当用户]** 在viewer1中平移时触发 *TrackPan规则*。 该调用将50%作为ZoomScale Data Element **[!UICONTROL 的值]** ，因为数据元素将知道规则由viewer1触发并 *提取相应* 的缩放值；
* 第二次调用是因 **[!UICONTROL 为当用户]** 在键盘上按下键时触发TrackKey规则。 该调用将发送25%作为ZoomScale **[!UICONTROL 数据元素的值]** ，因为该规则不是由查看器触发的。 因此，数据元素返回最新值。

上述设置的示例还影响“数据元素”值的寿命。 即使查看器本身已放置在网页上，Dynamic Media Viewer所管理的Adobe元素值也会存储在启动库代码中。 这意味着，如果存在由非Dynamic Media Viewer扩展触发并引用此类数据元素的规则，则数据元素将返回最后一个已知值，即使该查看器不再出现在网页上也是如此。

无论如何，由Dynamic Media查看器驱动的数据元素值不会存储在本地存储或服务器上；而是仅保留在客户端Adobe启动库中。 当网页重新加载时，此类数据元素的值会消失。

通常，数据元素编辑器支持 [存储持续时间选择](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/manage-resources/data-elements.html#create-a-data-element)。 但是，使用Dynamic Media查看器扩展的存储元素仅支持“无”的数据持 **[!UICONTROL 续时间]**。 在用户界面中可以设置任何其他值，但在本例中未定义数据元素行为。 扩展自行管理数据元素的值：在整个查看器生命周期中维护查看器事件参数值的数据元素。

### 关于Dynamic Media Viewers扩展中的规则 {#about-rules-in-the-dynamic-media-viewers-extension}

在规则编辑器中，扩展将为事件编辑器添加新的配置选项。 此外，还提供了一个选项，用于在“操作”编辑器中手动引用事件参数，作为一个简单选项，而不是使用预配置的数据元素。

#### 关于事件编辑器 {#about-the-events-editor}

在事件编辑器中，Dynamic Media 查看器扩展会添加一个新的&#x200B;**[!UICONTROL 事件类型]**，称为&#x200B;**[!UICONTROL 查看器事件]**。

选中后，事件编辑器会呈现下拉 **[!UICONTROL 式Dynamic Media Viewer事件]**，列出Dynamic Media查看器支持的所有可用事件。

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### 关于操作编辑器 {#about-the-actions-editor}

通过Dynamic Media查看器扩展，您可以使用Dynamic Media查看器的事件参数映射到Adobe Analytics扩展的“设置变量”编辑器中的分析变量。

执行此操作的最简单方法是完成以下两步过程：

* 首先，定义一个或多个数据元素，其中每个数据元素都表示Dynamic Media Viewer事件的参数。
* 最后，在Adobe Analytics扩展的“设置变量”编辑器中，单击“数据元素”选取器图标（三个堆叠的磁盘）以打开“选择数据元素”对话框，然后从中选择一个数据元素。

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

但是，可以使用替代方法并绕过数据元素创建。通过在 Analytics 变量赋值的&#x200B;**[!UICONTROL 值]**&#x200B;输入字段中输入事件参数的完全限定的名称（由百分号 (%) 括起来），您可以直接引用 Dynamic Media Viewer 事件中的参数。例如，

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

请注意，使用事件元素与直接数据参数引用之间有重要区别。 对于数据元素，触发“设置变量”操作的事件无关紧要，触发规则的事件可能与动态查看器无关（如从核心扩展中单击网页）。 但是，在使用直接参数引用时，务必确保触发规则的事件与它引用的事件参数对应。

例如，如果规 `%event.detail.dm.LOAD.asset%` 则是由Dynamic Media Viewer扩展的 **[!UICONTROL LOAD]** 事件触发的，则引用将返回正确的资产名称。 但是，对于任何其他事件，它都会返回一个空值。

下表列表了Dynamic Media Viewer事件及其支持的参数：

<table>
 <tbody>
  <tr>
   <td>查看器事件名</td>
   <td>参数引用</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## 配置所有集成部分 {#configuring-all-the-integration-pieces}

**开始之前**

如果您尚未完成此操作，Adobe建议您在本节之前仔细查看所有文档，以了解完整集成。

本节介绍将Dynamic Media查看器与Adobe Analytics和Adobe Analytics音频和视频部门集成所需的配置步骤。 虽然在Adobe启动中将Dynamic Media查看器扩展用于其他用途是可能的，但本文档未介绍此类情况。

您将在以下Adobe产品中配置集成：

* Adobe Analytics-您将配置跟踪变量和报表。
* Adobe启动——您将定义一个属性、一个或多个规则以及一个或多个数据元素，以启用查看器跟踪。

此外，如果此集成解决方案与AEM Sites一起使用，则还需要进行以下配置：

* AdobeI/O控制台——为Adobe启动创建集成。
* AEM作者节点- IMS配置和Adobe启动云配置。

作为配置的一部分，请确保您有权访问已启用Adobe Analytics和Adobe启动的Adobe Experience Cloud公司。

## 为集成配置Adobe Analytics {#configuring-adobe-analytics-for-the-integration}

配置Adobe Analytics后，将为集成设置以下内容：

* 报告套件就位并处于选定状态。
* 分析变量可用于接收跟踪数据。
* 报告可用于视图Adobe Analytics内收集的数据。

另请参 [阅分析实施指南](https://docs.adobe.com/content/help/en/analytics/implementation/home.html)。

**为集成配置Adobe Analytics**:

1. 开始，从Experience Cloud [主页](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/)。 在菜单栏中，单击页面右上角附近的解决方案图标（三个圆点乘以三个圆点表），然后单击分 **[!UICONTROL 析]**。

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   您现在将选择一个报表包。

### 选择报表包 {#selecting-a-report-suite}

1. 在 Adobe Analytics 页面的右上角附近，在&#x200B;**[!UICONTROL 搜索报告]**&#x200B;字段的右侧，从下拉列表中选择正确的报表包。如果有多个可用报表包，并且您不确定要使用哪个报表包，请与 Adobe Analytics 管理员联系，帮助您选择要使用的报表包。

   在下图中，用户创建了一个名为DynamicMediaViewersExtensionDoc *的报表包* ，并从下拉列表中将其选中。 报告套件名称仅供说明；最终选择的报表包名称将有所不同。

   如果没有可用的报表包，则您或您的Adobe Analytics管理员必须创建一个报表包，然后才能继续进行配置。

   请参 [阅报表和报表](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/report-suites-admin.html)[包以及创建报表包](https://docs.adobe.com/content/help/en/analytics/admin/admin-console/create-report-suite.html)。

   在Adobe Analytics，报表包通过“管理员”>“ **[!UICONTROL 报表包”进行管理]**。

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   你现在设置Adobe Analytics变量。

### 设置Adobe Analytics变量 {#setting-up-adobe-analytics-variables}

1. 您现在将指定一个或多个要用于跟踪网页上Dynamic Media查看器行为的Adobe Analytics变量。

   可以使用Adobe Analytics支持的任何类型的变量。 有关变量类型(如自定义流量 [prop]、转换 [eVar])的决定应由您实施Analytics的特定需求来驱动。

   请参 [阅prop和eVar的概述](https://docs.adobe.com/content/help/en/analytics/implementation/vars/page-vars/evar.html)。

   就本文档而言，将仅使用自定义流量(props)变量，因为在网页上执行操作后几分钟内，这些变量便会显示在分析报告中。

   要启用新的自定义流量变量，请在工具栏的Adobe Analytics，单 **[!UICONTROL 击管理>报表包]**。

1. 在&#x200B;**[!UICONTROL 报表包管理器]**&#x200B;页面上，选择正确的报表，然后在工具栏中，单击&#x200B;**[!UICONTROL 编辑设置 > 流量 > 流量变量]**。
1. 在这里，选取未使用的变量，为它提供一个描述性 **[!UICONTROL 名称(查看器资产(prop 30)]**)，并将组合框更改为“已启用”列中的“已启用”。

   以下屏幕截图是自定义流量变量( **[!UICONTROL prop30]**)的示例，用于跟踪查看器使用的资产名称：

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. 在变量列表的底部，单击“保 **[!UICONTROL 存”]**。

### 设置报告 {#setting-up-a-report}

1. 通常，在Adobe Analytics设置报告是由特定项目需求驱动的。 因此，详细的报告设置超出了此集成的范围。

   但是，在设置Adobe Analytics变量中设置自定义流量变量后，您应该知道自定义流量报告在Adobe Analytics自动 **[变得可用](#setting-up-adobe-analytics-variables)**。

   例如，可从&#x200B;**[!UICONTROL 自定义流量 > 自定义流量 21 - 30 > 查看器资产 (prop 30)]**&#x200B;下的“报告”菜单中获得&#x200B;**[!UICONTROL 查看器资产 (prop 30)]**&#x200B;的报告。

   在查看器资产(prop 30)创 **[!UICONTROL 建后直接访问此报告]** ，不显示任何数据；在整合的这一阶段，人们就会期待它。

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## 为集成配置Adobe启动 {#configuring-adobe-launch-for-the-integration}

配置Adobe启动后，将为集成设置以下内容：

* 创建新属性以将您的所有配置保持一致。
* 扩展的安装和设置。 属性中安装的所有扩展的客户端代码一起编译为一个库。 此库稍后由网页使用。
* 数据元素和规则的配置。 此配置定义从Dynamic Media查看器捕获哪些数据、何时触发跟踪逻辑以及在Adobe Analytics将查看器的数据发送到何处。
* 发布库。

**为集成配置Adobe启动**:

1. 开始，即从Experience Cloud主页访问Adobe [启动](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/)。 在菜单栏中，单击页面右上角附近的解决方案图标（三个圆点对齐三个表），然后单击启 **[!UICONTROL 动]**。

   您还可以直 [接打开Adobe启动](https://launch.adobe.com/)。

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### 在Adobe启动中创建属性 {#creating-a-property-in-adobe-launch}

Adobe启动中的属性是将所有设置放在一起的命名配置。 将生成配置设置库并将其发布到不同的环境级别（开发、暂存和生产）。

另请参阅 [创建属性](https://docs.adobe.com/content/help/en/launch/using/implement/configure/create-a-property.html)。

1. 在Adobe启动中，单击 **[!UICONTROL 新建属性]**。
1. 在&#x200B;**[!UICONTROL 创建属性]**&#x200B;对话框的&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入描述性名称，如网站的标题。例如，`DynamicMediaViewersProp.`
1. 在“ **[!UICONTROL 域]** ”字段中，输入网站的域。
1. In the **[!UICONTROL Advanced Options]** drop-down, enable **[!UICONTROL Configure for extension development (cannot be modified later)]** in case the extension you want to use--in this case, *Dynamic Media Viewers*--is not yet released.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

   单击新创建的属性，然后继续 *安装和设置扩展*。

### 安装和设置扩展 {#installing-and-setup-of-extensions}

Adobe启动中的所有可用扩展都列在“扩展”>“ **[!UICONTROL 目录”下]**。

要安装扩展，请单击“ **[!UICONTROL 安装]**”。 如果需要，请执行一次性扩展配置，然后单击“ **[!UICONTROL 保存]**”。

在需要时，必须安装和配置以下扩展：

* （必需）*Experience CloudID服务*扩展

无需任何其他配置，接受任何建议的值。 完成后，请确保单击“保 **[!UICONTROL 存”]**。

请参 [阅Experience CloudID服务扩展](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)。

* （必需） *Adobe Analytics* 延保

要配置此扩展，您首先需要 Adobe Analytics 中&#x200B;**[!UICONTROL 管理员 > 报表包]** > **[!UICONTROL 报表包 ID]** 列标题下的报表包 ID。

（仅出于演示目的，在以下屏幕截图中将使用 **[!UICONTROL DynamicMediaViewersExtensionDoc]** 报表包的报表包 ID。此 ID 在之前的[选择报表包](#selecting-a-report-suite)中创建并使用。)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

在“安装扩展”页面的&#x200B;**[!UICONTROL 开发报表包]**&#x200B;字段、**[!UICONTROL 测试报表包]**&#x200B;字段和&#x200B;**[!UICONTROL 生产报表包]**&#x200B;字段中输入报表包 ID。

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*仅当您计划使用视频跟踪时，才配置以下项目：*

在“安 **[!UICONTROL 装扩展]** ”页面上，展 **[!UICONTROL 开“常规]**”，然后指定跟踪服务器。 跟踪服务器遵循模板 `<trackingNamespace>.sc.omtrdc.net`，即 `<trackingNamespace>` 在供应电子邮件中获取的信息。

单击&#x200B;**[!UICONTROL 保存]**。

请参阅 [Adobe Analytics分机](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)。

* (可选；（仅当需要视频跟踪时才需要） *Adobe音频和视频扩展的Media* Analytics

填写跟踪服务器字段。 用于音频和视 *频扩展的Adobe媒体分析的跟踪服务器* ，与用于Adobe Analytics的跟踪服务器不同。 它将遵循模 `<trackingNamespace>.hb.omtrdc.net`板， `<trackingNamespace>` 其中是供应电子邮件中的信息。

所有其他字段都是可选字段。

请参 [阅音频和视频扩展的Adobe媒体分析](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)。

* （必需） *Dynamic Media查看器扩* 展

选择&#x200B;**[!UICONTROL 启用 Adobe Analytics for Video]** 以启用（打开）视频检测信号跟踪。

请注意，在编写本文时，只有在创建Adobe *启动属性以供开发时* ,Dynamic Media Viewers扩展才可用。

请参 [阅在Adobe启动中创建属性](#creating-a-property-in-adobe-launch)。

安装和安装这些扩展后，“扩展”>“安装”区域至少会列出以下五个扩展（如果您没有跟踪视频，则至少列出四个）。

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### 设置数据元素和规则 {#setting-up-data-elements-and-rules}

在Adobe启动中，创建跟踪Dynamic Media查看器所需的数据元素和规则。

有 [关Adobe启动跟踪的概述，请参阅](#how-data-and-event-tracking-works-in-the-integration) “数据和事件跟踪在集成中的工作方式”。

请参 [阅Adobe启](#sample-configuration) 动中的示例配置示例，该示例配置演示如何在加载查看器时跟踪资产名称。

有 [关扩展功能的详细信息](#configuring-the-dynamic-media-viewers-extension) ，请参阅配置Dynamic Media Viewers扩展。

### 发布库 {#publishing-a-library}

要在Adobe启动配置（包括设置的属性、扩展、规则和数据元素）中进行更改，您需要发 *布* 此类更改*。*在Adobe启动中发布是从属性配置下的发布选项卡执行的。

Adobe启动可能具有多个开发环境、一个分阶段环境和一个生产环境。 默认情况下，AEM中的Adobe启动云配置将AEM作者节点指向Adobe启动的阶段环境，并将AEM发布节点指向Adobe启动的生产环境。 此安排意味着，使用默认的AEM设置，必须将Adobe启动库发布到临时环境，以便在AEM作者中使用它，然后将其发布到生产环境，以便在发布中使用它。

请参 [阅环境](https://docs.adobe.com/content/help/en/launch/using/reference/publish/environments.html) ，了解有关Adobe启动环境的更多信息。

发布库涉及以下两个步骤：

* 通过将所有必要的更改（新更改和更新）包含到库中来添加和构建新库。
* 将库向上移动到不同的环境级别（从开发到暂存和生产）

#### 添加和构建新库 {#adding-and-building-a-new-library}

1. 首次在Adobe启动中打开“发布”选项卡时，库列表为空。

   在左列中，单击“添 **[!UICONTROL 加新库”]**。

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. 在“创建新库”页面的“名 **[!UICONTROL 称]** ”字段中，输入新库的描述性名称。 例如，

   *DynamicMediaViewersLib*

   从环境下拉列表中，选择环境级别。 最初，只有“开发”级别可供选择。 在页面左下侧附近，单击“添加所有已 **[!UICONTROL 更改的资源”]**。

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Near the upper-right corner of the page, click **[!UICONTROL Save &amp; Build for Development]**.

   在几分钟内创建并准备使用库。

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >下次更改 Adobe Launch 配置时，转到&#x200B;**[!UICONTROL 属性]**&#x200B;配置下的&#x200B;**[!UICONTROL 发布]**&#x200B;选项卡，然后单击之前创建的库。
   >
   >
   >在库发布屏幕中，单击“添 **[!UICONTROL 加所有更改的资源]**”，然后单 **[!UICONTROL 击“保存并构建以供开发”]**。

#### 在环境级别上移库 {#moving-a-library-up-through-environment-levels}

1. 添加新库后，它最初位于“开发”环境。 要将其移至临时环境级别（与“已提交”列对应），请在库的下拉菜单中单击“提 **[!UICONTROL 交以待批准”]**。

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. 在确认对话框中，单击“ **[!UICONTROL 提交]**”。

   在库移到“已提交”列后，从库的下拉菜单中，单击“生成 **[!UICONTROL 以进行暂存”]**。

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. 按照类似的过程将库从暂存环境移动到生产环境（即已发布列）。

   首先，从下拉菜单中，单击“ **[!UICONTROL 批准发布”]**。

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. 从下拉菜单中，单击“构 **[!UICONTROL 建并发布到生产”]**。

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   请参 [阅发布](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) ，以了解有关Adobe启动中发布过程的更多信息。

## 为集成配置Adobe Experience Manager {#configuring-adobe-experience-manager-for-the-integration}

前提条件:

* AEM同时运行作者实例和发布实例。
* AEM作者节点在Dynamic Media -Scene7运行模式下设置(dynamicmedia_s7)
* 在AEM Sites启用Dynamic Media WCM组件。

AEM配置包含以下两个主要步骤：

* AEM IMS的配置
* 配置Adobe启动云。

### 配置AEM IMS {#configuring-aem-ims}

1. 在AEM作者中，单击工具图标（锤子），然后单 **[!UICONTROL 击安全>AdobeIMS配置]**。

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. 在“AdobeIMC配置”页的左上角附近，单击“创 **[!UICONTROL 建]**”。
1. 在 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面的&#x200B;**[!UICONTROL 云解决方案]**&#x200B;下拉列表中，单击 **[!UICONTROL Adobe Launch]**。
1. 启用 **[!UICONTROL 创建新证书]**，然后在文本字段中为证书输入任何有意义的值。 例如， *AdobeLaunchIMSCert*。 单击&#x200B;**[!UICONTROL 创建证书]**。

   将显示以下信息消息：

   *要检索有效访问令牌，必须将新证书的公钥添加到AdobeI/O！上的技术帐户*。

   Click **[!UICONTROL OK]** to dismiss the Info dialog box.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. 单 **[!UICONTROL 击“下载公钥]** ”，将公钥文件(*.crt)下载到本地系统。

   >[!NOTE]
   >
   >此时，请&#x200B;***保持打开*** **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面；***不要***&#x200B;关闭页面，并且&#x200B;***不要***&#x200B;单击“下一步”。在稍后的步骤中您将返回此页。

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. 在新的浏览器选项卡中，导航到 [AdobeI/O控制台](https://console.adobe.io/integrations)。

1. 在Adobe **[!UICONTROL I/O控制台集成页面]** （位于右上角附近），单击 **[!UICONTROL 新集成]**。
1. 在&#x200B;**[!UICONTROL 创建新集成]**&#x200B;对话框中，确保选中&#x200B;**[!UICONTROL 访问 API]** 单选按钮，然后单击&#x200B;**[!UICONTROL 继续]**。

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. 在第二个&#x200B;**[!UICONTROL 创建新集成]**&#x200B;页面上，启用（打开）**[!UICONTROL Experience Platform Launch API]** 单选按钮。在页面的右下角，单击&#x200B;**[!UICONTROL 继续]**。

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. 在第三个“ **[!UICONTROL 创建新集成]** ”页面上，执行以下操作：

   * 在名称 **[!UICONTROL 字段中]** ，输入描述性名称。 例如， *DynamicMediaViewersIO*。

   * 在“说 **[!UICONTROL 明]** ”字段中，输入集成的说明。

   * 在“公 **[!UICONTROL 钥证书]** ”区域，上传您之前在这些步骤中下载的公钥文件(*.crt)。

   * Under the **[!UICONTROL Select a role for Experience Platform Launch API]** heading, select **[!UICONTROL Admin]**.

   * 在“为 **[!UICONTROL Experience Platform LaunchAPI选择一个或多个产品用户档案]** ”标题下，选择 **[!UICONTROL 名为Launch - &lt;your_公司名称>的产品用户档案]**。

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Click **[!UICONTROL Create integration]**.
1. 在“已创 **[!UICONTROL 建集成]** ”页面上，单 **[!UICONTROL 击“继续”以获取集成详细信息]**。

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. 此时会显示“集成详细信 **** 息”页，与以下内容类似：

   >[!NOTE]
   >
   >***保持打开此集成详细信息页面***。稍后您将需要&#x200B;**[!UICONTROL 概述]**&#x200B;和 **[!UICONTROL JWT]** 选项卡中的各种信息。

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   集成详细信息页面。

1. 返回之前打开的 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面。在页面的右上角，单击&#x200B;**[!UICONTROL 下一步]**&#x200B;以在 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;窗口中打开&#x200B;**[!UICONTROL 帐户]**&#x200B;页面。

   （如果之前意外关闭了页面，请返回 AEM 作者，然后单击&#x200B;**[!UICONTROL 工具 > 安全 > Adobe IMS 配置]**。单击&#x200B;**[!UICONTROL 创建]**。在&#x200B;**[!UICONTROL 云解决方案]**&#x200B;下拉列表中，选择 **[!UICONTROL Adobe Launch]**。在&#x200B;**[!UICONTROL 证书]**&#x200B;下拉列表中，选择之前创建的证书的名称。）

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   AdobeIMS技术帐户配置——证书页。

1. “帐 **[!UICONTROL 户]** ”页面有五个字段，需要您使用上一步“集成”详细信息页面中的信息填写这些字段。

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   AdobeIMS技术帐户配置——帐户页。

1. 在“帐 **[!UICONTROL 户]** ”页面上，填写以下字段：

   * **[!UICONTROL 标题]** -输入描述性帐户标题。
   * **[!UICONTROL 授权服务器]** -返回到您之前打开的“集成详细信息”页。 Click the **[!UICONTROL JWT]** tab. 复制不带路径的服务器名称，如下所示高亮显示。

（示例服务器名称仅供说明之用）   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将名称粘贴到相应的字段中。例如，( `https://ims-na1.adobelogin.com/`示例服务器名称仅供说明之用)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   集成详细信息页- JWT选项卡

1. **[!UICONTROL API 密钥]** - 返回到“集成详细信息”页面。单击&#x200B;**[!UICONTROL 概述]**&#x200B;选项卡，然后单击 **[!UICONTROL API 密钥（客户端 ID）]**&#x200B;字段右侧的&#x200B;**[!UICONTROL 复制]**。

   Return to the **[!UICONTROL Account]** page, then paste the key into the respective ****field.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   集成详细信息页面。

1. **[!UICONTROL 客户端密钥]** - 返回到“集成详细信息”页面。在&#x200B;**[!UICONTROL 概述]**&#x200B;选项卡中，单击&#x200B;**[!UICONTROL 检索客户端密钥]**。在&#x200B;**[!UICONTROL 客户端密钥]**&#x200B;字段的右侧，单击&#x200B;**[!UICONTROL 复制]**。

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将密钥粘贴到相应的字段中。

1. **[!UICONTROL 有效负荷]** -返回到“集成详细信息”页。 从JWT **[!UICONTROL 选项卡]** 的JWT有效负荷字段中，复制整个JSON对象代码。

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将代码粘贴到相应的字段中。

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   集成详细信息页- JWT选项卡

   已填写所有字段的“帐户”页面的外观将类似于以下内容：

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Near the upper-right corner of the **[!UICONTROL Account]** page, click **[!UICONTROL Create]**.

   配置AEM IMS后，您现在有一个新的IMSAccount列在 **[!UICONTROL AdobeIMS配置下]**。

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## 配置Adobe启动云以进行集成 {#configuring-adobe-launch-cloud-for-the-integration}

1. 在AEM作者中，在左上角附近，单击工具图标（锤子），然后单击 **[!UICONTROL Cloud Services>Adobe启动配置]**。

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. 在Adobe **[!UICONTROL 启动配置页]** ，在左侧面板中，选择要应用Adobe启动配置的AEM站点。

   仅出于说明目的， **[!UICONTROL 在以下屏幕截图中选]** 择了We.Retail站点。

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. 在页面的左上角附近，单击&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建 Adobe Launch 配置]**&#x200B;窗口的&#x200B;**[!UICONTROL 常规]**&#x200B;页面（第 1/3 页）中，填写以下字段：

   * **[!UICONTROL 标题]** -输入描述性配置标题。 For example, `We.Retail Launch cloud configuration`.

   * **[!UICONTROL 关联AdobeIMS配置]** -选择您之前在配置AEM IMS时创 [建的IMS配置](#configuring-aem-ims)。

   * **[!UICONTROL 公司]** -从 **[!UICONTROL 公司下拉]** 列表中，选择您的Experience Cloud公司。 列表会自动填充。

   * **[!UICONTROL 属性]** -从“属性”下拉列表卡中，选择您之前创建的Adobe启动属性。 列表会自动填充。
   完成所有字段后，您的“ **[!UICONTROL 常规]** ”页面的外观将类似于以下内容：

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. 在左上角附近，单击“下 **[!UICONTROL 一步]**”。
1. 在&#x200B;**[!UICONTROL 创建 Adobe Launch 配置]**&#x200B;窗口的&#x200B;**[!UICONTROL 测试]**&#x200B;页面（第 2/3 页）中，填写以下字段：

   在&#x200B;**[!UICONTROL 库 URI]** 字段中，查看 Adobe Launch 库的测试版本的位置。AEM 会自动填充此字段。

   仅供说明，此步骤将使用部署到AdobeCDN的Adobe启动库。

   >[!NOTE]
   >
   >检查以确保自动填充的库URI（统一资源标识符）格式不正确。 如有必要，请修复它，使URI表示协议相对URI。 就是多次正斜杠开始.
   >
   >
   >For example: `//assets.adobetm.com/launch-xxxx`.

   **[!UICONTROL 测试]**&#x200B;页面应类似于以下内容。请注意，***未***&#x200B;设置异步&#x200B;**[!UICONTROL 存档]**&#x200B;和&#x200B;**[!UICONTROL 加载库]**&#x200B;选项：

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. 在右上角附近，单击“下 **[!UICONTROL 一步]**”。
1. 如有需要，在&#x200B;**[!UICONTROL 创建 Adobe Launch 配置]**&#x200B;窗口的&#x200B;**[!UICONTROL 生产]**&#x200B;页面（第 3/3 页）中，修复自动填充的生产 URI，类似于在上一个&#x200B;**[!UICONTROL 测试]**&#x200B;页面中的操作。
1. 在右上角附近，单击“创 **[!UICONTROL 建”]**。

   您的新Adobe启动云配置现已创建并列在您的网站旁边，如下例所示：

1. 选择新的Adobe启动云配置（选中配置标题后，将在其左侧显示复选标记）。 在工具栏中，单击“ **[!UICONTROL 发布]**”。

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

目前，AEM作者不支持将Dynamic Media查看器与Adobe启动相集成。

但是，AEM publish节点支持它。 使用Adobe启动云配置的默认设置，AEM publish使用Adobe启动的生产环境。 因此，在测试过程中，每次必须将Adobe启动库更新从开发推送到生产环境。

通过在上述Adobe发布的Adobe启动云配置中指定AEM启动库的开发或临时URL，可以解决此限制。 这样做会使AEM发布节点使用Adobe启动库的开发或暂存版本。

有关 [设置Adobe启](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html) 动云配置的详细信息，请参阅通过AdobeI/O将AEM与Adobe启动集成。
