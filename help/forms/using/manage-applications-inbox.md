---
title: 在AEM收件箱中管理Forms应用程序和任务
seo-title: 在AEM收件箱中管理Forms应用程序和任务
description: AEM Inbox允许您通过提交应用程序和管理工作流来启动以Forms为中心的任务。
seo-description: AEM Inbox允许您通过提交应用程序和管理工作流来启动以Forms为中心的任务。
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
translation-type: tm+mt
source-git-commit: d324586eb1d4fb809bf87641001b92a1941e6548
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 2%

---


# 在AEM收件箱中管理Forms应用程序和任务{#manage-forms-applications-and-tasks-in-aem-inbox}

启动或触发以Forms为中心的工作流的多种方法之一是通过AEM收件箱中的应用程序。 您需要创建一个工作流应用程序，以使Forms工作流作为应用程序显示在收件箱中。 有关工作流应用程序和启动Forms工作流的其他方式的更多信息，请 [参阅在OSGi上启动以Forms为中心的工作流](../../forms/using/aem-forms-workflow.md#launch)。

此外，AEM Inbox整合了来自各种AEM组件(包括Forms工作流)的通知和任务。 当触发包含分配任务步骤的表单工作流时，关联的应用程序将作为任务列在被分派人的收件箱中。 如果受分派人是组，则任务会显示在所有组成员的收件箱中，直到个人声明或委派任务。

收件箱用户界面为列表视图和日历视图提供数据。 您还可以配置视图设置。 您可以根据各种参数筛选任务。 有关视图和过滤器的更多信息，请参 [阅您的收件箱](/help/sites-authoring/inbox.md)。

总之，“收件箱”允许您创建新应用程序并管理分配的任务。

>[!NOTE]
>
>您必须是工作流用户组的成员才能使用AEM收件箱。

## 创建应用程序 {#create-application}

1. 转至AEM Inbox(位于[https://&#39;]server[]:port&#39;/aem/inbox)。
1. 在收件箱UI中，点按创 **[!UICONTROL 建>应用程序]**。 此时将显示“选择应用程序”页。
1. 选择一个应用程序，然后单 **[!UICONTROL 击创建]**。 此时将打开与应用程序关联的自适应表单。 在自适应表单中填写信息，然后点按 **[!UICONTROL 提交]**。 它启动关联的工作流并在被分派人的收件箱中创建任务。

## 管理任务 {#manage-tasks}

当Forms工作流触发并且您是被分派人或被分派人组的一部分时，任务会显示在您的收件箱中。 您可以从收件箱中视图任务详细信息并对任务执行可用操作。

### 索赔或委托任务 {#claim-or-delegate-tasks}

分配给组的任务会显示在所有组成员的收件箱中。 任何组成员都可以声明将其任务或委派给其他组成员。 为此，请执行以下操作：

1. 点按以选择任务的缩略图。 用于打开或委派任务的选项显示在顶部。

   ![select-任务](assets/select-task.png)

1. 执行下列操作之一：

   * 要委派任务，请点按 **[!UICONTROL 委派]**。 此时将打开委派项对话框。 选择用户，（可选）添加评论，然后点按 **[!UICONTROL 确定]**。

   ![委托](assets/delegate.png)

   * 要声明任务，请点 **[!UICONTROL 击打开]**。 “指定到自身”对话框打开。 点按 **[!UICONTROL 继续]** ，以声明任务。 声明的任务将作为被分派人出现在您的收件箱中。

   ![索赔](assets/claim.png)

### 视图详细信息并对任务执行操作 {#view-details-and-perform-actions-on-tasks}

打开任务时，您可以视图任务详细信息并执行可用操作。 可用于任务的操作在关联的Forms工作流的分配任务步骤中定义。

1. 点按以选择任务的缩略图。 用于打开或委派选定任务的选项显示在顶部。
1. 点按 **打开** ，以视图任务详细信息并执行操作。 将打开详细的任务视图。 在此视图中，您可以视图任务详细信息并对任务执行操作。

   >[!NOTE]
   >
   >如果任务被分配给组，您必须声明该组能够在详细视图中打开它。

![任务详细信息](assets/task-details.png)

详细的任务视图包括以下部分：

* 任务详细信息
* 表单
* 工作流详细信息
* 操作工具栏

#### Task details {#task-details}

“任务详细信息”部分显示有关任务的信息。 显示的信息取决于工作流中分配 [任务步骤的](/help/sites-developing/workflows-step-ref.md) 配置设置。 上例显示用于任务的描述、状态、开始日期和工作流。 它还允许将文件附加到任务。

#### 表单 {#form}

主内容区域中的“表单”选项卡显示已提交的表单和字段级附件（如果有）。

#### Workflow details {#workflow-details}

顶部的工作流详细信息选项卡显示任务在工作流中各个阶段的进度。 它显示任务的已完成、当前和待处理阶段。 工作流的阶段在关联工作流的 [分配任务步](/help/sites-developing/workflows-step-ref.md) 骤中进行定义。

此外，该选项卡还显示工作流中每个已完成阶段的任务历史记录。 您可以点按 **[!UICONTROL 视图详细]** 信息以查看已完成的阶段的详细信息。 它显示有关任务的注释、表单和开始附件、状态、任务和结束日期等。

![工作流详细信息](assets/workflow-details.png)

#### Actions toolbar {#actions-toolbar}

“操作”工具栏显示该任务的所有可用选项。 保存、重置和委派是默认操作，而其他可用操作则在分配任务步 [骤中进行配置](/help/sites-developing/workflows-step-ref.md)。 在以上示例中，工作流中配置了批准和拒绝。

在您对任务执行操作时，它会在工作流中进一步进行。

### 视图完成任务 {#view-completed-tasks}

AEM收件箱仅显示活动任务。 已完成的任务不显示在列表中。 但是，您可以使用收件箱过滤器根据多个参数(如任务类型、状态、开始和结束日期等)筛选任务。 要视图已完成的任务:

1. 在AEM收件箱中， ![点按切换侧面板](assets/toggle-side-panel1.png) 1以打开筛选器选择器。
1. 点按 **[!UICONTROL 任务状态]** ，相应的面板并 **[!UICONTROL 选择完成]**。 将显示所有已完成的任务。

   ![过滤器](assets/filter.png)

1. 点按以选择任务，然后单击 **[!UICONTROL 打开]**。

任务将打开以显示与文档关联的任务或自适应表单。 对于自适应表单，任务显示只读自适应表单或其PDF记录文档，该在“指定任务”工作流步骤的“表单/文档”选 [项卡中配置](/help/sites-developing/workflows-step-ref.md)。

任务详细信息部分显示执行的操作、任务状态、开始日期和结束日期等信息。

![completed-任务](assets/completed-task.png)

“工 **[!UICONTROL 作流详细信息]** ”选项卡显示工作流的每个步骤。 点按 **[!UICONTROL 视图详]** 细信息以获取详细信息。

![completed-任务-workflow](assets/completed-task-workflow.png)

## 疑难解答 {#troubleshooting-workflows}

### 无法在AEM收件箱中视图与AEM工作流相关的项目 {#unable-to-see-aem-worklow-items}

工作流模型所有者无法在AEM收件箱中视图与AEM工作流相关的项目。 要解决此问题，请将以下列出的索引添加到AEM存储库并重新构建索引。

1. 使用以下方法之一添加索引：

   * 在CRX DE中，使用下表中 `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` 指定的相应属性在创建以下节点：

      | 节点 | 属性 | 类型 |
      |---|---|---|
      | sharedWith | sharedWith | 字符串 |
      | 已锁定 | 已锁定 | Boolean |
      | 返回 | 返回 | Boolean |
      | allowInboxSharing | allowInboxSharing | Boolean |
      | allowExplicitSharing | allowExplicitSharing | Boolean |


   * 通过AEM包部署索引。 您可以使用AEM [Archetype项目](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype) ，创建可部署的AEM包。 使用以下示例代码向AEM Archetype项目添加索引：

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [创建属性索引并将其设置为true](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/queries-and-indexing.html#the-property-index)。

1. 在CRX DE中配置索引或通过包部署后， [重新为存储库编制索引](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex)。

https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/queries-and-indexing.html
