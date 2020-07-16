---
title: 适用于社区的FFmpeg
seo-title: 适用于社区的FFmpeg
description: 如何为社区安装和配置FFmpeg
seo-description: 如何为社区安装和配置FFmpeg
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: cbb5a6bac5e9932fd36abf20d4424890080d39bf
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# 适用于社区的FFmpeg {#ffmpeg-for-communities}

## 概述 {#overview}

FFmpeg是用于转换和流式传输音频和视频的解决方案，安装后可用于对视频资源进行正确 [转码](../../help/sites-authoring/default-components-foundation.md#video) ，以及AEM Communities支持功能。

在创作环境中使用FFmpeg获取已上传的启用资源的元数据，并在列出启用资源时生成要显示的缩略图。

## 安装 FFmpeg {#installing-ffmpeg}

FFmpeg应安装在承载AEM作者实 *例* 的服务器上。

1. 请访问 [https://www.ffmpeg.org](https://www.ffmpeg.org/)。
1. 下载适用于您的特定环境（Macintosh、Windows或Linux）的最新版FFmpeg。

   * 由于旧版本中存在安全漏洞，因此务必使FFmpeg保持最新。

1. 按照操作系统的说明安装FFmpeg。

1. 确保在系统路径中设置FFmpeg可执行文件。

   您应该能够从系统中的任何目录运行FFmpeg。

   * For example, `ffmpeg -version`.

## 配置FFmpeg转码服务 {#configure-ffmpeg-transcoding-service}

默认情况下，安装FFmpeg后，会根据DAM更新资产工作流定义配置多个再 [!UICONTROL 现(转码] )。

由于转换占用CPU大量，建议修改目标再现的列表。 在大多数情况下，无需转码。

要修改DAM更 [!UICONTROL 新资产工作流] ，并在此示例中，请关闭转码：

* 以管理权限登录创作实例。
* 在全局导航中，导航到 **[!UICONTROL 工具]** >工 **[!UICONTROL 作流]** > **[!UICONTROL 模型]**。
* 找到 **[!UICONTROL DAM更新资产]**。
* 多次单击以打开要在经典UI中编辑的工作流。

   结果位置： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 多次单击 **[!UICONTROL FFmpeg转码]** 步骤以访问“步骤属性”对话框。
* 在“流程 **[!UICONTROL ”选项卡]** 下：

   * **[!UICONTROL 文章]**: 清除所有条目以禁用转码默认值： `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

   ![chlimage_1-372](assets/chlimage_1-372.png)

* 选择 **[!UICONTROL “确定]** ”以关闭 `Step Properties` 对话框。

* 选择 **[!UICONTROL 保存]** ，以保存工 `DAM Update Asset` 作流。



