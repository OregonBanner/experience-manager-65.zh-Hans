---
title: 旋转集
description: 了解如何在Dynamic Media中使用旋转集
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
feature: Spin Sets,Asset Management
role: User, Admin
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 24%

---

# 旋转集{#spin-sets}

旋转集模拟旋转对象的真实动作，以便于进行检查。通过旋转集，可以从任意角度查看项目，从而获取任意角度的重要可视细节。

旋转集模拟360°的查看体验。 Dynamic Media 提供单轴旋转集，查看者可在该旋转集中旋转项目。此外，用户只需单击几下鼠标即可“自由”缩放和平移任何视图。 这样，用户就可以从任何特定视角更仔细地检查项目。

旋转集由带有单词的横幅来指定 **[!UICONTROL 旋转集]**.此外，如果旋转集已发布，则发布日期(由 **[!UICONTROL 世界]** 图标，以及上次修改日期(由 **[!UICONTROL 铅笔]** 图标。

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>有关Assets用户界面的信息，请参阅 [管理资产](/help/assets/manage-assets.md).

在创建旋转集时，Adobe建议遵循以下最佳实践，并强制实施以下限制：

| 限制类型 | 最佳实践 | 规定的限制 |
| --- | --- | --- |
| 每个2D集的最大行/列数 | 每套12-18页图片 | 1000 |

另请参阅 [Dynamic Media限制](/help/assets/limitations.md).

## 快速入门：旋转集 {#quick-start-spin-sets}

要快速设置并运行旋转集，请执行以下步骤：

1. [为多个视图上传图像](#uploading-assets-for-spin-sets).

   对于一维旋转集，您至少需要一个项目8-12张拍照；对于二维旋转集，您至少需要16-24张拍照。必须定期拍摄这些照片，以给人以项目正在旋转和被翻动的印象。 例如，如果一维旋转集包含12张照片，则对于每张照片，旋转项目30° (360/12)。

   请参阅 [Dynamic Media — 支持的栅格图像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 以获取旋转集支持的格式列表。

1. [创建旋转集](#creating-spin-sets).

   要创建旋转集，请选择 **[!UICONTROL 创建>旋转集]** 然后命名该集，选择资产，然后选择图像的显示顺序。

   请参阅 [使用选择器](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >您还可以通过[批量集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建旋转集。**重要信息：** 批量集由IPS（图像生产系统）作为资产摄取的一部分创建，并且只能在Dynamic Media - Scene7模式下使用。

1. 根据需要设置[旋转集查看器预设](/help/assets/managing-viewer-presets.md)。

   管理员可以创建或修改旋转集查看器预设。要查看带有查看器预设的旋转集，请选择旋转集，然后在左边栏下拉菜单中，选择&#x200B;**查看器**。

   请参阅 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]** 要创建或编辑查看器预设。

   请参阅 [添加和编辑查看器预设](/help/assets/managing-viewer-presets.md).

1. [查看旋转集](#viewing-spin-sets).

   您可以通过三种不同方式查看和访问通过批集预设方式创建的集。 (使用批集预设创建的集，可以 *not* 显示在用户界面中。)

1. [预览旋转集](/help/assets/previewing-assets.md).

   选择旋转集，之后您便可以进行预览。旋转该旋转集。您可以从 **[!UICONTROL 查看器]** 菜单（可从左边栏下拉菜单中访问）。

1. [发布旋转集](/help/assets/publishing-dynamicmedia-assets.md).

   发布旋转集时，将会激活 URL 和嵌入字符串。此外，您还必须 [发布查看器预设](/help/assets/managing-viewer-presets.md).

1. [将URL关联到您的Web应用程序](/help/assets/linking-urls-to-yourwebapplication.md) 或 [嵌入视频查看器或图像查看器](/help/assets/embed-code.md).

   Adobe Experience Manager Assets会为旋转集创建URL调用，并在您发布旋转集后将其激活。 预览资产时，您可以复制这些 URL。或者，您也可以将这些 URL 嵌入到网站中。

   选择旋转集，然后在左边栏下拉菜单中选择&#x200B;**[!UICONTROL 查看器]**。

   请参阅 [将旋转集关联到网页](/help/assets/linking-urls-to-yourwebapplication.md) 和 [嵌入视频查看器或图像查看器](/help/assets/embed-code.md).

如有必要，您可以 [编辑旋转集](#editing-spin-sets). 此外，您还可以查看和修改 [旋转集属性](/help/assets/manage-assets.md#editing-properties).

## 上传旋转集的资产 {#uploading-assets-for-spin-sets}

对于一维旋转集，您至少需要一个项目8-12张拍照；对于二维旋转集，您至少需要16-24张拍照。必须定期拍摄这些照片，以给人以项目正在旋转和被翻动的印象。 例如，如果一维旋转集包含12张照片，则对于每张照片，旋转项目30° (360/12)。

您可以像上传一样上传旋转集的图像 [上传Experience Manager Assets中的任何其他资产](/help/assets/manage-assets.md).

请参阅 [Dynamic Media — 支持的栅格图像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 以获取旋转集支持的格式列表。

### 为旋转集捕获图像的准则 {#guidelines-for-shooting-spin-set-images}

以下是关于旋转集图像的一些最佳实践。一般而言，旋转集中的图像越多，图像的旋转效果越好。但是，在旋转集中包含很多图像也会使加载图像所需的时间变长。Experience Manager建议，拍摄图像以在旋转集中使用的准则如下：

* 在一维旋转集中至少使用8-12幅图像，在二维旋转集中至少使用16-24幅图像。要转到360°，至少需要8张图像。 一维旋转集比较常见，因为创建二维旋转集需要耗费大量人力。
* 使用无损格式；建议使用 TIFF 和 PNG。
* 对所有图像使用蒙版，以使项目显示在纯白或其他高对比度的背景中。或者，也可以添加阴影。
* 确保充分突出产品细节，使其成为焦点。
* 拍摄时装的旋转图像时，使用模特道具或真人模特。通常，模特人道模型会被蒙版（使用玻璃材质的模特人道模型），或者图像中会显示风格化的模特人道模型/裁缝。 您可以通过定义多个角度来创建真人模特展示旋转集。用胶带在地板上标出每个角度，以便引导模型步进并查看每个拍摄方向。

## 创建旋转集 {#creating-spin-sets}

本节介绍如何在Experience Manager中创建旋转集。

>[!NOTE]
>
>您还可以通过[批量集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建旋转集。**重要信息：** 批量集由IPS（图像生产系统）作为资产摄取的一部分创建，并且只能在Dynamic Media - Scene7模式下使用。
>
>请参阅 [配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).

>[!NOTE]
>
>旋转集中的图像显示顺序很重要。请务必对其进行排序，以便旋转是一个平滑的360°视图。

在创建旋转集时，Adobe建议遵循以下最佳实践，并强制实施以下限制：

| 限制类型 | 最佳实践 | 有限制 |
| --- | --- | --- |
| 每个2D集的最大行/列数 | 每套12-18页图片 | 1000 |

另请参阅 [Dynamic Media限制](/help/assets/limitations.md).

**要创建旋转集，请执行以下操作：**

1. 在资产中，导航到要创建旋转集的位置，选择 **[!UICONTROL 创建]**，然后选择 **[!UICONTROL 旋转集]**. 您还可以从包含资产的文件夹中创建旋转集。此时将显示旋转集编辑器。

   ![6_5_spinset_createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. 在旋转集编辑器中， **[!UICONTROL 标题]** 字段，输入旋转集的名称。 该名称会显示在旋转集的横幅中。（可选）输入说明。

   ![6_5_spinset_spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >创建旋转集时，您可以更改旋转集缩略图，或允许Experience Manager根据旋转集中的资产自动选择缩略图。 要选择缩略图，请选择 **[!UICONTROL 更改缩略图]** 并选择任意图像（您也可以导航到其他文件夹以查找图像）。 如果您选择了缩略图，然后决定让Experience Manager从旋转集中生成缩略图，请选择 **[!UICONTROL 切换到自动缩略图]**.

1. 执行以下操作之一：

   * 在“旋转集编辑器”页面的左上角附近，选择 **[!UICONTROL 添加资产]**.

   * 在“旋转集编辑器”页面的中间附近，选择 **[!UICONTROL 点按以打开资产选择器]**.
   点按以选择要包含在旋转集中的资产。 选定资产上有一个复选标记图标。完成后，在页面的右上角附近，选择 **[!UICONTROL 选择]**.

   借助资产选择器，您可以通过键入关键字并点按&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后选择 **[!UICONTROL 过滤器]** 图标。 点按“视图”图标并选择&#x200B;**[!UICONTROL 列视图]**、**[!UICONTROL 卡片视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;可更改视图。

   请参阅 [使用选择器](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在将资产添加到资产集时，资产会按字母数字顺序自动添加。 您可以在添加资产后手动重新排序或排序资产。

   如有必要，请将资产的重新排序图标拖动到资产文件名右侧，以在设置列表的上下方对图像重新排序。

   ![通过将旋转集中的第11帧拖动到新位置来重新排序](assets/6_5_spinset-reorderassets.png).

   通过将旋转集中的第11帧拖动到新位置，对其重新排序。

1. （可选）执行以下操作之一：

   * 要删除图像，请选择该图像并选择 **[!UICONTROL 删除资产]**.

   * 要应用预设，请在页面的右上角附近，选择 **[!UICONTROL 预设]**，然后选择要同时应用于所有资产的预设。

1. 选择&#x200B;**[!UICONTROL 保存]**。您新创建的旋转集会显示在创建时所用的文件夹中。

## 查看旋转集 {#viewing-spin-sets}

您可以在用户界面中创建旋转集，也可以使用 [批次集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). 但是，使用批集预设创建的集，请执行 *not* 显示在用户界面中。 您可以通过三种不同方式访问通过批集预设创建的集。 （即使您是在用户界面中创建旋转集，这些方法也可用）。

>[!NOTE]
>
>您还可以通过用户界面查看集，如 [编辑旋转集](#editing-spin-sets).

**要查看旋转集，请执行以下操作：**

1. 打开单个资产的属性时。 属性指示所选资产是的成员集(在 **[!UICONTROL 集成员]**)。 选择集的名称，以便您能够查看整个集。

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 来自任何集的成员图像。选择 **[!UICONTROL 集]** 菜单，以显示资产所属的集。

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 从搜索中，您可以选择&#x200B;**[!UICONTROL 过滤器]**，然后展开 **[!UICONTROL Dynamic Media]**，并选择&#x200B;**[!UICONTROL 集]**。

   搜索会返回在UI中手动创建的匹配集，或通过批集预设自动创建的匹配集。 对于自动集，使用 `Starts with` 搜索标准，与基于使用的Experience Manager搜索不同 `Contains` 搜索标准。 将过滤器设置为 **[!UICONTROL 集]** 是搜索自动集的唯一方法。

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 编辑旋转集 {#editing-spin-sets}

您可以对旋转集执行各种编辑任务，如下所示：

* 向旋转集中添加图像。
* 对旋转集中的图像重新排序。
* 删除旋转集中的资产。
* 应用查看器预设。
* 删除旋转集。

**要编辑旋转集，请执行以下操作：**

1. 执行以下任一操作：

   * 将鼠标悬停在旋转集资产上，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。
   * 将鼠标悬停在旋转集资产上，选择 **[!UICONTROL 选择]** （复选标记图标），然后选择 **[!UICONTROL 编辑]** 中。

   * 在旋转集资产上选择，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。

1. 要编辑旋转集，请执行以下任一操作：

   * 要对图像重新排序，请将图像拖到新位置（选择重新排序图标以移动项目）。
   * 要按升序或降序对项目进行排序，请选择列标题。
   * 要添加资产或更新现有资产，请选择 **[!UICONTROL 添加资产]**. 导航到资产，选择该资产，然后选择 **[!UICONTROL 选择]** 在右上角附近。
如果您通过将Experience Manager用作缩略图的图像替换为其他图像来删除图像，则仍会显示原始资产。
   * 要删除资产，请选择资产，然后选择 **[!UICONTROL 删除资产]**.
   * 要应用预设，请选择预设图标，然后选择预设。
   * 要删除整个旋转集，请导航到旋转集，将其选中，然后选择 **[!UICONTROL 删除]**

   >[!NOTE]
   >
   >您可以通过导航到旋转集并选择 **[!UICONTROL 设置成员]** ，然后选择单个资产上的铅笔图标以打开编辑窗口。

1. 选择 **[!UICONTROL 保存]** 完成编辑时。

## 预览旋转集 {#previewing-spin-sets}

请参阅 [预览资产](/help/assets/previewing-assets.md).

## 发布旋转集 {#publishing-spin-sets}

请参阅 [发布资产](/help/assets/publishing-dynamicmedia-assets.md).
