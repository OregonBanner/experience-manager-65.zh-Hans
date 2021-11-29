---
title: 创建内容片段模型无头快速入门指南
description: 使用AEM无标题功能通过内容片段模型定义您将创建和提供的内容的结构。
exl-id: 8e3e4d00-34d3-4d4f-bc3a-43b8a322b986
source-git-commit: a5cb385aa369a5e59889e77597119358b77b55be
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# 创建内容片段模型无头快速入门指南 {#creating-content-fragment-models}

使用AEM无标题功能通过内容片段模型定义您将创建和提供的内容的结构。

## 什么是内容片段模型？ {#what-are-content-fragment-models}

[现在您已创建配置，](create-configuration.md) 您可以使用它创建内容片段模型。

内容片段模型定义要在AEM中创建和管理的数据和内容的结构。 它们是你内容的脚手架。 选择创建内容时，作者将从您定义的内容片段模型中进行选择，这将指导他们创建内容。

## 如何创建内容片段模型 {#how-to-create-a-content-fragment-model}

信息架构师只有在需要新模型时才偶尔执行这些任务。 在本快速入门指南中，我们只需创建一个模型。

1. 登录AEM，然后从主菜单中选择 **工具 — >资产 — >内容片段模型**.
1. 点按或单击通过创建配置所创建的文件夹。

   ![模型文件夹](../assets/models-folder.png)
1. 点按或单击&#x200B;**创建**。
1. 提供 **模型标题**, **标记** 和 **描述**. 您还可以选择/取消选择 **启用模型** 以控制创建时是否立即启用模型。

   ![创建模型](../assets/models-create.png)
1. 在确认窗口中，点按或单击 **打开** 来配置模型。

   ![确认窗口](../assets/models-confirmation.png)
1. 使用 **内容片段模型编辑器**，通过拖放 **数据类型** 列。

   ![拖放字段](../assets/models-drag-and-drop.png)

1. 放置字段后，必须配置其属性。 编辑器将自动切换到 **属性** 选项卡，您可以在其中提供必填字段。

   ![配置属性](../assets/models-configure-properties.png)
1. 完成模型构建后，点按或单击 **保存**.

1. 新创建模型的模式取决于您是否选择了 **启用模型** 创建模型时：
   * 已选 — 新模型将已 **已启用**
   * 未选中 — 将在 **草稿** 模式

1. 如果尚未启用，则模型必须为 **已启用** 以便使用它。
   1. 选择之前创建的模型，然后点按或单击 **启用**.

      ![启用模型](../assets/models-enable.png)
   1. 通过点按或单击确认启用模型 **启用** 在确认对话框中。

      ![启用确认对话框](../assets/models-enabling.png)
1. 模型现已启用并可供使用。

   ![已启用模型](../assets/models-enabled.png)

的 **内容片段模型编辑器** 支持许多不同的数据类型，例如简单文本字段、资产引用、对其他模型的引用和JSON数据。

您可以创建多个模型。 模型可以引用其他内容片段。 使用 [配置](create-configuration.md) 来组织模型。

## 后续步骤 {#next-steps}

现在，您已通过创建模型来定义内容片段的结构，接下来可以转到入门指南的第三部分和 [创建文件夹，以便您自己存储片段。](create-assets-folder.md)

>[!TIP]
>
>有关内容片段模型的完整详细信息，请参阅 [内容片段模型文档](/help/assets/content-fragments/content-fragments-models.md)
