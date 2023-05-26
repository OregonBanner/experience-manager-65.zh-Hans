---
title: 适用于社区的FFmpeg
seo-title: FFmpeg for Communities
description: 如何安装和配置适用于社区的FFmpeg
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# 适用于社区的FFmpeg {#ffmpeg-for-communities}

## 概述 {#overview}

FFmpeg是一种用于转换和流式传输音频和视频的解决方案，在安装后用于正确的转码 [视频资产](../../help/sites-authoring/default-components-foundation.md#video).

## 安装FFmpeg {#installing-ffmpeg}

FFmpeg应安装在托管AEM的服务器上 *作者* 实例。

1. 转到 [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. 针对您的特定环境（Macintosh、Windows或Linux）下载最新版本的FFmpeg。

   * 由于旧版本中存在安全漏洞，请务必保持FFmpeg处于最新状态。

1. 按照操作系统的说明安装FFmpeg。

1. 确保在系统路径中设置了FFmpeg可执行文件。

   您应该能够从系统中的任何目录运行FFmpeg。

   * 例如：`ffmpeg -version`。

## 配置FFmpeg转码服务 {#configure-ffmpeg-transcoding-service}

默认情况下，在安装FFmpeg时，将根据 [!UICONTROL DAM更新资产] 工作流定义。

由于转码占用大量CPU，因此建议修改目标演绎版列表。 在大多数情况下，不需要转码。

要修改 [!UICONTROL DAM更新资产] 工作流，在本例中，要关闭转码，请执行以下操作：

* 使用管理权限登录创作实例。
* 在全局导航中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
* 查找 **[!UICONTROL DAM更新资产]**.
* 双击以打开工作流，以便在经典UI中进行编辑。

   结果位置： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 双击 **[!UICONTROL FFmpeg转码]** 步骤以访问步骤属性对话框。
* 在 **[!UICONTROL 进程]** 选项卡：

   * **[!UICONTROL arguments]**：清除所有条目以禁用转码默认值： `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 选择 **[!UICONTROL 确定]** 关闭 `Step Properties` 对话框。

* 选择 **[!UICONTROL 保存]** 以保存 `DAM Update Asset` 工作流。
