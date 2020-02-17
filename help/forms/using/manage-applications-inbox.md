---
title: 在AEM收件箱中管理表单应用程序和任务
seo-title: 在AEM收件箱中管理表单应用程序和任务
description: AEM收件箱允许您通过提交应用程序和管理任务来启动以表单为中心的工作流。
seo-description: AEM收件箱允许您通过提交应用程序和管理任务来启动以表单为中心的工作流。
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 在AEM收件箱中管理表单应用程序和任务{#manage-forms-applications-and-tasks-in-aem-inbox}

启动或触发以表单为中心的工作流程的多种方式之一是通过AEM收件箱中的应用程序。 您需要创建一个工作流应用程序，以使表单工作流在收件箱中作为应用程序可用。 有关工作流应用程序和启动表单工作流的其他方式的详细信息，请参 [阅在OSGi上启动以表单为中心的工作流](../../forms/using/aem-forms-workflow.md#launch)。

此外，AEM收件箱还合并了来自各种AEM组件（包括表单工作流）的通知和任务。 当触发包含分配任务步骤的表单工作流时，关联的应用程序将作为任务列在被分派人的收件箱中。 如果被分派人是组，则任务将显示在所有组成员的收件箱中，直到个人请求或委派任务为止。

收件箱用户界面提供列表视图和日历视图以查看任务。 您还可以配置视图设置。 您可以根据各种参数筛选任务。 有关视图和过滤器的详细信息，请参 [阅收件箱](/help/sites-authoring/inbox.md)。

总之，收件箱允许您创建新应用程序并管理分配的任务。

>[!NOTE] {graybox=&quot;true&quot;}
>
>您必须是工作流用户组的成员才能使用AEM收件箱。

## 创建应用程序 {#create-application}

1. 转到https://[server]:[port]/aem/inbox的AEM收件箱。
1. 在收件箱UI中，点按创 **[!UICONTROL 建>应用程序]**。 此时将显示“选择应用程序”页。
1. 选择一个应用程序，然后单击“ **[!UICONTROL 创建]**”。 随即会打开与应用程序关联的自适应表单。 在自适应表单中填写信息，然后点按提 **[!UICONTROL 交]**。 它会启动关联的工作流并在被分派人的收件箱中创建任务。

## 管理任务 {#manage-tasks}

当Forms工作流触发且您是被分派人或被分派人组的一部分时，您的收件箱中会显示一个任务。 您可以从收件箱中查看任务详细信息并对任务执行可用的操作。

### 声明或委托任务 {#claim-or-delegate-tasks}

分配给用户组的任务将显示在所有用户组成员的收件箱中。 任何用户组成员都可以申请该任务或将其委派给其他用户组成员。 为此，请执行以下操作：

1. 点按以选择任务的缩略图。 用于打开或委派任务的选项显示在顶部。

   ![select-task](assets/select-task.png)

1. 执行下列操作之一：

   * 要委派任务，请点按委 **[!UICONTROL 派]**。 此时将打开委派项目对话框。 选择用户，（可选）添加评论，然后点按确 **[!UICONTROL 定]**。
   ![委托](assets/delegate.png)

   * 要声明任务，请点按打 **[!UICONTROL 开]**。 此时将打开“指定到自身”对话框。 点按 **[!UICONTROL 继续]** ，以声明任务。 已申请的任务将作为被分派人出现在您的收件箱中。
   ![索赔](assets/claim.png)

### 查看详细信息并对任务执行操作 {#view-details-and-perform-actions-on-tasks}

打开任务时，可以查看任务详细信息并执行可用的操作。 任务的可用操作在关联的表单工作流的分配任务步骤中定义。

1. 点按以选择任务的缩略图。 用于打开或委派选定任务的选项显示在顶部。
1. 点按 **打开** ，以查看任务详细信息并执行操作。 此时会打开详细的任务视图。 在此视图中，您可以查看任务详细信息并对任务执行操作。

   >[!NOTE]
   >
   >如果某个任务被分配给某个组，则必须声明该任务能够在详细视图中打开它。

![task-details](assets/task-details.png)

详细的任务视图包括以下几节：

* 任务详细信息
* 表单
* 工作流详细信息
* 操作工具栏

#### Task details {#task-details}

“任务详细信息”部分显示有关任务的信息。 显示的信息取决于工作流中分配任 [务步骤的配置](/help/sites-developing/workflows-step-ref.md) 。 上例显示用于任务的说明、状态、开始日期和工作流。 它还允许将文件附加到任务。

#### 表单 {#form}

主内容区域中的“表单”选项卡显示已提交的表单和字段级附件（如果有）。

#### Workflow details {#workflow-details}

顶部的“工作流详细信息”选项卡显示任务在工作流中各个阶段的进度。 它显示任务的已完成、当前和待处理阶段。 工作流的阶段在关联工作流的分配 [任务步骤中定](/help/sites-developing/workflows-step-ref.md) 义。

此外，该选项卡还显示工作流中每个已完成阶段的任务历史记录。 您可以点按已 **[!UICONTROL 完成的阶段的]** “查看详细信息”，以了解有关该阶段的详细信息。 它显示有关任务的注释、表单和任务附件、状态、开始日期和结束日期等。

![工作流详细信息](assets/workflow-details.png)

#### Actions toolbar {#actions-toolbar}

“操作”工具栏显示任务的所有可用选项。 虽然“保存”、“重置”和“委托”是默认操作，但“分配”任务步骤中会配置其 [他可用的操作](/help/sites-developing/workflows-step-ref.md)。 在以上示例中，工作流中配置了批准和拒绝。

当您对任务执行操作时，该任务将在工作流中进一步执行。

### 查看已完成的任务 {#view-completed-tasks}

AEM收件箱仅显示活动任务。 已完成的任务不会显示在列表中。 但是，您可以使用收件箱过滤器根据任务类型、状态、开始日期和结束日期等多个参数筛选任务。 要查看已完成的任务，请执行以下操作：

1. 在AEM收件箱中，点 ![按切换侧面板1](assets/toggle-side-panel1.png) ，打开筛选器选择器。
1. 点按 **[!UICONTROL 任务状态]** accordion，然后选择 **[!UICONTROL 完成]**。 将显示所有已完成的任务。

   ![过滤器](assets/filter.png)

1. 点按以选择任务，然后单击“ **[!UICONTROL 打开]**”。

此时会打开任务，以显示与任务关联的文档或自适应表单。 对于自适应表单，任务将显示只读自适应表单或其PDF记录文档，该文档在“分配任务”工作流步骤的“表单／文档”选 [项卡中配置](/help/sites-developing/workflows-step-ref.md)。

任务详细信息部分显示执行的操作、任务状态、开始日期和结束日期等信息。

![completed-task](assets/completed-task.png)

“工 **[!UICONTROL 作流详细信息]** ”选项卡显示工作流的每个步骤。 点按 **[!UICONTROL 查看详细信息]** ，以获取详细信息。

![completed-task-workflow](assets/completed-task-workflow.png)

