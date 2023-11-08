---
title: 使用工作流处理资源
description: 资源处理，用于转换格式、创建演绎版、管理资源、验证资源和运行工作流。
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 2%

---

# 处理数字资产 {#process-assets}

[!DNL Adobe Experience Manager Assets] 让您可通过多种方式处理数字资产，从而实现强大的资产处理。 您可以使用默认或自定义的处理方法来确保端到端业务流程的完成、审核和法规遵从性、发现和分发，以及数字资产的基本健全性。 您可以在实现所需的扩展和自定义的同时执行资源管理任务。

## 了解工作流 {#understand-workflows}

对于资产处理， [!DNL Experience Manager] 使用工作流。 工作流有助于自动执行一个或多个业务逻辑。 默认情况下，提供了完成特定任务的精细步骤，开发人员可以创建自己的自定义步骤。 这些步骤可以按逻辑顺序组合以创建工作流。 例如，工作流可以根据特定条件对已上传的图像应用水印，例如将其上传到的文件夹、图像分辨率等。 另一个示例是配置为给元数据添加水印并同时添加元数据、创建演绎版、添加智能标记和发布到数据存储的工作流。

## 默认工作流在以下位置提供： [!DNL Experience Manager] {#default-workflows}

默认情况下，使用处理所有上传的资源 [!UICONTROL DAM更新资产] 工作流。 该工作流会为每个上传的资源执行，并完成基本资源管理任务，例如演绎版生成、元数据写回、页面提取、媒体提取和转码。

要查看默认可用的各种工作流模型，请参阅 **[!UICONTROL “工具”>“工作流”>“模型”]** 在 [!DNL Experience Manager].

![部分默认工作流](assets/aem-default-workflows.png)

*图：中提供的某些默认工作流 [!DNL Experience Manager].*

## 应用工作流以处理资产 {#applying-workflows-to-assets}

将工作流应用于数字资产与应用于网站页面相同。 有关如何创建和使用工作流的完整指南，请参阅 [开始工作流](/help/sites-authoring/workflows-participating.md).

在数字资产中使用工作流来激活资产或创建水印。 资产的许多工作流都会自动打开。 例如，会自动打开在编辑图像后自动创建演绎版的工作流。

>[!NOTE]
>
>如果经典UI中可用的工作流在触屏UI中不可用，例如 [!UICONTROL 请求激活] 和 [!UICONTROL 请求停用]，请参见 [创建工作流模型](/help/sites-developing/workflows-models.md#classic2touchui).

## 将工作流应用于资产 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
要将工作流应用于资产，请执行以下步骤：

1. 导航到要启动工作流的资产位置，然后单击该资产以打开资产页面。 选择 **[!UICONTROL 时间线]** 从菜单以显示时间轴。

   ![时间轴–1](assets/timeline.png)

1. 单击 **[!UICONTROL 操作]** 以打开资产可用的操作列表。

1. 单击 **[!UICONTROL 启动工作流]** 从名单上。

1. 在 **[!UICONTROL 启动工作流]** 对话框中，从列表中选择工作流模型。

1. （可选）指定可用于引用工作流实例的工作流标题。

   ![选择工作流，提供标题，然后单击“开始”](assets/start-workflow.png)

1. 单击 **[!UICONTROL 开始]** 然后单击 **[!UICONTROL 继续]**. 工作流的每个步骤都会作为事件显示在时间轴中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 将工作流应用于多个资产 {#applying-a-workflow-to-multiple-assets}

1. 从 [!DNL Assets] 在控制台中，导航到要启动工作流的资产位置，然后选择资产。 选择 **[!UICONTROL 时间线]** 从菜单以显示时间轴。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 单击 **[!UICONTROL 操作]** ![V形向上](assets/do-not-localize/chevron-up-icon.png) 在底部。
1. 单击 **[!UICONTROL 启动工作流]**. 在 **[!UICONTROL 启动工作流]** 对话框中，从列表中选择工作流模型。

   ![启动工作流](assets/start-workflow.png)

1. （可选）指定工作流的标题，该标题可用于引用工作流实例。
1. 单击 **[!UICONTROL 开始]** ，然后在对话 **[!UICONTROL 框中单击确]** 认。 该工作流会在您选择的所有资产上运行。

## 将工作流应用于多个文件夹 {#applying-a-workflow-to-multiple-folders}

将工作流应用于多个文件夹的过程与将工作流应用于多个资产的过程类似。 选择中的文件夹 [!DNL Assets] 界面，然后执行过程中的步骤2-7 [将工作流应用于多个资产](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## 将工作流应用于收藏集 {#applying-a-workflow-to-a-collection}

请参阅 [对收藏集应用工作流](/help/assets/manage-collections.md#running-a-workflow-on-a-collection).

## 自动启动工作流以有条件地处理资产 {#auto-execute-workflow-on-some-assets}

管理员可以配置工作流以根据预定义条件自动执行和处理资源。 此功能对于业务线用户和营销人员非常有用，例如在特定文件夹上创建自定义工作流。 假设某个机构照片拍摄的所有资产都可以添加水印，或者自由职业者上传的所有资产都可以经过处理以创建特定演绎版。

对于工作流模型，用户可以创建用于执行该模型的工作流启动器。 工作流启动器监视内容存储库中的更改，并在满足预定义条件时执行工作流。 管理员可以向营销人员提供创建工作流和配置启动器的访问权限。 用户可以修改默认值 [!UICONTROL DAM更新资产] 工作流中添加处理特定资产所需的额外步骤。 该工作流将在所有新上传的资源上执行。 使用以下方法之一来限制对特定资源执行额外的步骤：

* 复制 [!UICONTROL DAM更新资产] 工作流并对其进行修改，使其在特定文件夹层次结构上执行。 这种方法对于几个文件夹很有用。
* 可以使用添加额外的处理步骤 [OR拆分](/help/sites-developing/workflows-step-ref.md#or-split) 适用于所需数量的文件夹。

## 最佳实践和限制 {#best-practices-limitations-tips}

* 在设计工作流时，请考虑您对所有类型的演绎版的需求。 如果您预计将来不需要节目，请从工作流中删除其创建步骤。 之后无法批量删除节目。 长期使用后，不需要的演绎版可能会占用存储空间 [!DNL Experience Manager]. 对于单个资源，您可以从用户界面手动删除演绎版。 对于多个资源，您可以进行自定义 [!DNL Experience Manager] 以删除特定演绎版或删除资源，然后再次上传这些资源。
* 默认情况下， [!UICONTROL DAM更新资产] 工作流包括创建缩略图和Web呈现的一些步骤。 如果从工作流中删除了任何默认呈现版本，则其用户界面 [!DNL Assets] 无法正确呈现。

>[!MORELIKETHIS]
>
>* [应用和参与工作流](/help/sites-authoring/workflows.md)
>* [创建工作流模型和扩展工作流功能](/help/sites-developing/workflows.md)
>* [执行工作流的方法](/help/sites-administering/workflows-starting.md)
>* [工作流最佳实践](/help/sites-developing/workflows-best-practices.md)
