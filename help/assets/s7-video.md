---
title: 视频
description: 了解集中式视频资源管理Adobe Experience Manager Assets ，您可以在其中将视频上传到Dynamic Media Classic以进行自动编码，并直接从Experience Manager Assets访问Dynamic Media Classic视频。 Dynamic Media Classic视频集成将优化视频的覆盖范围扩展到所有屏幕。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
role: User, Admin
mini-toc-levels: 3
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Video
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 1%

---

# 视频 {#video}

Adobe Experience Manager Assets提供了集中式视频资源管理，您可以在其中直接将视频上传到Assets以自动编码到Dynamic Media Classic，并直接从Assets访问Dynamic Media Classic视频以进行页面创作。

Dynamic Media Classic视频集成将优化视频的覆盖范围扩展到所有屏幕（自动设备和带宽检测）。

* 此 **[!UICONTROL Scene7视频]** 组件自动执行设备和带宽检测，从而在台式机、平板电脑和移动设备上播放正确格式和正确质量的视频。
* 资源 — 您可以包含自适应视频集，而不是只包含单个视频资源。 自适应视频集包含要在多个屏幕上无缝回放视频所需的所有视频演绎版。 自适应视频集对使用不同比特率和格式（例如400 kbps、800 kbps和1000 kbps）编码的相同视频的版本进行分组。 您可以使用自适应视频集和S7视频组件在多个屏幕(包括台式机、iOS、Android™、BlackBerry®和Windows移动设备)上实现自适应视频流传输。
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## 关于FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

默认视频编码过程基于使用与视频配置文件基于FFMPEG的集成。 因此，现成的DAM摄取工作流包含以下两个基于ffmpeg的工作流步骤：

* FFMPEG缩略图
* FFMPEG编码

启用和配置Dynamic Media Classic集成不会自动从现成的DAM摄取工作流中删除或停用这两个工作流步骤。 如果您已在Adobe Experience Manager中使用基于FFMPEG的视频编码，则可能在创作环境中安装了FFMPEG。 在这种情况下，使用DAM摄取的新视频将编码两次：一次来自FFMPEG编码器，一次来自Dynamic Media Classic集成。

如果已配置Experience Manager中基于FFMPEG的视频编码并安装了FFMPEG，Adobe建议您从DAM摄取工作流中删除这两个FFMPEG工作流。

## 支持的格式 {#supported-formats}

Scene7视频组件支持以下格式：

* F4V H.264
* MP4 H.264

## 决定上传视频的位置 {#deciding-where-to-upload-your-video}

根据以下条件确定上传视频资产的位置：

* 您是否需要视频资产的工作流？
* 视频资源是否需要版本控制？

如果对其中任一问题或两个问题的答案为“是”，则直接将您的视频上传到AdobeDAM。 如果这两个问题的答案都为“否”，则直接将您的视频上传到Dynamic Media Classic。 下节将介绍每个方案的工作流。

### 如果您将视频直接上传到AdobeDAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

如果您需要资源的工作流或版本控制，请先上传到AdobeDAM。 以下是推荐的工作流：

1. 将视频资源上传到AdobeDAM，并自动编码和发布到Dynamic Media Classic。
1. 在Experience Manager中，访问WCM中的视频资源 **[!UICONTROL 电影]** 内容查找器的选项卡。
1. 作者 **[!UICONTROL Scene7视频]** 或 **[!UICONTROL Foundation视频]** 组件。

### 如果您正在将视频上传到Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要资源的工作流或版本控制，请将资源上传到Scene7。 以下是推荐的工作流：

1. 在Dynamic Media Classic中， [设置计划的FTP上传和编码到Scene7（系统自动）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp).
1. 在Experience Manager中，访问WCM中的视频资源 **[!UICONTROL Scene7]** 内容查找器的选项卡。
1. 使用创作 **[!UICONTROL Scene7视频]** 组件。

## 配置与Scene7的集成视频 {#configuring-integration-with-scene-video}

1. 在 **[!UICONTROL Cloud Service]**，导航到 **[!UICONTROL Scene7]** 配置和选择 **[!UICONTROL 编辑]**.
1. 选择 **[!UICONTROL 视频]** 选项卡。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >此 **[!UICONTROL 视频]** 如果页面没有云配置，则不会显示选项卡。

1. 选择自适应视频编码配置文件、现成的单个视频编码配置文件或自定义视频编码配置文件。

   >[!NOTE]
   >
   >有关视频预设含义的更多信息，请参阅 [Dynamic Media Classic文档](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe建议您在配置通用预设时同时选择两个自适应视频集，或者选择 **[!UICONTROL 自适应视频编码]** 选项。

1. 所选的编码配置文件将自动应用于上传到您为此Scene7云配置设置的CQ DAM目标文件夹的所有视频。 您可以使用不同的Target文件夹设置多个Scene7云配置，以根据需要应用不同的编码配置文件。

## 更新查看器和编码预设 {#updating-viewer-and-encoding-presets}

要更新视频的查看器和编码预设，因为已在Scene7中更新了这些预设，请导航到云配置中的Scene7配置，然后选择 **[!UICONTROL 更新查看器和编码预设]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## 从AdobeDAM将您的主源视频上传到Scene7 {#uploading-your-master-video}

1. 导航到CQ DAM目标文件夹，您已在该文件夹中使用Scene7编码配置文件设置云配置。
1. 选择 **[!UICONTROL 上传]** 上传主源视频。 视频上传和编码在 [!UICONTROL DAM更新资产] 工作流已完成，并且 **[!UICONTROL 发布到Scene7]** 有一个复选标记。

   >[!NOTE]
   >
   >生成视频缩略图需要时间。

   将DAM主源视频拖动到视频组件访问 *所有* 用于投放的Scene7编码代理呈现。

## Foundation视频组件与Scene7视频组件 {#foundation-video-component-versus-scene-video-component}

使用Experience Manager时，您可以同时访问Sites中可用的视频组件和Scene7视频组件。 这些组件不可互换。

Scene7视频组件仅适用于Scene7视频。 基础组件可处理从Experience Manager（使用ffmpeg）存储的视频和Scene7视频。

以下矩阵说明了何时使用哪个组件：

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>S7视频组件使用通用视频配置文件，这是开箱即用的功能。 但是，您可以获取基于HTML5的视频播放器，以供Experience Manager使用。 在Scene7中，复制现成HTML5视频播放器的嵌入代码，并将其放入您的Experience Manager页面中。

## Experience Manager视频组件 {#aem-video-component}

即使推荐使用Scene7视频组件来查看Scene7视频，本节也介绍如何在Experience Manager中将Scene7视频与Foundation视频组件结合使用，以获取完整性的帮助。

### Experience Manager视频与Scene7视频比较 {#aem-video-and-scene-video-comparison}

下表提供了Experience Manager Foundation视频组件与Scene7视频组件之间支持的功能之间的高级比较：

|   | Experience Manager Foundation视频 | Scene7视频 |
|---|---|---|
| 方针 | HTML5先进。 Flash仅用于非HTML5回退。 | 在大多数台式机上Flash。 HTML5用于手机和平板电脑。 |
| 交付 | 渐进式 | 自适应流 |
| 跟踪 | 是 | 是 |
| 可扩展性 | 是 | 否 |
| 移动视频 | 是 | 是 |

### 设置 {#setting-up}

#### 创建视频配置文件 {#creating-video-profiles}

根据S7云配置中选择的S7编码预设创建各种视频编码。 要让foundation视频组件使用它们，必须为所选的每个S7编码预设创建视频配置文件。 此方法允许视频组件相应地选择DAM演绎版。

>[!NOTE]
>
>必须激活新的视频配置文件以及对它们所做的更改才能发布。

1. 在Experience Manager中，选择 **[!UICONTROL 工具]** > **[!UICONTROL 配置控制台]**.
1. 在 **[!UICONTROL 配置控制台]**，导航到 **[!UICONTROL 工具]** > **[!UICONTROL DAM]** > **[!UICONTROL 视频配置文件]** 在导航树中。
1. 创建S7视频配置文件。 在 **[!UICONTROL 新建]**. 菜单，选择 **[!UICONTROL 创建页面]** 然后选择Scene7视频配置文件模板。 为新视频配置文件页面命名，然后选择 **[!UICONTROL 创建]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 编辑新的视频配置文件。 首先选择云配置。 然后选择在云配置中选择的相同编码预设。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | 属性 | 描述 |
   |---|---|
   | Scene7 云配置 | 用于编码预设的云配置。 |
   | Scene7 编码预设 | 用于映射此视频配置文件的编码预设。 |
   | HTML5 视频类型 | 此属性允许您设置HTML5视频源元素的type属性的值。 S7编码预设不提供此信息，但在使用HTML5视频元素正确呈现视频时需要此信息。 提供了常见格式的列表，但其他格式可以覆盖该列表。 |

   对云配置中选定的、要在视频组件中使用的所有编码预设重复此步骤。

#### 配置设计 {#configuring-design}

此 **[!UICONTROL Foundation视频]** 组件必须了解哪些视频配置文件可用来构建视频源列表。 打开视频组件设计对话框，并为使用新视频配置文件配置组件设计。

>[!NOTE]
>
>如果您使用 **[!UICONTROL Foundation视频]** 组件时，请在设计移动设备页面时重复这些步骤。

>[!NOTE]
>
>对设计所做的更改需要激活设计，才能在发布时生效。

1. 打开 **[!UICONTROL Foundation视频]** 组件的“设计”对话框，并更改为 **[!UICONTROL 配置文件]** 选项卡。 然后，删除现成的用户档案并添加新的S7视频用户档案。 在“设计”对话框中，配置文件列表的顺序定义呈现时视频源元素的顺序。
1. 对于不支持HTML5的浏览器，可使用视频组件配置Flash回退。 打开视频组件设计对话框，然后更改为 **[!UICONTROL Flash]** 选项卡。 配置Flash播放器设置并为Flash播放器分配回退配置文件。

#### 清单 {#checklist}

1. 创建S7云配置。 确保设置了视频编码预设并且导入程序正在运行。
1. 为云配置中选择的每个视频编码预设创建S7视频配置文件。
1. 必须激活视频配置文件。
1. 配置设计 **[!UICONTROL Foundation视频]** 组件。
1. 完成设计更改后激活设计。
