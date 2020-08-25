---
title: 在中管理视频资产 [!DNL Adobe Experience Manager]。
description: 在中上传、预览、批注和发布视频资产 [!DNL Adobe Experience Manager]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 268689d534f8bf649335269f9169455c381f9554
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 10%

---


# 管理视频资产 {#manage-video-assets}

视频格式是组织数字资产的关键部分。 [!DNL Adobe Experience Manager] 优惠可以提供成熟的产品和功能，在视频资产创建后管理其整个生命周期。

了解如何在中管理和编辑视频资 [!DNL Adobe Experience Manager Assets]产。 此外，如果您获得使用许可， [!DNL Dynamic Media]请参阅Dynamic [Media视频文档](/help/assets/video.md)。

## 上传和预览视频资产 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 为扩展名为MP4的视频资产生成预览。 如果资产的格式不是MP4，请安装FFmpeg包以生成预览。 FFmpeg创建OGG和MP4类型的视频演绎版。 您可以在用户界面中预览 [!DNL Assets] 再现。

1. 在数字资产文件夹或子文件夹中，导航到要添加数字资产的位置。
1. 要上传资产，请单击工 **[!UICONTROL 具栏]** 中的创建，然后选择 **[!UICONTROL 文件]**。 或者，直接将其拖放到资产区域。 See [upload assets](managing-assets-touch-ui.md#uploading-assets) for details around the upload operation.
1. To preview a video in the Card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. 您只能在卡视图中暂停或播放视频。 “播 [!UICONTROL 放] ”和“ [!UICONTROL 暂停] ”选项在列表视图中不可用。

1. 要预览资产详细信息页面中的视频，请单 **[!UICONTROL 击]** 卡上的编辑。 视频会在浏览器自带的视频播放器中播放。您可以播放视频，暂停视频，控制视频音量，以及将视频放大到全屏。

   ![视频播放控件](assets/video-playback-controls.png)

## 上传大于2 GB的资产的配置 {#configuration-to-upload-assets-that-are-larger-than-gb}

默认情 [!DNL Assets] 况下，您不会上传任何大于2 GB的资产，因为文件大小限制。 但是，您可以通过进入CRXDE Lite并在目录下创建节点来覆盖此 `/apps` 限制。 该节点必须具有相同的节点名称、目录结构和可比的节点属性。

除了配置 [!DNL Assets] 之外，还要更改以下配置以上传大型资产：

* 增加令牌过期时间。 请参 [!UICONTROL 阅在Web控制台中Adobe] Granite CSRF Servlet `https://[aem_server]:[port]/system/console/configMgr`，网址为。 有关详细信息，请参 [阅CSRF保护](/help/sites-developing/csrf-protection.md)。
* 增加调 `receiveTimeout` 度程序配置。 有关详细信息，请参阅 [Experience Manager调度程序配置](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)。

>[!NOTE]
>
>经 [!DNL Experience Manager] 典用户界面没有2-GB文件大小限制。 此外，大型视频的端对端工作流程不完全受支持。

要配置更高的文件大小限制，请在目录中执行以下 `/apps` 步骤。

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. 在CRXDE Lite中，导航到 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`。 要查看目录窗口，请单击 `>>`。
1. From the toolbar, click the **[!UICONTROL Overlay Node]**. 或者，从上下文菜单中选择&#x200B;**[!UICONTROL 覆盖节点]**。
1. In the **[!UICONTROL Overlay Node]** dialog, click **[!UICONTROL OK]**.

   ![叠加节点](assets/overlay-node-path.png)

1. 刷新浏览器。 叠加节 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 点被选中。
1. 在“属 **[!UICONTROL 性]** ”选项卡中，输入相应的字节值，将大小限制增加到所需大小。 例如，要将大小限制增加到30 GB，请输入 `32212254720` 值。

1. 在工具栏中，单击“保 **[!UICONTROL 存全部”]**。
1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. 在Web控 [!DNL Adobe Experience Manager] 制台 [!UICONTROL 的“捆绑包”页面] ，在表的“名称”列下，找到并单击“AdobeGranite Workflow External Process Job Handler”(Granite工作 **[!UICONTROL 流外部进程作业处理程序)]**。
1. On the [!UICONTROL Adobe Granite Workflow External Process Job Handler] page, set the seconds for both **[!UICONTROL Default Timeout]** and **[!UICONTROL Max Timeout]** fields to `18000` (five hours). 单击&#x200B;**[!UICONTROL 保存]**。
1. 在中， [!DNL Experience Manager]单击“ **[!UICONTROL 工具]** ”>“ **[!UICONTROL 工作流]** ”>“ **[!UICONTROL 模型]**”。
1. 在“工作流模型”页面上，选 **[!UICONTROL 择Dynamic Media编码视频]**，然后单击 **[!UICONTROL 编辑]**。
1. 在工作流页面上，多次并单 **[!UICONTROL 击Dynamic Media视频服务流程组]** 件。
1. 在[!UICONTROL 步骤属性]对话框的&#x200B;**[!UICONTROL 常用]**&#x200B;选项卡下，展开&#x200B;**高级设置**。
1. In the **[!UICONTROL Timeout]** field, specify a value of `18000`, then click **[!UICONTROL OK]** to return to the **[!UICONTROL Dynamic Media Encode Video]** workflow page.
1. 在页面顶部附近的Dynamic Media编码视 [!UICONTROL 频页面标题下] ，单击 **[!UICONTROL 保存]**。

## 发布视频资产 {#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中或直接嵌入资产。 有关详细信息，请 [参阅发布Dynamic Media资产](/help/assets/publishing-dynamicmedia-assets.md)。

## 注释视频资产 {#annotate-video-assets}

1. 在控制 [!DNL Assets] 台中，单 [!UICONTROL 击资产] 卡上的编辑以显示资产详细信息页面。
1. 要播放视频，请单击 [!UICONTROL 预览]。
1. 要对视频添加注释，请单击“注 **[!UICONTROL 释]** ”按钮。 注释会在视频中的特定时间（帧）添加。 添加注释时，您可以在画布上绘图，并在绘图中包含注释。 注释将自动保存。

   ![在视频帧上绘制和添加注释](assets/annotate-video.png)

   要退出注释向导，请单击“关 **[!UICONTROL 闭”]**。

1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。

   ![在视频中搜索时间以跳过指定秒数](assets/seek-in-video.png)

1. 要在时间轴中视图它，请单击注释。 要从时间轴中删除注释，请单击“ **[!UICONTROL 删除]**”。

   ![视图注释和时间轴中的详细信息](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [管理Experience Manager资产中的数字资产](/help/assets/managing-assets-touch-ui.md)
>* [管理Experience Manager资产中的收藏集](/help/assets/managing-collections-touch-ui.md)

