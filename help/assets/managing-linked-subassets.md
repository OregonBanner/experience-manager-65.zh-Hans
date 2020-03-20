---
title: 在Experience Manager中使用引用和多页资产管理复合资产
description: 了解如何从InDesign、Illustrator和Photoshop中创建对AEM资产的引用。 使用页面查看器功能可查看多页文件（如PDF、INDD、PPT、PPTX和AI文件）的各个子资产页面。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# 管理复合和多页资产 {#managing-compound-assets}

Adobe Experience Manager(AEM)资产可以识别上传的文件是否包含对存储库中已存在资产的引用。 此功能仅对支持的文件格式可用。 如果已上传的资产包含对AEM资产的任何引用，则会在已上传和引用的资产之间创建双向链接。

除了消除冗余外，在Adobe Creative Cloud应用程序中引用AEM资产还可增强协作，并提高用户的效率和工作效率。

AEM资产支持双向引用。 您可以在已上传文件的资产详细信息页面中查找引用的资产。 此外，您还可以在被引用资产的资产详细信息页面中查看AEM资产的引用文件。

引用会根据引用资产的路径、文档ID和实例ID进行解析。

## Add AEM Assets as references in Adobe Illustrator {#refai}

您可以从 Adobe Illustrator 文件中引用现有的 AEM 资产。

1. 使用 [AEM桌面应用程序](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)，将AEM资产存储库作为驱动器装载到本地计算机。 在已装载的驱动器中，导航到要引用的资产所在的位置。
1. 将资产从安装的驱动器拖到 Illustrator 文件。

1. Save the Illustrator file to the mounted drive, or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the AEM repository.

1. 工作流完成后，转到资产的资产详细信息页面。 对现有AEM资产的引用列在“引用”列 **[!UICONTROL 的]** “依赖项 **[!UICONTROL ”下]** 。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 在“依赖关系”下显示的 **[!UICONTROL 引用资产]** ，也可以由当前文件以外的文件引用。 要查看资产的引用文件列表，请单击依赖项下的资产 **[!UICONTROL 列表]**。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 单击 **[!UICONTROL 工具栏中的]** “查看属性”。 在“属 [!UICONTROL 性] ”页中，引用当前资产的文件列表显示在“基本”选项卡的“ **[!UICONTROL 引用]****[!UICONTROL ”列]** 下方。

   ![在资产详细信息的“引用”列中查看Experience Manager资产的引用](assets/asset-references.png)

   *图：资产详细信息中的资产引用*

## Add AEM assets as references in Adobe InDesign {#add-aem-assets-as-references-in-adobe-indesign}

要从InDesign文件中引用AEM资产，请将AEM资产拖动到InDesign文件，或将InDesign文件导出为ZIP文件。

AEM资产中已存在引用的资产。 您可以通过配置InDesign服 [务器提取子资产](/help/assets/indesign.md)。 InDesign文件中的嵌入资源会作为子资产进行提取。

>[!NOTE]
>
>如果InDesign服务器是代理的，则InDesign文件的预览将嵌入到其XMP元数据中。 在这种情况下，不显式需要提取缩略图。 但是，如果InDesign服务器未代理，则必须显式提取InDesign文件的缩略图。

### 通过拖动资产创建引用 {#create-references-by-dragging-aem-assets}

This procedure is similar to [Add AEM assets as references in Adobe Illustrator](#refai).

### Create references to assets by exporting a ZIP file {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Perform the steps in [Create workflow models](/help/sites-developing/workflows-models.md) to create a new workflow.
1. 使用 Adobe InDesign 的打包功能导出文档。
Adobe InDesign 可将文档和关联的资产作为包导出。在这种情况下，导出的文件夹包含“Links”文件夹，其中含有 InDesign 文件中的子资产。
1. 创建 ZIP 文件并将其上传到 AEM 存储库。
1. Start the `Unarchiver` workflow.
1. When the workflow completes, the references in the Links folder are automatically referenced as subassets. To view a list of referred assets, navigate to the asset details page of the InDesign asset and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## Add AEM assets as references in Adobe Photoshop {#refps}

1. 使用WebDav客户端，将AEM资产作为驱动器装载。
1. 要在 Photoshop 文件中创建 AEM 资产引用，请使用 Photoshop 中的“放置链接”功能，导航到已安装驱动器中的相应资产。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Save in Photoshop file to the mounted drive or or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the AEM repository.
1. 工作流完成后，对现有AEM资产的引用会列在资产详细信息页面中。

   To view the referenced assets, close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector) in the asset details page.

1. The referenced assets also contain the list of assets they are referenced from. To view a list of referenced assets, navigate to the asset details page and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>复合资产中的资产也可以根据文档ID和实例ID进行引用。 此功能仅在Adobe Illustrator和Adobe Photoshop版本中可用。 对于其他资产，则根据主复合资产中链接资产的相对路径进行引用，这与在AEM的早期版本中一样。

## 创建子资产 {#generate-subassets}

对于支持的多页格式资产— PDF文件、AI文件、Microsoft PowerPoint和Apple Keynote文件以及Adobe InDesign文件— AEM可以生成与原始资产的每个单独页面对应的子资产。 这些子资产链接到父 *资产* ，便于多页查看。 出于所有其他目的，子资产在AEM中的处理方式与普通资产相同。

默认情况下，子资产生成处于禁用状态。 要启用子资产生成，请执行以下步骤：

1. 以管理员身份登录到Experience Manager。 访问 **[!UICONTROL 工具>工作流>模型]**。
1. 选择 **[!UICONTROL DAM更新资产工作流]** ，然后单击 **[!UICONTROL 编辑]**。
1. 单击 **[!UICONTROL 切换侧面板]** ，然后找到创 **[!UICONTROL 建子资产步骤]** 。 将步骤添加到工作流。 单击 **[!UICONTROL 同步]**。

要生成子资产，请执行以下操作之一：

* 新资产：DAM更  新资产工作流对上传到AEM的任何新资产执行。 子资产是为新的多页资产自动生成的。
* 现有多页资产：按照以下任一步 [!UICONTROL 骤手动执行DAM更新资产] :

   * 选择一个资产，然后单击 [!UICONTROL 时间轴] ，以打开左侧面板。 或者，使用键盘快捷键 `alt + 3`。 单击 [!UICONTROL 启动工作流]，选择 [!UICONTROL DAM更新资产]，单击 [!UICONTROL 启动]，然后 单击继续。
   * 选择一个资产，然后从工 [!UICONTROL 具栏中单击创建] >工作流。 从弹出对话框中，选择 [!UICONTROL DAM更新资产工作流] ，单击 [!UICONTROL 开始]，然后单击继 [!UICONTROL 续]。

尤其是对于Microsoft Word文档，请执行 **[!UICONTROL DAM分析Word文档工作流]** 。 它从Microsoft `cq:Page` Word文档的内容生成组件。 从文档提取的图像从组件中引 `cq:Page` 用。 即使禁用了子资产生成功能，也会提取这些图像。

## View subassets {#viewing-subassets}

仅当生成子资产并且这些子资产可用于选定的多页资产时，才会显示子资产。 要查看生成的子资产，请打开多页资产。 在页面的左上角区域，单击左边栏图 ![标](assets/do-not-localize/aem_leftrail_contentonly.png) ，然后单 **[!UICONTROL 击列表中的子资产]** 。 当您从列表 **[!UICONTROL 中选择]** “子资产”时。 或者，使用键盘快捷键 `alt + 5`。

![查看多页资产的子资产](assets/view_subassets_simulation.gif)

## 查看多页文件的页面 {#view-pages-of-a-multi-page-file}

您可以使用AEM资产的页面查看器功能查看多页文件，如PDF、INDD、PPT、PPTX和AI文件。 打开多页资产，然后单 **[!UICONTROL 击页面左上角]** 的查看页面。 打开的页面查看器显示资产的页面以及用于浏览和缩放每个页面的控件。

![查看和查看多页资产的页面](assets/view_multipage_asset_fmr.gif)

对于InDesign，可以使用InDesign服务器提取页面。 如果在InDesign文件创建过程中保存了页面预览，则页面提取不需要InDesign Server。

工具栏、左边栏和页面查看器控件中提供以下选项：

* **[!UICONTROL 桌面操作]** ，以使用AEM桌面应用程序打开或显示特定子资产。 如果您使用 [AEM桌面应用程序](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) ，请参阅如何配置桌面操作。

* **[!UICONTROL “属性]** ”选项会打开特 [!UICONTROL 定子资产的] “属性”页面。

* **[!UICONTROL “注释]** ”选项允许您对特定子资产进行注释。 在打开父资产进行查看时，您在单独的子资产上使用的注释会一起收集并显示。

* **[!UICONTROL “页面概述]** ”选项同时显示所有子资产。

* **[!UICONTROL 单击]** “左边栏”图标后，左边栏中 ![的时间轴选项](assets/do-not-localize/aem_leftrail_contentonly.png) ，显示文件的活动流。
