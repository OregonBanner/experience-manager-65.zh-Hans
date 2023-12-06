---
title: 旋转集
description: 了解如何在Dynamic Media中创建旋转集来模拟实际转动对象的行为，以便从任何角度查看对象，从而查看详细信息。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Spin Sets,Asset Management
role: User, Admin
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 8%

---

# 旋转集{#spin-sets}

旋转集模拟旋转对象以对其进行检查的真实行为。 旋转集允许从任何角度查看项目，从任何角度获取关键的可视详细信息。

旋转集模拟360度的观看体验。 Dynamic Media提供单轴旋转集，查看器可以在其中旋转项目。 此外，用户只需点击几下鼠标即可“自由变形”缩放和平移任何视图。 通过这种方式，用户可以从特定的视点更细致地检查项目。

旋转集由带有单词的横幅指定 **[!UICONTROL 旋转集]**. 此外，如果旋转集已发布，则显示发布日期，由 **[!UICONTROL World]** 图标以及上次修改日期均在横幅上，由 **[!UICONTROL 铅笔]** 图标显示。

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>有关Assets用户界面的信息，请参阅 [管理资源](/help/assets/manage-assets.md).

在创建旋转集时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| 每个2D集的最大行/列数 | 每组12-18个图像 | 1000 |

另请参阅 [Dynamic Media限制](/help/assets/limitations.md).

## 快速入门：旋转集 {#quick-start-spin-sets}

要快速启动并运行旋转集，请执行以下步骤：

1. [上传图像供多个视图使用](#uploading-assets-for-spin-sets).

   对于一维旋转集，至少需要8-12次拍摄项目；对于二维旋转集，至少需要16-24次拍摄项目。 拍摄必须定期进行，以便给人一种旋转和翻转项目的印象。 例如，如果一维旋转集包含12个镜头，则为每个镜头旋转项目30° (360/12)。

   请参阅 [Dynamic Media — 支持的栅格图像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 有关旋转集支持的格式的列表。

1. [创建旋转集](#creating-spin-sets).

   要创建旋转集，请选择 **[!UICONTROL “创建”>“旋转集”]** 然后命名该集，选择资源，并选择图像的显示顺序。

   请参阅 [使用选择器](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >您还可以通过[批量集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建旋转集。**重要提示：** 批量集由IPS(Image Production System)作为资产引入的一部分创建，并且仅在Dynamic Media - Scene7模式下可用。

1. 设置 [旋转集查看器预设](/help/assets/managing-viewer-presets.md)（根据需要）。

   管理员可以创建或修改旋转集查看器预设。要查看带有查看器预设的旋转集，请选择旋转集，然后在左边栏下拉菜单中，选择&#x200B;**查看器**。

   请参阅 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]** 创建或编辑查看器预设。

   请参阅 [添加和编辑查看器预设](/help/assets/managing-viewer-presets.md).

1. [查看旋转集](#viewing-spin-sets).

   您可以通过三种不同的方式，查看和访问通过批次集预设创建的批次集。 (使用批次集预设创建的集，执行 *非* 显示在用户界面中。)

1. [预览旋转集](/help/assets/previewing-assets.md).

   选择旋转集并预览。 旋转旋转集。 您可以从中选择不同的查看器 **[!UICONTROL 查看器]** 菜单，可从左边栏下拉菜单中获取。

1. [发布旋转集](/help/assets/publishing-dynamicmedia-assets.md).

   发布旋转集将激活URL和嵌入字符串。 此外，您必须 [发布查看器预设](/help/assets/managing-viewer-presets.md).

1. [将URL链接到您的Web应用程序](/help/assets/linking-urls-to-yourwebapplication.md) 或 [嵌入视频查看器或图像查看器](/help/assets/embed-code.md).

   Adobe Experience Manager Assets会为旋转集创建URL调用，并在您发布旋转集后激活它们。 您可以在预览资产时复制这些URL。 或者，您可以将其嵌入到您的网站上。

   选择旋转集，然后在左边栏下拉菜单中选择&#x200B;**[!UICONTROL 查看器]**。

   请参阅 [将旋转集链接到网页](/help/assets/linking-urls-to-yourwebapplication.md) 和 [嵌入视频查看器或图像查看器](/help/assets/embed-code.md).

如有必要，您可以 [编辑旋转集](#editing-spin-sets). 此外，您还可以查看和修改 [旋转集属性](/help/assets/manage-assets.md#editing-properties).

## 上传旋转集的资产 {#uploading-assets-for-spin-sets}

对于一维旋转集，至少需要8-12次拍摄项目；对于二维旋转集，至少需要16-24次拍摄项目。 拍摄必须定期进行，以便给人一种旋转和翻转项目的印象。 例如，如果一维旋转集包含12个镜头，则为每个镜头旋转项目30° (360/12)。

您可以像上传一样上传旋转集的图像 [在Experience Manager Assets中上传任何其他资源](/help/assets/manage-assets.md).

请参阅 [Dynamic Media — 支持的栅格图像格式](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) 有关旋转集支持的格式的列表。

### 为旋转集捕获图像的准则 {#guidelines-for-shooting-spin-set-images}

以下是有关旋转集图像的一些最佳实践。 通常，旋转集中拥有的图像越多，图像旋转效果就越好。 但是，在集中包含许多图像也会增加加载图像所需的时间。 Experience Manager建议在拍摄旋转集中使用的图像时遵循以下准则：

* 至少，在一维旋转集中使用8-12个图像，在二维旋转集中使用16-24个图像。 至少需要8张图像才能旋转360度。 一维旋转集更常见，因为创建二维旋转集需要大量劳力。
* 使用无损格式；建议使用TIFF和PNG。
* 对所有图像进行蒙版，使项目出现在纯白色或其他高对比度背景上。 （可选）添加阴影。
* 确保产品详细信息光照良好且清晰。
* 拍摄带有人体模型或模特的时尚服装旋转图像。 通常，人体模型会被遮蔽（使用玻璃人体模型），或者图像中显示风格化的人体模型/服装。 可通过定义角度数来创建模型上的旋转集。 使用地板上的胶带标记每个角度，以便引导模型步进，并查看每个拍摄的方向。

## 创建旋转集 {#creating-spin-sets}

本节介绍如何在Experience Manager中创建旋转集。

>[!NOTE]
>
>您还可以通过[批量集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建旋转集。**重要提示：** 批量集由IPS(Image Production System)作为资产引入的一部分创建，并且仅在Dynamic Media - Scene7模式下可用。
>
>请参阅中的“创建批次集预设以自动生成图像集和旋转集” [配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
>

>[!NOTE]
>
>图像在旋转集物质中出现的顺序。 请务必对它们进行排序，以使旋转为360度的平滑视图。

在创建旋转集时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 限制类型 | 最佳实践 | 有限强制 |
| --- | --- | --- |
| 每个2D集的最大行/列数 | 每组12-18个图像 | 1000 |

另请参阅 [Dynamic Media限制](/help/assets/limitations.md).

**要创建旋转集，请执行以下操作：**

1. 在Assets中，导航到要创建旋转集的位置，然后选择 **[!UICONTROL 创建]**，并选择 **[!UICONTROL 旋转集]**. 您还可以从包含资产的文件夹中创建旋转集。此时将显示旋转集编辑器。

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. 在旋转集编辑器中，使用 **[!UICONTROL 标题]** 字段中，输入旋转集的名称。 该名称将显示在旋转集的横幅中。 （可选）输入说明。

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >创建旋转集时，您可以更改旋转集缩略图，或允许Experience Manager根据旋转集中的资源自动选择缩略图。 要选择缩略图，请选择 **[!UICONTROL 更改缩略图]** 并选择任意图像（您也可以导航到其他文件夹以查找图像）。 如果选择了缩略图，然后决定让Experience Manager从旋转集生成缩略图，请选择 **[!UICONTROL 切换到自动缩略图]**.

1. 执行以下任一操作：

   * 在旋转集编辑器页面的左上角附近，选择 **[!UICONTROL 添加资源]**.

   * 在“旋转集编辑器”页面中间附近，选择 **[!UICONTROL 选择以打开资产选择器]**.

   选择以选择要包含在旋转集中的资产。 选定资产上有一个复选标记图标。完成后，在页面的右上角附近，选择 **[!UICONTROL 选择]**.

   借助资产选择器，您可以通过键入关键字并点按&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后选择 **[!UICONTROL 筛选]** 图标。 点按“视图”图标并选择&#x200B;**[!UICONTROL 列视图]**、**[!UICONTROL 卡片视图]**&#x200B;或&#x200B;**[!UICONTROL 列表视图]**&#x200B;可更改视图。

   请参阅 [使用选择器](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 将资源添加到集时，会自动按字母数字顺序添加资源。 添加资源后，您可以手动对资源重新排序或排序。

   如有必要，请将资产的“重新排序”图标拖动到资产文件名的右侧，以将图像向上或向下重新排序。

   ![通过将旋转集中的帧11拖动到新位置来重新排序它](assets/6_5_spinset-reorderassets.png).

   通过将旋转集中的帧11拖动到新位置来重新对其进行排序。

1. （可选）执行以下任一操作：

   * 要删除图像，请选择该图像并选择 **[!UICONTROL 删除资源]**.

   * 要应用预设，请选择页面右上角附近的 **[!UICONTROL 预设]**，然后选择要一次性应用于所有资产的预设。

1. 选择&#x200B;**[!UICONTROL 保存]**。新创建的旋转集将出现在您创建该旋转集的文件夹中。

## 查看旋转集 {#viewing-spin-sets}

可在用户界面中创建旋转集，也可使用 [批次集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). 但是，使用批次集预设创建的集，请 *非* 显示在用户界面中。 您可以通过三种不同的方式访问通过批次集预设创建的批次集。 （即使已在用户界面中创建旋转集，这些方法也可用）。

>[!NOTE]
>
>您还可以通过用户界面查看集，如中所述 [编辑旋转集](#editing-spin-sets).

**要查看旋转集，请执行以下操作：**

1. 打开单个资产的属性时。 属性指示所选资产所属的集(在 **[!UICONTROL 集成员]**)。 选择集的名称，以便查看整个集。

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 来自任何集的成员图像。选择 **[!UICONTROL 集]** 菜单以显示资产所属的集。

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. 从搜索中，您可以选择&#x200B;**[!UICONTROL 过滤器]**，然后展开 **[!UICONTROL Dynamic Media]**，并选择&#x200B;**[!UICONTROL 集]**。

   搜索会返回在UI中手动创建或通过批次集预设自动创建的匹配集。 对于自动化集，搜索查询使用 `Starts with` 搜索条件不同于基于使用搜索的Experience Manager搜索 `Contains` 搜索条件。 将筛选条件设置为 **[!UICONTROL 集]** 是搜索自动化集的唯一方法。

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 编辑旋转集 {#editing-spin-sets}

您可以对旋转集执行各种编辑任务，如下所示：

* 将图像添加到旋转集。
* 对旋转集中的图像重新排序。
* 删除旋转集中的资产。
* 应用查看器预设。
* 删除旋转集。

**要编辑旋转集，请执行以下操作：**

1. 执行以下任一操作：

   * 将鼠标悬停在旋转集资产上，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。
   * 将鼠标悬停在旋转集资产上，选择 **[!UICONTROL 选择]** （复选标记图标），然后选择 **[!UICONTROL 编辑]** 工具栏上。

   * 选择旋转集资源，然后选择 **[!UICONTROL 编辑]** （铅笔图标）。

1. 要编辑旋转集，请执行以下任一操作：

   * 要重新排序图像，请将图像拖动到新位置（选择重新排序图标以移动项目）。
   * 要按升序或降序对项排序，请选择列标题。
   * 要添加资源或更新现有资源，请选择 **[!UICONTROL 添加资源]**. 导航到资源，选择它，然后选择 **[!UICONTROL 选择]** 靠近右上角。
如果通过将Experience Manager用于缩略图的图像替换为其他图像来删除该图像，则仍会显示原始资源。
   * 要删除某个资源，请选择该资源并选择 **[!UICONTROL 删除资源]**.
   * 要应用预设，请选择“预设”图标并选择预设。
   * 要删除整个旋转集，请导航到该旋转集，选择它，然后选择 **[!UICONTROL 删除]**
   >[!NOTE]
   >
   >您可以通过导航到旋转集来编辑图像，然后选择 **[!UICONTROL 设置成员]** 在左边栏中，然后选择单个资产上的铅笔图标以打开编辑窗口。

1. 选择 **[!UICONTROL 保存]** 完成编辑时。

## 预览旋转集 {#previewing-spin-sets}

请参阅 [预览资源](/help/assets/previewing-assets.md).

## 发布旋转集 {#publishing-spin-sets}

请参阅 [发布资源](/help/assets/publishing-dynamicmedia-assets.md).
