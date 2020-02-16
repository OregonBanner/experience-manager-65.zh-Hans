---
title: 视频演绎版
description: 视频演绎版
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
translation-type: tm+mt
source-git-commit: 66f46a34832254af74c72da16ec8ebe3eb8cd46d

---


# Video renditions {#video-renditions}

Adobe Experience Manager(AEM)资产可为各种格式（包括OGG、FLV等）的视频资产生成视频演绎版。

AEM 资产支持媒体资产的静态和动态演绎版（DM 编码的演绎版）。

静态演绎版是使用FFMPEG（在系统路径上安装并可用）本机生成的，并存储在内容存储库中。

DM编码的演绎版存储在代理服务器中，并在运行时提供。

AEM资产在客户端为这些演绎版提供播放支持。

要查看特定视频资产的演绎版，请打开其资产页面，然后点按全局导航图标。 然后，从列 **[!UICONTROL 表中选]** 择演绎版。

![chlimage_1-478](assets/chlimage_1-478.png)

视频演绎版列表显示在“演绎版” **[!UICONTROL 面板中]** 。

![chlimage_1-479](assets/chlimage_1-479.png)

要为DM编码的演绎版配置代理服务器，请 [配置Dynamic Media cloud服务。](config-dynamic.md)

To generate video renditions with desired parameters, [create a corresponding video profile](video-profiles.md).

配置代理服务器并创建视频配置文件后，您可以将此视频预设包含在处理配置文件中，并将处理配置文件应用到文件夹。

>[!NOTE]
>
>在Microsoft Internet Explorer 11上，音频播放不适用于OGG和WAV文件。 对于扩展 `Invalid Source` 名为OGG或WAV的资产，资产详细信息页面上会显示一个错误。
>
>在MS edge和iPad上，OGG文件不播放并引发不支持的格式错误。
