---
title: 增强型智能标记
description: 增强型智能标记
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 1%

---

# 了解、应用和策划智能标记 {#enhanced-smart-tags}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=en) |
| AEM 6.5 | 本文 |

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包括员工、合作伙伴和客户通常用于引用和搜索特定类的数字资产的关键字列表。 使用分类控制的词汇标记资产可确保轻松识别和检索资产。

与自然语言词汇相比，根据业务分类标记数字资产有助于使其与公司的业务保持一致，并确保最相关的资产出现在搜索中。

例如，汽车制造商可以使用型号名称标记汽车图像，以便在搜索各种型号的图像以设计促销活动时只显示相关图像。

要使智能内容服务应用正确的标记，请对其进行培训以识别您的分类。 要培训该服务，首先要策划一组最能描述这些资源的资源和标记。 为帮助该服务学习，请在资产上应用这些标记并运行培训工作流。

标记经过培训并准备就绪后，该服务现在可以通过标记工作流将这些标记应用于资产。

在后台，智能内容服务使用Adobe Sensei AI框架根据您的标记结构和业务分类培训其图像识别算法。 然后，可使用此内容智能在不同资产集上应用相关标记。

智能内容服务是一个托管在上的云服务 [!DNL Adobe Developer Console]. 在中使用 [!DNL Adobe Experience Manager]，系统管理员必须集成 [!DNL Experience Manager] 部署 [!DNL Adobe Developer Console].

总之，以下是使用“智能内容服务”的主要步骤：

* 入门培训
* 审查资产和标记（分类定义）
* 培训智能内容服务
* 自动标记

![流程图](assets/flowchart.gif)

## 先决条件和支持的格式 {#prerequisites}

在使用智能内容服务之前，请确保满足以下条件以在其上创建集成 [!DNL Adobe Developer Console]：

* 具有组织管理员权限的Adobe ID帐户。
* 为您的组织启用智能内容服务服务。
* 要将Smart Content Services基本包添加到部署，请许可 [!DNL Adobe Experience Manager Sites] 基本包和 [!DNL Assets] 加载项。

该服务将智能标记应用于以下MIME类型的资产：

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

该服务将智能标记应用于以下MIME类型的资产演绎版：

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## 入门培训 {#onboarding}

智能内容服务可作为的加载项购买 [!DNL Experience Manager]. 购买后，会向贵组织的管理员发送一封电子邮件，其中包含指向的链接 [!DNL Adobe I/O].

管理员可以按照链接操作，将智能内容服务与集成 [!DNL Experience Manager]. 要将服务与集成，请执行以下操作 [!DNL Experience Manager Assets]，请参见 [配置智能标记](config-smart-tagging.md).

管理员配置服务并将用户添加到时，载入流程即完成 [!DNL Experience Manager].

## 查看资源和标记 {#reviewing-assets-and-tags}

在您加入后，您首先要做的是确定一组最适合您在业务环境中描述这些图像的标记。

接下来，查看图像以确定最能代表您的产品以满足特定业务需求的一组图像。 确保策划集中的资产符合 [智能内容服务培训准则](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

将资源添加到文件夹，并从属性页面将标记应用于每个资源。 然后，在此文件夹上运行培训工作流。 策划的资产集使智能内容服务能够使用您的分类定义有效地培训更多资产。

>[!NOTE]
>
>1. 培训是一个不可撤消的过程。 Adobe建议您在对智能内容服务进行标记培训之前，查看策划的资源集中的标记。
>1. 在对标记进行培训之前，请参阅 [智能内容服务培训准则](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. 首次培训智能内容服务时，Adobe建议您至少在两个不同的标签上对其进行培训。


## 了解 [!DNL Experience Manager] 包含智能标记的搜索结果 {#understandsearch}

默认情况下， [!DNL Experience Manager] 搜索将搜索词与 `AND` 子句。 使用智能标记不会更改此默认行为。 使用智能标记会额外添加 `OR` 子句查找与智能标记相关的任何搜索词。 例如，考虑搜索 `woman running`. 具有的资产 `woman` 或只是 `running` 默认情况下，元数据中的关键字不会出现在搜索结果中。 但是，使用任一标记进行标记的资产 `woman` 或 `running` 使用智能标记会出现在此类搜索查询中。 所以搜索结果是，

* 具有的资产 `woman` 和 `running` 元数据中的关键字。

* 使用任一关键字智能标记的资产。

首先显示与元数据字段中的所有搜索词匹配的搜索结果，随后显示与智能标记中的任何搜索词匹配的搜索结果。 在上例中，搜索结果的大致显示顺序为：

1. 匹配项 `woman running` 在各个元数据字段中。
1. 匹配项 `woman running` 在智能标记中。
1. 匹配项 `woman` 或 `running` 在智能标记中。

>[!CAUTION]
>
>如果Lucene索引完成于 [!DNL Adobe Experience Manager]，则基于智能标记的搜索无法按预期工作。

## 自动标记资产 {#tagging-assets-automatically}

在培训了智能内容服务后，您可以触发标记工作流，以自动将适当的标记应用于一组不同的类似资产。

您可以定期或根据需要运行标记工作流。

>[!NOTE]
>
>标记工作流在资源和文件夹上运行。

### 定期标记 {#periodic-tagging}

您可以启用智能内容服务定期标记文件夹中的资产。 打开资产文件夹的属性页面，选择 **[!UICONTROL 启用智能标记]** 在 **[!UICONTROL 详细信息]** 选项卡，并保存更改。

为文件夹选择此选项后，智能内容服务将自动标记文件夹中的资产。 默认情况下，标记工作流每天凌晨12:00运行。

### 按需标记 {#on-demand-tagging}

您可以从工作流控制台或时间轴触发标记工作流，以立即标记您的资产。

>[!NOTE]
>
>如果从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。

#### 从工作流控制台中标记资产 {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] 界面，转到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 从 **[!UICONTROL 工作流模型]** 页面上，选择 **[!UICONTROL DAM智能标记资产]** 工作流，然后单击 **[!UICONTROL 启动工作流]** 工具栏中。

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. 在 **[!UICONTROL 运行工作流]** 对话框中，浏览到包含要自动应用标记的资源的有效负荷文件夹。
1. 指定工作流的标题和可选注释。 单击 **[!UICONTROL 运行]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   要验证智能内容服务是否正确标记了您的资产，请导航到资产文件夹并查看标记。

#### 从时间轴标记资产 {#tagging-assets-from-the-timeline}

1. 从 [!DNL Assets] 用户界面上，选择包含要应用智能标记的资产或特定资产的文件夹。
1. 从左上角，打开 **[!UICONTROL 时间线]**.
1. 打开左侧边栏底部的操作，然后单击 **[!UICONTROL 启动工作流]**.

   ![start_workflow](assets/start_workflow.png)

1. 选择 **[!UICONTROL DAM智能标记资产]** 工作流，并指定工作流的标题。
1. 单击 **[!UICONTROL 开始]**. 工作流会将标记应用于资产。 要验证智能内容服务是否正确标记了您的资产，请导航到资产文件夹并查看标记。

>[!NOTE]
>
>在后续标记周期中，只有已修改的资产会再次使用新训练的标记进行标记。 但是，如果标记工作流的最后一个标记周期与当前标记周期之间的间隔超过24小时，则即使未更改资产也会进行标记。 对于定期标记工作流，当时间间隔超过六个月时，会标记未更改的资产。

## 组织或审核应用的智能标记 {#manage-smart-tags}

您可以组织智能标记，以删除分配给品牌图像的任何不准确的标记，以便仅显示最相关的标记。

审核智能标记还可以确保您的图像显示在最相关标记的搜索结果中，从而帮助优化基于标记的图像搜索。 基本上，它有助于消除无关图像出现在搜索结果中的机会。

您还可以为标记分配较高的排名，以提高其与图像的相关性。 提升图像的标记会增加搜索特定标记时，图像出现在搜索结果中的机会。

1. 在搜索框中，使用标记作为关键词搜索资产。
1. 要识别与搜索不相关的图像，请查看搜索结果。
1. 选择图像，然后单击 **[!UICONTROL 管理标记]** 工具栏中。
1. 从 **[!UICONTROL 管理标记]** 页面上，查看标记。 如果不希望根据特定标记搜索图像，请选择该标记，然后单击 **[!UICONTROL 删除]** 工具栏中。 或者，单击 `x` 标记旁边显示的符号。
1. （可选）要向标记分配较高的排名，请选择标记并单击 **[!UICONTROL 提升]** 工具栏中。 您提升的标记将移至 **[!UICONTROL 标记]** 部分。
1. 单击 **[!UICONTROL 保存]** 然后单击 **[!UICONTROL 确定]**
1. 导航到 **[!UICONTROL 属性]** 页面查找图像。 请注意，您提升的标记会获得更多的相关性，并且会更早地显示在搜索结果中。

## 提示和限制 {#tips-best-practices-limitations}

* 要训练模型，请使用最合适的图像。 无法还原训练或无法删除训练模型。 您的标记准确性取决于当前的培训，因此请谨慎操作。
* 智能内容服务的使用限制为每年最多200万张标记图像。 任何经过处理和标记的重复图像均计为已标记的图像。
* 如果从时间轴运行标记工作流，则一次最多可以对15个资产应用标记。
* 智能标记仅适用于PNG和JPG图像格式。 因此，如果支持的资产具有以这两种格式创建的演绎版，则会使用智能标记进行标记。
