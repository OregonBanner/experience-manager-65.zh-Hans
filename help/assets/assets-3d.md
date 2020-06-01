---
title: 在Dynamic Media中处理3D资产
seo-title: 在Dynamic Media中处理3D资产
description: 了解如何在Dynamic Media中使用3D资产
seo-description: 了解如何在Dynamic Media中使用3D资产
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and AEM as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 46848fee0a3f838354ec65f2ea733cf70ac53deb
workflow-type: tm+mt
source-wordcount: '2162'
ht-degree: 4%

---


# 在Dynamic Media中处理3D资产 {#working-with-three-d-assets-dm}

Dynamic Media可让您将3D资产作为沉浸式体验进行上传、管理、视图和交付。

* 单击发布(使用工 **[!UICONTROL 具栏上的]** “快速发布”)3D图像以生成其URL。
* 借助以Adobe Dimension为后盾的高质量交互式维查看器预设，优化了对查看3D资产的支持。 查看器预设包括一组交互式相机控件，这些控件可让您绕行、缩放和平移。
* 通过3D Media WCM组件，您可以轻松地将3D资产添加到AEM Sites页面。

在Dynamic Media中不安装或配置任何类型的3D资产。

![3d鞋](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media中支持的3D文件格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支持以下3D文件格式：

| 3D文件扩展名 | 文件格式 | MIME类型 | 注释 |
|---|---|---|---|
| GLB | 二进制GL传输 | 模型/gltf二进制 | 将纹理与资产一起包含，而不是将它们作为外部图像引用。 |
| OBJ | WaveFront 3D对象文件 | application/x-tgif |  |
| STL | 光固化成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用场景描述Zip存档 | model/vnd.usdz+zip | *仅支持摄取； 不提供查看或交互。* USDZ是Apple的专有3D格式，只能由Safari或iOS视图。 |

## 快速开始: Dynamic Media中的3D资产 {#quick-start-three-d}

以下工作流分步说明旨在帮助您在Dynamic Media - Scene7模式下快速设置并运行3D资产。

>[!NOTE]
>
>3D资源在Dynamic Media —— 混合模式中不受支持。

在Dynamic Media中处理3D资产之前，请确保AEM管理员已在Dynamic Media - Scene7模式中启用和配置Dynamic Media云服务。

请参 [阅配置Dynamic Media](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) - Scene7模式和Dynamic Media - Scene7模 [式疑难解答中的配置Dynamic Media Cloud Services。](/help/assets/troubleshoot-dms7.md)

1. **上传3D资产**

   * [上传要在Dynamic Media中使用的3D资产](/help/assets/managing-assets-touch-ui.md#uploading-assets)。
   * [支持的3D文件格式，可在Dynamic Media中上传](#supported-three-d-file-formats-in-dm)。

1. **管理3D资产**

   * 组织和搜索3D资产

      * [组织数字资产](/help/assets/organize-assets.md#organize-digital-assets)。
      * [搜索3D资产](/help/assets/search-assets.md)。
      * [使用自定义谓词筛选搜索结果](/help/assets/search-assets.md#custompredicates)。
   * 视图3D资源

      * [查看3D资产并与之交互](#viewing-three-d-assets)。
      * [管理维查看器预设](/help/assets/managing-viewer-presets.md)。
   * 使用3D资产元数据

      * [管理数字资产的元数据](/help/assets/metadata.md).
      * [元数据架构](/help/assets/metadata-schemas.md).



1. **发布3D资产**

   * [发布Dynamic Media 3D资源](#publishing-three-d-assets)

## 关于查看3D资产并与之交互 {#viewing-three-d-assets}

本节介绍如何以两种不同的方式视图3D资产并与之交互： 从资产详细信息页面和站点中的3D媒体组件。

交互式3D查看器包括一组交互式相机控件，这些控件可让您绕行、缩放和平移3D资产。

请注意，在“资产详细信息”页面视图打开3D资产所花费的时间取决于多个因素。 这些因素包括如下几项：

* 服务器带宽。
* 服务器延迟
* 图像的复杂性。

此外，在以交互方式操作相机时，还要考虑客户端计算机（如工作站、笔记本或移动触控设备）的功能。 具备良好图形功能的相当强大的系统可以使交互式 3D 查看体验更流畅、更舒适。

>[!TIP]
>
>您可以在查看器预设编辑器中打开维查看器预设，以练习在3D资产上导航，而无需先上传任何3D文件。 维查看器预设包含一个内置的3D资源，供您进行交互。
>
>See [Managing viewer presets](/help/assets/managing-viewer-presets.md).

## 从资产详细信息页面查看3D资产并与之交互 {#viewing-three-d-assets-from-asset-details-page}

另请参阅 [使用软件界面预览资产](/help/assets/previewing-assets.md)。

**从资产详细信息页面视图3D资产并与之交互**

1. 确保您已将 3D 资产上传到 AEM。

   请参 [阅上传要在Dynamic Media中使用的3D资产](/help/assets/managing-assets-touch-ui.md#uploading-assets)。

1. 从AEM的导航页 **[!UICONTROL 面]** ，点按 **[!UICONTROL 资产>文件]**。
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.
1. 导航到要查看的 3D 资产。
1. 点按3D资产的卡片，以在资产详细信息页面中将其打开。
1. 在3D资产的详细信息视图页面上，执行下列任一操作：

   * **旋转相机** -围绕3D场景和对象绕行视图。
      * _鼠标_: 左键单击+拖动。
      * _触摸屏_: 单指按+拖动。
   * **平移相机** -向左、向右、向上或向下平移视图。
      * _鼠标_: 右键单击并拖动。
      * _触摸屏_: 双指按+拖动。
   * **缩放相机** -缩放相机以移入和移出3D场景的区域。
      * _鼠标_: 滚轮。
      * _触摸屏_: 两指捏合。
   * **重新输入相机** -将相机重新输入到3D场景中对象上的某个点。
      * _鼠标_: 多次单击。
      * _触摸屏_: 多次点击。
   * **重置** -在页面的右下角附近，点按重置图标以将视图目标点恢复到3D资产的中心。 重置还会使相机更近或更远地移动，以便以合理的查看大小完整显示资产。
   * **全屏模式** -要进入全屏模式，请点按页面右下角的全屏图标。

1. 在该页面的右上角，点按&#x200B;**[!UICONTROL 关闭]**&#x200B;以返回到“资产”页面。

## 在3D媒体组件中查看3D资产并与之交互 {#interacting-with-asset-inside-three-d-media-component}

当网页处于“编 **[!UICONTROL 辑]** ”模式时，不能与3D资源进行交互。 要使资产具有交互性，您可以 **[!UICONTROL 使用预览]** 功能在页面编辑器中视图网页，并完全访问3D媒体组件的功能。

>[!IMPORTANT]
>
>只有在将3D媒体组件添加到网页并将3D资产分配给该组件后，您才能完成此任务。 请 [参阅将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)[和将3D资产分配到3D媒体组件](#assigning-a-three-d-asset-to-the-component)。

另请参阅 [使用软件界面预览资产](/help/assets/previewing-assets.md)。

**视图3D媒体组件中的3D资产并与之交互**

1. 当网页处于编辑模 **[!UICONTROL 式时]** ，请执行下列操作之一：

   * 在页面的右上角附近，单击 **[!UICONTROL 预览]** ，进 **[!UICONTROL 入预览模式]** 。
   * 从浏 `/editor.html` 览器中的页面URL中删除。
   ![3D资产显示在3D媒体组件内部](/help/assets/assets-dm/3d-asset-in-3d-media.png)在预览模式下显示的完全交互 **[!UICONTROL 式3D资]** 产。

1. 在预览 **[!UICONTROL 模式下]** ，请执行下列任一操作：

   * **旋转相机** -围绕3D场景和对象绕行视图。
      * _鼠标_: 左键单击+拖动。
      * _触摸屏_: 单指按+拖动。
   * **平移相机** -向左、向右、向上或向下平移视图。
      * _鼠标_: 右键单击并拖动。
      * _触摸屏_: 双指按+拖动。
   * **缩放相机** -缩放相机以移入和移出3D场景的区域。
      * _鼠标_: 滚轮。
      * _触摸屏_: 两指捏合。
   * **重新输入相机** -将相机重新输入到3D场景中对象上的某个点。
      * _鼠标_: 多次单击。
      * _触摸屏_: 多次点击。
   * **重置** -在页面的右下角附近，点按重置图标以将视图目标点恢复到3D资产的中心。 重置还会使相机更近或更远地移动，以便以合理的查看大小完整显示资产。
   * **全屏模式** -要进入全屏模式，请点按页面右下角的全屏图标。

## 关于使用3D媒体组件 {#working-with-three-d-media-component}

Dynamic Media包含Dynamic Media 3D Media组件，可在AEM Sites中使用它在网页上启用3D模型的交互式查看。

* [将3D媒体组件添加到页面模板](#adding-three-d-media-component-to-page-template)
* [将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)
   * [可选——配置3D媒体组件](#configuring-the-three-d-component)
* [将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)


## 将3D媒体组件添加到页面模板 {#adding-three-d-media-component-to-page-template}

1. 导航到 **[!UICONTROL 工具>常规>模板]**。
1. 导航到要在其中启用3D组件的页面模板，然后选择该模板。
1. 点按 **[!UICONTROL 编辑]** ，打开模板。
1. 在页面右上角的下拉菜单中，选择“结构 **[!UICONTROL 模式]** ”（如果它尚未处于活动状态）。

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. 点按布局容器区域 **[!UICONTROL 中的空]** ，以选择该区域并打开其关联的工具栏。
1. 在工具栏中，点按 **[!UICONTROL 策略]** 图标以打开策 **[!UICONTROL 略编辑器]**。
1. 在“属 **[!UICONTROL 性]** ”部分的“允许的组 **[!UICONTROL 件]** ”选项卡下，滚动至 **[!UICONTROL Dynamic Media]**，然后展开列表并检 ****&#x200B;查3D媒体。
1. 点按 **[!UICONTROL 完成]** ，以保存更改并关闭策 **[!UICONTROL 略编辑器]**。

   您现在可以将Dynamic Media 3D Media组件放置到使用此模板的所有页面上。

## 将3D媒体组件添加到网页 {#adding-the-three-d-media-component-to-a-web-page}

如果您使用Adobe Experience Manager作为Web内容管理系统，则可以通过3D媒体组件将3D资产添加到网页。

See also [Adding Dynamic Media assets to pages](/help/assets/adding-dynamic-media-assets-to-pages.md).

1. 打开AEM Sites，选择要向其添加Dynamic Media 3D Media组件的网页。
1. 点按编 **[!UICONTROL 辑]** （铅笔）图标以在页面编辑器中打开页面。 确保 **[!UICONTROL 在页]** 面的右上角附近选择了“编辑”模式。

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. 在工具栏中，点按侧面板图标以切换或“打开”面板的显示。

1. 在侧面板中，点按加号图标以打开组 **[!UICONTROL 件]** 列表。

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. 将3 **[!UICONTROL D Media]** 组件从“ **[!UICONTROL 组件]** ”列表拖到页面上希望显示3D查看器的位置。

您现在可以为组件分配3D资产。

请 [参阅将3D资产分配给3D媒体组件](#assigning-a-three-d-asset-to-the-component)。

### 可选——配置3D媒体组件 {#configuring-the-three-d-component}

1. 在AEM Sites页面编辑器中，选 **[!UICONTROL 择之前添加到页面的]** 3D Media Viewer组件。
1. 点按配 **[!UICONTROL 置图标]** （扳手）以打开组件配置对话框。

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. 在“3D媒体”对话框的“查看器预设”下拉列表中，选 **[!UICONTROL 择]** “维”以将维查看器预设分配给组件。

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. 在右上角，点按复选标记以保存更改。

## 将3D资产分配给3D媒体组件 {#assigning-a-three-d-asset-to-the-component}

在将3D媒体组件添加到网页后，您可以为其分配3D资产。

请参 [阅将3D媒体组件添加到网页](#adding-the-three-d-media-component-to-a-web-page)。

1. 在AEM Sites页面编辑器中，单击 **[!UICONTROL 资产]** 图标以 **[!UICONTROL 打开侧]** 面板中的资产。
1. 在下拉列表中，选择 **[!UICONTROL 3D]** 以仅显示3D资产文件类型。
1. 在侧面板中，搜索或滚动到要在所编辑页面上视图的3D资产。
1. 将3D资产从“资产”侧面板拖放到您之前 **[!UICONTROL 添加到页面的]** 3D媒体组件上。

   ![将3d资产分配给3d媒体组件](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>当网页处于AEM Sites编辑模 **[!UICONTROL 式]** 时，3D Media组件会显示3D资产，但无法与资产交互。 要使资产具有交互性，您可以 **[!UICONTROL 使用预览]** 功能在页面编辑器中视图网页，并完全访问3D媒体组件的功能。

## Publishing Dynamic Media 3D assets {#publishing-three-d-assets}

Dynamic Media接受Dynamic Media中支持的各种3D文件格 *式作为静* 态内容。 静态内容意味着您可以上传和发布3D资产，但不支持与 *3D资产* 相关的动态成像或图像重新编排。 原因是Dynamic Media Imaging Server无法识别3D格式。 因此，在Dynamic Media中发布3D资产后，您可以复制一个即时URL。 3D资产的URL遵循通常的Dynamic Media URL结构。 但是，与Dynamic Media中的传统图像资产不同，您无法编辑资产URL中的任何参数。

在卡 **[!UICONTROL 片视图]**&#x200B;中，资产名称的正下方以及日期和时间的左侧会显示一个小地球图标，以指示资产已发布。 在&#x200B;**[!UICONTROL 列表视图]**&#x200B;中，**[!UICONTROL 已发布]**&#x200B;列显示已发布的资产和未发布的资产。

See also [Publishing Dynamic Media assets](publishing-dynamicmedia-assets.md).

另请参阅 [发布页面](/help/sites-authoring/publishing-pages.md)。

>[!MORELIKETHIS]
>
>如果您使用的是第三方Web内容管理系统，则可以将3D资产链接或嵌入到您的网页。
>
>请参阅[将 URL 关联到您的 Web 应用程序](linking-urls-to-yourwebapplication.md)。


**要发布Dynamic Media 3D资产，请执行以下操作：**

1. 打开3D资产（GLB、OBJ或STL文件格式），在资产详细信息页面中视图它。
1. On the toolbar, tap **[!UICONTROL Quick Publish]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. 点按 **[!UICONTROL 关闭]** ，以退出对话框并返回到资产详细信息页面。
1. 从3D资产文件名左侧的下拉列表中，点按演绎 **[!UICONTROL 版]**。

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. 点按 **[!UICONTROL 原始]**。 发布（或“激活”）3D资产后，如果满足以下所有3D资产条件，则URL按钮将出现在页面左下角附近：
   * 3D资产是受支持的格式（GLB、OBJ、STL和USDZ）。
   * 3D资源已被引入Dynamic Media图像生产系统(IPS)。
   * 将发布3D资产。
   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. 点 **[!UICONTROL 按]** URL以显示3D资产的生产URL。
