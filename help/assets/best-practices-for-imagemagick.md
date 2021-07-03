---
title: 安装和配置ImageMagick
description: 了解ImageMagick软件、如何安装它、设置命令行处理步骤，以及使用它编辑、撰写和从图像生成缩略图。
contentOwner: AG
role: Admin
feature: 演绎版，开发人员工具
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# 安装并配置ImageMagick以与[!DNL Experience Manager Assets]配合使用 {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick是用于创建、编辑、合成或转换位图图像的软件插件。 它可以以各种格式（超过200种）读写图像，包括PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF和SVG。 使用ImageMagick调整图像大小、翻转、镜像、旋转、扭曲、剪切和变换图像。 您还可以使用ImageMagick调整图像颜色、应用各种特殊效果，或绘制文本、线、多边形、省略号和曲线。

使用命令行中的[!DNL Adobe Experience Manager]媒体处理程序通过ImageMagick处理图像。 要使用ImageMagick处理各种文件格式，请参阅[资产文件格式最佳实践](/help/assets/assets-file-format-best-practices.md)。 要了解所有支持的文件格式，请参阅[资产支持的格式](/help/assets/assets-formats.md)。

要使用ImageMagick处理大型文件，请考虑比通常的内存要求高、IM策略所需的潜在更改以及对性能的总体影响。 内存要求取决于各种因素，如分辨率、位深度、颜色配置文件和文件格式。 如果您打算使用ImageMagick处理非常大的文件，请为[!DNL Experience Manager]服务器正确设置基准。 最后提供了一些有用的资源。

>[!NOTE]
>
>如果您在[!DNL Adobe Managed Services](AMS)上使用[!DNL Experience Manager]，请联系Adobe客户关怀团队，以便您计划处理许多高分辨率PSD或PSB文件。 [!DNL Experience Manager] 可能无法处理超过30000 x 23000像素的高分辨率PSB文件。

## 安装ImageMagick {#installing-imagemagick}

ImageMagic安装文件的多个版本可用于各种操作系统。 为您的操作系统使用相应的版本。

1. 下载适用于您的操作系统的相应[ImageMagick安装文件](https://www.imagemagick.org/script/download.php)。
1. 要在托管[!DNL Experience Manager]服务器的磁盘上安装ImageMagick，请启动安装文件。

1. 将路径环境变量设置为ImageMagic安装目录。
1. 要检查安装是否成功，请执行`identify -version`命令。

## 设置命令行处理步骤 {#set-up-the-command-line-process-step}

您可以为特定用例设置命令行流程步骤。 每次在[!DNL Experience Manager]服务器上的`/content/dam`中添加JPEG图像文件时，请执行以下步骤以生成翻转图像和缩略图（140x100、48x48、319x319和1280）：

1. 在[!DNL Experience Manager]服务器上，转到工作流控制台(`https://[aem_server]:[port]/workflow`)，然后打开&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流模型。
1. 从&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流模型中，打开&#x200B;**[!UICONTROL EPS缩略图（由ImageMagick提供支持）]**&#x200B;步骤。
1. 在&#x200B;**[!UICONTROL 参数选项卡]**&#x200B;中，将`image/jpeg`添加到&#x200B;**[!UICONTROL Mime类型]**&#x200B;列表。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 在&#x200B;**[!UICONTROL Commands]**&#x200B;框中，输入以下命令：

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 选择&#x200B;**[!UICONTROL 删除生成的演绎版]**&#x200B;和&#x200B;**[!UICONTROL 生成Web演绎版]**&#x200B;标记。

   ![select_flags](assets/select_flags.png)

1. 在&#x200B;**[!UICONTROL Web Enabled Image]**&#x200B;选项卡中，指定尺寸为1280x1280像素的呈现版本的详细信息。 此外，在&#x200B;**[!UICONTROL Mimetype]**&#x200B;框中指定`image/jpeg`。

   ![web_enabled_image](assets/web_enabled_image.png)

1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

   >[!NOTE]
   >
   >`convert`命令可能无法在某些Windows版本（例如Windows SE）中运行，因为它与Windows安装中的本机`convert`实用程序冲突。 在这种情况下，请提及ImageMagick实用程序的完整路径。 例如，指定
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. 打开&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤，并在&#x200B;**[!UICONTROL 跳过Mime类型]**&#x200B;下添加MIME类型`image/jpeg`。

   ![skip_mime_types](assets/skip_mime_types.png)

1. 在&#x200B;**[!UICONTROL 启用Web的图像]**&#x200B;选项卡的&#x200B;**[!UICONTROL 跳过列表]**&#x200B;下添加MIME类型`image/jpeg`。 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

   ![web_enabled](assets/web_enabled.png)

1. 保存工作流。

1. 要验证处理是否正确，请将JPG图像上传到[!DNL Assets]。 处理完成后，检查是否生成了翻转的图像和演绎版。

## 缓解安全漏洞 {#mitigating-security-vulnerabilities}

使用ImageMagick处理图像时存在多个安全漏洞。 例如，处理用户提交的图像涉及远程代码执行(RCE)的风险。

此外，各种图像处理插件依赖于ImageMagick库，包括但不限于PHP的图像、Ruby的图像和平装剪辑，以及nodejs的图像。

如果您使用ImageMagick或受影响的库，则Adobe建议您通过执行以下至少一项任务（但最好同时执行两项任务）来缓解已知的漏洞：

1. 在将所有图像文件发送到ImageMagick进行处理之前，请确认所有图像文件都以您支持的图像文件类型对应的预期[&quot;magic bytes&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures)开头。
1. 使用策略文件禁用易受攻击的ImageMagick代码。 ImageMagick的全局策略位于`/etc/ImageMagick`。
