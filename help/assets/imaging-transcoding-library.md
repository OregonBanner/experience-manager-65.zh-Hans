---
title: 图像转码库
description: 了解如何配置和使用Adobe的图像转码库，它是一款可执行核心图像处理功能（包括编码、转码、图像重新取样和图像大小调整）的图像处理解决方案。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 图像转码库 {#imaging-transcoding-library}

Adobe的成像转码库是一款专有的图像处理解决方案，可以执行核心图像处理功能，包括：

* 编码
* 转码（转换支持的格式）
* 使用PS和“英特尔IPP”算法重新取样图像
* 位深度和颜色用户档案保留
* JPEG质量压缩
* 调整图像大小

成像转码库提供CMYK支持和完全Alpha支持，CMYK -Alpha除外。

除了支持各种文件格式和用户档案，在性能、可伸缩性和质量方面，成像转码库与其他第三方解决方案相比还具有显着优势。 以下是使用图像转码库的一些主要优点：

* **随文件大小或分辨率的增加而缩放**:缩放主要通过图像转码库获得专利的能力实现，在解码文件时重新调整大小。 此功能可确保运行时内存使用始终是最佳的，而不是增加文件大小或分辨率百万像素的二次函数。 图像转码库可以处理更大、高分辨率（包含更高百万像素）的文件。 第三方工具（如ImageMagick）无法处理大文件，在处理此类文件时崩溃。
* **Photoshop质量压缩和调整大小算法**:在缩减采样质量（平滑、锐利和自动双立方）和压缩质量方面与行业标准一致。 成像转码库进一步评估输入图像的品质因数，并智能地使用输出图像的最佳表和品质设置。 此功能可生成最佳大小的文件，而不会影响视觉质量。
* **高吞吐量：** 响应时间较短，吞吐量始终高于ImageMagick。 因此，成像转码库应减少用户的等待时间和托管成本。
* **利用并发负载更好地进行缩放：** 成像转码库在并发加载条件下表现最佳。 它提供高吞吐量、最佳CPU性能、内存使用和低响应时间，这有助于降低托管成本。

## Supported platforms {#supported-platforms}

图像转码库仅适用于RHEL 7和CentOS 7分发。

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

您可以为参数配置以下选 `-resize` 项：

* `X`: `Works similar to AEM. For example -resize 319.`
* `WxH`: `Aspect Ratio will not be maintained, For example -resize 319X319.`
* `Wx`: `Fixes the width and calculates the height maintaining the aspect ratio. For example -resize 319x.`
* `xH`: `Fixes the height and calculates the width maintaining the aspect ratio. For example -resize x319.`

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 配置成像转码库 {#configuring-imaging-transcoding-library}

要配置ITL处理，请创建配置文件并更新工作流以执行它。

### 为提取的包创建配置文件 {#create-conf-file}

要配置库，请使用以下步骤创建一个。conf文件以指示库。 您需要管理员或根权限。

1. 下载 [Imaging Cronding Library包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) ，然后使用包管理器安装它。 该包与AEM 6.5兼容。

1. 要了解捆绑ID，请登 `com.day.cq.dam.cq-dam-switchengine`录到Web控制台，然后点按 **[!UICONTROL OSGi >捆绑]**。 或者，要打开包控制台，请访问 `https://[aem_server:[port]/system/console/bundles/` URL。 找到 `com.day.cq.dam.cq-dam-switchengine` 捆绑包及其ID。

1. 通过使用命令检查文件夹，确保提取所有所需的库 `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`，在该文件夹中，文件夹名称是使用bundle ID构建的。 例如，如果bundle id为， `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` 则该命令为 `588`。

1. 创建 `SWitchEngineLibs.conf` 要链接到库的文件。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 使用 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` 命令添加会议文件的 `cat SWitchEngineLibs.conf` 路径。

1. 执行 `ldconfig` 命令以创建必要的链接和缓存。

1. 在用于开始AEM的帐户中，编辑文 `.bash_profile` 件。 通过 `LD_LIBRARY_PATH` 添加以下内容进行添加。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. 要确保将路径的值设置为，请使 `.`用命 `echo $LD_LIBRARY_PATH` 令。 输出应该就是 `.`。 如果该值未设置为，请 `.`重新启动会话。

### 配置 [!UICONTROL DAM更新资产工作流]{#configure-dam-asset-update-workflow}

更新 [!UICONTROL DAM更新资产工作流] ，以使用库处理图像。

1. 点按/单击 AEM 徽标，然后转到&#x200B;**[!UICONTROL 工具 > 工作流 > 模式]**。

1. 在“工 **[!UICONTROL 作流模型]** ”页面中，在编辑模 **** 式下打开DAM更新资产工作流模型。

1. 打开“流程 **[!UICONTROL 缩略图]** ”工作流程步骤。 在“缩 **[!UICONTROL 略图]** ”选项卡中，添加要跳过“跳过MIME类型”列表中默认缩略图生成过程的 **[!UICONTROL MIME类型]** 。
例如，如果要使用成像转码库为TIFF图像创建缩略图，请在“跳过MIME类 `image/tiff` 型”字 **[!UICONTROL 段中指定]** 。

1. 在“启 **[!UICONTROL 用Web的图像]** ”选项卡中，添加要跳过“跳过”列表中默认Web再现生成过程的MIME **[!UICONTROL 类型]**。 例如，如果您在上述步骤中跳 `image/tiff` 过了MIME类型，请添加 `image/tiff` 到跳过列表。

1. 打开 **[!UICONTROL EPS缩览图（由ImageMagick提供支持）步骤]** ，导航到“参 **[!UICONTROL 数]** ”选项卡。 在“ **[!UICONTROL Mime类型]** ”列表中，添加您希望成像转码库处理的MIME类型。 例如，如果您跳过了上述步骤中 `image/tiff` 的MIME类型，请添加 `image/jpeg` 到 **[!UICONTROL Mime类型列表]** 。

1. 如果存在默认命令，请删除该命令。

1. 切换侧面板，并从步骤列表添加 **[!UICONTROL SWitchEngine处理程序]**。

1. 根据您的自定义要 [!UICONTROL 求，向SwitchEngine处理程序] 添加命令。 调整您为满足要求而指定的命令的参数。 例如，如果要保留JPEG图像的颜色用户档案，请向“命令”列表添加以 **[!UICONTROL 下命令]** :

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![赤石](assets/chlimage_1-199.png)

1. （可选）使用单个命令从中间再现生成缩略图。 中间再现用作源以生成静态和Web再现。 该方法比以前的方法快。 但是，不能使用此方法将自定义参数应用于缩略图。

   ![赤石](assets/chlimage_1-200.png)

1. 要生成Web再现，请在“启用Web的图像” **[!UICONTROL 选项卡中配置参数]** 。

1. 同步更新的 [!UICONTROL DAM更新资产工作流模] 型。 保存工作流。

验证配置、上传TIFF图像并监视error.log文件。 您会注意到 `INFO` 提及的消息 `SwitchEngineHandlingProcess execute: executing command line`。 日志中提到生成的演绎版。 工作流完成后，您可以在AEM中视图新演绎版。

>[!MORELIKETHIS]
>
>* [支持的MIME类型文章](assets-formats.md#supported-image-transcoding-library)