---
title: '[!DNL Adobe Camera Raw] 支持。'
description: 了解如何在 [!DNL Adobe Experience Manager Assets]中启用 [!DNL Adobe Camera Raw] 支持。
contentOwner: AG
translation-type: tm+mt
source-git-commit: bccc937c1e1a349ab292a748c3c7b9d0c68b6199
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---


# 使用Camera Raw{#camera-raw-support}处理图像

您可以启用[!DNL Adobe Camera Raw]支持处理CR2、NEF和RAF等原始文件格式，并以JPEG格式渲染图像。 在[!DNL Adobe Experience Manager Assets]中，使用“软件分发”提供的[Camera Raw包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)支持该功能。

>[!NOTE]
>
>该功能仅支持JPEG再现。 Windows 64位、Mac OS和RHEL 7.x支持此功能。

要在[!DNL Experience Manager Assets]中启用[!DNL Camera Raw]支持，请执行以下步骤：

1. 从软件分发下载[Camera Raw包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)。
1. 访问 `https://[aem_server]:[port]/workflow`. 打开&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流。
1. 打开&#x200B;**[!UICONTROL 处理缩略图]**&#x200B;步骤。
1. 在&#x200B;**[!UICONTROL 缩略图]**&#x200B;选项卡中提供以下配置：

   * **[!UICONTROL 缩略图]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 跳过 MIME 类型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在&#x200B;**[!UICONTROL 启用Web的图像]**&#x200B;选项卡的&#x200B;**[!UICONTROL 跳过列表]**&#x200B;字段中，指定`audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 从侧面板中，在&#x200B;**[!UICONTROL 缩略图创建]**&#x200B;步骤下添加&#x200B;**[!UICONTROL Camera Raw/DNG处理程序]**&#x200B;步骤。
1. 在&#x200B;**[!UICONTROL Camera Raw/DNG处理程序]**&#x200B;步骤中，在&#x200B;**[!UICONTROL 参数]**&#x200B;选项卡中添加以下配置：

   * **[!UICONTROL MIME类型]**: `image/dng` 和  `image/x-raw-(.*)`
   * **[!UICONTROL Command]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>确保以上配置与使用Camera Raw和DNG处理步骤&#x200B;]**配置的**[!UICONTROL &#x200B;示例DAM更新资产相同。

您现在可以将相机原始数据文件导入资源。 安装Camera Raw包并配置所需的工作流后，侧窗格列表中将显示&#x200B;**[!UICONTROL 图像调整]**&#x200B;选项。

![chlimage_1-131](assets/chlimage_1-337.png)

*图：侧窗格中的选项。*

![chlimage_1-132](assets/chlimage_1-338.png)

*图：使用选项对图像进行轻量级编辑。*

将编辑保存到[!DNL Camera Raw]图像后，将为该图像生成新的再现`AdjustedPreview.jpg`。 对于除[!DNL Camera Raw]之外的其他图像类型，更改会反映在所有再现中。

## 最佳实践、已知问题和限制{#best-practices}

该功能具有以下限制：

* 该功能仅支持JPEG再现。 Windows 64位、Mac OS和RHEL 7.x支持此功能。
* RAW和DNG格式不支持元数据写回。
* [!DNL Camera Raw]库在每次可处理的总像素数方面存在限制。 目前，它最多可处理文件长边的65000像素，或先遇到任何条件时的512 MP。
