---
title: 将Dynamic Media Classic功能添加到页面
description: 如何将Dynamic Media Classic功能和组件添加到Adobe Experience Manager中的页面。
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: d947bd98b3a0f6fd79cde5b5b2fca23487077da3
workflow-type: tm+mt
source-wordcount: '2845'
ht-degree: 0%

---

# 将Dynamic Media Classic功能添加到页面 {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) 是一个托管解决方案，用于管理、增强、发布富媒体资产，并将其交付到Web、移动设备、电子邮件和连接Internet的显示和打印设备。

您可以在各种查看器中查看在Dynamic Media Classic中发布的Experience Manager资源：

* 缩放
* 弹出
* 视频
* 图像模板
* 图像

您可以将数字资源直接从Experience Manager发布到Dynamic Media Classic，也可以将数字资源从Dynamic Media Classic发布到Experience Manager。

本文档介绍了如何将Experience Manager中的数字资源发布到Dynamic Media Classic，反之亦然。 此外，还详细介绍了查看器。 有关为Dynamic Media Classic配置Experience Manager的信息，请参阅 [将Dynamic Media Classic与Experience Manager集成](/help/sites-administering/scene7.md).

另请参阅 [添加图像映射](image-maps.md).

有关在Experience Manager中使用视频组件的更多信息，请参阅 [视频](video.md).

>[!NOTE]
>
>如果Dynamic Media Classic资源显示不正确，请确保Dynamic Media [已禁用](config-dynamic.md#disabling-dynamic-media) 然后刷新页面。

## 从Assets手动发布到Dynamic Media Classic {#manually-publishing-to-scene-from-assets}

您可以按如下方式将数字资源发布到Dynamic Media Classic：

* [在Assets控制台的传统用户界面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [在资产的经典用户界面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [在CQ Target文件夹外部的经典用户界面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager以异步方式发布到Dynamic Media Classic。 选择后 **[!UICONTROL Publish]**，您的资源需要几秒钟才能发布到Dynamic Media Classic。

## Dynamic Media Classic组件 {#scene-components}

Experience Manager中提供了以下Dynamic Media Classic组件：

* 缩放
* 弹出（缩放）
* 图像模板
* 图像
* 视频

>[!NOTE]
>
>默认情况下，这些组件不可用，必须从中进行选择 **[!UICONTROL 设计]** 模式。

在中提供这些区段后 **[!UICONTROL 设计]** 在模式中，您可以像添加任何其他Experience Manager组件一样将这些组件添加到页面。 如果位于同步文件夹或页面上，或者使用Dynamic Media Classic云配置，则尚未发布到Dynamic Media Classic的资产将发布到Dynamic Media Classic。

>[!NOTE]
>
>如果您正在创建和开发自定义查看器并使用“内容查找器”，则必须明确添加 `allowfullscreen` 参数。

### Flash 查看器生命周期终止通知 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Dynamic Media Classic停止支持Flash查看器平台。

### 将Dynamic Media Classic (Scene7)组件添加到页面 {#adding-a-scene-component-to-a-page}

将Dynamic Media Classic (Scene7)组件添加到页面与将组件添加到任何页面相同。 以下各节将详细介绍Dynamic Media Classic组件。

**要将Dynamic Media Classic (Scene7)组件添加到页面，请执行以下操作：**

1. 在Experience Manager中，打开要添加 **[!UICONTROL Dynamic Media Classic (Scene7)]** 组件。

1. 如果没有可用的Dynamic Media Classic组件，请选择 **[!UICONTROL 设计]** 模式，选择任何具有蓝色边框的组件，选择 **[!UICONTROL 父级]** 图标，然后 **[!UICONTROL 配置]** 图标。 In **[!UICONTROL Parsys（设计）]**，选择所有Dynamic Media Classic组件以使其可用，然后选择 **[!UICONTROL 确定]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 选择 **[!UICONTROL 编辑]** 以便返回 **[!UICONTROL 编辑]** 模式。

1. 将组件从sidekick中的Dynamic Media Classic组拖动到页面上的所需位置。

1. 选择 **[!UICONTROL 配置]** 图标，以打开组件。

1. 根据需要编辑组件并选择 **[!UICONTROL 确定]** 以保存更改。
1. 将图像或视频从内容浏览器拖动到您添加到页面的Dynamic Media Classic组件上。

   >[!NOTE]
   >
   >仅限触控式UI中，您必须将图像或视频拖放到放到页面上放置的Dynamic Media Classic组件上。 不支持选择和编辑Dynamic Media Classic组件，然后选择资源。

### 向响应式网站添加交互式查看体验 {#adding-interactive-viewing-experiences-to-a-responsive-website}

资产的响应式设计意味着您的资产会根据显示的位置进行调整。 通过响应式设计，可以在多个设备上有效地显示相同的资产。

另请参阅 [网页的响应式设计](/help/sites-developing/responsive.md).

**要将交互式查看体验添加到响应式网站，请执行以下操作：**

1. 登录到Experience Manager，并确保您拥有 [已配置的Adobe Dynamic Media ClassicCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) 并且Dynamic Media Classic组件可用。

   >[!NOTE]
   >
   >如果Dynamic Media Classic组件不可用，请确保 [以通过“设计”模式启用它们](/help/sites-authoring/default-components-designmode.md).

1. 在具有 **[!UICONTROL Dynamic Media Classic]** 组件已启用，请拖动 **[!UICONTROL 图像]** 组件添加到页面。
1. 选择组件并选择配置图标。
1. 在 **[!UICONTROL Dynamic Media Classic设置]** 选项卡，调整断点。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. 确认查看者正在响应式地调整大小，并且所有交互都针对桌面、平板电脑和移动设备进行了优化。

### 所有Dynamic Media Classic组件的通用设置 {#settings-common-to-all-scene-components}

尽管配置选项各不相同，但以下内容对所有用户都是通用的 [!UICONTROL Dynamic Media Classic] 组件：

* **[!UICONTROL 文件引用]**  — 浏览到要引用的文件。 文件引用显示资源URL，但不一定是完整的Dynamic Media Classic URL，包括URL命令和参数。 您无法在此字段中添加Dynamic Media Classic URL命令和参数。 相反，您可以通过组件中的相应功能添加它们。
* **[!UICONTROL 宽度]**  — 用于设置宽度。
* **[!UICONTROL 高度]**  — 用于设置高度。

您可以通过打开（双击）Dynamic Media Classic组件来设置这些配置选项，例如，当您打开 **[!UICONTROL 缩放]** 组件：

![chlimage_1-226](assets/chlimage_1-226.png)

### 缩放 {#zoom}

HTML5缩放组件在您按下 **[!UICONTROL +]** 按钮。

资产底部有缩放工具。 选择 **[!UICONTROL +]** 如果要放大，请选择 **[!UICONTROL -]** 如果你想要减少。 点按 **[!UICONTROL x]** 或者使用重置缩放箭头将图像恢复为导入图像的原始大小。 选择对角线箭头，以便全屏显示。 选择 **[!UICONTROL 编辑]** 以便配置组件。 通过此组件，您可以配置 [所有用户通用的设置 [!UICONTROL Dynamic Media Classic] 组件](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### 弹出 {#flyout}

在HTML中5 **[!UICONTROL 弹出]** 组件时，资源显示为分屏；将资源左移为指定大小；右侧显示缩放部分。 选择 **[!UICONTROL 编辑]** 以便配置组件。 通过此组件，您可以配置 [所有Dynamic Media Classic组件的通用设置](#settings-common-to-all-scene-components).

>[!NOTE]
>
>如果您的 **[!UICONTROL 弹出]** 组件使用自定义大小，然后使用该自定义大小并禁用组件的响应式设置。
>
>如果您的 **[!UICONTROL 弹出]** 组件使用缺省大小，如中所设置 **[!UICONTROL 设计视图]**，然后使用默认大小，组件在启用了组件的响应式设置的情况下展开以适应页面布局大小。 组件的响应式设置存在限制。 当您使用 **[!UICONTROL 弹出]** 组件具有响应式设置，请勿将其用于全页延伸。 否则， **[!UICONTROL 弹出]** 超出页面的右边框。

![chlimage_1-228](assets/chlimage_1-228.png)

### 图像 {#image}

Dynamic Media Classic **[!UICONTROL 图像]** 组件允许您将Dynamic Media Classic功能添加到图像，例如Dynamic Media Classic修饰符、图像或查看器预设，以及锐化。 Dynamic Media Classic **[!UICONTROL 图像]** 组件与Experience Manager中的其他图像组件类似，具有特殊的Dynamic Media Classic功能。 在此示例中，图像具有Dynamic Media Classic URL修饰符， `&op_invert=1` 已应用。

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL 标题，替换文本]**  — 在 **[!UICONTROL 高级]** 选项卡，为图像添加标题，并为已关闭图形的用户添加替换文本。

**[!UICONTROL URL，打开方式]**  — 您可以从设置资产以打开链接。 设置 **[!UICONTROL URL]** 和 **[!UICONTROL 打开方式]** 指明是希望它在同一窗口中打开，还是希望它在新窗口中打开。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 参见 [管理查看器预设](/help/assets/managing-viewer-presets.md). 如果您使用的是图像预设，则无法选择查看器预设，反之亦然。

**[!UICONTROL Dynamic Media Classic配置]**  — 选择要用于从SPS获取活动图像预设的Dynamic Media Classic配置。

**[!UICONTROL 图像预设]**  — 从下拉菜单中选择现有的图像预设。 如果您要查找的图像预设不可见，则必须使其可见。 参见 [管理图像预设](/help/assets/managing-image-presets.md). 如果您使用的是图像预设，则无法选择查看器预设，反之亦然。

**[!UICONTROL 输出格式]**  — 选择图像的输出格式，例如jpeg。 根据您选择的输出格式，还有其他配置选项。 参见 [图像预设最佳实践](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL 锐化]**  — 选择要如何锐化图像。 中详细解释了锐化 [图像预设最佳实践](/help/assets/managing-image-presets.md#image-preset-options) 和 [强化最佳实践](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL URL修饰符]**  — 您可以通过提供其他Dynamic Media Classic图像命令来更改图像效果。 这些命令在 [图像预设](/help/assets/managing-image-presets.md) 和 [命令引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL 断点]**  — 如果您的网站有响应，则需要调整断点。 断点必须以逗号( 、 )分隔。

### 图像模板 {#image-template}

[Dynamic Media Classic图像模板](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) 是导入到Dynamic Media Classic的分层Photoshop内容，其中内容和属性进行了参数化以显示可变性。 此 **[!UICONTROL 图像模板]** 组件允许您导入图像并在Experience Manager中动态更改文本。 此外，您还可以配置 **[!UICONTROL 图像模板]** 组件来使用来自客户端上下文的值，以便每个用户都能以个性化的方式体验图像。

选择 **[!UICONTROL 编辑]** （如果要配置组件）。 您可以配置 [所有Dynamic Media Classic组件的通用设置](#settings-common-to-all-scene-components) 以及本节中描述的其他设置。

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL 文件引用、宽度、高度]**  — 查看所有ScDynamic Media Classicene7组件的通用设置。

>[!NOTE]
>
>Dynamic Media Classic URL命令和参数不能直接添加到文件引用URL。 它们只能在的组件UI中定义 **[!UICONTROL 参数]** 面板。

**[!UICONTROL 标题，替换文本]**  — 在Dynamic Media Classic图像模板选项卡中，为已关闭图形的用户添加图像标题和替换文本。

**[!UICONTROL URL，打开方式]**  — 您可以从设置资产以打开链接。 在的“打开”中设置URL并指示您想要在同一窗口中打开它还是在新窗口中打开。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL 参数面板]**  — 在导入图像时，使用图像中的信息预填充参数。 如果没有可动态更改的内容，则此窗口为空。

![chlimage_1-233](assets/chlimage_1-233.png)

#### 动态更改文本 {#changing-text-dynamically}

要动态更改文本，请在字段中输入新文本并选择 **[!UICONTROL 确定]**. 在此示例中， **[!UICONTROL 价格]** 现在是50美元，运费是99美分。

![chlimage_1-234](assets/chlimage_1-234.png)

图像中的文本会更改。 您可以通过点按将文本重置回原始值 **[!UICONTROL 重置]** 在字段旁边。

![chlimage_1-235](assets/chlimage_1-235.png)

#### 更改文本以反映客户端上下文值的值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

要将字段链接到客户端上下文值，请选择 **[!UICONTROL 选择]** 要打开client-context菜单，请选择客户端上下文，然后选择 **[!UICONTROL 确定]**. 在此示例中，根据将名称与配置文件中的格式化名称之间的链接，名称会发生更改。

![chlimage_1-236](assets/chlimage_1-236.png)

该文本反映当前登录用户的名称。 通过单击，可以将文本重置回原始值 **[!UICONTROL 重置]** 在字段旁边。

![chlimage_1-237](assets/chlimage_1-237.png)

#### 将Dynamic Media Classic图像模板设为一个链接 {#making-the-scene-image-template-a-link}

1. 在具有Dynamic Media Classic的页面上 **[!UICONTROL 图像模板]** 组件，选择 **[!UICONTROL 编辑]**.
1. 在 **[!UICONTROL URL]** 字段中，输入用户点击图像时前往的URL。 在 **[!UICONTROL 打开方式]** 字段，选择是否要打开目标（新窗口或同一窗口）。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 选择 **[!UICONTROL 确定]**.

### 视频组件 {#video-component}

Dynamic Media Classic **[!UICONTROL 视频]** 组件(可从sidekick的Dynamic Media Classic部分获得)使用设备和带宽检测将正确的视频提供给每个屏幕。 此组件是一个HTML5视频播放器；它是一个可用于跨渠道的查看器。

它可用于自适应视频集、单个MP4视频或单个F4V视频。

参见 [视频](s7-video.md) 有关视频如何与Dynamic Media Classic集成配合使用的更多信息。 此外，请参阅 [Dynamic Media Classic视频组件与Foundation视频组件](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### 视频组件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM显示是否上传了主源视频。 它们不显示这些代理资源：

* Dynamic Media Classic编码的演绎版
* Dynamic Media Classic自适应视频集

将自适应视频集与Dynamic Media Classic视频组件结合使用时，必须调整组件大小以适合视频的尺寸。

## Dynamic Media Classic内容浏览器 {#scene-content-browser}

Dynamic Media Classic内容浏览器允许您直接在Experience Manager中查看Dynamic Media Classic中的内容。 要访问内容浏览器，请在 **[!UICONTROL 内容查找器]**，选择 **[!UICONTROL Dynamic Media Classic]** 在触控优化用户界面中或 **[!UICONTROL S7]** 图标。 两个用户界面之间的功能相同。

如果您有多个配置，默认情况下Experience Manager将显示 [默认配置](/help/sites-administering/scene7.md#configuring-a-default-configuration). 您可以直接在Dynamic Media Classic内容浏览器的下拉菜单中选择不同的配置。

>[!NOTE]
>
>* 按需文件夹中的资源不会出现在Dynamic Media Classic内容浏览器中。
>* 时间 [已启用安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)中，Dynamic Media Classic上已发布和未发布的资源都会显示在Dynamic Media Classic内容浏览器中。
>* 如果您没有看到 **[!UICONTROL Dynamic Media Classic]** 或 **[!UICONTROL S7]** 图标作为内容浏览器中的选项，您必须 [配置Dynamic Media Classic以用于Experience Manager](/help/sites-administering/scene7.md).
>* 对于视频，Dynamic Media Classic内容浏览器支持：
   >
   >   * 自适应视频集：包含跨多个屏幕无缝播放所需的所有视频演绎版的容器
   >   * 单个MP4视频
   >   * 单个F4V视频


### 在触屏优化UI中浏览内容 {#browsing-content-in-the-touch-optimized-ui}

您可以在触控优化或经典UI中访问内容浏览器。 目前，触控优化具有以下限制：

* 不支持来自Dynamic Media Classic的FXG和Flash资源。

通过选择浏览Dynamic Media Classic资源 **[!UICONTROL Dynamic Media Classic]** 从第三个下拉菜单中。 如果您尚未配置Dynamic Media Classic/Experience Manager集成，则Dynamic Media Classic不会显示在列表中。

>[!NOTE]
>
>* Dynamic Media Classic内容浏览器加载了大约100个资源，并按名称对它们进行排序。
>* 如果您设置了安全预览服务器，则浏览器会使用该预览服务器渲染缩略图和资产。
>


![chlimage_1-240](assets/chlimage_1-240.png)

此外，您可以将鼠标悬停在浏览器中的资产上，以浏览分辨率信息、大小、修改后的天数以及文件名。

![chlimage_1-241](assets/chlimage_1-241.png)

* 对于自适应视频集和模板，不会为缩略图生成大小信息。
* 对于自适应视频集，不会为缩略图生成分辨率。

### 使用内容浏览器搜索Dynamic Media Classic资源 {#searching-for-scene-assets-with-the-content-browser}

在Dynamic Media Classic中搜索资源与在Experience Manager Assets中搜索资源类似。 但是，当您搜索时，您实际上会看到Dynamic Media Classic系统中资源的远程视图，而不是直接将资源导入Experience Manager。

您可以使用经典UI或触屏优化UI来查看和搜索资产。 根据界面，搜索方式略有不同。

在任一UI中搜索时，您可以按以下条件进行筛选（如触屏优化UI中此处所示）：

**[!UICONTROL 输入关键字]**  — 您可以按名称搜索资源。 搜索时，您输入的关键字是文件名开头的。 例如，键入“swimming”一词会查找任何以相应顺序的字母开头的资产文件名。 在键入搜索词以查找资源后，请务必按Enter键。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL 文件夹/路径]**  — 所显示的文件夹名称基于您选择的配置。 您可以通过点按文件夹图标并选择子文件夹，然后点按复选标记以将其选中来向下钻取到更低级别。

如果输入关键字并选择文件夹，则Experience Manager将搜索该文件夹及其所有子文件夹。 但是，如果在搜索时未输入任何关键字，则选择该文件夹只会显示该文件夹中的资产，而不包括任何子文件夹。

默认情况下，Experience Manager会搜索选定的文件夹和所有子文件夹。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL 资源类型]**  — 选择 **[!UICONTROL Dynamic Media Classic]** 以浏览Dynamic Media Classic内容。 此选项仅在配置Dynamic Media Classic后才可用。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 配置]**  — 如果您在中定义了多个Dynamic Media Classic配置 [!UICONTROL Cloud Services]，您可以在此处选择它。 因此，文件夹会根据您选择的配置进行更改。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL 资源类型]**  — 在Dynamic Media Classic浏览器中，您可以筛选结果以包括以下任一项：图像、模板、视频和自适应视频集。 如果未选择任何资源类型，默认情况下，Experience Manager将搜索所有资源类型。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* 在经典UI中，您还可以搜索 **Flash** 和 **FXG**. 不支持在触屏优化UI中筛选这些类型。
>
>* 搜索视频时，您搜索的是单个演绎版。 结果返回原始演绎版（仅&amp;ast；.mp4）和编码的演绎版。
>* 搜索自适应视频集时，您将搜索文件夹和所有子文件夹，但前提是已向搜索添加了关键词。 如果尚未添加关键字，则Experience Manager不会搜索子文件夹。
>


**[!UICONTROL 发布状态]**  — 您可以根据发布状态筛选资产： **[!UICONTROL 已取消发布]** 或 **[!UICONTROL 已发布]**. 如果您未选择任何 **[!UICONTROL 发布状态]**，默认情况下，Experience Manager会搜索所有发布状态。

![chlimage_1-247](assets/chlimage_1-247.png)
