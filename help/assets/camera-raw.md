---
title: ”[!DNL Adobe Camera Raw] 支持处理数字资产”
description: 了解如何启用 [!DNL Adobe Camera Raw] 中的支持 [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# 处理图像，使用 [!DNL Adobe Camera Raw] {#camera-raw-support}

您可以启用 [!DNL Adobe Camera Raw] 支持处理原始文件格式（如CR2、NEF和RAF），并以JPEG格式渲染图像。 中支持该功能 [!DNL Adobe Experience Manager Assets] 使用 [Camera Raw包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 可从Software Distribution获得。

>[!NOTE]
>
>功能仅支持JPEG呈现版本。 它在Windows 64位、Mac OS和RHEL 7.x上受支持。

启用 [!DNL Camera Raw] 中的支持 [!DNL Experience Manager Assets]，请按照以下步骤操作：

1. 下载 [[!DNL Camera Raw] 包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) 起始日期 [!DNL Software Distribution].
1. 访问 `https://[aem_server]:[port]/workflow`. 打开 **[!UICONTROL DAM更新资产]** 工作流。
1. 编辑 **[!UICONTROL 进程缩略图]** 步骤。
1. 在中提供以下配置 **[!UICONTROL 缩略图]** 选项卡：

   * **[!UICONTROL 缩略图]**： `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 跳过 MIME 类型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在 **[!UICONTROL 启用Web的图像]** 选项卡，在 **[!UICONTROL 跳过列表]** 字段，指定 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 从侧面板中，添加 **[!UICONTROL Camera Raw/DNG处理程序]** 步骤低于 **[!UICONTROL 进程缩略图]** 步骤。
1. 在 **[!UICONTROL Camera Raw/DNG处理程序]** 步骤，将以下配置添加到 **[!UICONTROL 参数]** 选项卡：

   * **[!UICONTROL Mime类型]**： `image/dng` 和 `image/x-raw-(.*)`
   * **[!UICONTROL 命令]**：

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 单击“**[!UICONTROL 保存]**”。

>[!NOTE]
>
>确保上述配置与 **[!UICONTROL 具有Camera Raw和DNG处理步骤的DAM更新资源示例]** 配置。

您现在可以将Camera Raw文件导入Assets。 安装Camera Raw包并配置所需的工作流后， **[!UICONTROL 图像调整]** 选项将显示在侧窗格列表中。

![chlimage_1-131](assets/chlimage_1-337.png)

*图：侧窗格中的选项。*

![chlimage_1-132](assets/chlimage_1-338.png)

*图：使用选项对图像进行轻量级编辑。*

将编辑内容保存到之后 [!DNL Camera Raw] 图像，新演绎版 `AdjustedPreview.jpg` 为图像生成。 对于其他图像类型，不包括 [!DNL Camera Raw]，则更改会反映在所有演绎版中。

## 最佳实践、已知问题和限制 {#best-practices}

该功能具有以下限制：

* 功能仅支持JPEG呈现版本。 它在Windows 64位、Mac操作系统和RHEL 7.x上受支持。
* RAW和DNG格式不支持元数据写回。
* 此 [!DNL Camera Raw] 库在每次可处理的总像素数方面存在限制。 目前，它最多可以在文件的长边处理65000像素，或者处理无论首先遇到什么标准的512 MP文件。
