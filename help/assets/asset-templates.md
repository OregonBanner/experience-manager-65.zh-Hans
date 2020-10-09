---
title: 资产模板
description: 了解资产模板 [!DNL Adobe Experience Manager Assets] 以及如何使用资产模板创建营销宣传资料。
contentOwner: AG
translation-type: tm+mt
source-git-commit: f9f745369ba0fe242dea1e5a5e5af0b8263b1ec0
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---


# Asset templates {#asset-templates}

资产模板是一种特殊的资产类别，它有助于快速为数字和印刷媒体重用视觉效果丰富的内容。 资产模板包括两个部分，即固定消息部分和可编辑部分。 固定消息部分可以包含专有内容，如品牌徽标和禁用进行编辑的版权信息。 可编辑部分可在可编辑以自定义消息的字段中包含可视内容和文本内容。

在保护全球标牌的同时灵活地进行有限的编辑，使资产模板成为快速调整内容和分发内容的理想构件块，并将其作为各种功能的内容伪像。 重新调整内容用途有助于降低管理印刷和数字渠道的成本，并在这些渠道提供全面、一致的体验。

作为营销人员，您可以在内部存储和管理模板， [!DNL Experience Manager Assets] 并使用单个基本模板轻松创建多个个性化的印刷体验。 您可以创建各种类型的营销宣传资料，包括小册子、传单、明信片、名片等，以便向客户清晰地传达您的营销信息。 您还可以从现有或新的打印输出组合多页打印输出。 最重要的是，您可以轻松同时提供数字和印刷体验，为用户提供一致、集成的体验。

虽然资产模板大多 [!DNL Adobe InDesign] 是文件，但熟练 [!DNL Adobe InDesign] 使用并不妨碍创建明星人工物。 您无需将模板的字段与您 [!DNL Adobe InDesign] 的产品字段进行映射，否则，创建目录时需要这些字段。 您可以直接在Web界面上以WYSIWYG模式编辑模板。 但是，要 [!DNL Adobe InDesign] 处理编辑更改，您必须先配置 [!DNL Experience Manager Assets] 以与集成 [!DNL Adobe InDesign Server]。

从Web界面编辑模 [!DNL Adobe InDesign] 板的能力有助于促进创意人员与营销人员之间的更紧密协作。 内容速度的提高缩短了营销抵押品的上市时间。

通过资产模板，您可以实现以下目标：

* 从Web界面修改可编辑的模板字段。
* 控制文本的基本样式，例如字体大小、样式和标记级别的文字。
* 使用内容选取器更改模板中的图像。
* 预览模板编辑。
* 合并多个模板文件以创建多页对象。

为宣传品选择模板时， [!DNL Experience Manager Assets] 会创建可编辑的模板副本。 原始模板将保留，这可确保您的全球标牌保持不变，并可以重复使用，以实现品牌一致性。

可以以INDD、PDF或JPG格式导出父文件夹中的更新文件。 您还可以将这些格式的输出下载到本地文件系统。

## 创建宣传品 {#creating-a-collateral}

请考虑您希望为即将到来的活动制作数字可打印宣传品（如小册子、传单和广告）并与全球直销店共享的场景。 根据模板创建宣传资料有助于跨渠道提供统一的客户体验。 设计人员可以使用创意解决方案创建活动模板（单页或多页）, [!DNL InDesign] 然后为您上传 [!DNL Experience Manager Assets] 模板。 在创建宣传品之前，请事先将一个或多个INDD模板上传 [!DNL Experience Manager] 到并可用。

1. 在界 [!DNL Experience Manager] 面中，单击 [!UICONTROL 资产]。

1. 从选项中，选择“模 **[!UICONTROL 板”]**。

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 单击 **[!UICONTROL 创建]**，然后从菜单中选择要创建的宣传品。 例如，选择“ **[!UICONTROL 小册子]**”。

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 提前上传一个或多个INDD模 [!DNL Experience Manager] 板并可用。 为您的宣传册选择一个模板，然后单击“下 **[!UICONTROL 一步”]**。
1. 指定手册的名称和可选说明。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （可选）单击“ **[!UICONTROL 标记]** ”，然后为小册子选择一个或多个标记。 单击 **[!UICONTROL 确认]** ，以确认您的选择。
1. 单击&#x200B;**[!UICONTROL 创建]**。对话框会确认新手册的制作。 单击 **[!UICONTROL 打开]** ，以编辑模式打开宣传册。

   <!--![chlimage_1-106](assets/.png) -->

   或者，关闭对话框并导航到您开始使用的“模板”页面中的文件夹，以视图您创建的小册子。 附属品的类型显示在其缩略图上的卡片视图。 例如，在这种情况下，缩略图上 [!UICONTROL 会显] 示“手册”一词。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 编辑宣传资料 {#editing-a-collateral}

您可以在创建宣传品后立即对其进行编辑。 或者，也可以从模板页 [!UICONTROL 面或资] 产页面打开它。

1. 要打开要编辑的宣传品，请执行下列操作之一：

   * 打开您在创建宣传资料第7步中创建的宣传资料(本例中 [为宣传册)](/help/assets/asset-templates.md#creating-a-collateral)。
   * 在“模板”页面中，导航到您创建宣传品的文件夹，然后单击宣传 [!UICONTROL 品缩略图] 上的“编辑”快速操作。
   * 在宣传品的资产页面中，单击工 **[!UICONTROL 具栏]** 中的编辑。
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   资产查找器和文本编辑器显示在页面左侧。 默认情况下，文本编辑器处于打开状态。

   您可以使用文本编辑器修改要在文本字段中显示的文本。 您可以在标记级别修改字体大小、样式、颜色和文字。

   使用资产查找器，您可以浏览或搜索模板中的 [!DNL Experience Manager Assets] 图像，并将模板中的可编辑图像替换为您选择的图像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可编辑内容显示在右侧。 要在中编辑字段， [!DNL Experience Manager Assets]模板中的相应字段必须在中进行标记 [!DNL InDesign]。 换言之，它们应在中标为可编辑 [!DNL InDesign]。

   >[!NOTE]
   >
   >确保您的 [!DNL Experience Manager] 部署与集成， [!DNL InDesign Server] 以启用 [!DNL Experience Manager Assets] 从模板提取数据并 [!DNL InDesign] 使其可供编辑。 有关详细信息，请 [参阅将Experience Manager资产与InDesign Server集成](/help/assets/indesign.md)。

1. 要修改可编辑字段中的文本，请单击可编辑字段列表中的文本字段，然后编辑该字段中的文本。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以编辑文本属性，例如字体样式、颜色和大小，使用提供的选项。

1. 单击 **[!UICONTROL 预览]** ，以预览文本更改。

1. 要交换图像，请单 **[!UICONTROL 击资产]**![查找器chlimage_1-113](assets/chlimage_1-318.png)。

1. 从可编辑字段的列表中选择图像字段，然后将所需图像从资产选取器拖到可编辑字段。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您还可以使用关键字、标记并根据图像的发布状态搜索图像。 您可以浏览存储 [!DNL Experience Manager Assets] 库并导航到所需图像的位置。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 单击 **[!UICONTROL 预览]** ，以预览图像。
1. 要编辑多页宣传资料中的特定页面，请使用底部的页面导航器。

1. 单击 **[!UICONTROL 工具栏]** 上的预览，以预览所有更改。 单击 **[!UICONTROL 完成]** ，以保存对宣传资料的编辑更改。

   >[!NOTE]
   >
   >只有在宣传品中的可编辑图像字段没有任何缺失的图标时，预览和完成选项才会启用。 如果您的宣传品中缺少图标，则 [!DNL Experience Manager] 是因为无法解析模板中的 [!DNL InDesign] 图像。 通常， [!DNL Experience Manager] 在以下情况下无法解析图像：
   >
   >* 图像未嵌入到基础模 [!DNL InDesign] 板中。
   >* 图像从本地文件系统链接。

   >
   >要启用 [!DNL Experience Manager] 解析图像，请执行以下操作：
   >
   >* 在创建模板时嵌 [!DNL InDesign] 入图像(请 [参阅关于链接和嵌入图形](https://helpx.adobe.com/indesign/using/graphics-links.html))。
   >* 装载 [!DNL Experience Manager] 到本地文件系统，然后将缺少的图标与中的现有资源映射 [!DNL Experience Manager]。

   >
   >有关使用文档的更多信 [!DNL InDesign] 息，请参 [阅在Experience Manager中使用InDesign文档的最佳实践](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html)。

1. 要为手册生成PDF再现，请在对话框中选择“Acrobat”选项，然后单击“继 **[!UICONTROL 续”]**。
1. 附属品会在您开始使用的文件夹中创建。 要视图演绎版，请打开宣传品，然 **[!UICONTROL 后从]** GlobalNav列表中选择“演绎版”。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 从演绎版列表单击PDF演绎版以下载PDF文件。 打开PDF文件以查看宣传资料。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合并附属品 {#merge-collateral}

1. 在界面 [!DNL Experience Manager] 中，单 [!UICONTROL 击导] 航页面上的资产。

1. 从选项中，选择“模 **[!UICONTROL 板”]**。

1. 单击 **[!UICONTROL 创建]** ，然后从菜 **[!UICONTROL 单中选]** 择“合并”。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 在“模 [!UICONTROL 板合并] ”页面中，单 **[!UICONTROL 击合]** 并 ![](assets/do-not-localize/assets_add_icon.png)添加资产。

1. 导航到要合并的宣传品所在的位置，单击要合并的宣传品的缩略图以选择它们。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您还可以从“全局搜索”框中搜索模板。

   您可以浏览存储库 [!DNL Experience Manager Assets] 或集合，导航到所需模板的位置，然后选择它们进行合并。

   您可以应用各种过滤器来搜索所需的模板。 例如，您可以根据文件类型或标记搜索模板。

1. Click **[!UICONTROL Next]** from the toolbar.
1. 在“预览 **[!UICONTROL 和重新排序]** ”屏幕中，根据需要重新排列模板，并预览要合并的模板选择。 然后，单击工 **[!UICONTROL 具栏]** 中的“下一步”。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在“配 [!UICONTROL 置模板] ”屏幕中，指定宣传品的名称。 （可选）指定您认为合适的任何标记。 如果要以PDF格式导出输出，请选 **[!UICONTROL 择Acrobat(.PDF)]**。 默认情况下，辅助材料以JPG和格式 [!DNL InDesign] 导出。 要更改多页宣传资料的显示缩略图，请单击“更 **[!UICONTROL 改缩略图]**”。

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 单击 **[!UICONTROL “保存]** ”，然后 **[!UICONTROL 在对话]** 框中单击“确定”以关闭对话框。 多页宣传资料会在您开始使用的文件夹中创建。

   >[!NOTE]
   >
   >以后不能编辑合并的宣传资料，也不能使用它创建其他宣传资料。

## 最佳实践和限制 {#best-practices-limitations-tips}

* 编辑 [!DNL InDesign] 器在标 [!DNL Experience Manager] 记级别工作，单个标记下的所有文本都被视为单个实体。 要在编辑时保留文本格式和样式，请分别标记每个段落（或具有不同样式的文本）。
