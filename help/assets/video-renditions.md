---
title: 视频演绎版
description: 视频演绎版
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# 视频演绎版 {#video-renditions}

Adobe Experience Manager Assets可为各种格式（包括OGG、FLV等）的视频资产生成视频演绎版。

Experience Manager Assets支持媒体资产的静态和动态演绎版（DM编码的演绎版）。

静态演绎版是使用FFMPEG（在系统路径上安装并可用）在本地生成的，并存储在内容存储库中。

DM编码的演绎版存储在代理服务器中，并在运行时提供。

Experience Manager Assets在客户端为这些演绎版提供播放支持。

要查看特定视频资产的演绎版，请打开其资产页面，然后选择全局导航图标。 然后，选择 **[!UICONTROL 演绎版]** 列表。

![chlimage_1-478](assets/chlimage_1-478.png)

视频演绎版的列表显示在 **[!UICONTROL 演绎版]** 的上界。

![chlimage_1-479](assets/chlimage_1-479.png)

要为DM编码的演绎版配置代理服务器，请执行以下操作： [配置Dynamic Media云服务](config-dynamic.md).

要使用所需的参数生成视频演绎版，请执行以下操作： [创建相应的视频配置文件](video-profiles.md).

配置代理服务器并创建视频配置文件后，您可以将此视频预设包含在处理配置文件中，并将处理配置文件应用到文件夹。

>[!NOTE]
>
>Microsoft® Internet Explorer 11上的OGG和WAV文件无法播放音频。 错误 `Invalid Source` 在扩展名为OGG或WAV的资产的资产的资产详细信息页面上显示。
>
>在MS® Edge和iPad上，OGG文件不播放，并引发不受支持的格式错误。
