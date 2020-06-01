---
title: 预览3D资产
description: 了解如何预览3D资源
contentOwner: Rick Brough
docset: aem65
translation-type: tm+mt
source-git-commit: 1cabc87dc58a4dbcac64a2797a3b1e0cca995d63
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 15%

---


# 在AEM中预览3D资产{#previewing-3d-assets-aem}

Adobe Experience Manager支持3D资产的上传、投放和交互式预览，作为创作流程的一部分。

AEM 中的资产详细信息页面提供了交互式 3D 查看器。该查看器提供了各种控件，其中包括一组交互式相机控件，可让您对 3D 资产执行绕行、缩放和平移操作。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## AEM中支持的3D预览格式 {#supported-3d-previewing-assets}

交互式3D预览支持以下文件格式：

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | 模型/gltf二进制 |  |
| GLTF | GL传输格式 | model/gltf+json | 请参 **阅下** 面的说明。 |
| OBJ | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 光固化成形 | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 仅支持摄取； 预览不可用。 |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | 仅支持摄取； 预览不可用。 |

**注意**: 如果材料未在gLTF模型的预览下呈现，请确保它们的命名正确，并且位于与模型 `textures` 相同的根文件夹中的文件夹中，如下所示：

    资产（文件夹）
    model.
    gltfmodel.
    bintextures（文件夹）
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## 在AEM中预览3D资产时的性能注意事项{#performance-3d-previewing-assets}

在资产详细信息视图页中打开3D资产所花费的时间取决于若干因素，如带宽、图像复杂性和服务器延迟。

此外，在以交互方式操作相机时，客户端计算机（如工作站、笔记本或移动触控设备）的功能也很重要。 具备良好图形功能的相当强大的系统可以使交互式 3D 查看体验更流畅、更舒适。

**在AEM中预览3D资产**

1. 确保您已将 3D 资产上传到 AEM。See [Supported formats for 3D preview](#supported-3d-previewing-assets) and [Uploading assets](/help/assets/managing-assets-touch-ui.md#uploading-assets).
1. 从AEM的导航页 **[!UICONTROL 面]** ，点按 **[!UICONTROL 资产>文件]**。

   ![导航页](/help/assets/assets-dm/navigation-assets.png)

1. 在页面的右上角附近，从“视图”下拉列表中，点按&#x200B;**[!UICONTROL 卡片视图]**，然后导航到要预览的 3D 资产。

   ![3D卡选择](/help/assets/assets-dm/3d-card-select.png)
   _在卡片视图中，点按要预览的3D资产的卡片。_

1. 点按3D资产的卡片，以在资产详细信息视图页面中将其打开。

   ![交互式3D预览](/help/assets/assets-dm/3d-preview.png)
   _资产详细信息预览页面中3D资产的交互式视图。_
1. 在3D资产的资产详细信息视图页面上，执行下列任一操作：
   * **旋转相机**-围绕3D场景和对象绕行视图。
      * _鼠标_: 左键单击+拖动。
      * _触摸屏_: 单指按+拖动。
   * **平移相机**-向左、向右、向上或向下平移视图。
      * _鼠标_: 右键单击并拖动。
      * _触摸屏_: 双指按+拖动。
   * **缩放相机**-缩放相机以移入和移出3D场景的区域。
      * _鼠标_: 滚轮。
      * _触摸屏_: 两指捏合。
   * **重新输入相机**-将相机重新输入到3D场景中对象上的某个点。
      * _鼠标_: 多次单击。
      * _触摸屏_: 多次点击。
   * **重置**-在页面的右下角附近，点按重置图标以将视图目标点恢复到3D资产的中心。 重置还会使相机更近或更远地移动，以便以合理的查看大小完整显示资产。
   * **全屏模式**-要进入全屏模式，请点按页面右下角的全屏图标。

1. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Close]**.
