---
title: 图像集
description: 了解如何在Dynamic Media中使用图像集
uuid: ca2fd5b0-656e-4960-b10c-f0ec3d418760
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ccc4eb23-934c-4e67-860b-a6faa2bcaafc
docset: aem65
feature: Image Sets,Asset Management
role: User, Admin
exl-id: 2a536745-fa13-4158-8761-2ac5b6e1893e
source-git-commit: d83a647d8ac5466ba09230c584d5d501aab55274
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 27%

---

# 图像集 {#image-sets}

图像集为用户提供了集成的查看体验，用户可以通过选择缩略图图像来查看项目的不同视图。 图像集使您可以展示同一项目的替换视图，并且查看器提供了可用于仔细检查图像的缩放工具。

图像集由带有单词的横幅指定 `IMAGESET`. 此外，如果图像集已发布，则横幅上会显示由 **[!UICONTROL World]** 图标指示的发布日期以及由铅笔图标指示的上次修改日期 **** 。

![图像集](assets/chlimage_1-339.png)

在图像集中，您还可以通过创建图像集并添加缩略图来创建色板。

当您想要以不同的颜色、图案或成品显示项目时，此应用程序非常有用。 要创建包含颜色样本的图像集，您需要为要呈现给用户的每种颜色、图案或完成程度都创建一个图像。 每种颜色、模式或外表还需要有一个颜色、模式或外表样本。

例如，假定您要展示帽檐颜色各异的帽子图像，且帽檐分别为红色、绿色和蓝色。在这种情况下，您需要准备同一款帽子的三张拍照。这三张拍照分别对应红色、绿色和蓝色的帽檐。您还需要准备红色、绿色和蓝色三种颜色的样本。颜色样本用作用户在样本集查看器中选择的缩略图，以查看红色计费、绿色计费或蓝色计费的次数上限。

>[!NOTE]
>
>有关Assets用户界面的信息，请参阅 [管理资源](/help/assets/manage-assets.md).

创建图像集时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| 每集的重复资产数 | 无重复项 | 20 |
| 每组图像的最大数量 | 每组5-10个图像 | 1000 |

另请参阅 [Dynamic Media限制](/help/assets/limitations.md).

## 快速入门：图像集 {#quick-start-image-sets}

**要快速设置并运行图像集，请执行以下操作：**

1. [上传主源图像以供多个视图使用](#uploading-assets-in-image-sets).

   首先为图像集上传图像。当您选择图像时，请记住，您的客户可以在图像集查看器中放大图像。 确保图像的最大尺寸至少为2000像素，以获得最佳的缩放细节。 Dynamic Media可以渲染每个高达2500万像素(MB)的图像。 例如，您可以使用5000 x 5000 MP图像或任何其他大小组合，最大可达25 MP。

   参见 [Dynamic Media — 支持的栅格图像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 有关图像集支持的格式的列表。

<!--    Adobe Experience Manager Assets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

1. [创建图像集](#creating-image-sets).

   在图像集中，用户在图像集查看器中选择缩略图图像。

   要在资产中创建图像集，请转到 **[!UICONTROL 创建]** > **[!UICONTROL 图像集]**. 然后，添加图像并选择 **[!UICONTROL 保存]**.

   您还可以通过自动创建图像集 [批次集预设](/help/assets/config-dms7.md).
   >[!IMPORTANT]
   >
   >批量集由IPS(Image Production System)作为资产引入的一部分创建，并且仅在Dynamic Media - Scene7模式下可用。

   参见 [准备图像集资产以上传和上传文件](#uploading-assets-in-image-sets).

   参见 [使用选择器](/help/assets/working-with-selectors.md).

1. 添加 [图像集查看器预设](/help/assets/managing-viewer-presets.md)（根据需要）。

   管理员可以创建或修改图像集查看器预设。要查看带有查看器预设的图像集，请选择图像集，然后在左边栏下拉菜单中，选择 **[!UICONTROL 查看器]**.

   导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]** 创建或编辑查看器预设。

1. （可选） [查看图像集](/help/assets/image-sets.md#viewing-image-sets) 使用批次集预设创建的。
1. [预览图像集](/help/assets/previewing-assets.md).

   选择图像集后，您便可以预览该图像集。选择缩略图图标，以便在选定的查看器中检查图像集。 您可以从中选择不同的查看器 **[!UICONTROL 查看器]** 菜单，可从左边栏下拉菜单中访问。

1. [发布图像集](/help/assets/publishing-dynamicmedia-assets.md).

   发布图像集将激活URL和嵌入代码。 此外，您必须 [发布任何自定义查看器预设](/help/assets/managing-viewer-presets.md) 您已创建的内容。 现成的查看器预设已发布。

1. [将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)或者[嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

   Experience Manager Assets为图像集创建URL调用，并在您发布图像集后激活它们。 预览资产时，您可以复制这些 URL。或者，您也可以将它们嵌入到网站中。

   选择图像集，然后在左边栏下拉菜单中选择&#x200B;**[!UICONTROL 查看器]**。

   参见 [将图像集链接到网页](/help/assets/linking-urls-to-yourwebapplication.md) 和 [嵌入视频查看器或图像查看器](/help/assets/embed-code.md).

要编辑图像集，请参阅 [编辑图像集](#editing-image-sets). 此外，您还可以查看和编辑 [图像集属性](/help/assets/manage-assets.md#editing-properties).

如果在创建集时遇到问题，请参阅以下文档中的图像和集： [Dynamic Media故障诊断 — Scene7模式](/help/assets/troubleshoot-dms7.md#images-and-sets).

## 上传图像集中的资产 {#uploading-assets-in-image-sets}

首先为图像集上传图像。当您选择图像时，请记住，您的客户可以在图像集查看器中放大图像。 确保图像的最大尺寸至少为2000像素。图像集支持很多种图像文件格式，但建议使用无损的 TIFF、PNG 和 EPS 图像。

为图像集上传图像的方法与[在资产中上传任何其他资产](/help/assets/manage-assets.md#uploading-assets)的方法相同。

参见 [Dynamic Media — 支持的栅格图像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 有关图像集支持的格式的列表。

### 准备图像集资源以供上传 {#preparing-image-set-assets-for-upload}

在创建图像集之前，请确保图像的大小和格式均合适。

要创建多视图的图像集，您需要多个图像，它们要从不同视角显示一个项目或显示同一项目的不同方面。其目标是突出一个项目的各项重要功能，以便查看者能够全面地了解该项目的外观或用途。

由于用户可以缩放图像集中的图像，请确保图像的最大尺寸至少有 2000 像素。<!-- Assets support many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

>[!NOTE]
>
>此外，如果使用缩略图指示产品样本，则必须执行以下操作：
>
>您需要小插图，也就是同一图像的不同拍照，以显示该图像的不同颜色、模式或外表。您还需要与不同颜色、模式或外表相对应的缩略图文件。例如，要通过显示同一款夹克的黑色、咖色和绿色版的图像集展示缩略图，您需要：
>
>* 同一款夹克的黑色、咖色和绿色版拍照。
>* 黑色、咖色和绿色版的缩略图。


## 创建图像集 {#creating-image-sets}

您可以通过用户界面或 API 创建图像集。本节将会介绍如何在用户界面中创建图像集。

>[!NOTE]
>
>您还可以通过自动创建图像集 [批次集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
>**重要提示：** 批量集由IPS(Image Production System)作为资产引入的一部分创建，并且仅在Dynamic Media - Scene7模式下可用。

在将资源添加到集时，会自动按字母数字顺序添加资源。 添加资源后，您可以手动对资源重新排序或排序。

>[!NOTE]
>
>文件名中带有“，”（逗号）的资源不支持图像集。

创建图像集时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| 每集的重复资产数 | 无重复项 | 20 |
| 每组图像的最大数量 | 每组5-10个图像 | 1000 |

另请参阅 [Dynamic Media限制](/help/assets/limitations.md).

**要创建图像集，请执行以下操作：**

1. 在Experience Manager中，选择Experience Manager徽标以访问全局导航控制台，然后转到 **[!UICONTROL 导航]** > **[!UICONTROL 资产]**. 导航到要创建图像集的位置，然后转到 **[!UICONTROL 创建]** > **[!UICONTROL 图像集]** 以打开“图像集编辑器”页面。

   您还可以从包含资产的文件夹中创建旋转集。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 在“图像集编辑器”页面的 **[!UICONTROL 标题]** 字段中，输入图像集的名称。 该名称会显示在图像集的横幅中。（可选）输入说明。

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. 执行以下操作之一：

   * 在“图像集编辑器”页面的左上角附近，选择 **[!UICONTROL 添加资产]**.

   * 在“图像集编辑器”页面中间附近，选择 **[!UICONTROL 点按以打开资产选择器]**.
   选择要包含在图像集中的资源。 选定资产上有一个复选标记图标。完成后，在页面的右上角附近，选择 **[!UICONTROL 选择]**.

   借助资产选择器，您可以通过键入关键字并点按或单击&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后选择 **[!UICONTROL 筛选条件]** 图标。 点按“视图”图标并选择&#x200B;**[!UICONTROL 列视图]**、**[!UICONTROL 卡片视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;可更改视图。

   参见 [使用选择器](/help/assets/working-with-selectors.md).

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 在将资源添加到集时，会自动按字母数字顺序添加资源。 添加资源后，您可以手动对资源重新排序或排序。

   如有必要，请将资源的“重新排序”图标拖动到资源文件名的右侧，以将图像在集列表中向上或向下重新排序。

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   如果要更改缩略图或色板，请选择 **+** **缩略图** 图标，然后导航到所需的缩略图或色板。 选择完所有图像后，选择 **[!UICONTROL 保存]**.

1. （可选）执行以下操作之一：

   * 要删除图像，请选择该图像并选择 **[!UICONTROL 删除资源]**.

   * 要应用预设，请在页面的右上角附近，选择 **[!UICONTROL 预设]**，然后选择要一次性应用于所有资产的预设。
   >[!NOTE]
   >
   >创建图像集时，您可以更改图像集缩略图，或允许Experience Manager根据图像集中的资源自动选择缩略图。 要选择缩略图，请选择 **[!UICONTROL 更改缩略图]** 在“图像集编辑器”页面上的“标题”字段上方，选择任意图像（您也可以导航到其他文件夹以查找图像）。 如果您选择了缩略图，然后决定让Experience Manager从图像集生成缩略图，请选择 **[!UICONTROL 切换到]** > **[!UICONTROL 自动缩略图]**.

1. 选择&#x200B;**[!UICONTROL 保存]**。您新创建的图像集会显示在创建时所用的文件夹中。

## 查看图像集 {#viewing-image-sets}

您可以在用户界面中创建图像集，也可以使用 [批次集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).

>[!IMPORTANT]
>
>批次集由IPS创建 [图像制作系统] 作为资源提取的一部分，并且仅在Dynamic Media - Scene7模式下可用。)

但是，使用批次集预设创建的集可以 *非* 显示在用户界面中。 您可以通过三种不同的方式查看这些集合。 （即使在用户界面中创建了图像集，这些方法也可用）。

* 打开单个资产的属性。 属性指明所选资产被引用或作为成员的设置。 如果要查看整个集，请选择集的名称。

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties2.png)

* 来自任何集的成员图像。选择 **[!UICONTROL 集]** 菜单以显示资产所属的集。

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 在搜索中，您可以选择 **[!UICONTROL 筛选条件]**，然后展开 **[!UICONTROL Dynamic Media]** 并选择 **[!UICONTROL 集]**.

   搜索会返回在UI中手动创建或通过批次集预设自动创建的匹配集。 对于自动集，搜索查询使用“开头为”搜索条件执行，这与基于使用“包含”搜索条件的Experience Manager搜索不同。 将筛选条件设置为 **[!UICONTROL 集]** 这是搜索自动化集的唯一方法。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以通过用户界面查看集，如中所述 [编辑图像集](#editing-image-sets).

## 编辑图像集 {#editing-image-sets}

您可以对图像集执行各种编辑任务，如下所示：

* 向图像集中添加图像。
* 对图像集中的图像重新排序。
* 删除图像集中的资源。
* 应用查看器预设。
* 删除图像集。

**要编辑图像集，请执行以下操作：**

1. 执行以下任一操作：

   * 将鼠标悬停在图像集资源上，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。
   * 将鼠标悬停在图像集资源上，选择 **[!UICONTROL 选择]** （复选标记图标），然后选择 **[!UICONTROL 编辑]** 工具栏上。
   * 在图像集资源上选择，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。

1. 要编辑图像集中的图像，请执行以下任意操作：

   * 要重新排序资产，请将图像拖动到新位置（选择重新排序图标以移动项目）。
   * 要按升序或降序对项排序，请选择列标题。
   * 要添加资源或更新现有资源，请选择 **[!UICONTROL 添加资产]**. 导航到某个资源，选择该资源，然后选择 **[!UICONTROL 选择]** 在页面的右上角附近。

      >[!NOTE]
      >
      >如果通过将Experience Manager用于缩略图的图像替换为其他图像来删除该图像，则仍会显示原始资源。
   * 要删除资源，请选择该资源并选择 **[!UICONTROL 删除资源]**.
   * 要应用预设，请在页面的右上角附近，选择 **[!UICONTROL 预设]**，然后选择查看器预设。
   * 要添加或更改缩略图，请选择资源右侧旁边的缩略图图标。 导航到新的缩略图或样本资源，选择它，然后选择 **[!UICONTROL 选择]**.
   * 要删除整个图像集，请导航到该图像集，选择它，然后选择 **[!UICONTROL 删除]**.

   >[!NOTE]
   >
   >您可以通过导航到图像集来编辑图像，然后选择 **[!UICONTROL 设置成员]** 然后，选择单个资产上的“铅笔”图标以打开编辑窗口。

1. 选择 **[!UICONTROL 保存]** 完成编辑时。

## 预览图像集 {#previewing-image-sets}

参见 [预览资源](/help/assets/previewing-assets.md).

## 发布图像集 {#publishing-image-sets}

请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。
