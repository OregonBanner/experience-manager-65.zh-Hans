---
title: '[!DNL Adobe Camera Raw]支持。'
description: 了解如何在 [!DNL Adobe Camera Raw] 中启用支持 [!DNL Adobe Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: bf840b0e13e58f961c32b0231e4b691cb47b947a
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---


# 使用Camera Raw处理图像 {#camera-raw-support}

您可以启用 [!DNL Adobe Camera Raw] 支持以处理原始文件格式（如CR2、NEF和RAF）并以JPEG格式渲染图像。 使用通过包共享或 [!DNL Adobe Experience Manager Assets] 从软 [件分发提供的](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) Camera Raw包时支 [持此功能](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)。

>[!NOTE]
>
>该功能仅支持JPEG再现。 Windows 64位、Mac OS和RHEL 7.x支持此功能。

要在中启 [!DNL Camera Raw] 用支 [!DNL Experience Manager Assets]持，请执行以下步骤：

1. 从“包 [共享](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) ”或“软件分发”下 [载Camera Raw包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg)。
1. 访问 `https://[aem_server]:[port]/workflow`. 打开DAM **[!UICONTROL 更新资产工作流]** 。
1. 打开“流 **[!UICONTROL 程缩略图]** ”步骤。
1. 在“缩略图”选项卡中提 **[!UICONTROL 供以]** 下配置：

   * **[!UICONTROL 缩略图]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 跳过 MIME 类型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在“启 **[!UICONTROL 用Web的图像]** ”选项卡中， **[!UICONTROL 在“跳过列表]** ”字段中指 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`定。

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 从侧面板中，在“缩览 **[!UICONTROL 图创建”步骤下添加Camera Raw]** /DNG处 **[!UICONTROL 理程序步骤]** 。
1. 在Camera Raw/ **[!UICONTROL DNG处理程序步骤中]** ，在“参数”选项卡中添加以 **[!UICONTROL 下配置]** :

   * **[!UICONTROL MIME类型]**: `image/dng` 和 `image/x-raw-(.*)`
   * **[!UICONTROL Command]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>确保以上配置与使用Camera RAW和DNG **[!UICONTROL 处理步骤配置的示例DAM更新资产相同]** 。

您现在可以将相机原始数据文件导入资源。 安装Camera RAW包并配置所需的工作流程后，“图 **[!UICONTROL 像调整]** ”选项会显示在侧窗格的列表中。

![chlimage_1-131](assets/chlimage_1-337.png)

*图： 侧窗格中的选项。*

![chlimage_1-132](assets/chlimage_1-338.png)

*图： 使用选项对图像进行轻量级编辑。*

将编辑保存到图像 [!DNL Camera Raw] 后，将为图像 `AdjustedPreview.jpg` 生成新的再现。 对于除外的其他图像 [!DNL Camera Raw]类型，更改会反映在所有再现中。

## 最佳实践、已知问题和限制 {#best-practices}

该功能具有以下限制：

* 该功能仅支持JPEG再现。 Windows 64位、Mac OS和RHEL 7.x支持此功能。
* RAW和DNG格式不支持元数据写回。
* 库 [!DNL Camera Raw] 在每次可处理的总像素方面存在限制。 目前，它最多可处理文件长边的65000像素，或先遇到任何条件时的512 MP。
