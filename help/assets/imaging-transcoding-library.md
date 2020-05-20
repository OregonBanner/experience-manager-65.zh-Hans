---
title: 图像转码库
description: 了解如何配置和使用Adobe的图像转码库，它是一款可以执行核心图像处理功能的图像处理解决方案，包括编码、转码、图像重新取样和图像大小调整。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# 图像转码库 {#imaging-transcoding-library}

Adobe的成像转码库是一种专有的图像处理解决方案，可以执行核心图像处理功能，包括：

* 编码
* 转码（转换支持的格式）
* 使用PS和英特尔IPP算法重新取样图像
* 位深度和颜色用户档案保留
* JPEG质量压缩
* 调整图像大小

成像转码库提供CMYK支持和完全alpha支持，CMYK -Alpha除外。

除了支持各种文件格式和用户档案，在性能、可伸缩性和质量方面，成像转码库与其他第三方解决方案相比具有显着优势。 以下是使用图像转码库的一些主要优点：

* **随文件大小或分辨率的增加进行缩放**: 缩放主要通过图像转码库获得专利的能力实现，在对文件进行解码时重新调整大小。 此功能可确保运行时内存使用始终是最佳的，而不是增加文件大小或分辨率百万像素的二次函数。 成像转码库可以处理更大、高分辨率（包含更高百万像素）的文件。 第三方工具（如ImageMagick）无法处理大文件，在处理此类文件时崩溃。
* **Photoshop质量压缩和调整大小算法**: 在下采样质量（平滑、锐利和自动双立方）和压缩质量方面与行业标准一致。 成像转码库进一步评估输入图像的质量因子，并智能地为输出图像使用最佳表和质量设置。 此功能可生成最佳大小的文件，而不会影响视觉质量。
* **高吞吐量：** 响应时间较短，吞吐量始终高于ImageMagick。 因此，成像转码库应减少用户的等待时间和托管成本。
* **通过并发加载实现更好的缩放：** 映像转码库在并发加载条件下性能最佳。 它提供高吞吐量、最佳CPU性能、内存使用和低响应时间，有助于降低托管成本。

## Supported platforms {#supported-platforms}

成像转码库仅可用于RHEL 7和CentOS 7分发。

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

您可以为参数配置以下 `-resize` 选项：

* `X`: `Works similar to AEM. For example -resize 319.`
* `WxH`: `Aspect Ratio will not be maintained, For example -resize 319X319.`
* `Wx`: `Fixes the width and calculates the height maintaining the aspect ratio. For example -resize 319x.`
* `xH`: `Fixes the height and calculates the width maintaining the aspect ratio. For example -resize x319.`

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 配置图像转码库 {#configuring-imaging-transcoding-library}

要配置ITL处理，请创建配置文件并更新工作流以执行它。

### 为提取的捆绑包创建配置文件 {#create-conf-file}

要配置库，请创建一个。conf文件，使用以下步骤指示库。 您需要管理员或根权限。

1. 下载 [Imaging Transcoding Library包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) ，并使用包管理器进行安装。 该包与AEM 6.5兼容。

1. 要了解捆绑ID，请 `com.day.cq.dam.cq-dam-switchengine`登录到Web控制台，然后单击“OSGi **[!UICONTROL >捆绑”]**。 或者，要打开捆绑包控制台，请访 `https://[aem_server:[port]/system/console/bundles/` 问URL。 找到 `com.day.cq.dam.cq-dam-switchengine` 捆绑包及其ID。

1. 通过使用命令检查文件夹，确保提取所 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`有所需的库，其中文件夹名称是使用捆绑ID构建的。 例如，该命令是 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` 如果bundle id为 `588`。

1. 创建 `SWitchEngineLibs.conf` 要链接到库的文件。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 使用 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` 命令添加会议文件的 `cat SWitchEngineLibs.conf` 路径。

1. 执行 `ldconfig` 命令以创建必要的链接和缓存。

1. 在用于开始AEM的帐户中，编辑文 `.bash_profile` 件。 添 `LD_LIBRARY_PATH` 加以下内容。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 要确保路径的值设置为，请使 `.`用命 `echo $LD_LIBRARY_PATH` 令。 输出应该只是 `.`。 如果该值未设置为， `.`请重新启动会话。

### 配置 [!UICONTROL DAM更新资产工作流] 。 {#configure-dam-asset-update-workflow}

更新DAM [!UICONTROL 更新资产工作流] ，以使用库处理图像。

1. 在Experience Manager用户界面中，选择“工 **[!UICONTROL 具”>“工作流”>“模型]**”。

1. 在“工作 **[!UICONTROL 流模型]** ”页面中，在编 **[!UICONTROL 辑模式下打开DAM]** 更新资产工作流模型。

1. 打开“流程 **[!UICONTROL 缩略图]** ”工作流流程步骤。 在“缩 **[!UICONTROL 略图]** ”选项卡中，添加要跳过“跳过MIME类型”列表中默认缩略图生 **[!UICONTROL 成流程的MIME类型]** 。
例如，如果要使用成像转码库创建TIFF图像的缩略图，请在“跳过MIME类 `image/tiff` 型”字 **[!UICONTROL 段中指定]** 。

1. 在“启 **[!UICONTROL 用Web的图像]** ”选项卡中，添加要跳过“跳过”列表中默认Web再现生成流程的MIME **[!UICONTROL 类型]**。 例如，如果您在上面的步骤中 `image/tiff` 跳过了MIME类型， `image/tiff` 请添加到跳过列表。

1. 打开EPS **[!UICONTROL 缩略图（由ImageMagick提供）]** 步骤，导航到“ **[!UICONTROL 参数]** ”选项卡。 在“ **[!UICONTROL Mime类型]** ”列表中，添加您希望映像转码库处理的MIME类型。 例如，如果您跳过了上述步 `image/tiff` 骤中的MIME类型，请 `image/jpeg` 添加 **[!UICONTROL 到Mime类型]** 列表。

1. 如果存在默认命令，请删除该命令。

1. 切换侧面板，并从步骤列表添加 **[!UICONTROL SWitchEngine Handler]**。

1. 根据您的自定 [!UICONTROL 义要求将命令] 添加到SwitchEngine处理程序。 调整您指定的命令的参数以满足您的要求。 例如，如果要保留JPEG图像的颜色用户档案，请向“命令”列表添加以 **[!UICONTROL 下命]** 令：

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![石](assets/chlimage_1-199.png)

1. （可选）使用单个命令从中间再现生成缩略图。 中间再现用作源，以生成静态和Web再现。 这种方法比以前的方法快。 但是，不能使用此方法将自定义参数应用于缩略图。

   ![石](assets/chlimage_1-200.png)

1. 要生成Web再现，请在启用Web的 **[!UICONTROL 图像选项卡中配置参数]** 。

1. 同步更新的 [!UICONTROL DAM更新资产工作流] 模型。 保存工作流。

验证配置、上传TIFF图像并监视error.log文件。 您会注意到 `INFO` 提到的消息 `SwitchEngineHandlingProcess execute: executing command line`。 日志中提到生成的演绎版。 工作流完成后，您可以在AEM中视图新演绎版。

>[!MORELIKETHIS]
>
>* [支持的MIME类型文章](assets-formats.md#supported-image-transcoding-library)