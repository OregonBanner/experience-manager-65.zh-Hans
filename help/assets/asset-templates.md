---
title: 资产模板
description: 了解 [!DNL Adobe Experience Manager Assets] 中的资产模板以及如何使用资产模板创建营销宣传资料。
contentOwner: AG
role: 商务从业人员
feature: 资源管理，开发人员工具
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 0%

---


# 资产模板{#asset-templates}

资产模板是一种特殊的资产类别，可帮助快速为数字和印刷媒体重用视觉效果丰富的内容。 资产模板包括两个部分，即固定消息部分和可编辑部分。 固定消息部分可包含专有内容，如品牌徽标和禁止编辑的版权信息。 可编辑部分可以在可编辑以自定义消息的字段中包含可视内容和文本内容。

在保护全局标牌的同时进行有限的编辑的灵活性使得资产模板成为快速调整和分发内容的理想构件块，并将其作为各种功能的内容伪像。 重新调整内容用途有助于降低管理印刷和数字渠道的成本，并在这些渠道中提供整体一致的体验。

作为营销人员，您可以在[!DNL Experience Manager Assets]中存储和管理模板，并使用单个基本模板轻松创建多个个性化的打印体验。 您可以创建各种类型的营销宣传资料，包括宣传册、传单、明信片、名片等，以便向客户清晰地传达您的营销信息。 您还可以从现有或新的打印输出组合多页打印输出。 最重要的是，您可以同时轻松提供数字和印刷体验，为用户提供一致、集成的体验。

虽然资产模板大多为[!DNL Adobe InDesign]文件，但熟练掌握[!DNL Adobe InDesign]并不妨碍创建星光伪像。 您无需将[!DNL Adobe InDesign]模板的字段与您在创建目录时需要的产品字段进行映射。 您可以直接在Web界面上以WYSIWYG模式编辑模板。 但是，要使[!DNL Adobe InDesign]处理编辑更改，必须首先配置[!DNL Experience Manager Assets]以与[!DNL Adobe InDesign Server]集成。

从Web界面编辑[!DNL Adobe InDesign]模板的能力有助于促进创意人员与营销人员之间更紧密的协作。 内容速度的提高缩短了营销抵押品的上市时间。

使用资产模板，您可以实现以下目标：

* 从Web界面修改可编辑的模板字段。
* 控制文本的基本样式，例如，字体大小、样式和标记级别的文字。
* 使用内容选取器更改模板中的图像。
* 预览模板编辑。
* 合并多个模板文件以创建多页对象。

当您为宣传品选择模板时，[!DNL Experience Manager Assets]会创建可编辑的模板副本。 保留原始模板，这可确保您的全球标牌保持不变，并可以重复使用以实现品牌一致性。

可以以INDD、PDF或JPG格式导出父文件夹中的更新文件。 您还可以将这些格式的输出下载到本地文件系统。

## 创建宣传品{#creating-a-collateral}

假设您希望为即将到来的活动创建数字可打印宣传品（如宣传册、传单和广告）并与全球直销商店共享。 根据模板创建宣传资料有助于跨渠道提供统一的客户体验。 设计人员可以使用创意解决方案（如[!DNL InDesign]）创建活动模板（单页或多页），并为您上传模板至[!DNL Experience Manager Assets]。 在创建宣传品之前，请提前将一个或多个INDD模板上载到[!DNL Experience Manager]并在中可用。

1. 在[!DNL Experience Manager]接口中，单击[!UICONTROL 资产]。

1. 从选项中选择&#x200B;**[!UICONTROL 模板]**。

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. 单击&#x200B;**[!UICONTROL 创建]**，然后从菜单中选择要创建的宣传品。 例如，选择&#x200B;**[!UICONTROL 手册]**。

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. 提前将一个或多个INDD模板上载到[!DNL Experience Manager]并在中可用。 为您的宣传册选择模板，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 指定宣传册的名称和可选说明。

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. （可选）单击&#x200B;**[!UICONTROL 标记]**&#x200B;并为手册选择一个或多个标记。 单击&#x200B;**[!UICONTROL 确认]**&#x200B;以确认您的选择。
1. 单击&#x200B;**[!UICONTROL 创建]**。对话框确认已创建新的宣传册。 单击&#x200B;**[!UICONTROL 打开]**&#x200B;以编辑模式打开宣传册。

   <!--![chlimage_1-106](assets/.png) -->

   或者，关闭对话框并导航到您开始使用的“模板”页面中的文件夹，以视图您创建的宣传册。 宣传品的类型会以卡片视图显示在其缩略图上。 例如，在此例中，缩览图上会显示单词[!UICONTROL Brochure]。

   ![chlimage_1-107](assets/chlimage_1-312.png)

## 编辑宣传品{#editing-a-collateral}

在创建宣传品后，您可以立即对其进行编辑。 或者，也可以从[!UICONTROL 模板]页面或资产页面打开它。

1. 要打开要编辑的宣传品，请执行以下操作之一：

   * 打开您在[创建宣传品](/help/assets/asset-templates.md#creating-a-collateral)的步骤7中创建的宣传品（本例中为手册）。
   * 在“模板”页面中，导航到创建宣传品的文件夹，然后单击宣传品缩略图上的[!UICONTROL 编辑]快速操作。
   * 在宣传品的资产页面中，单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。
   * 选择宣传品，然后单击工具栏中的&#x200B;**[!UICONTROL 编辑]**。

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   资产查找器和文本编辑器显示在页面左侧。 默认情况下，文本编辑器处于打开状态。

   您可以使用文本编辑器修改要在文本字段中显示的文本。 您可以在标记级别修改字体大小、样式、颜色和文字。

   使用资产查找器，您可以浏览或搜索[!DNL Experience Manager Assets]中的图像，并将模板中的可编辑图像替换为您选择的图像。

   ![chlimage_1-109](assets/chlimage_1-314.png)

   可编辑内容显示在右侧。 要在[!DNL Experience Manager Assets]中编辑字段，必须在[!DNL InDesign]中标记模板中的相应字段。 换句话说，它们应在[!DNL InDesign]中标记为可编辑。

   >[!NOTE]
   >
   >确保您的[!DNL Experience Manager]部署与[!DNL InDesign Server]集成，以启用[!DNL Experience Manager Assets]从[!DNL InDesign]模板提取数据并使其可供编辑。 有关详细信息，请参阅[将Experience Manager资产与InDesign Server](/help/assets/indesign.md)集成。

1. 要修改可编辑字段中的文本，请单击可编辑字段列表中的文本字段，然后编辑该字段中的文本。

   ![chlimage_1-111](assets/chlimage_1-316.png)

   您可以编辑文本属性，例如，使用提供的选项编辑字体样式、颜色和大小。

1. 单击&#x200B;**[!UICONTROL 预览]**&#x200B;以预览文本更改。

1. 要交换图像，请单击&#x200B;**[!UICONTROL 资产查找器]** ![chlimage_1-113](assets/chlimage_1-318.png)。

1. 从可编辑字段的列表中选择图像字段，然后将所需图像从资产选取器拖到可编辑字段。

   ![chlimage_1-114](assets/chlimage_1-319.png)

   您还可以使用关键字、标记并根据图像的发布状态搜索图像。 您可以浏览[!DNL Experience Manager Assets]存储库并导航到所需图像的位置。

   ![chlimage_1-114](assets/chlimage_1-320.png)

1. 单击&#x200B;**[!UICONTROL 预览]**&#x200B;以预览图像。
1. 要在多页宣传资料中编辑特定页面，请使用底部的页面导航器。

1. 单击工具栏上的&#x200B;**[!UICONTROL 预览]**&#x200B;以预览所有更改。 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以保存对宣传资料的编辑更改。

   >[!NOTE]
   >
   >仅当宣传品中的可编辑图像字段没有任何缺少的图标时，才会启用“预览”和“完成”选项。 如果宣传品中缺少图标，则是因为[!DNL Experience Manager]无法解析[!DNL InDesign]模板中的图像。 通常，[!DNL Experience Manager]在以下情况下无法解析映像：
   >
   >* 图像未嵌入基础[!DNL InDesign]模板中。
   >* 图像从本地文件系统链接。

   >
   >要启用[!DNL Experience Manager]解析图像，请执行以下操作：
   >
   >* 在创建[!DNL InDesign]模板时嵌入图像（请参阅[关于链接和嵌入式图形](https://helpx.adobe.com/indesign/using/graphics-links.html)）。
   >* 将[!DNL Experience Manager]装载到本地文件系统，然后将缺少的图标与[!DNL Experience Manager]中的现有资源进行映射。

   >
   >有关使用[!DNL InDesign]文档的详细信息，请参阅[使用Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html)中的InDesign文档的最佳实践。

1. 要为宣传册生成PDF再现，请在对话框中选择Acrobat选项，然后单击&#x200B;**[!UICONTROL 继续]**。
1. 附属品会在您开始使用的文件夹中创建。 要视图演绎版，请打开宣传品，然后从GlobalNav列表中选择&#x200B;**[!UICONTROL 演绎版]**。

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. 从演绎版列表单击PDF演绎版以下载PDF文件。 打开PDF文件以查看宣传品。

   ![chlimage_1-119](assets/chlimage_1-324.png)

## 合并宣传品{#merge-collateral}

1. 在[!DNL Experience Manager]界面中，单击“导航”页面上的[!UICONTROL 资产]。

1. 从选项中选择&#x200B;**[!UICONTROL 模板]**。

1. 单击&#x200B;**[!UICONTROL 创建]**，然后从菜单中选择&#x200B;**[!UICONTROL 合并]**。

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. 在[!UICONTROL 模板合并]页中，单击&#x200B;**[!UICONTROL 合并]** ![添加资产](assets/do-not-localize/assets_add_icon.png)。

1. 导航到要合并的宣传品所在的位置，单击要合并的宣传品缩略图以选择它们。

   ![chlimage_1-122](assets/chlimage_1-327.png)

   您还可以从“全局搜索”框中搜索模板。

   您可以浏览[!DNL Experience Manager Assets]存储库或集合，导航到所需模板的位置，然后选择它们进行合并。

   您可以应用各种过滤器来搜索所需的模板。 例如，您可以根据文件类型或标记搜索模板。

1. 单击工具栏中的&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL “预览和重新排序”]**&#x200B;屏幕中，根据需要重新排列模板并预览要合并的模板选择。 然后，单击工具栏中的&#x200B;**[!UICONTROL 下一步]**。

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. 在[!UICONTROL 配置模板]屏幕中，指定宣传品的名称。 （可选）指定您认为合适的任何标记。 如果要以PDF格式导出输出，请选择&#x200B;**[!UICONTROL Acrobat(.PDF)]**。 默认情况下，辅助材料以JPG和[!DNL InDesign]格式导出。 要更改多页宣传资料的显示缩略图，请单击&#x200B;**[!UICONTROL 更改缩略图]**。

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. 单击&#x200B;**[!UICONTROL 保存]**，然后单击对话框中的&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭对话框。 多页宣传资料会在您开始使用的文件夹中创建。

   >[!NOTE]
   >
   >以后不能编辑合并的宣传品，也不能使用它创建其他宣传品。

## 最佳实践和限制{#best-practices-limitations-tips}

* [!DNL Experience Manager]中的[!DNL InDesign]编辑器在标签级别工作，单个标签下的所有文本都被视为单个实体。 要在编辑时保留文本格式和样式，请分别为每个段落（或具有不同样式的文本）添加标签。
