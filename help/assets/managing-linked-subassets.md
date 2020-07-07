---
title: 使用中的引用和多页资产管理复合资产 [!DNL Adobe Experience Manager]。
description: 了解如何从中创建数字资产引用 [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]。 使用页面查看器功能可视图多页文件（如PDF、INDD、PPT、PPTX和AI文件）的各个子资产页面。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 0%

---


# 管理复合和多页资产 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可以标识已上传的文件是否包含对存储库中已存在资产的引用。 此功能仅适用于支持的文件格式。 如果上传的资产包含对资产的任何引 [!DNL Experience Manager] 用，则会在上传的资产和引用的资产之间创建双向链接。

Besides eliminating redundancy, referencing the assets in [!DNL Adobe Creative Cloud] applications enhances collaboration and increases the efficiency and productivity of users.

[!DNL Experience Manager Assets] 支持双向引用。 您可以在已上传文件的资产详细信息页面中查找引用的资产。 此外，您还可以视图引用资产的资产详细信息页面中的引用文件。

引用会根据引用资产的路径、文档ID和实例ID解析。

## 将数字资产作为引用添加到 [!DNL Adobe Illustrator] {#refai}

You can reference existing digital assets from within an [!DNL Adobe Illustrator] file.

1. 使用 [Experience Manager桌面应用](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)，在本地文件系统上获取数字资产。 导航到要引用的资产的文件系统位置。
1. Drag the asset from the local folder to the [!DNL Illustrator] file.

1. Save the [!DNL Illustrator] file to the mounted drive, or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the [!DNL Experience Manager] repository.

1. 工作流完成后，转到资产的资产详细信息页面。 对现有数字资产的引用列在“引 **[!UICONTROL 用]** ”列的“ **[!UICONTROL 依赖项]** ”下。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. “依赖关系”下显示的 **[!UICONTROL 引用资]** 产也可由当前文件以外的文件引用。 要视图引用资产文件的列表，请在依赖项下单击资产 ****。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 单击 **[!UICONTROL 工具栏中]** 的视图属性。 在“属 [!UICONTROL 性] ”页中，引用当前资产的文件列表显示在“基本”选项 **[!UICONTROL 卡的]** “引用 **** ”列下方。

   ![视图资产详细信息中引用列中Experience Manager资产的引用](assets/asset-references.png)

   *图： 资产详细信息中的资产引用。*

## 将数字资产作为引用添加到 [!DNL Adobe InDesign] {#add-aem-assets-as-references-in-adobe-indesign}

To reference digital assets from within an [!DNL InDesign] file, either drag assets to the [!DNL InDesign] file or export the [!DNL InDesign] file as a ZIP archive.

中已存在引用的资产 [!DNL Experience Manager Assets]。 您可以通过配置InDesign [Server提取子资产](indesign.md)。 文件中的嵌入 [!DNL InDesign] 资产会被提取为子资产。

>[!NOTE]
>
>如果代 [!DNL InDesign Server] 理，则 [!DNL InDesign] 文件的预览将嵌入到其XMP元数据中。 在这种情况下，缩略图提取不是明确必需的。 但是，如果未 [!DNL InDesign Server] 代理，则必须显式提取文件的缩 [!DNL InDesign] 略图。

### 通过拖动资产创建引用 {#create-references-by-dragging-aem-assets}

This procedure is similar to [add digital assets as references in Adobe Illustrator](#refai).

### Create references to assets by exporting a ZIP file {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Perform the steps in [Create workflow models](/help/sites-developing/workflows-models.md) to create a new workflow.
1. Use the Package feature of [!DNL Adobe InDesign] to export the document. [!DNL Adobe InDesign] 可将文档和关联的资产作为包导出。In this case, the exported folder contains a Links folder that contains sub-assets in the [!DNL InDesign] file.
1. Create a ZIP file and upload it to the [!DNL Experience Manager] repository.
1. Start the `Unarchiver` workflow.
1. 该工作流完成后，Links文件夹中的引用将自动作为子资产进行引用。 To view a list of referred assets, navigate to the asset details page of the [!DNL InDesign] asset and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## 将数字资产作为引用添加到 [!DNL Adobe Photoshop] {#refps}

1. 使用 [!DNL Experience Manager] 桌面应用程序访 [!DNL Experience Manager Assets]问。 下载并显示本地文件系统上的资源。 使用中 [!UICONTROL 的“置入链接] ”功能 [!DNL Adobe Photoshop]。 请参 [阅将资源放入桌面应用程序](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Save in [!DNL Photoshop] file to the mounted drive or or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the [!DNL Experience Manager] repository.
1. After the workflow completes, the references to existing [!DNL Experience Manager] assets are listed in the asset details page.

   To view the referenced assets, close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector) in the asset details page.

1. The referenced assets also contain the list of assets they are referenced from. To view a list of referenced assets, navigate to the asset details page and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>复合资产中的资产也可以根据其文档ID和实例ID进行引用。 此功能仅在和 [!DNL Adobe Illustrator] 版本 [!DNL Adobe Photoshop] 中可用。 For others, referencing is done on the basis of relative path of linked assets in the main compound asset as done in earlier versions of [!DNL Experience Manager].

## 创建子资产 {#generate-subassets}

对于多页格式(PDF文件、AI文件、 [!DNL Microsoft PowerPoint] 文 [!DNL Apple Keynote] 件以及文件)的受支 [!DNL Adobe InDesign] 持资 [!DNL Experience Manager] 产，可以生成与原始资产的每个单独页面对应的子资产。 这些子资产与父资产 *相关联* ，有助于进行多页视图。 出于所有其他目的，子资产在中的处理方式与正常资产相同 [!DNL Experience Manager]。

默认情况下，子资产生成处于禁用状态。 要启用子资产生成，请执行以下步骤：

1. 以管理 [!DNL Experience Manager] 员身份登录。 访问 **[!UICONTROL 工具]** >工 **[!UICONTROL 作流]** > **[!UICONTROL 模型]**。
1. 选择 **[!UICONTROL DAM更新资产工作流]** ，然后单击 **[!UICONTROL 编辑]**。
1. 单击 **[!UICONTROL 切换侧面板]** ，然后找到 **[!UICONTROL 创建子资产步骤]** 。 将步骤添加到工作流。 单击 **[!UICONTROL 同步]**。

要生成子资产，请执行以下操作之一：

* 新资产： DAM [!UICONTROL 更新资产工作流] ，对上传到的任何新资产执行 [!DNL Experience Manager]。 子资产是为新的多页资产自动生成的。
* 现有多页资产： 按照以下任 [!UICONTROL 一步骤手动执行] DAM更新资产工作流：

   * 选择一个资产，然 [!UICONTROL 后单击] “时间轴”以打开左侧面板。 或者，使用键盘快捷键 `alt + 3`。 单击 [!UICONTROL 开始工]作流，选 [!UICONTROL 择DAM更新资产]，单击 [!UICONTROL 开始]，然后 [!UICONTROL 单击继]续。
   * 选择资产，然后从工 [!UICONTROL 具栏中] ，单 [!UICONTROL 击创] 建>工作流。 从弹出对话框中，选 [!UICONTROL 择DAM更新资产工作] 流，单击 [!UICONTROL 开始]，然后 [!UICONTROL 单击继续]。

特别是对于Microsoft Word文档，请执 **[!UICONTROL 行DAM分析Word文档工作流]** 。 它从Microsoft `cq:Page` Word文档的内容生成一个组件。 从文档提取的图像从组件中引 `cq:Page` 用。 即使禁用了子资产生成，也会提取这些图像。

## View subassets {#viewing-subassets}

仅当生成子资产并且这些子资产可用于选定的多页资产时，才会显示子资产。 要视图生成的子资产，请打开多页资产。 在页面的左上角，单击选项以打 ![开左边栏](assets/do-not-localize/aem_leftrail_contentonly.png) ，然 **[!UICONTROL 后单击列表]** 中的子资产。 当您从列表 **[!UICONTROL 中选择]** “子资产”时。 或者，使用键盘快捷键 `alt + 5`。

![视图多页资产的子资产](assets/view_subassets_simulation.gif)

## 视图多页文件的页面 {#view-pages-of-a-multi-page-file}

您可以使用的页面查看器功能视图多页文件，如PDF、INDD、PPT、PPTX和AI文件 [!DNL Experience Manager Assets]。 打开多页资产，然后 **[!UICONTROL 单击页面]** 左上角的视图页面。 打开的页面查看器显示资产的页面以及用于浏览和缩放每个页面的控件。

![视图和查看多页资产的页面](assets/view_multipage_asset_fmr.gif)

对于 [!DNL InDesign]，您可以使用提取页 [!DNL InDesign Server]面。 如果在文件创建过程中保 [!DNL InDesign] 存了一预览页面， [!DNL InDesign Server] 则页面提取不需要。

工具栏、左边栏和页面查看器控件中提供以下选项：

* **[!UICONTROL 桌面操作]** ，使用桌面应用程序打开或显示特定 [!DNL Experience Manager] 子资产。 如果您使用桌 [面应用程序](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) ，请了解如何配置 [!DNL Experience Manager] 桌面操作。

* **[!UICONTROL 属性]** 选项会打开 [!UICONTROL 特定子资] 产的属性页面。

* **[!UICONTROL “注释]** ”选项允许您对特定子资产进行注释。 在打开父资产进行查看时，您在单独的子资产上使用的注释会一起收集和显示。

* **[!UICONTROL “页面概述]** ”选项同时显示所有子资产。

* **[!UICONTROL 单击]** “选项”打开左边栏后，左边 ![栏中的时间轴选项](assets/do-not-localize/aem_leftrail_contentonly.png) ，显示文件的活动流。

## 最佳实践和限制 {#best-practice-limitation-tips}

* 子资产生成会占用大量资源用于任何Experience Manager部署。 如果您是在上传复杂资产时生成子资产，请在DAM更新资产工作流中添加该步骤。 如果要按需生成子资产，请创建单独的工作流以生成子资产。 专用工作流允许您跳过DAM更新资产工作流中的其他步骤并保存计算资源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager桌面应用程序](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager中配置桌面操作](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop中创建链接的智能对象](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [将图形置入Adobe InDesign中](https://helpx.adobe.com/indesign/using/placing-graphics.html)

