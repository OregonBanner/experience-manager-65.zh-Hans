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
translation-type: tm+mt
source-git-commit: c3ae4447581d946554d792c68d31b47a6b67d5df
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 45%

---


# 图像集 {#image-sets}

借助图像集，用户可以通过单击缩略图来查看项目的不同视图，从而为用户提供集成式查看体验。图像集使您可以展示同一项目的替换视图，并且查看器提供了可用于仔细检查图像的缩放工具。

图像集由带有单词的横幅来指定 `IMAGESET`。 此外，如果图像集已发布，则横幅上会显示由 **[!UICONTROL World]** 图标指示的发布日期以及由铅笔图标指示的上次修改日期 **** 。

![chlimage_1-133](assets/chlimage_1-339.png)

在图像集中，您还可以通过创建图像集并添加缩略图来创建色板。

当您希望以不同的颜色、模式或外表显示某个项目时，此应用程序尤其有用。要创建带有颜色样本的图像集，您要向用户展示的每种不同的颜色、模式或外表都需要有一个图像。每种颜色、模式或外表还需要有一个颜色、模式或外表样本。

例如，假定您要展示帽檐颜色各异的帽子图像，且帽檐分别为红色、绿色和蓝色。在这种情况下，您需要准备同一款帽子的三张拍照。这三张拍照分别对应红色、绿色和蓝色的帽檐。您还需要准备红色、绿色和蓝色三种颜色的样本。颜色样本用作用户在样本集查看器中单击以查看红标、绿标或蓝标帽子的缩略图。

>[!NOTE]
>
>有关资产用户界面的信息，请参阅[管理资产](/help/assets/manage-assets.md)。

## 快速入门：图像集 {#quick-start-image-sets}

要快速设置并运行图像集，请执行以下操作：

1. [为多个视图上传主源图像。](#uploading-assets-in-image-sets)

   首先为图像集上传图像。由于用户可以在图像集查看器中缩放图像，因此在选择图像时，请考虑缩放因素。确保图像的最大尺寸至少有2000像素，以实现最佳缩放细节。 Dynamic Media可以渲染每幅高达2500万像素的图像。 例如，您可以使用5000 x 5000万像素的图像或任何其他大小的组合，最高可达2500万像素。

   AEM 资产支持很多种图像文件格式，但建议使用无损的 TIFF、PNG 和 EPS 图像。

1. [创建图像集。](#creating-image-sets)

   在图像集中，用户在图像集查看器中单击缩略图。

   要在资产中创建图像集，请点按或单击&#x200B;**[!UICONTROL 创建>图像集。]** 然后，添加图像，并单击“ **[!UICONTROL 保存”。]**

   您还可以通过[批集预设](/help/assets/config-dms7.md)自动创建图像集。
   >[!IMPORTANT]
   >
   >批集由IPS（图像生产系统）创建，作为资产摄取的一部分，并且仅在Dynamic Media -Scene7模式下可用。

   请参阅[准备要上传的图像集资产和上传文件](#uploading-assets-in-image-sets)。

   请参阅[使用选择器。](/help/assets/working-with-selectors.md)

1. 根据需要添加[图像集查看器预设](/help/assets/managing-viewer-presets.md)。

   管理员可以创建或修改图像集查看器预设。要查看带有查看器预设的图像集，请选择图像集，在左边栏下拉菜单中，选择&#x200B;**[!UICONTROL 查看器。]**

   请参阅&#x200B;**[!UICONTROL 工具>资产>查看器预设]**&#x200B;以创建或编辑查看器预设。

1. （可选）[查看使用批集预设创建的图像集](/help/assets/image-sets.md#viewing-image-sets)。
1. [预览图像集。](/help/assets/previewing-assets.md)

   选择图像集后，您便可以预览该图像集。单击缩略图图标可在选定的查看器中检查图像集。您可以从左边栏下拉菜单中的&#x200B;**[!UICONTROL 查看器]**&#x200B;菜单中选择不同的查看器。

1. [发布图像集。](/help/assets/publishing-dynamicmedia-assets.md)

   发布图像集时，将激活URL和嵌入代码。 此外，您必须[发布已创建的任何自定义查看器预设](/help/assets/managing-viewer-presets.md)。 现成查看器预设已发布。

1. [将URL关联到您的Web](/help/assets/linking-urls-to-yourwebapplication.md) 应用程 [序或嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

   在发布图像集后，AEM 资产会为该图像集创建 URL 调用并将其激活。预览资产时，您可以复制这些 URL。或者，也可以将它们嵌入到您的网站上。

   选择图像集，然后在左边栏下拉菜单中，选择&#x200B;**[!UICONTROL 查看器。]**

   请参 [阅将图像集链接到网页和嵌入视](/help/assets/linking-urls-to-yourwebapplication.md) 频查看器或图像查看器 [](/help/assets/embed-code.md)。

要编辑图像集，请参阅[编辑图像集。](#editing-image-sets) 此外，您还可以视图和编 [辑图像集属性](/help/assets/manage-assets.md#editing-properties)。

如果创建集时遇到问题，请参阅[ Dynamic Media -Scene7模式疑难解答](/help/assets/troubleshoot-dms7.md#images-and-sets)中的图像和集。

## 上传图像集中的资产 {#uploading-assets-in-image-sets}

首先为图像集上传图像。由于用户可以在图像集查看器中缩放图像，因此在选择图像时，请考虑缩放因素。确保图像的最大尺寸至少为2000像素。图像集支持很多种图像文件格式，但建议使用无损的 TIFF、PNG 和 EPS 图像。

您可以像上传资产](/help/assets/manage-assets.md#uploading-assets)中的任何其他资产一样，为图像集上传图像。[

### 准备要上传的图像集资产 {#preparing-image-set-assets-for-upload}

在创建图像集之前，请确保图像的大小和格式均合适。

要创建多视图的图像集，您需要多个图像，它们要从不同视角显示一个项目或显示同一项目的不同方面。其目标是突出一个项目的各项重要功能，以便查看者能够全面地了解该项目的外观或用途。

由于用户可以缩放图像集中的图像，请确保图像的最大尺寸至少有 2000 像素。资产支持很多种图像文件格式，但建议使用无损的 TIFF、PNG 和 EPS 图像。

>[!NOTE]
>
>此外，如果您使用缩略图指示产品样本，则需要以下各项：
>
>您需要小插图，也就是同一图像的不同拍照，以显示该图像的不同颜色、模式或外表。您还需要与不同颜色、模式或外表相对应的缩略图文件。例如，要通过显示同一款夹克的黑色、咖色和绿色版的图像集展示缩略图，您需要：
>
>* 同一款夹克的黑色、咖色和绿色版拍照。
>* 黑色、咖色和绿色版的缩略图。


## 创建图像集 {#creating-image-sets}

您可以通过用户界面或 API 创建图像集。本节将会介绍如何在用户界面中创建图像集。

>[!NOTE]
>
>您还可以通过[批集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建图像集。
>**重要：**&#x200B;批集由IPS（映像生产系统）创建，作为资产摄取的一部分，并且仅在Dynamic Media -Scene7模式中可用。

将资产添加到资产集时，资产会按字母数字顺序自动添加。 在添加资产后，您可以手动对资产重新排序或排序。

>[!NOTE]
>
>文件名中带有“,”（逗号）的资产不支持图像集。

**创建图像集**

1. 在AEM中，点按AEM徽标以访问全局导航控制台，然后点按导航 **[!UICONTROL >资产。]**&#x200B;导航到要创建图像集的位置，然后点按创建 **[!UICONTROL >图像集]** ，以打开“图像集编辑器”页。

   您还可以从包含资产的文件夹中创建旋转集。

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. 在“图像集编辑器”页面的&#x200B;**[!UICONTROL 标题]**&#x200B;字段中，输入图像集的名称。 该名称会显示在图像集的横幅中。（可选）输入说明。

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. 执行以下操作之一：

   * 在“图像集编辑器”页面的左上角附近，点按&#x200B;**[!UICONTROL 添加资产。]**

   * 在“图像集编辑器”页面的中间附近，点按&#x200B;**[!UICONTROL 点按以打开资产选择器。]**
   点按以选择要包含在图像集中的资产。 选定资产上有一个复选标记图标。完成后，在页面右上角附近，点按&#x200B;**[!UICONTROL 选择。]**

   借助资产选择器，您可以通过键入关键字并点按或单击&#x200B;**[!UICONTROL 返回来搜索资产。]**&#x200B;您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后点按工具栏上的&#x200B;**[!UICONTROL 过滤器]**&#x200B;图标。点按视图图标并选择&#x200B;**[!UICONTROL 列视图]**、**[!UICONTROL 卡视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图，以更改视图。]**

   请参阅[使用选择器。](/help/assets/working-with-selectors.md)

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. 将资产添加到资产集时，资产会按字母数字顺序自动添加。 在添加资产后，您可以手动对资产重新排序或排序。

   如有必要，请将资产的重新排序图标拖动到资产文件名的右侧，以在设置的列表中向上或向下对图像重新排序。

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   如果要更改缩略图或色板，请单击图像旁的 **+** **缩略图**&#x200B;图标，然后导航到所需的缩略图或色板。选择完所有图像后，单击“保存”。]****[!UICONTROL 

1. （可选）执行以下操作之一：

   * 要删除图像，请选择该图像，然后点按&#x200B;**[!UICONTROL 删除资产。]**

   * 要应用预设，请点按页面右上角附近的&#x200B;**[!UICONTROL 预设]**，然后选择一个预设以一次应用于所有资产。
   >[!NOTE]
   >
   >创建图像集时，您可以更改图像集缩略图，或允许 AEM 根据图像集中的资产自动选择缩略图。要选择缩略图，请点按“图像集编辑器”页面中“标题”字段上方的&#x200B;**[!UICONTROL 更改缩略图]**，然后选择任意图像（您也可以导航到其他文件夹以查找图像）。如果您已选择缩略图，然后决定要AEM从图像集生成缩略图，请选择&#x200B;**[!UICONTROL 切换到]** **[!UICONTROL 自动缩略图。]**

1. 单击&#x200B;**[!UICONTROL 保存。]**&#x200B;您新创建的图像集会显示在创建时所用的文件夹中。

## 查看图像集{#viewing-image-sets}

您可以在用户界面中创建图像集，也可以使用[批集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建图像集。

>[!IMPORTANT]
>
>批集由IPS [映像生产系统]创建，作为资产摄取的一部分，并且仅在Dynamic Media -Scene7模式下可用。)

但是，使用批集预设创建的集合，在用户界面中不显示&#x200B;*。*&#x200B;您可以通过三种不同的方式视图这些集。 （即使您在用户界面中创建了图像集，这些方法也可用。）

* 打开单个资产的属性。 属性指示引用选定资产或其成员的集合。 单击集合的名称可查看整个集合。

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties2.png)

* 来自任何集的成员图像。选择&#x200B;**[!UICONTROL 集]**&#x200B;菜单以显示资产所属的集。

   ![6_5_imageset_setspuldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* 在搜索中，您可以选择&#x200B;**[!UICONTROL 过滤器]**，然后展开&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;并选择&#x200B;**[!UICONTROL 集。]**

   搜索会返回在UI中手动创建或通过批集预设自动创建的匹配集。 对于自动集，搜索查询使用与AEM搜索不同的“具有开始”搜索条件（基于使用“包含”搜索条件）进行。 将过滤器设置为&#x200B;**[!UICONTROL Sets]**&#x200B;是搜索自动集的唯一方法。

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>您可以通过用户界面视图集，如[编辑图像集](#editing-image-sets)中所述。

## 编辑图像集 {#editing-image-sets}

您可以对图像集执行各种编辑任务，如：

* 向图像集中添加图像。
* 对图像集中的图像重新排序。
* 删除图像集中的资产。
* 应用查看器预设。
* 删除图像集。

**编辑图像集**

1. 执行下列任一操作：

   * 将鼠标悬停在图像集资产上，然后点按&#x200B;**[!UICONTROL 编辑]**（铅笔图标）。
   * 将鼠标悬停在图像集资产上，点按&#x200B;**[!UICONTROL 选择]**（复选标记图标），然后点按工具栏上的&#x200B;**[!UICONTROL 编辑]**。
   * 点按图像集资产，然后点按工具栏上的&#x200B;**[!UICONTROL 编辑]**（铅笔图标）。

1. 要编辑图像集中的图像，请执行以下任意操作：

   * 要对资产重新排序，请将图像拖动到新位置（选择重新排序图标以移动项目）。
   * 要按升序或降序对项目排序，请单击列标题。
   * 要添加资产或更新现有资产，请单击&#x200B;**[!UICONTROL 添加资产。]** 导航到资产，选择它，然 **** 后点按页面右上角附近的选择。

      >[!NOTE]
      >
      >如果通过将缩略图替换为其他图像来删除AEM用的缩略图图像，则仍会显示原始资产。
   * 要删除资产，请选择该资产，然后点按或单击&#x200B;**[!UICONTROL 删除资产。]**
   * 要应用预设，请点按页面右上角附近的&#x200B;**[!UICONTROL 预设]**，然后选择查看器预设。
   * 要添加或更改缩略图，请选择资产右侧的缩略图图标。 导航到新的缩略图或样本资产，选择它，然后点按&#x200B;**[!UICONTROL 选择。]**
   * 要删除整个图像集，请导航到该图像集，将其选中，然后点按&#x200B;**[!UICONTROL 删除。]**

   >[!NOTE]
   >
   >您可以导航到图像组，点按左边栏中的&#x200B;**[!UICONTROL 设置成员]**，然后点按单个资产上的“铅笔”图标以打开编辑窗口，来编辑图像。

1. 完成编辑后，点按&#x200B;**[!UICONTROL 保存]**。

## 预览图像集 {#previewing-image-sets}

请参阅[预览资产](/help/assets/previewing-assets.md)。

## 发布图像集 {#publishing-image-sets}

请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。
