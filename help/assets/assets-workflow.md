---
title: 处理资产以完成业务流程、进行审核、实现法规遵从性并保持基本的完整性
description: 资产处理功能，可转换格式、创建演绎版、管理资产、验证资产和运行工作流。
contentOwner: AG
translation-type: tm+mt
source-git-commit: bf291206a8c0e435053fbdba493ad949619ee5b3

---


# 处理数字资产 {#process-assets}

[!DNL Adobe Experience Manager Assets] 允许您通过多种方式处理数字资产，从而实现强大的资产处理。 您可以使用可用的处理方法或扩展这些方法，以确保使用、审核和遵守、发现和分发数字资产以及基本的完整性来完成端到端的业务流程。 您可以在实现所需规模和自定义的同时完成所有这些操作。

## 了解工作流 {#understand-workflows}

对于资产处理，请 [!DNL Experience Manager] 使用工作流。 工作流帮助实现业务逻辑或活动的自动化。 默认情况下，提供完成特定任务的精细步骤，开发人员可以创建自己的自定义步骤。 这些步骤可以按逻辑顺序组合，以创建工作流。 例如，工作流可以根据特定条件（如嵌入到图像中的元数据、上传到的文件夹、图像的分辨率等）对上传的图像自动应用水印。 另一个示例是以这样的方式配置的工作流，以水印图像并同时满足多个资产管理需求，如添加元数据、创建再现、添加智能标记以进行资产发现、发布到数据存储、设置用户访问权限等。

## Experience Manager中的默认工作流 {#default-workflows}

默认情况下，所有上传的资产都会使用 [!UICONTROL DAM更新资产工作流] 。 该工作流对每个上传的资产执行，并实现基本的资产管理任务，如再现生成、元数据写回、页面提取、媒体提取和转码。

要查看默认情况下可用的各种工作流模型，请参 [!UICONTROL 阅中的“工具”>“工作流”] >“模型” [!DNL Experience Manager]。

![部分默认工作流](assets/aem-default-workflows.png)

*图：在Adobe Cloud中，[!DNL Experience Manager]*

## 将工作流应用于处理资产 {#applying-workflows-to-assets}

将工作流应用到数字资产与对网站页面的应用相同。 有关如何创建和使用工作流的完整指南，请参阅 [开始工作流](/help/sites-authoring/workflows-participating.md)。

使用数字资产中的工作流激活资产或创建水印。 资产的许多工作流会自动打开。 例如，编辑图像后自动创建再现的工作流会自动打开。

>[!NOTE]
>
>如果经典UI中可用的工作流在触屏优化UI中不可用，如 [!UICONTROL 请求激活] , [!UICONTROL 请求取消激活]，请参阅 [建立工作流模型](/help/sites-developing/workflows-models.md#classic2touchui)。

## 将工作流应用于资产 {#apply-a-workflow-to-an-asset}

要将工作流应用到资产，请执行以下步骤：

1. 导航到您要为其开始工作流的资产所在的位置，然后单击资产以打开资产页面。 从菜 **[!UICONTROL 单中选择]** “时间轴”以显示时间轴。

   ![时间轴-1](assets/timeline.png)

1. 单 **[!UICONTROL 击底部的]** “操作”以打开资产可用的操作列表。

   ![chlimage_1-252](assets/chlimage_1-45.png)

1. 单击 **[!UICONTROL 开始中的列表]** “工作流”。

   ![chlimage_1-253](assets/chlimage_1-49.png)

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

## 将工作流应用到多个文件夹 {#applying-a-workflow-to-multiple-folders}

将工作流应用到多个文件夹的过程与将工作流应用到多个资产的过程类似。 在“资产”控制台中选择文件夹，然后执行过程中的第2-7步， [将工作流应用到多个资产](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)。

## 将工作流应用于集合 {#applying-a-workflow-to-a-collection}

请参 [阅对集合应用工作流](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection)。

## 自动开始工作流以有条件地处理资产 {#auto-execute-workflow-on-some-assets}

管理员可以配置工作流以根据预定义的条件自动执行和处理资产。 该功能对业务用户和营销人员非常有用，例如，在特定文件夹上创建自定义工作流。 假设机构照片拍摄中的所有资产都可以添加水印，或者自由职业者上传的所有资产都可以处理以创建特定演绎版。

对于工作流模型，用户可以创建启动该模型的工作流启动器。 管理员可以向营销人员提供创建工作流和配置启动器的权限。 用户可以修改默认的 [!UICONTROL DAM更新资产工作流] ，以添加处理特定资产所需的额外步骤。 该工作流会对所有新上传的资产执行，因此，请使用以下方法之一来限制对特定资产执行额外步骤：

* 制作 [!UICONTROL DAM更新资产工作流的副本] ，并将其修改为在特定文件夹层次结构上执行。 此方法对于一些文件夹很有用。
* 可以使用“或”拆分( [OR](/help/sites-developing/workflows-step-ref.md#or-split) split)添加额外的处理步骤，该拆分有条件地适用于所需数量的文件夹。

>[!MORELIKETHIS]
>
>* [申请并参与工作流](/help/sites-authoring/workflows.md)
>* [创建工作流模型并扩展工作流功能](/help/sites-developing/workflows.md)
>* [工作流程最佳实践](/help/sites-developing/workflows-best-practices.md)
>* [关于使用工作流修改资产的社区文章](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)

