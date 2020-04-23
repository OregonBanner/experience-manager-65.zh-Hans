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
source-git-commit: e8f97f6164a5021609917b99feb0608bcea59553

---


# 将 Dynamic Media 查看器与 Adobe Analytics 和 Adobe Launch 集成 {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## 什么是Dynamic Media Viewer与Adobe Analytics和Adobe Launch集成？ {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

The new *Dynamic Media Viewers* extension for Adobe Launch, along with the recent release of Dynamic Media Viewers 5.13, lets customers of Dynamic Media, Adobe Analytics, and Adobe Launch to use events and data specific for the Dynamic Media Viewers in their Adobe Launch configuration.

此集成意味着您可以使用Adobe Analytics跟踪网站上Dynamic Media查看器的使用情况。 同时，您可以将查看者公开的事件和数据与来自Adobe或第三方的任何其他Launch扩展一起使用。

请参 [阅Experience Platform Launch用户指南中的Adobe Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/overview.html) ，以进一步了解扩展。

**谁应阅读此文档：** AEM 平台及操作中的站点管理员、开发人员。

### 集成的限制 {#limitations-of-the-integration}

* Adobe Launch集成在AEM作者节点中不起作用。 在WCM页面发布之前，您无法看到任何跟踪。
* “弹出”操作模式不支持Adobe Launch集成Dynamic Media查看器，在该模式下，查看器URL是使用“资产详细信息”页面上的“URL”按钮获取的。
* Adobe Launch集成不能与旧版查看器分析集成（通过该参数）同时 `config2=` 使用。
* 视频跟踪支持仅限于核心回放跟踪，如跟踪概述 [中所述](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html)。 特别是，不支持QoS、广告、章节／段或错误跟踪。
* 使用Dynamic Media Viewer扩展的数据元素不支持数据元素的存储持 *续时间配置* 。 存储持续时间必须设置为 **[!UICONTROL 无]**。

### 集成用例 {#use-cases-for-the-integration}

与Adobe Launch集成的主要用例是同时使用AEM资产和AEM Sites的客户。 在这些情况下，您可以在AEM作者节点与Adobe Launch之间设置标准集成，然后将站点实例与Adobe Launch属性关联。 之后，添加到“站点”页面的任何Dynamic Media WCM组件都将跟踪查看者的数据和事件。

请参 [阅关于在AEM Sites中跟踪Dynamic Media查看器](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersinAEMSites)。

集成支持的次要用例是那些仅使用AEM资产或Dynamic Media Classic的客户。 在这种情况下，您可以获得查看器的嵌入代码并将其添加到网站页面。 然后，从Adobe Launch获取Adobe Launch库生产URL，然后手动将其添加到网页代码。

请参 [阅关于使用嵌入代码跟踪Dynamic Media查看器](https://wiki.corp.adobe.com/display/~oufimtse/Dynamic+Media+Viewers+integration+with+Adobe+Launch#DynamicMediaViewersintegrationwithAdobeLaunch-TrackingDynamicMediaViewersusingEmbedcode)。

## 数据和事件跟踪在集成中的工作方式 {#how-data-and-event-tracking-works-in-the-integration}

该集成利用两种独立的Dynamic Media查看器跟踪类型： *Adobe Analytics**和Adobe Analytics for Audio和Video*。

### 关于使用Adobe Analytics进行跟踪 {#about-tracking-using-adobe-analytics}

通过Adobe Analytics，您可以跟踪最终用户在与网站上的Dynamic Media查看器交互时执行的操作。 Adobe Analytics还允许您跟踪特定于查看器的数据。 例如，您可以跟踪和记录视图加载事件以及资产名称、发生的任何缩放操作、视频播放操作等。

在Adobe Launch中，数据元素和规 *则的概念可**以协同工作* ，从而实现Adobe Analytics跟踪。

#### 关于Adobe Launch中的数据元素 {#about-data-elements-in-adobe-launch}

Adobe Launch中的数据元素是一个命名的属性，其值是静态定义的，或是根据网页或Dynamic Media查看器数据的状态动态计算的。

可用于数据元素定义的选项取决于Adobe Launch属性中安装的扩展的列表。 “核心”扩展已预装，可在任何配置中开箱即用。 此“核心”扩展允许定义来自cookie、JavaScript代码、查询字符串和许多其他源的数据元素。

对于跟踪多个其他扩展的Adobe Analytics，需要安装这些扩展，如扩 [展的安装和设置中所述](#installing-and-setup-of-extensions)。 Dynamic Media查看器扩展添加了定义数据元素的功能，该值是Dynamic Viewer事件的参数。 例如，可引用查看器类型或查看器在加载时报告的资产名称、最终用户缩放时报告的缩放级别等。

Dynamic Media Viewer扩展可自动保持其数据元素的值保持最新。

定义数据元素后，可以使用数据元素选取器构件在Adobe Launch UI的其他位置使用数据元素。 特别是，为了跟踪Dynamic Media查看器而定义的数据元素将由规则中Adobe Analytics扩展的“设置变量操作”引用（请参阅下文）。

请参 [阅Experience Platform](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/manage-resources/data-elements.html) Launch用户指南中的数据元素以了解更多信息。

#### 关于Adobe Launch中的规则 {#about-rules-in-adobe-launch}

Adobe Launch中的规则是一个不可知的配置，它定义了构成规则的三个区域： *事件*、条 *件*、 *操作*:

* *事件* （如果）告知Adobe Launch何时触发规则。
* *条件* （如果）告知Adobe Launch在触发规则时允许或禁止哪些其他限制。
* *操作* （然后）告知Adobe Launch在触发规则时要执行什么操作。

“事件”、“条件”和“操作”部分中提供的选项取决于Adobe Launch属性中安装的扩展。 Core *扩展已预装* ，并可在任何配置中开箱即用。 该扩展为事件提供多个选项，如基本的浏览器级操作，这些操作包括焦点更改、按键、表单提交等。 它还包含Conditions选项，如cookie值、浏览器类型等。 对于“操作”，仅“自定义代码”选项可用。

对于Adobe Analytics跟踪，必须安装若干附加扩展，如扩展的安 [装和设置中所述](#installing-and-setup-of-extensions)。 具体而言：

* Dynamic Media Viewer扩展将受支持事件的列表扩展到特定于Dynamic Media查看器的事件，如查看器加载、资产交换、放大和视频播放。
* Adobe Analytics扩展扩展了支持的操作的列表，其中包含向跟踪服务器发送数据所需的两个操作：设 *置变量* , *发送信标*。

要跟踪Dynamic Media查看器，可以使用以下任何类型：

* Dynamic Media Viewers扩展、核心扩展或任何其他扩展的事件。
* 规则定义中的条件。 或者，您可以将条件区域留空。

在“操作”部分，您必须执行“设置变 *量”操作* 。 此操作告诉Adobe Analytics如何用数据填充跟踪变量。 同时，“设置变量 ** ”动作不会向跟踪服务器发送任何内容。

“设 *置变量* ”动作后面必须有“发送信 *标”动作* 。 “发 *送信标* ”动作实际会向分析跟踪服务器发送数据。 这两个操 *作(设置变量* )和 *发送信标*)都来自Adobe Analytics扩展。

请参 [阅](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/manage-resources/rules.html) Experience Platform Launch用户指南中的规则，了解更多信息。

#### 示例配置 {#sample-configuration}

Adobe Launch中的以下示例配置演示了如何在加载查看器时跟踪资产名称。

1. 在“数 **[!UICONTROL 据元素]** ”选项卡中，定义一个数据元素， `AssetName` 该元素从Dynamic Media Viewers扩 `asset` 展引用 `LOAD` 事件的参数。

   ![image2019-11](assets/image2019-11.png)

1. 在“规 **[!UICONTROL 则]** ”选项卡中，定义规则 *TrackAssetOnLoad*。

   在此规则中， **[!UICONTROL 事件字段]** 使用Dynamic Media Viewers扩 **[!UICONTROL 展的LOAD]** 事件。

   ![image2019-22](assets/image2019-22.png)

1. 操作配置有Adobe Analytics扩展中的两种操作类型：

   *设置变量*，将您选择的分析变量映射到数据元素 `AssetName` 的值。

   *发送信标*，将跟踪信息发送到Adobe Analytics。

   ![image2019-3](assets/image2019-3.png)

1. 生成的规则配置如下所示：

   ![image2019-4](assets/image2019-4.png)

### 关于Adobe Analytics for Audio和Video {#about-adobe-analytics-for-audio-and-video}

订阅Experience Cloud帐户后，即可使用Adobe Analytics for Audio和Video，这足以在 *Dynamic Media Viewers扩展设置中启用视频跟踪* 。 视频指标在Adobe Analytics中可用。 视频跟踪取决于是否存在Adobe Media Analytics for Audio和Video扩展。

请参 [阅安装和设置扩展](#installing-and-setup-of-extensions)。

目前，对视频跟踪的支持仅限于“核心回放”跟踪，如跟踪概述 [中所述](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/track-av-playback/track-core-overview.html)。 特别是，不支持QoS、广告、章节／段或错误跟踪。

## 使用Dynamic Media Viewer扩展 {#using-the-dynamic-media-viewers-extension}

如集成 [的使用案例中所述](#use%20cases%20for%20the%20integration)，可以通过AEM Sites中新的Adobe Launch集成和嵌入代码跟踪Dynamic Media查看器。

### 在AEM Sites中跟踪Dynamic Media查看器 {#tracking-dynamic-media-viewers-in-aem-sites}

要跟踪AEM Sites中的Dynamic Media查看器，必须执行配置所 [有集成部分下列出的所有步骤](#configuring-all-the-integration-pieces) 。 具体而言，您必须创建IMS配置和Adobe Launch Cloud配置。

在正确配置后，您使用Dynamic Media支持的WCM组件添加到“站点”页面的任何Dynamic Media查看器都会自动跟踪数据至Adobe Analytics或Adobe Analytics for Video，或同时跟踪数据至两者。

请参 [阅使用Adobe Sites将Dynamic Media资产添加到页面](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)。

### 使用嵌入代码跟踪Dynamic Media查看器 {#tracking-dynamic-media-viewers-using-embed-code}

未使用AEM Sites或将Dynamic Media查看器嵌入AEM Sites外的网页或两者兼有的客户仍可使用Adobe Launch集成。

您必须完成[配置 Adobe Analytics](#configuringadobeanalytics) 和[配置 Adobe Launch](#configuringadobelaunch) 部分中的配置步骤。但是，不需要执行与 AEM 相关的配置步骤。

在进行正确配置后，您可以使用Dynamic Media查看器将Adobe Launch支持添加到网页。

请参 [阅添加启动项嵌入代码](https://docs.adobe.com/content/help/en/launch/using/implement/configure/implement-the-launch-install-code.html) ，进一步了解如何使用Adobe Launch库嵌入代码。

请参 [阅在网页上嵌入视频查看器或图像查看器](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html) ，进一步了解如何使用AEM Dynamic Media的嵌入代码功能。

**要使用嵌入代码跟踪Dynamic Media查看器**:

1. 准备网页以嵌入Dynamic Media查看器。
1. 首先登录Adobe Launch，获取Adobe Launch库的嵌入代码(请参阅配 [置Adobe Launch](#configuringadobelaunch))。
1. 单击 **[!UICONTROL 属性]**，然后单击 **[!UICONTROL 环境]** 选项卡。
1. 提高与网页环境相关的环境级别。 然后，在“安 **[!UICONTROL 装]** ”列中，单击框图标。
1. **[!UICONTROL 在“Web安装说明]** ”对话框中，复制完整的Adobe Launch库嵌入代码以及周围的标 `<script/>` 记。

## Dynamic Media查看器扩展的参考指南 {#reference-guide-for-the-dynamic-media-viewers-extension}

### 关于Dynamic Media查看器配置 {#about-the-dynamic-media-viewers-configuration}

如果满足以下所有条件，则Dynamic Media Viewer扩展会自动与Adobe Launch库集成：

* 页面上存在Adobe Launch库 `_satellite`全局对象()。
* Dynamic Media Viewer扩展功能 `_dmviewers_v001()` 在上定义 `_satellite`。

* `config2=` 未指定查看器参数，这表示查看器不使用传统Analytics集成。

此外，还有一个选项，可通过在查看器的配置中指定参数来显 `launch=0` 式禁用查看器中的Adobe Launch集成。 此参数的默认值是 `1`。

### 配置Dynamic Media Viewer扩展 {#configuring-the-dynamic-media-viewers-extension}

Dynamic Media Viewer扩展的唯一配置选项是 **[!UICONTROL 为音频和视频启用Adobe Media Analytics]**。

选中（启用或“打开”）此选项后，如果安装并正确配置了Adobe Media Analytics for Audio和Video扩展，则视频播放量度将发送到Adobe Analytics for Audio和Video解决方案。 禁用此选项将关闭视频跟踪。

请注意，如果您启用此选 *项* ，但未安装Adobe Media Analytics for Audio和Video扩展，则此选项无效。

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### 关于Dynamic Media Viewer扩展中的数据元素 {#about-data-elements-in-the-dynamic-media-viewers-extension}

Dynamic Media Viewers 扩展提供的唯一数据元素类型是&#x200B;**[!UICONTROL 数据元素类型]**&#x200B;下拉列表中的&#x200B;**[!UICONTROL 查看器事件]**。

选择此选项后，数据元素编辑器将呈现一个包含两个字段的表单：

* **[!UICONTROL DM 查看器事件数据类型]** - 一个下拉列表，标识了 Dynamic Media 查看器扩展支持的所有查看器事件（具有参数）以及特殊的 **[!UICONTROL COMMON]** 项目。**[!UICONTROL COMMON]** 项目表示事件参数列表，这些事件参数对查看器发送的所有类型事件都是通用的。
* **[!UICONTROL 跟踪参数]** -选定Dynamic Media查看器事件的参数。

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

有关按每 [种查看器类型列表受支持事件的信息](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_s7_aem_asset_viewers.html) ，请参阅Dynamic Media查看器参考指南；转到特定查看器部分，然后单击Adobe Analytics跟踪支持子部分。 目前，Dynamic Media查看器参考指南不文档事件参数。

现在，我们来考虑Dynamic Media查看器数据元素的 *生命周期*。 在页面上发生相应的Dynamic Media查看器事件后，将填充此类数据元素的值。 例如，如果数据元素指向 **[!UICONTROL LOAD]** 事件及其“asset”参数，则此类数据元素的值将在查看器首次运行LOAD事件后接收有效数据。 如果数据元素指向 **[!UICONTROL ZOOM]** 事件及其“scale”参数，则此类数据元素的值将保持为空，直到查看器首次发送 **[!UICONTROL ZOOM]** 事件。

同样，当查看器在页面上发送相应事件时，数据元素的值也会自动更新。即使在规则配置中未指定特定事件，也会发生值更新。例如，如果为 ZOOM 事件的“scale”参数定义了数据元素 **[!UICONTROL ZoomScale]**，但“规则”配置中唯一存在的规则由 **[!UICONTROL LOAD]** 事件触发，则每当用户在查看器中运行缩放时，**[!UICONTROL ZoomScale]** 的值仍会更新。

任何Dynamic media查看器在网页上都有唯一标识符。 数据元素会跟踪值本身以及已填充该值的查看器。 这意味着，如果同一页面上有多个查看器，并且有一个指向 **[!UICONTROL LOAD]** 事件及其“asset”参数的 **[!UICONTROL AssetName]** Data Element，则 **[!UICONTROL AssetName]** Data Element将保留与页面上加载的每个查看器关联的资产名称集合。

数据元素返回的确切值取决于上下文。 如果在由Dynamic Media查看器事件触发的规则中请求数据元素，则为启动该规则的查看器返回数据元素值。 而且，如果数据元素是在由某个其他Adobe Launch扩展的事件触发的规则中请求的，则数据元素的值是查看器中最后一个更新此数据元素的值。

**请考虑以下示例设置**:

* 包含两个Dynamic Media缩放查看器的网页；我们将它们称为 *viewer1* 和 *viewer2*。

* **[!UICONTROL ZoomScale]** Data Element指向 **[!UICONTROL ZOOM]** 事件及其“scale”参数。
* **[!UICONTROL TrackPan规则]** ，包含以下内容：

   * 使用Dynamic Media Viewer **[!UICONTROL PAN事件]** 作为触发器。
   * 将 **[!UICONTROL ZoomScale数据元素的值发送]** 到Adobe Analytics。

* 
   * **[!UICONTROL TrackKey规则]** ，包含以下内容：

   * 使用核心Adobe Launch扩展的按键事件作为触发器。
   * 将 **[!UICONTROL ZoomScale数据元素的值发送]** 到Adobe Analytics。

现在，假设最终用户加载包含两个查看器的网页。 在 *viewer1中*，它们放大到50%;然后，在 *viewer2中*，它们放大到25%的缩放比例。 在 *viewer1中*，它们会四处平移图像，最后按下键盘上的键。

最终用户的活动导致对Adobe Analytics进行以下两次跟踪调用：

* 第一次调用是因 **[!UICONTROL 为当用户在viewer1中平移时触发]** TrackPan *Rule*。 该调用将50%作为 **[!UICONTROL ZoomScale]** Data Element的值发送，因为数据元素将知道规则是由 *viewer1触发的* ，并提取相应的缩放值；
* 第二次调用是因 **[!UICONTROL 为当用户按下键盘上的键时，将触发]** TrackKey Rule。 该调用将发送25%作为 **[!UICONTROL ZoomScale]** Data Element的值，因为该规则不是由查看器触发的。 因此，数据元素会返回最新值。

上述设置的样本也会影响“数据元素”值的寿命。 Dynamic Media Viewer管理的数据元素的值存储在Adobe Launch库代码中，即使查看器本身已放置在网页上也是如此。 这意味着，如果存在由非Dynamic Media Viewer扩展触发并引用此类数据元素的规则，则数据元素将返回上一个已知值，即使查看器不再出现在网页上也是如此。

无论如何，由Dynamic Media查看器驱动的数据元素的值不会存储在本地存储或服务器上；而是仅保留在客户端Adobe Launch库中。 重新加载网页时，此类数据元素的值会消失。

通常，数据元素编辑器支持选择 [存储持续时间](https://docs.adobe.com/content/help/zh-Hans/launch/using/reference/manage-resources/data-elements.html#create-a-data-element)。 但是，使用Dynamic Media查看器扩展的数据元素仅支持“无”的存储持续时 **[!UICONTROL 间选项]**。 在用户界面中可以设置任何其他值，但在这种情况下，“数据元素”行为没有定义。 该扩展自行管理数据元素的值：在整个查看器生命周期中维护查看器事件参数值的数据元素。

### 关于Dynamic Media查看器扩展中的规则 {#about-rules-in-the-dynamic-media-viewers-extension}

在规则编辑器中，该扩展为事件编辑器添加新的配置选项。 还提供了在操作编辑器中手动引用事件参数的选项，作为简单选项，而不是使用预配置的数据元素。

#### 关于事件编辑器 {#about-the-events-editor}

在事件编辑器中，Dynamic Media 查看器扩展会添加一个新的&#x200B;**[!UICONTROL 事件类型]**，称为&#x200B;**[!UICONTROL 查看器事件]**。

选择事件编辑器后，将呈现下拉式 **[!UICONTROL Dynamic Media Viewer事件]**，其中列出Dynamic Media查看器支持的所有可用事件。

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### 关于操作编辑器 {#about-the-actions-editor}

通过Dynamic Media查看器扩展，您可以使用Dynamic Media查看器的事件参数映射到Adobe Analytics扩展的“设置变量”编辑器中的分析变量。

执行此操作的最简单方法是完成以下两个步骤：

* 首先，定义一个或多个数据元素，其中每个数据元素表示Dynamic Media Viewer事件的参数。
* 最后，在Adobe Analytics扩展的“设置变量”编辑器中，单击“数据元素”选取器图标（三个堆叠的磁盘）以打开“选择数据元素”对话框，然后从中选择一个数据元素。

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

但是，可以使用替代方法并绕过数据元素创建。通过在 Analytics 变量赋值的&#x200B;**[!UICONTROL 值]**&#x200B;输入字段中输入事件参数的完全限定的名称（由百分号 (%) 括起来），您可以直接引用 Dynamic Media Viewer 事件中的参数。例如，

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

请注意，使用数据元素与直接事件参数引用之间有重要区别。 对于数据元素，触发“设置变量”动作的事件无关紧要，触发规则的事件可能与Dynamic Viewer无关（如从核心扩展中在网页上单击鼠标）。 但是，在使用直接参数引用时，务必确保触发规则的事件与它引用的事件参数相对应。

例如，如果规 `%event.detail.dm.LOAD.asset%` 则是由Dynamic Media Viewer扩展的 **[!UICONTROL LOAD]** 事件触发的，则引用将返回正确的资产名称。 但是，对于任何其他事件，它都会返回一个空值。

下表列表了Dynamic Media Viewer事件及其支持的参数：

<table>
 <tbody>
  <tr>
   <td>查看器事件名称</td>
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

**开始前**

如果您尚未这样做，Adobe建议您仔细查看本节之前的所有文档，以了解完整集成。

本节介绍将Dynamic Media查看器与Adobe Analytics及Adobe Analytics for Audio和Video集成所需的配置步骤。 虽然在Adobe Launch中可能将Dynamic Media查看器扩展用于其他用途，但本文档未涵盖此类场景。

您将在以下Adobe产品中配置集成：

* Adobe Analytics —— 您将配置跟踪变量和报告。
* Adobe Launch —— 您将定义一个属性、一个或多个规则以及一个或多个数据元素以启用查看器跟踪。

此外，如果此集成解决方案与AEM Sites一起使用，则还需要执行以下配置：

* Adobe I/O Console —— 为Adobe Launch创建集成。
* AEM作者节点- IMS配置和Adobe Launch云配置。

作为配置的一部分，请确保您有权访问已启用Adobe Analytics和Adobe Launch的Adobe Experience Cloud中的公司。

## 配置Adobe Analytics以进行集成 {#configuring-adobe-analytics-for-the-integration}

配置Adobe Analytics后，将为集成设置以下内容：

* “报表包”就位并处于选中状态。
* 分析变量可用于接收跟踪数据。
* 报告可用于视图Adobe Analytics中收集的数据。

另请参阅 [分析实施指南](https://docs.adobe.com/content/help/en/analytics/implementation/home.html)。

**要配置Adobe Analytics进行集成，请执行以下操作**:

1. 开始，即可从Experience Cloud [主页访问Adobe Analytics](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/)。 在菜单栏中，单击页面右上角附近的解决方案图标（三个圆点对齐三个表），然后单击分 **[!UICONTROL 析]**。

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   您现在将选择一个报表包。

### 选择报表包 {#selecting-a-report-suite}

1. 在 Adobe Analytics 页面的右上角附近，在&#x200B;**[!UICONTROL 搜索报告]**&#x200B;字段的右侧，从下拉列表中选择正确的报表包。如果有多个可用报表包，并且您不确定要使用哪个报表包，请与 Adobe Analytics 管理员联系，帮助您选择要使用的报表包。

   在下图中，用户创建了一个名为 ** DynamicMediaViewersExtensionDoc的报表包，并从下拉列表中将其选中。 报告套件名称仅供说明；您最终选择的报表包的名称将有所不同。

   如果没有可用的报告套件，则您或您的Adobe Analytics管理员必须先创建一个报告套件，然后才能继续进一步配置。

   请参 [阅报告和报告套件](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/ref-reports-report-suites.html) , [以及创建报告套件](https://docs.adobe.com/content/help/en/analytics/admin/admin-console/create-report-suite.html)。

   在Adobe Analytics中，报表包在“管理员”>“报 **[!UICONTROL 表包”下进行管理]**。

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   您现在将设置Adobe Analytics变量。

### 设置Adobe Analytics变量 {#setting-up-adobe-analytics-variables}

1. 您现在将指定一个或多个Adobe Analytics变量，以便用于跟踪网页上的Dynamic Media查看器行为。

   可以使用Adobe Analytics支持的任何类型的变量。 关于变量类型(如自定义流量 [prop]、转 [化eVar])的决定应由您实施Analytics的特定需求驱动。

   请参 [阅prop和eVar概述](https://docs.adobe.com/content/help/en/analytics/implementation/analytics-basics/traffic-props-evars/props-evars.html)。

   就本文档而言，只有自定义流量(props)变量才会被使用，因为在网页上发生操作后的几分钟内，这些变量便会在分析报告中可用。

   要启用新的自定义流量变量，请在Adobe Analytics的工具栏中，单击管理员> **[!UICONTROL 报表包]**。

1. 在&#x200B;**[!UICONTROL 报表包管理器]**&#x200B;页面上，选择正确的报表，然后在工具栏中，单击&#x200B;**[!UICONTROL 编辑设置 > 流量 > 流量变量]**。
1. 在此，选取未使用的变量，为它指定一个描述性名称( **[!UICONTROL Viewer asset(prop 30)]**)，并在“已启用”列中将组合框更改为“已启用”。

   以下屏幕截图是自定义流量变量( **[!UICONTROL prop30]**)的示例，用于跟踪查看器使用的资产名称：

   ![image2019-6-26_23-6-59](assets/image2019-6-26_23-6-59.png)

1. 在变量列表的底部，单击“保 **[!UICONTROL 存”]**。

### 设置报告 {#setting-up-a-report}

1. 通常，在Adobe Analytics中设置报告由特定项目需求驱动。 因此，详细的报告设置超出了此集成的范围。

   但是，在设置Adobe Analytics变量中设置“自定义流量”变量后，您应该知道“自定义流量”报表 **[会在Adobe Analytics中自动可用](#setting-up-adobe-analytics-variables)**。

   例如，可从&#x200B;**[!UICONTROL 自定义流量 > 自定义流量 21 - 30 > 查看器资产 (prop 30)]**&#x200B;下的“报告”菜单中获得&#x200B;**[!UICONTROL 查看器资产 (prop 30)]**&#x200B;的报告。

   在查看器资产(prop 30)创 **[!UICONTROL 建后直接访问此报告]** ，不显示任何数据；在整合的这一阶段，人们就会期待它。

   ![image2019-6-26_23-12-49](assets/image2019-6-26_23-12-49.png)

## 配置Adobe Launch以进行集成 {#configuring-adobe-launch-for-the-integration}

配置Adobe Launch后，将为集成设置以下内容：

* 创建新属性以将所有配置保持一致。
* 扩展的安装和设置。 属性中安装的所有扩展的客户端代码一起编译到一个库中。 此库稍后由网页使用。
* 配置数据元素和规则。 此配置定义从Dynamic Media查看器捕获哪些数据，何时触发跟踪逻辑，以及在Adobe Analytics中将查看器的数据发送到何处。
* 发布库。

**要配置Adobe Launch以进行集成，请执行以下操作**:

1. 开始，即可从Experience Cloud [主页访问Adobe Launch](https://exc-home.experiencecloud.adobe.com/exc-home/home.html#/)。 在菜单栏中，单击页面右上角附近的解决方案图标（三个圆点对齐三个表），然后单击启 **[!UICONTROL 动]**。

   您还可以直 [接打开Adobe Launch](https://launch.adobe.com/)。

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### 在Adobe Launch中创建属性 {#creating-a-property-in-adobe-launch}

Adobe Launch中的属性是将所有设置放在一起的命名配置。 将生成配置设置库并发布到不同的环境级别（开发、升级和生产）。

另请参阅 [创建属性](https://docs.adobe.com/content/help/en/launch/using/implement/configure/create-a-property.html)。

1. 在Adobe Launch中，单击“新 **[!UICONTROL 建属性”]**。
1. 在&#x200B;**[!UICONTROL 创建属性]**&#x200B;对话框的&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入描述性名称，如网站的标题。例如，`DynamicMediaViewersProp.`
1. 在“ **[!UICONTROL 域]** ”字段中，输入网站的域。
1. In the **[!UICONTROL Advanced Options]** drop-down, enable **[!UICONTROL Configure for extension development (cannot be modified later)]** in case the extension you want to use--in this case, *Dynamic Media Viewers*--is not yet released.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

   单击新创建的属性，然后继续安 *装和设置扩展*。

### 安装和设置扩展 {#installing-and-setup-of-extensions}

Adobe Launch中的所有可用扩展都列在“扩展”>“ **[!UICONTROL 目录”下]**。

要安装扩展，请单击“安 **[!UICONTROL 装”]**。 如果需要，请执行一次性扩展配置，然后单击“保 **[!UICONTROL 存”]**。

在需要时，必须安装和配置以下扩展：

* （必需）*Experience Cloud ID服务*扩展

无需其他配置，接受任何建议的值。 完成后，请确保单击“保 **[!UICONTROL 存”]**。

请参 [阅Experience Cloud ID服务扩展](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)。

* （必需） *Adobe Analytics扩展*

要配置此扩展，您首先需要 Adobe Analytics 中&#x200B;**[!UICONTROL 管理员 > 报表包]** > **[!UICONTROL 报表包 ID]** 列标题下的报表包 ID。

（仅出于演示目的，在以下屏幕截图中将使用 **[!UICONTROL DynamicMediaViewersExtensionDoc]** 报表包的报表包 ID。此 ID 在之前的[选择报表包](#selecting-a-report-suite)中创建并使用。)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

在“安装扩展”页面的&#x200B;**[!UICONTROL 开发报表包]**&#x200B;字段、**[!UICONTROL 测试报表包]**&#x200B;字段和&#x200B;**[!UICONTROL 生产报表包]**&#x200B;字段中输入报表包 ID。

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*仅当您计划使用视频跟踪时，才配置以下项目：*

在“安 **[!UICONTROL 装扩展]** ”页上，展开“ **[!UICONTROL 常规]**”，然后指定跟踪服务器。 跟踪服务器会遵循模 `<trackingNamespace>.sc.omtrdc.net`板，其 `<trackingNamespace>` 中是在供应电子邮件中获取的信息。

单击&#x200B;**[!UICONTROL 保存]**。

请参 [阅Adobe Analytics扩展](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)。

* (可选；仅在需要视频跟踪时才需要) *Adobe Media Analytics for Audio和Video* Extension

填写跟踪服务器字段。 用于 ** Adobe Media Analytics for Audio和Video扩展的跟踪服务器与用于Adobe Analytics的跟踪服务器不同。 它将遵循模 `<trackingNamespace>.hb.omtrdc.net`板，其 `<trackingNamespace>` 中是供应电子邮件中的信息。

所有其他字段都是可选的。

请参 [阅适用于音频和视频扩展的Adobe Media Analytics](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)。

* （必需） *Dynamic Media查看器扩展*

选择&#x200B;**[!UICONTROL 启用 Adobe Analytics for Video]** 以启用（打开）视频检测信号跟踪。

请注意，在编写本文时， *Dynamic Media Viewers* extension仅在创建Adobe Launch属性用于开发时可用。

请参 [阅在Adobe Launch中创建属性](#creating-a-property-in-adobe-launch)。

安装和设置这些扩展后，“扩展”>“安装”区域中至少将列出以下五个扩展（如果不跟踪视频，则至少列出四个）。

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### 设置数据元素和规则 {#setting-up-data-elements-and-rules}

在Adobe Launch中，创建跟踪Dynamic Media查看器所需的数据元素和规则。

有关 [使用Adobe Launch进行跟踪的概述](#how-data-and-event-tracking-works-in-the-integration) ，请参阅数据和事件跟踪在集成中的工作方式。

请参 [阅Adobe Launch中的示例配置](#sample-configuration) ，该配置演示了如何在加载查看器时跟踪资产名称。

有 [关扩展功能的详细信息](#configuring-the-dynamic-media-viewers-extension) ，请参阅配置Dynamic Media Viewers扩展。

### 发布库 {#publishing-a-library}

要在Adobe Launch配置中进行更改（包括设置的属性、扩展、规则和数据元素），您需要发 *布* 此类更改*。*在Adobe Launch中发布是从属性配置下的发布选项卡执行的。

Adobe Launch可能具有多个开发环境、一个分阶段环境和一个生产环境。 默认情况下，AEM中的Adobe Launch Cloud配置将AEM作者节点指向Adobe Launch的舞台环境，将AEM发布节点指向Adobe Launch的生产环境。 此安排意味着，使用默认的AEM设置，必须将Adobe Launch库发布到“暂存”环境，以便在AEM作者中使用它，然后将其发布到“生产”环境，以便在AEM发布中使用它。

有关Adobe [Launch环境](https://docs.adobe.com/content/help/en/launch/using/reference/publish/environments.html) ，请参阅环境。

发布库涉及以下两个步骤：

* 通过将所有必要的更改（新更改和更新）包含到库中来添加和构建新库。
* 在不同的环境级别（从开发到暂存和生产）之间移动库

#### 添加和构建新库 {#adding-and-building-a-new-library}

1. 第一次在Adobe Launch中打开“发布”选项卡时，库列表为空。

   在左列中，单击“添 **[!UICONTROL 加新库”]**。

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. 在“创建新库”页面的“名 **[!UICONTROL 称]** ”字段中，输入新库的描述性名称。 例如，

   *DynamicMediaViewersLib*

   从环境下拉列表中，选择环境级别。 最初，只有“开发”级别可供选择。 在页面左下侧附近，单击“添加所有更 **[!UICONTROL 改的资源”]**。

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Near the upper-right corner of the page, click **[!UICONTROL Save &amp; Build for Development]**.

   几分钟后，库即会创建并准备使用。

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >下次更改 Adobe Launch 配置时，转到&#x200B;**[!UICONTROL 属性]**&#x200B;配置下的&#x200B;**[!UICONTROL 发布]**&#x200B;选项卡，然后单击之前创建的库。
   >
   >
   >在库发布屏幕中，单击“添 **[!UICONTROL 加所有更改的资源”]**，然后单击“ **[!UICONTROL 保存并构建以供开发”]**。

#### 在环境级别中向上移动库 {#moving-a-library-up-through-environment-levels}

1. 添加新库后，它最初位于开发环境中。 要将其移至暂存环境级别（与“已提交”列相对应），请在库的下拉菜单中，单击“提 **[!UICONTROL 交以待批准”]**。

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. 在确认对话框中，单击“提 **[!UICONTROL 交”]**。

   在库移到“已提交”列后，从库的下拉菜单中，单击“构建 **[!UICONTROL 以进行暂存”]**。

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. 按照类似的过程将库从暂存环境移到生产环境（即已发布列）。

   首先，从下拉菜单中，单击“批准 **[!UICONTROL 发布”]**。

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. 从下拉菜单中，单击“构建并 **[!UICONTROL 发布到生产”]**。

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   有关 [Adobe Launch中发布过程的更多信息](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) ，请参阅发布。

## 配置Adobe Experience Manager以实现集成 {#configuring-adobe-experience-manager-for-the-integration}

前提条件:

* AEM同时运行作者实例和发布实例。
* AEM作者节点在Dynamic Media - Scene7运行模式(dynamicmedia_s7)中设置
* 在AEM Sites中启用了Dynamic Media WCM组件。

AEM配置包含以下两个主要步骤：

* 配置AEM IMS
* Adobe Launch Cloud的配置。

### 配置AEM IMS {#configuring-aem-ims}

1. 在AEM作者中，单击工具图标（锤子），然后单击 **[!UICONTROL 安全> Adobe IMS配置]**。

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. 在Adobe IMC配置页面左上角附近，单击创 **[!UICONTROL 建]**。
1. 在 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面的&#x200B;**[!UICONTROL 云解决方案]**&#x200B;下拉列表中，单击 **[!UICONTROL Adobe Launch]**。
1. 启用 **[!UICONTROL 创建新证书]**，然后在文本字段中为证书输入任何有意义的值。 例如， *AdobeLaunchIMSCert*。 单击“ **[!UICONTROL 创建证书]**”。

   此时将显示以下信息消息：

   *要检索有效的访问令牌，必须将新证书的公钥添加到Adobe I/O！上的技术帐户中*。

   Click **[!UICONTROL OK]** to dismiss the Info dialog box.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. 单 **[!UICONTROL 击“下载公钥]** ”以将公钥文件(*.crt)下载到本地系统。

   >[!NOTE]
   >
   >此时，请&#x200B;***保持打开*** **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面；***不要***&#x200B;关闭页面，并且&#x200B;***不要***&#x200B;单击“下一步”。在稍后的步骤中您将返回此页。

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. 在新的浏览器选项卡中，导航到 [Adobe I/O控制台](https://console.adobe.io/integrations)。

1. 在 **[!UICONTROL Adobe I/O Console集成页面的右上角附近]** ，单击新 **[!UICONTROL 建集成]**。
1. 在&#x200B;**[!UICONTROL 创建新集成]**&#x200B;对话框中，确保选中&#x200B;**[!UICONTROL 访问 API]** 单选按钮，然后单击&#x200B;**[!UICONTROL 继续]**。

   ![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. 在第二个&#x200B;**[!UICONTROL 创建新集成]**&#x200B;页面上，启用（打开）**[!UICONTROL Experience Platform Launch API]** 单选按钮。在页面的右下角，单击&#x200B;**[!UICONTROL 继续]**。

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. 在第三个“ **[!UICONTROL 创建新集成]** ”页面上，执行以下操作：

   * 在“名 **[!UICONTROL 称]** ”字段中，输入描述性名称。 例如， *DynamicMediaViewersIO*。

   * 在“说 **[!UICONTROL 明]** ”字段中，输入集成的说明。

   * 在“公 **[!UICONTROL 钥证书]** ”区域，上传您之前在这些步骤中下载的公钥文件(*.crt)。

   * Under the **[!UICONTROL Select a role for Experience Platform Launch API]** heading, select **[!UICONTROL Admin]**.

   * 在“为 **[!UICONTROL Experience Platform Launch API]** ”标题下，选择名为 **[!UICONTROL Launch - &lt;your_公司_name>的产品用户档案]**。
   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. 单击“ **[!UICONTROL 创建集成]**”。
1. 在“集成 **[!UICONTROL 创建”页面上]** ，单击“继 **[!UICONTROL 续”以查看集成详细信息]**。

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. 此时会显示集成详细信息页 **** 面，与以下内容类似：

   >[!NOTE]
   >
   >***保持打开此集成详细信息页面***。稍后您将需要&#x200B;**[!UICONTROL 概述]**&#x200B;和 **[!UICONTROL JWT]** 选项卡中的各种信息。

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)

   集成详细信息页面。

1. 返回之前打开的 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面。在页面的右上角，单击&#x200B;**[!UICONTROL 下一步]**&#x200B;以在 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;窗口中打开&#x200B;**[!UICONTROL 帐户]**&#x200B;页面。

   （如果之前意外关闭了页面，请返回 AEM 作者，然后单击&#x200B;**[!UICONTROL 工具 > 安全 > Adobe IMS 配置]**。单击&#x200B;**[!UICONTROL 创建]**。在&#x200B;**[!UICONTROL 云解决方案]**&#x200B;下拉列表中，选择 **[!UICONTROL Adobe Launch]**。在&#x200B;**[!UICONTROL 证书]**&#x200B;下拉列表中，选择之前创建的证书的名称。）

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)

   “Adobe IMS技术帐户配置——证书”页。

1. “帐 **[!UICONTROL 户]** ”页面有五个字段，这些字段要求您使用上一步“集成详细信息”页面中的信息来填写。

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)

   Adobe IMS技术帐户配置——帐户页。

1. 在“帐 **[!UICONTROL 户]** ”页面上，填写以下字段：

   * **[!UICONTROL 标题]** -输入描述性帐户标题。
   * **[!UICONTROL Authorization Server]** —— 返回到您之前打开的“集成详细信息”页面。 Click the **[!UICONTROL JWT]** tab. 复制不带路径的服务器名称，如下所示。
   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将名称粘贴到相应的字段中。例如，( `https://ims-na1.adobelogin.com/`示例服务器名称仅用于说明目的)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)

   集成详细信息页- JWT选项卡

1. **[!UICONTROL API 密钥]** - 返回到“集成详细信息”页面。单击&#x200B;**[!UICONTROL 概述]**&#x200B;选项卡，然后单击 **[!UICONTROL API 密钥（客户端 ID）]**&#x200B;字段右侧的&#x200B;**[!UICONTROL 复制]**。

   Return to the **[!UICONTROL Account]** page, then paste the key into the respective ****field.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)

   集成详细信息页面。

1. **[!UICONTROL 客户端密钥]** - 返回到“集成详细信息”页面。在&#x200B;**[!UICONTROL 概述]**&#x200B;选项卡中，单击&#x200B;**[!UICONTROL 检索客户端密钥]**。在&#x200B;**[!UICONTROL 客户端密钥]**&#x200B;字段的右侧，单击&#x200B;**[!UICONTROL 复制]**。

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将密钥粘贴到相应的字段中。

1. **[!UICONTROL 有效负荷]** -返回到“集成详细信息”页面。 从 **[!UICONTROL JWT]** 选项卡的JWT有效负荷字段中，复制整个JSON对象代码。

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将代码粘贴到相应的字段中。

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)

   集成详细信息页面- JWT选项卡

   “帐户”页面（已填写所有字段）的外观将类似于以下内容：

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Near the upper-right corner of the **[!UICONTROL Account]** page, click **[!UICONTROL Create]**.

   配置AEM IMS后，您现在有一个新的IMSAccount列在 **[!UICONTROL Adobe IMS配置下]**。

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## 配置Adobe Launch Cloud以进行集成 {#configuring-adobe-launch-cloud-for-the-integration}

1. 在AEM作者中，在左上角附近，单击工具图标（锤子），然后单击 **[!UICONTROL 云服务> Adobe Launch配置]**。

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. 在 **[!UICONTROL Adobe启动配置页面的左侧面板中]** ，选择要为其应用Adobe启动配置的AEM站点。

   仅出于说明目的， **[!UICONTROL 在以下屏幕截图中选择了We.Retail]** Site。

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. 在页面的左上角附近，单击&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建 Adobe Launch 配置]**&#x200B;窗口的&#x200B;**[!UICONTROL 常规]**&#x200B;页面（第 1/3 页）中，填写以下字段：

   * **[!UICONTROL 标题]** -输入描述性配置标题。 For example, `We.Retail Launch cloud configuration`.

   * **[!UICONTROL 关联的Adobe IMS配置]** -选择您之前在配置AEM IMS中创 [建的IMS配置](#configuring-aem-ims)。

   * **[!UICONTROL 公司]** -从 **[!UICONTROL 公司下拉列表]** ，选择您的Experience Cloud公司。 列表会自动填充。

   * **[!UICONTROL 属性]** -从“属性”下拉列表中，选择您之前创建的Adobe Launch属性。 列表会自动填充。
   完成所有字段后，您的“一 **[!UICONTROL 般信息]** ”页面的外观将类似于以下内容：

   ![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. 在左上角附近，单击“下 **[!UICONTROL 一步”]**。
1. 在&#x200B;**[!UICONTROL 创建 Adobe Launch 配置]**&#x200B;窗口的&#x200B;**[!UICONTROL 测试]**&#x200B;页面（第 2/3 页）中，填写以下字段：

   在&#x200B;**[!UICONTROL 库 URI]** 字段中，查看 Adobe Launch 库的测试版本的位置。AEM 会自动填充此字段。

   仅出于说明目的，此步骤将使用部署到Adobe CDN的Adobe Launch库。

   >[!NOTE]
   >
   >检查以确保自动填充的库URI（统一资源标识符）的格式不正确。 如果需要，请修复它，使URI表示协议相对URI。 即它开始于多次正斜杠。
   >
   >
   >For example: `//assets.adobetm.com/launch-xxxx`.

   **[!UICONTROL 测试]**&#x200B;页面应类似于以下内容。请注意，***未***&#x200B;设置异步&#x200B;**[!UICONTROL 存档]**&#x200B;和&#x200B;**[!UICONTROL 加载库]**&#x200B;选项：

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. 在右上角附近，单击“下 **[!UICONTROL 一步”]**。
1. 如有需要，在&#x200B;**[!UICONTROL 创建 Adobe Launch 配置]**&#x200B;窗口的&#x200B;**[!UICONTROL 生产]**&#x200B;页面（第 3/3 页）中，修复自动填充的生产 URI，类似于在上一个&#x200B;**[!UICONTROL 测试]**&#x200B;页面中的操作。
1. 在右上角附近，单击“创 **[!UICONTROL 建”]**。

   您的新Adobe Launch Cloud配置现已创建并列在您的网站旁边，如下例所示：

1. 选择您的新Adobe Launch Cloud配置（选中配置标题后，其左侧会显示一个复选标记）。 在工具栏中，单击“发 **[!UICONTROL 布”]**。

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

目前，AEM作者不支持将Dynamic Media Viewer与Adobe Launch集成。

但是，AEM发布节点中支持该属性。 AEM发布使用Adobe Launch云配置的默认设置，它使用Adobe Launch的生产环境。 因此，在测试过程中，必须每次将Adobe Launch库更新从“开发”推送到“生产”环境。

通过在上述AEM发布的Adobe Launch Cloud配置中指定Adobe Launch库的开发或暂存URL，可以解决此限制。 这样，AEM发布节点就会使用Adobe Launch库的开发或暂存版本。

有关 [设置Adobe Launch Cloud配置的更多信息，请参阅通过Adobe I/O将AEM与Adobe Launch集成](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html) 。
