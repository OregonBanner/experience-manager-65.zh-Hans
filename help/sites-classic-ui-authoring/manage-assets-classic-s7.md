---
title: 将 Scene7 功能添加到您的页面
seo-title: 将 Scene7 功能添加到您的页面
description: Adobe Scene7 是一种托管的解决方案，用于管理和增强丰富的媒体资产，并将其发布和交付到 Web、移动设备、电子邮件及连接 Internet 的显示屏和打印设备。
seo-description: Adobe Scene7 是一种托管的解决方案，用于管理和增强丰富的媒体资产，并将其发布和交付到 Web、移动设备、电子邮件及连接 Internet 的显示屏和打印设备。
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3250'
ht-degree: 62%

---

# 将 Scene7 功能添加到您的页面{#adding-scene-features-to-your-page}

[Adobe Scene7](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) 是一种托管的解决方案，用于管理和增强丰富的媒体资产，并将其发布和交付到 Web、移动设备、电子邮件及连接 Internet 的显示屏和打印设备。

您可以在各种查看器中查看在Scene7中发布的Experience Manager资产：

* 缩放
* 弹出
* 视频
* 图像模板
* 图像

您可以将数字资产从Experience Manager直接发布到Scene7，也可以将数字资产从Scene7发布到Experience Manager。

本文档介绍如何将数字资产从Experience Manager发布到Scene7，反之亦然。 此外，还详细介绍了各种查看器。有关为Scene7配置Experience Manager的信息，请参阅[将Scene7与Experience Manager集成](/help/sites-administering/scene7.md)。

另请参阅[添加图像映射](/help/assets/image-maps.md)。

有关将视频组件与Experience Manager结合使用的更多信息，请参阅以下内容：

* [视频](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>如果Scene7资产显示不正确，请确保Dynamic Media [disabled](/help/assets/config-dynamic.md#disabling-dynamic-media)，然后刷新页面。

## 从资产手动发布到 Scene7 {#manually-publishing-to-scene-from-assets}

您可以从经典 UI 中的“资产”控制台，或直接从资产中将数字资产发布到 Scene7。

>[!NOTE]
>
>Experience Manager会异步发布到Scene7。 单击&#x200B;**发布**&#x200B;后，您的资产可能需要几秒钟时间才能发布到 Scene7。


### 从“资产”控制台发布 {#publishing-from-the-assets-console}

如果资产位于 Scene7 目标文件夹中，要将其从“资产”控制台发布到 Scene7，请执行以下操作：

1. 在Experience Manager经典UI中，单击&#x200B;**数字资产**&#x200B;以访问数字资产管理器。

1. 从目标文件夹中选择要发布到 Scene7 的资产（一个或多个）或文件夹，然后单击鼠标右键并选择&#x200B;**发布到 Scene7**。或者，您也可以从&#x200B;**工具菜单**&#x200B;中选择&#x200B;**发布到Scene7**。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. 转到 Scene7，并确认发布的资产可用。

   >[!NOTE]
   >
   >如果资产没有位于 Scene7 同步文件夹中，则&#x200B;**发布到 Scene7** 选项在上述两个菜单中虽可见，但处于禁用状态。

### 从资产发布  {#publishing-from-an-asset}

当资产位于 Scene7 同步文件夹中时，您可以手动发布资产。

>[!NOTE]
>
>如果资产没有位于 Scene7 同步文件夹中，则不会显示&#x200B;**发布到 Scene7** 链接。

要直接从数字资产发布到 Scene7，请执行以下操作：

1. 在Experience Manager中，单击&#x200B;**数字资产**&#x200B;以访问数字资产管理器。

1. 双击以打开某个资产。

1. 在资产详细信息窗格中，选择&#x200B;**发布到 Scene7**。

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. 该链接随即会变为&#x200B;**正在发布...**，之后又变为&#x200B;**已发布**。转到 Scene7，并确认发布的资产可用。

   >[!NOTE]
   >
   >如果资产未正确发布到 Scene7，则该链接会变为&#x200B;**发布失败**。如果资产已发布到 Scene7，则该链接会显示&#x200B;**重新发布到 Scene7**。重新发布允许您在Experience Manager中对资产进行更改，然后重新发布资产。

### 从 CQ 目标文件夹外部发布资产 {#publishing-assets-from-outside-the-cq-target-folder}

Adobe 建议您只从 Scene7 目标文件夹内部的资产将资产发布到 Scene7。但是，如果您需要从目标文件夹以外的文件夹上传资产，您仍然可以这样做，方法是将资产上传到Scene7上的&#x200B;**ad-hoc**&#x200B;文件夹。

要执行上述操作，您首先需要在要显示资产的页面上配置云配置。然后，将某个 Scene7 组件添加到该页面，并将资产拖放到该组件中。为该页面设置页面属性后，会显示一个&#x200B;**发布到Scene7**&#x200B;链接，选择该链接后，将触发上传到Scene7。

>[!NOTE]
>
>位于临时文件夹中的资产不会在 Scene7 内容浏览器中显示。

要发布位于 CQ 目标文件夹之外的资产，请执行以下操作：

1. 在经典UI的Experience Manager中，单击&#x200B;**网站**，然后导航到要将数字资产添加到但尚未发布到Scene7的网页。 （普通页面继承规则适用。）

1. 在 Sidekick 中，单击&#x200B;**页面**&#x200B;图标，然后单击&#x200B;**页面属性**。

1. 单击&#x200B;**云服务**，单击&#x200B;**添加服务**，然后选择 **Scene7**。
1. 在&#x200B;**Adobe Scene7**&#x200B;下拉列表中，选择所需的配置，然后单击&#x200B;**确定**。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 在网页上，将 Scene7 组件添加到页面上的所需位置。
1. 从内容查找器中，将相应的数字资产拖放到该组件中。您随即会看到&#x200B;**检查 Scene7 发布状态**&#x200B;链接。

   >[!NOTE]
   >
   >如果数字资产位于CQ目标文件夹中，则不会显示指向&#x200B;**检查Scene7发布状态**&#x200B;的链接。 资产只是放置在组件中。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 单击&#x200B;**检查 Scene7 发布状态**。如果资产未发布，Experience Manager会将资产发布到Scene7。 上传后，资产会被放置在临时文件夹中。默认情况下，该临时文件夹位于 **name_of_the_company/CQ5_adhoc**。您可以[根据需要配置此位置](#configuringtheadhocfolder)。

   >[!NOTE]
   >
   >如果资产没有位于 Scene7 同步文件夹中，并且当前页面没有关联的 Scene7 云配置，则上传将会失败。

## Scene7 组件  {#scene-components}

Experience Manager中提供了以下Scene7组件：

* 缩放
* 弹出（缩放）
* 图像模板
* 图像
* 视频

>[!NOTE]
>
>这些组件在默认情况下不可用，需要先在设计模式中选择这些组件才能使用。

在设计模式下使组件可用后，您可以像任何其他Experience Manager组件一样将组件添加到页面。 尚未发布到 Scene7 的资产若满足以下条件便会发布到 Scene7：位于同步文件夹中，或位于具有 Scene7 云配置的页面上。

>[!NOTE]
>
>如果要创建和开发自定义S7查看器，并使用内容查找器，则需要明确添加&#x200B;**allowfullscreen**&#x200B;参数。

### Flash 查看器生命周期终止通知 {#flash-viewers-end-of-life-notice}

自 2017 年 1 月 31 日起，Adobe Scene7 将正式停止对 Flash 查看器平台的支持。

有关此项重大变更的更多信息，请参阅 [Flash 查看器生命周期终止常见问题解答](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html)。

### 将 Scene7 组件添加到页面  {#adding-a-scene-component-to-a-page}

将 Scene7 组件添加到页面的过程与将任何其他组件添加到页面相同。以下部分详细介绍了 Scene7 组件。

在经典 UI 中，要将 Scene7 组件/查看器添加到页面，请执行以下操作：

1. 在Experience Manager中，打开要添加Scene7组件的页面。

1. 如果没有可用的 Scene7 组件，请单击 Sidekick 中的标尺图标以进入&#x200B;**设计**&#x200B;模式，单击&#x200B;**编辑** parsys，然后选择所有 **Scene7** 组件，以使其变为可用。

1. 通过单击Sidekick中的铅笔，返回到&#x200B;**编辑**&#x200B;模式。

1. 将某个组件从 Sidekick 中的 **Scene7** 组拖放到页面上的所需位置。

1. 单击&#x200B;**编辑**&#x200B;以打开该组件。

1. 根据需要编辑该组件，然后单击&#x200B;**确定**&#x200B;以保存更改。

### 在响应式网站中添加交互式查看体验  {#adding-interactive-viewing-experiences-to-a-responsive-website}

如果您的资产具有响应式设计，则意味着您的资产会根据其显示的位置自行进行调整。利用响应式设计，可以在多种设备上有效地显示同一资产。

在经典 UI 中，要在响应式网站中添加交互式查看体验，请执行以下操作：

1. 登录Experience Manager，并确保已配置[的Adobe Scene7Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration)，并且Scene7组件可用。

   >[!NOTE]
   >
   >如果Scene7 WCM组件不可用，请确保通过设计模式启用它们。

1. 在启用了 Scene7 组件的网站上，将&#x200B;**图像**&#x200B;查看器拖放到页面。
1. 编辑该组件，并在 **Scene7 设置**&#x200B;选项卡中调整断点。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 确认查看器可实现响应式大小调整，并且所有交互已针对台式机、平板电脑和移动设备进行了优化。

### 所有 Scene7 组件的通用设置  {#settings-common-to-all-scene-components}

虽然配置选项各有不同，但以下设置在所有 Scene7 组件中是通用的：

* **文件引用** - 浏览到要引用的文件。文件引用会显示资产 URL，但显示的不一定是包括 URL 命令和参数的完整 Scene7 URL。您无法在此字段中添加 Scene7 URL 命令和参数。必须使用组件中的相应功能才能添加这些命令和参数。
* **宽度** - 允许您设置宽度。
* **高度** - 允许您设置高度。

打开（双击）某个 Scene7 组件（例如打开&#x200B;**缩放**&#x200B;组件），即可设置这些配置选项：

![chlimage_1-52](assets/chlimage_1-52.png)

### 缩放 {#zoom}

按下 + 按钮时，HTML5 缩放组件会显示放大的图像。

缩放工具位于资产底部。单击 **+** 可放大。单击 **-** 可缩小。单击&#x200B;**x**&#x200B;或重置缩放箭头可将图像恢复为导入时的原始大小。 单击对角线可进入全屏模式。单击&#x200B;**编辑**&#x200B;可配置该组件。使用此组件，可以配置所有Scene7组件通用的[设置](#settings-common-to-all-scene-components)。

![](do-not-localize/chlimage_1-3.png)

### 弹出 {#flyout}

在 HTML5 弹出组件中，资产会分屏显示；左侧屏幕以指定大小显示资产；右侧屏幕则显示缩放部分。单击&#x200B;**编辑**&#x200B;可配置该组件。使用此组件，可以配置所有Scene7组件通用的[设置](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>如果弹出组件使用自定义大小，则系统会使用该自定义大小，并禁用该组件的响应设置。
>
>如果您的弹出组件使用在设计视图中设置的默认大小，则会使用默认大小，该组件会在启用组件响应设置的情况下拉伸以适应页面布局大小。 但是，请注意，组件的响应设置存在限制。 在弹出组件中使用响应设置时，您不应该将弹出组件延伸到整个页面。否则，弹出窗口可能会超出页面的右边框。

![chlimage_1-53](assets/chlimage_1-53.png)

### 图像 {#image}

通过 Scene7 图像组件，您可以在图像中添加 Scene7 功能，包括 Scene7 修饰符、图像预设或查看器预设，以及锐化功能。Scene7图像组件与Experience Manager中具有特殊Scene7功能的其他图像组件类似。 在此示例中，图像应用了Scene7 URL修饰符&#x200B;**&amp;op_invert=1**。

![](do-not-localize/chlimage_1-4.png)

**标题替换文** 本在高级选项卡中，为图像添加标题，为关闭图形的用户添加替换文本。

**URL，打开** 您可以设置资产来打开链接。设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

![chlimage_1-54](assets/chlimage_1-54.png)

**查看** 器预设从下拉菜单中选择一个现有的查看器预设。如果未显示您要查找的查看器预设，则可能需要将其显示出来。请参阅管理查看器预设。如果您正在使用图像预设，则无法选择查看器预设，反之亦然。

**Scene7** 配置选择要从SPS中获取活动图像预设的Scene7配置。

**图像** 预设从下拉菜单中选择一个现有的图像预设。如果未显示您要查找的图像预设，则可能需要将其显示出来。请参阅管理图像预设。如果您正在使用图像预设，则无法选择查看器预设，反之亦然。

**输出** 格式选择图像的输出格式，例如jpeg。根据所选的输出格式，您可能会有额外的配置选项。请参阅图像预设最佳实践。

**** 锐化选择要锐化图像的方式。图像预设最佳实践和锐化最佳实践中详细介绍了锐化。

**URL修** 饰符您可以通过提供其他S7图像命令来更改图像效果。相关内容在图像预设和命令参考中进行了介绍。

**** 断点如果您的网站是响应式的，您需要调整断点。断点之间必须使用逗号 (,) 分隔。

### 图像模板 {#image-template}

[Scene7 图像模板](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html)是已导入到 Scene7 的 Photoshop 分层内容，该组件中的内容和属性已进行参数化，以便提供可变性。**图像模板**&#x200B;组件允许您导入图像并在Experience Manager中动态更改文本。 此外，您还可以配置&#x200B;**图像模板**&#x200B;组件，以使用 Client Context 中的值，从而让每个客户获取个性化的图像体验。

单击&#x200B;**编辑**&#x200B;可配置该组件。您可以配置所有Scene7组件通用的[设置](/help/sites-administering/scene7.md#settingscommontoallscene7components)以及此部分中描述的其他设置。

![chlimage_1-55](assets/chlimage_1-55.png)

**文件引用、宽度、高** 度请参阅所有Scene7组件通用的设置。

>[!NOTE]
>
>无法将 Scene7 URL 命令和参数直接添加到文件引用 URL。只能在组件 UI 的&#x200B;**参数**&#x200B;面板中定义这些命令和参数。

**标题、替** 换文本在Scene7图像模板选项卡中，为图像添加标题，为关闭图形的用户添加替换文本。

**URL，打开** 您可以设置资产来打开链接。设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

![chlimage_1-56](assets/chlimage_1-56.png)

**参** 数面板导入图像时，参数会预填充图像中的信息。如果没有可以动态更改的内容，则此窗口将是空的。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 动态更改文本 {#changing-text-dynamically}

要动态更改文本，请在字段中输入新文本，然后单击&#x200B;**确定**。在此示例中，**价格**&#x200B;现在为 50 美元，运费为 99 美分。

![chlimage_1-58](assets/chlimage_1-58.png)

图像中的文本发生了更改。您可以通过单击相应字段旁边的&#x200B;**重置**，将文本重置为原始值。

![chlimage_1-59](assets/chlimage_1-59.png)

#### 更改文本以反映 Client Context 值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

要将字段链接到客户端上下文值，请单击&#x200B;**选择**&#x200B;以打开客户端上下文菜单，选择客户端上下文，然后单击&#x200B;**确定**。 在此示例中，由于已将名称与个人资料中设置的格式化名称链接在一起，因此名称会相应地发生更改。

![chlimage_1-60](assets/chlimage_1-60.png)

文本反映了当前已登录用户的名称。您可以通过单击相应字段旁边的&#x200B;**重置**，将文本重置为原始值。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 将 Scene7 图像模板设为链接 {#making-the-scene-image-template-a-link}

要将 Scene7 图像模板组件设为可单击的链接，请执行以下操作：

1. 在具有 Scene7 图像模板组件的页面上，单击&#x200B;**编辑**。
1. 在 **URL** 字段中，输入用户单击图像后所转到的 URL。在&#x200B;**打开方式**&#x200B;字段中，选择您希望在新窗口中还是在同一窗口中打开目标。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 单击&#x200B;**确定**。

### 视频组件  {#video-component}

Scene7 **视频**&#x200B;组件(可从Sidekick的Scene7部分获取)使用设备和带宽检测为每个屏幕提供正确的视频。 此组件是一种 HTML5 视频播放器，它是可以跨渠道使用的单一查看器。

它可用于自适应视频集、单个MP4视频或单个F4V视频。

有关视频在 Scene7 集成中的运行方式的更多信息，请参阅[视频](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)。此外，请参阅 [**Scene7 视频**&#x200B;组件与基础&#x200B;**视频**&#x200B;组件的对比](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)。

![chlimage_1-63](assets/chlimage_1-63.png)

### 视频组件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM显示是否上传了主源视频。 但它们不会显示以下代理资产：

* Scene7 编码视频呈现
* Scene7 自适应视频集

将自适应视频集与 Scene7 视频组件结合使用时，需要调整此组件的大小，以使其适应视频的大小。

## Scene7 内容浏览器 {#scene-content-browser}

通过Scene7内容浏览器，您可以直接在Experience Manager中查看Scene7中的内容。 要访问内容浏览器，请在内容查找器中，选择触屏优化用户界面中的&#x200B;**Scene7**&#x200B;或经典用户界面中的&#x200B;**S7**&#x200B;图标。 这两种用户界面的功能是相同的。

如果您有多个配置，则默认情况下Experience Manager会显示[默认配置](/help/sites-administering/scene7.md#configuring-a-default-configuration)。 您可以直接在 Scene7 内容浏览器的下拉菜单中选择不同的配置。

>[!NOTE]
>
>* 位于临时文件夹中的资产不会在 Scene7 内容浏览器中显示。
>* [启用安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)后，在 Scene7 中已发布和已取消发布的资产都会在 Scene7 内容浏览器中显示。
>* 如果在内容浏览器中未看到&#x200B;**Scene7**&#x200B;或&#x200B;**S7**&#x200B;图标作为选项，则需要[配置Scene7以使用Experience Manager](/help/sites-administering/scene7.md)。
>* Scene7 内容浏览器支持以下视频：
   >   * 自适应视频集：一种容器，包含在多种屏幕上实现无缝播放所需的所有视频呈现
   >   * 单个 MP4 视频
   >   * 单个F4V视频


### 浏览内容{#browsing-content-in-the-classic-ui}

单击 **S7** 选项卡，可浏览 Scene7 中的内容。

通过选择配置，您可以更改所访问的配置。文件夹会根据您选择的配置相应地进行更改。

![chlimage_1-64](assets/chlimage_1-64.png)

与资产的内容查找器一样，您也可以搜索资产并筛选结果。但是，与资产查找器不同的是，在 **S7** 选项卡中输入关键字时，文件名是以您输入的字符串&#x200B;**开头**，而不是将关键字&#x200B;**包含**&#x200B;在文件名中。

默认情况下，资产会按文件名显示。您也可以按资产类型筛选结果。

>[!NOTE]
>
>WCM 的 Scene7 内容浏览器支持以下视频：
>
>* 自适应视频集：一种容器，包含在多种屏幕上实现无缝播放所需的所有视频呈现
>* 单个 MP4 视频
>* 单个F4V视频

>



### 使用内容浏览器搜索 Scene7 资产 {#searching-for-scene-assets-with-the-content-browser}

搜索Scene7资产与搜索Experience Manager资产类似，不同之处在于，在搜索资产时，您实际上会在Scene7系统中看到资产的远程视图，而不是直接将资产导入Experience Manager。

您可以使用经典 UI 或触屏优化 UI 来查看和搜索资产。根据所用的界面，搜索方式会略有不同。

在任一 UI 中进行搜索时，您都可以按以下条件进行筛选（此处显示的是触屏优化 UI）：

**输入** 关键词您可以按名称搜索资产。搜索时，您输入的关键字是文件名称的开头。例如，键入“swimming”一词后，将在该文件夹中查找任何以这些字母开头的资产文件名。键入搜索词后，请务必单击 Enter，这样才能查找资产。

![chlimage_1-65](assets/chlimage_1-65.png)

**文件夹/** 路径显示的文件夹名称基于您选择的配置。您可以向下选择更低级别的文件夹，方法是单击文件夹图标并选择一个子文件夹，然后单击复选标记以将其选中。

如果输入关键字并选择文件夹，则Experience Manager会搜索该文件夹和任何子文件夹。 但是，如果您在搜索时未输入任何关键字，则选择文件夹后，只会显示此文件夹中的资产，而不会包括所有子文件夹。

默认情况下，Experience Manager会搜索选定的文件夹和所有子文件夹。

![chlimage_1-66](assets/chlimage_1-66.png)

**资产类** 型选择Scene7可浏览Scene7内容。仅当配置了 Scene7 时，此选项才可用。

![chlimage_1-67](assets/chlimage_1-67.png)

**** 配置如果您在Cloud Services中定义了多个Scene7配置，则可以在此处选择该配置。根据您选择的配置，文件夹会相应地进行更改。

![chlimage_1-68](assets/chlimage_1-68.png)

**资产** 类型在Scene7浏览器中，您可以筛选结果以包含以下任一项：图像、模板、视频和自适应视频集。如果您未选择任何资产类型，则默认情况下，Experience Manager会搜索所有资产类型。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* 在经典 UI 中，您还可以搜索 **Flash** 和 **FXG**。在触屏优化 UI 中，当前并不支持筛选这两项。
   >
   >
* 搜索视频时，您搜索的是单个视频呈现。结果会返回原始视频呈现（仅限 *.mp4）以及编码视频呈现。
* 在搜索自适应视频集时，您正在搜索文件夹和所有子文件夹，但前提是您向搜索添加了关键字。 如果您未添加关键词，则Experience Manager不会搜索子文件夹。



**发布** 状态您可以根据发布状态筛选资产：已取消发布或已发布。如果未选择任何发布状态，则默认情况下，Experience Manager会搜索所有发布状态。

![chlimage_1-70](assets/chlimage_1-70.png)
