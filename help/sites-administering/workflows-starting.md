---
title: 启动工作流
seo-title: Starting Workflows
description: 了解如何在AEM中启动工作流。
seo-description: Learn how to start Workflows in AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
source-git-commit: 71b3f7c6ad2c7712762a29518de6cf0639081cb7
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 5%

---

# 启动工作流{#starting-workflows}

在管理工作流时，您可以使用各种方法启动它们：

* 手动:

   * 从 [工作流模型](#workflow-models).
   * 将工作流包用于 [批次处理](#workflow-packages-for-batch-processing).

* 自动：

   * 响应节点的变化； [使用启动器](#workflows-launchers).

>[!NOTE]
>
>作者也可以使用其他方法；有关完整的详细信息，请参阅：
>
>* [将工作流程应用于页面](/help/sites-authoring/workflows-applying.md)
>* [如何将工作流应用于DAM资产](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [翻译项目](/help/sites-administering/tc-manage.md)
>

## 工作流模型 {#workflow-models}

您可以启动工作流 [基于其中一个模型](/help/sites-administering/workflows.md#workflow-models-and-instances) 列在工作流模型控制台上。 唯一强制提供的信息是有效负载，不过也可以添加标题和/或评论。

## 工作流启动器 {#workflows-launchers}

工作流启动器监控内容存储库中的更改，从而根据已更改节点的位置和资源类型启动工作流。

使用 **启动器** 您可以：

* 请参阅已为特定节点启动的工作流。
* 选择在创建/修改/删除特定节点/节点类型时要启动的工作流。
* 删除现有的工作流与节点关系。

可以为任何节点创建启动器。 但是，对某些节点所做的更改不会启动工作流。 对以下路径下的节点所做的更改不会导致工作流启动：

* `/var/workflow/instances`
* 位于中的任何位置的任何工作流收件箱节点 `/home/users` 分支
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * 例外：对以下节点进行了更改 `/var/statistics/tracking` *do* 导致工作流启动。

标准安装包含各种定义。 这些资源用于数字资产管理和社会协作任务：

![wf-100](assets/wf-100.png)

## 用于批处理的工作流包 {#workflow-packages-for-batch-processing}

工作流包是可作为有效负荷传递到工作流以供处理的包，从而允许处理多个资源。

工作流包：

* 包含指向一组资源（如页面、资产）的链接。
* 保存文件包信息，例如创建日期、创建文件包的用户以及简短说明。
* 使用专用页面模板定义；此类页面允许用户指定包中的资源。
* 可以多次使用。
* 可以在工作流实例实际运行时由用户更改（添加或删除资源）。

## 从模型控制台启动工作流 {#starting-a-workflow-from-the-models-console}

1. 导航至 **模型** 控制台使用 **工具**， **工作流**，则 **模型**.
1. 选择工作流（根据控制台视图）；如果需要，您还可以使用搜索（左上方）：

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >此 **[瞬态](/help/sites-developing/workflows.md#transient-workflows)** 指示器显示不保留工作流历史记录的工作流。

1. 选择 **启动工作流** 工具栏中。
1. 此时将打开“运行工作流”对话框，允许您指定：

   * **有效负荷**

     这可以是页面、节点、资产、包和其他资源。

   * **标题**

     帮助标识此实例的可选标题。

   * **注释**

     帮助指示此实例详细信息的可选注释。

   ![wf-104](assets/wf-104.png)

## 创建启动器配置 {#creating-a-launcher-configuration}

1. 导航至 **工作流启动器** 控制台使用 **工具**， **工作流**，则 **启动器**.
1. 选择 **创建**，则 **添加启动器** 要打开对话框，请执行以下操作：

   ![wf-105](assets/wf-105.png)

   * **事件类型**

     将启动工作流的事件类型：

      * 创建时间
      * 修改时间
      * 已删除

   * **节点类型**

     工作流启动器应用的节点类型。

   * **路径**

     工作流启动器应用的路径。

   * **运行模式**

     工作流启动器应用于的服务器的类型。 选择 **作者**， **Publish**，或 **创作和发布**.

   * **条件**

     节点值的条件列表，在评估后用于确定是否启动工作流。 例如，如果节点的属性名称值为User，则以下条件会导致启动工作流：

     名称==用户

   * **功能**

     要启用的功能列表。 使用下拉选择器选择所需的功能。

   * **禁用的功能**

   要禁用的功能列表。 使用下拉选择器选择所需的功能。

   * **工作流模型**

     当事件类型发生在定义条件下的节点类型和/或路径上时要启动的工作流。

   * **描述**

     您自己的文本，用于描述和标识启动器配置。

   * **激活**

     控制是否激活工作流启动器：

      * 选择 **启用** 在满足配置属性后启动工作流。
      * 选择 **禁用** 不应执行工作流时（即使满足配置属性时也不应执行）。

   * **排除列表**

     这指定在确定是否应触发工作流时要排除的任何JCR事件（即忽略）。

     此启动器属性是一个以逗号分隔的项目列表：&#39;&#39;

      * `property-name` 忽略任何 `jcr` 在指定的属性名称上触发的事件。&quot;
      * `event-user-data:<*someValue*>` 忽略任何包含 `*<someValue*`> `user-data` 通过 [`ObservationManager` API](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String.

     例如：

     `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

     此功能可用于通过添加排除项来忽略由其他工作流进程触发的任何更改：

     `event-user-data:changedByWorkflowProcess`

1. 选择 **创建**，以创建启动器并返回到控制台。

   发生相应的事件后，将触发启动器并启动工作流。

## 管理启动器配置 {#managing-a-launcher-configuration}

创建启动器配置后，您可以使用同一控制台选择实例，然后 **查看属性** （并编辑它们）或 **删除**.
