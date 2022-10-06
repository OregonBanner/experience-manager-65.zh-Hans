---
title: 资产模板
description: 了解 [!DNL Adobe Experience Manager Assets] 以及如何使用资产模板创建营销宣传资料。
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# 资产模板 {#asset-templates}

资产模板是一种特殊的资产类别，有助于快速重新利用数字和打印媒体中视觉上丰富的内容。 资产模板包括固定消息传送部分和可编辑部分两部分。 固定消息部分可以包含专有内容，如品牌徽标和禁用进行编辑的版权信息。 可编辑的部分可以在字段中包含可视内容和文本内容，这些内容可以编辑以自定义消息传送。

在保护全局标牌的同时，灵活地进行有限的编辑，这使得资产模板成为快速调整内容和将内容分发为各种功能的内容对象的理想构建块。 重新调整内容用途有助于降低管理打印和数字渠道的成本，并在这些渠道中提供整体一致的体验。

作为营销人员，您可以在 [!DNL Experience Manager Assets] 并使用单个基本模板轻松创建多个个性化的打印体验。 您可以创建各种类型的营销宣传资料，包括小册子、传单、明信片、名片等，以便向客户清晰地传达您的营销信息。 您还可以从现有或新打印输出组合多页打印输出。 最重要的是，您可以轻松地同时提供数字和打印体验，从而为用户提供一致的集成体验。

虽然资产模板大多 [!DNL Adobe InDesign] 文件，熟练程度 [!DNL Adobe InDesign] 并不是创造恒星伪像的障碍。 您无需映射 [!DNL Adobe InDesign] 模板，以及在创建目录时需要使用的产品字段。 您可以直接在Web界面上以WYSIWYG模式编辑模板。 但是，对于 [!DNL Adobe InDesign] 要处理编辑更改，您必须首先配置 [!DNL Experience Manager Assets] 与集成 [!DNL Adobe InDesign Server].

能够编辑 [!DNL Adobe InDesign] web界面中的模板有助于促进创意人员与营销人员之间的更大协作。 内容速度的提高缩短了营销抵押品的上市时间。

通过资产模板，您可以实现以下目标：

* 从Web界面修改可编辑的模板字段。
* 控制文本的基本样式，例如，字体大小、样式和标记级别的类型。
* 使用内容选取器更改模板中的图像。
* 预览模板编辑。
* 合并多个模板文件以创建多页对象。

当您为抵押品选择模板时， [!DNL Experience Manager Assets] 创建可编辑的模板副本。 原始模板将保留，以确保全局标牌保持不变，并可重复使用以强制保持品牌一致性。

您可以采用INDD、PDF或JPG格式，将更新的文件导出到父文件夹中。 您也可以将这些格式的输出下载到本地文件系统。

## 创建宣传资料 {#creating-a-collateral}

假设您想要创建数字可打印宣传资料（如宣传册、传单和广告等），以便在即将开展的活动中进行宣传，并与全球直销店共享。 根据模板创建宣传资料有助于跨渠道提供统一的客户体验。 设计人员可以使用创意解决方案(例如， [!DNL InDesign] 并将模板上传到 [!DNL Experience Manager Assets] 为你。 在创建宣传资料之前，请在 [!DNL Experience Manager] 提前。

1. 在 [!DNL Experience Manager] 界面点击 [!UICONTROL 资产].

1. 从选项中，选择 **[!UICONTROL 模板]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 单击 **[!UICONTROL 创建]**，然后从菜单中选择要创建的宣传资料。 例如，选择 **[!UICONTROL 手册]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 已将一个或多个INDD模板上传到，并在 [!DNL Experience Manager] 提前。 为您的手册选择模板，然后单击 **[!UICONTROL 下一个]**.
1. 为手册指定名称和可选描述。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （可选）单击 **[!UICONTROL 标记]** 并为手册选择一个或多个标签。 单击 **[!UICONTROL 确认]** 以确认您的选择。
1. 单击&#x200B;**[!UICONTROL 创建]**。对话框确认创建了新手册。 单击 **[!UICONTROL 打开]** 以编辑模式打开手册。

   <!--![chlimage_1-106](assets/.png) -->

   或者，关闭对话框，然后导航到您开始使用的“模板”页面中的文件夹，以查看您创建的手册。 在卡片视图中，宣传品的类型显示在其缩略图上。 例如，在本例中， [!UICONTROL 手册] 显示在缩略图上。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 编辑宣传资料 {#editing-a-collateral}

您可以在创建宣传资料后立即对其进行编辑。 或者，您也可以从 [!UICONTROL 模板] 页面或资产页面。

1. 要打开宣传资料进行编辑，请执行以下操作之一：

   * 打开您在的步骤7中创建的宣传资料（在本例中为手册） [创建宣传资料](/help/assets/asset-templates.md#creating-a-collateral).
   * 在“模板”页面中，导航到创建宣传品的文件夹，然后单击 [!UICONTROL 编辑] 对宣传资料的缩略图快速执行操作。
   * 在抵押品的资产页面中，单击 **[!UICONTROL 编辑]** 中。
   * 选择宣传品并单击 **[!UICONTROL 编辑]** 中。

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   资产查找器和文本编辑器显示在页面左侧。 默认情况下，会打开文本编辑器。

   您可以使用文本编辑器修改要在文本字段中显示的文本。 您可以在标记级别修改字体大小、样式、颜色和类型。

   使用资产查找器，您可以在 [!DNL Experience Manager Assets] 并将模板中可编辑的图像替换为您选择的图像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可编辑内容将显示在右侧。 要在 [!DNL Experience Manager Assets]，模板中的相应字段必须在 [!DNL InDesign]. 换言之，应在 [!DNL InDesign].

   >[!NOTE]
   >
   >确保 [!DNL Experience Manager] 部署与 [!DNL InDesign Server] 启用 [!DNL Experience Manager Assets] 从提取数据 [!DNL InDesign] 模板，并使其可供编辑。 有关详细信息，请参阅 [将Experience Manager Assets与InDesign Server集成](/help/assets/indesign.md).

1. 要修改可编辑字段中的文本，请单击可编辑字段列表中的文本字段，然后编辑该字段中的文本。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以使用提供的选项编辑文本属性，例如字体样式、颜色和大小。

1. 单击 **[!UICONTROL 预览]** 以预览文本更改。

1. 要交换图像，请单击 **[!UICONTROL 资产查找器]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. 从可编辑字段列表中选择图像字段，然后将所需图像从资产选取器拖到可编辑的字段。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您还可以使用关键词、标记并根据图像的发布状态来搜索图像。 您可以浏览 [!DNL Experience Manager Assets] 存储库，然后导航到所需图像的位置。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 单击 **[!UICONTROL 预览]** 来预览图像。
1. 要编辑多页宣传资料中的特定页面，请使用底部的页面导航器。

1. 单击 **[!UICONTROL 预览]** ，以预览所有更改。 单击 **[!UICONTROL 完成]** 以保存对辅助资料的编辑更改。

   >[!NOTE]
   >
   >只有在宣传品中可编辑的图像字段没有任何缺失的图标时，才会启用“预览”和“完成”选项。 如果宣传品中缺少图标，那是因为 [!DNL Experience Manager] 无法解析 [!DNL InDesign] 模板。 通常， [!DNL Experience Manager] 在以下情况下无法解析图像：
   >
   >* 图像未嵌入到底层 [!DNL InDesign] 模板。
   >* 图像从本地文件系统链接。

   >
   >启用 [!DNL Experience Manager] 要解析图像，请执行以下操作：
   >
   >* 创建时嵌入图像 [!DNL InDesign] 模板(请参阅 [关于链接和嵌入式图形](https://helpx.adobe.com/indesign/using/graphics-links.html))。
   >* 装载 [!DNL Experience Manager] 映射到您的本地文件系统，然后使用 [!DNL Experience Manager].

   >
   >有关使用的更多信息 [!DNL InDesign] 文档，请参阅 [在Experience Manager中处理InDesign文档的最佳实践](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. 要为手册生成PDF呈现，请在对话框中选择Acrobat选项，然后单击 **[!UICONTROL 继续]**.
1. 辅助资料会在您开始使用的文件夹中创建。 要查看演绎版，请打开宣传品并选择 **[!UICONTROL 演绎版]** GlobalNav列表中。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 从演绎版列表中单击PDF演绎版，以下载PDF文件。 打开PDF文件以审核宣传资料。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合并抵押品 {#merge-collateral}

1. 在 [!DNL Experience Manager] 界面点击 [!UICONTROL 资产] 中。

1. 从选项中，选择 **[!UICONTROL 模板]**.

1. 单击 **[!UICONTROL 创建]** 选择 **[!UICONTROL 合并]** 中。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 从 [!UICONTROL 模板合并] 页面，单击 **[!UICONTROL 合并]** ![添加资产](assets/do-not-localize/assets_add_icon.png).

1. 导航到要合并的宣传品所在的位置，单击要合并的宣传品缩略图以选择它们。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您还可以从Omnisearch框中搜索模板。

   您可以浏览 [!DNL Experience Manager Assets] 存储库或收藏集，然后导航到所需模板的位置，然后选择要合并的模板。

   您可以应用各种过滤器来搜索所需的模板。 例如，您可以根据文件类型或标记搜索模板。

1. 单击 **[!UICONTROL 下一个]** 中。
1. 在 **[!UICONTROL 预览和重新排序]** ，根据需要重新排列模板并预览要合并的选定模板。 然后，单击 **[!UICONTROL 下一个]** 中。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在 [!UICONTROL 配置模板] 屏幕上，指定宣传品的名称。 （可选）指定您认为合适的任何标记。 如果要以PDF格式导出输出，请选择 **[!UICONTROL Acrobat(.PDF)]**. 默认情况下，抵押品会以JPG和 [!DNL InDesign] 格式。 要更改多页宣传资料的显示缩略图，请单击 **[!UICONTROL 更改缩略图]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 单击 **[!UICONTROL 保存]** 然后单击 **[!UICONTROL 确定]** 中，以关闭对话框。 多页宣传资料会在您开始使用的文件夹中创建。

   >[!NOTE]
   >
   >您以后无法编辑合并的宣传资料，也无法使用它创建其他宣传资料。

## 最佳实践和限制 {#best-practices-limitations-tips}

* 的 [!DNL InDesign] 编辑器 [!DNL Experience Manager] 在标记级别工作，并且单个标记下的所有文本都被视为单个实体。 要在编辑时保留文本格式和样式，请分别标记每个段落（或具有不同样式的文本）。
