---
title: 图像转码库
description: 了解如何配置和使用Adobe的图像转码库，它是一款可以执行核心图像处理功能的图像处理解决方案，包括编码、转码、图像重新取样和图像大小调整。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---


# 成像转码库{#imaging-transcoding-library}

Adobe的成像转码库是一种专有的图像处理解决方案，可以执行核心图像处理功能，包括：

* 编码
* 转码（转换支持的格式）
* 使用PS和英特尔IPP算法重新取样图像
* 位深度和颜色用户档案保留
* JPEG质量压缩
* 调整图像大小

成像转码库提供CMYK支持和完全alpha支持，CMYK -Alpha除外。

除了支持各种文件格式和用户档案，在性能、可伸缩性和质量方面，成像转码库与其他第三方解决方案相比具有显着优势。 以下是使用图像转码库的一些主要优点：

* **随文件大小或分辨率的增加进行缩放**:缩放主要通过图像转码库获得专利的能力实现，在对文件进行解码时重新调整大小。此功能可确保运行时内存使用始终是最佳的，而不是增加文件大小或分辨率百万像素的二次函数。 成像转码库可以处理更大、高分辨率（包含更高百万像素）的文件。 第三方工具（如ImageMagick）无法处理大文件，在处理此类文件时崩溃。
* **Photoshop质量压缩和调整大小算法**:在下采样质量（平滑、锐利和自动双立方）和压缩质量方面与行业标准一致。成像转码库进一步评估输入图像的质量因子，并智能地为输出图像使用最佳表和质量设置。 此功能可生成最佳大小的文件，而不会影响视觉质量。
* **高吞吐量：** 响应时间较短，吞吐量始终高于ImageMagick。因此，成像转码库应减少用户的等待时间和托管成本。
* **借助并发加载实现更好的缩放：** 在并发加载条件下，成像转码库具有最佳性能。它提供高吞吐量、最佳CPU性能、内存使用和低响应时间，有助于降低托管成本。

## 支持的平台{#supported-platforms}

成像转码库仅适用于RHEL 7和CentOS 7分发。

>[!NOTE]
>
>不支持Mac OS和其他*nix分发（例如，Debian和Ubuntu）。

## 使用 {#usage}

成像转码库的命令行参数可以包括：

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

可以为`-resize`参数配置以下选项：

* `X`:工作方式类似 [!DNL Experience Manager]。例如-resize 319。
* `WxH`:例如，长宽比不被保留 `-resize 319x319`。
* `Wx`:修复宽度并计算保持宽高比的高度。例如`-resize 319x`。
* `xH`:固定高度并计算保持宽高比的宽度。例如`-resize x319`。

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 配置映像转码库{#configuring-imaging-transcoding-library}

要配置ITL处理，请创建配置文件并更新工作流以执行它。

### 为提取的包{#create-conf-file}创建配置文件

要配置库，请创建一个CONF文件，以使用以下步骤指示库。 您需要管理员或根权限。

1. 从软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg)下载[映像转码库包，并使用包管理器安装它。 该软件包与[!DNL Experience Manager] 6.5兼容。

1. 要了解`com.day.cq.dam.cq-dam-switchengine`的捆绑id，请登录Web控制台，然后单击&#x200B;**[!UICONTROL OSGi]** > **[!UICONTROL 捆绑]**。 或者，要打开捆绑包控制台，请访问`https://[aem_server:[port]/system/console/bundles/` URL。 找到`com.day.cq.dam.cq-dam-switchengine`捆绑包及其ID。

1. 通过使用命令`ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`检查文件夹，确保解压所有所需的库，其中文件夹名称是使用捆绑ID构建的。 例如，如果bundle id为`588`，则命令为`ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/`。

1. 创建`SWitchEngineLibs.conf`文件以链接到库。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 使用`cat SWitchEngineLibs.conf`命令将`/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`路径添加到conf文件。

1. 执行`ldconfig`命令以创建必要的链接和缓存。

1. 在用于开始[!DNL Experience Manager]的帐户中，编辑`.bash_profile`文件。 添加`LD_LIBRARY_PATH`。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 要确保路径的值设置为`.`，请使用`echo $LD_LIBRARY_PATH`命令。 输出应该只为`.`。 如果该值未设置为`.`，请重新启动会话。

### 配置[!UICONTROL DAM更新资产]工作流{#configure-dam-asset-update-workflow}

更新[!UICONTROL DAM更新资产]工作流，以使用库处理图像。

1. 在[!DNL Experience Manager]用户界面中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。

1. 从&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面，在编辑模式下打开&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流模型。

1. 打开&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;工作流流程步骤。 在&#x200B;**[!UICONTROL 缩略图]**&#x200B;选项卡中，添加要跳过&#x200B;**[!UICONTROL 跳过MIME类型]**列表中默认缩略图生成过程的MIME类型。
例如，如果要使用成像转码库为TIFF图像创建缩览图，请在**[!UICONTROL 跳过MIME类型]**&#x200B;字段中指定`image/tiff`。

1. 在&#x200B;**[!UICONTROL 启用Web的图像]**&#x200B;选项卡中，添加要跳过其默认Web再现生成过程的MIME类型(在&#x200B;**[!UICONTROL 跳过列表]**&#x200B;中)。 例如，如果您在上述步骤中跳过了MIME类型`image/tiff`，请将`image/tiff`添加到跳过列表。

1. 打开&#x200B;**[!UICONTROL EPS缩略图（由ImageMagick提供）]**&#x200B;步骤，导航到&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡。 在&#x200B;**[!UICONTROL Mime类型]**&#x200B;列表中，添加您希望映像转码库处理的MIME类型。 例如，如果您跳过了上述步骤中的MIME类型`image/tiff`，请将`image/jpeg`添加到&#x200B;**[!UICONTROL Mime类型]**&#x200B;列表。

1. 如果存在默认命令，请删除该命令。

1. 切换侧面板，从步骤列表添加&#x200B;**[!UICONTROL SWitchEngine Handler]**。

1. 根据您的自定义要求，向[!UICONTROL SwitchEngine Handler]添加命令。 调整您指定的命令的参数以满足您的要求。 例如，如果要保留JPEG图像的颜色用户档案，请将以下命令添加到&#x200B;**[!UICONTROL Commands]**&#x200B;列表:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![石](assets/chlimage_1-199.png)

1. （可选）使用单个命令从中间再现生成缩略图。 中间再现用作源，以生成静态和Web再现。 这种方法比以前的方法快。 但是，不能使用此方法将自定义参数应用于缩略图。

   ![石](assets/chlimage_1-200.png)

1. 要生成Web再现，请在&#x200B;**[!UICONTROL 启用Web的图像]**&#x200B;选项卡中配置参数。

1. 同步更新的[!UICONTROL DAM更新资产]工作流模型。 保存工作流。

验证配置、上传TIFF图像并监视error.log文件。 您会注意到`INFO`消息中提及`SwitchEngineHandlingProcess execute: executing command line`。 日志中提到生成的演绎版。 工作流完成后，您可以在[!DNL Experience Manager]中视图新演绎版。

>[!MORELIKETHIS]
>
>* [支持的MIME类型文章](assets-formats.md#supported-image-transcoding-library)

