---
title: 在AEM收件箱中管理Forms应用程序和任务
seo-title: 在AEM收件箱中管理Forms应用程序和任务
description: AEM收件箱允许您通过提交应用程序和管理任务来启动以Forms为中心的工作流。
seo-description: AEM收件箱允许您通过提交应用程序和管理任务来启动以Forms为中心的工作流。
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
exl-id: 8d17194b-8baf-4878-b3ae-d351a056aebf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 2%

---

# 在AEM收件箱中管理Forms应用程序和任务{#manage-forms-applications-and-tasks-in-aem-inbox}

启动或触发以Forms为中心的工作流的多种方式之一，就是在AEM收件箱中通过应用程序。 您需要创建一个工作流应用程序，以使Forms工作流作为应用程序在收件箱中提供。 有关工作流应用程序以及其他启动Forms工作流的方法的更多信息，请参阅[在OSGi](../../forms/using/aem-forms-workflow.md#launch)上启动以Forms为中心的工作流。

此外，AEM收件箱可整合来自各种AEM组件(包括Forms工作流)的通知和任务。 触发包含“分配”任务步骤的表单工作流时，关联的应用程序将作为任务列在被分派人的收件箱中。 如果受分配人是组，则任务会显示在所有组成员的收件箱中，直到个人声明或委派任务为止。

收件箱用户界面提供列表视图和日历视图以查看任务。 您还可以配置视图设置。 您可以根据各种参数筛选任务。 有关视图和过滤器的更多信息，请参阅[您的收件箱](/help/sites-authoring/inbox.md)。

总之，收件箱允许您创建新应用程序并管理分配的任务。

>[!NOTE]
>
>您必须是工作流用户组的成员，才能使用AEM收件箱。

## 创建应用程序{#create-application}

1. 转到位于https://&#39;[server]的AEM收件箱：[port]&#39;/aem/inbox。
1. 在收件箱UI中，点按&#x200B;**[!UICONTROL 创建>应用程序]**。 此时将显示“选择应用程序”页。
1. 选择应用程序并单击&#x200B;**[!UICONTROL 创建]**。 随即会打开与应用程序关联的自适应表单。 在自适应表单中填写信息，然后点按&#x200B;**[!UICONTROL Submit]**。 它会启动关联的工作流，并在被分派人的收件箱中创建任务。

## 管理任务 {#manage-tasks}

当触发Forms工作流并且您是代理人或代理人组的一部分时，您的收件箱中会显示一个任务。 您可以在收件箱中查看任务详细信息并对任务执行可用操作。

### 声明或委派任务{#claim-or-delegate-tasks}

分配给群组的任务将显示在所有群组成员的收件箱中。 任何组成员都可以声明该任务或将其委派给另一个组成员。 为此，请执行以下操作：

1. 点按以选择任务的缩略图。 用于打开或委派任务的选项显示在顶部。

   ![选择任务](assets/select-task.png)

1. 执行下列操作之一：

   * 要委派任务，请点按&#x200B;**[!UICONTROL 委派]**。 此时将打开委派项目对话框。 选择用户，（可选）添加评论，然后点按&#x200B;**[!UICONTROL 确定]**。

   ![委托](assets/delegate.png)

   * 要声明该任务，请点按&#x200B;**[!UICONTROL 打开]**。 “指定到自身”(Assign to Self)对话框打开。 点按&#x200B;**[!UICONTROL 继续]**&#x200B;以声明任务。 声明的任务将以您的收件箱中的代理人身份显示。

   ![索赔](assets/claim.png)

### 查看任务{#view-details-and-perform-actions-on-tasks}的详细信息并执行相应操作

打开任务时，可以查看任务详细信息并执行可用操作。 任务可用的操作在关联的Forms工作流的“分配任务”步骤中定义。

1. 点按以选择任务的缩略图。 用于打开或委派所选任务的选项显示在顶部。
1. 点按&#x200B;**打开**&#x200B;以查看任务详细信息并执行操作。 此时将打开详细的任务视图。 在此视图中，您可以查看任务详细信息并对任务执行操作。

   >[!NOTE]
   >
   >如果任务被分配给某个组，则必须声明该任务能够在详细视图中打开它。

![任务详细信息](assets/task-details.png)

详细的任务视图包括以下部分：

* 任务详细信息
* 表单
* 工作流详细信息
* “操作”工具栏

#### 任务详细信息{#task-details}

“任务详细信息”部分显示有关任务的信息。 显示的信息取决于工作流中[分配任务步骤](/help/sites-developing/workflows-step-ref.md)的配置设置。 上例显示用于任务的描述、状态、开始日期和工作流。 它还允许将文件附加到任务。

#### 表单 {#form}

主内容区域中的“表单”选项卡显示已提交的表单和字段级附件（如果有）。

#### 工作流详细信息 {#workflow-details}

顶部的“工作流详细信息”选项卡显示任务在工作流中各个阶段的进度。 它显示任务的已完成、当前和待定阶段。 工作流的阶段在关联工作流的[分配任务步骤](/help/sites-developing/workflows-step-ref.md)中定义。

此外，选项卡还显示工作流中每个已完成阶段的任务历史记录。 您可以点按&#x200B;**[!UICONTROL 查看详细信息]**&#x200B;以查看已完成的阶段，以了解该阶段的详细信息。 它显示有关任务的注释、表单和任务附件、状态、开始和结束日期等。

![工作流详细信息](assets/workflow-details.png)

#### 操作工具栏{#actions-toolbar}

“操作”工具栏显示任务的所有可用选项。 虽然“保存”、“重置”和“委派”是默认操作，但其他可用操作在[分配任务步骤](/help/sites-developing/workflows-step-ref.md)中进行配置。 在以上示例中，工作流中配置了批准和拒绝。

当您对任务执行操作时，该任务会在工作流中继续执行。

### 查看已完成的任务{#view-completed-tasks}

AEM收件箱仅显示活动任务。 已完成的任务不会显示在列表中。 但是，您可以使用收件箱过滤器根据多个参数（如任务类型、状态、开始和结束日期等）筛选任务。 要查看已完成的任务，请执行以下操作：

1. 在AEM收件箱中，点按![toggle-side-panel1](assets/toggle-side-panel1.png)以打开过滤器选择器。
1. 点按&#x200B;**[!UICONTROL 任务状态]**&#x200B;折叠面板，然后选择&#x200B;**[!UICONTROL 完成]**。 将显示所有已完成的任务。

   ![过滤器](assets/filter.png)

1. 点按以选择任务，然后单击&#x200B;**[!UICONTROL 打开]**。

此时会打开任务以显示与任务关联的文档或自适应表单。 对于自适应表单，任务显示只读自适应表单或其记录的PDF文档，如[分配任务工作流步骤](/help/sites-developing/workflows-step-ref.md)的“表单/文档”选项卡中所配置。

“任务详细信息”部分显示已执行的操作、任务状态、开始日期和结束日期等信息。

![已完成任务](assets/completed-task.png)

**[!UICONTROL 工作流详细信息]**&#x200B;选项卡显示工作流的每个步骤。 点按&#x200B;**[!UICONTROL 查看详细信息]**&#x200B;以获取详细信息的步骤。

![已完成的任务 — 工作流](assets/completed-task-workflow.png)

## 疑难解答 {#troubleshooting-workflows}

### 无法在AEM收件箱{#unable-to-see-aem-worklow-items}中查看与AEM Workflow相关的项目

工作流模型所有者无法在AEM收件箱中查看与AEM Workflow相关的项目。 要解决此问题，请将下列索引添加到您的AEM存储库并重新构建索引。

1. 使用以下方法之一添加索引：

   * 在CRX DE的`/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties`处创建以下节点，并按照下表中指定的相应属性：

      | 节点 | 属性 | 类型 |
      |---|---|---|
      | sharedWith | sharedWith | 字符串 |
      | 已锁定 | 已锁定 | Boolean |
      | 返回 | 返回 | Boolean |
      | allowInboxSharing | allowInboxSharing | Boolean |
      | allowExplicitSharing | allowExplicitSharing | Boolean |


   * 通过AEM包部署索引。 您可以使用[AEM Archetype](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype)项目创建可部署的AEM包。 使用以下示例代码向AEM Archetype项目添加索引：

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [创建属性索引并将其设置为true](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/queries-and-indexing.html#the-property-index)。

1. 在CRX DE中配置索引或通过包部署后， [会重新为存储库](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex)编入索引。

https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/queries-and-indexing.html
