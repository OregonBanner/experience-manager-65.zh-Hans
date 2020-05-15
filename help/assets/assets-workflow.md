---
title: 处理资产以完成业务流程、进行审核、实现法规遵从性并保持基本健全
description: 资产处理功能，可转换格式、创建演绎版、管理资产、验证资产和运行工作流。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 94f7f2cde3c87ed4693b9e2004f80fc5f0cd9855
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 3%

---


# 处理数字资产 {#process-assets}

[!DNL Adobe Experience Manager Assets] 允许您通过多种方式处理数字资产，从而实现强大的资产处理。 您可以使用默认或自定义的处理方法来确保端到端业务流程的完成、审核和合规性、发现和分发，以及数字资产的基本完整性。 您可以在完成资产管理任务的同时实现所需的规模和自定义。

## 了解工作流 {#understand-workflows}

对于资产处理， [!DNL Experience Manager] 请使用工作流。 工作流帮助实现业务逻辑或活动的自动化。 默认情况下，提供完成特定任务的精细步骤，开发人员可以创建自己的自定义步骤。 这些步骤可以按逻辑顺序组合，以创建工作流。 例如，工作流可以根据特定条件对上传的图像应用水印，如上传到的文件夹、图像的分辨率等。 另一个示例是配置为水印和同时添加元数据、创建再现、添加智能标记和发布到数据存储的工作流。

## 默认工作流 [!DNL Experience Manager] {#default-workflows}

默认情况下，所有上传的资产都会使用DAM更 [!UICONTROL 新资产工作流进] 行处理。 该工作流会针对每个上传的资产执行，并实现基本的资产管理任务，如演绎版生成、元数据写回、页面提取、媒体提取和转码。

要查看默认情况下可用的各种工作流模型，请参 **[!UICONTROL 阅中的“工具”>“工作流]** ”>“模型 [!DNL Experience Manager]”。

![部分默认工作流](assets/aem-default-workflows.png)

*图： 中提供的一些默认工作流[!DNL Experience Manager]。*

## 应用工作流处理资产 {#applying-workflows-to-assets}

将工作流应用于数字资产与对网站页面的操作相同。 有关如何创建和使用工作流的完整指南，请参阅 [开始工作流](/help/sites-authoring/workflows-participating.md)。

使用数字资产中的工作流激活资产或创建水印。 资产的许多工作流会自动打开。 例如，编辑图像后自动创建再现的工作流会自动打开。

>[!NOTE]
>
>如果经典UI中可用的工作流在触屏优化UI中不可用， [!UICONTROL 如请求激活][!UICONTROL 和请求取消激活]，请参 [阅建立工作流模型](/help/sites-developing/workflows-models.md#classic2touchui)。

## 将工作流应用于资产 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
要将工作流应用于资产，请执行以下步骤：

1. 导航到您要为其开始工作流的资产所在的位置，然后单击资产以打开资产页面。 从菜 **[!UICONTROL 单中选择]** “时间轴”以显示时间轴。

   ![时间线-1](assets/timeline.png)

1. 单击 **[!UICONTROL 底部的]** “操作”以打开资产可用的操作列表。

1. 单击 **[!UICONTROL 开始]** 中的列表工作流。

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-254](assets/chlimage_1-50.png)

1. （可选）指定可用于引用工作流实例的工作流的标题。

   ![chlimage_1-255](assets/chlimage_1-51.png)

1. 单击 **[!UICONTROL 开始]** ，然后单击 **[!UICONTROL 继续]**。 工作流的每个步骤都会作为事件显示在时间轴中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 将工作流应用于多个资产 {#applying-a-workflow-to-multiple-assets}

1. 从“资产”控制台中，导航到您要为其开始工作流的资产所在的位置，然后选择资产。 从菜 **[!UICONTROL 单中选择]** “时间轴”以显示时间轴。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 单击 **[!UICONTROL 底部的]** “操作”。

   ![chlimage_1-30](assets/chlimage_1-137.png)

1. 单击 **[!UICONTROL 开始工作流]**。 In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. （可选）指定工作流的标题，该标题可用于引用工作流实例。
1. 单击 **[!UICONTROL 开始]** ，然后在对话 **[!UICONTROL 框中单击确]** 认。 该工作流会在您选择的所有资产上运行。

## 将工作流应用于多个文件夹 {#applying-a-workflow-to-multiple-folders}

将工作流应用到多个文件夹的过程与将工作流应用到多个资产的过程类似。 在界面中选择文 [!DNL Assets] 件夹，然后执行将工作流应用于多 [个资产的过程步骤2-7](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)。

## 将工作流应用于集合 {#applying-a-workflow-to-a-collection}

请参 [阅对集合应用工作流](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection)。

## 自动开始工作流以有条件地处理资产 {#auto-execute-workflow-on-some-assets}

管理员可以配置工作流，以根据预定义的条件自动执行和处理资产。 该功能对业务主管用户和营销人员非常有用，例如，在特定文件夹上创建自定义工作流。 假定机构照片拍摄的所有资产都可以水印，或者自由职业者上传的所有资产都可以处理，以创建特定的演绎版。

对于工作流模型，用户可以创建执行该模型的工作流启动器。 工作流启动器监视内容存储库中的更改，并在满足预定义条件时执行工作流。 管理员可以向营销人员提供创建工作流和配置启动器的权限。 用户可以修改默认的 [!UICONTROL DAM更新资产工作流] ，以添加处理特定资产所需的额外步骤。 此工作流会对所有新上传的资产执行。 使用以下方法之一限制特定资产上额外步骤的执行：

* 制作DAM更新资产工 [!UICONTROL 作流的副本] ，并对其进行修改以在特定文件夹层次结构上执行。 此方法对于一些文件夹很有用。
* 可以使用“或”拆分(按条件 [适用](/help/sites-developing/workflows-step-ref.md#or-split) )来添加额外的处理步骤，以根据需要将其拆分为任意多个文件夹。

## 最佳实践和限制 {#best-practices-limitations-tips}

* 设计工作流时，请考虑您对所有类型再现的需求。 如果您不认为将来需要再现，请从工作流中删除其创建步骤。 之后无法批量删除演绎版。 长期使用后，不需要的再现可能占用大量存储空间 [!DNL Experience Manager]。 对于单个资产，您可以从用户界面手动删除演绎版。 对于多个资产，您可以自定 [!DNL Experience Manager] 义删除特定演绎版，也可以删除资产，然后再次上传这些资产。

>[!MORELIKETHIS]
>
>* [申请并参与工作流](/help/sites-authoring/workflows.md)
>* [创建工作流模型并扩展工作流功能](/help/sites-developing/workflows.md)
>* [执行工作流的方法](/help/sites-administering/workflows-starting.md)
>* [工作流程最佳实践](/help/sites-developing/workflows-best-practices.md)
>* [关于使用工作流修改资产的社区文章](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)

