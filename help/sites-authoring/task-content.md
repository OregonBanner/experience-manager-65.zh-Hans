---
title: 处理任务
seo-title: 处理任务
description: 任务是指要对内容完成的工作项，可在项目中使用任务来确定当前任务的完成程度
seo-description: 任务是指要对内容完成的工作项，可在项目中使用任务来确定当前任务的完成程度
uuid: df4efb3f-8298-4159-acfe-305ba6b46791
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 1b79d373-73f4-4228-b309-79e74d191f3e
translation-type: tm+mt
source-git-commit: e3f1c932a5937e8a115e2849935b8f5ea5c2613d
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 98%

---


# 处理任务{#working-with-tasks}

任务是指要对内容完成的工作项。当有任务分配给您时，它会显示在您的 Workflow 收件箱中。任务项目在“类型”列中有一个任务值。

项目中也会使用任务来确定当前任务的完成程度，包括工作流任务。

## 跟踪项目进度  {#tracking-project-progress}

您可以通过查看项目内由&#x200B;**任务**&#x200B;拼贴表示的活动/已完成任务来跟踪项目进度。项目进度可由以下两项决定：

* **任务拼贴：**&#x200B;项目详细信息页面上的“任务拼贴”中描述了项目的整体进度。

* **任务列表：**&#x200B;单击“任务拼贴”时，将显示任务列表。此列表包含与项目相关的所有任务的详细信息。

这两项均列出了工作流任务以及您直接在&#x200B;**任务**&#x200B;拼贴中创建的任务。

### “任务”拼贴  {#task-tile}

如果项目具有任何相关任务，项目内部会显示一个“任务”拼贴。“任务”拼贴显示了项目的当前状态。“任务”拼贴基于工作流内的现有任务，它不包括将来随着工作流的继续执行而生成的任何任务。以下信息会显示在“任务”拼贴中：

* 已完成任务的百分比
* 活动任务的百分比
* 过期任务的百分比

![chlimage_1-98](assets/chlimage_1-98a.png)

### 查看或修改项目中的任务 {#viewing-or-modifying-the-tasks-in-a-project}

除了跟踪进度外，您还可能想要查看有关项目的更多信息或对其进行修改。

#### 任务列表  {#task-list}

单击“任务”拼贴中的省略号 (...) 可显示与项目相关的任务列表。这些任务按父工作流进行划分。任务详细信息会与元数据一起显示，例如到期日期、被分派人、优先级和状态。

![chlimage_1-99](assets/chlimage_1-99a.png)

#### 任务详细信息 {#task-details}

要查看特定任务的更多信息，请点按/单击任务列表中的任务，此时会打开&#x200B;**任务详细信息**。

![chlimage_1-100](assets/chlimage_1-100a.png)

### 查看和修改任务评论 {#viewing-and-modifying-task-comments}

在任务详细信息中，您可以编辑或添加评论。此外，项目中的所有评论都会显示在“评论”区域。

![chlimage_1-101](assets/chlimage_1-101a.png)

### 添加任务 {#adding-tasks}

您可以将新任务添加到项目中。之后，这些任务便会出现在“任务”拼贴中，并且还会显示在“通知”收件箱中以供对其执行操作。

要添加任务，请执行以下操作：

1. 在项目的任务拼贴 **中** ，点按／单击+图标。 此时将 **打开“添加任务** ”窗口。
1. 输入有关该任务的信息。必须填写任务的标题以及要将任务分配到的组。可选填其他信息，例如内容路径、描述、任务优先级和到期日期。另外，您还可以选择&#x200B;**高级**&#x200B;选项卡来输入任务的名称，该名称用于命名 URL。

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 点按/单击&#x200B;**创建**。

## 在收件箱中处理任务  {#working-with-tasks-in-the-inbox}

访问任务的另一种方式是使用收件箱。您可以在收件箱中打开内容以实施必需的更改。完成此操作后，将任务状态设置为“已完成”。如果任务被分配到您所属的用户组，则它们也会显示在您的收件箱中。在这种情况下，组内的任何成员都可以执行工作并完成任务。

![chlimage_1-103](assets/chlimage_1-103a.png)

要完成任务，请选择相应的任务并单击&#x200B;**完成**。向该任务中添加信息，然后单击&#x200B;**完成**。有关更多信息，请参阅[您的收件箱](/help/sites-authoring/inbox.md)。

![chlimage_1-104](assets/chlimage_1-104.png)