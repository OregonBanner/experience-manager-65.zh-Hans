---
title: 资产模板
description: 在中了解资产模板 [!DNL Adobe Experience Manager Assets] 以及如何使用资产模板创建营销宣传材料。
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# 资产模板 {#asset-templates}

资产模板是一类特殊的资产，有助于快速将富含视觉效果的内容重新用于数字和印刷媒体。 资产模板包括固定消息传递部分和可编辑部分两部分。 固定消息部分可以包含专有内容，例如禁用编辑的品牌徽标和版权信息。 可编辑部分可在可编辑以自定义消息传递的字段中包含可视和文本内容。

在保护全局标牌的同时进行有限编辑的灵活性使资产模板成为快速内容调整和分发的理想构建块，可作为各种功能的内容构件。 重新调整内容用途有助于降低管理打印和数字渠道的成本，并在这些渠道中提供全面一致的体验。

作为营销人员，您可以在中存储和管理模板 [!DNL Experience Manager Assets] 并使用单个基本模板轻松创建多种个性化打印体验。 您可以创建各种类型的营销宣传资料，包括小册子、传单、明信片、名片等，以便向客户清楚地传达您的营销信息。 您还可以从现有或新的打印输出组合多页打印输出。 最重要的是，您可以轻松地同时提供数字和打印体验，从而为用户提供一致的集成体验。

虽然资产模板大部分 [!DNL Adobe InDesign] 文件，熟练掌握 [!DNL Adobe InDesign] 并不是制造星象的障碍。 您无需映射 [!DNL Adobe InDesign] 模板以及创建目录时所需的产品字段。 可直接在Web界面上以WYSIWYG模式编辑模板。 但是，对于 [!DNL Adobe InDesign] 要处理编辑更改，必须先配置 [!DNL Experience Manager Assets] 要与集成 [!DNL Adobe InDesign Server].

编辑功能 [!DNL Adobe InDesign] Web界面中的模板有助于促进创意和营销人员之间的进一步协作。 提高的内容速度缩短了营销抵押品的上市时间。

您可以使用资产模板实现以下目标：

* 从Web界面修改可编辑的模板字段。
* 控制文本的基本样式，例如，标签级别的字体大小、样式和文字。
* 使用内容选取器更改模板中的图像。
* 预览模板编辑。
* 合并多个模板文件以创建多页构件。

在为宣传材料选择模板时， [!DNL Experience Manager Assets] 创建可编辑的模板副本。 原始模板将被保留，这将确保您的全局标牌保持不变，并且可重复使用以强制实施品牌一致性。

可以在INDD、PDF或JPG格式的父文件夹中导出更新的文件。 您还可以将这些格式的输出下载到本地文件系统。

## 创建宣传品 {#creating-a-collateral}

考虑以下情景：您希望为即将到来的营销活动创建数字可打印的宣传资料，例如宣传册、传单和广告，并在全球范围内与折扣商店共享。 基于模板创建宣传材料有助于跨渠道提供统一的客户体验。 设计人员可以使用创意解决方案（例如）创建营销活动模板（单页或多页） [!DNL InDesign] 并将模板上传到 [!DNL Experience Manager Assets] 为了你。 在创建宣传材料之前，请上传一个或多个INDD模板并在中提供 [!DNL Experience Manager] 事前准备。

1. 在 [!DNL Experience Manager] 界面点击 [!UICONTROL 资产].

1. 从选项中，选择 **[!UICONTROL 模板]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 单击 **[!UICONTROL 创建]**，然后从菜单中选择您要创建的宣传品。 例如，选择 **[!UICONTROL 宣传册]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 上传一个或多个INDD模板并在中可用 [!DNL Experience Manager] 事前准备。 选择小册子的模板，然后单击 **[!UICONTROL 下一个]**.
1. 指定小册子的名称和可选描述。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （可选）单击 **[!UICONTROL 标记]** 并为宣传册选择一个或多个标记。 单击 **[!UICONTROL 确认]** 以确认您的选择。
1. 单击&#x200B;**[!UICONTROL 创建]**。将显示一个对话框，确认已创建新宣传册。 单击 **[!UICONTROL 打开]** 以在编辑模式下打开宣传册。

   <!--![chlimage_1-106](assets/.png) -->

   或者，关闭对话框并导航到开始使用的“模板”页面中的文件夹，以查看您创建的宣传册。 宣传品的类型将显示在卡片视图的缩略图上。 例如，在本例中， [!UICONTROL 宣传册] 在缩略图上显示。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 编辑宣传品 {#editing-a-collateral}

您可以在创建宣传品后立即对其进行编辑。 或者，您也可从 [!UICONTROL 模板] 页面或资产页面。

1. 要打开宣传资料进行编辑，请执行下列操作之一：

   * 打开您在步骤7中创建的宣传品（此例中为宣传册），共 [创建宣传品](/help/assets/asset-templates.md#creating-a-collateral).
   * 在“模板”页面中，导航至创建宣传品的文件夹，然后单击 [!UICONTROL 编辑] 宣传资料缩略图上的快速操作。
   * 在抵押资产的资产页面中，单击 **[!UICONTROL 编辑]** 工具栏中。
   * 选择宣传品，然后单击 **[!UICONTROL 编辑]** 工具栏中。

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   资产查找器和文本编辑器将显示在页面左侧。 默认情况下，文本编辑器处于打开状态。

   您可以使用文本编辑器修改要在文本字段中显示的文本。 您可以在标记级别修改字体大小、样式、颜色和文字。

   使用资源查找器，您可以浏览或搜索以下位置的图像： [!DNL Experience Manager Assets] 并将模板中的可编辑图像替换为您选择的图像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可编辑内容将显示在右侧。 对于在中可编辑的字段 [!DNL Experience Manager Assets]，模板中的相应字段必须标记为 [!DNL InDesign]. 换句话说，它们应该在中标记为可编辑 [!DNL InDesign].

   >[!NOTE]
   >
   >确保 [!DNL Experience Manager] 部署与集成 [!DNL InDesign Server] 以启用 [!DNL Experience Manager Assets] 以从提取数据 [!DNL InDesign] 模板并使其可用于编辑。 有关详细信息，请参阅 [将Experience Manager Assets与InDesign Server集成](/help/assets/indesign.md).

1. 要修改可编辑字段中的文本，请单击可编辑字段列表中的文本字段，然后编辑该字段中的文本。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以使用提供的选项编辑文本属性，例如字体样式、颜色和大小。

1. 单击 **[!UICONTROL 预览]** 以预览文本更改。

1. 要交换图像，请单击 **[!UICONTROL 资产查找器]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. 从可编辑字段列表中选择图像字段，然后将所需图像从资产选取器拖到可编辑字段中。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您还可以使用关键字、标记并根据其发布状态搜索图像。 您可以浏览 [!DNL Experience Manager Assets] 并导航到所需图像的位置。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 单击 **[!UICONTROL 预览]** 以预览图像。
1. 要编辑多页宣传资料中的特定页面，请使用底部的页面导航器。

1. 单击 **[!UICONTROL 预览]** 以预览所有更改。 单击 **[!UICONTROL 完成]** 以保存对宣传品的编辑更改。

   >[!NOTE]
   >
   >仅当宣传品中的可编辑图像字段没有任何缺少图标时，才会启用“预览”和“完成”选项。 如果您的宣传资料中缺少图标，原因如下 [!DNL Experience Manager] 无法解析 [!DNL InDesign] 模板。 通常， [!DNL Experience Manager] 在以下情况下无法解析图像：
   >
   >* 图像未嵌入在底层中 [!DNL InDesign] 模板。
   >* 从本地文件系统链接图像。
   >
   >要启用 [!DNL Experience Manager] 要解析图像，请执行以下操作：
   >
   >* 创建时嵌入图像 [!DNL InDesign] 模板(请参阅 [关于链接和嵌入式图形](https://helpx.adobe.com/indesign/using/graphics-links.html))。
   >* 装载 [!DNL Experience Manager] 到您的本地文件系统，然后将缺少的图标映射到中的现有资源 [!DNL Experience Manager].
   >
   >有关使用的更多信息 [!DNL InDesign] 文档，请参阅 [使用Experience Manager中的InDesign文档的最佳实践](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. 要为宣传册生成PDF演绎版，请选择对话框中的Acrobat选项，然后单击 **[!UICONTROL 继续]**.
1. 宣传品在您开始使用的文件夹中创建。 要查看格式副本，请打开宣传品并选择 **[!UICONTROL 节目]** 从GlobalNav列表中。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 单击格式副本列表中的PDF格式副本以下载PDF文件。 打开PDF文件以查看宣传品。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合并宣传品 {#merge-collateral}

1. 在 [!DNL Experience Manager] 界面点击 [!UICONTROL 资产] 在导航页面上。

1. 从选项中，选择 **[!UICONTROL 模板]**.

1. 单击 **[!UICONTROL 创建]** 和选择 **[!UICONTROL 合并]** 菜单。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 从 [!UICONTROL 模板合并] 页面，单击 **[!UICONTROL 合并]** ![添加资产](assets/do-not-localize/assets_add_icon.png).

1. 导航到要合并的宣传品的位置，单击要合并的宣传品的缩略图以选择它们。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您还可以从Omnisearch框中搜索模板。

   您可以浏览 [!DNL Experience Manager Assets] 存储库，并导航到所需模板的位置，然后选择要合并的模板。

   您可以应用各种筛选器来搜索所需的模板。 例如，您可以根据文件类型或标记搜索模板。

1. 单击 **[!UICONTROL 下一个]** 工具栏中。
1. 在 **[!UICONTROL 预览和重新排序]** 屏幕，根据需要重新排列模板并预览所选要合并的模板。 然后，单击 **[!UICONTROL 下一个]** 工具栏中。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在 [!UICONTROL 配置模板] 屏幕，指定宣传品的名称。 （可选）指定您认为合适的任何标记。 如果要以PDF格式导出输出，请选择 **[!UICONTROL Acrobat (.PDF)]**. 默认情况下，宣传品以JPG导出，并且 [!DNL InDesign] 格式。 要更改多页宣传品的显示缩略图，请单击 **[!UICONTROL 更改缩略图]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 单击 **[!UICONTROL 保存]** 然后单击 **[!UICONTROL 确定]** ，以关闭对话框。 多页宣传资料是在您开始使用的文件夹中创建的。

   >[!NOTE]
   >
   >您以后不能编辑合并的宣传品，也不能使用它来创建其他宣传品。

## 最佳实践和限制 {#best-practices-limitations-tips}

* 此 [!DNL InDesign] 编辑者 [!DNL Experience Manager] 在标记级别工作，单个标记下的所有文本被视为单个实体。 要在编辑时保留文本格式和样式，请单独标记每个段落（或使用不同样式的文本）。
