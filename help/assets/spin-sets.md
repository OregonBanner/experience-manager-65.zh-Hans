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
translation-type: tm+mt
source-git-commit: 74f259d579bcf8d7a9198f93ef667288787a4493
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 32%

---


# 旋转集{#spin-sets}

旋转集模拟旋转对象的真实动作，以便于进行检查。通过旋转集，可以从任意角度查看项目，从而获取任意角度的重要可视细节。

旋转集模拟 360 度全方位查看体验。Dynamic Media 提供单轴旋转集，查看者可在该旋转集中旋转项目。另外，用户可以自由缩放和平移任何视图，只需几次简单的鼠标单击操作即可实现。这样，用户就可以从任何特定视角更仔细地检查项目。

Spin Sets are designated by a banner with the word **[!UICONTROL SPINSET.]** In addition, if the Spin Set is published, then the publish date, indicated by the **[!UICONTROL World]** icon is on the banner along with the last modification date, indicated by the **[!UICONTROL Pencil]** icon displays.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>有关资产用户界面的信息，请参 [阅使用触屏UI管理资产](/help/assets/managing-assets-touch-ui.md)。

## 快速开始:旋转集 {#quick-start-spin-sets}

要快速设置并运行旋转集，请执行以下步骤：

1. [上传多个视图的图像。](#uploading-assets-for-spin-sets)

   对于一维旋转集，一个项目至少需要8-12张照片；对于二维旋转集，一个项目至少需要16-24张照片。拍摄时必须定期进行，以给人以项目正在旋转和翻动的印象。例如，如果一维旋转集包含12个镜头，则对每个镜头将项目旋转30度(360/12)。

1. [创建旋转集。](#creating-spin-sets)

   To create a Spin Set, select **[!UICONTROL Create > Spin Set]** and then name the set, choose the assets, and choose the order the images appear.

   See [Working with Selectors](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >您还可以通过[批量集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建旋转集。**重要：** 批集由IPS（图像生产系统）创建，作为资产摄取的一部分，并且仅在Dynamic Media -Scene7模式下可用。

1. 根据需要设置[旋转集查看器预设](/help/assets/managing-viewer-presets.md)。

   管理员可以创建或修改旋转集查看器预设。要查看带有查看器预设的旋转集，请选择旋转集，然后在左边栏下拉菜单中，选择&#x200B;**查看器**。

   See **[!UICONTROL Tools > Assets > Viewer Presets]** to create or edit viewer presets.

   See [Adding and editing viewer presets.](/help/assets/managing-viewer-presets.md)

1. [查看旋转集](#viewing-spin-sets)。

   您可以通过三种不同的方式视图和访问通过批集预设创建的集。 (使用批集预设创建的集 *合* ，不显示在用户界面中。)

1. [预览旋转集。](/help/assets/previewing-assets.md)

   选择旋转集，之后您便可以进行预览。旋转该旋转集。您可以从左边栏下拉菜 **[!UICONTROL 单的]** “查看器”菜单中选择不同的查看器。

1. [发布旋转集。](/help/assets/publishing-dynamicmedia-assets.md)

   发布旋转集时，将会激活 URL 和嵌入字符串。此外，您必须发 [布查看器预设](/help/assets/managing-viewer-presets.md)。

1. [将URL关联到Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md) , [或嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

   在发布旋转集后，AEM 资产会为该旋转集创建 URL 调用并将其激活。预览资产时，您可以复制这些 URL。或者，您也可以将这些 URL 嵌入到网站中。

   Select the Spin Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers.]**

   请参 [阅将旋转集关联到网页](/help/assets/linking-urls-to-yourwebapplication.md)[和嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。

If you need to, you can [edit Spin Sets](#editing-spin-sets). In addition, you can view and modify [Spin Set properties](/help/assets/managing-assets-touch-ui.md#editing-properties).

## 上传旋转集的资产 {#uploading-assets-for-spin-sets}

对于一维旋转集，一个项目至少需要8-12张照片；对于二维旋转集，一个项目至少需要16-24张照片。拍摄时必须定期进行，以给人以项目正在旋转和翻动的印象。例如，如果一维旋转集包含12个镜头，则对每个镜头将项目旋转30度(360/12)。

You can upload images for the Spin Sets as you would [upload any other asset in AEM Assets](/help/assets/managing-assets-touch-ui.md).

### 为旋转集捕获图像的指南 {#guidelines-for-shooting-spin-set-images}

以下是关于旋转集图像的一些最佳实践。一般而言，旋转集中的图像越多，图像的旋转效果越好。但是，在旋转集中包含很多图像也会使加载图像所需的时间变长。在拍摄用于旋转集的图像时，AEM 建议遵循以下准则：

* 在一维旋转集中至少使用8-12幅图像，在二维旋转集中至少使用16-24幅图像。必须至少使用8张图像才能进行360度旋转。一维旋转集比较常见，因为创建二维旋转集非常繁琐。
* 使用无损格式；建议使用 TIFF 和 PNG。
* 对所有图像使用蒙版，以使项目显示在纯白或其他高对比度的背景中。或者，也可以添加阴影。
* 确保充分突出产品细节，使其成为焦点。
* 拍摄时装的旋转图像时，使用模特道具或真人模特。通常，模特道具会完全遮罩住（使用玻璃材质的模特道具），或者图像中会显示风格化的模特道具/人体模型。您可以通过定义多个角度来创建真人模特展示旋转集。可使用卷尺在地面上标出各个角度，以指导模特行走并目视每个拍摄方向。

## 创建旋转集 {#creating-spin-sets}

本节介绍如何在AEM中创建旋转集。

>[!NOTE]
>
>您还可以通过[批量集预设](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)自动创建旋转集。**重要：** 批集由IPS（图像生产系统）创建，作为资产摄取的一部分，并且仅在Dynamic Media -Scene7模式下可用。
>
>请参阅配置Dynamic Media -Scene7模式中的“创建批集预设以自动生成图 [像集和旋转集”](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。


>[!NOTE]
>
>旋转集中的图像显示顺序很重要。请务必对它们进行排序，使旋转保持360度的平滑视图。

**创建旋转集**

1. 在 Assets 中，导航到要创建旋转集的位置，单击&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 旋转集。]**&#x200B;您还可以从包含资产的文件夹中创建旋转集。此时将显示旋转集编辑器。

   ![6_5_spinset_createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. 在旋转集编辑器的标题 **[!UICONTROL 字段中]** ，输入旋转集的名称。 该名称会显示在旋转集的横幅中。（可选）输入说明。

   ![6_5_spinset_spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >创建旋转集时，您可以更改旋转集缩略图，或允许AEM根据旋转集中的资产自动选择缩略图。 To select a thumbnail, click **[!UICONTROL Change thumbnail]** and select any image (you can navigate to other folders to find images as well). If you have selected a thumbnail and then decide that you want AEM to generate one from the spin set, select **[!UICONTROL Switch to Automatic thumbnail.]**

1. 执行以下操作之一：

   * 在“旋转集编辑器”页面的左上角附近，点按添 **[!UICONTROL 加资产。]**

   * 在“旋转集编辑器”页面的中间附近，点按 **[!UICONTROL 以打开资产选择器。]**
   点按以选择要包含在旋转集中的资产。 选定资产上有一个复选标记图标。When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Select.]**

   借助资产选择器，您可以通过键入关键字并点按&#x200B;**[!UICONTROL 返回]**&#x200B;来搜索资产。您还可以应用过滤器来优化搜索结果。您可以按路径、收藏集、文件类型和标记进行过滤。选择过滤器，然后点按工具栏上的&#x200B;**[!UICONTROL 过滤器]**&#x200B;图标。Change the view by tapping the View icon and selecting **[!UICONTROL Column View]**, **[!UICONTROL Card View]**, or **[!UICONTROL List View.]**

   See [Working with Selectors](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 将资产添加到资产集时，资产会按字母数字顺序自动添加。 在添加资产后，您可以手动对资产重新排序或排序。

   如有必要，请将资产的重新排序图标拖动到资产文件名的右侧，以在设置的列表中向上或向下对图像重新排序。

   ![通过将旋转集中的第11帧拖动到新位置，重新排序该帧。](assets/6_5_spinset-reorderassets.png)

   通过将旋转集中的第11帧拖动到新位置，重新排序该帧。

1. （可选）执行以下操作之一：

   * 要删除图像，请选择该图像，然后点按删 **[!UICONTROL 除资产。]**

   * To apply a preset, near the upper-right corner of the page, tap **[!UICONTROL Preset]**, then select a preset to apply to all the assets at once.

1. Click **[!UICONTROL Save.]** Your newly created Spin Set appears in the folder you created it in.

## 查看旋转集 {#viewing-spin-sets}

您可以在用户界面中创建旋转集，也可以使用批 [集预设自动创建](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)。 但是，使用批集预设创建的集 *不会* 显示在用户界面中。 您可以通过三种不同方式访问通过批集预设创建的集。 （即使您在用户界面中创建了旋转集，这些方法也可用）。

>[!NOTE]
>
>您还可以通过用户界面视图集，如编辑旋转 [集中所述](#editing-spin-sets)。

**视图旋转集**

1. 打开单个资产的属性时。 属性指明所选资产是其成员(在“集 **[!UICONTROL 成员”下]**)。 单击集合的名称可查看整个集合。

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. 来自任何集的成员图像。Select the **[!UICONTROL Sets]** menu to display the sets that the asset is a member of.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. From search, you can Select **[!UICONTROL Filters]**, then expand **[!UICONTROL Dynamic Media]** and select **[!UICONTROL Sets.]**

   搜索会返回在UI中手动创建或通过批集预设自动创建的匹配集。 对于自动集，搜索查询使用与AEM搜索 `Starts with` 不同的搜索条件进行，后者基于使用搜索 `Contains` 条件进行。 将过滤器设 **[!UICONTROL 置为]** “集”是搜索自动集的唯一方法。

   ![chlimage_1-158](assets/chlimage_1-386.png)

## 编辑旋转集 {#editing-spin-sets}

您可以对旋转集执行各种编辑任务，如：

* 向旋转集中添加图像。
* 对旋转集中的图像进行重新排序。
* 删除旋转集中的资产。
* 应用查看器预设。
* 删除旋转集。

**编辑旋转集**

1. 执行下列任一操作：

   * 将鼠标悬停在旋转集资产上，然后点按 **[!UICONTROL 编辑]** （铅笔图标）。
   * 将鼠标悬停在旋转集资产上，点按 **[!UICONTROL 选择]** （复选标记图标），然后点按工 **[!UICONTROL 具栏]** 上的编辑。

   * 点按旋转集资产，然后点按工 **[!UICONTROL 具栏]** 上的编辑（铅笔图标）。

1. 要编辑旋转集，请执行以下任意操作：

   * 要对图像重新排序，请将图像拖到新位置（选择重新排序图标以移动项目）。
   * 要按升序或降序对项目排序，请单击列标题。
   * To add an asset or update an existing asset, click **[!UICONTROL Add Asset.]** 导航到资产，选择它，然 **[!UICONTROL 后点]** 按右上角附近的选择。
如果通过将缩略图替换为其他图像来删除AEM用的缩略图图像，则仍会显示原始资产。
   * 要删除资产，请选择该资产，然后单击或点按删 **[!UICONTROL 除资产。]**
   * 要应用预设，请点按或单击预设图标，然后选择预设。
   * To delete an entire Spin Set, navigate to the Spin Set, select it, and select **[!UICONTROL Delete]**

   >[!NOTE]
   >
   >You can edit the images in a Spin Set by navigating to the set, tap **[!UICONTROL Set Members]** in the left rail, and then tap the Pencil icon on an individual asset to open the editing window.

1. 完成编辑后，单击&#x200B;**[!UICONTROL 保存]**。

## 预览旋转集 {#previewing-spin-sets}

See [Previewing Assets](/help/assets/previewing-assets.md).

## 发布旋转集 {#publishing-spin-sets}

请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。
