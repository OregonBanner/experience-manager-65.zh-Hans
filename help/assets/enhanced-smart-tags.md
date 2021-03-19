---
title: 增强型智能标记
description: 增强型智能标记
contentOwner: AG
feature: 智能标记，搜索
role: 业务从业者
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 1%

---


# 了解、应用和管理智能标签{#enhanced-smart-tags}

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包含一列表关键字，员工、合作伙伴和客户通常使用这些关键字来引用和搜索特定类别的数字资产。 使用分类控制的词汇标记资产可确保轻松识别和检索资产。

与自然语言词汇相比，基于业务分类标记数字资产有助于使其与公司的业务相协调，并确保最相关的资产出现在搜索中。

例如，汽车制造商可以用型号名称标记汽车图像，以便在搜索各种型号的图像以设计促销活动时只显示相关图像。

要使智能内容服务应用正确的标签，请对其进行培训以识别您的分类。 要培训该服务，请首先创建一组最能描述这些资源的资源和标记。 要帮助服务学习，请对资产应用这些标记并运行培训工作流。

培训并准备好标记后，该服务现在可以通过标记工作流将这些标记应用于资产。

在后台，智能内容服务使用Adobe Sensei AI框架，根据您的标签结构和业务分类培训其图像识别算法。 然后，此内容智能可用于对不同的资产集应用相关标记。

智能内容服务是在[!DNL Adobe Developer Console]上托管的云服务。 要在[!DNL Adobe Experience Manager]中使用它，系统管理员必须将[!DNL Experience Manager]部署与[!DNL Adobe Developer Console]集成。

总而言之，以下是使用智能内容服务的主要步骤：

* 入门
* 审核资产和标记（分类定义）
* 培训智能内容服务
* 自动标记

![流程图](assets/flowchart.gif)

## 先决条件和支持的格式{#prerequisites}

在使用智能内容服务之前，请确保在[!DNL Adobe Developer Console]上创建集成：

* 具有组织管理员权限的Adobe ID帐户。
* 为您的组织启用智能内容服务。
* 要将智能内容服务基础包添加到部署，请许可[!DNL Adobe Experience Manager Sites]基础包和[!DNL Assets]加载项。

该服务将智能标记应用于以下MIME类型的资产：

* image/jpeg
* image/tiff
* image/png
* image/bmp
* image/gif
* image/pjpeg
* image/x-portable-anymap
* image/x-portable-bitmap
* image/x-portable-graymap
* image/x-portable-pixmap
* image/x-rgb
* image/x-xbitmap
* image/x-xpixmap
* image/x-icon
* image/photoshop
* image/x-photoshop
* image/psd
* image/vnd.adobe.photoshop

该服务将智能标记应用于以下MIME类型的资产演绎版：

* image/jpeg
* image/pjpeg
* image/png

## 入门 {#onboarding}

智能内容服务可作为[!DNL Experience Manager]的加载项购买。 购买后，系统会向组织的管理员发送一封电子邮件，其中包含指向[!DNL Adobe I/O]的链接。

管理员可以按照链接将智能内容服务与[!DNL Experience Manager]集成。 要将服务与[!DNL Experience Manager Assets]集成，请参阅[配置智能标签](config-smart-tagging.md)。

管理员配置服务并在[!DNL Experience Manager]中添加用户时，入门过程即完成。

>[!NOTE]
>
>如果您使用的是[!DNL Experience Manager] 6.3或更早版本，并且需要为您的资产提供标记服务，请参阅[智能标记](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)。 智能标签不使用最新的AI功能，因此不如增强的智能标签服务准确。

## 查看资产和标记{#reviewing-assets-and-tags}

入职后，您首先想要做的就是确定一组标签，以在业务环境中最好地描述这些图像。

接下来，查看图像以确定最能代表您的产品满足特定业务需求的图像集。 确保您所选集合中的资产符合[智能内容服务培训指南](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。

将资产添加到文件夹，然后从属性页面将标记应用到每个资产。 然后，在此文件夹上运行培训工作流。 该精选的资产集使智能内容服务能够使用您的分类定义有效地培训更多资产。

>[!NOTE]
>
>1. 培训是一个不可撤消的过程。 Adobe建议您在培训标记上的智能内容服务之前，先查看特选资产集中的标记。
>1. 在培训标记之前，请参阅[智能内容服务培训指南](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。
>1. 首次培训智能内容服务时，Adobe建议您至少使用两个不同的标签对其进行培训。


## 使用智能标签{#understandsearch}了解[!DNL Experience Manager]搜索结果

默认情况下，[!DNL Experience Manager]搜索将搜索词与`AND`子句组合。 使用智能标签不会更改此默认行为。 使用智能标签会添加额外的`OR`子句，以查找与智能标签相关的任何搜索词。 例如，考虑搜索`woman running`。 默认情况下，元数据中仅包含`woman`或`running`关键字的资产不会显示在搜索结果中。 但是，此类搜索查询中会显示使用智能标签标记为`woman`或`running`的资产。 搜索结果是，

* 元数据中具有`woman`和`running`关键字的资产。

* 使用任一关键字标记的资产智能。

首先显示与元数据字段中所有搜索词匹配的搜索结果，然后显示与智能标记中任何搜索词匹配的搜索结果。 在上例中，搜索结果的大致显示顺序为：

1. `woman running`在各种元数据字段中的匹配项。
1. 智能标记中`woman running`的匹配项。
1. 智能标记中`woman`或`running`的匹配项。

>[!CAUTION]
>
>如果在[!DNL Adobe Experience Manager]之外完成了Lucene索引，则基于智能标签的搜索不会按预期工作。

## 自动标记资源{#tagging-assets-automatically}

在培训了智能内容服务后，您可以触发标记工作流以自动对另一组类似资产应用适当的标记。

您可以定期或在需要时运行标记工作流。

>[!NOTE]
>
>标记工作流可在资产和文件夹上运行。

### 定期标记{#periodic-tagging}

您可以启用智能内容服务来定期标记文件夹中的资产。 打开资产文件夹的属性页面，在&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡下选择&#x200B;**[!UICONTROL 启用智能标记]**，然后保存更改。

为文件夹选择此选项后，智能内容服务会自动为文件夹内的资产添加标记。 默认情况下，标记工作流每天在半夜12:00运行。

### 按需标记{#on-demand-tagging}

您可以从工作流控制台或时间轴中触发标记工作流，以立即标记您的资产。

>[!NOTE]
>
>如果您从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。

#### 从工作流控制台{#tagging-assets-from-the-workflow-console}中标记资源

1. 在[!DNL Experience Manager]接口中，转至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 在&#x200B;**[!UICONTROL 工作流模型]**&#x200B;页面中，选择&#x200B;**[!UICONTROL DAM智能标记资产]**&#x200B;工作流，然后单击工具栏中的&#x200B;**[!UICONTROL 开始工作流]**。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在&#x200B;**[!UICONTROL 运行工作流]**&#x200B;对话框中，浏览至包含要自动应用标记的资产的有效负荷文件夹。
1. 指定工作流的标题和可选注释。 单击&#x200B;**[!UICONTROL 运行]**。

   ![tagging_dialog](assets/tagging_dialog.png)

   要验证智能内容服务是否正确标记了您的资产，请导航到资产文件夹并复查标记。

#### 从时间轴{#tagging-assets-from-the-timeline}标记资源

1. 从[!DNL Assets]用户界面中，选择包含要应用智能标记的资产或特定资产的文件夹。
1. 从左上角，打开&#x200B;**[!UICONTROL 时间轴]**。
1. 从左侧栏底部打开操作，然后单击&#x200B;**[!UICONTROL 开始工作流]**。

   ![开始_workflow](assets/start_workflow.png)

1. 选择&#x200B;**[!UICONTROL DAM智能标记资产]**&#x200B;工作流，然后为工作流指定标题。
1. 单击&#x200B;**[!UICONTROL 开始]**。 该工作流会对资产应用标记。 要验证智能内容服务是否正确标记了您的资产，请导航到资产文件夹并检查标记。

>[!NOTE]
>
>在随后的标记周期中，只有修改后的资产再次被标记为新训练的标记。 但是，如果标记工作流的上次和当前标记周期之间的间隙超过24小时，即使是未更改的资产也会被标记。 对于定期添加标签的工作流，当时间间隔超过六个月时，将标记未更改的资产。

## 管理或审核应用的智能标签{#manage-smart-tags}

您可以创建智能标签来删除分配给您的品牌图像的任何不准确标签，以便仅显示最相关的标签。

调节智能标签还可确保图像显示在最相关标签的搜索结果中，从而帮助优化基于标签的图像搜索。 本质上，它有助于消除不相关图像在搜索结果中出现的可能性。

您还可以为标记分配更高的排名，以提高其与图像的相关性。 提升图像的标签会增加在搜索特定标签时在搜索结果中出现图像的可能性。

1. 在搜索框中，使用标记作为关键字来搜索资产。
1. 要识别您认为与搜索无关的图像，请查看搜索结果。
1. 选择图像，然后单击工具栏中的&#x200B;**[!UICONTROL 管理标记]**。
1. 在&#x200B;**[!UICONTROL 管理标记]**&#x200B;页中，查看标记。 如果您不希望根据特定标记搜索图像，请选择该标记，然后单击工具栏中的&#x200B;**[!UICONTROL 删除]**。 或者，单击标记旁边显示的`x`符号。
1. 或者，要为标记指定更高的等级，请选择该标记，然后单击工具栏中的&#x200B;**[!UICONTROL 提升]**。 您提升的标记将移至&#x200B;**[!UICONTROL Tags]**&#x200B;部分。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后单击&#x200B;**[!UICONTROL 确定]**
1. 导航到图像的&#x200B;**[!UICONTROL 属性]**&#x200B;页。 请注意，您提升的标记已分配更多相关性，并会在搜索结果的前面显示。

## 提示和限制{#tips-best-practices-limitations}

* 智能内容服务的使用限制为每年最多200万张标记图像。 处理和标记的任何重复图像均计为标记图像。
* 如果您从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。
* “智能标签”仅适用于PNG和JPG图像格式。 因此，如果受支持的资产以这两种格式创建了演绎版，则会使用智能标记进行标记。
