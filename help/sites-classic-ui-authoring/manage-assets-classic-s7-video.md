---
title: 视频
seo-title: 视频
description: 资产提供了集中式视频资产管理功能，您可以将视频直接上传到资产，以便自动编码到Dynamic Media经典，并直接从资产访问Dy视频以进行页面创作。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
translation-type: tm+mt
source-git-commit: 801d57bbe8a1bede6dcb4bf7884e5f71ddea1e83
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 39%

---


# 视频{#video}

资产提供了集中式视频资产管理功能，您可以将视频直接上传到资产以自动编码到Dynamic Media经典，并直接从资产访问Dynamic Media经典视频以进行页面创作。

Dynamic Media经典视频集成将优化视频的范围扩展到所有屏幕（自动设备和带宽检测）。

* Dynamic Media经典视频组件可自动执行设备和带宽检测，以跨桌面、平板电脑和移动设备播放格式正确且质量正确的视频。
* Assets - 您可以包含自适应视频集，而不只是单个视频资产。自适应视频集是一个容器，其中包含在多种屏幕上无缝播放视频所需的所有视频演绎版。自适应视频集是同一个视频的一组版本，这些版本以不同的比特率和格式进行编码，例如 400 kbps、800 kbps 和 1000 kbps。使用自适应视频集以及 S7 视频组件，可在多种屏幕（包括台式机、iOS、Android、Blackberry 和 Windows 移动设备）上实现自适应视频流式传输。有关详细信息，请参阅[关于自适应视频集的Dynamic Media经典文档](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video)。

## 关于FFMPEG和Dynamic Media经典{#about-ffmpeg-and-scene}

默认的视频编码流程以使用基于 FFMPEG 的视频配置文件集成为基础。因此，现成的[!UICONTROL DAM更新资产]工作流包含以下两个基于ffmpeg的工作流步骤：

* FFMPEG 缩略图
* FFMPEG 编码

请注意，启用和配置Dynamic Media经典集成不会自动从现成[!UICONTROL DAM更新资产]摄取工作流中删除或取消激活这两个工作流步骤。 如果您已经在 AEM 中使用基于 FFMPEG 的视频编码，则您很可能已经在创作环境中安装了 FFMPEG。在这种情况下，使用资产摄取的新视频将进行两次编码：一次来自FFMPEG编码器，另一次来自Dynamic Media经典集成。

如果您在AEM中配置了基于FFMPEG的视频编码并安装了FFMPEG,Adobe建议您从[!UICONTROL DAM更新资产]工作流中删除两个FFMPEG工作流。

### 支持的格式 {#supported-formats}

Dynamic Media经典视频组件支持以下格式：

* F4V H.264
* MP4 H.264

### 确定要将视频上传到的位置  {#deciding-where-to-upload-your-video}

确定要将视频资产上传到的位置取决于以下因素：

* 您是否需要对视频资产使用工作流？
* 您是否需要对视频资产进行版本控制？

如果上述任一问题的答案为“是”或两个问题的答案都为“是”，请将您的视频直接上传到 Adobe DAM。如果两个问题的答案都是“否”，则直接将视频上传到Dynamic Media经典。 以下部分介绍了针对每种情景的工作流。

#### 如果您要将视频直接上传到 Adobe Assets  {#if-you-are-uploading-your-video-directly-to-adobe-assets}

如果您需要对资产使用工作流或进行版本控制，应首先将资产上传到 Adobe Assets。下面是建议的工作流：

1. 将视频资产上传到Adobe资产，并自动编码并发布到Dynamic Media经典。
1. 在 AEM 中，从内容查找器的&#x200B;**[!UICONTROL 电影]**&#x200B;选项卡的 WCM 中访问视频资产。
1. 使用Dynamic Media经典视频或基础视频组件进行创作。

#### 如果要将视频上传到Dynamic Media经典{#if-you-are-uploading-your-video-to-scene}

如果您不需要资产的工作流或版本控制，您应将资产上传到Dynamic Media经典。 下面是建议的工作流：

1. 在Dynamic Media经典桌面应用程序中，[设置到Dynamic Media经典（系统自动）](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html)的计划FTP上传和编码。
1. 在AEM中，访问内容查找器的&#x200B;**[!UICONTROL Dynamic Media经典]**&#x200B;选项卡中WCM中的视频资产。
1. 使用Dynamic Media经典视频组件进行创作。

### 配置与Dynamic Media经典视频{#configuring-integration-with-scene-video}的集成

**要配置通用预设，请执行以下操作**:

1. 在&#x200B;**[!UICONTROL Cloud Services]**&#x200B;中，导航到您的&#x200B;**[!UICONTROL Dynamic Media经典]**&#x200B;配置，然后单击“编辑”。]****[!UICONTROL 
1. 选择&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。

   >[!NOTE]
   >
   >如果页面中没有云配置，则不会显示&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。请参阅[为WCM启用Dynamic Media经典](#enablingscene7forwcm)。

1. 选择自适应视频编码配置文件、现成的单个视频编码配置文件，或自定义视频编码配置文件。

   >[!NOTE]
   >
   >有关视频预设含义的更多信息，请参阅[视频预设，以对视频文件进行编码](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=en#video-presets-for-encoding-video-files)。
   >
   >Adobe 建议您在配置通用预设时选择两个自适应视频集，或选择&#x200B;**[!UICONTROL 自适应视频编码]**&#x200B;选项。

1. 选定的编码用户档案将自动应用于上传到您为此Dynamic Media经典云配置设置的CQ DAM目标文件夹的所有视频。 您可以设置多个具有不同目标文件夹的Dynamic Media经典云配置，以根据需要应用不同的编码用户档案。

### 更新查看器和编码预设 {#updating-viewer-and-encoding-presets}

如果由于Dynamic Media经典中的预设已更新，您需要更新AEM中视频的查看器和编码预设，请导航到云配置中的Dynamic Media经典配置，然后单击&#x200B;**更新查看器和编码预设**。

![chlimage_1-131](assets/chlimage_1-131.png)

### 上传主源视频{#uploading-your-master-video}

要从AdobeDAM将主源视频上传到Dynamic Media经典，请执行以下操作：

1. 导航到CQ DAM目标文件夹，您已在该文件夹中使用Dynamic Media经典编码用户档案设置云配置。
1. 单击&#x200B;**[!UICONTROL 上传]**&#x200B;以上传主源视频。 在[!UICONTROL DAM更新资产]工作流完成且&#x200B;**[!UICONTROL 发布到Dynamic Media经典]**&#x200B;具有复选标记后，视频上传和编码即完成。

   >[!NOTE]
   >
   >可能需要一些时间才能生成视频缩略图。

   将DAM主源视频拖动到视频组件上可访问Dynamic Media经典编码的代理演绎版的&#x200B;*所有*&#x200B;以进行投放。

### 基础视频组件与Dynamic Media经典视频组件{#foundation-video-component-versus-scene-video-component}

使用AEM时，您可以访问站点中提供的视频组件和Dynamic Media经典视频组件。 这些组件不能交换使用。

Dynamic Media经典视频组件仅适用于Dynamic Media经典视频。 基础组件可处理从AEM（使用ffmpeg）和Dynamic Media经典视频存储的视频。

下表说明了何时应使用何种组件：

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>开箱即用的Dynamic Media经典视频组件使用通用视频用户档案。 但是，您可以获取AEM使用的基于HTML5的视频播放器。 在Dynamic Media经典中，复制现成HTML5视频播放器的嵌入代码，并将其放在AEM页面中。


## AEM 视频组件 {#aem-video-component}

即使建议使用Dynamic Media经典视频组件观看Dynamic Media经典视频，本节也会为了完整起见将Dynamic Media经典视频与AEM中的[!UICONTROL 基础视频组件]一起使用。

### AEM视频与Dynamic Media经典视频比较{#aem-video-and-scene-video-comparison}

下表提供了AEM Foundation Video组件与Dynamic Media经典视频组件之间受支持功能的高级比较：

|  | AEM 基础视频 | Dynamic Media经典视频 |
|---|---|---|
| 方法 | HTML5 为首选方法。Flash 仅用作不可使用 HTML5 时的回退方法。 | 在大多数台式机上使用 Flash。在移动设备和平板电脑上使用 HTML5。 |
| 交付 | 渐进式 | 自适应流式传输 |
| 跟踪 | 是 | 是 |
| 可扩展性 | 是 | 否 |
| 移动视频 | 是 | 是 |

### 设置  {#setting-up}

#### 创建视频配置文件 {#creating-video-profiles}

根据在Dynamic Media经典云配置中选择的Dynamic Media经典编码预设创建各种视频编码。 为了使基础视频组件能够利用它们，必须为选定的每个Dynamic Media经典编码预设创建视频用户档案。 这会相应地允许视频组件选择 DAM 演绎版。

>[!NOTE]
>
>必须激活新的视频配置文件以及对其所做的更改，才能进行发布。

1. 在 AEM 中，转到&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 配置控制台。]** 在配置控制台中，导航 **[!UICONTROL 树中]** ，导 **[!UICONTROL 航到]** “工具 **[!UICONTROL ”>“资]** 产”>“视频配置文件”。
1. 创建新的Dynamic Media经典视频用户档案。 在&#x200B;**[!UICONTROL 新建……]**&#x200B;菜单，选择&#x200B;**[!UICONTROL 创建页面]**，然后选择“Dynamic Media经典视频用户档案”模板。 为新的视频用户档案页命名，然后单击“创建”。]****[!UICONTROL 

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 编辑新的视频配置文件。首先选择云配置。然后，选择在云配置中选定的相同编码预设。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | 属性 | 描述 |
   |---|---|
   | Dynamic Media经典云配置 | 用于编码预设的云配置。 |
   | Dynamic Media经典编码预设 | 要映射此视频用户档案的编码预设。 |
   | HTML5 视频类型 | 此属性允许设置HTML5视频源元素的type属性的值。 此信息并非由Dynamic Media经典编码预设提供，而是为使用HTML5视频元素正确呈现视频所必需的。 提供了通用格式列表，但是通用格式可被其他格式覆盖。 |

   对要在视频组件中使用的云配置中选定的所有编码预设重复此步骤。

#### 配置设计  {#configuring-design}

基础视频组件必须知晓要使用哪些视频配置文件，才能构建视频源列表。您必须打开视频组件设计对话框，并配置组件设计，以便使用新的视频配置文件。

>[!NOTE]
>
>如果您在移动页面上使用基础视频组件，则可能需要在设计移动页面时重复这些步骤。

>[!NOTE]
>
>对设计所做的更改需要激活设计，才能在发布时生效。

1. 打开基础视频组件的设计对话框，并切换到&#x200B;**[!UICONTROL 配置文件]**&#x200B;选项卡。然后删除现成用户档案并添加新的Dynamic Media经典视频用户档案。 设计对话框中的用户档案列表的顺序还定义了渲染时视频源元素的顺序。
1. 对于不支持 HTML5 的浏览器，视频组件允许配置 Flash 回退方法。打开视频组件的设计对话框，并切换到 **[!UICONTROL Flash]** 选项卡。配置 Flash Player 设置，并指定 Flash Player 的回退配置文件。

#### 核对清单  {#checklist}

1. 创建Dynamic Media经典云配置。 确保已设置视频编码预设，且导入程序正在运行。
1. 为云配置中选定的每个视频编码预设创建Dynamic Media经典视频用户档案。
1. 必须激活视频配置文件。
1. 配置页面上基础视频组件的设计。
1. 完成对设计的更改后，激活设计。

