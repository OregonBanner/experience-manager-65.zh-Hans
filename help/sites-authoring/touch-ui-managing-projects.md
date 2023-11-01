---
title: 管理项目
seo-title: Managing Projects
description: 通过“项目”，您可以将资源分组到一个实体中，以便在“项目”控制台中对其进行访问和管理，从而组织项目
seo-description: Projects lets you organize your project by grouping resources into one entity which can be acessed and managed intheProjects console
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
exl-id: 62586c8e-dab4-4be9-a44a-2c072effe3c0
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 23%

---


# 管理项目 {#managing-projects}

在 **项目** 控制台，您可以访问和管理您的项目。

![“项目”控制台](assets/projects-console.png)

使用该控制台，您可以创建项目、将资源与项目关联，还可以删除项目或资源链接。

## 访问要求 {#access-requirements}

项目实施标准的AEM功能，无需任何其他设置。

但是，对于项目中的用户，如果要在使用项目（如在创建项目、创建任务/工作流或查看和管理团队时）时查看其他用户/组，这些用户需要拥有读取权限 `/home/users` 和 `/home/groups`.

最简单的方法是给出 **projects — 用户** 对的组读取访问权限 `/home/users` 和 `/home/groups`.

## 创建项目 {#creating-a-project}

按照以下步骤创建新项目。

1. 在 **项目** 控制台，点按或单击 **创建** 以打开 **创建项目** 向导。
1. 选择模板并单击&#x200B;**下一步**。您可以了解有关标准项目模板的更多信息 [此处。](/help/sites-authoring/projects.md#project-templates)

   ![创建项目向导](assets/create-project-wizard.png)

1. 定义&#x200B;**标题**&#x200B;和&#x200B;**描述**，然后根据需要添加&#x200B;**缩略图**&#x200B;图像。您还可以添加或删除用户以及他们所属的组。

   ![向导的“属性”步骤](assets/create-project-wizard-properties.png)

1. 点按/单击&#x200B;**创建**。确认对话框会询问您是要打开新项目还是要返回到控制台。

对于所有项目模板，创建项目的过程都是相同的。 项目类型之间的差异与可用有关 [用户角色](/help/sites-authoring/projects.md) 和 [工作流。](/help/sites-authoring/projects-with-workflows.md)

### 将资源与项目关联 {#associating-resources-with-your-project}

通过项目，可将资源分组到一个实体中以对其进行整体管理。 因此，您需要将资源关联到项目。 这些资源在项目中分组为 **磁贴**. 有关可添加的资源类型的说明，请参阅[项目拼贴](/help/sites-authoring/projects.md#project-tiles)。

要将资源与项目关联，请执行以下操作：

1. 从&#x200B;**项目**&#x200B;控制台中打开您的项目。
1. 点按/单击&#x200B;**添加拼贴**，然后选择您要链接到项目的拼贴。您可以选择多种类型的拼贴。

   ![添加拼贴](assets/project-add-tile.png)

1. 点按/单击&#x200B;**创建**。您的资源随即会链接到项目，从现在开始，您便可以从项目中访问该资源。

### 向拼贴中添加一些项 {#adding-items-to-a-tile}

在某些拼贴中，您可能想要添加多个项。例如，您可能会一次运行多个工作流或多个体验。

要将项目添加到拼贴，请执行以下操作：

1. 在 **项目**，导航到相应的项目，然后单击要将项目添加到的拼贴右上角的向下V形图标并选择相应的选项。

   * 选项取决于图块的类型。 例如，它可能 **创建任务** 对于 **任务** 平铺或 **启动工作流** 对于 **工作流** 磁贴。

   ![平铺V形](assets/project-tile-create-task.png)

1. 像创建新拼贴时一样将项目添加到拼贴。 描述了项目拼贴 [此处。](/help/sites-authoring/projects.md#project-tiles)

## 查看项目信息 {#viewing-project-info}

项目的主要目的是将关联信息分组到一个位置，使其更易于访问和操作。 您可以通过多种方式访问此信息。

### 打开拼贴 {#opening-a-tile}

您可能想要查看当前拼贴中包含的各个项，或者修改或删除拼贴中的一些项。

要打开拼贴，以便查看其中的各个项或修改一些项，请执行以下操作：

1. 点按或单击图块右下方的省略号图标。

   ![“任务”拼贴](assets/project-tile-tasks.png)

1. AEM将打开控制台，显示与拼贴关联的项目类型，并根据所选项目筛选条件。

   ![项目任务](assets/project-tasks.png)

### 查看项目时间线 {#viewing-a-project-timeline}

项目时间线提供了项目中的资源上次使用时间的相关信息。要查看项目时间线，请执行以下步骤。

1. 在 **项目** 控制台，单击或点按 **时间线** 位于控制台左上角的边栏选择器中。
   ![选择时间轴模式](assets/projects-timeline-rail.png)
2. 在控制台中，选择要查看其时间线的项目。
   ![项目时间线视图](assets/project-timeline-view.png)

资产会显示在边栏中。 完成后，使用边栏选择器返回到普通视图。

### 查看不活动的项目 {#viewing-active-inactive-projects}

要在活动状态与之间切换，请执行以下操作 [不活动的项目，](#making-projects-inactive-or-active) 在 **项目** 控制台，单击 **切换活动项目** 图标。

![“切换活动项目”图标](assets/projects-toggle-active.png)

默认情况下，控制台显示活动的项目。 单击 **切换活动项目** 图标一次，以切换到查看不活动的项目。 再次单击可切换回活动项目。

## 组织项目 {#organizing-projects}

有几个选项可以帮助组织您的项目以保持 **项目** 控制台可管理。

### 项目文件夹 {#project-folders}

您可以在中创建文件夹 **项目** 控制台来分组和组织类似项目。

1. 在 **项目** 控制台点按或单击 **创建** 然后 **创建文件夹**.

   ![创建文件夹](assets/project-create-folder.png)

1. 为文件夹提供一个标题，然后单击 **创建**.

1. 该文件夹即添加到控制台。

您现在可以在文件夹中创建项目。 可以创建多个文件夹并嵌套文件夹。

### 正在停用项目 {#making-projects-inactive-or-active}

如果项目已完成，您可能希望将其标记为非活动状态，但仍希望保留有关该项目的信息。 [现在不显示不活动的项目](#viewing-active-inactive-projects) 默认情况下，在 **项目** 控制台。

要使项目处于非活动状态，请执行以下步骤。

1. 打开 **项目属性** 窗口。
   * 您可以从控制台中选择项目，或者从项目中通过 **项目信息** 磁贴。
1. 在 **项目属性** 窗口，更改 **项目状态** 滑块来源 **活动** 到 **不活动**.

   ![属性窗口中的项目状态选择器](assets/project-status.png)

1. 点击或单击 **保存并关闭** 以保存更改。

### 删除项目 {#deleting-a-project}

按照以下步骤删除项目。

1. 导航到 **项目** 控制台。
1. 在控制台中选择您的项目。
1. 点击或单击 **删除** 工具栏中。
1. 删除项目时，AEM可以删除/修改关联的项目数据。 选择您需要在以下位置使用的选项： **删除项目** 对话框。
   * 删除项目组和角色
   * 删除项目资源文件夹
   * 终止项目工作流

   ![项目删除选项](assets/project-delete-options.png)
1. 点击或单击 **删除** 以删除选定的项目。

要了解有关项目自动创建的组的更多信息，请参阅 [自动组创建](/help/sites-authoring/projects.md#auto-group-creation) 以了解详细信息。
