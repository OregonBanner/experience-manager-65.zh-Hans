---
title: 资产模板
description: 了解AEM资产中的资产模板以及如何使用资产模板创建营销附属品。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Asset templates {#asset-templates}

资产模板是一种特殊的资产类别，它有助于快速为数字和印刷媒体重用视觉效果丰富的内容。 资产模板包括两个部分，即固定消息部分和可编辑部分。

固定消息部分可以包含专有内容，如品牌徽标和禁用编辑的版权信息。 可编辑部分可在可编辑的字段中包含可视内容和文本内容，以自定义消息。

在保护全局标牌的同时灵活进行有限的编辑使得资产模板成为快速调整内容和分发内容的理想构件块，并将其作为各种功能的内容伪像进行分发。 内容重用有助于降低管理印刷和数字渠道的成本，并跨这些渠道提供整体一致的体验。

作为营销人员，您可以在AEM资产中存储和管理模板，并使用单个基本模板轻松创建多个个性化的打印体验。 您可以创建各种类型的营销宣传资料，包括小册子、传单、明信片、名片等，以便向客户清晰地传达您的营销信息。 您还可以从现有或新的打印输出组合多页打印输出。 最重要的是，您可以同时轻松提供数字和印刷体验，为用户提供一致、集成的体验。

虽然资产模板大多为Adobe InDesign文件，但熟练掌握Adobe InDesign并不妨碍创建出众的人工作。 您无需将Adobe InDesign模板的字段与您在创建目录时需要的产品字段进行映射。 您可以直接在Web界面上以WYSIWYG模式编辑模板。 但是，要使Adobe InDesign处理您的编辑更改，您必须首先配置AEM资产以与Adobe InDesign服务器集成。

从Web界面编辑Adobe InDesign模板的能力有助于促进创意人员与营销人员之间更紧密的协作，同时缩短本地促销活动的上市时间。

您可以使用资产模板执行以下操作：

* 从Web界面修改可编辑的模板字段
* 控制文本的基本样式，例如，字体大小、样式和标记级别的文字
* 使用内容选取器更改模板中的图像
* 预览模板编辑
* 合并多个模板文件以创建多页对象

在您为宣传品选择模板时，AEM资产会创建可编辑的模板副本。 保留原始模板，这可确保您的全局标牌保持不变，并可以重复使用以实现品牌一致性。

可以采用以下格式导出父文件夹内的更新文件：

* INDD
* PDF
* JPG

您还可以将这些格式的输出下载到本地系统。

## 创建附属品 {#creating-a-collateral}

请考虑您希望为即将到来的活动创建数字可打印宣传品（如小册子、广告传单和广告）并与全球直销店共享的场景。 基于模板创建附属品有助于跨渠道提供统一的客户体验。 设计人员可以使用InDesign等创意解决方案创建活动模板（单页或多页），并为您上传模板到AEM资产。 在创建宣传资料之前，请事先将一个或多个INDD模板上载到Experience Manager并在其中可用。

1. 在Experience Manager界面中，单击“ [!UICONTROL 资产”]。

1. 从选项中，选择“模 **[!UICONTROL 板”]**。

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 单击 **[!UICONTROL 创建]**，然后从菜单中选择要创建的宣传品。 例如，选择“ **[!UICONTROL Brochure]**”。

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 提前将一个或多个INDD模板上传到Experience Manager并在其中可用。 为您的宣传册选择模板，然后单击“下 **[!UICONTROL 一步”]**。

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. 指定宣传册的名称和可选说明。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （可选）单击“ **[!UICONTROL 标记]** ”，然后为小册子选择一个或多个标记。 单击 **[!UICONTROL 确认]** ，以确认您的选择。

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. 单击&#x200B;**[!UICONTROL 创建]**。对话框会确认已创建新手册。 单击 **[!UICONTROL 打开]** ，以编辑模式打开宣传册。

   <!--![chlimage_1-106](assets/.png) -->

   或者，关闭对话框并导航到您开始使用的“模板”页面中的文件夹，以视图您创建的小册子。 附属品的类型显示在其缩略图上的卡片视图中。 例如，在这种情况下，Brochure会显示在缩略图上。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 编辑宣传资料 {#editing-a-collateral}

您可以在创建附属品后立即对其进行编辑。 或者，也可以从模板页面或资产页面打开它。

1. 要打开要编辑的宣传资料，请执行下列操作之一：

   * 打开您在创建宣传资料步骤7中创建的宣传资料(本例中为 [宣传册)](/help/assets/asset-templates.md#creating-a-collateral)。
   * 在“模板”页面中，导航到您创建宣传品的文件夹，然后单击宣传品缩略图上的 [!UICONTROL Edit] quick action。
   * 在附属品的资产页面中，单击工 **[!UICONTROL 具栏中]** 的编辑。
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.
   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   资产查找器和文本编辑器显示在页面的左侧。 默认情况下，文本编辑器处于打开状态。

   您可以使用文本编辑器修改要在文本字段中显示的文本。 您可以在标记级别修改字体大小、样式、颜色和类型。

   使用资产查找器，您可以浏览或搜索AEM资产中的图像，并将模板中的可编辑图像替换为您选择的图像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可编辑内容显示在右侧。 要在AEM资产中编辑字段，必须在InDesign中标记模板中的相应字段。 换句话说，它们应在InDesign中标记为可编辑。

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >确保您的AEM实例已与InDesign服务器集成，以使AEM资产能够从InDesign模板中提取数据并使其可供编辑。 有关详细信息，请 [参阅将AEM资产与InDesign Server集成](/help/assets/indesign.md)。

1. 要修改可编辑字段中的文本，请单击可编辑字段列表中的文本字段，然后编辑该字段中的文本。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以编辑文本属性，例如字体样式、颜色和大小，使用提供的选项。

1. 单击 **[!UICONTROL 预览]** ，以预览文本更改。

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. 要交换图像，请单击资产 **[!UICONTROL 查找器]**。

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. 从可编辑字段的列表中选择图像字段，然后将所需图像从资产选取器拖动到可编辑字段。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您还可以使用关键字、标记并根据图像的发布状态搜索图像。 您可以浏览AEM资产存储库，然后导航到所需图像的位置。

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. 单击 **[!UICONTROL 预览]** ，以预览图像。

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. 要编辑多页附属品中的特定页面，请使用底部的页面导航器。

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. 单击 **[!UICONTROL 工具栏上的预览]** ，以预览所有更改。 单击 **[!UICONTROL 完成]** ，以保存对宣传品的编辑更改。

   >[!NOTE]
   >
   >只有在附属品中的可编辑图像字段没有任何缺少的图标时，预览和完成图标才会启用。 如果您的附属品中缺少图标，这是因为AEM无法解析InDesign模板中的图像。 通常，AEM在以下情况下无法解析图像：
   >
   >    * 图像未嵌入底层InDesign模板中
   >    * 图像从本地文件系统链接
   >
   >要启用AEM解析图像，请执行以下操作：
   >
   >    * 在创建InDesign模板时嵌入图像(请参 [阅关于链接和嵌入图形](https://helpx.adobe.com/indesign/using/graphics-links.html))。
   >    * 将AEM装载到本地文件系统，然后将缺少的图标与现有AEM资产映射。
   >
   >有关使用InDesign文档的更多信息，请参 [阅在AEM中使用InDesign文档的最佳实践](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html)。

1. 要为小册子生成PDF再现，请在对话框中选择Acrobat选项，然后单击“继 **[!UICONTROL 续”]**。
1. 附属品会在您开始使用的文件夹中创建。 要视图演绎版，请打开附属品，然后从GlobalNav列表 **[!UICONTROL 中选择]** “演绎版”。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 从演绎版列表中单击PDF演绎版以下载PDF文件。 打开PDF文件以查看附属品。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合并附属品 {#merge-collateral}

1. 在Experience Manager界面中，单击导 [!UICONTROL 航页面] 上的资产。

1. 从选项中，选择“模 **[!UICONTROL 板”]**。

1. 单击 **[!UICONTROL 创建]** ，然后从菜 **[!UICONTROL 单中选]** 择“合并”。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 在“模 [!UICONTROL 板合并] ”页面中，单 **[!UICONTROL 击合并]**。

   ![chlimage_1-121](assets/chlimage_1-326.png)

1. 导航到要合并的附属品的位置，单击要合并的附属品的缩略图以选择它们。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您还可以从Omnisearch框中搜索模板。

   ![chlimage_1-123](assets/chlimage_1-328.png)

   您可以浏览AEM资产存储库或收藏集，然后导航到所需模板的位置，然后选择它们进行合并。

   ![chlimage_1-124](assets/chlimage_1-329.png)

   您可以应用各种过滤器来搜索所需的模板。 例如，您可以根据文件类型或标记搜索模板。

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. 单击 **[!UICONTROL 工具栏]** 中的下一步。
1. 在“预览 **[!UICONTROL 和重新排序]** ”屏幕中，根据需要重新排列模板，并预览要合并的模板选择。 然后，单击工 **[!UICONTROL 具栏]** 中的“下一步”。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在“配 [!UICONTROL 置模板] ”屏幕中，指定宣传品的名称。 （可选）指定您认为合适的任何标记。 如果要以PDF格式导出输出，请选择 **[!UICONTROL Acrobat(.PDF)]**。 默认情况下，辅助材料以JPG和InDesign格式导出。 要更改多页宣传资料的显示缩略图，请单击“更 **[!UICONTROL 改缩略图”]**。

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 单击 **[!UICONTROL 保存]** ，然后在对话 **[!UICONTROL 框中单击确定]** ，以关闭对话框。 将在您开始使用的文件夹中创建多页宣传资料。

   >[!NOTE]
   >
   >您以后不能编辑合并的附属品，也不能使用它创建其他附属品。
