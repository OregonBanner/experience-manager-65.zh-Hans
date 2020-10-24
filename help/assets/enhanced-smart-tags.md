---
title: 增强型智能标记
description: 增强型智能标记
contentOwner: AG
translation-type: tm+mt
source-git-commit: e124025295f29d6f3999dc52467301d48bceee75
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 1%

---


# 了解、应用和管理智能标签 {#enhanced-smart-tags}

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包含一列表关键字，员工、合作伙伴和客户通常使用这些关键字来引用和搜索特定类别的数字资产。 使用分类控制的词汇标记资产可确保通过基于标签的搜索轻松识别和检索资产。

与自然语言词汇相比，基于业务分类标记数字资产有助于使其与公司的业务保持一致，并确保最相关的资产出现在搜索中。

例如，汽车制造商可以用型号名称标记汽车图像，以便在搜索各种型号的图像以设计促销活动时只显示相关图像。

要使智能内容服务应用正确的标记，您必须对其进行培训以识别您的分类。 要培训服务，请首先创建一组最能描述这些资产的资产和标记。 在资产上应用这些标记并运行培训工作流，以帮助服务学习。

一旦标记经过培训并准备就绪，该服务现在就可以通过标记工作流将这些标记应用于资产。

在后台，智能内容服务使用Adobe Sensei人工智能框架来根据您的标签结构和业务分类训练其图像识别算法。 然后，此内容智能用于对另一组资产应用相关标记。

智能内容服务是托管在AdobeI/O上的云服务。要在中使 [!DNL Adobe Experience Manager]用它，系统管理员必须将您的 [!DNL Experience Manager] 部署与AdobeI/O集成。

总而言之，使用智能内容服务的主要步骤如下：

* 入门
* 审核资产和标记（分类定义）
* 培训智能内容服务
* 自动标记

![流程图](assets/flowchart.gif)

## 前提条件 {#prerequisites}

在使用智能内容服务之前，请确保以下各项在AdobeI/O上创建集成：

* 具备拥有组织管理员权限的 Adobe ID 帐户。
* 您的组织已启用智能内容服务。
* 智能内容服务基础包只能添加到基础包和 [!DNL Sites] 加载项 [!DNL Assets] 已获得许可的部署。

## 入门 {#onboarding}

The Smart Content Service is available for purchase as an add-on to [!DNL Experience Manager]. 购买后，系统会向组织的管理员发送一封电子邮件，其中包含指向AdobeI/O的链接。

管理员可以点击链接将智能内容服务与集成 [!DNL Experience Manager]。 要将服务与集成，请 [!DNL Experience Manager Assets]参阅 [配置智能标记](config-smart-tagging.md)。

管理员配置服务并在中添加用户时，入门过程即完成 [!DNL Experience Manager]。

>[!NOTE]
>
>如果您使用的是 [!DNL Experience Manager] 6.3或更早版本，并且需要为资产提供标记服务，请参阅智 [能标记](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)。 智能标记不使用最新的AI功能，因此不如增强的智能标记服务准确。

## 审核资产和标记 {#reviewing-assets-and-tags}

入职后，您首先想要做的是识别一组标签，在您的业务环境中最好地描述这些图像。

接下来，检查图像以确定最能代表您的产品以满足特定业务需求的图像集。 确保特选集合中的资产符合智能内 [容服务培训准则](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。

将资产添加到文件夹，然后从属性页面将标记应用到每个资产。 然后，在此文件夹上运行培训工作流。 该精选的资产集使智能内容服务能够使用您的分类定义有效地培训更多资产。

>[!NOTE]
>
>1. 培训是一个不可撤消的过程。 Adobe建议您在对标记培训智能内容服务之前，先查看特选资产集中的标记。
>1. 在培训标记之前，请参阅智 [能内容服务培训指南](/help/assets/config-smart-tagging.md#training-the-smart-content-service)。
>1. 首次培训智能内容服务时，Adobe建议您至少使用两个不同的标签对其进行培训。


## 使用智 [!DNL Experience Manager] 能标记了解搜索结果 {#understandsearch}

默认情况下， [!DNL Experience Manager] 搜索将搜索词与子句 `AND` 组合。 使用智能标记不会更改此默认行为。 使用智能标记可添加 `OR` 一个附加子句，以在应用智能标记中查找任何搜索词。 For example, consider searching for `woman running`. 默认情况下， `woman` 元数据 `running` 中仅包含关键字的资产不会显示在搜索结果中。 但是，在此类搜索查询中， `woman` 会显 `running` 示带有或使用智能标记的资产。 搜索结果是，

* 元数据 `woman` 中 `running` 包含和关键字的资产。

* 使用任一关键字标记的资产智能。

首先显示与元数据字段中所有搜索词匹配的搜索结果，然后显示与智能标记中任何搜索词匹配的搜索结果。 在上例中，搜索结果的近似显示顺序为：

1. 的匹配 `woman running` 项。
1. 智能标 `woman running` 记中的匹配项。
1. 智能标 `woman` 签的 `running` 匹配项或匹配项。

>[!CAUTION]
>
>如果Lucene索引完成 [!DNL Adobe Experience Manager] 后，基于智能标记的搜索无法按预期工作。

## 自动标记资源 {#tagging-assets-automatically}

在培训了智能内容服务后，您可以触发标记工作流以自动对另一组类似资产应用适当的标记。

您可以定期或在需要时运行标记工作流。

>[!NOTE]
>
>标记工作流同时在资产和文件夹上运行。

### 定期标记 {#periodic-tagging}

您可以启用智能内容服务来定期标记文件夹中的资产。 打开资产文件夹的属性页面，在详细 **[!UICONTROL 信息选项卡下]** ，选 **[!UICONTROL 择启]** 用智能标记，然后保存更改。

为文件夹选择此选项后，智能内容服务会自动为文件夹中的资产添加标记。 默认情况下，标记工作流每天在凌晨12:00运行。

### 按需标记 {#on-demand-tagging}

您可以从工作流控制台或时间轴触发标记工作流，以立即标记您的资产。

>[!NOTE]
>
>如果您从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。

#### 从工作流控制台标记资产 {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在运行 **[!UICONTROL 工作流]** ，浏览至包含要自动应用标记的资产的有效负荷文件夹。
1. 指定工作流的标题和可选注释。 单击“ **[!UICONTROL 运行]**”。

   ![tagging_dialog](assets/tagging_dialog.png)

   导航到资产文件夹并检查标记，以验证智能内容服务是否正确标记了您的资产。

#### 从时间轴标记资产 {#tagging-assets-from-the-timeline}

1. 从用 [!DNL Assets] 户界面中，选择包含要应用智能标记的资产或特定资产的文件夹。
1. 从左上角打开时间 **[!UICONTROL 轴]**。
1. 从左侧提要栏底部打开操作，然后单击“ **[!UICONTROL 开始工作流]**”。

   ![开始工作流](assets/start_workflow.png)

1. 选择DAM **[!UICONTROL 智能标记资产工作流]** ，然后为工作流指定标题。
1. 单击 **[!UICONTROL 开始]**。 该工作流会对资产应用您的标记。 导航到资产文件夹并检查标记，以验证智能内容服务是否正确标记了您的资产。

>[!NOTE]
>
>在随后的标记周期中，只有修改后的资产会再次使用经过新培训的标记进行标记。但是，如果标记工作流的上一个标记周期与当前标记周期之间的间隔超过24小时，即使资产未更改也会进行标记。 对于定期标记工作流，当时间间隔超过6个月时，将标记未更改的资产。

## 创建或审核应用的智能标记 {#manage-smart-tags}

您可以创建智能标记来删除可能分配给您的品牌图像的任何不准确标记，以便只显示最相关的标记。

调节智能标签还可确保图像显示在最相关标签的搜索结果中，从而帮助优化基于标签的图像搜索。 从根本上说，它有助于消除不相关图像在搜索结果中出现的可能性。

您还可以为标记分配更高的等级，以提高其与图像的相关性。 提升图像的标记可提高当基于特定标记执行搜索时在搜索结果中出现图像的可能性。

1. 在“全局搜索”框中，根据标记搜索资产。
1. Inspect搜索结果，以识别与搜索不相关的图像。
1. 选择图像，然后单击工 **[!UICONTROL 具栏中的]** “管理标记”。
1. 从“管 **[!UICONTROL 理标记]** ”页面检查标记。 如果不希望根据特定标记搜索图像，请选择该标记，然后单击工 **[!UICONTROL 具栏]** 中的删除。 或者，单 `x` 击标记旁边显示的符号。
1. （可选）要为标记分配更高的等级，请选择标记，然后单 **[!UICONTROL 击工]** 具栏中的提升。 您提升的标记将移到“标记 **[!UICONTROL ”部]** 分。
1. 单击“ **[!UICONTROL 保存]** ”，然后单击“确 **[!UICONTROL 定”]**
1. 导航到 **[!UICONTROL 图像的]** “属性”页。 请注意，您提升的标记已分配更多相关性，并会在搜索结果的前面显示。

## 提示和限制 {#tips-best-practices-limitations}

* 智能内容服务的使用限制为每年最多200万张标记图像。 处理和标记的任何重复图像均计为标记图像。
* 如果您从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。
