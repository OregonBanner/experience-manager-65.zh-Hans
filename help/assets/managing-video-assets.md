---
title: 管理视频资产
description: 了解如何上传、预览、批注和发布视频资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 管理视频资产 {#manage-video-assets}

了解如何在Adobe Experience Manager(AEM)资产中管理和编辑视频资产。 此外，如果您获得使用Dynamic Media的许可，请参阅 [Dynamic media视频文档](/help/assets/video.md)。

## 上传和预览视频资产 {#upload-and-preview-video-assets}

Adobe Experience Manager资产可生成扩展为MP4的视频资产的预览。如果资产的格式不是MP4，请安装FFmpeg包以生成预览。FFmpeg创建OGG和MP4类型的视频演绎版。 您可以在AEM资产用户界面中预览这些演绎版。

1. 在“数字资产”文件夹或子文件夹中，导览至要添加数字资产的位置。
1. 要上传资产，请单击或点按工 **[!UICONTROL 具栏中]** 的创建，然后选择 **[!UICONTROL 文件]**。 或者，直接将其拖放到资产区域。 See [Uploading assets](managing-assets-touch-ui.md#uploading-assets) for details around the upload operation.
1. To preview a video in the Card view, tap the **[!UICONTROL Play]** button on the video asset.

   ![chlimage_1-65](assets/chlimage_1-201.png)

   您只能在卡片视图中暂停或播放视频。 “播 [!UICONTROL 放] ”和“ [!UICONTROL 暂停] ”按钮在列表视图中不可用。

1. 要在资产详细信息页面中预览视频，请单击或点按卡 **[!UICONTROL 上的]** “编辑”图标。

   视频会在浏览器自带的视频播放器中播放。您可以播放视频，暂停视频，控制视频音量，以及将视频放大到全屏。

   ![chlimage_1-66](assets/chlimage_1-202.png)

## 用于上传大于2 GB的资产的配置 {#configuration-to-upload-assets-that-are-larger-than-gb}

默认情况下，Experience Manager资产不允许您上传任何大于2 GB的资产，因为文件大小限制。 但是，您可以通过进入CRXDE Lite并在目录下创建一个节点来覆盖此限 `/apps` 制。 该节点必须具有相同的节点名称、目录结构和可比的节点属性。

除了Experience Manager资产配置之外，还要更改以下配置以上传大资产：

* 增加令牌到期时间。 请参 [!UICONTROL 阅Web控制台中的] Adobe Granite CSRF Servlet `https://[aem_server]:[port]/system/console/configMgr`，网址为。 有关详细信息，请参 [阅CSRF保护](/help/sites-developing/csrf-protection.md)。
* 增加调 `receiveTimeout` 度程序配置。 有关详细信息，请参 [阅Experience Manager Dispatcher配置](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)。

>[!NOTE]
>
>AEM Classic用户界面没有2 GB文件大小限制。 此外，大型视频的端对端工作流程不完全受支持。

要配置更高的文件大小限制，请在目录中执行以下 `/apps` 步骤。

1. 在AEM中，点按工 **[!UICONTROL 具]** >常 **[!UICONTROL 规]** > **[!UICONTROL CRXDE Lite]**。
1. 在CRXDE Lite中，导航到 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`。 要查看目录窗口，请触摸图 `>>` 标。
1. 在工具栏中，点按叠 **[!UICONTROL 加节点]**。 或者，从上 **[!UICONTROL 下文菜单中选择]** “叠加节点”。
1. 在“叠加 **[!UICONTROL 节点”对话框中]** ，点按 **[!UICONTROL 确定]**。

   ![chlimage_1-67](assets/chlimage_1-203.png)

1. 刷新浏览器。 叠加节 `/jcr_root/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 点被选中。
1. 在“属 **[!UICONTROL 性]** ”选项卡中，输入相应的字节值，以将大小限制增加到所需大小。 例如，要将大小限制增加到30 GB，请输入 `{sizeLimit : "32212254720"}` 值。

1. 在工具栏中，点按保 **[!UICONTROL 存全部]**。
1. 在AEM中，点按工 **[!UICONTROL 具]** >操 **[!UICONTROL 作]** > **[!UICONTROL Web控制台]**。
1. 在Adobe Experience Manager Web Console捆绑包页面的表的“名称”列下，找到并点按 **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**。
1. 在Adobe Granite Workflow外部进程作业处理程序页面中，将默认超时和最大超时 **[!UICONTROL 字段的秒数设]******`18000` 置为（5小时）。
1. 点按&#x200B;**[!UICONTROL 保存]**。
1. 在AEM中，点按工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流]** > **[!UICONTROL 模型]**。
1. 在“工作流模型”页面上，选择“ **[!UICONTROL Dynamic Media编码视频]**”，然后点按 **[!UICONTROL 编辑]**。
1. 在工作流页面上，双击Dynamic Media视频 **[!UICONTROL 服务进程组件]** 。
1. 在“步 [!UICONTROL 骤属性] ”对话框的“常用”选 **[!UICONTROL 项卡下]** ，展开“ **高级设置”**。
1. 在“超 **[!UICONTROL 时]** ”字段中，指定值 `18000`，然后点按“确 **[!UICONTROL 定]** ”以返回到“Dynamic Media编码视频 **** ”工作流页。
1. 在页面顶部附近的Dynamic Media编码视频页面标题下，点按保 **[!UICONTROL 存]**。

## 发布视频资产 {#publish-video-assets}

发布视频资产后，您便可以通过URL或在网页上嵌入这些资产，以将其包含在网页中。 See [publishing assets](/help/assets/publishing-dynamicmedia-assets.md).

## 注释视频资产 {#annotate-video-assets}

1. 在“资产”控制台中，单击或点按资 [!UICONTROL 产卡上的] “编辑”图标以显示资产详细信息页面。
1. 要播放视频，请单击或点按“预 [!UICONTROL 览] ”图标。
1. 要对视频添加注释，请单击“注 **[!UICONTROL 释]** ”按钮。 注释会添加到视频中的特定时间点（帧）。添加注释时，您可以在画布上绘图，并在绘图中加入注释。 注释将自动保存。

   ![chlimage_1-68](assets/chlimage_1-204.png)

   要退出注释向导，请单击“关 **[!UICONTROL 闭”]**。

1. Seek to a specific point in the video, specify the time in seconds in the **text** field and click **Jump**. 例如，要跳过视频的前 20 秒，请在文本字段中输入 10。

   ![chlimage_1-69](assets/chlimage_1-205.png)

1. 要在时间轴中查看它，请单击注释。 要从时间轴中删除注释，请单击“删 **[!UICONTROL 除”]**。

   ![chlimage_1-70](assets/chlimage_1-206.png)
