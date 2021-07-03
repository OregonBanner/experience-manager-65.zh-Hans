---
title: 视频配置文件
description: Dynamic Media 附带预定义的自适应视频编码配置文件。此现成配置文件中的设置经过优化，可为客户提供最佳的查看体验。 您还可以向视频添加智能裁剪。
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
feature: 视频配置文件
role: User, Admin
exl-id: b290fac2-7259-45d7-b733-70419d632b07
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '3697'
ht-degree: 29%

---

# 视频配置文件 {#video-profiles}

Dynamic Media 附带预定义的自适应视频编码配置文件。此现成配置文件中的设置经过优化，可为客户提供最佳的查看体验。 当您使用自适应视频编码配置文件对主源视频进行编码时，在播放视频时，视频播放器会根据客户的Internet连接速度自动调整视频流的质量。 此功能称为自适应流播放。

以下是决定视频质量的其他因素：

* **上传的主源视频的分辨率**

   如果MP4视频以较低的分辨率（如240p或360p）进行录制，则无法以高清晰度对其进行流式处理。

* **视频播放器大小**

   默认情况下，“自适应视频编码”配置文件中的“宽度”设置为“自动”。 同样，在播放期间，会根据播放器的大小使用最佳质量。

请参阅[视频编码最佳实践](/help/assets/video.md#best-practices-for-encoding-videos)。

另请参阅[组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md)。

>[!NOTE]
>
>要生成视频的元数据和关联的视频图像缩略图，视频本身必须在Dynamic Media中完成编码过程。 在Adobe Experience Manager中，如果您已启用Dynamic Media并设置了视频云服务，则&#x200B;**[!UICONTROL Dynamic Media编码视频]**&#x200B;工作流会对视频进行编码。 此工作流会捕获工作流进程历史记录和失败信息。请参阅[监视视频编码和 YouTube 发布进度](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress)。如果您已启用Dynamic Media并设置了视频云服务，则在您上传视频时，**[!UICONTROL Dynamic Media编码视频]**&#x200B;工作流将自动生效。 (如果您没有使用Dynamic Media，则&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流将生效。)
>
>在搜索资产时元数据很有用。缩略图是在编码过程中生成的静态视频图像。 Experience Manager系统需要这些参数，并在用户界面中使用这些参数，以帮助您在“卡片”视图、“搜索结果”视图和“资产列表”视图中以可视方式识别视频。 当您点按编码视频的演绎版图标（画板）时，可以看到生成的缩略图。

创建完视频配置文件后，可将其应用到一个或多个文件夹。请参阅[将视频配置文件应用到文件夹](#applying-a-video-profile-to-folders)。

要为其他资产类型定义高级处理参数，请参阅[配置资产处理](/help/assets/config-dms7.md#configuring-asset-processing)。

另请参阅[用于处理元数据、图像和视频的配置文件](processing-profiles.md)。

## 自适应视频编码预设 {#adaptive-video-encoding-presets}

下表显示了可作为最佳实践的编码配置文件，这些配置文件适用于移动和平板电脑设备及台式计算机上的自适应视频流播放。您可以针对任何宽高比的视频使用这些预设。

<table>
 <tbody>
  <tr>
   <td><strong>视频格式编解码器</strong></td>
   <td><strong>视频大小 — 宽度(px)</strong></td>
   <td><strong>视频大小 — 高度(px)</strong></td>
   <td><strong>保持宽高比？</strong></td>
   <td><strong>视频比特率 (Kbps)</strong></td>
   <td><strong>视频帧速率 (Fps)</strong></td>
   <td><strong>音频编解码器</strong></td>
   <td><strong>音频比特率(Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>是</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264(mp4)</p> </td>
   <td>自动</td>
   <td>540</td>
   <td>是</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>杜比HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264(mp4)</p> </td>
   <td>自动</td>
   <td>720<br /> </td>
   <td>是</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>杜比HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## 关于在视频配置文件中使用智能裁剪 {#about-smart-crop-video}

视频智能裁剪 — 视频配置文件中提供的一项可选功能 — 是一款利用Adobe Sensei中人工智能功能的工具。 它会自动检测并裁剪您上传的任何自适应视频或渐进式视频中的焦点，而无论其大小如何。

支持的智能裁剪视频格式包括MP4、MKV、MOV、AVI、FLV和WMV。

智能裁剪支持的最大视频文件大小为以下条件：

* 持续五分钟。
* 每秒30帧(FPS)。
* 300 MB文件大小。

Adobe Sensei限制为9000帧。 即，以30 FPS的速度为5分钟。 如果视频的FPS较高，则支持的最大视频持续时间会减少。 例如，60 FPS的视频必须长2.5分钟，才能受Adobe Sensei和智能裁剪支持。

![视频智能裁剪](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>要使视频智能裁剪正常工作，您必须在视频配置文件中包含一个或多个视频编码预设。

要对视频使用智能裁剪，请创建自适应或渐进式视频编码配置文件。 在配置文件中，使用&#x200B;**[!UICONTROL 智能裁剪比例]**&#x200B;工具选择预定义的长宽比。 例如，在定义视频编码预设后，您可以添加宽高比为16x9的“移动横向”定义和宽高比为9x16的“移动纵向”定义。 您可以从中选择的其他宽高比或裁剪比例包括1x1、4x3和4x5。

![使用智能裁剪编辑视频编码配置文件](assets/edit-smart-crop-video2.png)

您可以使用用户界面中&#x200B;**[!UICONTROL 智能裁切比]**&#x200B;最右侧的滑块，打开或关闭视频配置文件中的视频智能裁切。

创建并保存视频配置文件后，可以将其应用到所需的文件夹。

请参阅[将视频配置文件应用到特定文件夹](#applying-video-profiles-to-specific-folders)或[全局应用视频配置文件](#applying-a-video-profile-globally)。

另请参阅[图像的智能裁剪](image-profiles.md)。

## 为自适应流播放创建视频配置文件 {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media已附带预定义的自适应视频编码配置文件，该配置文件是一组适用于MP4 H.264的视频上传设置，已针对最佳观看体验进行了优化。您可以在上传视频时使用此用户档案。

但是，如果该预定义的配置文件不符合您的需求，您也可以选择自行创建自适应视频编码配置文件。当您使用设置&#x200B;**[!UICONTROL 自适应流播放的编码]**&#x200B;时 — 作为最佳实践，系统会验证您添加到配置文件的所有编码预设，以确保所有视频具有相同的宽高比。 此外，编码的视频会被视为流播放的多比特率集。

在创建视频编码配置文件时，请注意，大多数编码选项都已预填充推荐的默认设置，以帮助您。 但是，如果您选择的值不是建议的默认值，则可能会在播放过程中导致视频质量不佳以及出现其他性能问题。

因此，对于配置文件中的所有MP4 H.264视频编码预设，将验证以下值，以确保这些值在配置文件中的各个编码预设中均相同，从而实现自适应流播放：

* 视频格式编解码器 - MP4 H.264 (.mp4)
* 音频编解码器
* 音频比特率
* 保持宽高比
* 两次编码
* 恒定比特率
* H264 配置文件
* 音频采样速率

如果这些值不相同，您仍然可以继续创建该配置文件。但是，自适应流播放是不可能的。 相反，用户会体验单比特率流播放。 建议您编辑编码设置，以在配置文件内的各个编码预设中均使用相同的值。（如果启用了&#x200B;**[!UICONTROL 自适应流播放的编码]**，则视频配置文件/预设编辑器强制对自适应视频编码设置执行奇偶校验。）

另请参阅[为渐进式流播放创建视频编码配置文件](#creating-a-video-encoding-profile-for-progressive-streaming)。

另请参阅[视频编码的最佳实践](/help/assets/video.md#best-practices-for-encoding-videos)。

要为其他资产类型定义高级处理参数，请参阅[配置资产处理](/help/assets/config-dms7.md#configuring-asset-processing)。

**要为自适应流播放创建视频配置文件**,

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 视频配置文件]**。
1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以添加视频配置文件。

1. 输入配置文件的名称和描述。
1. 在创建/编辑视频编码预设页面中，点按&#x200B;**[!UICONTROL 添加视频编码预设]**。
1. 在&#x200B;**[!UICONTROL 基本]**选项卡中，设置视频和音频选项。
点按每个选项旁边的信息图标，以了解基于所选视频格式编解码器的其他说明或推荐的设置。
1. 在“视频大小”标题下，确保选中&#x200B;**[!UICONTROL 保持宽高比]**。
1. 以像素为单位设置视频帧大小分辨率。 使用&#x200B;**[!UICONTROL Auto]**&#x200B;值自动缩放以匹配源宽高比（宽高比）。 例如，自动x 480或640 x自动。

1. 执行下列操作之一：

   * 在&#x200B;**[!UICONTROL Width]**&#x200B;字段中，输入&#x200B;**[!UICONTROL auto]**。 在&#x200B;**[!UICONTROL Height]**&#x200B;字段中，输入以像素为单位的值。

   * 要帮助您可视化视频大小，请点按&#x200B;**[!UICONTROL Height]**&#x200B;右侧的信息图标(i)以打开“大小计算器”页面。 使用&#x200B;**[!UICONTROL 大小计算器]**&#x200B;设置所需的视频尺寸（由蓝框表示）。 完成后，点按右上角的 **[!UICONTROL X]**。

1. （可选）点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡，并确保选中&#x200B;**[!UICONTROL 使用默认值]**&#x200B;复选框（推荐）。 或者，修改高级视频和音频设置。
1. 在该页面的右上角，点按&#x200B;**[!UICONTROL 保存]**&#x200B;以保存预设。
1. 执行下列操作之一：
   * 重复第 4-10 步来创建其他编码预设。（自适应视频流播放需要多个视频预设。）
   * 继续下一步。

1. （可选）要向应用此配置文件的视频添加视频智能裁剪，请执行以下操作：
   * 在“编辑视频配置文件”页面的“智能裁剪比例”标题右侧，点按&#x200B;**[!UICONTROL 新增]**。
   * 在“名称”字段中，键入裁剪比例的名称，以帮助您轻松识别它。
   * 从&#x200B;**[!UICONTROL 裁剪比率]**&#x200B;下拉列表中，选择要使用的比率。

1. 执行下列操作之一：

   * 根据需要继续添加新的裁剪比例。
   * 继续下一步。

1. 在该页面的右上角，再次点按&#x200B;**[!UICONTROL 保存]**&#x200B;以保存配置文件。

您现在可以将配置文件应用到包含视频的文件夹。 请参阅[将视频配置文件应用到文件夹](#applying-a-video-profile-to-folders)或[全局应用视频配置文件](#applying-a-video-profile-globally)。

## 为渐进式流播放创建视频配置文件 {#creating-a-video-encoding-profile-for-progressive-streaming}

如果您选择不使用选项&#x200B;**[!UICONTROL 自适应流播放的编码]**，则您添加到配置文件的所有编码预设都将被视为用于单比特率流播放或渐进式视频交付的各个视频演绎版。 此外，不会进行验证，以确保所有视频呈现具有相同的纵横比。

根据您运行的模式，支持的视频格式编解码器如下所示：

* Dynamic Media-Scene7模式：H.264(.mp4)
* Dynamic Media — 混合模式：H.264(.mp4), WebM

另请参阅[为自适应流播放创建视频编码配置文件](#creating-a-video-encoding-profile-for-adaptive-streaming)。

另请参阅[视频编码的最佳实践](/help/assets/video.md#best-practices-for-encoding-videos)。

要为其他资产类型定义高级处理参数，请参阅[配置资产处理](/help/assets/config-dms7.md#configuring-asset-processing)。

**要为渐进式流播放创建视频配置文件，请执行以下操作：**

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 视频配置文件]**。
1. 点按&#x200B;**[!UICONTROL 创建]**&#x200B;以添加视频配置文件。
1. 输入配置文件的名称和描述。
1. 在创建/编辑视频编码预设页面中，点按&#x200B;**[!UICONTROL 添加视频编码预设]**。
1. 在&#x200B;**[!UICONTROL 基本]**选项卡中，设置视频和音频选项。
点按每个选项旁边的信息图标，以了解基于所选视频格式编解码器的其他说明或推荐的设置。
1. （可选）在“视频大小”标题下，取消选中&#x200B;**[!UICONTROL 保持宽高比]**。
1. 执行以下操作：
   * 在&#x200B;**[!UICONTROL Width]**&#x200B;字段中，输入&#x200B;**[!UICONTROL auto]**。
   * 在&#x200B;**[!UICONTROL Height]**字段中，输入以像素为单位的值。
要帮助您可视化视频大小，请点按“高度”的信息图标以打开**[!UICONTROL 大小计算器]**&#x200B;页面。 使用&#x200B;**[!UICONTROL 大小计算器]**&#x200B;页面可进一步按需设置视频尺寸（蓝框）。 完成后，在对话框的右上角，点按&#x200B;**[!UICONTROL X]**。
1. （可选）执行以下操作之一：

   * 点按&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡，并确保选中&#x200B;**[!UICONTROL 使用默认值]**&#x200B;复选框（推荐）。

   * 清除&#x200B;**[!UICONTROL 使用默认值]**复选框，并指定所需的视频设置和音频设置。
点按每个选项旁边的信息图标，以了解基于所选视频格式编解码器的其他说明或推荐的设置。

1. 在该页面的右上角，点按&#x200B;**[!UICONTROL 保存]**&#x200B;以保存预设。
1. 执行下列操作之一：

   * 重复第 4-9 步来创建其他编码预设。
   * 继续下一步。

1. （可选）要向应用此配置文件的视频添加视频智能裁剪，请执行以下操作：

   * 在“编辑视频配置文件”页面的“智能裁剪比例”标题右侧，点按&#x200B;**[!UICONTROL 新增]**。
   * 在“名称”字段中，键入裁剪比例的名称，以帮助您轻松识别它。
   * 从&#x200B;**[!UICONTROL 裁剪比率]**&#x200B;下拉列表中，选择要使用的比率。

1. 执行下列操作之一：

   * 根据需要继续添加新的裁剪比例。
   * 继续下一步。

1. 在页面的右上角，点按保 **[!UICONTROL 存]** ，以保存配置文件。

您现在可以将配置文件应用到包含视频的文件夹。 请参阅[将视频配置文件应用到文件夹](#applying-a-video-profile-to-folders)或[全局应用视频配置文件](#applying-a-video-profile-globally)。

## 使用添加的自定义视频编码参数 {#using-custom-added-video-encoding-parameters}

您可以编辑现有视频编码配置文件，以利用在Experience Manager中创建或编辑视频配置文件时，用户界面中未找到的高级视频编码参数。 向现有配置文件中添加一个或多个高级参数，如minBitrate和maxBitrate 。

**要使用自定义添加的视频编码参数，请执行以下操作：**

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**。
1. 在CRXDE Lite页面的左侧资源管理器面板中，导航到以下内容：

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. 在页面右下方的面板中，从“属性”选项卡中，指定要使用的参数的&#x200B;**[!UICONTROL 名称]**、**[!UICONTROL 类型]**&#x200B;和&#x200B;**[!UICONTROL 值]**。

   可以使用以下高级参数：

<table>
 <tbody>
  <tr>
   <td><strong>名称</strong></td>
   <td><strong>描述</strong><br /> </td>
   <td><strong>类型</strong><br /> </td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>用于编码的H.264级。 通常，此参数会根据您使用的编码设置自动确定。</td>
   <td><code>String</code></td>
   <td><p>10 * h264级</p> <p>例如，3.0 = 30,1.3 = 13)</p> <p>没有默认值。</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>关键帧之间的目标帧数。 计算此值，以便每2到10秒生成一个关键帧。 例如，在每秒30帧时，关键帧间隔应为60-300。<br /> <br /> 较低的关键帧间隔可改进自适应视频编码的流搜寻和流切换行为，并且还可以提高具有大量运动的视频的质量。但是，由于关键帧会增加文件的大小，因此较低的关键帧间隔通常会导致在给定比特率下的整体视频质量降低。</td>
   <td><code>String</code></td>
   <td><p>正数。</p> <p>默认值为300。</p> <p>HLS（HTTP实时流）的推荐值为60-90。</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>允许使用可变比特率编码的最小比特率，以Kbps（千比特/秒）为单位。</p> <p>仅当您在创建或编辑视频编码配置文件时，在“高级”选项卡中取消选中<strong>使用常量比特率</strong>时，此参数才适用。</p> <p>另请参阅<a href="/help/assets/video.md#bitrate">Bitrate</a>。</p> </td>
   <td><code>String</code></td>
   <td><p>正数，以Kbps为单位。</p> <p>没有默认值。</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>允许使用可变比特率编码的最大比特率，以Kbps为单位。</p> <p>仅当您在创建或编辑视频编码配置文件时，在“高级”选项卡中取消选中<strong>使用常量比特率</strong>时，此参数才适用。</p> <p>另请参阅<a href="/help/assets/video.md#bitrate">Bitrate</a>。</p> </td>
   <td><code>String</code></td>
   <td><p>正数，以Kbps为单位。</p> <p>没有默认值。 但是，建议的值最多是编码比特率的两倍。</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>将值设置为<code>true</code>以强制音频流使用恒定的比特率（如果音频编解码器支持）。</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>默认值为<code>false</code>。</p> <p>HLS（HTTP实时流）的推荐值为<code>false</code>。</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. 在页面的右下角附近，点按&#x200B;**[!UICONTROL 添加]**。
1. 执行下列操作之一：

   * 重复步骤3和4，以向视频编码配置文件中添加其他参数。
   * 在页面的左上角附近，点按&#x200B;**[!UICONTROL 全部保存]**。

1. 在CRXDE Lite页面的左上角，点按&#x200B;**[!UICONTROL Back Home]**&#x200B;图标以返回Experience Manager。

### 编辑视频配置文件 {#editing-a-video-encoding-profile}

您可以编辑您创建的任何视频配置文件，以在该配置文件中添加、编辑或删除视频预设。

默认情况下，您无法编辑Dynamic Media附带的预定义现成&#x200B;**[!UICONTROL 自适应视频编码]**&#x200B;配置文件。 相反，您可以轻松复制配置文件并使用新名称进行保存。 然后，您可以在复制的配置文件中编辑所需的预设。

另请参阅[视频编码的最佳实践](/help/assets/video.md#best-practices-for-encoding-videos)。

要为其他资产类型定义高级处理参数，请参阅[配置资产处理](/help/assets/config-dms7.md#configuring-asset-processing)。

**要编辑视频配置文件，请执行以下操作：**

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 视频配置文件]**。
1. 在“视频配置文件”页面上，选中一个视频配置文件名称。
1. 在工具栏中，点按&#x200B;**[!UICONTROL 编辑]**。
1. 在“视频编码配置文件”页面上，根据需要编辑名称和描述。
1. 作为最佳实践，请确保选中“自 **[!UICONTROL 适应流播放的编码]** ”复选框。点按信息图标以获取自适应流播放的说明。 （如果正在编辑渐进式视频配置文件，请勿选中此复选框。）
1. 在“视频编码预设”标题下，添加、编辑或删除构成该配置文件的视频编码预设。

   点按“基本”和“高级”选项卡上每个选项旁 **[!UICONTROL 边的信息图标]****** ，以了解基于所选视频格式编解码器的其他说明或推荐的设置。

1. 在页面的右上角，点按&#x200B;**[!UICONTROL Save]**。

### 复制视频配置文件 {#copying-a-video-encoding-profile}

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 视频配置文件]**。
1. 在“视频配置文件”页面上，选中一个视频配置文件名称。
1. 在工具栏中，点按&#x200B;**[!UICONTROL 复制]**。
1. 在“视频编码配置文件”页面上，输入配置文件的新名称。
1. 作为最佳实践，请确保选中“自 **[!UICONTROL 适应流播放的编码]** ”复选框。 点按信息图标以获取自适应流播放的说明。 （如果要复制渐进式视频配置文件，请勿选中此复选框。）

   在Dynamic Media — 混合模式下，如果WebM视频预设是视频配置文件的一部分，则无法执行&#x200B;**[!UICONTROL 自适应流播放的编码]**，因为所有预设都必须是MP4。
1. 在“视频编码预设”标题下，添加、编辑或删除构成该配置文件的视频编码预设。

   点按基本和高级选项卡上每个选项旁边的信息图标，以了解推荐的设置和说明。

1. 在页面的右上角，点按&#x200B;**[!UICONTROL Save]**。

### 删除视频配置文件 {#deleting-a-video-encoding-profile}

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 视频配置文件]**。
1. 在“视频配置文件”页面上，选中一个或多个视频配置文件名称。
1. 在工具栏中，点按&#x200B;**[!UICONTROL 删除]**。
1. 点按&#x200B;**[!UICONTROL 确定]**。

## 将视频配置文件应用到文件夹 {#applying-a-video-profile-to-folders}

当您将视频配置文件分配给文件夹之后，该文件夹中的所有子文件夹都会自动继承父文件夹的配置文件。此规则表示您只能向文件夹分配一个视频配置文件。 因此，您在上传、存储、使用资产以及将资产存档的过程中，请妥善安排文件夹结构。

如果您为文件夹分配了一个不同的视频配置文件，新配置文件就会取代之前的配置文件。此前存在的文件夹资产将保持不变。此后添加到该文件夹的资产将会应用新的配置文件。

如果文件夹已经分配了配置文件，则用户界面中的卡片名称中会显示配置文件名称。

![chlimage_1-517](assets/chlimage_1-517.png)

您可以将视频配置文件应用到特定文件夹或全局应用到所有资产。

您可以重新处理文件夹中已有视频配置文件且稍后进行了更改的资产。 请参阅[编辑文件夹的处理配置文件后重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

### 将视频配置文件应用到特定文件夹 {#applying-video-profiles-to-specific-folders}

您可以从“工具”菜单中将视频配置文件应用到 **[!UICONTROL 文件夹]** ，或者如果您在文件夹中，也可以从“属 **[!UICONTROL 性”]**。 本节将介绍这两种将视频配置文件应用到文件夹的方法。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

另请参阅[编辑文件夹中的处理配置文件后，重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

#### 通过“配置文件”用户界面将视频配置文件应用到文件夹 {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 视频配置文件]**。
1. 选择您要应用到一个或多个文件夹的视频配置文件。
1. 点按&#x200B;**[!UICONTROL 将配置文件应用到文件夹]**，然后选择一个或多个用于接收新上传资产的文件夹，然后点按&#x200B;**[!UICONTROL 应用]**。 在&#x200B;**[!UICONTROL 卡片视图]**&#x200B;中，如果文件夹已经分配了配置文件，则文件夹名称的正下方会显示配置文件的名称。您可以[监视视频配置文件处理作业的进度](#monitoring-the-progress-of-an-encoding-job)。

#### 从“属性”将视频配置文件应用到文件夹 {#applying-video-profiles-to-folders-from-properties}

1. 点按或单击Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL Assets]**，然后导航到要将视频配置文件应用到的文件夹。
1. 在文件夹中，点按复选标记以将其选中，然后点按&#x200B;**[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 视频配置文件]**&#x200B;选项卡，然后从下拉菜单中选择配置文件，然后单击&#x200B;**[!UICONTROL 保存并关闭]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-518](assets/chlimage_1-518.png)
您可以监 [视视频配置文件处理作业的进度](#monitoring-the-progress-of-an-encoding-job)。

### 全局应用视频配置文件 {#applying-a-video-profile-globally}

除了将配置文件应用到文件夹之外，您还可以全局应用一个配置文件，以便任何文件夹中上传到Experience Manager资产的任何内容都会应用选定的配置文件。

另请参阅[编辑文件夹中的处理配置文件后，重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

**要全局应用视频配置文件，请执行以下操作：**

* 导航到CRXDE Lite到以下节点：`/content/dam/jcr:content`。 添加属性`videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>`并点按&#x200B;**[!UICONTROL 保存全部]**。

   ![chlimage_1-519](assets/chlimage_1-519.png)
* 您可以[监视视频配置文件处理作业的进度](#monitoring-the-progress-of-an-encoding-job)。

## 监控视频配置文件处理作业的进度 {#monitoring-the-progress-of-an-encoding-job}

将显示处理指示器（或进度条），以便您能够直观地监视视频配置文件处理作业的进度。

您还可以查看`error.log`文件以监视编码作业的进度、查看编码是否完成或查看任何作业错误。 `error.log`位于安装Experience Manager实例的`logs`文件夹中。

## 从文件夹删除视频配置文件 {#removing-a-video-profile-from-folders}

当您将视频配置文件从文件夹删除之后，该文件夹中的所有子文件夹都会自动删除从父文件夹继承的配置文件。但是，此前对文件夹中的文件所做的处理均予以保留。

您可以从“工具”菜单中将视频配置文件从文件夹删除 **** ，如果您在文件夹中，也可以从“文件夹设 **[!UICONTROL 置”中删除]**。 本节将介绍这两种将视频配置文件从文件夹删除的方法。

### 通过配置文件用户界面将视频配置文件从文件夹删除 {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 视频配置文件]**。
1. 选择您要从一个或多个文件夹删除的视频配置文件。
1. 点按&#x200B;**[!UICONTROL 从文件夹删除配置文件]**，并选择一个或多个要从中删除配置文件的文件夹，然后点按&#x200B;**[!UICONTROL 删除]**。

   如果视频配置文件的名称不再出现在文件夹名称的下方，则可以确定该视频配置文件不再应用于该文件夹。

### 通过“属性”将视频配置文件从文件夹删除 {#removing-video-profiles-from-folders-by-way-of-properties}

1. 点按Experience Manager徽标，然后导航到&#x200B;**[!UICONTROL Assets]**，然后导航到您要将视频配置文件从中删除的文件夹。
1. 在文件夹中，点按复选标记以将其选中，然后点按&#x200B;**[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 视频配置文件]**&#x200B;选项卡，从下拉菜单中选择&#x200B;**[!UICONTROL 无]**，然后单击&#x200B;**[!UICONTROL 保存并关闭]**。如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
