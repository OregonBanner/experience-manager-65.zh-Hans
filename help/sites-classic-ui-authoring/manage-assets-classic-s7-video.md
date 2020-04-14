---
title: 视频
seo-title: 视频
description: Assets 提供了集中式视频资产管理功能，您可以将视频直接上传到 Assets 以自动编码为 Scene7，并直接从 Assets 访问 Scene7 视频以进行页面创作。
seo-description: Assets 提供了集中式视频资产管理功能，您可以将视频直接上传到 Assets 以自动编码为 Scene7，并直接从 Assets 访问 Scene7 视频以进行页面创作。
uuid: 46da7a0d-d17b-4716-a304-ce5496421b5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 视频{#video}

资产提供了集中的视频资产管理功能，您可以将视频直接上传到资产，以便自动编码到Dynamic Media Classic，并直接从资产中访问Dynamic Media Classic视频以进行页面创作。

Dynamic Media Classic视频集成将优化视频的范围扩展到所有屏幕（自动设备和带宽检测）。

* 动态媒体经典(Scene7)视频组件可自动执行设备和带宽检测，以跨桌面、平板电脑和移动设备播放正确的格式和质量的视频。
* Assets - 您可以包含自适应视频集，而不只是单个视频资产。自适应视频集是一个容器，其中包含在多种屏幕上无缝播放视频所需的所有视频演绎版。自适应视频集是同一个视频的一组版本，这些版本以不同的比特率和格式进行编码，例如 400 kbps、800 kbps 和 1000 kbps。使用自适应视频集以及 S7 视频组件，可在多种屏幕（包括台式机、iOS、Android、Blackberry 和 Windows 移动设备）上实现自适应视频流式传输。请参阅[有关自适应视频集的 Scene7 文档以了解更多信息](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html)。

## 关于FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

默认的视频编码流程以使用基于 FFMPEG 的视频配置文件集成为基础。Therefore, the out-of-the-box [!UICONTROL DAM Update Asset] workflow contains the following two ffmpeg-based workflow steps:

* FFMPEG 缩略图
* FFMPEG 编码

Be aware that enabling and configuring the Dynamic Media Classic integration does not automatically remove or deactivate these two workflow steps from the out-of-the-box [!UICONTROL DAM Update Asset] ingestion workflow. 如果您已经在 AEM 中使用基于 FFMPEG 的视频编码，则您很可能已经在创作环境中安装了 FFMPEG。在这种情况下，使用资产摄取的新视频将进行两次编码：一次来自FFMPEG编码器，另一次来自Dynamic Media Classic集成。

If you have the FFMPEG-based video encoding in AEM configured and FFMPEG installed, Adobe recommends that you remove the two FFMPEG workflows from your [!UICONTROL DAM Update Asset] workflows.

### 支持的格式 {#supported-formats}

Dynamic Media Classic视频组件支持以下格式：

* F4V H.264
* MP4 H.264

### 确定要将视频上传到的位置 {#deciding-where-to-upload-your-video}

确定要将视频资产上传到的位置取决于以下因素：

* 您是否需要对视频资产使用工作流？
* 您是否需要对视频资产进行版本控制？

如果上述任一问题的答案为“是”或两个问题的答案都为“是”，请将您的视频直接上传到 Adobe DAM。如果两个问题的答案都是“否”，则直接将视频上传到Dynamic Media Classic。 以下部分介绍了针对每种情景的工作流。

#### 如果您要将视频直接上传到 Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

如果您需要对资产使用工作流或进行版本控制，应首先将资产上传到 Adobe Assets。下面是建议的工作流：

1. 将视频资产上传到Adobe资产，然后自动编码并发布到Dynamic Media Classic。
1. 在 AEM 中，从内容查找器的&#x200B;**[!UICONTROL 电影]**&#x200B;选项卡的 WCM 中访问视频资产。
1. 使用Dynamic Media Classic视频或基础视频组件进行创作。

#### 如果要将视频上传到Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要资产的工作流或版本控制，则应将资产上传到Dynamic Media Classic。 下面是建议的工作流：

1. 在Dynamic Media Classic中，设 [置到Dynamic Media Classic（系统自动化）的计划FTP上传和编码](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html)。
1. In AEM, access video assets in WCM in the **[!UICONTROL Dynamic Media Classic]** tab of the Content Finder.
1. 使用Dynamic Media Classic视频组件进行创作。

### 配置与Dynamic Media Classic视频的集成 {#configuring-integration-with-scene-video}

**要配置通用预设**:

1. In **[!UICONTROL Cloud Services]**, navigate to your **[!UICONTROL Dynamic Media Classic]** configuration and click **[!UICONTROL Edit]**.
1. 选择&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。

   >[!NOTE]
   >
   >如果页面中没有云配置，则不会显示&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。请参 [阅为WCM启用Dynamic Media Classic](#enablingscene7forwcm)。

1. 选择自适应视频编码配置文件、现成的单个视频编码配置文件，或自定义视频编码配置文件。

   >[!NOTE]
   >
   >For more information about what the video presets mean, see the [Dynamic Media Classic documentation](https://help.adobe.com/en_US/scene7/using/WSE86ACF2B-BD50-4c48-A1D7-9CD4405B62D0.html).
   >
   >Adobe 建议您在配置通用预设时选择两个自适应视频集，或选择&#x200B;**[!UICONTROL 自适应视频编码]**&#x200B;选项。

1. 所选的编码用户档案将自动应用于上传到您为此Dynamic Media Classic云配置设置的CQ DAM目标文件夹的所有视频。 您可以使用不同的目标文件夹设置多个Dynamic Media Classic云配置，以根据需要应用不同的编码用户档案。

### 更新查看器和编码预设 {#updating-viewer-and-encoding-presets}

If you need to update the viewer and encoding presets for video in AEM because the presets have been updated in Dynamic Media Classic, navigate to the Dynamic Media Classic configuration in the cloud configuration and click **Update the viewer and encoding presets**.

![chlimage_1-131](assets/chlimage_1-131.png)

### 上传主视频 {#uploading-your-master-video}

要从Adobe DAM将主视频上传到Dynamic Media Classic，请执行以下操作：

1. 导航到CQ DAM目标文件夹，您已在该文件夹中使用Dynamic Media Classic编码用户档案设置了云配置。
1. 单击&#x200B;**[!UICONTROL 上传]**&#x200B;以上传主视频。Video uploading and encoding is complete after the [!UICONTROL DAM Update Asset] workflow is complete and **[!UICONTROL Publish to Dynamic Media Classic]** has a checkmark.

   >[!NOTE]
   >
   >可能需要一些时间才能生成视频缩略图。

   Dragging the DAM master video on to the video component accesses *all* of the Dynamic Media Classic encoded proxy renditions for delivery.

### 基础视频组件与动态媒体经典视频组件 {#foundation-video-component-versus-scene-video-component}

使用AEM时，您可以访问站点中可用的视频组件和动态媒体经典(Scene7)视频组件。 这些组件不能交换使用。

动态媒体经典视频组件仅适用于动态媒体经典视频。 基础组件可处理从AEM（使用ffmpeg）和Dynamic Media Classic视频存储的视频。

下表说明了何时应使用何种组件：

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>开箱即用的Dynamic Media Classic视频组件使用通用视频用户档案。 但是，您可以获取供AEM使用的基于HTML5的视频播放器。 在Dynamic Media Classic中，复制现成HTML5视频播放器的嵌入代码，并将其放入AEM页面。


## AEM 视频组件 {#aem-video-component}

即使建议使用Dynamic Media Classic视频组件来查看Dynamic Media Classic视频，本节也会为了完整起见，在AEM中将Dynamic Media Classic视频与 [!UICONTROL Foundation Video Component] 一起使用进行说明。

### AEM Video和Dynamic Media Classic Video比较 {#aem-video-and-scene-video-comparison}

下表简单地比较了 AEM 基础视频组件与 Scene7 视频组件所支持的功能：

|  | AEM 基础视频 | Dynamic Media Classic视频 |
|---|---|---|
| 方法 | HTML5 为首选方法。Flash 仅用作不可使用 HTML5 时的回退方法。 | 在大多数台式机上使用 Flash。在移动设备和平板电脑上使用 HTML5。 |
| 交付 | 渐进式 | 自适应流式传输 |
| 跟踪 | 是 | 是 |
| 可扩展性 | 是 | 是（使用Dynamic Media Classic查看器SDK） |
| 移动视频 | 是 | 是 |

### 设置 {#setting-up}

#### 创建视频配置文件 {#creating-video-profiles}

根据在Dynamic Media Classic云配置中选择的Dynamic Media Classic编码预设创建各种视频编码。 为了使基础视频组件能够使用它们，必须为选定的每个Dynamic Media Classic编码预设创建视频用户档案。 这会相应地允许视频组件选择 DAM 演绎版。

>[!NOTE]
>
>必须激活新的视频配置文件以及对其所做的更改，才能进行发布。

1. 在 AEM 中，转到&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 配置控制台]**。In the Configuration Console navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]** in the navigation tree.
1. 创建新的Dynamic Media Classic视频用户档案。 In the **[!UICONTROL New...]** menu, select **[!UICONTROL Create Page]** and then select the Dynamic Media Classic Video Profile template. 为新的视频配置文件页面指定一个名称，然后单击&#x200B;**[!UICONTROL 创建]**。

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 编辑新的视频配置文件。首先选择云配置。然后，选择在云配置中选定的相同编码预设。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | 属性 | 描述 |
   |---|---|
   | Dynamic Media Classic(Scene7)云配置 | 用于编码预设的云配置。 |
   | Dynamic Media Classic(Scene7)编码预设 | 要映射此视频用户档案的编码预设。 |
   | HTML5 视频类型 | 此属性允许设置HTML5视频源元素的type属性的值。 Dynamic Media Classic编码预设不提供此信息，但使用HTML5视频元素正确呈现视频时需要此信息。 提供了通用格式列表，但是通用格式可被其他格式覆盖。 |

   对要在视频组件中使用的云配置中选定的所有编码预设重复此步骤。

#### 配置设计 {#configuring-design}

基础视频组件必须知晓要使用哪些视频配置文件，才能构建视频源列表。您必须打开视频组件设计对话框，并配置组件设计，以便使用新的视频配置文件。

>[!NOTE]
>
>如果您在移动页面上使用基础视频组件，则可能需要在设计移动页面时重复这些步骤。

>[!NOTE]
>
>对设计所做的更改需要激活设计，才能在发布时生效。

1. 打开基础视频组件的设计对话框，并切换到&#x200B;**[!UICONTROL 配置文件]**&#x200B;选项卡。然后，删除现成用户档案，并添加新的Dynamic Media Classic视频用户档案。 设计对话框中的用户档案列表的顺序还定义了渲染时视频源元素的顺序。
1. 对于不支持 HTML5 的浏览器，视频组件允许配置 Flash 回退方法。打开视频组件的设计对话框，并切换到 **[!UICONTROL Flash]** 选项卡。配置 Flash Player 设置，并指定 Flash Player 的回退配置文件。

#### 核对清单 {#checklist}

1. 创建Dynamic Media Classic(Scene7)云配置。 确保已设置视频编码预设，且导入程序正在运行。
1. 为云配置中选定的每个视频编码预设创建Dynamic Media Classic视频用户档案。
1. 必须激活视频配置文件。
1. 配置页面上基础视频组件的设计。
1. 完成对设计的更改后，激活设计。

