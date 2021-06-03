---
title: 使用PDF光栅器生成演绎版
description: 使用Adobe PDF光栅器库生成高质量缩略图和演绎版。
contentOwner: AG
role: Developer, Administrator
feature: 开发人员工具，演绎版
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: fbabf714a3b5066fdef144a4092eaad7e8a6b370
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# 使用PDF光栅器{#using-pdf-rasterizer}

将内容密集型大型PDF或AI文件上传到[!DNL Adobe Experience Manager Assets]时，默认库可能无法生成准确的输出。 Adobe的PDF光栅化器库与默认库的输出相比，可以生成更可靠、更准确的输出。 Adobe建议对以下情况使用PDF光栅器库：

Adobe建议为以下内容使用PDF光栅器库：

* 内容密集型的AI文件或PDF文件。
* AI文件和包含默认未生成缩略图的PDF文件。
* 具有Pantone匹配系统(PMS)颜色的AI文件。

与现成输出相比，使用PDF光栅器生成的缩略图和预览在质量上更好，因此可以跨设备提供一致的查看体验。 Adobe PDF光栅化器库不支持任何颜色空间转换。 它始终输出为RGB，而不考虑源文件的色彩空间。

1. 在[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip)的[!DNL Adobe Experience Manager]部署中安装PDF光栅化器包。

   >[!NOTE]
   >
   >PDF光栅器库仅适用于Windows和Linux。

1. 访问位于`https://[aem_server]:[port]/workflow`的[!DNL Assets]工作流控制台。 打开[!UICONTROL DAM更新资产]工作流。

1. 要阻止使用默认方法为PDF文件和AI文件生成缩略图和Web演绎版，请执行以下步骤：

   * 根据需要打开&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤，并在&#x200B;**[!UICONTROL Thumbnails]**&#x200B;选项卡下的&#x200B;**[!UICONTROL 跳过Mime类型]**&#x200B;字段中添加`application/pdf`或`application/postscript`。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在&#x200B;**[!UICONTROL 启用Web的图像]**&#x200B;选项卡的&#x200B;**[!UICONTROL 跳过列表]**&#x200B;下添加`application/pdf`或`application/postscript`，具体取决于您的要求。

   ![用于跳过图像格式的缩略图处理的配置](assets/web_enabled_imageskiplist.png)

1. 打开&#x200B;**[!UICONTROL 栅格化PDF/AI图像预览呈现版本]**&#x200B;步骤，并删除要跳过默认预览图像呈现版本的生成的MIME类型。 例如，从&#x200B;**[!UICONTROL MIME类型]**&#x200B;列表中删除MIME类型`application/pdf`、`application/postscript`或`application/illustrator`。

   ![process_arguments](assets/process_arguments.png)

1. 将&#x200B;**[!UICONTROL PDF光栅化处理程序]**&#x200B;步骤从侧面板拖到&#x200B;**[!UICONTROL 流程缩略图]**&#x200B;步骤的下方。
1. 为&#x200B;**[!UICONTROL PDF光栅化器处理程序]**&#x200B;步骤配置以下参数：

   * MIME类型：`application/pdf`或`application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 添加缩略图大小：319:319,140:100,48:48。 根据需要添加自定义缩略图配置。

   `PDFRasterizer`命令的命令行参数可以包括以下内容：

   * `-d`:用于实现文本、矢量图稿和图像的平滑渲染的标记。创建更优质的图像。 但是，包含此参数会导致命令运行缓慢并增大图像大小。

   * `-s`:最大图像尺寸（高度或宽度）。对于每个页面，此值将转换为DPI。 如果页面大小不同，则每个页面可能会按不同的数量缩放。 默认为实际页面大小。

   * `-t`:输出图像类型。有效类型为JPEG、PNG、GIF和BMP。 默认值为JPEG。

   * `-i`:输入PDF的路径。它是一个必需参数。

   * `-h`: 帮助


1. 要删除中间演绎版，请选择&#x200B;**[!UICONTROL 删除生成的演绎版]**。
1. 要让PDF光栅化器生成Web演绎版，请选择&#x200B;**[!UICONTROL 生成Web演绎版]**。

   ![generate_web_redintions1](assets/generate_web_renditions1.png)

1. 在&#x200B;**[!UICONTROL 启用Web的图像]**&#x200B;选项卡中指定设置。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 保存工作流。
1. 要启用PDF光栅化器以处理带有PDF库的PDF页面，请从[!UICONTROL 工作流]控制台中打开&#x200B;**[!UICONTROL DAM流程子资产]**&#x200B;模型。
1. 从侧面板中，拖动&#x200B;**[!UICONTROL 创建启用Web的图像呈现]**&#x200B;步骤下的“PDF光栅化器处理程序”步骤。
1. 为&#x200B;**[!UICONTROL PDF光栅化器处理程序]**&#x200B;步骤配置以下参数：

   * MIME类型：`application/pdf`或`application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 添加缩略图大小：`319:319`、`140:100`、`48:48`。 根据需要添加自定义缩略图配置。

   `PDFRasterizer`命令的命令行参数可以包括以下内容：

   * `-d`:用于实现文本、矢量图稿和图像的平滑渲染的标记。创建更优质的图像。 但是，包含此参数会导致命令运行缓慢并增大图像大小。

   * `-s`:最大图像尺寸（高度或宽度）。对于每个页面，此值将转换为DPI。 如果页面大小不同，则每个页面可能会按不同的数量缩放。 默认为实际页面大小。

   * `-t`:输出图像类型。有效类型为JPEG、PNG、GIF和BMP。 默认值为JPEG。

   * `-i`:输入PDF的路径。它是一个必需参数。

   * `-h`: 帮助


1. 要删除中间演绎版，请选择&#x200B;**[!UICONTROL 删除生成的演绎版]**。
1. 要让PDF光栅化器生成Web演绎版，请选择&#x200B;**[!UICONTROL 生成Web演绎版]**。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 在&#x200B;**[!UICONTROL 启用Web的图像]**&#x200B;选项卡中指定设置。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 保存工作流。
1. 将PDF文件或AI文件上传到[!DNL Experience Manager Assets]。 PDF光栅化器可为文件生成缩略图和Web演绎版。
