---
title: 管理视频资源
description: 在中上传、预览、注释和发布视频资产 [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 11%

---

# 管理视频资源 {#manage-video-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/managing-video-assets.html?lang=en) |

视频格式是组织数字资产的重要组成部分。 [!DNL Adobe Experience Manager] 提供成熟的产品和功能，用于在创建视频资产后管理其整个生命周期。

了解如何在中管理和编辑视频资产 [!DNL Adobe Experience Manager Assets]. 视频编码和转码，例如FFmpeg转码，可以使用 [!DNL Dynamic Media] 集成。

## 上传和预览视频资产 {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] 为扩展名为MP4的视频资源生成预览。 如果资产的格式不是MP4，请安装FFmpeg包以生成预览。 FFmpeg创建OGG和MP4类型的视频演绎版。 您可以在中预览演绎版 [!DNL Assets] 用户界面。

1. 在数字资产文件夹或子文件夹中，导航到要添加数字资产的位置。
1. 要上传资产，请单击 **[!UICONTROL 创建]** 从工具栏中选择 **[!UICONTROL 文件]**. 或者，在用户界面上拖动文件。 参见 [上传资产](manage-assets.md#uploading-assets) 了解详细信息。
1. 要在卡片视图中预览视频，请单击 **[!UICONTROL 播放]** ![播放选项](assets/do-not-localize/play.png) 选项。 您只能在卡片视图中暂停或播放视频。 此 [!UICONTROL 播放] 和 [!UICONTROL 暂停] 选项在列表视图中不可用。

1. 要在资源详细信息页面中预览视频，请单击 **[!UICONTROL 编辑]** 在卡片上。 视频会在浏览器自带的视频播放器中播放。您可以播放视频，暂停视频，控制视频音量，以及将视频放大到全屏。

   ![视频播放控制](assets/video-playback-controls.png)

## 用于上传大于2 GB的资产的配置 {#configuration-to-upload-assets-that-are-larger-than-gb}

默认情况下， [!DNL Assets] 不允许您上传任何因文件大小限制而大于2 GB的资产。 但是，您可以通过进入CRXDE Lite并在下创建节点来覆盖此限制 `/apps` 目录。 节点必须具有相同的节点名称、目录结构和顺序的可比较节点属性。

除此之外 [!DNL Assets] 配置，更改以下配置以上传大型资产：

* 增加令牌过期时间。 参见 [!UICONTROL AdobeGranite CSRF Servlet] 在Web控制台中的 `https://[aem_server]:[port]/system/console/configMgr`. 有关更多信息，请参阅 [CSRF保护](/help/sites-developing/csrf-protection.md).
* 增加 `receiveTimeout` 在Dispatcher配置中。 有关更多信息，请参阅 [Experience ManagerDispatcher配置](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>此 [!DNL Experience Manager] 传统用户界面没有2 GB文件大小限制。 此外，不完全支持大型视频的端到端工作流。

要配置更高的文件大小限制，请在 `/apps` 目录。

1. In [!DNL Experience Manager]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.
1. 在CRXDE Lite中，导航到 `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. 要查看目录窗口，请单击 `>>`.
1. 在工具栏中，单击 **[!UICONTROL 覆盖节点]**. 或者，从上下文菜单中选择&#x200B;**[!UICONTROL 覆盖节点]**。
1. 在 **[!UICONTROL 覆盖节点]** 对话框，单击 **[!UICONTROL 确定]**.

   ![覆盖节点](assets/overlay-node-path.png)

1. 刷新浏览器。 覆盖节点 `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` 已选中。
1. 在 **[!UICONTROL 属性]** 选项卡，以字节为单位输入相应的值，以将大小限制增加到所需的大小。 例如，要将大小限制增加到30 GB，请输入 `32212254720` 值。

1. 在工具栏中，单击 **[!UICONTROL 全部保存]**.
1. In [!DNL Experience Manager]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.
1. 在 [!DNL Adobe Experience Manager] [!UICONTROL Web控制台包] 在表的“名称”列下，找到并单击 **[!UICONTROL AdobeGranite工作流外部进程作业处理程序]**.
1. 在 [!UICONTROL AdobeGranite工作流外部进程作业处理程序] 页面，为两者设置秒数 **[!UICONTROL 默认超时]** 和 **[!UICONTROL 最大超时]** 字段至 `18000` （5小时）。 单击“**[!UICONTROL 保存]**”。
1. In [!DNL Experience Manager]，单击 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 在“工作流模型”页面上，选择 **[!UICONTROL Dynamic Media编码视频]**，然后单击 **[!UICONTROL 编辑]**.
1. 在工作流页面上，双击 **[!UICONTROL Dynamic Media视频服务进程]** 组件。
1. 在[!UICONTROL 步骤属性]对话框的&#x200B;**[!UICONTROL 常用]**&#x200B;选项卡下，展开&#x200B;**高级设置**。
1. 在 **[!UICONTROL 超时]** 字段，指定值 `18000`，然后单击 **[!UICONTROL 确定]** 以返回 **[!UICONTROL Dynamic Media编码视频]** 工作流页面。
1. 在页面顶部附近，在 [!UICONTROL Dynamic Media编码视频] 页面标题，单击 **[!UICONTROL 保存]**.

## 发布视频资产 {#publish-video-assets}

发布后，您可以将视频资产作为URL包含在网页中，也可以直接嵌入这些资产。 有关详细信息，请参阅 [发布Dynamic Media资源](/help/assets/publishing-dynamicmedia-assets.md).

## 为视频资源作批注 {#annotate-video-assets}

1. 从 [!DNL Assets] 控制台，选择 **[!UICONTROL 编辑]** 以显示“资产详细信息”页面。
1. 要播放视频，请单击 **[!UICONTROL 预览]**.
1. 要对视频添加批注，请单击 **[!UICONTROL 批注]**. 在视频中的特定时间（帧）添加注释。 在注释时，可以在画布上绘制并在绘图中包括注释。 评论将自动保存。 要退出注释向导，请单击 **[!UICONTROL 关闭]**.

   ![在视频帧上绘制和批注](assets/annotate-video.png)

1. 搜索到视频中的特定点，在&#x200B;**文本**&#x200B;字段中指定时间（以秒为单位），然后单击&#x200B;**跳转**。例如，要跳过视频的前 20 秒，请在文本字段中输入 20。

   ![搜寻视频中的时间以跳过指定的秒数](assets/seek-in-video.png)

1. 要在时间轴中查看注释，请单击注释。 要从时间轴中删除注释，请单击 **[!UICONTROL 删除]**.

   ![在时间轴中查看注释和详细信息](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [在Experience Manager Assets中管理数字资源](/help/assets/manage-assets.md)
>* [在Experience Manager Assets中管理收藏集](/help/assets/manage-collections.md)
>* [Dynamic Media视频文档](/help/assets/video.md).

