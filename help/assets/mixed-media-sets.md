---
title: 混合媒体集
description: 了解如何在Dynamic Media中使用混合媒体集
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
feature: 混合媒体集，资产管理
role: User, Admin
exl-id: 70a72fb9-a289-4eda-abcc-300edf9f1961
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 26%

---

# 混合媒体集{#mixed-media-sets}

通过混合媒体集，您可以在一份展示中提供图像、图像集、旋转集和视频的组合内容。

混合媒体集由带有MixedMediaSet字样的横幅 **[!UICONTROL 指定]**。 此外，如果混合媒体集已发布，则横幅上会显示发布日期(由 **[!UICONTROL World]** 图标指示)以及上次修改日期(由 **** Pencil图标指示)。

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>有关Assets用户界面的信息，请参阅[管理资产](/help/assets/manage-assets.md)。

## 快速入门：混合媒体集 {#quick-start-mixed-media-sets}

要快速设置并运行混合媒体集，请执行以下步骤：

1. [上传资产](#uploading-assets)。

   首先为混合媒体集上传图像和视频。 如有必要，请创 [建图像集](/help/assets/image-sets.md)[和旋转集](/help/assets/spin-sets.md)。 由于用户可以在混合媒体集查看器中缩放图像，因此请仔细选择图像。 确保图像的最大尺寸至少为2000像素。

1. [创建混合媒体集](#creating-mixed-media-sets)。

   要创建混合媒体集，请从“资产”页面中，选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 混合媒体集]**，然后命名该集，选择资产，并选择图像的显示顺序。

   请参阅[使用选择器](/help/assets/working-with-selectors.md)。

1. 根据需要设置[混合媒体查看器预设](/help/assets/managing-viewer-presets.md)。

   管理员可以创建或修改混合媒体集查看器预设。要查看带有查看器预设的混合媒体，请选择混合媒体集，然后在左边栏下拉菜单中，选择&#x200B;**[!UICONTROL 查看器]**。

   要创建或编辑查看器预设，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**。

   请参阅[添加和编辑查看器预设](/help/assets/managing-viewer-presets.md)。

1. [预览混合媒体集](#previewing-mixed-media-sets)。

   选择混合媒体集，之后您便可以进行预览。选择缩略图图标，以便在选定的查看器中检查混合媒体集。 您可以从左边栏下拉菜单的&#x200B;**[!UICONTROL 查看器]**&#x200B;菜单中选择不同的查看器。

1. [发布混合媒体集](#publishing-mixed-media-sets)。

   发布混合媒体集时，将会激活 URL 和嵌入字符串。此外，您还必须[发布查看器预设](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)。

1. [将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)或者[嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

   Adobe Experience Manager Assets会为混合媒体集创建URL调用，并在您发布混合媒体集后激活它们。 预览资产时，您可以复制这些 URL。或者，您也可以将这些 URL 嵌入到网站中。

   选择混合媒体集，然后在左边栏下拉菜单中，选择&#x200B;**[!UICONTROL 查看器]**。

   请参阅[将混合媒体集链接到网页](/help/assets/linking-urls-to-yourwebapplication.md)和[嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

如有必要，您可以编辑[混合媒体集](#editing-mixed-media-sets)。 此外，您还可以查看和修改[混合媒体集属性](/help/assets/manage-assets.md#editing-properties)。

>[!NOTE]
>
>如果在创建集时遇到问题，请参阅[Dynamic Media - Scene7模式疑难解答](/help/assets/troubleshoot-dms7.md)。

## 上传资产 {#uploading-assets}

首先为混合媒体集上传图像和视频。 由于用户可以在混合媒体集查看器中缩放图像，因此请仔细选择图像。 确保图像的最大尺寸至少为2000像素。

此外，如果要向混合媒体集添加旋转集或图像集，也应创建这些集。

## 创建混合媒体集 {#creating-mixed-media-sets}

您可以向混合媒体集添加图像、图像集、旋转集和视频。 在将您的文件、图像集和旋转集添加到混合媒体集之前，请确保您已准备好发布它们。

在将资产添加到资产集时，资产会按字母数字顺序自动添加。 您可以在添加资产后手动重新排序或排序资产。

**要创建混合媒体集，请执行以下操作：**

1. 在Assets中，导航到要创建混合媒体集的位置，选择&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 混合媒体集]**。 您还可以从包含资产的文件夹中创建旋转集。此时将显示混合媒体集编辑器。

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. 在混合媒体集编辑器的&#x200B;**[!UICONTROL 标题]**&#x200B;中，输入混合媒体集的名称。 该名称会显示在混合媒体集的横幅中。（可选）输入说明。

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >创建混合媒体集时，您可以更改混合媒体集缩略图，或允许Experience Manager根据混合媒体集中的资产自动选择缩略图。 要选择缩略图，请选择&#x200B;**[!UICONTROL 更改缩略图]**&#x200B;并选择任意图像（您也可以导航到其他文件夹以查找图像）。 如果您选择了缩略图，然后决定让Experience Manager从混合媒体集中生成缩略图，请选择&#x200B;**[!UICONTROL 切换到自动缩略图]**。

1. 选择资产选择器，以便您能够选择要包含在混合媒体集中的资产。 选择它们，然后选择&#x200B;**[!UICONTROL 选择]**。

   借助资产选择器，您可以通过键入关键字并点按&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后从工具栏中选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;图标。 选择&#x200B;**[!UICONTROL 视图]**&#x200B;图标，然后选择&#x200B;**[!UICONTROL 列表视图]**、**[!UICONTROL 列视图]**&#x200B;或&#x200B;**[!UICONTROL 卡片视图]**&#x200B;以更改视图。

   请参阅[使用选择器](/help/assets/working-with-selectors.md)。

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. 通过向上或向下拖动资产来重新排序资产（必要时必须选择&#x200B;**[!UICONTROL 重新排序]**&#x200B;图标）。

   ![chlimage_1-141](assets/chlimage_1-352.png)

   如果要添加缩略图，请选择图像旁边的&#x200B;**+** **[!UICONTROL 缩略图]**&#x200B;图标，然后导航到所需的缩略图。 选择完所有缩略图图像后，选择&#x200B;**[!UICONTROL 保存]**。

   >[!NOTE]
   >
   >如果要添加资产，请选择&#x200B;**[!UICONTROL 添加资产]**。

1. 要删除资产，请选中相应的复选框，然后选择&#x200B;**[!UICONTROL 删除资产]**。
1. 要应用预设，请选择右上角的&#x200B;**[!UICONTROL 预设]** ，然后选择要应用于资产的预设。
1. 选择&#x200B;**[!UICONTROL 保存]**。您新创建的混合媒体集会显示在创建时所用的文件夹中。

## 编辑混合媒体集 {#editing-mixed-media-sets}

您可以像在Assets](/help/assets/manage-assets.md)中对任意资产执行操作一样，直接在用户界面[中对混合媒体集中的资产执行各种编辑任务。 您还可以在混合媒体集中执行下列操作：

* 将资产添加到混合媒体集。
* 对混合媒体集中的资产重新排序。
* 删除混合媒体集中的资产。
* 应用查看器预设。
* 更改默认缩略图。

**要编辑混合媒体集，请执行以下操作：**

1. 执行以下任一操作：

   * 将鼠标悬停在混合媒体集资产上，然后选择&#x200B;**[!UICONTROL 编辑]**（铅笔图标）。
   * 将鼠标悬停在混合媒体集资产上，选择&#x200B;**[!UICONTROL 选择]**（复选标记图标），然后选择工具栏上的&#x200B;**[!UICONTROL 编辑]**。

   * 选择混合媒体集资产，然后选择工具栏上的&#x200B;**[!UICONTROL 编辑]**（铅笔图标）。

1. 在混合媒体集编辑器中，执行以下任一操作：

   * 要对资产重新排序 — 在左侧面板中，选择&#x200B;**[!UICONTROL Assets]**（图片图标），将资产拖动到新位置。
   * 要添加资产 — 在工具栏中，选择&#x200B;**[!UICONTROL 添加资产]**。 导航到资产。 对于要添加的每个资产，将鼠标悬停在资产的图像（而非资产名称）上，然后选择复选标记图标。 在右上角，选择&#x200B;**[!UICONTROL 选择]**。

   * 要删除资产 — 在左侧面板中，选择&#x200B;**[!UICONTROL 资产]**（图片图标），然后选择资产。 在工具栏中，选择&#x200B;**[!UICONTROL 删除资产]**。

   * 要按资产名称的升序或降序排序，请在左侧面板中选择&#x200B;**[!UICONTROL Assets]**（图片图标）。 在&#x200B;**[!UICONTROL Assets]**&#x200B;标题的右侧，选择向上或向下尖角图标。

      >[!NOTE]
      >
      >* 要删除整个混合媒体集，请从任何查看模式（如&#x200B;**[!UICONTROL 卡片视图]**&#x200B;或&#x200B;**[!UICONTROL 列视图]**）导航到混合媒体集。 将鼠标悬停在资产上，然后选择复选标记图标，以便您选择它。 按键盘上的&#x200B;**[!UICONTROL Backspace]**，或选择工具栏上的&#x200B;**[!UICONTROL 更多]**（三个圆点），然后选择&#x200B;**[!UICONTROL Delete]**。
         >
         >
      * 您可以导航到混合媒体集，然后单击左边栏中的&#x200B;**[!UICONTROL 设置成员]**，以编辑混合媒体集中的资产。 选择单个资产上的&#x200B;**[!UICONTROL Pencil]**&#x200B;图标，以便在编辑窗口中将其打开。


1. 完成编辑后，选择&#x200B;**[!UICONTROL Save]**。

   >[!NOTE]
   >
   >* 要编辑混合媒体集中的资产 — 请导航到混合媒体集。 点按（不选择）该集，以便该集在“Experience Manager集预览”页面中打开。 在左边栏中，选择向下尖角以打开下拉列表，然后选择&#x200B;**[!UICONTROL 设置成员]**。 在“设置成员”页面中，将鼠标悬停在资产上，然后选择&#x200B;**[!UICONTROL 编辑]**（铅笔图标）以打开编辑页面。
      >
      >
   * 要删除整个混合媒体集 — 从任何查看模式（如“卡片”视图或“列”视图）中，导航到混合媒体集。 将鼠标悬停在集上，然后选择&#x200B;**选择**（复选标记图标）。 在键盘上按&#x200B;**[!UICONTROL Backspace]**，或选择&#x200B;**[!UICONTROL 更多]**（三个圆点的行），然后选择&#x200B;**[!UICONTROL Delete]**。


## 预览混合媒体集 {#previewing-mixed-media-sets}

有关如何预览混合媒体集的详细信息，请参阅[预览资产](/help/assets/previewing-assets.md)。

## 发布混合媒体集 {#publishing-mixed-media-sets}

有关如何发布混合媒体集的详细信息，请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

>[!NOTE]
>
>如果混合媒体集在您首次发布时未完全在投放服务中结束，请第二次发布混合媒体集。
