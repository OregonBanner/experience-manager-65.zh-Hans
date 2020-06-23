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
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 38%

---


# 混合媒体集{#mixed-media-sets}

通过混合媒体集，您可以在一个演示文稿中提供图像、图像集、旋转集和视频的混合。

混合媒体集由带有MixedMediaSet字样的横幅 **[!UICONTROL 指定。]**&#x200B;此外，如果混合媒体集已发布，则横幅上会显示发布日期(由 **[!UICONTROL World]** 图标指示)以及上次修改日期(由 **** Pencil图标指示)。

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>有关资产用户界面的信息，请参 [阅使用触屏UI管理资产](/help/assets/managing-assets-touch-ui.md)。

## 快速入门：混合媒体集 {#quick-start-mixed-media-sets}

要快速设置并运行混合媒体集，请执行以下步骤：

1. [上传资产](#uploading-assets)。

   首先为混合媒体集上传图像和视频。 如有必要，请创 [建图像集](/help/assets/image-sets.md)[和旋转集](/help/assets/spin-sets.md)。 由于用户可以在混合媒体集查看器中缩放图像，因此在选择图像时，请考虑缩放因素。 确保图像的最大尺寸至少为2000像素。

1. [创建混合媒体集。](#creating-mixed-media-sets)

   要创建混合媒体集，请从“资产”页面中，点按创建 **[!UICONTROL >混合媒体集]** ，然后命名该集，选择资产，然后选择图像的显示顺序。

   See [Working with Selectors.](/help/assets/working-with-selectors.md)

1. Set up [Mixed Media Viewer presets](/help/assets/managing-viewer-presets.md), as needed.

   管理员可以创建或修改混合媒体集查看器预设。To see your mixed media with a viewer preset, select the mixed media set, and in the left-rail drop-down menu, select **[!UICONTROL Viewers.]**

   See **[!UICONTROL Tools > Assets > Viewer Presets]** to create or edit viewer presets.

   See [Adding and editing viewer presets.](/help/assets/managing-viewer-presets.md)

1. [预览混合媒体集。](#previewing-mixed-media-sets)

   选择混合媒体集，之后您便可以进行预览。单击缩略图图标可在选定的查看器中检查混合媒体集。您可以从左边栏下拉菜 **[!UICONTROL 单的]** “查看器”菜单中选择不同的查看器。

1. [发布混合媒体集。](#publishing-mixed-media-sets)

   发布混合媒体集时，将会激活 URL 和嵌入字符串。此外，您必须发 [布查看器预设](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)。

1. [将URL关联到Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md) , [或嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

   在发布混合媒体集后，AEM 资产会为该混合媒体集创建 URL 调用并将其激活。预览资产时，您可以复制这些 URL。或者，您也可以将这些 URL 嵌入到网站中。

   Select the Mixed Media Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers.]**

   请参 [阅将混合媒体集关联到网页](/help/assets/linking-urls-to-yourwebapplication.md)[和嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

If you need to, you can edit [Mixed Media Sets](#editing-mixed-media-sets). In addition, you can view and modify [Mixed Media Set properties](/help/assets/managing-assets-touch-ui.md#editing-properties).

>[!NOTE]
>
>如果您在创建集时遇到问题，请参 [阅疑难解答Dynamic Media- Scene7模式](/help/assets/troubleshoot-dms7.md)。

## 上传资产 {#uploading-assets}

首先为混合媒体集上传图像和视频。 由于用户可以在混合媒体集查看器中缩放图像，因此在选择图像时，请务必考虑缩放因素。 确保图像的最大尺寸至少为2000像素。

此外，如果您要向混合媒体集添加旋转集或图像集，也可创建这些集合。

## 创建混合媒体集 {#creating-mixed-media-sets}

您可以向混合媒体集添加图像、图像集、旋转集和视频。 在将您的文件、图像集和旋转集添加到混合媒体集之前，请确保您已准备好发布它们。

将资产添加到资产集时，资产会按字母数字顺序自动添加。 在添加资产后，您可以手动对资产重新排序或排序。

**创建混合媒体集**

1. 在 Assets 中，导航到要创建混合媒体集的位置，单击&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 混合媒体集。]**&#x200B;您还可以从包含资产的文件夹中创建旋转集。此时将显示混合媒体集编辑器。

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. In the Mixed Media Set Editor, in **[!UICONTROL Title]**, enter a name for the Mixed Media Set. 该名称会显示在混合媒体集的横幅中。（可选）输入说明。

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >创建混合媒体集时，您可以更改混合媒体集缩略图，或允许AEM根据混合媒体集中的资产自动选择缩略图。 To select a thumbnail, click **[!UICONTROL Change thumbnail]** and select any image (you can navigate to other folders to find images as well). If you have selected a thumbnail and then decide that you want AEM to generate one from the mixed media set, select **[!UICONTROL Switch to Automatic thumbnail.]**

1. 点按资产选择器，以选择要包含在混合媒体集中的资产。 Select them and click **[!UICONTROL Select.]**

   借助资产选择器，您可以通过键入关键字并点按&#x200B;**[!UICONTROL 返回来搜索资产。]**&#x200B;您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后点按工具栏中的&#x200B;**[!UICONTROL 过滤器]**&#x200B;图标。Change the view by selecting the **[!UICONTROL View]** icon and selecting **[!UICONTROL List View]**, **[!UICONTROL Column View]**, or **[!UICONTROL Card View.]**

   See [Working with Selectors](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Re-order the assets by dragging them up or down the list (must select the **[!UICONTROL Reorder]** icon), as necessary.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   如果要添加缩略图，请单击图像旁边的 **+** **[!UICONTROL 缩略图]**，然后导航到所需的缩略图。When done selecting all the thumbnail images click **[!UICONTROL Save.]**

   >[!NOTE]
   >
   >如果您要添加资产，请点按添 **[!UICONTROL 加资产。]**

1. To delete an asset, select the corresponding check box and tap **[!UICONTROL Delete Asset.]**
1. 要应用预设，请点 **[!UICONTROL 按右]** 上角的预设，然后选择要应用到资产的预设。
1. Click **[!UICONTROL Save.]** Your newly created Mixed Media Set appears in the folder you created it in.

## 编辑混合媒体集 {#editing-mixed-media-sets}

You can perform a variety of editing tasks to assets in Mixed Media Sets directly in the user interface [as you would any asset in Assets](/help/assets/managing-assets-touch-ui.md). 您还可以在混合媒体集中执行下列操作：

* 将资产添加到混合媒体集。
* 对混合媒体集中的资产重新排序。
* 删除混合媒体集中的资产。
* 应用查看器预设。
* 更改默认缩略图。

**编辑混合媒体集**

1. 执行下列任一操作：

   * 将鼠标悬停在混合媒体集资产上，然后点 **[!UICONTROL 按编]** 辑（铅笔图标）。
   * 将鼠标悬停在混合媒体集资产上，点按 **[!UICONTROL 选择]** （复选标记图标），然后点 **[!UICONTROL 按工具栏]** 上的编辑。

   * 点按混合媒体集资产，然后点按工 **[!UICONTROL 具栏]** 上的编辑（铅笔图标）。

1. 在混合媒体集编辑器中，执行下列任一操作：

   * 要重新排序资产——在左面板中，点 **[!UICONTROL 按资产]** （图片图标），将资产拖动到新位置。
   * 要添加资产——请点按工具栏中的添 **[!UICONTROL 加资产。]** 导航到资产。 对于要添加的每个资产，将鼠标悬停在资产的图像（而非资产名称）上，然后点按复选标记图标。 在右上角，点按选 **[!UICONTROL 择。]**

   * 要删除资产——在左侧面板中，点按 **[!UICONTROL 资产]** （图片图标），然后选择资产。 在工具栏栏中，点按删 **[!UICONTROL 除资产。]**

   * 要按资产名称的升序或降序排序，请在左侧面板中点按 **[!UICONTROL 资产]** （图片图标）。 在“资产”标题 **[!UICONTROL 的右侧]** ，点按向上或向下插入符号图标。

      >[!NOTE]
      >
      >    * To delete an entire Mixed Media Set, from any viewing mode (such as **[!UICONTROL Card View]** or **[!UICONTROL Column View]**) navigate to the Mixed Media Set. 将鼠标悬停在资产上，然后点按复选标记图标以将其选中。 Press **[!UICONTROL Backspace]** on the keyboard, or click **[!UICONTROL More]** (three dots) on the toolbar, then tap **[!UICONTROL Delete.]**
         >
         >    
      * You can edit the assets in a Mixed Media Set by navigating to the set, clicking **Set Members]** in the left rail, and then tapping the **[!UICONTROL Pencil]** icon on an individual asset to open the editing window.


1. 完成 **[!UICONTROL 编辑]** 后，点按保存。

   >[!NOTE]
   >
   >* 要编辑混合媒体集中的资产，请导航到混合媒体集。 点按（不选择）该集，以在“AEM 集预览”页面中将其打开。In the left rail, click the down caret to open the drop-down list, then tap **[!UICONTROL Set Members.]** 在“设置成员”页面中，将指针悬停在资产上，然 **[!UICONTROL 后点]** 按编辑（铅笔图标）以打开编辑页面。
      >
      >
   * 要删除整个混合媒体集——在任何查看模式(如卡片视图或列视图)中，导航到混合媒体集。 Hover on the set, then tap **Select]** (checkmark icon). Press **[!UICONTROL Backspace]** on your keyboard, or tap **[!UICONTROL More]** (row of three dots), then tap **[!UICONTROL Delete.]**


## 预览混合媒体集 {#previewing-mixed-media-sets}

有关如何预览混合媒体集的详细信息，请参阅[预览资产](/help/assets/previewing-assets.md)。

## 发布混合媒体集 {#publishing-mixed-media-sets}

有关如何发布混合媒体集的详细信息，请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

>[!NOTE]
>
>如果您第一次发布混合媒体集时，未全部完成传送服务，则您可能需要再次发布该混合媒体集。

