---
title: 适用于社区的FFmpeg
seo-title: 适用于社区的FFmpeg
description: 如何安装和配置用于社区的FFmpeg
seo-description: 如何安装和配置用于社区的FFmpeg
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Administrator
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 用于社区的FFmpeg {#ffmpeg-for-communities}

## 概述 {#overview}

FFmpeg是用于转换和流式传输音频和视频的解决方案，安装后，可用于对[视频资产](../../help/sites-authoring/default-components-foundation.md#video)进行正确转码，以及AEM Communities的启用功能。

FFmpeg可在创作环境中用来获取已上传启用资源的元数据，并在列出启用资源时生成要显示的缩略图。

## 安装 FFmpeg {#installing-ffmpeg}

应在托管AEM *author*&#x200B;实例的服务器上安装FFmpeg。

1. 转到[https://www.ffmpeg.org](https://www.ffmpeg.org/)。
1. 下载适用于您的特定环境（Macintosh、Windows或Linux）的FFmpeg最新版本。

   * 由于旧版本中存在安全漏洞，因此务必保持FFmpeg为最新。

1. 按照操作系统的说明安装FFmpeg。

1. 确保在系统路径中设置了FFmpeg可执行文件。

   您应该能够从系统中的任何目录运行FFmpeg。

   * 例如，`ffmpeg -version`。

## 配置FFmpeg转码服务{#configure-ffmpeg-transcoding-service}

默认情况下，安装FFmpeg后，将根据[!UICONTROL DAM更新资产]工作流定义配置多个演绎版（转码）。

由于转码占用大量CPU，因此建议修改目标演绎版列表。 在大多数情况下，无需转码。

要修改[!UICONTROL DAM更新资产]工作流，并在此示例中，关闭转码：

* 使用管理权限登录到创作实例。
* 在全局导航中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
* 找到&#x200B;**[!UICONTROL DAM更新资产]**。
* 双击以打开要在经典UI中编辑的工作流。

   生成位置：[http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 双击&#x200B;**[!UICONTROL FFmpeg转码]**&#x200B;步骤以访问步骤属性对话框。
* 在&#x200B;**[!UICONTROL Process]**&#x200B;选项卡下：

   * **[!UICONTROL 参数]**:清除所有条目以禁用转码默认值：  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 选择&#x200B;**[!UICONTROL OK]**&#x200B;以关闭`Step Properties`对话框。

* 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存`DAM Update Asset`工作流。
