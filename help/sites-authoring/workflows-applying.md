---
title: 将工作流应用于页面
seo-title: 将工作流应用于页面
description: 进行创作时，您可以调用工作流以在页面上执行操作；也可以应用多个工作流。
seo-description: 进行创作时，您可以调用工作流以在页面上执行操作；也可以应用多个工作流。
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
translation-type: tm+mt
source-git-commit: 611743cc4144f99968845093b3903fe7df8bf9d9
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 84%

---


# 将工作流应用于页面{#applying-workflows-to-pages}

创作时，您可以调用工作流以在页面上执行操作； 还可以应用多个工作流。

在应用工作流时，您需要指定以下信息：

* 要应用的工作流。您可以应用任何工作流（您有权访问，由 AEM 管理员分配）。
* （可选）有助于在用户收件箱中识别工作流实例的标题。
* 工作流有效负荷；这可以是一个或多个页面。

可以从以下位置启动工作流：

* [站点控制台](#starting-a-workflow-from-the-sites-console)。
* [编辑页面时，从页面信息](#starting-a-workflow-from-the-page-editor)启动。

>[!NOTE]
>
>另请参阅：
>
>* [如何将工作流应用于 DAM 资产](/help/assets/assets-workflow.md)。
>* [使用项目工作流](/help/sites-authoring/projects-with-workflows.md)。

>



>[!NOTE]
>
>AEM 管理员可以[使用其他几种方法来启动工作流](/help/sites-administering/workflows-starting.md)。

## 从“站点”控制台启动工作流 {#starting-a-workflow-from-the-sites-console}

您可以从以下任一项中启动工作流：

* [“站点”工具栏的创建选项](#starting-a-workflow-from-the-sites-toolbar)。
* [“站点”控制台的时间轴边栏](#starting-a-workflow-from-the-timeline)。

在这两种情况下，您都将需要：

* [在“创建工作流”向导中指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 从“站点”工具栏启动工作流 {#starting-a-workflow-from-the-sites-toolbar}

You can start a workflow from the toolbar of the **Sites** console:

1. 导航到所需的页面并选择该页面。

1. From the **Create** option in the toolbar you can now select **Workflow**.

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. **创建工作流**&#x200B;向导将帮助您[指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 从时间轴启动工作流 {#starting-a-workflow-from-the-timeline}

您可以从&#x200B;**时间轴**&#x200B;中启动要应用于所选资源的工作流。

1. [选择资源](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources) ，然后打 [开时间](/help/sites-authoring/basic-handling.md#timeline) 轴（或打开时间轴，然后选择资源）。
1. 可以使用评论字段中的箭头显示&#x200B;**启动工作流**：

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. **创建工作流**&#x200B;向导将帮助您[指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard)。

### 在“创建工作流”向导中指定工作流详细信息 {#specifying-workflow-details-in-the-create-workflow-wizard}

**创建工作流**&#x200B;向导将帮助您选择工作流并指定所需的详细信息。

从以下任一项中打开&#x200B;**创建工作流**&#x200B;向导后：

* [“站点”工具栏的创建选项](#starting-a-workflow-from-the-sites-toolbar)。
* [“站点”控制台的时间轴边栏](#starting-a-workflow-from-the-timeline)。

您可以指定详细信息：

1. 在&#x200B;**属性**&#x200B;步骤中，定义了工作流的基本选项：

   * **工作流模型**
   * **工作流标题**

      * 您可以指定此实例的标题，以帮助您在以后对其进行识别。

   根据工作流模型，还可以使用以下选项。这些选项允许在工作流完成后保留创建为有效负荷的包。

   * **保留工作流包**
   * **包标题**

      * 您可以指定包标题以便进行识别。
   >[!NOTE]
   >
   >为“ **多资源支持”配置了工作流并选择了多个资源时** ,“保留工作流包”选项可用。[](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)

   完成后，使用&#x200B;**下一步**&#x200B;以继续。

   ![wf-52](assets/wf-52.png)

1. 在&#x200B;**范围**&#x200B;步骤中，您可以选择：

   * **添加内容** ，打开路 [径浏览器](/help/sites-authoring/author-environment-tools.md#path-browser) ，并选择其他资源； 在浏览器中时，单击／点按 **选择** ，以将内容添加到工作流实例。

   * 现有资源以查看其他操作：

      * **包括子项**，指定将该资源的子项包含在工作流中。系统将打开一个对话框，允许您根据以下各项优化选择：

         * 仅包括下级子项。
         * 仅包括已修改的页面。
         * 仅包括已发布的页面。

         指定的任何子项都会添加到将应用工作流的资源列表中。

      * **删除选择**，从工作流中删除该资源。

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >如果添加其他资源，则可以使用“返回 **”** ，在“属性”步骤中调整“ **保留工作流包** ”的 **设置** 。

1. Use **Create** to close the wizard and create the workflow instance. “站点”控制台中随即会显示一则通知。

## 从页面编辑器启动工作流 {#starting-a-workflow-from-the-page-editor}

编辑页面时，您可以从工具栏中选择&#x200B;**页面信息**。下拉菜单中包含&#x200B;**启动工作流**&#x200B;选项。此选项将打开一个对话框，您可以在其中指定所需的工作流，如果需要，还可以指定标题：

![wf-54](assets/wf-54.png)
