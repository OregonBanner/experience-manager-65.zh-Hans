---
title: 参与工作流
description: 工作流通常包括需要人员在页面或资产上执行活动的步骤。 工作流会选择一个用户或组来执行活动，并将工作项分配给该人员或组。
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 9%

---

# 参与工作流{#participating-in-workflows}

工作流通常包括需要人员在页面或资产上执行活动的步骤。 工作流会选择一个用户或组来执行活动，并将工作项分配给该人员或组。

## 处理您的工作项 {#processing-your-work-items}

您可以执行以下操作来处理工作项：

* **完成**

   您可以完成一个项目，以允许工作流进入下一步。

* **委派**

   如果某个步骤已分配给您，但由于任何原因您无法执行操作，则可以将该步骤委派给其他用户或组。

   可以委派的用户取决于分配给谁的工作项：

   * 如果工作项已分配给组，则组成员可用。
   * 如果将工作项分配给某个组，然后该组又将其委派给某个用户，则可以向该组的成员和该组进行委派。
   * 如果工作项分配给单个用户，则无法委派该工作项。

* **回退**

   如果您发现某个步骤或一系列步骤需要重复，则可以回退。 这允许您选择在工作流中较早发生的步骤进行重新处理。 工作流将返回到您指定的步骤，然后从此处继续。

## 参与工作流 {#participating-in-a-workflow}

### 已分配工作流操作通知 {#notifications-of-assigned-workflow-actions}

为您分配了工作项（例如，**批准内容**）后，将显示各种警报和/或通知：

* 此 **状态** 网站控制台的列指示页面何时处于工作流中：

   ![workflowstatus-1](assets/workflowstatus-1.png)

* 当您或您所属的组被指定为工作流的工作项时，该工作项将显示在AEM Workflow收件箱中。

   ![workflowinbox](assets/workflowinbox.png)

### 完成参与者步骤 {#completing-a-participant-step}

执行指示的操作后，您可以完成工作项目，从而允许工作流继续。 请按下列步骤完成工作项目。

1. 选择工作流步骤，然后单击 **完成** 按钮进行导航。
1. 在生成的对话框中，选择 **下一步**；即下一步要执行的步骤。 下拉列表会显示所有相应的目标。 A **注释** 也可以输入。

   ![workflowcomplete](assets/workflowcomplete.png)

   列出的步骤数取决于工作流模型的设计。

1. 单击 **确定** 以确认操作。

### 委派参与者步骤 {#delegating-a-participant-step}

请按下列步骤委派工作项目。

1. 单击 **委派** 按钮进行导航。
1. 在对话框中，使用下拉列表选择 **用户** 以将工作项委派给。 您还可以添加 **注释**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. 单击 **确定** 以确认操作。

### 对参与者步骤执行回退 {#performing-step-back-on-a-participant-step}

请按下列步骤回退。

1. 单击顶部导航栏中的“回退”按钮。
1. 在生成的对话框中，选择“上一步”；即，要执行的下一步 — 即使该步骤出现在工作流的前面。 下拉列表会显示所有相应的目标。

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. 单击确定以确认操作。
