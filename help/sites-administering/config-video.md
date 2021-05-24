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
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# 配置视频组件{#configure-the-video-component}

[视频组件](/help/sites-authoring/default-components-foundation.md#video)允许您在页面上放置一个预定义的现成(OOTB)视频资产。

为了进行正确转码，管理员需单独安装FFmpeg。 请参阅[安装FFmpeg并配置AEM](#install-ffmpeg)。 管理员还可以[配置视频配置文件](#configure-video-profiles)以与HTML5元素一起使用。

>[!CAUTION]
>
>此基础组件已被弃用。Adobe建议改用[核心组件嵌入组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html)。

>[!CAUTION]
>
>如果没有进行广泛的项目级别自定义，此组件将不再能够开箱即用运行。

## 配置视频配置文件{#configure-video-profiles}

要使用HTML5元素，请定义视频配置文件。 这里选择的按顺序使用。 要访问，请使用[设计模式](/help/sites-authoring/default-components-designmode.md)（仅限经典UI），然后选择&#x200B;**[!UICONTROL 配置文件]**&#x200B;选项卡：

![chlimage_1-317](assets/chlimage_1-317.png)

在此对话框中，您还可以配置视频组件的设计以及[!UICONTROL Playback]、[!UICONTROL Flash]和[!UICONTROL Advanced]的参数。

## 安装FFmpeg并配置AEM {#install-ffmpeg}

视频组件依赖于第三方开源产品FFmpeg来转码视频。 从[https://ffmpeg.org/](https://ffmpeg.org/)下载。 安装FFmpeg后，配置AEM以使用特定的音频编解码器和特定的运行时选项。

要在&#x200B;**Windows**&#x200B;上安装FFmpeg，请执行以下步骤：

1. 将编译的二进制文件下载为`ffmpeg.zip`。
1. 取消存档到文件夹。
1. 将系统环境变量`PATH`设置为&lt;*your-ffmpeg-location*>`\bin`。
1. 重新启动AEM。

要在&#x200B;**Mac OS X**&#x200B;上安装FFmpeg，请执行以下步骤：

1. 安装位于[developer.apple.com/xcode](https://developer.apple.com/xcode/)的Xcode。
1. 安装位于[XQuartz](https://www.xquartz.org)以获取[X11](https://support.apple.com/en-us/HT201341)。
1. 安装位于[www.macports.org](https://www.macports.org/)的MacPorts。
1. 在控制台中，执行`sudo port install ffmpeg`命令并按照屏幕上的说明操作。 确保将`FFmpeg`可执行文件的路径添加到`PATH`系统变量中。

要使用预编译版本在&#x200B;**Mac OS X 10.6**&#x200B;上安装FFmpeg，请执行以下步骤：

1. 下载预编译版本。
1. 将其取消存档到`/usr/local`目录。
1. 在控制台中，执行`sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`。 根据需要更改路径。

要&#x200B;**配置AEM**，请执行以下步骤：

>[!NOTE]
>
>只有在需要进一步自定义编解码器时，才需要执行这些步骤。

1. 在Web浏览器中打开[!UICONTROL CRXDE Lite]。 访问[http://localhost:4502/crx/de](http://localhost:4502/crx/de)。
2. 选择`/libs/settings/dam/video/format_aac/jcr:content`节点，并确保节点属性如下所示：

   * `audioCodec` 是 `aac`.
   * `customArgs` 是 `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. 要自定义配置，请在`/apps/settings/`节点中创建一个叠加，并在`/conf/global/settings/`节点下移动相同的结构。 无法在`/libs`节点中编辑。 例如，要叠加路径`/libs/settings/dam/video/fullhd-bp`，请在`/conf/global/settings/dam/video/fullhd-bp`处创建路径。

   >[!NOTE]
   >
   >叠加并编辑整个配置文件节点，而不仅仅是需要修改的属性。 此类资源不会通过SlingResourceMebarer进行解析。

4. 如果更改了其中任一属性，请单击&#x200B;**[!UICONTROL 全部保存。]**

>[!NOTE]
>
>升级AEM实例时，不会保留对默认现成(OOTB)工作流模型所做的更改。 Adobe建议您先复制修改的工作流模型，然后再编辑这些模型。 例如，在[!UICONTROL DAM更新资产]模型中，在编辑FFmpeg转码步骤之前，请复制OOTB [!UICONTROL DAM更新资产]模型，以选取升级前存在的视频配置文件名称。 然后，您可以叠加`/apps`节点，以便AEM检索对OOTB模型的自定义更改。
