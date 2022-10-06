---
title: 开发和扩展工作流
seo-title: Developing and Extending Workflows
description: AEM提供了多种工具和资源，用于创建工作流模型、开发工作流步骤以及以编程方式与工作流交互
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 82b9b852fa3134f140f8de0bad229282979c8a30
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 3%

---


# 开发和扩展工作流{#developing-and-extending-workflows}

AEM提供了多种工具和资源，用于创建工作流模型、开发工作流步骤以及以编程方式与工作流交互。

工作流使您能够自动执行在AEM环境中管理资源和发布内容的流程。 工作流由一系列步骤组成，每个步骤都可完成一个离散的任务。 您可以使用逻辑和运行时数据来决定进程何时可以继续，并从多个可能的步骤中选择下一步。

例如，用于创建和发布网页的业务流程包括各种参与者的批准和注销任务。 这些流程可以使用AEM工作流进行建模并应用于特定内容。

下文将介绍主要方面，而以下页面将介绍更多详细信息：

* [创建工作流模型](/help/sites-developing/workflows-models.md)
* [扩展工作流功能](/help/sites-developing/workflows-customizing-extending.md)
* [以编程方式与工作流交互](/help/sites-developing/workflows-program-interaction.md)
* [工作流步骤参考](/help/sites-developing/workflows-step-ref.md)
* [工作流过程参考](/help/sites-developing/workflows-process-ref.md)
* [工作流最佳实践](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>有关信息:
>
>* 参与工作流，请参阅 [使用工作流](/help/sites-authoring/workflows.md).
>* 管理工作流和工作流实例，请参阅 [管理工作流](/help/sites-administering/workflows.md).
>* 有关端到端社区文章，请参阅 [使用Adobe Experience Manager工作流修改数字资产。](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* 请参阅 [向AEM专家提问工作流网络研讨会](https://bit.ly/ATACE218).
>* 有关端到端社区文章，请参阅 [创建自定义Adobe Experience Manager 6.3动态参与者步骤](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* 对信息位置的更改请参阅 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 和 [工作流最佳实践 — 位置](/help/sites-developing/workflows-best-practices.md#locations).
>


## 模型 {#model}

A `WorkflowModel` 表示工作流的定义（模型）。 它由 `WorkflowNodes` 和 `WorkflowTransitions`. 过渡连接节点并定义 *流量*. “模型”(Model)始终具有起始节点和结束节点。

### 运行时模型 {#runtime-model}

工作流模型已进行版本控制。 运行工作流实例时，它将使用（并保留）工作流的运行时模型（在工作流启动时可用）。

运行时模型为 [生成时间 **同步** 在工作流模型编辑器中触发](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

对所发生的工作流模型和/或所生成的运行时模型的编辑， *after* 启动的特定实例将不会应用到该实例。

>[!CAUTION]
>
>所执行的步骤由 [运行时模型](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model);这是在 **同步** 操作在工作流模型编辑器中触发。
>
>如果在此时间点之后工作流模型发生更改(如果 **同步** 触发)，则运行时实例将不会反映这些更改。 只有更新后生成的运行时模型才会反映这些更改。 基础ECMA脚本除外，它们只保留一次，因此对这些脚本进行了更改。

### 步骤 {#step}

每个步骤都完成一个离散的任务。 工作流步骤有不同类型：

* 参与者（用户/组）：这些步骤将生成一个工作项并将其分配给用户或组。 用户必须完成工作项才能推进工作流。
* 进程（脚本、Java方法调用）：这些步骤由系统自动执行。 ECMA脚本或Java类实现该步骤。 可以开发服务来监听特殊的工作流事件并根据业务逻辑执行任务。
* 容器（子工作流）：此类步骤将启动另一个工作流模型。
* 或拆分/连接：使用逻辑确定在工作流中要执行的下一步。
* 和拆分/连接：允许同时执行多个步骤。

所有步骤都共享以下通用属性： `Autoadvance` 和 `Timeout` 警报（可脚本编写）。

### 过渡 {#transition}

A `WorkflowTransition` 表示两个 `WorkflowNodes` a `WorkflowModel`.

* 它定义两个连续步骤之间的链接。
* 可以应用规则。

### 工作项 {#workitem}

A `WorkItem` 是通过 `Workflow` 实例 `WorkflowModel`. 它包含 `WorkflowData` 实例所执行并引用 `WorkflowNode` 描述基础工作流步骤的信息。

* 它用于标识任务并放入相应的收件箱中。
* 工作流实例可以具有一个或多个 `WorkItems` 同时（取决于工作流模型）。
* 的 `WorkItem` 引用工作流实例。
* 在存储库中， `WorkItem` 存储在工作流实例的下方。

### 有效负荷 {#payload}

引用必须通过工作流进行高级的资源。

有效负载实施引用存储库中的资源（按路径、UUID或URL）或序列化的java对象。 在存储库中引用资源非常灵活，并且与sling结合使用非常有效；例如，引用的节点可以呈现为表单。

### 生命周期 {#lifecycle}

启动新工作流时（通过选择相应的工作流模型并定义有效负荷）创建，并在处理结束节点时结束。

可以对工作流实例执行以下操作：

* 终止
* 暂停
* 继续
* 重新启动

已完成和终止的实例将被存档。

### 收件箱 {#inbox}

每个用户帐户都有其自己的工作流收件箱，分配了 `WorkItems` 可访问。

的 `WorkItems` 会直接分配给用户帐户或分配给其所属的组。

### 工作流类型 {#workflow-types}

工作流有各种类型的工作流，如工作流模型控制台中所示：

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **默认**

   这些是标准AEM实例中包含的现成工作流。

* 自定义工作流（控制台中没有指示器）

   这些工作流是创建为新工作流，或来自覆盖了自定义的现成工作流。

* **旧版**

   在以前版本的AEM中创建的工作流。 这些组件可以在升级期间保留，或从以前版本导出为工作流包，然后导入到新版本中。

### 瞬态工作流 {#transient-workflows}

标准工作流在执行运行时（历史记录）信息时会保存这些信息。 您还可以将工作流模型定义为 **瞬态** 避免这样的历史被持续存在。 这用于性能调整，因为它节省/避免了用于保留信息的时间/资源。

临时工作流可用于以下任何工作流：

* 经常运行。
* 不需要工作流历史记录。

引入了瞬态工作流以加载大量资产，其中资产信息很重要，但工作流运行时历史记录不重要。

>[!NOTE]
>
>请参阅 [创建临时工作流](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) 以了解更多详细信息。

>[!CAUTION]
>
>当工作流模型标记为“临时”时，有一些情况仍会保留运行时信息：
>
>* 负载类型（例如，视频）需要外部步骤进行处理；在这种情况下，需要运行时历史记录才能进行状态确认。
>* 工作流会进入 **和拆分**;在这种情况下，需要运行时历史记录才能进行状态确认。
>* 临时工作流进入参与者步骤时，会（在运行时）将模式更改为非临时；当任务被传递给某个人时，需要保留历史
>


>[!CAUTION]
>
>在临时工作流中，您不应使用 **跳转步骤**.
>
>这是 **跳转步骤** 创建sling作业以在 `goto` 指向。 这会破坏使工作流处于临时状态的目的，并在日志文件中生成错误。
>
>要在临时工作流中做出决策，您可以使用 **或拆分**.

>[!NOTE]
>
>请参阅 [资产最佳实践](/help/assets/performance-tuning-guidelines.md#transient-workflows) 有关瞬态工作流如何影响资产性能的更多信息。

### 多资源支持 {#multi-resource-support}

激活 **多资源支持** 对于工作流模型，意味着即使您选择了多个资源，也会启动单个工作流实例；这些文件将作为包附加。

如果 **多资源支持** 未为工作流模型激活并选择多个资源，则将为每个资源启动单个工作流实例。

>[!NOTE]
>
>请参阅 [为多资源支持配置工作流](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 以了解更多详细信息。

### 工作流阶段 {#workflow-stages}

工作流阶段有助于在处理任务时可视化工作流的进度。 它们可用于提供工作流处理过程的概述，例如，当运行工作流时，用户可以查看 **阶段** （而不是单个步骤）。

由于单个步骤名称可以是特定的、技术性的，因此可以定义阶段名称以提供工作流进度的概念视图。

例如，对于包含六个步骤和四个阶段的工作流：

1. 您可以 [配置工作流阶段（显示工作流进度），然后将相应的阶段分配给工作流中的每个步骤](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * 可以创建多个阶段名称。
   * 然后，将单个阶段名称分配给每个步骤（可以将阶段名称分配给一个或多个步骤）。

   | **步骤名称** | **阶段（分配给步骤）** |
   |---|---|
   | 步骤 1 | 创建 |
   | 步骤 2 | 创建 |
   | 步骤 3 | 审核 |
   | 步骤 4 | 批准 |
   | 步骤 5 | 完成 |
   | 步骤 6 | 完成 |

1. 运行工作流时，用户可以根据阶段名称（而不是步骤名称）查看进度。 工作流进度将显示在 [工作项任务详细信息窗口的“工作流信息”选项卡](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) 在 [收件箱](/help/sites-authoring/inbox.md).

### 工作流和Forms {#workflows-and-forms}

通常，工作流用于处理AEM中的表单提交。 这可以是 [核心组件表单组件](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) 在标准AEM实例中可用，或 [AEM Forms解决方案](/help/forms/using/aem-forms-workflow.md).

创建新表单时，表单提交可轻松与工作流模型关联；例如，将内容存储在存储库的特定位置，或通知用户表单提交及其内容。

### 工作流和翻译 {#workflows-and-translation}

工作流也是 [翻译](/help/sites-administering/translation.md) 进程。
