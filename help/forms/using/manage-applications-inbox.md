---
title: 在AEM收件箱中管理Forms应用程序和任务
seo-title: Manage Forms applications and tasks in AEM Inbox
description: AEM收件箱允许您通过提交应用程序来启动以Forms为中心的工作流，并管理任务。
seo-description: AEM Inbox lets you launch Forms-centric workflows through submitting applications and manage tasks.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
exl-id: 8d17194b-8baf-4878-b3ae-d351a056aebf
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 3%

---

# 在AEM收件箱中管理Forms应用程序和任务{#manage-forms-applications-and-tasks-in-aem-inbox}

启动或触发以Forms为中心的工作流的多种方法之一，是通过AEM收件箱中的应用程序。 要使Forms工作流可用作收件箱中的应用程序，请创建工作流应用程序。 有关工作流应用程序和其他启动Forms工作流方法的更多信息，请参阅 [在OSGi上启动以Forms为中心的工作流](../../forms/using/aem-forms-workflow.md#launch).

此外，AEM收件箱可整合来自各种AEM组件(包括Forms工作流程)的通知和任务。 触发包含“分配”任务步骤的表单工作流时，关联的应用程序将作为任务列在被分配人的收件箱中。 如果被分派人是组，则该任务会出现在所有组成员的“收件箱”中，直到个人声明或委派该任务为止。

收件箱用户界面提供列表和日历视图以查看任务。 您还可以配置视图设置。 您可以根据各种参数筛选任务。 有关视图和筛选器的详细信息，请参阅 [您的收件箱](/help/sites-authoring/inbox.md).

总之，收件箱允许您创建新应用程序并管理分配的任务。

>[!NOTE]
>
>您必须是workflow-users组的成员才能使用AEM收件箱。

## 创建应用程序 {#create-application}

1. 转到AEM收件箱，网址为https://&#39;[服务器]：[端口]&#39;/aem/inbox.
1. 在收件箱UI中，点击 **[!UICONTROL 创建>应用程序]**. 此时将显示“选择应用程序”页。
1. 选择应用程序并单击 **[!UICONTROL 创建]**. 将打开与应用程序关联的自适应表单。 在自适应表单中填写信息并点按 **[!UICONTROL 提交]**. 它会启动关联的工作流，并在被分派人的“收件箱”中创建任务。

## 管理任务 {#manage-tasks}

当触发Forms工作流并且您是被分配人或被分配人组的一部分时，您的收件箱中会显示一个任务。 您可以在“收件箱”中查看任务详细信息并对任务执行可用操作。

### 报销申请或委派任务 {#claim-or-delegate-tasks}

分配给组的任务将显示在所有组成员的“收件箱”中。 任何组成员都可以声明该任务或将其委派给其他组成员。 为此，请执行以下操作：

1. 点按以选择任务的缩略图。 用于打开或委派任务的选项显示在顶部。

   ![选择任务](assets/select-task.png)

1. 执行下列操作之一：

   * 要委派任务，请点按 **[!UICONTROL 委派]**. 这将打开委托项目对话框。 选择用户（可选）添加评论，然后点按 **[!UICONTROL 确定]**.

   ![委派](assets/delegate.png)

   * 要声明任务，请点击 **[!UICONTROL 打开]**. 将打开“分配给自身”对话框。 点按 **[!UICONTROL 继续]** 来承担这个任务。 您作为被分配者将会在收件箱中显示声明的任务。

   ![声明](assets/claim.png)

### 查看详细信息并对任务执行操作 {#view-details-and-perform-actions-on-tasks}

打开任务时，可以查看任务详细信息并执行可用操作。 任务可用的操作在关联的Forms工作流的分配任务步骤中定义。

1. 点按以选择任务的缩略图。 用于打开或委派选定任务的选项将显示在顶部。
1. 点按 **打开** 查看任务详细信息。 此时将打开详细的任务视图。 在此视图中，您可以查看任务详细信息并处理该任务。

   >[!NOTE]
   >
   >如果将任务分配给组，则必须声明该任务才能在详细视图中打开它。

![task-details](assets/task-details.png)

详细的任务视图包含以下部分：

* 任务详细信息
* 表单
* 工作流详细信息
* “操作”工具栏

#### 任务详细信息 {#task-details}

“任务详细信息”部分显示有关任务的信息。 显示的信息取决于 [分配任务步骤](/help/sites-developing/workflows-step-ref.md) 在工作流中。 上面的示例显示了用于任务的描述、状态、开始日期和工作流。 它还允许将文件附加到任务。

#### 表单 {#form}

主内容区域中的“表单”选项卡显示已提交的表单和字段级附件（如果有）。

#### 工作流详细信息 {#workflow-details}

顶部的“工作流详细信息”选项卡显示任务在工作流中各个阶段的进度。 它显示任务的已完成阶段、当前阶段和待定阶段。 在中定义工作流的阶段 [分配任务步骤](/help/sites-developing/workflows-step-ref.md) 关联工作流的ID。

此外，选项卡显示工作流中每个已完成阶段的任务历史记录。 您可以点按 **[!UICONTROL 查看详细信息]** 完成阶段以了解有关该阶段的详细信息。 它显示有关任务的注释、表单和任务附件、状态、开始和结束日期等。

![workflow-details](assets/workflow-details.png)

#### “操作”工具栏 {#actions-toolbar}

“操作”工具栏显示任务的所有可用选项。 虽然保存、重置和委派是默认操作，但在中配置了其他可用操作 [分配任务步骤](/help/sites-developing/workflows-step-ref.md). 以上示例中，在工作流中配置了批准和拒绝。

当您处理任务时，它会在工作流中进一步进行。

### 查看已完成的任务 {#view-completed-tasks}

AEM收件箱仅显示活动任务。 已完成的任务未出现在列表中。 但是，您可以使用收件箱筛选器根据多个参数（如任务类型、状态以及开始和结束日期）筛选任务。 要查看已完成的任务，请执行以下操作：

1. 在AEM收件箱中，点按 ![toggle-side-panel1](assets/toggle-side-panel1.png) 以打开过滤器选择器。
1. 点按 **[!UICONTROL 任务状态]** 可折叠项和选择 **[!UICONTROL 完成]**. 此时会显示所有已完成的任务。

   ![filter](assets/filter.png)

1. 点按以选择任务，然后单击 **[!UICONTROL 打开]**.

此时将打开任务，以显示与任务关联的文档或自适应表单。 对于自适应表单，任务显示只读自适应表单或其PDF记录文档，如在的表单/文档选项卡中配置 [分配任务工作流步骤](/help/sites-developing/workflows-step-ref.md).

任务详细信息部分显示所采取的操作、任务状态、开始日期和结束日期等信息。

![completed-task](assets/completed-task.png)

此 **[!UICONTROL 工作流详细信息]** 选项卡显示了工作流的每个步骤。 点按 **[!UICONTROL 查看详细信息]** 以了解详细信息。

![completed-task-workflow](assets/completed-task-workflow.png)

## 疑难解答 {#troubleshooting-workflows}

### 无法在AEM收件箱中查看与AEM工作流相关的项目 {#unable-to-see-aem-worklow-items}

工作流模型所有者无法在AEM收件箱中查看与AEM Workflow相关的项目。 要解决此问题，请将以下列出的索引添加到AEM资料档案库中，并重新构建该索引。

1. 使用下列方法之一添加索引：

   * 在CRX DE中的创建以下节点： `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` ，其各自的属性如下表所示：

     | 节点 | 属性 | 类型 |
     |---|---|---|
     | sharedwith | sharedwith | 字符串 |
     | 已锁定 | 已锁定 | Boolean |
     | 返回的 | 返回的 | Boolean |
     | allowInboxSharing | allowInboxSharing | Boolean |
     | allowExplicitSharing | allowExplicitSharing | Boolean |


   * 通过AEM包部署索引。 您可以使用 [AEM原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en) 创建可部署的AEM包的项目。 使用以下示例代码将索引添加到AEM Archetype项目中：

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [创建属性索引并将其设置为true](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html#the-property-index).

1. 在CRX DE中配置索引或通过包进行部署后， [重新索引存储库](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html
