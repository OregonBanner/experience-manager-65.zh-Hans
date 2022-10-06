---
title: 使用PDF光栅器生成演绎版
description: 使用Adobe PDF光栅器库生成高质量缩略图和演绎版。
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 使用PDF光栅器 {#using-pdf-rasterizer}

当您将内容密集型大型PDF或AI文件上传到 [!DNL Adobe Experience Manager Assets]，则默认库可能无法生成准确的输出。 Adobe的PDF光栅化器库与默认库的输出相比，可以生成更可靠、更准确的输出。 Adobe建议在以下情况下使用PDF光栅器库：

Adobe建议为以下内容使用PDF光栅器库：

* 内容密集型的AI文件或PDF文件。
* AI文件和PDF文件，以及默认未生成的缩略图。
* 具有Pantone匹配系统(PMS)颜色的AI文件。

与现成输出相比，使用PDF光栅器生成的缩略图和预览在质量上更好，因此可以跨设备提供一致的查看体验。 Adobe PDF光栅化器库不支持任何颜色空间转换。 它始终输出为RGB，而不考虑源文件的颜色空间。

1. 在上安装PDF光栅器包 [!DNL Adobe Experience Manager] 部署 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >PDF光栅器库仅可用于Windows和Linux。

1. 访问 [!DNL Assets] 工作流控制台位于 `https://[aem_server]:[port]/workflow`. 打开 [!UICONTROL DAM更新资产] 工作流。

1. 要阻止使用默认方法为PDF文件和AI文件生成缩略图和Web呈现版本，请执行以下步骤：

   * 打开 **[!UICONTROL 流程缩略图]** 步骤，然后添加 `application/pdf` 或 `application/postscript` 在 **[!UICONTROL 跳过Mime类型]** 字段 **[!UICONTROL 缩略图]** 选项卡。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在 **[!UICONTROL 启用Web的图像]** 选项卡，添加 `application/pdf` 或 `application/postscript` 在 **[!UICONTROL 跳过列表]** 取决于您的要求。

   ![用于跳过图像格式的缩略图处理的配置](assets/web_enabled_imageskiplist.png)

1. 打开 **[!UICONTROL 栅格化PDF/AI图像预览呈现版本]** 步骤，并删除要跳过默认预览图像呈现版本的MIME类型。 例如，删除MIME类型 `application/pdf`, `application/postscript`或 `application/illustrator` 从 **[!UICONTROL MIME类型]** 列表。

   ![process_arguments](assets/process_arguments.png)

1. 拖动 **[!UICONTROL PDF光栅化处理程序]** 从侧面板步骤到 **[!UICONTROL 流程缩略图]** 中。
1. 为 **[!UICONTROL PDF光栅化处理程序]** 步骤：

   * MIME类型： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 添加缩略图大小：319:319,140:100,48:48。 根据需要添加自定义缩略图配置。

   的命令行参数 `PDFRasterizer` 命令可以包含以下内容：

   * `-d`:用于实现文本、矢量图稿和图像的平滑渲染的标记。 创建更优质的图像。 但是，包含此参数会导致命令运行缓慢并增大图像大小。

   * `-s`:最大图像尺寸（高度或宽度）。 对于每个页面，此值将转换为DPI。 如果页面大小不同，则每个页面可能会按不同的数量缩放。 默认为实际页面大小。

   * `-t`:输出图像类型。 有效类型包括JPEG、PNG、GIF和BMP。 默认值为JPEG。

   * `-i`:输入PDF的路径。 它是一个必需参数。

   * `-h`: 帮助


1. 要删除中间演绎版，请选择 **[!UICONTROL 删除生成的演绎版]**.
1. 要让PDF光栅器生成Web呈现，请选择 **[!UICONTROL 生成Web呈现版本]**.

   ![generate_web_redintions1](assets/generate_web_renditions1.png)

1. 在 **[!UICONTROL 启用Web的图像]** 选项卡。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 保存工作流。
1. 要启用PDF光栅化器以处理具有PDF库的PDF页面，请打开 **[!UICONTROL DAM流程子资产]** 模型 [!UICONTROL 工作流] 控制台。
1. 从侧面板中，将PDF光栅化处理程序步骤拖动到 **[!UICONTROL 创建启用Web的图像呈现版本]** 中。
1. 为 **[!UICONTROL PDF光栅化处理程序]** 步骤：

   * MIME类型： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 添加缩略图大小： `319:319`, `140:100`, `48:48`. 根据需要添加自定义缩略图配置。

   的命令行参数 `PDFRasterizer` 命令可以包含以下内容：

   * `-d`:用于实现文本、矢量图稿和图像的平滑渲染的标记。 创建更优质的图像。 但是，包含此参数会导致命令运行缓慢并增大图像大小。

   * `-s`:最大图像尺寸（高度或宽度）。 对于每个页面，此值将转换为DPI。 如果页面大小不同，则每个页面可能会按不同的数量缩放。 默认为实际页面大小。

   * `-t`:输出图像类型。 有效类型包括JPEG、PNG、GIF和BMP。 默认值为JPEG。

   * `-i`:输入PDF的路径。 它是一个必需参数。

   * `-h`: 帮助


1. 要删除中间演绎版，请选择 **[!UICONTROL 删除生成的演绎版]**.
1. 要让PDF光栅器生成Web呈现，请选择 **[!UICONTROL 生成Web呈现版本]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 在 **[!UICONTROL 启用Web的图像]** 选项卡。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 保存工作流。
1. 将PDF文件或AI文件上传到 [!DNL Experience Manager Assets]. PDF光栅化器为文件生成缩略图和Web演绎版。
