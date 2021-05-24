---
title: 工作流最佳实践
seo-title: 工作流最佳实践
description: 工作流最佳实践
seo-description: 'null'
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 1%

---

# 工作流最佳实践{#workflow-best-practices}

工作流可让您自动执行Adobe Experience Manager(AEM)活动。

它们通常表示在AEM环境中发生的大量处理，因此当自定义工作流步骤没有根据最佳实践写入，或者现成工作流未配置为尽可能高效地运行时，系统可能会因此而受到影响。

因此，强烈建议仔细规划工作流的实施。

## 配置 {#configuration}

在配置工作流流程（自定义和/或即装即用）时，应牢记以下几点。

### 瞬态工作流 {#transient-workflows}

要优化高摄取负载，您可以将[工作流定义为临时](/help/sites-developing/workflows.md#transient-workflows)。

当工作流是临时的时候，与中间工作步骤相关的运行时数据在运行时不会保留在JCR中（当然会保留输出演绎版）。

优点包括：

* 缩短工作流处理时间；最多10%。
* 显着降低了存储库的增长。
* 不再需要CRUD工作流即可清除。
* 此外，它还可减少TAR文件的数量，以便压缩文件。

>[!CAUTION]
>
>如果您的业务要求您出于审核目的保留/存档工作流运行时数据，请不要启用此功能。

### 调整DAM工作流{#tuning-dam-workflows}

有关DAM工作流的性能调整指南，请参阅[AEM Assets性能调整指南](/help/assets/performance-tuning-guidelines.md)。

### 配置并发工作流的最大数{#configure-the-maximum-number-of-concurrent-workflows}

AEM可以允许同时运行多个工作流线程。 默认情况下，线程数配置为系统上处理器内核数的一半。

如果执行的工作流要求系统资源，则这可能意味着AEM将很少用于其他任务，如渲染创作UI。 因此，在批量图像上传等活动期间，系统可能运行缓慢。

要解决此问题，Adobe建议将&#x200B;**最大并行作业数**&#x200B;配置为系统上处理器内核数的半数到四分之三。 这应该允许系统有足够的容量在处理这些工作流时保持响应。

要配置&#x200B;**最大并行作业数**，您可以：

* 从AEM Web控制台中配置&#x200B;**[OSGi配置](/help/sites-deploying/configuring-osgi.md)**;对于&#x200B;**队列：Granite工作流队列**（**Apache Sling作业队列配置**）。

* 通过AEM Web控制台的&#x200B;**Sling作业**&#x200B;选项配置队列；对于&#x200B;**作业队列配置：Granite工作流队列**，位于`http://localhost:4502/system/console/slingevent`。

此外，还为&#x200B;**Granite工作流外部进程作业队列**&#x200B;提供了单独的配置。 它用于启动外部二进制文件的工作流进程，例如&#x200B;**InDesign Server**&#x200B;或&#x200B;**图像Magick**。

### 配置单个作业队列{#configure-individual-job-queues}

在某些情况下，配置单个作业队列以在单个作业的基础上控制并发线程或其他队列选项非常有用。 您可以通过&#x200B;**Apache Sling作业队列配置**&#x200B;工厂从Web控制台添加和配置单个队列。 要查找要列出的相应主题，请执行工作流的模型并在&#x200B;**Sling作业**&#x200B;控制台中查找该模型；例如，在`http://localhost:4502/system/console/slingevent`。

也可以为临时工作流添加单个作业队列。

### 配置工作流清除{#configure-workflow-purging}

在标准安装中， AEM提供维护控制台，可在其中安排和配置每日和每周的维护活动；例如，在：

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

默认情况下，**每周维护窗口**&#x200B;具有&#x200B;**工作流清除**&#x200B;任务，但需要在该任务运行之前对其进行配置。 要配置工作流清除，必须在Web控制台中添加新的&#x200B;**AdobeGranite工作流清除配置**。

有关AEM中维护任务的更多详细信息，请参阅[操作功能板](/help/sites-administering/operations-dashboard.md)。

## 自定义 {#customization}

编写自定义工作流流程时，应牢记一些事项。

### 位置 {#locations}

工作流模型、启动器、脚本和通知的定义按类型保存在存储库中；例如，现成、自定义等。

>[!NOTE]
>
>另请参阅AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的[存储库重组。

#### 位置 — 工作流模型{#locations-workflow-models}

工作流模型根据类型存储在存储库中：

* 开箱即用的工作流设计位于以下路径下：

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >请勿：
   >
   >* 将任何自定义工作流模型放置在此文件夹中
   >* 编辑`/libs`中的任何内容

   >
   >由于任何更改在升级或安装修补程序、累积修补程序包或Service Pack时可能会被覆盖，因此。

* 自定义工作流设计保留在以下位置：

   ```
   /conf/global/settings/workflow/models/...
   ```

* 运行时工作流设计（现成和自定义）保留在以下路径下：

   `/var/workflow/models/`

* 旧版工作流设计（设计时和运行时）保留在以下路径下：

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >如果使用AEM UI *编辑了这些设计*，则详细信息将会复制到新位置。

#### 位置 — 工作流启动器{#locations-workflow-launchers}

工作流启动器定义也根据类型存储在存储库中：

* 开箱即用的工作流启动器按以下路径持有：

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >请勿：
   >
   >* 将任何自定义工作流启动器放入此文件夹中
   >* 编辑`/libs`中的任何内容

   >
   >由于任何更改在升级或安装修补程序、累积修补程序包或Service Pack时可能会被覆盖，因此。

* 自定义工作流启动器位于：

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* 旧版工作流启动器位于以下路径下：

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >如果使用AEM UI *编辑这些定义*，则详细信息将会复制到新位置。

#### 位置 — 工作流脚本{#locations-workflow-scripts}

工作流脚本也会根据类型存储在存储库中：

* 现成工作流脚本保存在以下路径下：

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >请勿：
   >
   >* 将任何自定义工作流脚本放入此文件夹中
   >* 编辑`/libs`中的任何内容

   >
   >由于任何更改在升级或安装修补程序、累积修补程序包或Service Pack时可能会被覆盖，因此。

* 自定义工作流脚本保留在以下位置：

   ```
   /apps/workflow/scripts/...
   ```

* 旧版工作流脚本保留在以下路径下：

   `/etc/workflow/scripts/`

#### 位置 — 工作流通知{#locations-workflow-notifications}

工作流通知也会根据类型存储在存储库中：

* 开箱即用的工作流通知定义按以下路径保留：

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >请勿：
   >
   >* 将任何自定义工作流通知定义放置在此文件夹中
   >* 编辑`/libs`中的任何内容

   >
   >由于任何更改在升级或安装修补程序、累积修补程序包或Service Pack时可能会被覆盖，因此。

* 自定义工作流通知定义保留在以下位置：

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >如果要覆盖工作流通知文本，请在下创建一个覆盖的路径：
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* 旧版工作流通知定义保存在以下路径下：

   `/etc/workflow/notification/`

### 进程会话{#process-sessions}

与任何自定义开发一样，始终建议尽可能使用用户的会话：

* 以最好地遵守安全准则
* 允许系统管理会话的打开和关闭

实施工作流流程时：

* 将提供并应使用工作流会话，除非有令人信服的理由不提供。
* 不应从工作流步骤中创建新会话，因为这会导致状态不一致以及工作流引擎中可能出现的并发问题。
* 您不应从工作流中的流程步骤中获取新的JCR会话；您应将流程步骤API提供的工作流会话调整为jcr会话。 例如：

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

保存会话：

* 在工作流进程中，如果使用`WorkflowSession`修改存储库，则不要显式保存会话 — 工作流将在会话完成后保存该会话。
* `Session.Save` 不应从工作流步骤中调用：

   * 建议修改工作流jcr会话；然后，由于工作流引擎在工作流完成执行后自动保存会话，因此不需要`save`。
   * 不建议流程步骤创建自己的jcr会话。

* 通过消除不必要的保存，您可以减少开销，从而提高工作流的效率。

>[!CAUTION]
>
>如果尽管在此处提出了建议，但您确实创建了自己的jcr会话，则需要保存该会话。

### 最小化启动器数量/范围{#minimize-the-number-scope-of-launchers}

有一个侦听器负责所有已注册的[工作流启动器](/help/sites-administering/workflows-starting.md#workflows-launchers):

* 它将监听其他启动器的代换属性中指定的所有路径的更改。
* 在调度事件时，工作流引擎将评估每个启动器，以确定它是否应运行。

创建过多的启动器将导致评估过程运行更慢。

在单个启动器上的存储库根目录中创建通配路径，将导致工作流引擎侦听并评估对存储库中每个节点的创建/修改事件。 因此，建议仅创建所需的启动器，并尽可能使通配路径具体。

由于这些启动器对工作流行为的影响，禁用任何未使用的现成启动器也会有所帮助。

### 启动器{#configuration-enhancements-for-launchers}的配置增强

自定义[启动器配置](/help/sites-administering/workflows-starting.md#workflows-launchers)已得到增强，可支持以下内容：

* 将多个条件“AND”绑定在一起。
* 在单个条件中具有OR条件。
* 根据是启用还是禁用功能标志来禁用/启用启动器。
* 在启动器条件中支持正则表达式。

### 请勿从其他工作流启动工作流{#do-not-start-workflows-from-other-workflows}

无论是在内存中创建的对象，还是在存储库中跟踪的节点，工作流都可能产生大量开销。 因此，最好让工作流自行处理，而不是启动其他工作流。

例如，一个工作流可对一组内容实施业务流程，然后激活该内容。 最好创建一个可激活其中每个节点的自定义工作流进程，而不是为每个需要发布的内容节点启动&#x200B;**激活内容**&#x200B;模型。 此方法将需要额外的开发工作，但与为每个激活启动单独的工作流实例相比，其执行效率更高。

另一个示例是处理多个节点的工作流，创建工作流包，然后激活所述包。 您可以在创建资源包的步骤中更改工作流的有效负荷，然后调用该步骤以在同一工作流模型中激活资源包，而不是先创建资源包，然后再以该资源包作为有效负荷启动单独的工作流。

### 处理程序前进 {#handler-advance}

设计工作流模型时，您可以选择在工作流步骤中启用处理程序前进。 或者，您也可以向工作流步骤中添加代码，以确定下一步应该运行哪个步骤，然后执行该步骤。

建议使用处理程序高级，因为它可提供更好的性能。

### 工作流阶段{#workflow-stages}

您可以定义[工作流阶段](/help/sites-developing/workflows.md#workflow-stages)，然后将任务/步骤分配给特定的工作流阶段。

当您单击&#x200B;**收件箱**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)&#x200B;中某个工作项的&#x200B;[**工作流信息**&#x200B;选项卡时，此信息用于显示工作流的进度。 可以编辑现有的工作流模型以添加阶段。

### 激活页面处理步骤{#activate-page-process-step}

**激活页面进程**&#x200B;步骤将为您激活页面，但不会自动查找任何引用的DAM资产并激活这些资产。

如果您计划将此步骤用作工作流模型的一部分，请记住这一点。

### 升级注意事项{#upgrade-considerations}

升级实例时：

* 确保在升级实例之前备份任何自定义工作流模型。
* 确认您的任何自定义工作流均未存储在[location](#locations)下：

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>另请参阅AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的[存储库重组。

## 系统工具{#system-tools}

有许多系统工具可用于帮助监控、维护和疑难解答工作流。 以下所有示例URL都使用`localhost:4502`，但应在任何创作实例(`<hostname>:<port>`)上可用。

### Sling作业处理控制台{#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling作业处理控制台将显示：

* 上次重新启动后系统中作业状态的统计信息。
* 它还将显示所有作业队列的配置，并提供在配置管理器中编辑它们的快捷方式。

### 工作流报表工具{#workflow-report-tool}

工作流报告工具将在6.3中删除，以防止性能下降。

### 工作流维护操作MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

工作流维护MBean公开了一些有用的维护例程，例如清除已完成的工作流和检索工作流统计信息。

## 更多信息 {#further-information}

有关更多信息，请参阅：

* [使用工作流](/help/sites-authoring/workflows.md)
* [管理工作流](/help/sites-administering/workflows.md)
* [开发和扩展工作流](/help/sites-developing/workflows.md)
* [性能优化](/help/sites-deploying/configuring-performance.md)
