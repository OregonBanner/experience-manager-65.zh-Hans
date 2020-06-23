---
title: 视频
description: 了解集中式视频资产管理AEM Assets，您可以将视频上传到Dynamic Media经典，并直接从AEM Assets访问Dynamic Media经典视频。 Dynamic Media经典视频集成将优化视频的触及范围扩展到所有屏幕。
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1628'
ht-degree: 52%

---


# 视频 {#video}

资产提供了集中式视频资产管理功能，您可以将视频直接上传到资产，以便自动编码到Dynamic Media经典(Scene7)，并直接从资产中访问Dynamic Media经典视频以进行页面创作。

Dynamic Media经典视频集成将优化视频的范围扩展到所有屏幕（自动设备和带宽检测）。

* The **[!UICONTROL Scene7 Video]** component automatically performs device and bandwidth detection to play the right format and right quality video across desktop, tablets and mobile.
* Assets - 您可以包含自适应视频集，而不只是单个视频资产。自适应视频集是一个容器，其中包含在多种屏幕上无缝播放视频所需的所有视频演绎版。自适应视频集是同一个视频的一组版本，这些版本以不同的比特率和格式进行编码，例如 400 kbps、800 kbps 和 1000 kbps。使用自适应视频集以及 S7 视频组件，可在多种屏幕（包括台式机、iOS、Android、Blackberry 和 Windows 移动设备）上实现自适应视频流式传输。请参阅[有关自适应视频集的 Scene7 文档以了解更多信息](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html)。

## 关于FFMPEG和Dynamic Media经典 {#about-ffmpeg-and-scene}

默认的视频编码流程以使用基于 FFMPEG 的视频配置文件集成为基础。因此，现成的DAM摄取工作流包含以下两个基于ffmpeg的工作流步骤：

* FFMPEG 缩略图
* FFMPEG 编码

请注意，启用和配置Dynamic Media经典集成不会自动从现成的DAM摄取工作流中删除或取消激活这两个工作流步骤。 如果您已经在 AEM 中使用基于 FFMPEG 的视频编码，则您很可能已经在创作环境中安装了 FFMPEG。在这种情况下，使用DAM摄取的新视频将进行两次编码： 一次来自FFMPEG编码器，另一次来自Dynamic Media经典集成。

如果您在AEM中配置了基于FFMPEG的视频编码并安装了FFMPEG,Adobe建议您从DAM摄取工作流中删除两个FFMPEG工作流。

## 支持的格式 {#supported-formats}

Scene7 视频组件支持以下格式：

* F4V H.264
* MP4 H.264

## 确定要将视频上传到的位置 {#deciding-where-to-upload-your-video}

确定要将视频资产上传到的位置取决于以下因素：

* 您是否需要对视频资产使用工作流？
* 您是否需要对视频资产进行版本控制？

如果上述任一问题的答案为“是”或两个问题的答案都为“是”，请将您的视频直接上传到 Adobe DAM。如果两个问题的答案都是“否”，则直接将视频上传到Dynamic Media经典。 以下部分介绍了针对每种情景的工作流。

### If you are uploading your video directly to Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

如果您需要资产的工作流或版本控制，您应先上传到Adobe DAM。 下面是建议的工作流：

1. 将视频资产上传到Adobe DAM，并自动编码并发布到Dynamic Media经典。
1. 在 AEM 中，从内容查找器的&#x200B;**[!UICONTROL 电影]**&#x200B;选项卡的 WCM 中访问视频资产。
1. Author with **[!UICONTROL Scene7 Video]** or **[!UICONTROL Foundation Video]** component.

### 如果您要将视频上传到 Scene7 {#if-you-are-uploading-your-video-to-scene}

如果您不需要对资产使用工作流或进行版本控制，应将资产上传到 Scene7。下面是建议的工作流：

1. In Dynamic Media Classic, [set up a scheduled FTP uploading and encoding to Scene7 (system automated)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html).
1. 在 AEM 中，从内容查找器的 **[!UICONTROL Scene7]** 选项卡的 WCM 中访问视频资产。
1. Author with the **[!UICONTROL Scene7 Video]** component.

## 配置与 Scene7 视频的集成 {#configuring-integration-with-scene-video}

要配置通用预设，请执行以下操作：

1. In **[!UICONTROL Cloud Services]**, navigate to your **[!UICONTROL Scene7]** configuration and click **[!UICONTROL Edit.]**
1. 选择&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >如果页面中没有云配置，则不会显示&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。

1. 选择自适应视频编码配置文件、现成的单个视频编码配置文件，或自定义视频编码配置文件。

   >[!NOTE]
   >
   >For more information about what the video presets mean, see the [Dynamic Media Classic documentation](https://help.adobe.com/en_US/scene7/using/WSE86ACF2B-BD50-4c48-A1D7-9CD4405B62D0.html).
   >
   >Adobe 建议您在配置通用预设时选择两个自适应视频集，或选择&#x200B;**[!UICONTROL 自适应视频编码]**&#x200B;选项。

1. 选定的编码配置文件会自动应用于上传到您为此 Scene7 云配置设置的 CQ DAM 目标文件夹的所有视频。您可以根据需要设置多个具有不同目标文件夹的 Scene7 云配置，以便应用不同的编码配置文件。

## 更新查看器和编码预设 {#updating-viewer-and-encoding-presets}

If you need to update the viewer and encoding presets for video in AEM because the presets have been updated in Scene7, navigate to the Scene7 configuration in the cloud configuration and click **[!UICONTROL Update the viewer and encoding presets.]**

![chlimage_1-364](assets/chlimage_1-364.png)

## 将主源视频从Adobe DAM上传到Scene7 {#uploading-your-master-video}

1. 导航到在其中为云配置设置了 Scene7 编码配置文件的 CQ DAM 目标文件夹。
1. 单击 **[!UICONTROL 上传]** ，以上传主源视频。 Video uploading and encoding is complete after the [!UICONTROL DAM Update Asset] workflow is complete and **[!UICONTROL Publish to Scene7]** has a checkmark.

   >[!NOTE]
   >
   >可能需要一些时间才能生成视频缩略图。

   Dragging the DAM primary source video on to the video component accesses *all* of the Scene7 encoded proxy renditions for delivery.

## 基础视频组件与 Scene7 视频组件 {#foundation-video-component-versus-scene-video-component}

使用 AEM 时，您有权访问 Sites 中提供的视频组件以及 Scene7 视频组件。这些组件不能交换使用。

Scene7 视频组件仅适用于 Scene7 视频。而基础组件则适用于 AEM 中存储的视频（使用 FFMPEG）以及 Scene7 视频。

下表说明了何时应使用何种组件：

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>S7 视频组件使用现成的通用视频配置文件。但是，通过在Scene7中执行下列操作之一，您可以获得供AEM使用的基于HTML5的视频播放器： 复制现成HTML5视频播放器的嵌入代码，并将其放入AEM页面。

## AEM 视频组件 {#aem-video-component}

虽然建议使用 Scene7 视频组件来查看 Scene7 视频，但是为了确保内容的完整性，此部分介绍了如何在 AEM 中将 Scene7 视频与基础视频组件结合使用。

### AEM 视频与 Scene7 视频的比较 {#aem-video-and-scene-video-comparison}

下表简单地比较了 AEM 基础视频组件与 Scene7 视频组件所支持的功能：

|  | AEM 基础视频 | Scene7 视频 |
|---|---|---|
| 方法 | HTML5 为首选方法。Flash 仅用作不可使用 HTML5 时的回退方法。 | 在大多数台式机上使用 Flash。在移动设备和平板电脑上使用 HTML5。 |
| 交付 | 渐进式 | 自适应流式传输 |
| 跟踪 | 是 | 是 |
| 可扩展性 | 是 | 是（通过 Scene7 查看器 SDK） |
| 移动视频 | 是 | 是 |

### 设置 {#setting-up}

#### 创建视频配置文件 {#creating-video-profiles}

各种视频编码是根据在 S7 云配置中选定的 S7 编码预设创建的。要使基础视频组件能够利用这些视频编码，必须为每个选定的 S7 编码预设创建视频配置文件。这会相应地允许视频组件选择 DAM 演绎版。

>[!NOTE]
>
>必须激活新的视频配置文件以及对其所做的更改，才能进行发布。

1. 在AEM中，点 **按[!UICONTROL工具>配置控制台**。
1. In the **[!UICONTROL Configuration Console]** navigate to **[!UICONTROL Tools > DAM > Video Profiles]** in the navigation tree.
1. 创建一个新的 S7 视频配置文件。In the **[!UICONTROL New...]** menu, select **[!UICONTROL Create Page]** and then select the Scene7 Video Profile template. Give the new video profile page a name and click **[!UICONTROL Create.]**

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 编辑新的视频配置文件。首先选择云配置。然后，选择在云配置中选定的相同编码预设。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | 属性 | 描述 |
   |---|---|
   | Scene7 云配置 | 用于编码预设的云配置。 |
   | Scene7 编码预设 | 要映射此视频用户档案的编码预设。 |
   | HTML5 视频类型 | 此属性允许设置HTML5视频源元素的type属性的值。 此信息不是由 S7 编码预设提供，但却是使用 HTML5 视频元素正确渲染视频所必需的信息。提供了通用格式列表，但是通用格式可被其他格式覆盖。 |

   对要在视频组件中使用的云配置中选定的所有编码预设重复此步骤。

#### Configuring design {#configuring-design}

The **[!UICONTROL Foundation Video]** component must know about what video profiles to use in order to build the video sources list. 必须打开视频组件设计对话框并配置组件设计以使用新的视频用户档案。

>[!NOTE]
>
>If you use the **[!UICONTROL Foundation Video]** component on a mobile page, you might need to repeat these steps on the design of the mobile page.

>[!NOTE]
>
>对设计所做的更改需要激活设计，才能在发布时生效。

1. Open the **[!UICONTROL Foundation Video]** component&#39;s design dialog box and change to the **[!UICONTROL Profiles]** tab. 然后删除现成用户档案并添加新的S7视频用户档案。 设计对话框中的用户档案列表顺序定义渲染时视频源元素的顺序。
1. 对于不支持HTML5的浏览器，视频组件允许配置Flash回退。 Open the video components design dialog box and change to the **[!UICONTROL Flash]** tab. 配置Flash player设置并为flash player分配备用用户档案。

#### 核对清单 {#checklist}

1. 创建 S7 云配置。确保已设置视频编码预设，且导入程序正在运行。
1. 为云配置中选定的每个视频编码预设创建对应的 S7 视频配置文件。
1. 必须激活视频配置文件。
1. Configure the design of the **[!UICONTROL oundation Video]** component on your page.
1. 完成对设计的更改后，激活设计。

