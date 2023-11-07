---
title: 安装和配置ImageMagick
description: 了解ImageMagick软件、如何安装该软件、设置命令行流程步骤以及使用该软件从映像编辑、编写和生成缩略图。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# 安装和配置ImageMagick以用于 [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick是一个用于创建、编辑、合成或转换位图图像的软件插件。 它可以读写各种格式（超过200种）的图像，包括PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF和SVG。 使用ImageMagick调整图像大小、翻转、镜像、旋转、扭曲、剪切和变换图像。 也可以使用ImageMagick调整图像颜色、应用各种特殊效果或绘制文本、线条、多边形、椭圆和曲线。

使用 [!DNL Adobe Experience Manager] 命令行中的媒体处理程序，用于通过ImageMagick处理图像。 要使用ImageMagick处理各种文件格式，请参阅 [资产文件格式最佳实践](/help/assets/assets-file-format-best-practices.md). 要了解所有支持的文件格式，请参阅 [资源支持的格式](/help/assets/assets-formats.md).

要使用ImageMagick处理大型文件，请考虑比平常更高的内存要求、IM策略所需的潜在更改以及总体性能影响。 内存需求取决于分辨率、位深度、颜色配置文件和文件格式等多种因素。 如果您要使用ImageMagick处理非常大的文件，请对 [!DNL Experience Manager] 服务器。 最后提供了一些有用的资源。

>[!NOTE]
>
>如果您使用 [!DNL Experience Manager] 日期 [!DNL Adobe Managed Services] (AMS)，如果您计划处理许多高分辨率PSD或PSB文件，请联系Adobe客户支持。 [!DNL Experience Manager] 可能无法处理超过 30000 x 23000 像素的高分辨率 PSB 文件。

## 安装ImageMagick {#installing-imagemagick}

ImageMagic安装文件的多个版本可用于各种操作系统。 使用适用于您的操作系统的相应版本。

1. 下载相应的 [ImageMagick安装文件](https://www.imagemagick.org/script/download.php) 适用于您的操作系统。
1. 在托管的磁盘上安装ImageMagick [!DNL Experience Manager] 服务器，启动安装文件。

1. 将路径Environment变量设置为ImageMagic安装目录。
1. 要检查安装是否成功，请执行 `identify -version` 命令。

## 设置命令行流程步骤 {#set-up-the-command-line-process-step}

您可以为特定用例设置命令行流程步骤。 每次将JPEG图像文件添加到时，执行这些步骤可生成翻转的图像和缩略图（140x100、48x48、319x319和1280x1280） `/content/dam` 在 [!DNL Experience Manager] 服务器：

1. 在 [!DNL Experience Manager] 服务器，转到“工作流”控制台(`https://[aem_server]:[port]/workflow`)并打开 **[!UICONTROL DAM更新资产]** 工作流模型。
1. 从 **[!UICONTROL DAM更新资产]** 工作流模型，打开 **[!UICONTROL EPS缩略图（由ImageMagick提供支持）]** 步骤。
1. 在 **[!UICONTROL “参数”选项卡]**，添加 `image/jpeg` 到 **[!UICONTROL Mime类型]** 列表。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 在 **[!UICONTROL 命令]** 框中，输入以下命令：

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 选择 **[!UICONTROL 删除生成的呈现版本]** 和 **[!UICONTROL 生成Web演绎版]** 标志。

   ![select_flags](assets/select_flags.png)

1. 在 **[!UICONTROL 启用Web的图像]** 制表符，为尺寸为1280x1280像素的演绎版指定详细信息。 此外，请指定 `image/jpeg` 在 **[!UICONTROL Mimetype]** 盒子。

   ![web_enabled_image](assets/web_enabled_image.png)

1. 单击 **[!UICONTROL 确定]** 以保存更改。

   >[!NOTE]
   >
   >此 `convert` 命令不能与某些Windows版本（例如，Windows SE）一起运行，因为它与本机 `convert` 实用程序是Windows安装的一部分。 在这种情况下，请提及ImageMagick实用程序的完整路径。 例如，指定
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. 打开 **[!UICONTROL 进程缩略图]** 步骤，并添加MIME类型 `image/jpeg` 下 **[!UICONTROL 跳过MIME类型]**.

   ![skip_mime_type](assets/skip_mime_types.png)

1. 在 **[!UICONTROL 启用Web的图像]** 选项卡，添加MIME类型 `image/jpeg` 在 **[!UICONTROL 跳过列表]**. 单击 **[!UICONTROL 确定]** 以保存更改。

   ![web_enabled](assets/web_enabled.png)

1. 保存工作流。

1. 要验证是否进行了正确处理，请将JPG图像上传到 [!DNL Assets]. 处理完成后，检查是否生成了翻转的图像和演绎版。

## 减少安全漏洞 {#mitigating-security-vulnerabilities}

使用ImageMagick处理图像存在多个安全漏洞。 例如，处理用户提交的图像涉及远程代码执行(RCE)的风险。

此外，各种图像处理插件依赖于ImageMagick库，包括但不限于PHP的imagick 、 Ruby的rmagick和paperclip ，以及nodejs的imagemagick。

如果您使用ImageMagick或受影响的库，Adobe建议您通过执行以下至少一项任务（但最好是两项任务）来缓解已知漏洞：

1. 验证所有图像文件是否以预期的内容开头 [“幻字节”](https://en.wikipedia.org/wiki/List_of_file_signatures) 文件类型对应的文件，支持的图像文件类型随后将发送到ImageMagick进行处理。
1. 使用策略文件禁用易受攻击的ImageMagick编码器。 ImageMagick全局策略位于 `/etc/ImageMagick`.
