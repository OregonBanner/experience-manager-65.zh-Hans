---
title: 增强的智能标记
description: 增强的智能标记
contentOwner: AG
translation-type: tm+mt
source-git-commit: 678e91699523c22a7048bd7b344fa539b849ae8b
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 7%

---


# 增强的智能标记 {#enhanced-smart-tags}

## 增强的智能标记概述 {#overview-of-enhanced-smart-tags}

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包含一列表关键字，员工、合作伙伴和客户通常使用这些关键字来引用和搜索特定类别的数字资产。 使用分类控制的词汇标记资产可确保通过基于标签的搜索轻松识别和检索资产。

与自然语言词汇相比，基于业务分类标记数字资产有助于使其与公司的业务保持一致，并确保最相关的资产出现在搜索中。

例如，汽车制造商可以用型号名称标记汽车图像，以便在搜索各种型号的图像以设计促销活动时只显示相关图像。

要使智能内容服务应用正确的标记，您必须对其进行培训以识别您的分类。 要培训服务，请首先创建一组最能描述这些资产的资产和标记。 在资产上应用这些标记并运行培训工作流，以帮助服务学习。

一旦标记经过培训并准备就绪，该服务现在就可以通过标记工作流将这些标记应用于资产。

在后台，智能内容服务使用Adobe Sensei AI框架来根据您的标签结构和业务分类培训其图像识别算法。 然后，此内容智能用于对另一组资产应用相关标记。

智能内容服务是在Adobe I/O上托管的云服务。 要在Adobe Experience Manager中使用它，系统管理员必须将您的Experience Manager部署与Adobe I/O集成。

总而言之，使用智能内容服务的主要步骤如下：

* 入门
* 审核资产和标记（分类定义）
* 培训智能内容服务
* 自动标记

![流程图](assets/flowchart.gif)

## 前提条件 {#prerequisites}

在使用智能内容服务之前，请确保以下各项在Adobe I/O上创建集成：

* 具有组织管理员权限的Adobe ID帐户。
* 您的组织已启用智能内容服务。

## 入门 {#onboarding}

智能内容服务可作为附加组件购买Experience Manager。 购买后，系统会向组织的管理员发送一封电子邮件，其中包含指向Adobe I/O的链接。

管理员可以点击链接将智能内容服务与Experience Manager集成。 要将服务与Experience Manager资产集成，请参 [阅配置智能标记](config-smart-tagging.md)。

管理员配置服务并以Experience Manager添加用户时，入门过程即完成。

>[!NOTE]
>
>如果您使用的是Experience Manager6.3或更早版本，并且需要为资产提供标记服务，请参阅智 [能标记](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html)。 智能标记不使用最新的AI功能，因此不如增强的智能标记服务准确。

## 审核资产和标记 {#reviewing-assets-and-tags}

载入后，您首先想要做的是识别一组标签，在您的业务环境中最好地描述这些图像。

接下来，检查图像以确定最能代表您的产品以满足特定业务需求的图像集。 确保特选集合中的资产符合智能内 [容服务培训准则](smart-tags-training-guidelines.md)。

将资产添加到文件夹，然后从属性页面将标记应用到每个资产。 然后，在此文件夹上运行培训工作流。 该精选的资产集使智能内容服务能够使用您的分类定义有效地培训更多资产。

>[!NOTE]
>
>1. 培训是一个不可撤消的过程。 Adobe建议您在培训标记上的智能内容服务之前，先查看特选资产集中的标记。
>1. 请在开始针对 [任何标记的培训之前](smart-tags-training-guidelines.md) ，阅读智能内容服务培训指南。
>1. 首次培训智能内容服务时，Adobe建议您至少使用两个不同的标签对其进行培训。


## 培训智能内容服务 {#training-the-smart-content-service}

要使智能内容服务识别您的业务分类，请在已包含与您的业务相关标签的资产集上运行它。 培训后，服务可以对类似的资产集应用相同的分类。

您可以对服务进行多次培训，以提高应用相关标签的能力。 在每个培训周期后，运行一个标记工作流并检查您的资产是否已正确标记。

您可以定期或根据需要培训智能内容服务。

>[!NOTE]
>
>培训工作流仅在文件夹上运行。

### 定期培训 {#periodic-training}

您可以启用智能内容服务，以定期培训文件夹中的资产和相关标记。 打开资 [!UICONTROL 产文件] 夹的“属性”页，在“详细信 **[!UICONTROL 息”选项卡下选择]** “启用智 **[!UICONTROL 能标记]** ”，然后保存更改。

![enable_smart_tags](assets/enable_smart_tags.png)

为文件夹选择此选项后，Experience Manager将自动运行培训工作流，以对文件夹资产及其标记进行智能内容服务培训。 默认情况下，培训工作流程每周在星期六的凌晨12:30运行。

### 按需培训 {#on-demand-training}

您可以根据需要从工作流控制台培训智能内容服务。

1. 在Experience Manager界面中，转 **[!UICONTROL 到工具]** >工 **[!UICONTROL 作流]****[!UICONTROL >]**&#x200B;模型。
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.
1. 在“运 **[!UICONTROL 行工作流]** ”对话框中，浏览到有效负荷文件夹，该文件夹包含用于培训服务的标记资产。
1. 指定工作流的标题并添加评论。 然后，单击“ **[!UICONTROL 运行]**”。 资产和标记将提交用于培训。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>在对文件夹中的资产进行培训后，仅在后续培训周期中处理修改后的资产。

### 视图培训报告 {#viewing-training-reports}

要检查智能内容服务是否在资产培训集中的标记上接受过培训，请从“报告”控制台查看培训工作流报告。

1. 在Experience Manager界面中，转 **[!UICONTROL 到工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 报]**&#x200B;告。
1. In the **[!UICONTROL Asset Reports]** page, click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then click **[!UICONTROL Next]** from the toolbar.
1. 指定报表的标题和描述。在&#x200B;**[!UICONTROL 计划报告]**&#x200B;下，保持选中&#x200B;**[!UICONTROL 立即]**&#x200B;选项。如果要安排以后的计划报告，请选择&#x200B;**[!UICONTROL 稍后]**，然后指定日期和时间。Then, click **[!UICONTROL Create]** from the toolbar.
1. 在&#x200B;**[!UICONTROL 资产报表]**&#x200B;页面中，选择生成的报表。To view the report, click **[!UICONTROL View]** from the toolbar.
1. 查看报告的详细信息。

   报表显示您培训的标记的培训状态。**[!UICONTROL 培训状态]**&#x200B;列中的绿色表示已为标记培训“智能内容服务”。黄色表示服务未针对特定标记进行完整培训。在这种情况下，使用特定标记添加更多图像并运行培训工作流以在标签上完整地培训服务。

   如果此报告中未显示标记，请再次运行这些标记的培训工作流程。

1. 要下载报告，请从列表中选择它，然后单击工 **[!UICONTROL 具栏]** 中的下载。 报告以Microsoft Excel电子表格的形式下载。

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

您可以从以下内容触发标记工作流，以立即标记您的资产：

* “工作流”控制台
* 时间轴

>[!NOTE]
>
>如果您从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。

#### 从工作流控制台标记资产 {#tagging-assets-from-the-workflow-console}

1. 在Experience Manager界面中，转 **[!UICONTROL 到工具]** >工 **[!UICONTROL 作流]****[!UICONTROL >]**&#x200B;模型。
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在运行 **[!UICONTROL 工作流]** ，浏览至包含要自动应用标记的资产的有效负荷文件夹。
1. 指定工作流的标题和可选注释。 单击“ **[!UICONTROL 运行]**”。

   ![tagging_dialog](assets/tagging_dialog.png)

   导航到资产文件夹并检查标记，以验证智能内容服务是否正确标记了您的资产。 有关详细信息，请参 [阅管理智能标记](managing-smart-tags.md)。

#### 从时间轴标记资产 {#tagging-assets-from-the-timeline}

1. 从资产用户界面中，选择包含要应用智能标记的资产或特定资产的文件夹。
1. 从左上角打开时间 **[!UICONTROL 轴]**。
1. 从左侧提要栏底部打开操作，然后单击“ **[!UICONTROL 开始工作流]**”。

   ![开始工作流](assets/start_workflow.png)

1. 选择DAM **[!UICONTROL 智能标记资产工作流]** ，然后为工作流指定标题。
1. 单击 **[!UICONTROL 开始]**。 该工作流会对资产应用您的标记。 导航到资产文件夹并检查标记，以验证智能内容服务是否正确标记了您的资产。 有关详细信息，请参 [阅管理智能标记](managing-smart-tags.md)。

>[!NOTE]
>
>在随后的标记周期中，只有修改后的资产会再次使用经过新培训的标记进行标记。但是，如果标记工作流的上一个标记周期与当前标记周期之间的间隔超过24小时，即使资产未更改也会进行标记。 对于定期标记工作流，当时间间隔超过6个月时，将标记未更改的资产。
