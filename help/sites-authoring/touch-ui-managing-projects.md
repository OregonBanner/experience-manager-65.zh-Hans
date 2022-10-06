---
title: 管理项目
seo-title: Managing Projects
description: 通过“项目”，您可以将资源分组到一个实体中来组织项目，该实体可以在“项目”控制台中进行访问和管理
seo-description: Projects lets you organize your project by grouping resources into one entity which can be acessed and managed intheProjects console
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
exl-id: 62586c8e-dab4-4be9-a44a-2c072effe3c0
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 23%

---


# 管理项目 {#managing-projects}

在 **项目** 控制台中，您可以访问和管理项目。

![“项目”控制台](assets/projects-console.png)

使用控制台，您可以创建项目、将资源与项目关联，以及删除项目或资源链接。

## 访问要求 {#access-requirements}

项目是标准的AEM功能，无需任何其他设置。

但是，对于项目中的用户，如果要在使用项目时（例如创建项目、创建任务/工作流或查看和管理团队时）查看其他用户/组，这些用户需要具有 `/home/users` 和 `/home/groups`.

最简单的方法就是 **项目用户** 组读取访问权限 `/home/users` 和 `/home/groups`.

## 创建项目 {#creating-a-project}

按照以下步骤创建新项目。

1. 在 **项目** 控制台，点按或单击 **创建** 打开 **创建项目** 向导。
1. 选择模板并单击&#x200B;**下一步**。您可以进一步了解标准项目模板 [这里。](/help/sites-authoring/projects.md#project-templates)

   ![创建项目向导](assets/create-project-wizard.png)

1. 定义&#x200B;**标题**&#x200B;和&#x200B;**描述**，然后根据需要添加&#x200B;**缩略图**&#x200B;图像。您还可以添加或删除用户以及他们所属的组。

   ![向导的属性步骤](assets/create-project-wizard-properties.png)

1. 点按/单击&#x200B;**创建**。确认对话框会询问您是要打开新项目还是要返回到控制台。

对于所有项目模板，创建项目的过程都是相同的。 项目类型之间的差异与可用 [用户角色](/help/sites-authoring/projects.md) 和 [工作流。](/help/sites-authoring/projects-with-workflows.md)

### 将资源与项目关联 {#associating-resources-with-your-project}

通过项目，您可以将资源分组到一个实体中，以便将它们作为一个整体进行管理。 因此，您需要将资源与项目关联。 这些资源在项目中分组为 **图块**. 有关可添加的资源类型的说明，请参阅[项目拼贴](/help/sites-authoring/projects.md#project-tiles)。

要将资源与项目关联，请执行以下操作：

1. 从&#x200B;**项目**&#x200B;控制台中打开您的项目。
1. 点按/单击&#x200B;**添加拼贴**，然后选择您要链接到项目的拼贴。您可以选择多种类型的拼贴。

   ![添加拼贴](assets/project-add-tile.png)

1. 点按/单击&#x200B;**创建**。您的资源随即会链接到项目，从现在开始，您便可以从项目中访问该资源。

### 向拼贴中添加一些项 {#adding-items-to-a-tile}

在某些拼贴中，您可能想要添加多个项。例如，您可能会一次运行多个工作流或多个体验。

要向图块中添加项目，请执行以下操作：

1. 在 **项目**，导航到项目，然后单击要向其添加项目的图块右上角的向下V形图标，然后选择相应的选项。

   * 选项取决于拼贴的类型。 例如，可能 **创建任务** 对于 **任务** 磁贴或 **启动工作流** 对于 **工作流** 拼贴。

   ![拼贴V形标记](assets/project-tile-create-task.png)

1. 与创建新拼贴时一样，将项目添加到拼贴中。 描述了项目图块 [这里。](/help/sites-authoring/projects.md#project-tiles)

## 查看项目信息 {#viewing-project-info}

项目的主要用途是将相关信息分组到一个位置，使其更易于访问和操作。 您有多种方法可访问此信息。

### 打开拼贴 {#opening-a-tile}

您可能想要查看当前拼贴中包含的各个项，或者修改或删除拼贴中的一些项。

要打开拼贴，以便查看其中的各个项或修改一些项，请执行以下操作：

1. 点按或单击图块右下方的省略号图标。

   ![任务拼贴](assets/project-tile-tasks.png)

1. AEM会打开控制台，显示与图块关联的项目类型以及基于选定项目的过滤器。

   ![项目任务](assets/project-tasks.png)

### 查看项目时间线 {#viewing-a-project-timeline}

项目时间线提供了项目中的资产上次使用时间的相关信息。要查看项目时间轴，请执行以下步骤。

1. 在 **项目** 控制台，单击或点按 **时间轴** 在控制台左上角的边栏选择器中。
   ![选择时间轴模式](assets/projects-timeline-rail.png)
2. 在控制台中，选择要查看其时间轴的项目。
   ![项目时间轴视图](assets/project-timeline-view.png)

资产会显示在边栏中。 使用边栏选择器，在完成后返回到正常视图。

### 查看不活动项目 {#viewing-active-inactive-projects}

在活动和 [不活动项目，](#making-projects-inactive-or-active) 在 **项目** 控制台中，单击 **切换活动项目** 图标。

![切换活动项目图标](assets/projects-toggle-active.png)

默认情况下，控制台会显示活动项目。 单击 **切换活动项目** 图标，以切换到查看不活动项目。 再次单击该图标以切换回活动项目。

## 组织项目 {#organizing-projects}

有几个选项可帮助组织项目以保留 **项目** 控制台可管理。

### 项目文件夹 {#project-folders}

您可以在 **项目** 控制台来分组和组织类似项目。

1. 在 **项目** 控制台点按或单击 **创建** 然后 **创建文件夹**.

   ![创建文件夹](assets/project-create-folder.png)

1. 为文件夹指定标题并单击 **创建**.

1. 文件夹即会添加到控制台中。

您现在可以在文件夹中创建项目。 您可以创建多个文件夹，也可以嵌套文件夹。

### 停用项目 {#making-projects-inactive-or-active}

如果某个项目已完成，但您仍希望保留该项目的相关信息，则可能希望将该项目标记为不活动。 [不活动项目现在显示](#viewing-active-inactive-projects) 默认情况下，在 **项目** 控制台。

要使项目处于不活动状态，请执行以下步骤。

1. 打开 **项目属性** 窗口。
   * 您可以从控制台中选择项目，或从项目中通过 **项目信息** 拼贴。
1. 在 **项目属性** 窗口，更改 **项目状态** 滑块 **活动** to **不活动**.

   ![属性窗口中的项目状态选择器](assets/project-status.png)

1. 点按或单击 **保存并关闭** 以保存更改。

### 删除项目 {#deleting-a-project}

按照以下步骤删除项目。

1. 导航到 **项目** 控制台。
1. 在控制台中选择您的项目。
1. 点按或单击 **删除** 中。
1. AEM可在删除项目时删除/修改关联的项目数据。 选择在 **删除项目** 对话框。
   * 删除项目组和角色
   * 删除项目资产文件夹
   * 终止项目工作流

   ![项目删除选项](assets/project-delete-options.png)
1. 点按或单击 **删除** 以删除选定选项的项目。

要了解有关由项目自动创建的组的更多信息，请参阅 [自动创建组](/help/sites-authoring/projects.md#auto-group-creation) 以了解详细信息。
