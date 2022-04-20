---
title: 处理任务
seo-title: Working with Tasks
description: 任务是指要对内容完成的工作项，可在项目中使用任务来确定当前任务的完成程度
seo-description: Tasks represent items of work to be done on content and are used in projects to determine the level of completeness of current tasks
uuid: df4efb3f-8298-4159-acfe-305ba6b46791
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 1b79d373-73f4-4228-b309-79e74d191f3e
exl-id: a0719745-8d67-44bc-92ba-9ab07f31f8d2
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 41%

---


# 处理任务 {#working-with-tasks}

任务是指要执行的与内容有关的工作项目。 当有任务分配给您时，它会显示在您的 Workflow 收件箱中。任务项可以根据 **类型** 列。

项目中还会使用任务来确定项目的完整性级别。

## 跟踪项目进度 {#tracking-project-progress}

您可以通过查看项目内由&#x200B;**任务**&#x200B;拼贴表示的活动/已完成任务来跟踪项目进度。项目进度可由以下两项决定：

* **任务拼贴：** 任务拼贴中描述了项目的整体进度，该拼贴位于项目详细信息页面上。

* **任务列表：** 单击任务拼贴时，将显示任务列表。 此列表包含与项目相关的所有任务的详细信息。

这两个选项都列出了工作流任务以及直接在任务拼贴中创建的任务。

### “任务”拼贴 {#task-tile}

如果项目具有任何相关任务，则项目中会显示一个任务拼贴。 任务拼贴显示项目的当前状态。 “任务”拼贴基于工作流内的现有任务，它不包括将来随着工作流的继续执行而生成的任何任务。以下信息会显示在“任务”拼贴中：

* 已完成任务的百分比
* 活动任务的百分比
* 过期任务的百分比

![任务拼贴](assets/project-tile-tasks.png)

### 查看或修改项目中的任务 {#viewing-or-modifying-the-tasks-in-a-project}

除了跟踪进度外，您还可能想要查看有关项目的更多信息或对其进行修改。

#### 任务列表 {#task-list}

单击任务拼贴右下方的省略号按钮，可显示您的收件箱中已筛选到与项目相关的任务。 任务详细信息会与元数据一起显示，例如到期日期、被分派人、优先级和状态。

![项目任务收件箱](assets/project-tasks.png)

#### 任务详细信息 {#task-details}

有关特定任务的更多信息，请在收件箱中，点按或单击该任务以将其选中，然后点按或单击 **打开** 中。

![任务详细信息](assets/project-task-detail.png)

您可以通过不同的选项卡查看、编辑或向任务添加详细信息。

* **任务**  — 一般任务信息
* **项目信息**  — 与任务关联的项目摘要
* **工作流到**  — 与任务关联的工作流的摘要（如果适用）
* **评论**  — 对任务本身的一般性评论

### 添加任务 {#adding-tasks}

您可以将新任务添加到项目中。然后，这些任务会显示在任务拼贴中，并可在通知收件箱中使用，以便您了解未完成的任务。

要添加任务，请执行以下操作：

1. 在项目中，找到 **任务** 拼贴
1. 点按或单击图块右上方的向下V形标记，然后选择 **创建任务**.
1. 在 **添加任务** 窗口，提供任务详细信息，如优先级、被分派人和到期日期。

   ![添加任务](assets/project-add-task.png)

1. 点按或单击 **提交**.

## 在收件箱中处理任务 {#working-with-tasks-in-the-inbox}

您可以直接从收件箱中访问项目任务，而不是从项目本身访问项目任务。 您的收件箱会为您提供跨项目任务的概述，以便您了解整个工作流。

您可以从收件箱中打开任务并设置任务状态。 如果任务被分配到您所属的用户组，则它们也会显示在您的收件箱中。在这种情况下，组内的任何成员都可以执行工作并完成任务。

![收件箱](assets/project-inbox.png)

要完成任务，请选择任务并单击 **完成** 中。 向该任务中添加信息，然后单击&#x200B;**完成**。有关更多信息，请参阅[您的收件箱](/help/sites-authoring/inbox.md)。
