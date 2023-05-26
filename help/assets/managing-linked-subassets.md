---
title: 管理包含引用和多个页面的复合资产
description: 了解如何在中创建对数字资产的引用 [!DNL Adobe InDesign]， [!DNL Adobe Illustrator]、和 [!DNL Adobe Photoshop]. 使用“页面查看器”功能可以查看多页文件(如PDF、INDD、PPT、PPTX和AI文件)的各个子资源页面。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# 管理复合和多页资源 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可以识别上传的文件是否包含对存储库中已存在的资源的引用。 此功能仅适用于支持的文件格式。 如果上传的资源包含对的任何引用 [!DNL Experience Manager] 资源时，将在上传的资源和引用的资源之间创建一个双向链接。

除了消除冗余之外，还引用中的资产 [!DNL Adobe Creative Cloud] 应用程序增强了协作，提高了用户的效率和生产力。

[!DNL Experience Manager Assets] 支持双向引用。 您可以在上传文件的资源详细信息页面中找到引用的资源。 此外，还可以在引用资源的资源详细信息页面中查看引用文件。

引用是根据引用的资产的路径、文档ID和实例ID解析的。

## [!DNL Adobe Illustrator]：添加数字资产作为引用 {#refai}

您可以从中引用现有的数字资产 [!DNL Adobe Illustrator] 文件。

1. 使用 [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)，获取本地文件系统上的数字资产。 导航到要引用的资源的文件系统位置。
1. 将资源从本地文件夹拖到 [!DNL Illustrator] 文件。

1. 保存 [!DNL Illustrator] 文件到已装入的驱动器，或 [上传](/help/assets/manage-assets.md#uploading-assets) 到 [!DNL Experience Manager] 存储库。

1. 工作流完成后，转到资产的资产详细信息页面。 对现有数字资产的引用列在 **[!UICONTROL 依赖关系]** 在 **[!UICONTROL 引用]** 列。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 下显示的引用资产 **[!UICONTROL 依赖关系]** 也可以由当前文件以外的文件引用。 要查看某个资源的引用文件列表，请单击下方的资源 **[!UICONTROL 依赖关系]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 单击 **[!UICONTROL 查看属性]** 工具栏中。 在 [!UICONTROL 属性] 页面上，引用当前资源的文件列表显示在 **[!UICONTROL 引用]** 中的列 **[!UICONTROL 基本]** 选项卡。

   ![在资源详细信息中的引用列中查看Experience Manager Assets的引用](assets/asset-references.png)

   *图：资源详细信息中的资源引用。*

## [!DNL Adobe InDesign]：添加数字资产作为引用 {#add-aem-assets-as-references-in-adobe-indesign}

要从中引用数字资产，请执行以下操作 [!DNL InDesign] 文件，将资产拖到 [!DNL InDesign] 文件或导出 [!DNL InDesign] 文件作为ZIP存档。

引用的资产已存在于 [!DNL Experience Manager Assets]. 您可以通过以下方式提取子资源 [配置InDesign Server](indesign.md). 中的嵌入式资产 [!DNL InDesign] 文件将提取为子资产。

>[!NOTE]
>
>如果 [!DNL InDesign Server] 被代理了， [!DNL InDesign] 文件的XMP元数据中嵌入了其预览。 在这种情况下，不会明确要求提取缩略图。 但是，如果 [!DNL InDesign Server] 未进行代理，必须显式提取缩略图 [!DNL InDesign] 文件。

上传INDD文件时，将通过查询具有以下特征的资产来获取引用： `xmpMM:InstanceID` 和 `xmpMM:DocumentID` 属性。

### 通过拖动资产创建引用 {#create-references-by-dragging-aem-assets}

此过程类似于 [在Adobe Illustrator中添加数字资源作为引用](#refai).

### 通过导出ZIP文件创建对资产的引用 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 执行以下步骤： [创建工作流模型](/help/sites-developing/workflows-models.md) 以创建新工作流。
1. 使用 [包功能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) 之 [!DNL Adobe InDesign] 以导出文档。 [!DNL Adobe InDesign] 可将文档和链接的资产导出为资源包。 在这种情况下，导出的文件夹包含 `Links` 文件夹中包含子资产 [!DNL InDesign] 文件。 此 `Links` 文件夹与INDD文件位于同一文件夹中。
1. 创建ZIP文件并将其上传到 [!DNL Experience Manager] 存储库。
1. 启动 `Unarchiver` 工作流。
1. 工作流完成后，链接文件夹中的引用将自动引用为子资产。 要查看引用的资源列表，请导航到 [!DNL InDesign] 资产并关闭 [边栏](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]：添加数字资产作为引用 {#refps}

1. 使用 [!DNL Experience Manager] 要访问的桌面应用程序 [!DNL Experience Manager Assets]. 下载并显示本地文件系统上的资产。 使用 [!UICONTROL 置入已链接] 中的功能 [!DNL Adobe Photoshop]. 参见 [将资产放入桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. 保存位置 [!DNL Photoshop] 文件到已装入的驱动器或 [上传](/help/assets/manage-assets.md#uploading-assets) 到 [!DNL Experience Manager] 存储库。
1. 工作流完成后，对现有 [!DNL Experience Manager] 资产将在“资产详细信息”页面中列出。

   要查看引用的资产，请关闭 [边栏](/help/sites-authoring/basic-handling.md#rail-selector) 在资源详细信息页面中。

1. 引用的资产还包含从中引用它们的资产的列表。 要查看引用的资产列表，请导航到资产详细信息页面并关闭 [边栏](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>复合资产中的资产也可以根据其文档ID和实例ID进行引用。 此功能可用于 [!DNL Adobe Illustrator] 和 [!DNL Adobe Photoshop] 仅限版本。 对于其他人，引用是基于主复合资产中关联资产的相对路径，就像在早期版本中一样 [!DNL Experience Manager].

## 创建子资产 {#generate-subassets}

对于支持的多页格式资源 — PDF文件、AI文件、 [!DNL Microsoft PowerPoint] 和 [!DNL Apple Keynote] 文件，和 [!DNL Adobe InDesign] 文件 —  [!DNL Experience Manager] 可以生成与原始资产的每个单独页面对应的子资产。 这些子资产链接到 *父级* 资源并促进多页面查看。 对于所有其他目的，子资产在中被视为普通资产。 [!DNL Experience Manager].

默认情况下，子资源生成处于禁用状态。 要启用子资产生成，请执行以下步骤：

1. 登录 [!DNL Experience Manager] 作为管理员。 访问 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 选择 **[!UICONTROL DAM更新资产]** 工作流并单击 **[!UICONTROL 编辑]**.
1. 单击 **[!UICONTROL 切换侧面板]** 并找到 **[!UICONTROL 创建子资产]** 步骤。 将步骤添加到工作流。 单击&#x200B;**[!UICONTROL 同步]**。

要生成子资产，请执行下列操作之一：

* 新资产： [!UICONTROL DAM更新资产] 工作流会在上传到的任何新资产上执行 [!DNL Experience Manager]. 为新的多页面资源自动生成子资源。
* 现有的多页面资源：手动执行 [!UICONTROL DAM更新资产] 工作流会遵循以下任一步骤：

   * 选择资源并单击 [!UICONTROL 时间线] 以打开左侧面板。 或者，使用键盘快捷键 `alt + 3`. 单击 [!UICONTROL 启动工作流]，选择 [!UICONTROL DAM更新资产]，单击 [!UICONTROL 开始]，然后单击 [!UICONTROL 继续].
   * 选择资源并单击 [!UICONTROL 创建] > [!UICONTROL 工作流] 工具栏中。 从弹出对话框中，选择 [!UICONTROL DAM更新资产] 工作流，单击 [!UICONTROL 开始]，然后单击 [!UICONTROL 继续].

对于Microsoft Word文档，请执行 **[!UICONTROL DAM解析Word文档]** 工作流。 它会生成 `cq:Page` Microsoft Word文档内容中的组件。 从文档提取的图像将被引用 `cq:Page` 组件。 即使禁用子资产生成，也会提取这些图像。

>[!NOTE]
>
>在 [!UICONTROL 创建子资产进程 — 步骤属性] 在 [!UICONTROL 进程参数]，您可以指定满足以下条件的子资产数量： [!DNL Experience Manager] 生成。 默认值为 5。要生成所有子资产，请将字段留空。 如果字段为负，则不会生成任何子资产。

## 查看子资产 {#viewing-subassets}

仅当生成了子资产且可用于所选多页资产时，才会显示子资产。 要查看生成的子资产，请打开多页资产。 在页面的左上角区域，单击 ![打开左边栏的选项](assets/do-not-localize/aem_leftrail_contentonly.png) 并单击 **[!UICONTROL 子资产]** 从名单上。 当您选择时 **[!UICONTROL 子资产]** 从名单上。 或者，使用键盘快捷键 `alt + 5`.

![查看多页资源的子资源](assets/view_subassets_simulation.gif)

## 查看多页文件的页面 {#view-pages-of-a-multi-page-file}

您可以使用的“页面查看器”功能查看多页文件，如PDF、INDD、PPT、PPTX和AI文件 [!DNL Experience Manager Assets]. 打开多页资源并单击 **[!UICONTROL 查看页面]** 从页面的左上角。 打开的页面查看器会显示资产的页面，以及用于在每个页面中浏览和缩放的控件。

![查看并查看多页资源的页面](assets/view_multipage_asset_fmr.gif)

对象 [!DNL InDesign]，您可以使用提取页面 [!DNL InDesign Server]. 如果页面预览是在以下期间保存的： [!DNL InDesign] 创建文件，然后 [!DNL InDesign Server] 不是页面提取所必需的。

工具栏、左边栏和页面查看器控件中提供了以下选项：

* **[!UICONTROL 桌面操作]** 要打开或显示特定子资产，请使用 [!DNL Experience Manager] 桌面应用程序。 了解如何 [配置桌面操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) 如果您使用 [!DNL Experience Manager] 桌面应用程序。

* **[!UICONTROL 属性]** 选项打开 [!UICONTROL 属性] 页面。

* **[!UICONTROL 批注]** 选项允许您为特定子资源添加注释。 在打开父资产进行查看时，将收集并显示您在各个子资产上使用的注释。

* **[!UICONTROL 页面概述]** 选项同时显示所有子资产。

* **[!UICONTROL 时间线]** 选项（单击后左边栏中的） ![打开左边栏的选项](assets/do-not-localize/aem_leftrail_contentonly.png) 显示文件的活动流。

## 最佳实践和限制 {#best-practice-limitation-tips}

* 在任何情况下，子资产生成都可能会占用大量资源 [!DNL Experience Manager] 部署。 如果您在上传复杂资产时生成子资产，请在DAM更新资产工作流中添加该步骤。 如果要按需生成子资产，请创建单独的工作流以生成子资产。 专用工作流允许您跳过DAM更新资产工作流中的其他步骤并保存计算资源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager中配置桌面操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop中创建链接智能对象](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [在Adobe InDesign中置入图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)

