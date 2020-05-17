---
title: 安装并配置ImageMagick以与之配合 [!DNL Adobe Experience Manager Assets]。
description: 了解ImageMagick软件、如何安装、设置命令行处理步骤以及使用它编辑、合成和生成图像的缩略图。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5d66bf75a6751e41170e6297d26116ad33c2df44
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---


# 安装并配置ImageMagick以与 [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick是用于创建、编辑、合成或转换位图图像的软件插件。 它可以读写各种格式（超过200种）的图像，包括PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF和SVG。 使用ImageMagick调整图像大小、翻转、镜像、旋转、扭曲、剪切和变换图像。 您还可以使用ImageMagick调整图像颜色、应用各种特殊效果或绘制文本、直线、多边形、椭圆和曲线。

使用命 [!DNL Adobe Experience Manager] 令行中的媒体处理程序通过ImageMagick处理图像。 要使用ImageMagick处理各种文件格式，请参阅资 [产文件格式最佳实践](/help/assets/assets-file-format-best-practices.md)。 要了解所有支持的文件格式，请参阅资 [产支持的格式](/help/assets/assets-formats.md)。

要使用ImageMagick处理大型文件，请考虑内存要求高于常规要求、IM策略可能需要的更改以及对性能的总体影响。 内存要求取决于各种因素，如分辨率、位深度、颜色用户档案和文件格式。 如果要使用ImageMagick处理超大文件，请正确对服务器进行基 [!DNL Experience Manager] 准测试。 最后提供了一些有用的资源。

>[!NOTE]
>
>如果您正在使 [!DNL Experience Manager] 用 [!DNL Adobe Managed Services] (AMS)，如果您计划处理许多高分辨率PSD或PSB文件，请与Adobe客户服务部联系。 [!DNL Experience Manager] 可能无法处理超过30000 x 23000像素的高分辨率PSB文件。

## 安装ImageMagick {#installing-imagemagick}

各种操作系统都提供多个版本的ImageMagic安装文件。 为操作系统使用适当的版本。

1. 下载适合 [您的操作系统](https://www.imagemagick.org/script/download.php) 的ImageMagick安装文件。
1. 要在承载服务器的磁盘上安 [!DNL Experience Manager] 装ImageMagick，请启动安装文件。

1. 将路径环境变量设置为ImageMagic安装目录。
1. 要检查安装是否成功，请执行该 `identify -version` 命令。

## 设置命令行处理步骤 {#set-up-the-command-line-process-step}

您可以为特定用例设置命令行处理步骤。 每次在服务器上添加JPEG图像文件时，请执行以下步骤以生成翻转的图像和缩览图（140x100、48x48、319x319和1280x1280） `/content/dam`[!DNL Experience Manager] :

1. 在服 [!DNL Experience Manager] 务器上，转到工作流控制台()`https://[aem_server]:[port]/workflow`并打开DAM **[!UICONTROL 更新资产工作流模型]** 。
1. 从DAM更 **[!UICONTROL 新资产工作流模型]** ，打开EPS缩 **[!UICONTROL 略图（由ImageMagick提供）步骤]** 。
1. 在“参 **[!UICONTROL 数”选项卡]**, `image/jpeg` 添加到“ **[!UICONTROL Mime类型]** ”列表。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 在“命 **[!UICONTROL 令]** ”框中，输入以下命令：

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 选择“删 **[!UICONTROL 除生成的演绎版]** ” **[!UICONTROL 和“生成Web演绎版]** ”标志。

   ![select_flags](assets/select_flags.png)

1. 在“启 **[!UICONTROL 用Web的图像]** ”选项卡中，指定尺寸为1280x1280像素的再现的详细信息。 此外，在“Mimetype `image/jpeg` ”框 **[!UICONTROL 中指定]** 。

   ![web_enabled_image](assets/web_enabled_image.png)

1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

   >[!NOTE]
   >
   >该命 `convert` 令可能无法在某些Windows版本（例如Windows SE）中运行，因为它与作为Windows安装一 `convert` 部分的本机实用程序相冲突。 在这种情况下，请提及ImageMagick实用程序的完整路径。 例如，指定
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. 打开“ **[!UICONTROL 流程缩略图]** ”步骤，并在“跳过MIME类 `image/jpeg` 型” **[!UICONTROL 下添加MIME类型]**。

   ![skip_mime_types](assets/skip_mime_types.png)

1. 在“启 **[!UICONTROL 用Web的图像]** ”选项卡中，在“跳过” `image/jpeg` 列表下添 **[!UICONTROL 加MIME类型]**。 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

   ![web_enabled](assets/web_enabled.png)

1. 保存工作流。

1. 要验证处理是否正确，请将JPG图像上传到 [!DNL Assets]。 处理完成后，检查是否生成翻转的图像和再现。

## 减轻安全漏洞 {#mitigating-security-vulnerabilities}

存在多个与使用ImageMagick处理图像相关的安全漏洞。 例如，处理用户提交的图像涉及远程代码执行(RCE)的风险。

此外，各种图像处理插件都依赖于ImageMagick库，包括但不限于PHP的图像、Ruby的图像和平装剪辑以及nodejs的图像。

如果您使用ImageMagick或受影响的库，Adobe建议您通过执行以下至少一项任务（但最好同时执行两项操作）来减轻已知漏洞：

1. 在将所有图像文件发送到ImageMagick进行处 [理之前，请先验证所有图像文件是否以您支持的图像文件类型](https://en.wikipedia.org/wiki/List_of_file_signatures) ，对应的预期“幻数字节”开头。
1. 使用策略文件禁用易受攻击的ImageMagick编码器。 有关ImageMagick的全局策略，请访问 `/etc/ImageMagick`。
