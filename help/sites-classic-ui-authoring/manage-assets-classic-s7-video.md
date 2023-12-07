---
title: Sites Classic创作中的视频
description: Assets可提供集中式视频资源管理，在这里，您可以将视频直接上传到Assets以自动编码到Dynamic Media Classic，并直接从Assets访问视频以进行页面创作。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 0%

---

# 视频{#video}

Assets可提供集中式视频资源管理，您可以在其中直接将视频上传到Assets以自动编码到Dynamic Media Classic，并直接从Assets访问Dynamic Media Classic视频以进行页面创作。

Dynamic Media Classic视频集成将优化视频的覆盖范围扩展到所有屏幕（自动设备和带宽检测）。

* Dynamic Media Classic视频组件自动执行设备和带宽检测，以在台式机、平板电脑和移动设备之间播放正确格式和正确质量的视频。
* 资源 — 您可以包含自适应视频集，而不是只包含单个视频资源。 自适应视频集是用于在多个屏幕上无缝播放视频所需的所有视频演绎版的容器。 自适应视频集对使用不同比特率和格式（例如400 kbps、800 kbps和1000 kbps）编码的相同视频的版本进行分组。 您可以使用自适应视频集和S7视频组件在多个屏幕(包括台式机、iOS、Android™、BlackBerry®和Windows移动设备)上实现自适应视频流传输。 请参阅 [Dynamic Media Classic文档关于自适应视频集以了解更多信息](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## 关于FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

默认视频编码过程基于使用与视频配置文件基于FFMPEG的集成。 因此，开箱即用 [!UICONTROL DAM更新资产] 工作流包含以下两个基于ffmpeg的工作流步骤：

* FFMPEG缩略图
* FFMPEG编码

启用和配置Dynamic Media Classic集成不会自动从现成的工作流中删除或停用这两个工作流步骤 [!UICONTROL DAM更新资产] 摄取工作流。 如果您已在Adobe Experience Manager中使用基于FFMPEG的视频编码，则可能在创作环境中安装了FFMPEG。 在本例中，使用Experience Manager Assets摄取的新视频被编码两次：一次来自FFMPEG编码器，一次来自Dynamic Media Classic集成。

如果配置了Experience Manager中基于FFMPEG的视频编码并安装了FFMPEG，则Adobe建议从工作流中删除两个FFMPEG工作流。 [!UICONTROL DAM更新资产] 工作流。

### 支持的格式 {#supported-formats}

Dynamic Media Classic视频组件支持以下格式：

* F4V H.264
* MP4 H.264

### 决定上传视频的位置 {#deciding-where-to-upload-your-video}

根据以下条件确定上传视频资产的位置：

* 您是否需要视频资产的工作流？
* 视频资源是否需要版本控制？

如果对其中任一问题或两个问题的答案为“是”，则直接将您的视频上传到AdobeDAM。 如果这两个问题的答案都为“否”，则直接将您的视频上传到Dynamic Media Classic。 下节将介绍每个方案的工作流。

#### 如果您将视频直接上传到Adobe资源 {#if-you-are-uploading-your-video-directly-to-adobe-assets}

如果您需要为资源创建工作流或版本控制，则应先上传到Adobe资源。 以下是推荐的工作流：

1. 将视频资源上传到Adobe资源，并自动编码和发布到Dynamic Media Classic。
1. 在Experience Manager中，访问WCM中的视频资源 **[!UICONTROL 电影]** 内容查找器的选项卡。
1. 使用Dynamic Media Classic视频或基础视频组件创作。

#### 如果您正在将视频上传到Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要为资源创建工作流或版本控制，则应将资源上传到Dynamic Media Classic。 以下是推荐的工作流：

1. 在Dynamic Media Classic桌面应用程序中， [设置计划的FTP上传和编码到Dynamic Media Classic（系统自动）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options).
1. 在Experience Manager中，访问WCM中的视频资源 **[!UICONTROL Dynamic Media Classic]** 内容查找器的选项卡。
1. 使用Dynamic Media Classic视频组件创作。

### 配置与Dynamic Media Classic的集成视频 {#configuring-integration-with-scene-video}

1. 在 **[!UICONTROL Cloud Service]**，导航到 **[!UICONTROL Dynamic Media Classic]** 配置和选择 **[!UICONTROL 编辑]**.
1. 选择 **[!UICONTROL 视频]** 选项卡。

   >[!NOTE]
   >
   >此 **[!UICONTROL 视频]** 如果页面没有云配置，则不会显示选项卡。 请参阅 [为WCM启用Dynamic Media Classic](#enablingscene7forwcm).

1. 选择自适应视频编码配置文件、现成的单个视频编码配置文件或自定义视频编码配置文件。

   >[!NOTE]
   >
   >有关视频预设含义的更多信息，请参阅 [用于编码视频文件的视频预设](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe建议您在配置通用预设时同时选择两个自适应视频集，或者选择 **[!UICONTROL 自适应视频编码]** 选项。

1. 所选的编码配置文件将自动应用于上传到为此Dynamic Media Classic云配置设置的CQ DAM目标文件夹的所有视频。 您可以使用不同的Target文件夹设置多个Dynamic Media Classic云配置，以根据需要应用不同的编码配置文件。

### 更新查看器和编码预设 {#updating-viewer-and-encoding-presets}

如果在Dynamic Media Classic中更新了预设，请更新Experience Manager中视频的查看器和编码预设。 在这种情况下，请导航到云配置中的Dynamic Media Classic配置，然后选择 **更新查看器和编码预设**.

![chlimage_1-131](assets/chlimage_1-131.png)

### 上传您的主源视频 {#uploading-your-master-video}

要从AdobeDAM将主源视频上传到Dynamic Media Classic，请执行以下操作：

1. 导航到CQ DAM目标文件夹，您已在该文件夹中使用Dynamic Media Classic编码配置文件设置云配置。
1. 选择 **[!UICONTROL 上传]** 上传主源视频。 视频上传和编码在 [!UICONTROL DAM更新资产] 工作流已完成，并且 **[!UICONTROL 发布到Dynamic Media Classic]** 有一个复选标记。

   >[!NOTE]
   >
   >生成视频缩略图可能需要一些时间。

   将DAM主源视频拖到视频组件上时，它将访问 *所有* 用于投放的Dynamic Media Classic编码代理呈现。

### Foundation视频组件与Dynamic Media Classic视频组件 {#foundation-video-component-versus-scene-video-component}

使用Experience Manager时，您可以同时访问Sites中可用的视频组件和Dynamic Media Classic视频组件。 这些组件不可互换。

Dynamic Media Classic视频组件仅适用于Dynamic Media Classic视频。 基础组件可处理从Experience Manager（使用ffmpeg）存储的视频和Dynamic Media Classic视频。

以下矩阵说明了何时应使用哪个组件：

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Dynamic Media Classic视频组件开箱即用地使用通用视频配置文件。 但是，您可以获取基于HTML5的视频播放器，以供Experience Manager使用。 在Dynamic Media Classic中，复制现成HTML5视频播放器的嵌入代码，并将其放入您的Experience Manager页面中。
>

## Experience Manager视频组件 {#aem-video-component}

即使推荐使用Dynamic Media Classic视频组件来查看Dynamic Media Classic视频，本节也介绍如何将Dynamic Media Classic视频与 [!UICONTROL Foundation视频组件] Experience Manager完整性。

### Experience Manager视频与Dynamic Media Classic视频比较 {#aem-video-and-scene-video-comparison}

下表提供了Experience Manager Foundation视频组件与Dynamic Media Classic视频组件之间支持的功能之间的高级比较：

|   | Experience Manager Foundation视频 | Dynamic Media Classic视频 |
|---|---|---|
| 方针 | HTML5先进。 Flash仅用于非HTML5回退。 | 在大多数台式机上Flash。 HTML5用于手机和平板电脑。 |
| 交付 | 渐进式 | 自适应流 |
| 跟踪 | 是 | 是 |
| 可扩展性 | 是 | 否 |
| 移动视频 | 是 | 是 |

### 设置 {#setting-up}

#### 创建视频配置文件 {#creating-video-profiles}

根据在Dynamic Media Classic云配置中选择的Dynamic Media Classic编码预设创建各种视频编码。 要让foundation视频组件使用它们，您必须为每个选定的Dynamic Media Classic编码预设创建一个视频配置文件。 它允许视频组件相应地选择DAM演绎版。

>[!NOTE]
>
>必须激活新的视频配置文件以及对它们所做的更改才能发布。

1. 在Experience Manager中，转到 **[!UICONTROL 工具]**，然后选择 **[!UICONTROL 配置控制台]**.
1. 在Configuration Console，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]** 在导航树中。
1. 创建Dynamic Media Classic视频配置文件。 在 **[!UICONTROL 新建]** 菜单，选择 **[!UICONTROL 创建页面]**.
1. 选择Dynamic Media Classic视频配置文件模板。 为新视频配置文件页面命名，然后选择 **[!UICONTROL 创建]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 编辑新的视频配置文件。 首先选择云配置。 然后选择在云配置中选择的相同编码预设。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | 属性 | 描述 |
   |---|---|
   | Dynamic Media Classic云配置 | 用于编码预设的云配置。 |
   | Dynamic Media Classic编码预设 | 用于映射此视频配置文件的编码预设。 |
   | HTML5 视频类型 | 此属性允许您设置HTML5视频源元素的type属性的值。 Dynamic Media Classic编码预设不提供此信息，但在使用HTML5视频元素正确呈现视频时需要此信息。 提供了常见格式的列表，但其他格式可以覆盖该列表。 |

   对云配置中选定的、要在视频组件中使用的所有编码预设重复此步骤。

#### 配置设计 {#configuring-design}

Foundation视频组件必须了解哪些视频配置文件可用来构建视频源列表。 打开视频组件设计对话框，并为使用新视频配置文件配置组件设计。

>[!NOTE]
>
>如果您在移动设备页面上使用基础视频组件，请在移动设备页面的设计上重复这些步骤。

>[!NOTE]
>
>对设计所做的更改需要激活设计，才能在发布时生效。

1. 打开基础视频组件的“设计”对话框，然后更改为 **[!UICONTROL 配置文件]** 选项卡。 然后，删除现成的配置文件并添加新的Dynamic Media Classic视频配置文件。 配置文件列表在“设计”对话框中的顺序，以及渲染时视频源元素的顺序。
1. 对于不支持HTML5的浏览器，可使用视频组件配置闪存回退。 打开视频组件设计对话框并更改为 **[!UICONTROL Flash]** 选项卡。 配置flash player设置并为flash player分配回退配置文件。

#### 清单 {#checklist}

1. 创建Dynamic Media Classic云配置。 确保设置了视频编码预设并且导入程序正在运行。
1. 为云配置中选择的每个视频编码预设创建一个Dynamic Media Classic视频配置文件。
1. 必须激活视频配置文件。
1. 在页面上配置基础视频组件的设计。
1. 完成设计更改后激活设计。
