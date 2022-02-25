---
title: '"[!DNL Adobe Camera Raw] 支持处理数字资产”'
description: 了解如何启用 [!DNL Adobe Camera Raw] 支持 [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# 处理图像时使用 [!DNL Adobe Camera Raw] {#camera-raw-support}

您可以启用 [!DNL Adobe Camera Raw] 支持处理原始文件格式（如CR2、NEF和RAF），并以JPEG格式渲染图像。 在 [!DNL Adobe Experience Manager Assets] 使用 [Camera Raw包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 可从Software Distribution获取。

>[!NOTE]
>
>该功能仅支持JPEG演绎版。 Windows 64位、Mac OS和RHEL 7.x支持此功能。

启用 [!DNL Camera Raw] 支持 [!DNL Experience Manager Assets]，请执行以下步骤：

1. 下载 [[!DNL Camera Raw] 软件包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) 从 [!DNL Software Distribution].
1. 访问 `https://[aem_server]:[port]/workflow`. 打开 **[!UICONTROL DAM更新资产]** 工作流。
1. 编辑 **[!UICONTROL 流程缩略图]** 中。
1. 在 **[!UICONTROL 缩略图]** 选项卡：

   * **[!UICONTROL 缩略图]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 跳过 MIME 类型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在 **[!UICONTROL 启用Web的图像]** 选项卡 **[!UICONTROL 跳过列表]** 字段，指定 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 从侧面板中，将 **[!UICONTROL Camera Raw/DNG处理程序]** 步骤 **[!UICONTROL 流程缩略图]** 中。
1. 在 **[!UICONTROL Camera Raw/DNG处理程序]** 步骤，在 **[!UICONTROL 参数]** 选项卡：

   * **[!UICONTROL Mime类型]**: `image/dng` 和 `image/x-raw-(.*)`
   * **[!UICONTROL Command]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>确保上述配置与 **[!UICONTROL 使用Camera Raw和DNG处理步骤更新资产的DAM示例]** 配置。

您现在可以将相机原始文件导入资产。 安装Camera Raw包并配置所需的工作流后， **[!UICONTROL 图像调整]** 选项。

![chlimage_1-131](assets/chlimage_1-337.png)

*图：侧面板中的选项。*

![chlimage_1-132](assets/chlimage_1-338.png)

*图：使用选项对图像进行轻量级编辑。*

在保存对 [!DNL Camera Raw] 图像，新呈现版本 `AdjustedPreview.jpg` 为图像生成。 适用于除 [!DNL Camera Raw]，则所做的更改会反映在所有演绎版中。

## 最佳实践、已知问题和限制 {#best-practices}

该功能具有以下限制：

* 该功能仅支持JPEG演绎版。 Windows 64位、Mac OS和RHEL 7.x支持此功能。
* RAW和DNG格式不支持元数据写回。
* 的 [!DNL Camera Raw] 库每次可处理的总像素数存在限制。 目前，它最多可以处理文件长边上的65000个像素，或者无论先遇到什么标准，都可处理512 MP。
