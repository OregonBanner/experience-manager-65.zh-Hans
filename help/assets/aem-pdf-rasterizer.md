---
title: 使用PDF栅格化器生成再现
description: 使用中的Adobe PDF光栅器库生成高质量的缩略图和再现 [!DNL Adobe Experience Manager]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---


# 使用PDF光栅器 {#using-pdf-rasterizer}

将大型、内容密集型PDF或AI文件上传到 [!DNL Adobe Experience Manager Assets]时，默认转换可能无法生成准确的输出。 Adobe的PDF光栅化器库与默认库的输出相比，可以生成更可靠、更准确的输出。 Adobe建议在以下情况下使用PDF光栅器库：

* 内容密集的繁重AI文件或PDF文件。
* 默认不生成缩览图的AI文件和PDF文件。
* 具有Pantone Matching System(PMS)颜色的AI文件。

与开箱即用输出相比，使用PDF光栅器生成的缩略图和预览的质量更高，因此，可以跨设备提供一致的查看体验。 Adobe PDF光栅器库不支持任何色彩空间转换。 它始终输出为RGB，而与源文件的色彩空间无关。

1. 从“软件分发”在部署时安 [!DNL Adobe Experience Manager] 装PDF栅 [格器包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)。

   >[!NOTE]
   >
   >PDF光栅器库仅可用于Windows和Linux。

1. 访问工 [!DNL Assets] 作流控制 `https://[aem_server]:[port]/workflow`台。 打开 [!UICONTROL DAM更新资产工作流] 。

1. 要防止使用默认方法为PDF文件和AI文件生成缩览图和Web再现，请执行以下步骤：

   * 打开“ **[!UICONTROL 流程缩略图]** ”步骤，根据 `application/pdf` 需要 `application/postscript` ，在“缩略图 **[!UICONTROL ”选项卡下添加或添]** 加“跳过MIME类型” **** 字段。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在“启 **[!UICONTROL 用Web的图像]** ”选项卡中，根 `application/pdf` 据您的要 `application/postscript` 求在“跳 **[!UICONTROL 过列表]** ”下添加或添加。

   ![用于跳过图像格式的缩略图处理的配置](assets/web_enabled_imageskiplist.png)

1. 打开“ **[!UICONTROL 栅格化PDF/AI图像预览再现]** ”步骤，并删除要跳过默认生成预览图像再现的MIME类型。 例如，从MIME类型 `application/pdf`列表 `application/postscript`中 `application/illustrator` 删除MIME **[!UICONTROL 类型]** 。

   ![process_arguments](assets/process_arguments.png)

1. 将“PDF栅 **[!UICONTROL 格处理程序”步骤从侧面板]** 拖到“处理缩略图” **[!UICONTROL 步骤的下方]** 。
1. 为PDF光栅处理程序步 **[!UICONTROL 骤配置以下参数]** :

   * MIME类型： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 添加缩略图大小：319:319, 140:100, 48:48。 根据需要添加自定义缩略图配置。

   该命令的命令行参 `PDFRasterizer` 数可以包括以下参数：

   * `-d`:标记可实现文本、矢量图稿和图像的平滑渲染。 创建更优质的图像。 但是，包含此参数会导致命令运行缓慢并增加图像大小。

   * `-p`:页码。 默认值是所有页面。 要表示所有页面，请使用 `*`。

   * `-s`:最大图像尺寸（高度或宽度）。 此值将转换为每页的DPI。 如果页面大小不同，则每个页面都可能按不同数量缩放。 默认值为实际页面大小。

   * `-t`:输出图像类型。 有效类型有JPEG、PNG、GIF和BMP。 默认值为JPEG。

   * `-i`:输入PDF的路径。 它是一个必需参数。

   * `-h`: 帮助


1. 要删除中间演绎版，请选择“删 **[!UICONTROL 除生成的演绎版]**”。

1. 要让PDF栅格化器生成Web演绎版，请选择“ **[!UICONTROL 生成Web演绎版]**”。

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 在“启用Web的图像” **[!UICONTROL 选项卡中指定设置]** 。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 保存工作流。

1. 要启用PDF栅格化器以处理带有PDF库的PDF页面，请从“工 **[!UICONTROL 作流”控制台打开]** “DAM流程子 [!UICONTROL 资产”模] 型。

1. 从侧面板中，将“PDF栅格化处理程序”步骤拖至“创 **[!UICONTROL 建支持Web的图像演绎版]** ”步骤下。

1. 为PDF光栅处理程序步 **[!UICONTROL 骤配置以下参数]** :

   * MIME类型： `application/pdf` 或 `application/postscript`

   * 命令: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 添加缩略图大小： `319:319`, `140:100`, `48:48`根据需要添加自定义缩略图配置。

   该命令的命令行参 `PDFRasterizer` 数可以包括以下参数：

   * `-d`:标记可实现文本、矢量图稿和图像的平滑渲染。 创建更优质的图像。 但是，包含此参数会导致命令运行缓慢并增加图像大小。

   * `-p`:页码。 默认值是所有页面。 `*` 表示所有页面。

   * `-s`:最大图像尺寸（高度或宽度）。 此值将转换为每页的DPI。 如果页面大小不同，则每个页面都可能按不同数量缩放。 默认值为实际页面大小。

   * `-t`:输出图像类型。 有效类型有JPEG、PNG、GIF和BMP。 默认值为JPEG。

   * `-i`:输入PDF的路径。 它是一个必需参数。

   * `-h`: 帮助


1. 要删除中间演绎版，请选择“删 **[!UICONTROL 除生成的演绎版]**”。
1. 要让PDF栅格化器生成Web演绎版，请选择“ **[!UICONTROL 生成Web演绎版]**”。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 在“启用Web的图像” **[!UICONTROL 选项卡中指定设置]** 。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 保存工作流。
1. 将PDF或AI文件上传到 [!DNL Experience Manager Assets]。 PDF栅格化器可生成文件的缩略图和Web再现。
