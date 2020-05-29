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
source-git-commit: 44dbabeeea4e4e8d17cc69a2d8ea791c98be2bd2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 6%

---


# 配置视频组件 {#configure-the-video-component}

通 [过视频](/help/sites-authoring/default-components-foundation.md#video) 组件，您可以在页面上放置一个预定义的OOTB（现成）视频元素。

要进行正确转码，管理员必 [须单独安装FFmpeg和配置](#install-ffmpeg) AEM。 它们还可以[配置视频配置文件](#configure-video-profiles)以便与 HTML5 元素结合使用。

## 配置视频用户档案 {#configure-video-profiles}

您可能需要定义要用于HTML5元素的视频用户档案。 这里选择的按顺序使用。 要访问，请使 [用设计模式](/help/sites-authoring/default-components-designmode.md) （仅限经典UI）并选择 **[!UICONTROL 用户档案]** 选项卡：

![chlimage_1-317](assets/chlimage_1-317.png)

您还可以为Playback、Flash和Advanced配置视频组 [!UICONTROL 件和][!UICONTROL 参]数 [!UICONTROL 的]设计。

## 安装FFmpeg并配置AEM {#install-ffmpeg}

The Video Component relies on the third-party open-source product FFmpeg for proper transcoding of videos that can be downloaded from [https://ffmpeg.org/](https://ffmpeg.org/). 安装FFmpeg后，必须将AEM配置为使用特定音频编解码器和特定运行时选项。

**为平台安装FFmpeg**:

* **在 Windows 中：**

   1. 将编译后的二进制文件下载为 `ffmpeg.zip`
   1. 解压缩到一个文件夹中.
   1. 将系统环境变量设 `PATH` 置为 `<*your-ffmpeg-locatio*n>\bin`
   1. 重新启动AEM。

* **在 Mac OS X 中：**

   1. 安装Xcode([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. 安装XQuartz/X11。
   1. 安装MacPorts([https://www.macports.org/](https://www.macports.org/))
   1. 在控制台中，运行以下命令并按照说明操作：

      `sudo port install ffmpeg`

      `FFmpeg` 必须在中， `PATH` 这样AEM才能通过命令行选取它。

* **将预编译的版本用于 OS X 10.6：**

   1. 下载预编译版本。
   1. Extract it to the `/usr/local` directory.
   1. 从终端执行：

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**配置AEM**:

>[!NOTE]
>
>仅当需要进一步自定义编解码器时，才需要执行这些步骤。

1. Open [!UICONTROL CRXDE Lite] in your web browser. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
2. 选择节 `/libs/settings/dam/video/format_aac/jcr:content` 点并确保节点属性如下所示：

   * audioCodec：

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

3. 要自定义配置，请在节点中创建叠 `/apps/settings/` 加并在节点下移动相同 `/conf/global/settings/` 结构。 无法在节点中编 `/libs` 辑它。 例如，要叠加路径， `/libs/settings/dam/video/fullhd-bp`请在上创建该路 `/conf/global/settings/dam/video/fullhd-bp`径。

   >[!NOTE]
   >
   >叠加和编辑整个用户档案节点，而不仅仅是需要修改的属性。 这些资源不会通过SlingResourceMergare解决。

4. If you changed either of the properties, click **[!UICONTROL Save All]**.

>[!NOTE]
>
>升级AEM实例时，不保留OOTB工作流模型。 Adobe建议您在编辑OOTB工作流模型之前先复制它们。 例如，在编辑DAM更新资 [!UICONTROL 产模型中的] FFmpeg转码步骤之前，复制OOTB DAM更新资产  模型，以挑选在升级前存在的视频用户档案名称。 然后，可以叠加节 `/apps` 点，让AEM检索对OOTB模型的自定义更改。

