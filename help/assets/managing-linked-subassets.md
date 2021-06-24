---
title: 使用引用和多个页面管理复合资产
description: 了解如何从 [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]中创建对数字资产的引用。 使用页面查看器功能可查看多页文件（如PDF、INDD、PPT、PPTX和AI文件）的单个子资产页面。
contentOwner: AG
role: Business Practitioner, Administrator
feature: 资产管理
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: a564f158cf1040ef43cb9f5dde9f7cb22769587f
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# 管理复合资产和多页资产 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] 可以识别上传的文件是否包含对存储库中已存在资产的引用。此功能仅适用于支持的文件格式。 如果上传的资产包含对[!DNL Experience Manager]资产的任何引用，则会在上传的资产和引用的资产之间创建双向链接。

除了消除冗余外，在[!DNL Adobe Creative Cloud]应用程序中引用资产还可以增强协作，并提高用户的效率和工作效率。

[!DNL Experience Manager Assets] 支持双向引用。您可以在上传文件的资产详细信息页面中找到引用的资产。 此外，您还可以在引用资产的资产详细信息页面中查看引用文件。

引用会根据引用资产的路径、文档ID和实例ID进行解析。

## [!DNL Adobe Illustrator]:将数字资产添加为参考 {#refai}

您可以从[!DNL Adobe Illustrator]文件中引用现有数字资产。

1. 使用[[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)获取本地文件系统上的数字资产。 导航到要引用的资产的文件系统位置。
1. 将资产从本地文件夹拖到[!DNL Illustrator]文件。

1. 将[!DNL Illustrator]文件保存到已装载的驱动器，或将[上载](/help/assets/manage-assets.md#uploading-assets)到[!DNL Experience Manager]存储库。

1. 工作流完成后，转到资产的资产详细信息页面。 对现有数字资产的引用列在&#x200B;**[!UICONTROL 引用]**&#x200B;列的&#x200B;**[!UICONTROL 依赖项]**&#x200B;下。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 在&#x200B;**[!UICONTROL Dependencies]**&#x200B;下显示的引用资产也可由当前资产以外的文件引用。 要查看资产引用文件的列表，请单击&#x200B;**[!UICONTROL 依赖项]**&#x200B;下的资产。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 查看属性]** 。 在[!UICONTROL 属性]页面中，引用当前资产的文件列表显示在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡的&#x200B;**[!UICONTROL 引用]**&#x200B;列下。

   ![在资产详细信息的“引用”列中查看Experience Manager资产的引用](assets/asset-references.png)

   *图：资产详细信息中的资产引用。*

## [!DNL Adobe InDesign]:将数字资产添加为参考 {#add-aem-assets-as-references-in-adobe-indesign}

要从[!DNL InDesign]文件中引用数字资产，请将资产拖到[!DNL InDesign]文件中，或将[!DNL InDesign]文件导出为ZIP存档。

[!DNL Experience Manager Assets]中已存在引用的资产。 您可以通过[配置InDesign Server](indesign.md)来提取子资产。 [!DNL InDesign]文件中的嵌入式资产将作为子资产进行提取。

>[!NOTE]
>
>如果代理[!DNL InDesign Server]，则[!DNL InDesign]文件的预览会嵌入到其XMP元数据中。 在这种情况下，并非明确需要缩略图提取。 但是，如果[!DNL InDesign Server]未代理，则必须为[!DNL InDesign]文件显式提取缩略图。

上传INDD文件后，将通过查询存储库中具有`xmpMM:InstanceID`和`xmpMM:DocumentID`属性的资产来获取引用。

### 通过拖动资产创建引用 {#create-references-by-dragging-aem-assets}

此过程与[在Adobe Illustrator](#refai)中添加数字资产作为引用类似。

### 通过导出ZIP文件创建对资产的引用 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. 执行[创建工作流模型](/help/sites-developing/workflows-models.md)中的步骤，以创建新工作流。
1. 使用[!DNL Adobe InDesign]的[包功能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html)导出文档。 [!DNL Adobe InDesign] 可将文档和关联的资产作为包导出。在这种情况下，导出的文件夹包含一个`Links`文件夹，其中包含[!DNL InDesign]文件中的子资产。 `Links`文件夹与INDD文件位于同一文件夹中。
1. 创建ZIP文件并将其上传到[!DNL Experience Manager]存储库。
1. 启动`Unarchiver`工作流。
1. 工作流完成后，Links文件夹中的引用会自动作为子资产进行引用。 要查看引用的资产列表，请导航到[!DNL InDesign]资产的资产详细信息页面，并关闭[边栏](/help/sites-authoring/basic-handling.md#rail-selector)。

## [!DNL Adobe Photoshop]:将数字资产添加为参考 {#refps}

1. 使用[!DNL Experience Manager]桌面应用程序访问[!DNL Experience Manager Assets]。 下载并显示本地文件系统上的资产。 在[!DNL Adobe Photoshop]中使用[!UICONTROL Linked]功能。 请参阅[将资产放入桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)中。

1. 将[!DNL Photoshop]文件保存到已装载的驱动器，或将](/help/assets/manage-assets.md#uploading-assets)上载到[!DNL Experience Manager]存储库。[
1. 工作流完成后，对现有[!DNL Experience Manager]资产的引用将列在资产详细信息页面中。

   要查看引用的资产，请关闭资产详细信息页面中的[边栏](/help/sites-authoring/basic-handling.md#rail-selector)。

1. 引用的资产还包含引用这些资产的资产列表。要查看引用的资产列表，请导航到资产详细信息页面并关闭[边栏](/help/sites-authoring/basic-handling.md#rail-selector)。

>[!NOTE]
>
>复合资产中的资产还可以根据其文档ID和实例ID进行引用。 此功能仅在[!DNL Adobe Illustrator]和[!DNL Adobe Photoshop]版本中可用。 对于其他资产，则会按照[!DNL Experience Manager]早期版本中所述，基于主复合资产中链接资产的相对路径进行引用。

## 创建子资产 {#generate-subassets}

对于支持的多页格式资产（PDF文件、AI文件、[!DNL Microsoft PowerPoint]和[!DNL Apple Keynote]文件，以及[!DNL Adobe InDesign]文件） — [!DNL Experience Manager]可以生成与原始资产的每个单独页面对应的子资产。 这些子资产与&#x200B;*父*&#x200B;资产相关联，有助于进行多页面查看。 出于所有其他目的，子资产会像[!DNL Experience Manager]中的普通资产一样处理。

默认情况下，子资产生成处于禁用状态。 要启用子资产生成，请执行以下步骤：

1. 以管理员身份登录[!DNL Experience Manager]。 访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 选择&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流，然后单击&#x200B;**[!UICONTROL 编辑]**。
1. 单击&#x200B;**[!UICONTROL 切换侧面板]**&#x200B;并找到&#x200B;**[!UICONTROL 创建子资产]**&#x200B;步骤。 将步骤添加到工作流。 单击&#x200B;**[!UICONTROL 同步]**。

要生成子资产，请执行以下操作之一：

* 新资产：[!UICONTROL  DAM更新资产]工作流会对上传到[!DNL Experience Manager]的任何新资产执行。 子资产会为新的多页面资产自动生成。
* 现有的多页资产：按照以下任一步骤手动执行[!UICONTROL  DAM更新资产]工作流：

   * 选择资产并单击[!UICONTROL 时间轴]以打开左侧面板。 或者，使用键盘快捷键`alt + 3`。 单击[!UICONTROL 启动工作流]，选择[!UICONTROL DAM更新资产]，单击[!UICONTROL 启动]，然后单击[!UICONTROL 继续]。
   * 选择资产，然后单击工具栏中的[!UICONTROL 创建] > [!UICONTROL 工作流]。 在弹出对话框中，选择[!UICONTROL DAM更新资产]工作流，单击[!UICONTROL 启动]，然后单击[!UICONTROL 继续]。

特别是对于Microsoft Word文档，请执行&#x200B;**[!UICONTROL DAM解析Word文档]**&#x200B;工作流。 它从Microsoft Word文档的内容生成`cq:Page`组件。 从文档提取的图像将从`cq:Page`组件中引用。 即使禁用子资产生成，也会提取这些图像。

## 查看子资产 {#viewing-subassets}

只有在生成子资产并且该子资产可用于选定的多页面资产时，才会显示子资产。 要查看生成的子资产，请打开多页面资产。 在页面的左上角，单击![选项以打开左边栏](assets/do-not-localize/aem_leftrail_contentonly.png)，然后单击列表中的&#x200B;**[!UICONTROL Subassets]**。 从列表中选择&#x200B;**[!UICONTROL 子资产]**&#x200B;时。 或者，使用键盘快捷键`alt + 5`。

![查看多页面资产的子资产](assets/view_subassets_simulation.gif)

## 查看多页文件的页面 {#view-pages-of-a-multi-page-file}

使用[!DNL Experience Manager Assets]的页面查看器功能，可以查看多页文件，如PDF、INDD、PPT、PPTX和AI文件。 打开多页资产，然后单击页面左上角的&#x200B;**[!UICONTROL 查看页面]** 。 打开的页面查看器会显示资产的页面以及用于浏览和缩放每个页面的控件。

![查看和查看多页面资产的页面](assets/view_multipage_asset_fmr.gif)

对于[!DNL InDesign]，可以使用[!DNL InDesign Server]提取页面。 如果在[!DNL InDesign]文件创建期间保存了页面的预览，则页面提取不需要[!DNL InDesign Server]。

以下选项在工具栏、左边栏和“页面查看器”控件中可用：

* **[!UICONTROL 桌面]** 操作来使用桌面应用程序打开或显示特定 [!DNL Experience Manager] 的子资产。如果您使用的是[!DNL Experience Manager]桌面应用程序，请参阅如何[配置桌面操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)。

* **** 属性选项会打开  特定子资产的属性页面。

* **** 注释选项允许您对特定子资产添加注释。打开父资产进行查看时，系统会收集并显示您在单独的子资产上使用的注释。

* **[!UICONTROL 页面]** 概述选项同时显示所有子资产。

* **** 单击选项以打开左边栏后，左边栏中 ![的时间](assets/do-not-localize/aem_leftrail_contentonly.png) 线选项会显示文件的活动流。

## 最佳实践和限制 {#best-practice-limitation-tips}

* 任何[!DNL Experience Manager]部署中的子资源生成都会占用大量资源。 如果您在上传复杂资产时生成子资产，请在DAM更新资产工作流中添加该步骤。 如果要按需生成子资产，请创建单独的工作流以生成子资产。 利用专用工作流，可跳过DAM更新资产工作流中的其他步骤并保存计算资源。

>[!MORELIKETHIS]
>
>* [使用Adobe Experience Manager桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [在Adobe Experience Manager中配置桌面操作](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [在Adobe Photoshop中创建链接的智能对象](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [在Adobe InDesign中放置图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)

