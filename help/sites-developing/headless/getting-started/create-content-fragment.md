---
title: 创建内容片段Headless快速入门指南
description: 了解如何使用 AEM 的内容片段设计、创建、管理和使用独立于页面的内容，用于 Headless 投放。
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 73%

---

# 创建内容片段Headless快速入门指南 {#creating-content-fragments}

了解如何使用 AEM 的内容片段设计、创建、管理和使用独立于页面的内容，用于 Headless 投放。

## 什么是内容片段？ {#what-are-content-fragments}

[现在您已经创建了资源文件夹](create-assets-folder.md)，可以在其中存储您的内容片段，接下来可以创建片段！

内容片段允许您设计、创建、管理和发布独立于页面的内容。 利用这些功能，可准备内容以用于多个位置和多个渠道。

内容片段包含结构化内容，可以采用 JSON 格式投放。

## 如何创建内容片段 {#how-to-create-a-content-fragment}

内容作者将创建任意数量的内容片段，用于呈现他们创建的内容。这将是他们在 AEM 中的主要任务。对于本指南快速入门，我们只需要创建一个。

1. 登录AEM，从主菜单选择 **导航>资产**.
1. 导航至 [之前创建的文件夹。](create-assets-folder.md)
1. 单击 **创建>内容片段**.
1. 内容片段的创建以两步向导的方式呈现。首先，选择要使用哪个模型来创建内容片段，然后单击 **下一个**.
   * 可用的模型取决于&#x200B;[**您为资源文件夹定义的云配置**](create-assets-folder.md)，您将在该文件夹中创建内容片段。
   * 如果您收到消息 `We could not find any models`，请检查资源文件夹的配置。

   ![选择内容片段模型](assets/content-fragment-model-select.png)
1. 提供 **标题**， **描述**、和 **标记** （如有必要）并单击 **创建**.

   ![创建内容片段](assets/content-fragment-create.png)
1. 单击 **打开** 在确认窗口中。

   ![内容片段创建确认](assets/content-fragment-confirmation.png)
1. 在内容片段编辑器中提供内容片段的详细信息。

   ![内容片段编辑器](assets/content-fragment-edit.png)
1. 单击 **保存** 或  **保存并关闭**.

内容片段可以引用其他内容片段，在需要时允许嵌套内容结构。

内容片段还可以引用 AEM 中的其他资源。[这些资源需要存储在 AEM 中](/help/assets/manage-assets.md)，然后才能创建引用内容片段。

## 后续步骤 {#next-steps}

现在您已经创建了内容片段，接下来可以转到快速入门指南的最后一个部分并[创建 API 请求来访问和提供内容片段。](create-api-request.md)

>[!TIP]
>
>有关管理内容片段的完整详细信息，请参阅[内容片段文档](/help/assets/content-fragments/content-fragments.md)
