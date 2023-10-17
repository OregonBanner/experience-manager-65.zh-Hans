---
title: 在Dynamic Media中使用3D资源
description: 了解如何在Dynamic Media中上传、管理、查看和交付3D资源作为沉浸式体验。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 3%

---

# 在Dynamic Media中使用3D资源 {#working-with-three-d-assets-dm}

Dynamic Media允许您上传、管理、查看和交付3D资源作为沉浸式体验。

* 一键发布(使用 **[!UICONTROL 快速发布]** （工具栏中）以生成URL。
* 优化支持使用由Adobe Dimension提供支持的高质量交互式Dimensional查看器预设查看3D资源。
* 通过3D Media WCM组件，您可以轻松将3D资源添加到Adobe Experience Manager Sites页面。

在Dynamic Media中使用3D资源无需额外配置。

![3d鞋](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *三维鞋的详细信息页面。*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media支持的3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支持以下3D格式。

另请参阅 [支持的3D格式](/help/assets/assets-formats.md).

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary | 将材料和纹理作为单个资产包含在内。 |
| 对象 | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 立体成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | *仅支持摄取；不可查看或交互。* USDZ是一种专有的3D格式，可供Safari和iOS设备本机查看。 |

>[!NOTE]
>
>资产详细信息页面上的3D Media WCM组件和3D预览与最新版本的Chrome (97.x)不兼容。 要处理3D资产，请使用Firefox或Safari，或使用早期版本的Chrome (96.x)。

## 快速入门：Dynamic Media中的3D资源 {#quick-start-three-d}

以下分步工作流描述旨在帮助您在Dynamic Media - Scene7模式下快速启动和运行3D资源。

>[!IMPORTANT]
>
>Dynamic Media — 混合模式不支持3D资源。

在Dynamic Media中使用3D资产之前，请确保您的Experience Manager管理员已在Dynamic Media - Scene7模式下启用和配置Dynamic MediaCloud Service。

请参阅 [配置Dynamic MediaCloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) 在配置Dynamic Media - Scene7模式和 [Dynamic Media - Scene7模式疑难解答](/help/assets/troubleshoot-dms7.md).

1. **上传3D资产**

   * [上传要在Dynamic Media中使用的3D资源](/help/assets/manage-assets.md#uploading-assets).
   * [在Dynamic Media中上传的受支持的3D文件格式](#supported-three-d-file-formats-in-dm).

1. **管理3D**

   * 组织和搜索3D资产

      * [组织数字资源](/help/assets/organize-assets.md#organize-digital-assets).
      * [搜索3D资产](/help/assets/search-assets.md).
      * [使用自定义谓词筛选搜索结果](/help/assets/search-assets.md#custompredicates).

   * 查看3D资产

      * [查看3D资源并与之交互](#viewing-three-d-assets).
      * [管理维查看器预设](/help/assets/managing-viewer-presets.md).

   * 使用3D资源元数据

      * [管理数字资源的元数据](/help/assets/metadata.md).
      * [元数据架构](/help/assets/metadata-schemas.md).

1. **发布三维资产**

   * [发布静态Dynamic Media 3D资源](#publishing-three-d-assets)
   * [使用维度查看器发布Dynamic Media 3D资源的备用方法](#alternate-publish-methods)

## 关于查看和与3D资产交互 {#viewing-three-d-assets}

本节将介绍如何以两种不同的方式查看和与3D资源：在资源详细信息页面中，以及在Experience Manager Sites的3D媒体组件中。

交互式3D查看器包括一组交互式相机控件等，可让您环绕、缩放和平移3D资产。

在“资产详细信息”页面视图中打开3D资产所需的时间取决于多个因素。 这些因素包括：

* 到服务器的带宽。
* 服务器的延迟
* 图像的复杂性。

此外，当以交互方式操作摄像头时，客户端计算机的功能（如工作站、笔记本或移动触控设备）也非常重要。 功能相当强大、图形功能良好的系统可使交互式3D观看体验更加流畅和更加有利。

>[!TIP]
>
>您可以在查看器预设编辑器中打开维查看器预设，以练习导航3D资产，而无需首先上传任何3D文件。 维查看器预设提供了一个内置的3D资产供您与交互。
>
>请参阅 [管理查看器预设](/help/assets/managing-viewer-presets.md).

## 从资源详细信息页面查看并与3D资源交互 {#viewing-three-d-assets-from-asset-details-page}

另请参阅 [使用软件界面预览资源](/help/assets/previewing-assets.md).

**要从资产详细信息页面查看和交互3D资产，请执行以下操作：**

1. 确保您已将3D资源上传到Experience Manager。

   请参阅 [上传要在Dynamic Media中使用的3D资源](/help/assets/manage-assets.md#uploading-assets).

1. 从Experience Manager，在 **[!UICONTROL 导航]** 页面，转到 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 在页面的右上角附近，从 **[!UICONTROL 视图]** 下拉列表，选择 **[!UICONTROL 卡片视图]**.
1. 导航到要查看的3D资产。
1. 选择3D资产的卡。
1. 在3D资产的详细信息视图页面上，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触摸屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击+拖动。 | 单指按下+拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击+拖动。 | 双指按下+拖动。 |
   | **缩放相机** | 在3D场景中移入和移出区域。 | 滚轮。 | 两指捏合。 |
   | **重新居中相机** | 将相机重新居中到3D场景中对象上的某个点。 | 双击。 | 双击。 |
   | **重置** | 在页面的右下角附近，选择“重置”图标以将视图目标点恢复到3D资产的中心。 重置还会将相机靠近或远离其他位置，以便以合理的观看大小完整地显示资产。 |   |   |
   | **全屏模式** | 要进入全屏模式，请选择页面右下角的全屏图标。 |   |   |

1. 在页面的右上角，选择 **[!UICONTROL 关闭]** 以返回到“资源”页面。

## 在3D媒体组件中查看和与3D资产交互 {#interacting-with-asset-inside-three-d-media-component}

当网页处于 **[!UICONTROL 编辑]** 模式，无法与3D资产交互。 要使资源具有交互性，您可以使用 **[!UICONTROL 预览]** 功能以查看页面编辑器中的网页，该功能可完全访问3D媒体组件的功能。

>[!IMPORTANT]
>
>只有在将3D媒体组件添加到网页并为其分配了3D资产后，您才能完成此任务。 请参阅 [将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page) 和 [将3D资源分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component).

另请参阅 [使用软件界面预览资源](/help/assets/previewing-assets.md).

**要在3D媒体组件中查看并与3D资产交互，请执行以下操作：**

1. 当网页在 **[!UICONTROL 编辑]** 模式，执行以下任一操作：

   * 在页面的右上角附近，选择 **[!UICONTROL 预览]** 以进入 **[!UICONTROL 预览]** 模式。
   * 删除 `/editor.html` 从浏览器中的页面URL。

   ![3D资产显示在3D媒体组件内](/help/assets/assets-dm/3d-asset-in-3d-media.png)
完全交互式的3D资产，如 **[!UICONTROL 预览]** 模式。

1. 在中 **[!UICONTROL 预览]** 模式，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触摸屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击+拖动。 | 单指按下+拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击+拖动。 | 双指按下+拖动。 |
   | **缩放相机** | 在3D场景中移入和移出区域。 | 滚轮。 | 两指捏合。 |
   | **重新居中相机** | 将相机重新居中到3D场景中对象上的某个点。 | 双击。 | 双击。 |
   | **重置** | 在页面的右下角附近，选择“重置”图标以将视图目标点恢复到3D资产的中心。 重置还会将相机靠近或远离其他位置，以便以合理的观看大小完整地显示资产。 |   |   |
   | **全屏模式** | 要进入全屏模式，请选择页面右下角的全屏图标。 |   |   |

## 关于使用3D媒体组件 {#working-with-three-d-media-component}

Dynamic Media包含一个Dynamic Media 3D媒体组件，您可以在Adobe Experience Manager Sites中使用它来启用在网页上交互式查看3D模型的功能。

* [将3D媒体组件添加到页面模板](#adding-three-d-media-component-to-page-template)
* [将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)
   * [可选 — 配置3D媒体组件](#configuring-the-three-d-component)
* [将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)

## 将3D媒体组件添加到页面模板 {#adding-three-d-media-component-to-page-template}

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]**.
1. 导航到要在其中启用3D组件的页面模板，然后选择该模板。
1. 选择 **[!UICONTROL 编辑]** 以便打开该模板。
1. 在页面的右上角附近的下拉菜单中，选择 **[!UICONTROL 结构]** 模式（如果尚未处于活动状态）。

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. 选择空白区域 **[!UICONTROL 布局容器]** 区域，以便您选择该区域并打开其关联的工具栏。
1. 在工具栏上，选择 **[!UICONTROL 策略]** 图标以打开 **[!UICONTROL 策略编辑器]**.
1. 在 **[!UICONTROL 属性]** 部分，在 **[!UICONTROL 允许的组件]** 选项卡，滚动到 **[!UICONTROL Dynamic Media]**，然后展开列表并选中 **[!UICONTROL 3D媒体]**.
1. 选择 **[!UICONTROL 完成]** 以保存更改并关闭 **[!UICONTROL 策略编辑器]**.

   现在，您可以将Dynamic Media 3D媒体组件放在使用此模板的所有页面上。

## 在网页上添加3D媒体组件 {#adding-the-three-d-media-component-to-a-web-page}

如果您将Experience Manager用作Web内容管理系统，则可以通过3D媒体组件将3D资源添加到网页。

另请参阅 [在页面上添加Dynamic Media资源](/help/assets/adding-dynamic-media-assets-to-pages.md).

**要在网页上添加3D媒体组件，请执行以下操作：**

1. 打开Experience Manager Sites并选择要将Dynamic Media 3D Media组件添加到其中的网页。
1. 选择 **[!UICONTROL 编辑]** （铅笔）图标，以便您可以在页面编辑器中打开页面。 确保 **[!UICONTROL 编辑]** 将在页面右上角附近选择模式。

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. 在工具栏上，选择侧面板图标以切换或“打开”面板的显示。

1. 在侧面板中，选择加号图标以打开 **[!UICONTROL 组件]** 列表。

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. 拖动 **[!UICONTROL 3D媒体]** 来自的组件 **[!UICONTROL 组件]** 列出页面上要显示3D查看器的位置。

现在，您可以为该组件分配3D资产了。

请参阅 [将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component).

### 可选 — 配置3D媒体组件 {#configuring-the-three-d-component}

1. 在Experience Manager Sites页面编辑器中，选择 **[!UICONTROL 3D媒体查看器]** 之前添加到页面的组件。
1. 选择 **[!UICONTROL 配置]** 图标（扳手），以打开组件配置对话框。

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. 在“3D媒体”对话框中，从“查看器预设”下拉列表中选择 **[!UICONTROL 维度]** 将维查看器预设分配给组件。

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. 选择右上角的复选标记以保存更改。

## 将3D资产分配给3D媒体组件 {#assigning-a-three-d-asset-to-the-component}

将3D媒体组件添加到网页后，即可为其分配3D资产。

请参阅 [将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page).

**要将3D资产分配给3D媒体组件，请执行以下操作：**

1. 在Experience Manager Sites页面编辑器中，选择 **[!UICONTROL 资产]** 图标以打开 **[!UICONTROL 资产]** 在侧面板中。
1. 在下拉列表中，选择 **[!UICONTROL 三维]** 以仅显示3D资源文件类型。
1. 在侧面板中，搜索或滚动到要在编辑的页面上查看的3D资产。
1. 将资产侧面板中的3D资产拖放到 **[!UICONTROL 3D媒体]** 之前添加到页面的组件。

   ![将3D资产分配给3D媒体组件](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>当网页在Experience Manager Sites中时 **[!UICONTROL 编辑]** 模式，3D媒体组件会显示3D资产，但无法与资产交互。 要使资源具有交互性，您可以使用 **[!UICONTROL 预览]** 功能以查看页面编辑器中的网页，该功能可完全访问3D媒体组件的功能。

## 发布静态Dynamic Media 3D资源 {#publishing-three-d-assets}

Dynamic Media接受支持的各种3D文件格式 *静态内容* 在Dynamic Media中。 静态内容表示您可以上传和发布3D资产，但不支持此类资产 *可变成像* 或与3D资产关联的图像重新调整。 原因是Dynamic Media Imaging Server无法识别3D格式。 因此，在Dynamic Media中发布3D资源后，您可以立即复制一个URL。 3D资源的URL遵循常规的Dynamic Media URL结构。 但是，与Dynamic Media中的传统图像资源不同，您无法编辑资源URL中的任何参数。

另请参阅 [获取静态资源的URL](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

在 **[!UICONTROL 卡片视图]**，资产名称的正下方及其日期和时间左侧会显示一个小地球图标，指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

如果您将Experience Manager用作WCM，请使用此发布方法直接在网页上添加Dynamic Media 3D资产。

另请参阅 [发布Dynamic Media资源](publishing-dynamicmedia-assets.md).

另请参阅 [发布页面](/help/sites-authoring/publishing-pages.md).

**要发布静态Dynamic Media 3D资源，请执行以下操作：**

1. 打开3D资产（GLB、OBJ或STL文件格式），以便在资产详细信息页面中查看它。
1. 在工具栏上，选择 **[!UICONTROL 快速发布]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. 选择 **[!UICONTROL 关闭]** 以退出对话框并返回资产详细信息页面。
1. 从3D资产文件名左侧的下拉列表中，选择 **[!UICONTROL 节目]**.

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. 选择 **[!UICONTROL 原有]**. 发布（或“激活”）3D资产时， **[!UICONTROL URL]** 如果满足以下所有3D资产条件，则按钮将出现在页面的左下角附近：
   * 3D资产是受支持的格式（GLB、OBJ、STL和USDZ）。
   * 已将3D资源摄取到Dynamic Media Image Production System (IPS)。
   * 发布3D资产。

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. 选择 **[!UICONTROL URL]** 这样即可显示3D资产的直接生产URL，以供您在网页上复制和使用。

### 使用维度查看器发布Dynamic Media 3D资源的备用方法 {#alternate-publish-methods}

请通过以下两种方法发布Dynamic Media 3D资产（如果这样做） *非* 使用Experience Manager作为WCM。

* **[!UICONTROL URL]**  — 使用 **[!UICONTROL URL]** 如果您使用的是第三方Web内容管理系统，并且希望使用维度查看器将Dynamic Media 3D资产链接到您的网页。

  请参阅 [将URL链接到您的Web应用程序](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL 嵌入]**  — 使用 **[!UICONTROL 嵌入]** 当您想要使用维度查看器查看嵌入到网页上的Dynamic Media 3D资产时。 将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 中不允许编辑代码 **[!UICONTROL 嵌入]** 对话框。

  请参阅 [在网页上嵌入Dynamic Media视频、图像查看器或维度查看器](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
