---
title: 创建内容片段模型Headless快速入门指南
description: 定义您创建的内容的结构，并使用内容片段模型通过Adobe Experience Manager (AEM) Headless功能提供内容。
exl-id: 653e35c9-7b6a-49ae-b55d-af2ec40e257d
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 55%

---

# 创建内容片段模型Headless快速入门指南 {#creating-content-fragment-models}

定义您创建的内容的结构，并使用内容片段模型通过Adobe Experience Manager (AEM) Headless功能提供内容。

## 什么是内容片段模型？ {#what-are-content-fragment-models}

[现在您已经创建了配置，](create-configuration.md)您可以用它来创建内容片段模型。

内容片段模型定义您在 AEM 中创建和管理的数据及内容的结构。它们在某种程度上用作内容的基架。选择创建内容时，作者将从您定义的内容片段模型中选择，这会引导他们创建内容。

## 如何创建内容片段模型 {#how-to-create-a-content-fragment-model}

信息架构师只会在偶尔需要新模型时执行这些任务。对于本指南快速入门，您只创建一个模型。

1. 登录AEM，从主菜单选择 **工具 — >资产 — >内容片段模型**.
1. 点按或单击通过创建配置生成的文件夹。

   ![模型文件夹 ](assets/models-folder.png)
1. 点按或单击&#x200B;**创建**。
1. 提供 **模型标题**， **标记**、和 **描述**. 您还可以选择/取消选择&#x200B;**启用模型**&#x200B;以控制模型是否在创建后立即启用。

   ![创建模型](assets/models-create.png)
1. 在确认窗口中，点按或单击&#x200B;**打开**&#x200B;以配置模型。

   ![确认窗口](assets/models-confirmation.png)
1. 使用&#x200B;**内容片段模型编辑器**，通过从&#x200B;**数据类型**&#x200B;列拖放字段来构建内容片段模型。

   ![拖放字段](assets/models-drag-and-drop.png)

1. 放置字段之后必须配置其属性。编辑器会自动切换到 **属性** 用于已添加字段的选项卡，您可以在其中提供必填字段。

   ![配置属性](assets/models-configure-properties.png)
1. 当您完成模型构建之后，点按或单击&#x200B;**保存**。

1. 新创建模型的模式取决于您在创建模型时是否选择了&#x200B;**启用模型**：
   * 选择 — 新模型已为 **已启用**
   * 未选择 – 新模型会以&#x200B;**草稿**&#x200B;模式创建

1. 如果尚未启用，则模型必须&#x200B;**启用**&#x200B;才能使用。
   1. 选择您创建的模型，然后点按或单击 **启用**.

      ![启用模型](assets/models-enable.png)
   1. 通过在确认对话框中点按或单击&#x200B;**启用**&#x200B;来确认启用模型。

      ![启用确认对话框](assets/models-enabling.png)
1. 模型现在已启用，可以使用。

   ![模型已启用](assets/models-enabled.png)

此 **内容片段模型编辑器** 支持许多不同的数据类型，例如简单文本字段、资产引用、引用其他模型和JSON数据。

您可以创建多个模型。模型可以引用其他内容片段。使用[配置](create-configuration.md)可组织您的模型。

## 后续步骤 {#next-steps}

现在，您已通过创建模型定义了内容片段的结构，您可以转到快速入门指南的第三部分并 [创建用于存储片段的文件夹。](create-assets-folder.md)

>[!TIP]
>
>有关内容片段模型的完整详细信息，请参阅 [内容片段模型文档](/help/assets/content-fragments/content-fragments-models.md)
