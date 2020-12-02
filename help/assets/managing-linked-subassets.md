---
title: 使用引用和多个页面管理复合资产
description: 了解如何从 [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]中创建对数字资产的引用。 使用页面查看器功能可视图多页文件（如PDF、INDD、PPT、PPTX和AI文件）的各个子资产页面。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 0%

---


# 管理复合和多页资产{#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可以标识已上传的文件是否包含对存储库中已存在资产的引用。此功能仅适用于支持的文件格式。 如果上传的资产包含对[!DNL Experience Manager]资产的任何引用，则会在上传的资产和引用的资产之间创建双向链接。

除了消除冗余外，在[!DNL Adobe Creative Cloud]应用程序中引用资产还增强了协作，提高了用户的效率和工作效率。

[!DNL Experience Manager Assets] 支持双向引用。您可以在已上传文件的资产详细信息页面中查找引用的资产。 此外，您还可以视图引用资产的资产详细信息页面中的引用文件。

引用会根据引用资产的路径、文档ID和实例ID解析。

## 将数字资产作为[!DNL Adobe Illustrator] {#refai}中的引用添加

您可以从[!DNL Adobe Illustrator]文件中引用现有数字资产。

1. 使用[[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)在本地文件系统上提取数字资产。 导航到要引用的资产的文件系统位置。
1. 将资产从本地文件夹拖到[!DNL Illustrator]文件。

1. 将[!DNL Illustrator]文件保存到已装载的驱动器，或将[上载](/help/assets/manage-assets.md#uploading-assets)到[!DNL Experience Manager]存储库。

1. 工作流完成后，转到资产的资产详细信息页面。 对现有数字资产的引用列在&#x200B;**[!UICONTROL 引用]**&#x200B;列中的&#x200B;**[!UICONTROL 依赖项]**&#x200B;下。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 在&#x200B;**[!UICONTROL Dependencies]**&#x200B;下显示的引用资产也可由当前资产以外的文件引用。 要视图引用资产文件的列表，请单击&#x200B;**[!UICONTROL 依赖项]**&#x200B;下的资产。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 视图属性]**。 在[!UICONTROL 属性]页面中，引用当前资产的文件列表显示在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡的&#x200B;**[!UICONTROL 引用]**&#x200B;列下。

   ![视图资产详细信息中引用列中Experience Manager资产的引用](assets/asset-references.png)

   *图：资产详细信息中的资产引用。*

## 将数字资产作为[!DNL Adobe InDesign] {#add-aem-assets-as-references-in-adobe-indesign}中的引用添加

要从[!DNL InDesign]文件中引用数字资产，请将资产拖动到[!DNL InDesign]文件，或将[!DNL InDesign]文件导出为ZIP存档。

[!DNL Experience Manager Assets]中已存在引用的资产。 您可以通过[配置InDesign Server](indesign.md)提取子资产。 [!DNL InDesign]文件中的嵌入式资产会被提取为子资产。

>[!NOTE]
>
>如果[!DNL InDesign Server]是代理文件，[!DNL InDesign]文件的预览将嵌入到其XMP元数据中。 在这种情况下，缩略图提取不是明确必需的。 但是，如果[!DNL InDesign Server]未代理，则必须显式提取[!DNL InDesign]文件的缩略图。

### 通过拖动资产{#create-references-by-dragging-aem-assets}创建引用

此过程类似于在Adobe Illustrator](#refai)中添加数字资产作为引用。[

### 通过导出ZIP文件{#create-references-to-aem-assets-by-exporting-a-zip-file}创建对资产的引用

1. 执行[创建工作流模型](/help/sites-developing/workflows-models.md)中的步骤以创建新工作流。
1. 使用[!DNL Adobe InDesign]的“包”功能导出文档。 [!DNL Adobe InDesign] 可将文档和关联的资产作为包导出。在这种情况下，导出的文件夹包含一个Links文件夹，其中包含[!DNL InDesign]文件中的子资产。
1. 创建ZIP文件并将其上传到[!DNL Experience Manager]存储库。
1. 开始`Unarchiver`工作流。
1. 该工作流完成后，Links文件夹中的引用将自动作为子资产进行引用。 要视图引用的资产的列表，请导航到[!DNL InDesign]资产的资产详细信息页面，然后关闭[边栏](/help/sites-authoring/basic-handling.md#rail-selector)。

## 将数字资产作为[!DNL Adobe Photoshop] {#refps}中的引用添加

1. 使用[!DNL Experience Manager]桌面应用程序访问[!DNL Experience Manager Assets]。 下载并显示本地文件系统上的资源。 在[!DNL Adobe Photoshop]中使用[!UICONTROL 放置链接的]功能。 请参阅[将资源放入桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. 保存在[!DNL Photoshop]文件中到装载的驱动器或[上载](/help/assets/manage-assets.md#uploading-assets)到[!DNL Experience Manager]存储库。
1. 工作流完成后，对现有[!DNL Experience Manager]资产的引用会列在资产详细信息页面中。

   要视图引用的资产，请关闭资产详细信息页面中的[边栏](/help/sites-authoring/basic-handling.md#rail-selector)。

1. 引用的资产还包含引用这些资产的资产的列表。要视图引用的资产的列表，请导航到资产详细信息页面，然后关闭[边栏](/help/sites-authoring/basic-handling.md#rail-selector)。

>[!NOTE]
>
>复合资产中的资产也可以根据其文档ID和实例ID进行引用。 此功能仅在[!DNL Adobe Illustrator]和[!DNL Adobe Photoshop]版本中可用。 对于其他资产，引用的基础是主复合资产中链接资产的相对路径，与在[!DNL Experience Manager]的早期版本中一样。

## 创建子资产{#generate-subassets}

对于多页格式的受支持资产— PDF文件、AI文件、[!DNL Microsoft PowerPoint]和[!DNL Apple Keynote]文件以及[!DNL Adobe InDesign]文件— [!DNL Experience Manager]可以生成与原始资产的每个单独页面对应的子资产。 这些子资产链接到&#x200B;*父资产*，便于多页视图。 出于所有其他目的，子资产在[!DNL Experience Manager]中的处理方式与普通资产相同。

默认情况下，子资产生成处于禁用状态。 要启用子资产生成，请执行以下步骤：

1. 以管理员身份登录到[!DNL Experience Manager]。 访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 选择&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流，然后单击&#x200B;**[!UICONTROL 编辑]**。
1. 单击&#x200B;**[!UICONTROL 切换侧面板]**&#x200B;并找到&#x200B;**[!UICONTROL 创建子资产]**&#x200B;步骤。 将步骤添加到工作流。 单击&#x200B;**[!UICONTROL 同步]**。

要生成子资产，请执行以下操作之一：

* 新资产：[!UICONTROL DAM更新资产]工作流对上传到[!DNL Experience Manager]的任何新资产执行。 子资产是为新的多页资产自动生成的。
* 现有多页资产：按照以下任一步骤手动执行[!UICONTROL DAM更新资产]工作流：

   * 选择资产，然后单击[!UICONTROL 时间轴]以打开左面板。 或者，使用键盘快捷键`alt + 3`。 单击[!UICONTROL 开始工作流]，选择[!UICONTROL DAM更新资产]，单击[!UICONTROL 开始]，然后单击[!UICONTROL 继续]。
   * 选择资产，然后单击工具栏中的[!UICONTROL 创建] > [!UICONTROL 工作流]。 从弹出对话框中，选择[!UICONTROL DAM更新资产]工作流，单击[!UICONTROL 开始]，然后单击[!UICONTROL 继续]。

特别是对于Microsoft Word文档，执行&#x200B;**[!UICONTROL DAM分析Word文档]**&#x200B;工作流。 它从Microsoft Word文档的内容生成`cq:Page`组件。 从文档提取的图像引用自`cq:Page`组件。 即使禁用了子资产生成，也会提取这些图像。

## 视图子资产{#viewing-subassets}

仅当生成子资产并且这些子资产可用于选定的多页资产时，才会显示子资产。 要视图生成的子资产，请打开多页资产。 在页面的左上角，单击![选项以打开左边栏](assets/do-not-localize/aem_leftrail_contentonly.png)，然后单击列表中的&#x200B;**[!UICONTROL 子资产]**。 从列表中选择&#x200B;**[!UICONTROL 子资产]**&#x200B;时。 或者，使用键盘快捷键`alt + 5`。

![视图多页资产的子资产](assets/view_subassets_simulation.gif)

## 视图多页文件{#view-pages-of-a-multi-page-file}的页面

可以使用[!DNL Experience Manager Assets]的页面查看器功能视图多页文件，如PDF、INDD、PPT、PPTX和AI文件。 打开多页资产，然后单击页面左上角的&#x200B;**[!UICONTROL 视图页面]**。 打开的页面查看器显示资产的页面以及用于浏览和缩放每个页面的控件。

![视图和查看多页资产的页面](assets/view_multipage_asset_fmr.gif)

对于[!DNL InDesign]，可使用[!DNL InDesign Server]提取页面。 如果在[!DNL InDesign]文件创建过程中保存了一预览页面，则页面提取不需要[!DNL InDesign Server]。

工具栏、左边栏和页面查看器控件中提供以下选项：

* **[!UICONTROL 桌面]** 操作，以使用桌面应用程序打开或显示特 [!DNL Experience Manager] 定子资产。如果您使用[!DNL Experience Manager]桌面应用程序，请参阅如何[配置桌面操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)。

* **[!UICONTROL “属]** 性”选项会打  开特定子资产的“属性”页。

* **[!UICONTROL “注]** 释”选项允许您对特定子资产进行注释。在打开父资产进行查看时，您在单独的子资产上使用的注释会一起收集和显示。

* **[!UICONTROL 页面]** 概述选项可同时显示所有子资产。

* **[!UICONTROL 单]** 击“选项”打开左栏后，左边栏 ![中的时间](assets/do-not-localize/aem_leftrail_contentonly.png) 线选项会显示文件的活动流。

## 最佳实践和限制{#best-practice-limitation-tips}

* 子资产生成可能会占用任何[!DNL Experience Manager]部署的大量资源。 如果您是在上传复杂资产时生成子资产，请在DAM更新资产工作流中添加该步骤。 如果要按需生成子资产，请创建单独的工作流以生成子资产。 专用工作流允许您跳过DAM更新资产工作流中的其他步骤并保存计算资源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager配置桌面操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop创建链接的智能对象](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [将图形置入Adobe InDesign](https://helpx.adobe.com/indesign/using/placing-graphics.html)

