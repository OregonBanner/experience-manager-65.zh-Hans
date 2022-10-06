---
title: 使用引用和多个页面管理复合资产
description: 了解如何从内部创建对数字资产的引用 [!DNL Adobe InDesign], [!DNL Adobe Illustrator]和 [!DNL Adobe Photoshop]. 使用页面查看器功能可查看多页文件(如PDF、INDD、PPT、PPTX和AI文件)的单个子资产页面。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 1%

---

# 管理复合资产和多页资产 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可以识别上传的文件是否包含对存储库中已存在资产的引用。 此功能仅适用于支持的文件格式。 如果上传的资产包含对 [!DNL Experience Manager] 资产时，会在上传的资产和引用的资产之间创建双向链接。

除了消除冗余外，还会在 [!DNL Adobe Creative Cloud] 应用程序可增强协作，并提高用户的效率和工作效率。

[!DNL Experience Manager Assets] 支持双向引用。 您可以在上传文件的资产详细信息页面中找到引用的资产。 此外，您还可以在引用资产的资产详细信息页面中查看引用文件。

引用会根据引用资产的路径、文档ID和实例ID进行解析。

## [!DNL Adobe Illustrator]:将数字资产添加为参考 {#refai}

您可以从 [!DNL Adobe Illustrator] 文件。

1. 使用 [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)，获取本地文件系统上的数字资产。 导航到要引用的资产的文件系统位置。
1. 将资产从本地文件夹拖到 [!DNL Illustrator] 文件。

1. 保存 [!DNL Illustrator] 文件到已装载的驱动器，或 [上传](/help/assets/manage-assets.md#uploading-assets) 到 [!DNL Experience Manager] 存储库。

1. 工作流完成后，转到资产的资产详细信息页面。 对现有数字资产的引用列于 **[!UICONTROL 依赖关系]** 在 **[!UICONTROL 引用]** 列。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 在 **[!UICONTROL 依赖关系]** 也可以被当前文件以外的文件引用。 要查看资产的引用文件列表，请在 **[!UICONTROL 依赖关系]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 单击 **[!UICONTROL 查看属性]** 中。 在 [!UICONTROL 属性] 页面上，引用当前资产的文件列表将显示在 **[!UICONTROL 引用]** 列 **[!UICONTROL 基本]** 选项卡。

   ![在资产详细信息的引用列中查看Experience Manager Assets的引用](assets/asset-references.png)

   *图：资产详细信息中的资产引用。*

## [!DNL Adobe InDesign]:将数字资产添加为参考 {#add-aem-assets-as-references-in-adobe-indesign}

从 [!DNL InDesign] 文件中，将资产拖动到 [!DNL InDesign] 文件或导出 [!DNL InDesign] 文件作为ZIP存档。

中已存在引用的资产 [!DNL Experience Manager Assets]. 您可以通过 [配置InDesign Server](indesign.md). 中的嵌入式资产 [!DNL InDesign] 文件将提取为子资产。

>[!NOTE]
>
>如果 [!DNL InDesign Server] 代理， [!DNL InDesign] 文件的预览已嵌入到其XMP元数据中。 在这种情况下，并非明确需要缩略图提取。 但是，如果 [!DNL InDesign Server] 未代理，则必须明确提取缩略图以 [!DNL InDesign] 文件。

上传INDD文件后，通过查询具有 `xmpMM:InstanceID` 和 `xmpMM:DocumentID` 属性。

### 通过拖动资产创建引用 {#create-references-by-dragging-aem-assets}

此过程类似于 [将数字资产作为引用添加到Adobe Illustrator](#refai).

### 通过导出ZIP文件创建对资产的引用 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 执行 [创建工作流模型](/help/sites-developing/workflows-models.md) 创建新工作流。
1. 使用 [包功能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) of [!DNL Adobe InDesign] 以导出文档。 [!DNL Adobe InDesign] 可将文档和关联的资产作为包导出。在这种情况下，导出的文件夹包含 `Links` 包含子资产的文件夹 [!DNL InDesign] 文件。 的 `Links` 文件夹与INDD文件位于同一文件夹中。
1. 创建ZIP文件并将其上传到 [!DNL Experience Manager] 存储库。
1. 启动 `Unarchiver` 工作流。
1. 工作流完成后，Links文件夹中的引用会自动作为子资产进行引用。 要查看引用的资产列表，请导航到 [!DNL InDesign] 资产并关闭 [边栏](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]:将数字资产添加为参考 {#refps}

1. 使用 [!DNL Experience Manager] 桌面应用程序访问 [!DNL Experience Manager Assets]. 下载并显示本地文件系统上的资产。 使用 [!UICONTROL 置入链接的对象] 功能 [!DNL Adobe Photoshop]. 请参阅 [在桌面应用程序中放置资产](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. 保存 [!DNL Photoshop] 文件到已装载的驱动器或 [上传](/help/assets/manage-assets.md#uploading-assets) 到 [!DNL Experience Manager] 存储库。
1. 工作流完成后，对现有 [!DNL Experience Manager] 资产会在资产详细信息页面中列出。

   要查看引用的资产，请关闭 [边栏](/help/sites-authoring/basic-handling.md#rail-selector) （位于资产详细信息页面）。

1. 引用的资产还包含引用这些资产的资产列表。要查看引用的资产列表，请导航到资产详细信息页面并关闭 [边栏](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>复合资产中的资产还可以根据其文档ID和实例ID进行引用。 此功能在 [!DNL Adobe Illustrator] 和 [!DNL Adobe Photoshop] 版本。 对于其他资产，则会按照主复合资产中链接资产的相对路径进行引用，这与早期版本 [!DNL Experience Manager].

## 创建子资产 {#generate-subassets}

对于支持的多页格式资产 — PDF文件、AI文件、 [!DNL Microsoft PowerPoint] 和 [!DNL Apple Keynote] 文件和 [!DNL Adobe InDesign] 文件 —  [!DNL Experience Manager] 可以生成与原始资产的每个单独页面对应的子资产。 这些子资产与 *父项* 并促进多页面查看。 出于所有其他目的，子资产会像 [!DNL Experience Manager].

默认情况下，子资产生成处于禁用状态。 要启用子资产生成，请执行以下步骤：

1. 登录 [!DNL Experience Manager] 作为管理员。 访问 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 选择 **[!UICONTROL DAM更新资产]** 工作流和单击 **[!UICONTROL 编辑]**.
1. 单击 **[!UICONTROL 切换侧面板]** 并找到 **[!UICONTROL 创建子资产]** 中。 将步骤添加到工作流。 单击&#x200B;**[!UICONTROL 同步]**。

要生成子资产，请执行以下操作之一：

* 新资产：的 [!UICONTROL DAM更新资产] 工作流会对上传到的任何新资产执行 [!DNL Experience Manager]. 子资产会为新的多页面资产自动生成。
* 现有的多页资产：手动执行 [!UICONTROL DAM更新资产] 工作流执行以下任一步骤：

   * 选择资产并单击 [!UICONTROL 时间轴] 打开左侧面板。 或者，使用键盘快捷键 `alt + 3`. 单击 [!UICONTROL 启动工作流]，选择 [!UICONTROL DAM更新资产]，单击 [!UICONTROL 开始]，然后单击 [!UICONTROL 继续].
   * 选择资产并单击 [!UICONTROL 创建] > [!UICONTROL 工作流] 中。 从弹出对话框中，选择 [!UICONTROL DAM更新资产] 工作流，单击 [!UICONTROL 开始]，然后单击 [!UICONTROL 继续].

特别是对于Microsoft Word文档，请执行 **[!UICONTROL DAM解析Word文档]** 工作流。 它会生成 `cq:Page` 组件。 从文档提取的图像将从 `cq:Page` 组件。 即使禁用了子资产生成，也会提取这些图像。

>[!NOTE]
>
>在 [!UICONTROL 创建子资产流程 — 步骤属性] in [!UICONTROL 进程参数]，您可以指定 [!DNL Experience Manager] 生成。 默认值为 5。要生成所有子资产，请将字段留空。 如果字段为负数，则不会生成子资产。

## 查看子资产 {#viewing-subassets}

只有在生成子资产并且该子资产可用于选定的多页面资产时，才会显示子资产。 要查看生成的子资产，请打开多页面资产。 在页面的左上角，单击 ![用于打开左边栏的选项](assets/do-not-localize/aem_leftrail_contentonly.png) 单击 **[!UICONTROL 子资产]** 列表。 选择 **[!UICONTROL 子资产]** 列表。 或者，使用键盘快捷键 `alt + 5`.

![查看多页面资产的子资产](assets/view_subassets_simulation.gif)

## 查看多页文件的页面 {#view-pages-of-a-multi-page-file}

您可以使用的页面查看器功能查看多页文件，如PDF、INDD、PPT、PPTX和AI文件 [!DNL Experience Manager Assets]. 打开多页面资产并单击 **[!UICONTROL 查看页面]** 的上角。 打开的页面查看器会显示资产的页面以及用于浏览和缩放每个页面的控件。

![查看和查看多页面资产的页面](assets/view_multipage_asset_fmr.gif)

对于 [!DNL InDesign]，您可以使用 [!DNL InDesign Server]. 如果页面的预览是在 [!DNL InDesign] 创建文件，然后 [!DNL InDesign Server] 页面提取不是必需的。

以下选项在工具栏、左边栏和“页面查看器”控件中可用：

* **[!UICONTROL 桌面操作]** 使用打开或显示特定子资产 [!DNL Experience Manager] 桌面应用程序。 了解如何 [配置桌面操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2) 如果您使用 [!DNL Experience Manager] 桌面应用程序。

* **[!UICONTROL 属性]** 选项 [!UICONTROL 属性] 页面。

* **[!UICONTROL 注释]** 选项允许您在特定子资产中添加批注。 打开父资产进行查看时，系统会收集并显示您在单独的子资产上使用的注释。

* **[!UICONTROL 页面概述]** 选项可同时显示所有子资产。

* **[!UICONTROL 时间轴]** 选项 ![用于打开左边栏的选项](assets/do-not-localize/aem_leftrail_contentonly.png) 显示文件的活动流。

## 最佳实践和限制 {#best-practice-limitation-tips}

* 子资产生成对任何 [!DNL Experience Manager] 部署。 如果您在上传复杂资产时生成子资产，请在DAM更新资产工作流中添加该步骤。 如果要按需生成子资产，请创建单独的工作流以生成子资产。 利用专用工作流，可跳过DAM更新资产工作流中的其他步骤并保存计算资源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager中配置桌面操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop中创建链接的智能对象](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [在Adobe InDesign中放置图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)

