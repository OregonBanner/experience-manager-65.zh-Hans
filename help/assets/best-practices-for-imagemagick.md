---
title: 安装和配置ImageMagick以与AEM Assets一起使用
description: 了解ImageMagick软件、如何安装它、设置命令行处理步骤以及使用它编辑、合成和生成图像的缩略图。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# 安装和配置ImageMagick以与AEM Assets一起使用{#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick是用于创建、编辑、合成或转换位图图像的软件插件。 它可以读写各种格式（超过200种）的图像，包括PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF和SVG。 使用ImageMagick调整图像大小、翻转、镜像、旋转、扭曲、切变和变换图像。 您还可以使用ImageMagick调整图像颜色、应用各种特殊效果，或绘制文本、线、多边形、椭圆和曲线。

使用命令行中的Adobe Experience Manager(AEM)媒体处理程序通过ImageMagick处理图像。 要使用ImageMagick处理各种文件格式，请参阅资 [产文件格式最佳实践](/help/assets/assets-file-format-best-practices.md)。 要了解所有支持的文件格式，请参阅资 [产支持的格式](/help/assets/assets-formats.md)。

要使用ImageMagick处理大型文件，请考虑内存要求高于常规要求、IM策略可能需要的更改以及对性能的总体影响。 内存要求取决于各种因素，如分辨率、位深度、颜色用户档案和文件格式。 如果要使用ImageMagick处理超大文件，请正确对AEM服务器进行基准测试。 最后给出了一些有用的资源。

>[!NOTE]
>
>如果您在Adobe Managed Services(AMS)上使用AEM，则如果您计划处理大量大型PSD或PSB文件，请联系Adobe支持部门。

## 安装ImageMagick {#installing-imagemagick}

ImageMagic安装文件的多个版本可用于各种操作系统。 为操作系统使用相应的版本。

1. 下载适合您的 [操作系统的ImageMagick安装文件](https://www.imagemagick.org/script/download.php) 。
1. 要在承载AEM服务器的磁盘上安装ImageMagick，请启动安装文件。

1. 将路径环境变量设置为ImageMagic安装目录。
1. 要检查安装是否成功，请执行该命 `identify -version` 令。

## 设置命令行处理步骤 {#set-up-the-command-line-process-step}

您可以为特定用例设置命令行进程步骤。 每次在AEM服务器上添加JPEG图像文件时，请执行以下步骤以生成翻转的图像和缩览图（140x100、48x48、319x319和1280x1280）: `/content/dam`

1. 在AEM服务器上，转到工作流控制台(`https://[aem_server]:[port]/workflow`)并打开 **[!UICONTROL DAM更新资产工作流模型]** 。
1. 从 **[!UICONTROL DAM更新资产工作流模型中]** ，打开 **[!UICONTROL EPS缩略图（由ImageMagick提供支持）步骤]** 。
1. 在“参 **[!UICONTROL 数”选项卡中]**，添加 `image/jpeg` 到“Mime类型 **** ”列表。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 在“命 **[!UICONTROL 令]** ”框中，输入以下命令：

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 选择“删 **[!UICONTROL 除生成的演绎版]** ”和“ **[!UICONTROL 生成Web演绎版”标志]** 。

   ![select_flags](assets/select_flags.png)

1. 在“启 **[!UICONTROL 用Web的图像]** ”选项卡中，指定尺寸为1280x1280像素的再现的详细信息。 此外，在“Mimetype”( `image/jpeg` Mimetype)框 **[!UICONTROL 中指定]** 。

   ![web_enabled_image](assets/web_enabled_image.png)

1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

   >[!NOTE]
   >
   >该命 `convert` 令不能与某些Windows版本（例如Windows SE）一起运行，因为它与作为Windows安装一部分的本 `convert` 机实用程序相冲突。 在这种情况下，请提及ImageMagick实用程序的完整路径。 例如，指定
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. 打开“流 **[!UICONTROL 程缩略图]** ”步骤，并在“跳过Mime类型”下 `image/jpeg` 添加 **[!UICONTROL MIME类型]**。

   ![skip_mime_types](assets/skip_mime_types.png)

1. 在“启 **[!UICONTROL 用Web的图像]** ”选项卡中，在“跳过”列表 `image/jpeg` 下添加MIME **[!UICONTROL 类型]**。 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

   ![web_enabled](assets/web_enabled.png)

1. 保存工作流。
1. 要检查ImageMagic是否能够正确处理图像，请将JPG图像上传到AEM资产。 验证是否为翻转的图像和再现生成了它。

## 缓解安全漏洞 {#mitigating-security-vulnerabilities}

存在多个与使用ImageMagick处理图像相关的安全漏洞。 例如，处理用户提交的图像涉及远程代码执行(RCE)的风险。

此外，各种图像处理插件取决于ImageMagick库，包括但不限于PHP的图像、Ruby的图像和回形针以及nodejs的图像。

如果您使用ImageMagick或受影响的库，Adobe建议您通过执行以下至少一个任务（但最好同时执行两者）来减轻已知漏洞：

1. 在将所有图像文件发送到ImageMagick进行处理之前，请先验证所有图像文 [件是否以与您支持的图像文件类型对应的预期“magic bytes](https://en.wikipedia.org/wiki/List_of_file_signatures) ”开头。
1. 使用策略文件禁用易受攻击的ImageMagick编码器。 有关ImageMagick的全局策略，请访问 `/etc/ImageMagick`。
