---
title: 配置视频组件
seo-title: 配置视频组件
description: 了解如何配置视频组件。
seo-description: 了解如何配置视频组件。
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
translation-type: tm+mt
source-git-commit: 535a175486a2d0f31762d71954c4fead2ef246e1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# 配置视频组件 {#configure-the-video-component}

通 [过视频](/help/sites-authoring/default-components-foundation.md#video) 组件，您可以将预定义的现成(OOTB)视频资产放在页面上。

为了进行正确的转码，管理员单独安装FFmpeg。 请参 [阅安装FFmpeg和配置AEM](#install-ffmpeg)。 Administrators also [Configure Video Profiles](#configure-video-profiles) for use with HTML5 elements.

## 配置视频用户档案 {#configure-video-profiles}

要使用HTML5元素，请定义视频用户档案。 这里选择的按顺序使用。 要访问，请使 [用设计模式](/help/sites-authoring/default-components-designmode.md) （仅限经典UI）并选择 **[!UICONTROL 用户档案]** 选项卡：

![chlimage_1-317](assets/chlimage_1-317.png)

在此对话框中，您还可以配置视频组件的设计以及播放、 [!UICONTROL Flash][!UICONTROL 和高]级参数 。

## 安装FFmpeg并配置AEM {#install-ffmpeg}

视频组件依赖第三方开源产品FFmpeg来转码视频。 已从https://ffmpeg.org/ [下载](https://ffmpeg.org/)。 安装FFmpeg后，请配置AEM以使用特定的音频编解码器和特定的运行时选项。

要在Windows上安装 **FFmpeg**，请执行以下步骤：

1. 将编译后的二进制文件下载为 `ffmpeg.zip`。
1. 取消存档到文件夹。
1. 将系统环境变 `PATH` 量设&#x200B;*置为&lt;your-ffmpeg-location*>`\bin`。
1. 重新启动AEM。

要在Mac OS X上 **安装FFmpeg**，请执行以下步骤：

1. 安装Xcode，网址 [为developer.apple.com/xcode](https://developer.apple.com/xcode/)。
1. 可在XQuartz [安装](https://www.xquartz.org) 以获取 [X11](https://support.apple.com/en-us/HT201341)。
1. 安装MacPorts，网址 [为www.macports.org](https://www.macports.org/)。
1. 在控制台中，执 `sudo port install ffmpeg` 行命令并按照屏幕上的说明操作。 确保将可执行文件 `FFmpeg` 的路径添加到系统 `PATH` 变量中。

要在Mac OS X **10.6上安装FFmpeg**，请使用预编译版本，请执行以下步骤：

1. 下载预编译版本。
1. 将其取消存档到 `/usr/local` 目录。
1. 在控制台中，执行 `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`。 根据需要更改路径。

要配 **置AEM**，请执行以下步骤：

>[!NOTE]
>
>仅当需要进一步自定义编解码器时，才需要执行这些步骤。

1. Open [!UICONTROL CRXDE Lite] in your web browser. 访 [问http://localhost:4502/crx/de](http://localhost:4502/crx/de)。
2. 选择节 `/libs/settings/dam/video/format_aac/jcr:content` 点并确保节点属性如下所示：

   * `audioCodec` 是 `aac`.
   * `customArgs` 是 `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. 要自定义配置，请在节点中创建叠 `/apps/settings/` 加并在节点下移动相同 `/conf/global/settings/` 结构。 无法在节点中编 `/libs` 辑它。 例如，要叠加路径， `/libs/settings/dam/video/fullhd-bp`请在上创建该路 `/conf/global/settings/dam/video/fullhd-bp`径。

   >[!NOTE]
   >
   >叠加和编辑整个用户档案节点，而不仅仅是需要修改的属性。 这些资源不会通过SlingResourceMergare解决。

4. If you changed either of the properties, click **[!UICONTROL Save All.]**

>[!NOTE]
>
>升级AEM实例时，不保留对默认现成工作流模型(OOTB)所做的更改。 Adobe建议您在编辑修改的工作流模型之前复制这些模型。 例如，在编辑DAM更新资 [!UICONTROL 产模型中的] FFmpeg转码步骤之前，复制OOTB DAM更新资产  模型，以挑选在升级前存在的视频用户档案名称。 然后，可以叠加节 `/apps` 点，让AEM检索对OOTB模型的自定义更改。
