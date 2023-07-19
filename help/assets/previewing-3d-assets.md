---
title: 预览 3D 资源
description: 了解如何在Experience Manager中预览3D资源。
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
hide: true
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 8%

---

# 在Adobe Experience Manager中预览3D资源 {#previewing-3d-assets-aem}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=en) |
| AEM 6.5 | 本文 |

Experience Manager支持在创作过程中上传、交付和以交互方式预览3D资源。

交互式3D查看器可在Experience Manager的资源详细信息页面中找到。 该查看器提供了各种控件，其中包括一组交互式相机控件，可让您对 3D 资产执行绕行、缩放和平移操作。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Experience Manager中支持的3D预览格式 {#supported-3d-previewing-assets}

交互式3D预览支持以下文件格式：

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary | |
| GLTF | GL传输格式 | model/gltf+json | 参见 **注释** 下面的。 |
| 对象 | WaveFront 3D对象文件 | application/x-tgif | |
| STL | 立体光刻 | application/vnd.ms-pki.stl | |
| DN | Adobe Dimension | model/x-adobe-dn | 仅支持摄取；预览不可用。 |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | 仅支持摄取；预览不可用。 |

>[!NOTE]
>
>如果材料未在gLTF模型的预览中渲染，请确保在 `textures` 与模型位于同一根文件夹中的文件夹，如下所示：

    资产（文件夹）
    model.gltf
    model.bin
    纹理（文件夹）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## 在Experience Manager中预览3D资源时的性能注意事项{#performance-3d-previewing-assets}

在资产详细信息视图页面中打开3D资产所需的时间取决于多种因素，例如带宽、图像复杂性和到服务器的延迟。

此外，在交互操作相机时，客户端计算机的功能（如工作站、笔记本电脑或移动触摸设备）也很重要。 一个功能相当强大、图形功能良好的系统，可以使交互式3D观看体验更顺畅、更顺畅。

**要在Experience Manager中预览3D资源，请执行以下操作：**

1. 确保已将3D资源上传到Experience Manager。
参见 [3D预览支持的格式](#supported-3d-previewing-assets) 和 [上传资产](/help/assets/manage-assets.md#uploading-assets).
1. 从Experience Manager，在 **[!UICONTROL 导航]** 页面，选择 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.

   ![导航页面](/help/assets/assets-dm/navigation-assets.png)

1. 在页面的右上角附近，从“视图”下拉列表中选择 **[!UICONTROL 卡片视图]**，然后导航到要预览的3D资产。

   ![3D卡选择](/help/assets/assets-dm/3d-card-select.png)
   _在卡片视图中，选择要预览的3D资源的卡片。_

1. 选择3D资产的卡。

   ![交互式三维预览](/help/assets/assets-dm/3d-preview.png)
   _在资源详细信息视图页面中交互式预览3D资源。_
1. 在3D资产的资产详细信息视图页面上，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触摸屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击+拖动。 | 单指按下+拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击+拖动。 | 两指按下+拖动。 |
   | **缩放相机** | 在3D场景中移入和移出区域。 | 滚轮。 | 两指捏合。 |
   | **重新居中相机** | 将相机重新居中到3D场景中对象上的某个点。 | 双击。 | 双击。 |
   | **重置** | 在页面的右下角附近，选择“重置”图标以将视图目标点恢复到3D资产的中心。 重置也会将相机移近或移远一点，以便以合理的查看大小完整地显示资产。 |   |   |
   | **全屏模式** | 要进入全屏模式，请在页面的右下角选择全屏图标。 |   |   |

1. 完成后，在页面的右上角附近，选择 **[!UICONTROL 关闭]**.
