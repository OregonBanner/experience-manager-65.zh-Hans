---
title: 管理视频资产
description: 在 [!DNL Adobe Experience Manager]中上传、预览、批注和发布视频资产。
contentOwner: AG
role: Business Practitioner
feature: Asset Management
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 11%

---


# 管理视频资产 {#manage-video-assets}

视频格式是组织数字资产的关键部分。 [!DNL Adobe Experience Manager] 优惠可以提供成熟的产品和功能，在视频资产创建后对其整个生命周期进行管理。

了解如何在[!DNL Adobe Experience Manager Assets]中管理和编辑视频资产。 通过使用[!DNL Dynamic Media]集成，可以进行视频编码和转码，例如FFmpeg转码。

## 上传和预览视频资产{#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 为扩展名为MP4的视频资源生成预览。如果资产的格式不是MP4，请安装FFmpeg包以生成预览。 FFmpeg可创建OGG和MP4类型的视频演绎版。 您可以在[!DNL Assets]用户界面中预览再现。

1. 在数字资产文件夹或子文件夹中，导航到要添加数字资产的位置。
1. 要上传资产，请单击工具栏中的&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 文件]**。 或者，在用户界面上拖动文件。 有关详细信息，请参阅[上传资产](manage-assets.md#uploading-assets)。
1. 要在卡片视图中预览视频，请单击视频资产上的&#x200B;**[!UICONTROL 播放]** ![播放选项](assets/do-not-localize/play.png)选项。 您只能在卡视图中暂停或播放视频。 [!UICONTROL 播放]和[!UICONTROL 暂停]选项在列表视图中不可用。

1. 要在资产详细信息页面中预览视频，请单击卡上的&#x200B;**[!UICONTROL 编辑]**。 视频会在浏览器自带的视频播放器中播放。您可以播放视频，暂停视频，控制视频音量，以及将视频放大到全屏。

   ![视频播放控件](assets/video-playback-controls.png)

## 上传大于2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}的资产的配置

默认情况下，[!DNL Assets]不允许您上传任何大于2 GB的资产，因为文件大小限制。 但是，可以通过进入CRXDE Lite并在`/apps`目录下创建节点来覆盖此限制。 节点必须具有相同的节点名称、目录结构和顺序的可比节点属性。

除[!DNL Assets]配置外，更改以下配置以上传大资产：

* 增加令牌过期时间。 请参阅Web控制台中`https://[aem_server]:[port]/system/console/configMgr`的[!UICONTROL AdobeGranite CSRF Servlet]。 有关详细信息，请参阅[CSRF保护](/help/sites-developing/csrf-protection.md)。
* 增加Dispatcher配置中的`receiveTimeout`。 有关详细信息，请参阅[Experience Manager调度程序配置](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)。

>[!NOTE]
>
>[!DNL Experience Manager]经典用户界面没有2-GB文件大小限制。 此外，大型视频的端到端工作流程也不完全受支持。

要配置更高的文件大小限制，请在`/apps`目录中执行以下步骤。

1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**。
1. 在CRXDE Lite中，导航到`/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`。 要查看目录窗口，请单击`>>`。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 叠加节点]**。 或者，从上下文菜单中选择&#x200B;**[!UICONTROL 覆盖节点]**。
1. 在&#x200B;**[!UICONTROL 叠加节点]**&#x200B;对话框中，单击&#x200B;**[!UICONTROL 确定]**。

   ![叠加节点](assets/overlay-node-path.png)

1. 刷新浏览器。 叠加节点`/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`已选中。
1. 在&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡中，以字节为单位输入适当的值，将大小限制增加到所需大小。 例如，要将大小限制增加到30 GB，请输入`32212254720`值。

1. 在工具栏中，单击&#x200B;**[!UICONTROL 全部保存]**。
1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在[!DNL Adobe Experience Manager] [!UICONTROL Web控制台包]页面的表的“名称”列下，找到并单击&#x200B;**[!UICONTROL AdobeGranite工作流外部进程作业处理程序]**。
1. 在[!UICONTROL AdobeGranite工作流外部进程作业处理程序]页面上，将&#x200B;**[!UICONTROL 默认超时]**&#x200B;和&#x200B;**[!UICONTROL 最大超时]**&#x200B;字段的秒数设置为`18000`（五小时）。 单击&#x200B;**[!UICONTROL 保存]**。
1. 在[!DNL Experience Manager]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在“工作流模型”页面上，选择&#x200B;**[!UICONTROL Dynamic Media编码视频]**，然后单击&#x200B;**[!UICONTROL 编辑]**。
1. 在工作流页面上，多次单击&#x200B;**[!UICONTROL Dynamic Media视频服务进程]**&#x200B;组件。
1. 在[!UICONTROL 步骤属性]对话框的&#x200B;**[!UICONTROL 常用]**&#x200B;选项卡下，展开&#x200B;**高级设置**。
1. 在&#x200B;**[!UICONTROL 超时]**&#x200B;字段中，指定值`18000`，然后单击&#x200B;**[!UICONTROL 确定]**&#x200B;返回至&#x200B;**[!UICONTROL Dynamic Media编码视频]**&#x200B;工作流页。
1. 在页面顶部附近，在[!UICONTROL Dynamic Media编码视频]页面标题下，单击&#x200B;**[!UICONTROL 保存]**。

## 发布视频资产{#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中或直接嵌入资产。 有关详细信息，请参阅[发布Dynamic Media资产](/help/assets/publishing-dynamicmedia-assets.md)。

## 注释视频资产{#annotate-video-assets}

1. 从[!DNL Assets]控制台中，选择资产卡上的&#x200B;**[!UICONTROL 编辑]**&#x200B;以显示资产详细信息页面。
1. 要播放视频，请单击&#x200B;**[!UICONTROL 预览]**。
1. 要对视频添加注释，请单击&#x200B;**[!UICONTROL 注释]**。 注释会在视频中的特定时间（帧）添加。 添加注释时，您可以在画布上绘制图像，并在绘图中加入注释。 注释会自动保存。 要退出注释向导，请单击&#x200B;**[!UICONTROL 关闭]**。

   ![在视频帧上绘制和添加注释](assets/annotate-video.png)

1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。

   ![搜索视频中要跳过指定秒数的时间](assets/seek-in-video.png)

1. 要在时间轴中视图它，请单击注释。 要从时间轴中删除注释，请单击&#x200B;**[!UICONTROL 删除]**。

   ![视图注释和时间轴中的详细信息](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [管理Experience Manager资产中的数字资产](/help/assets/manage-assets.md)
>* [在Experience Manager资产中管理收藏集](/help/assets/manage-collections.md)
>* [Dynamic Media视频文档](/help/assets/video.md)。

