---
title: 使用PDF栅格化器生成再现
description: 本文介绍如何使用Adobe PDF Rasterizer库生成高质量的缩览图和再现。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# 使用PDF栅格化器 {#using-pdf-rasterizer}

有时，当您将内容密集型的大型PDF或AI文件上传到Adobe Experience Manager(AEM)资产时，默认库可能无法生成准确的输出。 在这种情况下，Adobe的PDF栅格化器库可以生成比默认库的输出更可靠、更准确的输出。

Adobe建议对以下内容使用PDF栅格化器库：

* 内容密集的大量AI/PDF文件。
* 未开箱即用生成缩览图的AI和PDF文件。
* 具有Pantone Matching System(PMS)颜色的AI文件。

与开箱即用输出相比，使用PDF栅格化器生成的缩览图和预览的质量更高，因此，可以跨设备提供一致的查看体验。 Adobe PDF Rasterizer库不支持任何色彩空间转换。 它始终输出为RGB，而与源文件的色彩空间无关。

1. 从包共享在AEM部署中安装PDF栅格化 [器包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)。

   >[!NOTE]
   >
   >PDF栅格化器库仅可用于Windows和Linux。

1. 访问AEM资产工作流控制台(位于 `https://[server]:[port]/workflow`)。 打开“ [!UICONTROL DAM更新资产”工作流] ”页。

1. 要防止使用默认方法为PDF和AI文件生成缩览图和Web再现，请执行以下步骤：

   * 打开“流 **[!UICONTROL 程缩略图]** ”步骤，并根据需要在“缩略图”选项卡 `application/pdf` 下的“跳过 `application/postscript`******** MIME类型”字段中添加或添加。
   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在“启用 **[!UICONTROL Web的图像]** ”选项卡中，根据您的 `application/pdf` 要求在“跳 `application/postscript` 过列表 **** ”下添加或添加。
   ![用于跳过图像格式的缩略图处理的配置](assets/web_enabled_imageskiplist.png)

1. 打开“ **[!UICONTROL 栅格化PDF/AI图像预览再现]** ”步骤，并删除要跳过默认生成预览图像再现的MIME类型。 例如，从“MIME类型 `application/pdf`”列表 `application/postscript`中删 `application/illustrator` 除MIME类 **[!UICONTROL 型]** 、或。

   ![process_arguments](assets/process_arguments.png)

1. 将“ **[!UICONTROL PDF栅格化处理程序”步骤从侧面板拖到“进程缩略图]** ”步骤 **[!UICONTROL 的下方]** 。
1. 为 **[!UICONTROL PDF栅格化器处理程序步骤配置以下参数]** :

   * MIME类型： `application/pdf` or `application/postscript`

   * 命令: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 添加缩略图大小：319:319, 140:100, 48:48。 根据需要添加自定义缩略图配置。
   该命令的命令行参 `PDFRasterizer` 数可以包括：

   * `-d`:标记可实现文本、矢量图稿和图像的平滑渲染。 创建更高质量的图像。 但是，包含此参数会导致命令运行缓慢并增加图像大小。

   * `-p`:页码。 默认值是所有页面。 “*”表示所有页面。

   * `-s`:最大图像尺寸（高度或宽度）。 这将转换为每页的DPI。 如果页面大小不同，则每页可能会按不同的数量缩放。 默认值为实际页面大小。

   * `-t`:输出图像类型。 有效类型有JPEG、PNG、GIF和BMP。 默认值为JPEG。

   * `-i`:输入PDF的路径。 它是必需参数。

   * `-h`: 帮助


1. 要删除中间演绎版，请选择“删 **[!UICONTROL 除生成的演绎版”]**。
1. 要让PDF栅格化生成Web再现，请选择“ **[!UICONTROL 生成Web再现”]**。

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 在“启用Web的图像” **[!UICONTROL 选项卡中指定设置]** 。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 保存工作流。
1. 要启用PDF栅格化器以处理带有PDF库的PDF页面，请从“工作流”控制台中打开 **[!UICONTROL DAM进程子资产模型]** 。
1. 从侧面板中，将“PDF栅格化处理程序”步骤拖至“创建支持Web的图 **[!UICONTROL 像再现”步骤下]** 。
1. 为 **[!UICONTROL PDF栅格化器处理程序步骤配置以下参数]** :

   * MIME类型： `application/pdf` or `application/postscript`

   * 命令: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * 添加缩略图大小：319:319, 140:100, 48:48。 根据需要添加自定义缩略图配置。
   PDFRasterizer命令的命令行参数可以包括：

   * `-d`:标记可实现文本、矢量图稿和图像的平滑渲染。 创建更高质量的图像。 但是，包含此参数会导致命令运行缓慢并增加图像大小。

   * `-p`:页码。 默认值是所有页面。 `*` 表示所有页面。

   * `-s`:最大图像尺寸（高度或宽度）。 这将转换为每页的DPI。 如果页面大小不同，则每页可能会按不同的数量缩放。 默认值为实际页面大小。

   * `-t`:输出图像类型。 有效类型有JPEG、PNG、GIF和BMP。 默认值为JPEG。

   * `-i`:输入PDF的路径。 它是必需参数。

   * `-h`: 帮助


1. 要删除中间演绎版，请选择“删 **[!UICONTROL 除生成的演绎版”]**。
1. 要让PDF栅格化生成Web再现，请选择“ **[!UICONTROL 生成Web再现”]**。

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 在“启用Web的图像” **[!UICONTROL 选项卡中指定设置]** 。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 保存工作流。
1. 将PDF或AI文件上传到AEM资产。 PDF栅格化器可为文件生成缩览图和Web再现。
