---
title: 将工作流应用于内容页面
description: 进行创作时，您可以调用工作流以在页面上执行操作；也可以应用多个工作流。
uuid: 652d9a23-907d-43ad-9eef-7ab1d07918cd
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 6472dc94-96e0-4286-8f86-d85726cc843c
docset: aem65
exl-id: e00da2b3-046a-4d93-aed0-07dd8c66899f
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 55%

---

# 将工作流应用于页面{#applying-workflows-to-pages}

进行创作时，您可以调用工作流以在页面上执行操作；也可以应用多个工作流。

在应用工作流时，需要指定以下信息：

* 要应用的工作流。您可以应用任何工作流（您有权访问，由 AEM 管理员分配）。
* （可选）帮助标识用户收件箱中的工作流实例的标题。
* 工作流有效负载；这可以是一个或多个页面。

工作流可从以下位置启动：

* [站点控制台](#starting-a-workflow-from-the-sites-console)。
* [编辑页面时，从“页面信息”](#starting-a-workflow-from-the-page-editor)启动。

>[!NOTE]
>
>另请参阅：
>
>* [如何将工作流应用于DAM资产](/help/assets/assets-workflow.md).
>* [使用项目工作流](/help/sites-authoring/projects-with-workflows.md)。
>


>[!NOTE]
>
>AEM管理员可以 [使用其他几种方法启动工作流](/help/sites-administering/workflows-starting.md).

## 从站点控制台启动工作流 {#starting-a-workflow-from-the-sites-console}

您可以通过以下任一方式启动工作流：

* [“站点”工具栏的“创建”选项](#starting-a-workflow-from-the-sites-toolbar)。
* [“站点”控制台的时间线边栏](#starting-a-workflow-from-the-timeline)。

在这两种情况下，您都需要：

* [在“创建工作流向导”中指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard).

### 从站点工具栏启动工作流 {#starting-a-workflow-from-the-sites-toolbar}

您可以从&#x200B;**站点**&#x200B;控制台的工具栏中启动工作流：

1. 导航到所需的页面并选择该页面。

1. 现在，您可以从工具栏的&#x200B;**创建**&#x200B;选项中选择&#x200B;**工作流**。

   ![screen_shot_2019-03-06at121237pm](assets/screen_shot_2019-03-06at121237pm.png)

1. 此 **创建工作流** 向导将帮助您 [指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard).

### 从时间线启动工作流 {#starting-a-workflow-from-the-timeline}

您可以从&#x200B;**时间线**&#x200B;中启动要应用于所选资源的工作流。

1. [选择资源](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)，然后打开[时间线](/help/sites-authoring/basic-handling.md#timeline)（或打开时间线，然后选择资源）。
1. 可以使用评论字段中的箭头显示&#x200B;**启动工作流**：

   ![screen-shot_2019-03-05at120026](assets/screen-shot_2019-03-05at120026.png)

1. 此 **创建工作流** 向导将帮助您 [指定工作流详细信息](#specifying-workflow-details-in-the-create-workflow-wizard).

### 在“创建工作流”向导中指定工作流详细信息 {#specifying-workflow-details-in-the-create-workflow-wizard}

此 **创建工作流** 向导将帮助您选择工作流并指定所需的详细信息。

打开 **创建工作流** 从以下任一位置创建向导：

* [“站点”工具栏的“创建”选项](#starting-a-workflow-from-the-sites-toolbar)。
* [“站点”控制台的时间线边栏](#starting-a-workflow-from-the-timeline)。

您可以指定详细信息：

1. 在 **属性** 步骤，定义工作流的基本选项：

   * **工作流模型**
   * **工作流标题**

      * 您可以为此实例指定标题，以帮助您在以后阶段识别它。

   根据工作流模型，以下选项也可用。 这些功能允许在工作流完成后保留作为有效负载创建的包。

   * **保留工作流包**
   * **包标题**

      * 您可以指定包的标题，以帮助识别。
   >[!NOTE]
   >
   >为多资源支持配置了工作流并选择了多个资源时，**保留工作流包**&#x200B;选项可用。[](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)

   完成后，单击&#x200B;**下一步**&#x200B;继续。

   ![wf-52](assets/wf-52.png)

1. 在&#x200B;**范围**&#x200B;步骤中，您可以选择：

   * **添加内容**&#x200B;以打开[路径浏览器](/help/sites-authoring/author-environment-tools.md#path-browser)并选择其他资源；在浏览器中，单击/点按&#x200B;**选择**&#x200B;以将内容添加到工作流实例。

   * 现有资源以查看其他操作：

      * **包括子项**，指定将该资源的子项包含在工作流中。
系统将打开一个对话框，允许您根据以下各项优化选择：

         * 仅包括下级子项.
         * 仅包括已修改的页面.
         * 仅包括已发布的页面.

         指定的任何子项都会添加到将应用工作流的资源列表中。

      * **删除选择** 以从工作流中删除该资源。

   ![wf-53](assets/wf-53.png)

   >[!NOTE]
   >
   >如果添加其他资源，则可以使用&#x200B;**返回**，在&#x200B;**属性**&#x200B;步骤中调整&#x200B;**保留工作流包**&#x200B;的设置。

1. 使用&#x200B;**创建**&#x200B;关闭向导并创建工作流实例。站点控制台中将显示通知。

## 从页面编辑器启动工作流 {#starting-a-workflow-from-the-page-editor}

编辑页面时，您可以选择 **页面信息** 工具栏中。 下拉菜单具有选项 **在工作流中开始**. 此选项将打开一个对话框，您可以在其中指定所需的工作流，如果需要，还可以指定标题：

![wf-54](assets/wf-54.png)
