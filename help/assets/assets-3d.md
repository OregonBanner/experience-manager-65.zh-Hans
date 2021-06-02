---
title: 在Dynamic Media中使用3D资产
seo-title: 在Dynamic Media中使用3D资产
description: 了解如何在Dynamic Media中使用3D资产
seo-description: 了解如何在Dynamic Media中使用3D资产
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D资产，资产管理
role: Business Practitioner, Administrator
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 1c95217c98cdf24182eebbfea09c807318b2d514
workflow-type: tm+mt
source-wordcount: '2306'
ht-degree: 6%

---

# 在Dynamic Media中使用3D资产{#working-with-three-d-assets-dm}

Dynamic Media让您可以上传、管理、查看和交付3D资产，充当沉浸式体验。

* 单击发布（使用工具栏上的&#x200B;**[!UICONTROL 快速发布]**）3D资产以生成URL。
* 通过由Adobe Dimension提供支持的高质量交互式维度查看器预设，优化了对查看3D资产的支持。
* 通过3D Media WCM组件，您可以轻松地将3D资产添加到Adobe Experience Manager Sites页面。

在Dynamic Media中使用3D资产无需其他配置。

![3D鞋](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media支持的3D格式{#supported-three-d-file-formats-in-dm}

Dynamic Media支持以下3D格式。

另请参阅[支持的3D格式](/help/assets/assets-formats.md)。

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | model/gltf-binary | 将材料和纹理作为单个资产包含在内。 |
| OBJ | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 立体成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | *仅支持摄取；无法查看或进行交互。* USDZ是一种专有的3D格式，Safari和iOS设备可在本机查看该格式。 |

## 快速入门：Dynamic Media中的3D资产{#quick-start-three-d}

以下工作流分步描述旨在帮助您在Dynamic Media - Scene7模式下快速启动和运行3D资产。

>[!NOTE]
>
>Dynamic Media — 混合模式不支持3D资产。

在Dynamic Media中处理3D资产之前，请确保Experience Manager管理员已在Dynamic Media - Scene7模式下启用并配置了Dynamic MediaCloud Services。

请参阅配置Dynamic Media - Scene7模式中的[配置Dynamic MediaCloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)和[Dynamic Media - Scene7模式疑难解答](/help/assets/troubleshoot-dms7.md)。

1. **上传3D资产**

   * [上传3D资产以在Dynamic Media中使用](/help/assets/manage-assets.md#uploading-assets)。
   * [支持在Dynamic Media中上传的3D文件格式](#supported-three-d-file-formats-in-dm)。

1. **管理3D资产**

   * 组织和搜索3D资产

      * [组织数字资产](/help/assets/organize-assets.md#organize-digital-assets)。
      * [搜索3D资产](/help/assets/search-assets.md)。
      * [使用自定义谓词过滤搜索结果](/help/assets/search-assets.md#custompredicates)。
   * 查看3D资产

      * [查看3D资产并与之交互](#viewing-three-d-assets)。
      * [管理维查看器预设](/help/assets/managing-viewer-presets.md)。
   * 使用3D资产元数据

      * [管理数字资产的元数据](/help/assets/metadata.md).
      * [元数据架构](/help/assets/metadata-schemas.md).



1. **发布3D资产**

   * [发布静态Dynamic Media 3D资产](#publishing-three-d-assets)
   * [使用维度查看器发布Dynamic Media 3D资产的替代方法](#alternate-publish-methods)

## 关于查看3D资产并与之交互{#viewing-three-d-assets}

本节将介绍两种不同的查看和与3D资产交互的方法：从资产详细信息页面和站点的3D媒体组件中。

交互式3D查看器包括一组交互式相机控件等，这些控件允许您绕行、缩放和平移3D资产。

在“资产详细信息”页面视图中打开3D资产所花费的时间取决于多个因素。 这些因素包括如下几项：

* 服务器的带宽。
* 服务器延迟
* 图像的复杂性。

此外，在以交互方式操作相机时，客户端计算机（如工作站、笔记本或移动触控设备）的功能也很重要。 具备良好图形功能的相当强大的系统可以使交互式 3D 查看体验更流畅、更舒适。

>[!TIP]
>
>您可以在查看器预设编辑器中打开维度查看器预设，以练习在3D资产中导航，而无需先上传任何3D文件。 维度查看器预设具有一个内置的3D资产，可供您与之交互。
>
>请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

## 从资产详细信息页面{#viewing-three-d-assets-from-asset-details-page}查看3D资产并与其交互

另请参阅[使用软件界面预览资产](/help/assets/previewing-assets.md)。

**要从资产详细信息页面查看3D资产并与其交互，请执行以下操作：**

1. 确保已将3D资产上传到Experience Manager。

   请参阅[上传3D资产以在Dynamic Media中使用](/help/assets/manage-assets.md#uploading-assets)。

1. 从Experience Manager中，在&#x200B;**[!UICONTROL 导航]**&#x200B;页面上，点按&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 在页面的右上角附近，从&#x200B;**[!UICONTROL 视图]**&#x200B;下拉列表中，点按&#x200B;**[!UICONTROL 卡片视图]**。
1. 导航到要查看的 3D 资产。
1. 点按3D资产的卡片。
1. 在3D资产的详细信息视图页面上，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击并拖动。 | 单指按住并拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击并拖动。 | 双指按并拖动。 |
   | **缩放相机** | 进出3D场景中的区域。 | 滚轮。 | 双指捏。 |
   | **重新输入相机** | 将相机重新调到3D场景中对象上的某个点。 | 双击. | 双击。 |
   | **重置** | 在页面的右下角附近，点按重置图标，以将视图目标点恢复到3D资产的中心。 重置还会使相机更近或更远地移开，以便以合理的查看大小完整地显示资产。 |  |  |
   | **全屏模式** | 要进入全屏模式，请点按页面右下角的全屏图标。 |  |  |

1. 在该页面的右上角，点按&#x200B;**[!UICONTROL 关闭]**&#x200B;以返回到“资产”页面。

## 查看3D媒体组件内的3D资产并与之交互{#interacting-with-asset-inside-three-d-media-component}

当网页处于&#x200B;**[!UICONTROL 编辑]**&#x200B;模式时，无法与3D资产进行交互。 要使资产具有交互性，您可以使用&#x200B;**[!UICONTROL 预览]**&#x200B;功能在页面编辑器中查看网页，并完全访问3D媒体组件的功能。

>[!IMPORTANT]
>
>只有在将3D媒体组件添加到网页并将3D资产分配给该组件后，才能完成此任务。 请参阅[将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)和[将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)。

另请参阅[使用软件界面预览资产](/help/assets/previewing-assets.md)。

**要在3D媒体组件内查看3D资产并与之交互，请执行以下操作：**

1. 当网页处于&#x200B;**[!UICONTROL 编辑]**&#x200B;模式时，请执行以下任一操作：

   * 在页面的右上角附近，单击&#x200B;**[!UICONTROL 预览]**&#x200B;以进入&#x200B;**[!UICONTROL 预览]**&#x200B;模式。
   * 从浏览器的页面URL中删除`/editor.html`。

完全交互的3D资产，如    ![在3D媒体组件内显示的3D资](/help/assets/assets-dm/3d-asset-in-3d-media.png)
产在预览模式下显示的完全交互的3D **** 资产。

1. 在&#x200B;**[!UICONTROL 预览]**&#x200B;模式下，执行以下任一操作：

   | 查看 | 描述 | 鼠标操作 | 触屏操作 |
   | --- | --- | --- | --- |
   | **转动相机** | 围绕 3D 场景和对象旋转视图。 | 左键单击并拖动。 | 单指按住并拖动。 |
   | **平移相机** | 向左、向右、向上或向下平移视图。 | 右键单击并拖动。 | 双指按并拖动。 |
   | **缩放相机** | 进出3D场景中的区域。 | 滚轮。 | 双指捏。 |
   | **重新输入相机** | 将相机重新调到3D场景中对象上的某个点。 | 双击. | 双击。 |
   | **重置** | 在页面的右下角附近，点按重置图标，以将视图目标点恢复到3D资产的中心。 重置还会使相机更近或更远地移开，以便以合理的查看大小完整地显示资产。 |  |  |
   | **全屏模式** | 要进入全屏模式，请点按页面右下角的全屏图标。 |  |  |

## 关于使用3D媒体组件{#working-with-three-d-media-component}

Dynamic Media包含Dynamic Media 3D媒体组件，您可以在Adobe Experience Manager Sites中使用该组件，以在网页上实现3D模型的交互式查看。

* [将3D媒体组件添加到页面模板](#adding-three-d-media-component-to-page-template)
* [将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)
   * [可选 — 配置3D媒体组件](#configuring-the-three-d-component)
* [将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)

## 将3D媒体组件添加到页面模板{#adding-three-d-media-component-to-page-template}

1. 导航到&#x200B;**[!UICONTROL 工具>常规>模板]**。
1. 导航到要在中启用3D组件的页面模板，然后选择该模板。
1. 点按&#x200B;**[!UICONTROL 编辑]**&#x200B;以打开模板。
1. 在页面右上角附近的下拉菜单中，选择&#x200B;**[!UICONTROL 结构]**&#x200B;模式（如果它尚未处于活动状态）。

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. 点按&#x200B;**[!UICONTROL 布局容器]**&#x200B;区域中的空区域以选择该区域并打开其关联的工具栏。
1. 在工具栏中，点按&#x200B;**[!UICONTROL Policy]**&#x200B;图标以打开&#x200B;**[!UICONTROL Policy Editor]**。
1. 在&#x200B;**[!UICONTROL 属性]**&#x200B;部分的&#x200B;**[!UICONTROL 允许的组件]**&#x200B;选项卡下，滚动到&#x200B;**[!UICONTROL Dynamic Media]**，然后展开列表并检查&#x200B;**[!UICONTROL 3D媒体]**。
1. 点按&#x200B;**[!UICONTROL Done]**&#x200B;以保存更改并关闭&#x200B;**[!UICONTROL 策略编辑器]**。

   现在，您可以将Dynamic Media 3D媒体组件放置到使用此模板的所有页面上。

## 将3D媒体组件添加到网页{#adding-the-three-d-media-component-to-a-web-page}

如果您将Experience Manager用作Web内容管理系统，则可以通过3D媒体组件将3D资产添加到网页。

另请参阅[将Dynamic Media资产添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

1. 打开Experience Manager站点，然后选择要将Dynamic Media 3D媒体组件添加到的网页。
1. 点按&#x200B;**[!UICONTROL 编辑]**（铅笔）图标，以便在页面编辑器中打开该页面。 确保在页面右上方附近选择了&#x200B;**[!UICONTROL 编辑]**&#x200B;模式。

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. 在工具栏中，点按侧面板图标，以切换或“打开”面板的显示。

1. 在侧面板中，点按加号图标以打开&#x200B;**[!UICONTROL 组件]**&#x200B;列表。

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. 将&#x200B;**[!UICONTROL 3D Media]**&#x200B;组件从&#x200B;**[!UICONTROL 组件]**&#x200B;列表中拖动到您希望3D查看器显示的页面位置。

现在，您可以为组件分配3D资产。

请参阅[将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)。

### 可选 — 配置3D媒体组件{#configuring-the-three-d-component}

1. 在Experience Manager站点页面编辑器中，选择您之前添加到页面的&#x200B;**[!UICONTROL 3D媒体查看器]**&#x200B;组件。
1. 点按&#x200B;**[!UICONTROL 配置]**&#x200B;图标（扳手），以打开组件配置对话框。

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. 在“3D媒体”对话框的“查看器预设”下拉列表中，选择&#x200B;**[!UICONTROL Dimensional]**&#x200B;以将维查看器预设分配给组件。

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. 点按右上角的复选标记以保存更改。

## 将3D资产分配给3D媒体组件{#assigning-a-three-d-asset-to-the-component}

将3D媒体组件添加到网页后，您可以为其分配3D资产。

请参阅[将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)。

1. 在“Experience Manager站点”页面编辑器中，单击&#x200B;**[!UICONTROL Assets]**&#x200B;图标以打开侧面板中的&#x200B;**[!UICONTROL Assets]** 。
1. 在下拉列表中，选择&#x200B;**[!UICONTROL 3D]**&#x200B;以仅显示3D资产文件类型。
1. 在侧面板中，搜索或滚动到要在编辑的页面上查看的3D资产。
1. 将3D资产从“资产”侧面板拖放到您之前添加到页面的&#x200B;**[!UICONTROL 3D Media]**&#x200B;组件上。

   ![将3D资产分配给3D媒体组件](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>当网页处于Experience Manager站点&#x200B;**[!UICONTROL 编辑]**&#x200B;模式时，3D媒体组件会显示3D资产，但无法与资产进行交互。 要使资产具有交互性，您可以使用&#x200B;**[!UICONTROL 预览]**&#x200B;功能在页面编辑器中查看网页，并完全访问3D媒体组件的功能。

## 发布静态Dynamic Media 3D资产{#publishing-three-d-assets}

Dynamic Media接受Dynamic Media中支持的各种3D文件格式为&#x200B;*静态内容*。 静态内容表示您可以上传和发布3D资产，但不支持与3D资产关联的&#x200B;*dynamic*&#x200B;图像或图像重新调整。 原因是Dynamic Media Imaging Server无法识别3D格式。 因此，在Dynamic Media中发布3D资产后，您即可复制一个即时URL。 3D资产的URL遵循常规的Dynamic Media URL结构。 但是，与Dynamic Media中的传统图像资产不同，您无法编辑资产URL中的任何参数。

另请参阅[获取静态资产的URL](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)。

在&#x200B;**[!UICONTROL 卡片视图]**&#x200B;中，资产名称的正下方以及其日期和时间左侧会显示一个小地球图标，指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

如果您使用Experience Manager作为WCM，请使用此发布方法直接将Dynamic Media 3D资产添加到您的网页上。

另请参阅[发布Dynamic Media资产](publishing-dynamicmedia-assets.md)。

另请参阅[发布页面](/help/sites-authoring/publishing-pages.md)。

**要发布静态Dynamic Media 3D资产，请执行以下操作：**

1. 打开3D资产（GLB、OBJ或STL文件格式），以便在资产详细信息页面中查看资产。
1. 在工具栏中，点按&#x200B;**[!UICONTROL 快速发布]**。

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. 点按&#x200B;**[!UICONTROL 关闭]**&#x200B;以退出对话框，并返回到资产详细信息页面。
1. 从3D资产文件名左侧的下拉列表中，点按&#x200B;**[!UICONTROL 演绎版]**。

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. 点按&#x200B;**[!UICONTROL 原始]**。 发布3D资产（或“已激活”）后，如果满足以下所有3D资产条件，则&#x200B;**[!UICONTROL URL]**&#x200B;按钮将显示在页面左下角附近：
   * 3D资产是受支持的格式（GLB、OBJ、STL和USDZ）。
   * 3D资产已摄取到Dynamic Media图像生产系统(IPS)中。
   * 3D资产已发布。

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. 点按&#x200B;**[!UICONTROL URL]**，以显示3D资产的直接生产URL，您可以在网页上复制和使用该URL。

### 使用维度查看器{#alternate-publish-methods}发布Dynamic Media 3D资产的替代方法

如果您执行&#x200B;*not*&#x200B;使用Experience Manager作为WCM，请使用以下两种方法发布Dynamic Media 3D资产。

* **[!UICONTROL URL]**  — 如果您 **** 使用的是第三方Web内容管理系统，并且希望使用维度查看器将Dynamic Media 3D资产关联到您的网页，请使用URL。

   请参阅[将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)。

* **[!UICONTROL 嵌入]**  — 当您 **** 想要使用维度查看器查看嵌入到网页中的Dynamic Media 3D资产时，请使用“嵌入”。将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 不允许在&#x200B;**[!UICONTROL Embed]**&#x200B;对话框中编辑代码。

   请参阅[在网页上嵌入Dynamic Media视频、图像查看器或维度查看器](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)。
