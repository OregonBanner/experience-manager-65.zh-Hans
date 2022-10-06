---
title: 适用于社区的FFmpeg
seo-title: FFmpeg for Communities
description: 如何安装和配置用于社区的FFmpeg
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# 适用于社区的FFmpeg {#ffmpeg-for-communities}

## 概述 {#overview}

FFmpeg是一种用于转换和流式传输音频和视频的解决方案，安装后可用于对 [视频资产](../../help/sites-authoring/default-components-foundation.md#video) 以及AEM社区启用功能。

FFmpeg可在创作环境中用来获取已上传启用资源的元数据，并在列出启用资源时生成要显示的缩略图。

## 安装 FFmpeg {#installing-ffmpeg}

应在托管AEM的服务器上安装FFmpeg *作者* 实例。

1. 转到 [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. 下载适用于您的特定环境（Macintosh、Windows或Linux）的FFmpeg最新版本。

   * 由于旧版本中存在安全漏洞，因此务必保持FFmpeg为最新。

1. 按照操作系统的说明安装FFmpeg。

1. 确保在系统路径中设置了FFmpeg可执行文件。

   您应该能够从系统中的任何目录运行FFmpeg。

   * 例如：`ffmpeg -version`。

## 配置FFmpeg转码服务 {#configure-ffmpeg-transcoding-service}

默认情况下，安装FFmpeg后，会根据 [!UICONTROL DAM更新资产] 工作流定义。

由于转码占用大量CPU，因此建议修改目标演绎版列表。 在大多数情况下，无需转码。

修改 [!UICONTROL DAM更新资产] 工作流，在本例中，要关闭转码，请执行以下操作：

* 使用管理权限登录到创作实例。
* 从全局导航中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
* 定位 **[!UICONTROL DAM更新资产]**.
* 双击以打开要在经典UI中编辑的工作流。

   生成位置： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 双击 **[!UICONTROL FFmpeg转码]** 步骤以访问“步骤属性”对话框。
* 在 **[!UICONTROL 进程]** 选项卡：

   * **[!UICONTROL 项目]**:清除所有条目以禁用转码默认值： `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 选择 **[!UICONTROL 确定]** 关闭 `Step Properties` 对话框。

* 选择 **[!UICONTROL 保存]** 保存 `DAM Update Asset` 工作流。
