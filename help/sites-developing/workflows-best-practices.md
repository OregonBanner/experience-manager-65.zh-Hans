---
title: 工作流最佳实践
seo-title: Workflow Best Practices
description: 了解在Adobe Experience Manager中使用工作流的最佳实践。
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1923'
ht-degree: 1%

---

# 工作流最佳实践{#workflow-best-practices}

通过工作流，您可以自动化Adobe Experience Manager (AEM)活动。

它们通常代表AEM环境中发生的大量处理，因此，当自定义工作流步骤未根据最佳实践编写时，或者未将现成工作流配置为尽可能高效地运行时，系统可能会受损。

因此，强烈建议仔细规划工作流实施。

## 配置 {#configuration}

在配置工作流进程（自定义和/或现成）时，有一些事项需要牢记。

### 瞬态工作流 {#transient-workflows}

要优化高摄取负载，您可以定义 [作为临时工作流](/help/sites-developing/workflows.md#transient-workflows).

当工作流是瞬态时，与中间工作步骤相关的运行时数据在运行时不会保留在JCR中（保留输出演绎版）。

其优势可以包括：

* 工作流处理时间减少；最多减少10%。
* 显着减少存储库增长。
* 无需清除其他CRUD工作流。
* 此外，它还减少了要压缩的TAR文件数量。

>[!CAUTION]
>
>如果您的企业要求您保留/存档工作流运行时数据以进行审核，请勿启用此功能。

### 调整DAM工作流 {#tuning-dam-workflows}

有关DAM工作流的性能优化准则，请参阅 [AEM Assets Performance Tuning指南](/help/assets/performance-tuning-guidelines.md).

### 配置最大并发工作流数 {#configure-the-maximum-number-of-concurrent-workflows}

AEM允许同时运行多个工作流线程。 默认情况下，线程数配置为系统处理器内核数的一半。

如果正在执行的工作流需要系统资源，这可能意味着AEM几乎无法将其用于其他任务，例如渲染创作UI。 因此，系统在批量图像上传等活动期间可能会变得缓慢。

要解决此问题，Adobe建议将 **最大并行作业数** 介于系统处理器核心数量的一半到四分之三之间。 这应该允许系统在处理这些工作流时保持响应性的足够容量。

配置 **最大并行作业数**，您可以：

* 配置 **[OSGi配置](/help/sites-deploying/configuring-osgi.md)** 从AEM Web控制台；对于 **队列： Granite工作流队列** (一 **Apache Sling作业队列配置**)。

* 配置队列可以从 **Sling作业** AEM选项；对于 **作业队列配置： Granite工作流队列**，在 `http://localhost:4502/system/console/slingevent`.

此外，还有单独的配置 **Granite工作流外部进程作业队列**. 这用于启动外部二进制文件的工作流进程，例如 **InDesign Server** 或 **Magick图像**.

### 配置单个作业队列 {#configure-individual-job-queues}

在某些情况下，配置单个作业队列来控制并发线程或基于单个作业的其他队列选项会很有用。 您可以通过以下方式从Web控制台添加和配置单个队列 **Apache Sling作业队列配置** 工厂。 要查找要列出的相应主题，请执行工作流模型并在 **Sling作业** 控制台；例如，在 `http://localhost:4502/system/console/slingevent`.

也可以为临时工作流添加单个作业队列。

### 配置工作流清除 {#configure-workflow-purging}

在标准安装中，AEM提供了一个维护控制台，可以在其中计划和配置每日和每周维护活动；例如，在：

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

默认情况下， **每周维护时段** 具有 **工作流清除** 任务，但需要在运行之前对其进行配置。 要配置工作流清除，请使用 **AdobeGranite工作流清除配置** 必须在Web控制台中添加。

有关AEM中维护任务的更多详细信息，请参阅 [操作功能板](/help/sites-administering/operations-dashboard.md).

## 自定义 {#customization}

在编写自定义工作流进程时，有一些事项应牢记。

### 位置 {#locations}

工作流模型、启动器、脚本和通知的定义根据类型保存在存储库中；即现成、自定义等。

>[!NOTE]
>
>另请参阅 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md).

#### 位置 — 工作流模型 {#locations-workflow-models}

工作流模型根据类型存储在存储库中：

* 现成的工作流设计位于以下路径下：

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >请勿：
  >
  >* 将您的任何自定义工作流模型放置在此文件夹中
  >* 编辑任何内容 `/libs`
  >
  >因为任何更改都可能在升级时或在安装热修复程序、累积修补程序包或Service Pack时被覆盖。

* 自定义工作流设计保存在下：

  ```
  /conf/global/settings/workflow/models/...
  ```

* 运行时工作流设计（现成和自定义）保存在以下路径下：

  `/var/workflow/models/`

* 旧版工作流设计（设计时和运行时）保存在以下路径下：

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >如果编辑这些设计 *使用AEM UI*，则详细信息将会复制到新位置。

#### 位置 — 工作流启动器 {#locations-workflow-launchers}

工作流启动器定义还根据类型存储在存储库中：

* 现成的工作流启动器位于以下路径下：

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >请勿：
  >
  >* 将您的任何自定义工作流启动器放置在此文件夹中
  >* 编辑任何内容 `/libs`
  >
  >因为任何更改都可能在升级时或在安装热修复程序、累积修补程序包或Service Pack时被覆盖。

* 自定义工作流启动器位于下：

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* 旧版工作流启动器位于以下路径下：

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >如果编辑了这些定义 *使用AEM UI*，则详细信息将会复制到新位置。

#### 位置 — 工作流脚本 {#locations-workflow-scripts}

工作流脚本还根据类型存储在存储库中：

* 现成的工作流脚本位于以下路径下：

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >请勿：
  >
  >* 将您的任何自定义工作流脚本放在此文件夹中
  >* 编辑任何内容 `/libs`
  >
  >因为任何更改都可能在升级时或在安装热修复程序、累积修补程序包或Service Pack时被覆盖。

* 自定义工作流脚本保存在下：

  ```
  /apps/workflow/scripts/...
  ```

* 旧版工作流脚本保存在以下路径下：

  `/etc/workflow/scripts/`

#### 位置 — 工作流通知 {#locations-workflow-notifications}

工作流通知还根据类型存储在存储库中：

* 现成的工作流通知定义位于以下路径下：

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >请勿：
  >
  >* 将您的任何自定义工作流通知定义放在此文件夹中
  >* 编辑任何内容 `/libs`
  >
  >因为任何更改都可能在升级时或在安装热修复程序、累积修补程序包或Service Pack时被覆盖。

* 自定义工作流通知定义保留在下：

  ```
  /conf/global/settings/workflow/notification/...
  ```

  >[!NOTE]
  >
  >如果要覆盖工作流通知文本，请在以下位置创建一个覆盖的路径：
  >
  >
  >`/conf/global/settings/workflow/notification/<path-under-libs>`

* 旧版工作流通知定义保存在以下路径下：

  `/etc/workflow/notification/`

### 进程会话 {#process-sessions}

与任何自定义开发一样，始终建议尽可能使用用户会话：

* 以最佳方式遵守安全准则
* 允许系统管理会话的打开和关闭

实施工作流进程时：

* 将提供工作流会话，除非有令人信服的理由不提供该会话，否则应使用该会话。
* 不应通过工作流步骤创建新会话，因为这会导致状态不一致，并可能导致工作流引擎中出现并发问题。
* 您不应从工作流中的流程步骤中获取新的JCR会话；您应使流程步骤API提供的工作流会话适应JCR会话。 例如：

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

保存会话：

* 在工作流进程内，如果 `WorkflowSession` 正用于修改存储库，但不明确保存会话 — 工作流完成时将保存会话。
* `Session.Save` 不应从工作流步骤中调用：

   * 建议调整工作流jcr会话； `save` 没有必要使用，因为工作流引擎会在工作流执行完成后自动保存会话。
   * 建议不要对流程步骤创建自己的jcr会话。

* 通过消除不必要的保存，您可以减少开销，从而使工作流更加高效。

>[!CAUTION]
>
>尽管有此处提供的建议，但如果您确实创建了自己的jcr会话，则必须保存它。

### 最大程度地减少启动器的数量/范围 {#minimize-the-number-scope-of-launchers}

有一个监听器负责所有 [工作流启动器](/help/sites-administering/workflows-starting.md#workflows-launchers) 注册的：

* 它会侦听其他启动器的通配属性中指定的所有路径的更改。
* 调度事件后，工作流引擎将评估每个启动器，以确定它是否应运行。

创建过多启动器将导致评估过程运行速度变慢。

在单个启动器的存储库根目录中创建通配路径会导致工作流引擎侦听并评估存储库中每个节点的创建/修改事件。 因此，建议仅创建所需的启动器，并尽可能具体化全局连接路径。

由于这些启动器对工作流行为的影响，禁用任何未使用的现成启动器也会很有用。

### 启动器的配置增强功能 {#configuration-enhancements-for-launchers}

自定义 [启动器配置](/help/sites-administering/workflows-starting.md#workflows-launchers) 已得到增强，可支持以下内容：

* 同时具备多个条件“AND”。
* 在单个条件中具有OR条件。
* 根据功能标志是启用还是禁用，禁用/启用启动器。
* 在启动器条件中支持正则表达式。

### 不要从其他工作流启动工作流 {#do-not-start-workflows-from-other-workflows}

工作流可能会产生大量开销，无论是在内存中创建的对象还是在存储库中跟踪的节点。 因此，最好让工作流在自身中进行处理，而不是启动其他工作流。

例如，某个工作流在一组内容上实施业务流程，然后激活该内容。 最好创建一个自定义工作流进程来激活其中的每个节点，而不是启动 **激活内容** 需要发布的每个内容节点的模型。 此方法将需要额外的开发工作，但在执行时比为每个激活启动单独的工作流实例更有效。

另一个示例是处理多个节点、创建工作流包，然后激活所述包的工作流。 您无需创建资源包，然后启动一个将资源包作为有效负载的单独工作流，您可以在创建资源包的步骤中更改工作流的有效负载，然后调用该步骤以激活同一工作流模型中的资源包。

### 处理程序前进 {#handler-advance}

设计工作流模型时，您可以选择启用工作流步骤上的处理程序前进。 或者，您也可以将代码添加到工作流步骤中，以确定下一步应该运行哪个步骤，然后执行它。

建议使用处理程序前进，因为它可提供更好的性能。

### 工作流暂存 {#workflow-stages}

您可以定义 [工作流暂存](/help/sites-developing/workflows.md#workflow-stages)，然后将任务/步骤分配给特定工作流暂存。

此信息用于在您单击 [**工作流信息** 选项卡中的工作项 **收件箱**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). 可以编辑现有工作流模型以添加暂存。

### 激活页面流程步骤 {#activate-page-process-step}

此 **激活页面进程** 步骤将为您激活页面，但不会自动查找任何引用的DAM资产并激活这些资产。

如果您计划将此步骤用作工作流模型的一部分，请牢记这一点。

### 升级注意事项 {#upgrade-considerations}

升级实例时：

* 确保在升级实例之前备份任何自定义工作流模型。
* 确认您的自定义工作流均未存储在 [位置](#locations)：

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>另请参阅 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md).

## 系统工具 {#system-tools}

有许多系统工具可以帮助监控、维护和排除工作流故障。 以下所有示例URL都使用 `localhost:4502`，但应在任何创作实例上可用( `<hostname>:<port>`)。

### Sling作业处理控制台 {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling作业处理控制台将显示：

* 自上次重新启动以来系统中作业状态的统计信息。
* 它还将显示所有作业队列的配置，并提供在配置管理器中编辑它们的快捷方式。

### 工作流报告工具 {#workflow-report-tool}

将在6.3中删除工作流报告工具，以防止性能下降。

### 工作流维护操作MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

工作流维护MBean公开了几个有用的维护例程，例如清除已完成的工作流和检索工作流统计信息。

## 更多信息 {#further-information}

有关更多信息，请参阅：

* [使用工作流程](/help/sites-authoring/workflows.md)
* [管理工作流程](/help/sites-administering/workflows.md)
* [开发和扩展工作流](/help/sites-developing/workflows.md)
* [性能优化](/help/sites-deploying/configuring-performance.md)
