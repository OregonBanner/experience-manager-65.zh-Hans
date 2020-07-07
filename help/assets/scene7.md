---
title: 将Dynamic Media经典功能添加到页面
description: 了解如何将Dynamic Media经典功能和组件添加到AEM页面。
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '2862'
ht-degree: 25%

---


# 将Dynamic Media经典功能添加到页面 {#adding-scene-features-to-your-page}

[AdobeDynamic MediaClassic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) 是一款托管解决方案，用于管理、增强、发布富媒体资产并将富媒体资产交付到Web、移动、电子邮件以及连接Internet的显示屏和印刷品。

您可以在各种查看器中视图发布在Dynamic Media经典中的AEM资产：

* 缩放
* 弹出
* 视频
* 图像模板
* 图像

您可以将数字资产从AEM直接发布到Dynamic Media经典，也可以将数字资产从Dynamic Media经典发布到AEM。

本文档介绍如何将数字资产从AEM发布到Dynamic Media经典，反之亦然。 此外，还详细介绍了各种查看器。有关为Dynamic Media经典配置AEM的信息，请参 [阅将Dynamic Media经典与AEM集成](/help/sites-administering/scene7.md)。

另请参阅[添加图像映射](image-maps.md)。

For more information on using video components with AEM, see [Video](video.md).

>[!NOTE]
>
>If Dynamic Media Classic assets do not display properly, make sure that Dynamic media is [disabled](config-dynamic.md#disabling-dynamic-media) and then refresh the page.

## 从资产手动发布到Dynamic Media经典 {#manually-publishing-to-scene-from-assets}

您可以按如下方式将数字资产发布到Dynamic Media经典：

* [在经典用户界面中，从“资产”控制台访问](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [在资产的经典用户界面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [在经典用户界面中，从外部CQ目标文件夹](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEM异步发布到Dynamic Media经典。 After you click **[!UICONTROL Publish]**, it may take several seconds for your asset to publish to Dynamic Media Classic.


## Dynamic Media经典组件 {#scene-components}

AEM中提供以下Dynamic Media经典组件：

* 缩放
* 弹出（缩放）
* 图像模板
* 图像
* 视频

>[!NOTE]
>
>These components are not available by default and need to be selected in **[!UICONTROL Design]** mode before using.

After they are made available in **[!UICONTROL Design]** mode, you can add the components to your page like any other AEM component. 尚未发布到Dynamic Media经典的资产会发布到Dynamic Media经典(如果位于同步文件夹中、页面上或具有Dynamic Media经典云配置)。

>[!NOTE]
>
>If you are creating and developing custom viewers and using the Content Finder, you need to explicity add the **[!UICONTROL allowfullscreen]** parameter.

### Flash 查看器生命周期终止通知 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，AdobeDynamic Media经典终止了对Flash查看器平台的支持。

有关此项重大变更的更多信息，请参阅 [Flash 查看器生命周期终止常见问题解答](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html)。

### Adding a Dynamic Media Classic component (Scene7) to a page {#adding-a-scene-component-to-a-page}

向页面添加Dynamic Media经典(Scene7)组件与向任何页面添加组件相同。 Dynamic Media经典组件在以下各节中有详细介绍。

**向页面添加Dynamic Media经典(Scene7)组件**

1. 在AEM中，打开要添加Dynamic Media经典(Scene7)组件的页面。

1. 如果没有Dynamic Media经典组件可用，请单 **[!UICONTROL 击]** “设计”模式，点按带有蓝色边框的任何组件，点按父项 **[!UICONTROL 图标]** ，然后点按 **[!UICONTROL 配置图标]** 。 在 **[!UICONTROL Parsys(Design)中]**，选择所有Dynamic Media经典组件以使其可用，然后单击 **[!UICONTROL 确定。]**

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 单击 **[!UICONTROL 编辑]** ，以返回 **[!UICONTROL 编辑模]** 式。

1. 将组件从Sidekick中的Dynamic Media经典组拖动到页面的所需位置。

1. Click the **[!UICONTROL Configuration]** icon to open the component.

1. 根据需要编辑该组件，然后单击&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。
1. 将图像或视频从内容浏览器拖到您添加到页面的Dynamic Media经典组件上。

   >[!NOTE]
   >
   >仅在触屏UI中，必须将图像或视频拖放到您放置在页面上的Dynamic Media经典组件上。 不支持选择和编辑Dynamic Media经典组件，然后选择资产。

### Adding interactive viewing experiences to a responsive site {#adding-interactive-viewing-experiences-to-a-responsive-website}

如果您的资产具有响应式设计，则意味着您的资产会根据其显示的位置自行进行调整。利用响应式设计，可以在多种设备上有效地显示同一资产。

另请参阅 [网页响应式设计](/help/sites-developing/responsive.md)。

**向响应式网站添加交互式查看体验**

1. Log in to AEM, and ensure that you have [configured Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) and that Dynamic Media Classic components are available.

   >[!NOTE]
   >
   >如果Dynamic Media经典组件不可用，请 [确保通过设计模式启用它们](/help/sites-authoring/default-components-designmode.md)。

1. In a website with the **[!UICONTROL Dynamic Media Classic]** components enabled, drag an **[!UICONTROL Image]** component to the page.
1. 选择组件，然后点按配置图标。
1. 在“Dynamic Media **[!UICONTROL 经典设置]** ”选项卡中，调整断点。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. 确认查看器可实现响应式大小调整，并且所有交互已针对台式机、平板电脑和移动设备进行了优化。

### 所有Dynamic Media经典组件的通用设置 {#settings-common-to-all-scene-components}

Although configuration options vary, the following are common to all [!UICONTROL Dynamic Media Classic] components:

* **[!UICONTROL 文件引用]** -浏览到要引用的文件。 文件引用显示资产URL，但不一定是完整的Dynamic Media经典URL（包括URL命令和参数）。 不能在此字段中添加Dynamic Media经典URL命令和参数。 必须使用组件中的相应功能才能添加这些命令和参数。
* **[!UICONTROL 宽度]** -允许您设置宽度。
* **[!UICONTROL 高度]** -允许您设置高度。

You set these configuration options by opening (double-clicking) a Dynamic Media Classic component, for example, when you open a **[!UICONTROL Zoom]** component:

![chlimage_1-226](assets/chlimage_1-226.png)

### 缩放 {#zoom}

The HTML5 Zoom component displays a larger image when you press the **[!UICONTROL +]** button.

缩放工具位于资产底部。点 **[!UICONTROL 击]** +放大。 点 **[!UICONTROL 击]** 可减少。 Tapping the **[!UICONTROL x]** or the reset zoom arrow brings the image back to the original size it was imported as. 点按对角箭头，使其全屏显示。 Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all [!UICONTROL Dynamic Media Classic] components](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### 弹出 {#flyout}

In the HTML5 **[!UICONTROL Flyout]** component, the asset is shown as split screen; left the asset in the specified size; right the zoom portion is displayed. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components).

>[!NOTE]
>
>If your **[!UICONTROL Flyout]** component uses a custom size, then that custom size is used and responsive setup of the component is disabled.
>
>If your **[!UICONTROL Flyout]** component uses the default size, as set in the **[!UICONTROL Design View]**, then the default size is used and the component stretches to accomodate the page layout size with responsive setup of the component enabled. 但是，请注意，组件的响应式设置存在限制。 When the you use the **[!UICONTROL Flyout]** component with responsive setup, you should not use it with full page stretch. Otherwise, the **[!UICONTROL Flyout]** may extend beyond the page&#39;s right border.

![chlimage_1-228](assets/chlimage_1-228.png)

### 图像 {#image}

Dynamic Media经 **[!UICONTROL 典图像]** 组件允许您向图像添加Dynamic Media经典功能，如Dynamic Media经典修饰符、图像预设或查看器预设，以及锐化。 Dynamic Media经 **[!UICONTROL 典图像]** 组件与AEM中具有特殊Dynamic Media经典功能的其他图像组件类似。 在此示例中，图像应用了Dynamic Media经典URL修饰 `&op_invert=1` 符。

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL 标题、替代文本]** -在高级 **[!UICONTROL 选项卡中]** ，为图像添加一个标题，并为关闭图形的用户添加替代文本。

**[!UICONTROL URL，打开方式]** -您可以设置资产以打开链接。 设置 **[!UICONTROL URL]**，并在&#x200B;**[!UICONTROL 打开方式]**&#x200B;中指示是要在同一窗口中还是在新窗口中打开该 URL。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL 查看器预设]** -从下拉菜单中选择现有的查看器预设。 如果未显示您要查找的查看器预设，则可能需要将其显示出来。请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。如果您正在使用图像预设，则无法选择查看器预设，反之亦然。

**[!UICONTROL Dynamic Media经典配置]** -选择要从SPS中提取活动图像预设的Dynamic Media经典配置。

**[!UICONTROL 图像预设]** -从下拉菜单中选择现有的图像预设。 如果未显示您要查找的图像预设，则可能需要将其显示出来。请参阅[管理图像预设](/help/assets/managing-image-presets.md)。如果您正在使用图像预设，则无法选择查看器预设，反之亦然。

**[!UICONTROL 输出格式]** -选择图像的输出格式，例如jpeg。 根据所选的输出格式，您可能会有额外的配置选项。请参阅[图像预设最佳实践](/help/assets/managing-image-presets.md#image-preset-options)。

**[!UICONTROL 锐化]** -选择要如何锐化图像。 [图像预设最佳实践](/help/assets/managing-image-presets.md#image-preset-options)和[锐化最佳实践](/help/assets/assets/s7_sharpening_images.pdf)中详细介绍了锐化。

**[!UICONTROL URL修饰符]** -您可以通过提供其他Dynamic Media经典图像命令来更改图像效果。 相关内容在[图像预设](/help/assets/managing-image-presets.md)和[命令参考](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)中进行了介绍。

**[!UICONTROL 断点]** -如果您的网站是响应式的，您需要调整断点。 断点之间必须使用逗号 (,) 分隔。

### 图像模板 {#image-template}

[Dynamic Media经典图像模板](https://docs.adobe.com/help/en/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) 是已导入到Dynamic Media经典的分层Photoshop内容，其中内容和属性经过参数化以实现可变性。 通过&#x200B;**[!UICONTROL 图像模板]**&#x200B;组件，您可以在 AEM 中导入图像并对文本进行动态更改。此外，您还可以配置&#x200B;**[!UICONTROL 图像模板]**&#x200B;组件，以使用 Client Context 中的值，从而让每个客户获取个性化的图像体验。

Tap **[!UICONTROL Edit]** to configure the component. You can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components) as well as other settings described in this section.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL 文件引用、宽度]** 、高度——查看所有ScDynamic Media Classicene7组件的常用设置。

>[!NOTE]
>
>Dynamic Media经典URL命令和参数不能直接添加到文件引用URL。 只能在组件 UI 的&#x200B;**[!UICONTROL 参数]**&#x200B;面板中定义这些命令和参数。

**[!UICONTROL 标题、替代文本]** -在Dynamic Media经典图像模板选项卡中，为图像添加一个标题，并为关闭了图形的用户添加替代文本。

**[!UICONTROL URL，打开方式]** -您可以设置资产以打开链接。 设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL 参数面板]** -导入图像时，参数会预填充图像中的信息。 如果没有可以动态更改的内容，则此窗口将是空的。

![chlimage_1-233](assets/chlimage_1-233.png)

#### 动态更改文本 {#changing-text-dynamically}

要动态更改文本，请在字段中输入新文本，然后单击&#x200B;**[!UICONTROL 确定。]**&#x200B;在此示例中，**[!UICONTROL 价格]**&#x200B;现在为 50 美元，运费为 99 美分。

![chlimage_1-234](assets/chlimage_1-234.png)

图像中的文本发生了更改。You can reset the text back to the original value by tapping **[!UICONTROL Reset]** next to the field.

![chlimage_1-235](assets/chlimage_1-235.png)

#### 更改文本以反映 Client Context 值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

To link a field to a client context value, tap **[!UICONTROL Select]** to open the client-context menu, select the client context, and tap **[!UICONTROL OK.]**&#x200B;在此示例中，由于已将名称与个人资料中设置的格式化名称链接在一起，因此名称会相应地发生更改。

![chlimage_1-236](assets/chlimage_1-236.png)

文本反映了当前已登录用户的名称。您可以通过单击相应字段旁边的&#x200B;**[!UICONTROL 重置]**，将文本重置为原始值。

![chlimage_1-237](assets/chlimage_1-237.png)

#### 使Dynamic Media经典图像模板成为链接 {#making-the-scene-image-template-a-link}

1. 在具有Dynamic Media经典图像模板 **[!UICONTROL 组件的页面]** ，点按 **[!UICONTROL 编辑。]**
1. In the **[!UICONTROL URL]** field, enter the URL that users go to when the image is tapped. In the **[!UICONTROL Open in]** field, select whether you want the target to open (a new window or same window).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 点按 **[!UICONTROL 确定。]**

### 视频组件 {#video-component}

The Dynamic Media Classic **[!UICONTROL Video]** component (available from the Dynamic Media Classic section of the sidekick) uses device and bandwidth detection to serve the right video to each screen. 此组件是一种 HTML5 视频播放器，它是可以跨渠道使用的单一查看器。

它可用于自适应视频集、单个MP4视频或单个F4V视频。

See [Video](s7-video.md) for more information on how videos work with Dynamic Media Classic integration. 此外，请参 [阅Dynamic Media经典视频组件与基础视频组件](s7-video.md)。

![chlimage_1-239](assets/chlimage_1-239.png)

### 视频组件的已知限制 {#known-limitations-for-the-video-component}

Adobe DAM和WCM显示是否上传了主源视频。 但它们不会显示以下代理资产：

* Dynamic Media经典编码再现
* Dynamic Media经典自适应视频集

在将自适应视频集与Dynamic Media经典视频组件一起使用时，您需要调整组件大小以适合视频的尺寸。

## Dynamic Media经典内容浏览器 {#scene-content-browser}

通过Dynamic Media经典内容浏览器，您可以直接在AEM中从Dynamic Media经典视图内容。 To access the content browser, in the **[!UICONTROL Content Finder]**, select **[!UICONTROL Dynamic Media Classic]** in the touch-optimized user interface or the **[!UICONTROL S7]** icon in the classic user interface. 这两种用户界面的功能是相同的。

如果您有多个配置，默认情况下，AEM 会显示[默认配置](/help/sites-administering/scene7.md#configuring-a-default-configuration)。您可以直接在Dynamic Media经典内容浏览器中的下拉菜单中选择不同的配置。

>[!NOTE]
>
>* 位于临时文件夹中的资产不会显示在Dynamic Media经典内容浏览器中。
>* 启用 [安全预览后](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene),Dynamic Media经典上已发布和取消发布的资产都会显示在Dynamic Media经典内容浏览器中。
>* If you do not see **[!UICONTROL Dynamic Media Classic]** or the **[!UICONTROL S7]** icon as an option in the content browser, you need to [configure Dynamic Media Classic to work with AEM](/help/sites-administering/scene7.md).
>* 对于视频，Dynamic Media经典内容浏览器支持：

   >
   >   
   * 自适应视频集：一种容器，包含在多种屏幕上实现无缝播放所需的所有视频呈现
   >   * 单个MP4视频
   >   * 单个F4V视频


### Browsing content in the touch-optimized UI {#browsing-content-in-the-touch-optimized-ui}

您可以在触屏优化UI或经典UI中访问内容浏览器。 目前，触屏优化具有以下限制：

* 不支持Dynamic Media经典中的FXG和Flash资源。

通过从第三个下拉菜单中选择 **[!UICONTROL Dynamic Media经典]** ，浏览Dynamic Media经典资产。 Dynamic Media经典不会显示在列表中(如果尚未配置Dynamic Media经典/AEM集成)。

>[!NOTE]
>
>* Dynamic Media经典内容浏览器加载约100个资源，并按名称对其进行排序。
>* 如果您设置了安全预览服务器，浏览器将使用该预览服务器来呈现缩略图和资产。

>



![chlimage_1-240](assets/chlimage_1-240.png)

此外，您还可以通过将鼠标悬停在浏览器中的资产上，浏览分辨率信息、大小、修改后的天数以及文件名。

![chlimage_1-241](assets/chlimage_1-241.png)

* 对于自适应视频集和模板，不会为缩略图生成大小信息。
* 对于自适应视频集，不会为缩略图生成分辨率。

### 使用内容浏览器搜索Dynamic Media经典资产 {#searching-for-scene-assets-with-the-content-browser}

搜索Dynamic Media经典资产与搜索AEM资产类似，但搜索时您实际看到的是Dynamic Media经典系统中资产的远程视图，而不是直接将其导入AEM。

您可以使用经典 UI 或触屏优化 UI 来查看和搜索资产。根据所用的界面，搜索方式会略有不同。

在任一 UI 中进行搜索时，您都可以按以下条件进行筛选（此处显示的是触屏优化 UI）：

**[!UICONTROL 输入关键字]** -您可以按名称搜索资产。 搜索时，您输入的关键字是文件名称的开头。例如，键入“swimming”一词后，将在该文件夹中查找任何以这些字母开头的资产文件名。键入词后，请务必点按Enter以查找资产。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL 文件夹／路径]** -显示的文件夹名称基于您选择的配置。 您可以通过点按文件夹图标并选择子文件夹，然后点按复选标记以选择它，向下展开到更低级别。

如果您输入了关键字并选择了文件夹，则 AEM 会搜索此文件夹及其所有子文件夹。但是，如果您在搜索时未输入任何关键字，则选择文件夹后，只会显示此文件夹中的资产，而不会包括所有子文件夹。

默认情况下，AEM 会搜索选中的文件夹及其所有子文件夹。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL 资产类型]** -选择 **[!UICONTROL Dynamic Media经典]** ，浏览Dynamic Media经典内容。 仅当配置了Dynamic Media经典时，此选项才可用。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 配置]** -如果在Dynamic Media中定义了多个Cloud Service经典 [!UICONTROL 配置]，则可以在此处选择它。 根据您选择的配置，文件夹会相应地进行更改。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL 资产类型]** -在Dynamic Media经典浏览器中，您可以筛选结果以包含以下任一内容： 图像、模板、视频和自适应视频集。 如果您没有选择任何资产类型，则默认情况下，AEM 会搜索所有资产类型。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* 在经典 UI 中，您还可以搜索 **Flash** 和 **FXG**。在触屏优化 UI 中，当前并不支持筛选这两项。
   >
   >
* 搜索视频时，您搜索的是单个视频呈现。结果返回原始再现（仅&amp;ast;.mp4）和编码再现。
>* 搜索自适应视频集时，您正在搜索文件夹和所有子文件夹，但前提是您已向搜索添加了关键字。 如果您没有添加关键字，则 AEM 不会搜索子文件夹。

>



**[!UICONTROL 发布状态]** -您可以根据发布状态筛选资产： **[!UICONTROL 已取消发布]** 或已 **[!UICONTROL 发布。]** 如果未选择任何发布 **[!UICONTROL 状态]**，则默认情况下，AEM会搜索所有发布状态。

![chlimage_1-247](assets/chlimage_1-247.png)

