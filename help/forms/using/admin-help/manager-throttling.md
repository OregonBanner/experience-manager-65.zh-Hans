---
title: Work Manager和限制
seo-title: Work Manager和限制
description: 本文档提供了有关Work Manager的背景信息，并提供了有关配置Work Manager限制选项的说明。
seo-description: 本文档提供了有关Work Manager的背景信息，并提供了有关配置Work Manager限制选项的说明。
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---

# Work Manager和限制{#work-manager-and-throttling}

AEM表单（及更早版本）使用JMS队列异步执行操作。 在AEM表单中，JMS队列已被Work Manager替换。 本文档提供了有关Work Manager的背景信息，并提供了有关配置Work Manager限制选项的说明。

## 关于长时间（异步）操作{#about-long-lived-asynchronous-operations}

在AEM表单中，由服务执行的操作可以是短期（同步）操作，也可以是长期（异步）操作。 在从中调用它们的同一线程上同步完成短期操作。 这些操作需要等待响应才能继续。

长期运营可能会跨越系统，甚至延伸到组织之外，例如，客户必须完成并提交贷款申请表，作为集成多个自动化和人力任务的大型解决方案的一部分。 在等待答复的同时，这些行动必须继续。 长期运营可以异步执行其底层工作，从而允许在等待完成时以其他方式参与资源。 与短期操作不同，工作管理器在调用后不会认为长期操作已完成。 必须出现外部触发器，例如在同一服务上请求另一个操作的系统或提交表单的用户，才能完成操作。

## 关于Work Manager {#about-work-manager}

AEM表单（及更早版本）使用JMS队列异步执行操作。 AEM Forms使用Work Manager通过托管线程计划和执行异步操作。

异步操作以下方式处理：

1. 工作管理器接收要执行的工作项。
1. Work Manager将工作项存储在数据库表中，并为工作项分配唯一标识符。 数据库记录包含执行工作项所需的所有信息。
1. 当线程空闲时，Work Manager线程会提取工作项。 在提取工作项之前，线程可以检查所需的服务是否已启动，是否有足够的堆大小来提取下一个工作项，以及是否有足够的CPU周期来处理该工作项。 Work Manager还会在计划执行工作项时评估其属性（如其优先级）。

AEM Forms管理员可以使用运行状况监视器来检查Work Manager统计信息，如队列中工作项的数量及其状态。 您还可以使用运行状况监视器来暂停、恢复、重试或删除工作项。 （请参阅[查看与Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)相关的统计信息。）

## 配置Work Manager限制选项{#configuring-work-manager-throttling-options}

您可以为Work Manager配置限制，以便仅在有足够的可用内存资源时才计划工作项目。 通过在应用程序服务器中设置以下JVM选项来配置限制。

<table>
 <thead>
  <tr>
   <th><p>属性</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>指定Work Manager在检查其队列中的新项目时所使用的时间间隔（以毫秒为单位）。</p><p>此选项的值是一个整数。 默认值为<code>1000</code>毫秒（1秒）。 </p><p>如果异步调用的数量较少，则可以增加此值。 例如，您可以将其增加到2000到5000（2到5秒）之间的某个时间段。 </p><p>如果异步调用的数量较大，则默认值应该足够，但您可以根据需要使用较小的值。 过多地降低此值（例如，低于50，导致轮询频率为每秒20次）会导致系统产生大量开销。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>将此选项设置为<code>true</code>以启用调试模式，或将其设置为false以禁用。 </p><p>在调试模式下，将记录有关Work Manager策略违规和Work Manager暂停/恢复操作的消息。 仅当进行故障诊断时，才将此选项设置为true。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>将此选项设置为<code>true</code>以根据下面所述的内存控制设置启用限制，或将此选项设置为<code>false</code>以禁用限制。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>指定在Work Manager限制传入作业之前可使用的内存的最大百分比。</p><p>此选项的默认值为<code>95</code>。 此值对于大多数系统来说都是合适的。 仅当您的系统需要推送到其最大容量时，才应增加容量。 但请注意，随着此值的增加，内存不足问题的风险也会增加。</p><p>如果您在群集环境中运行AEM表单，则可能需要在群集的不同节点上以不同方式设置内存控制限制设置。 例如，您可以对节点A和B设置较低的上限，这两个节点是在负载平衡器中编程的，用于进行交互式工作。 而且您可以在节点C和D上设置更高的高限值，这些高限值不由负载平衡器使用，但保留用于异步工作。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>指定在Work Manager停止限制传入作业之前，可使用的内存的最大百分比。</p><p>此选项的默认值为<code>20</code>。 此值对于大多数系统来说都是合适的。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>指定Workmanager的批处理大小上限。 默认批次大小为10。</p><p>如果即使任务完成后仍未更新Workmanager中进程的状态，则将批次大小设置为1。</p></td>
  </tr>
 </tbody>
</table>

**将Java选项添加到JBoss**

1. 停止JBoss应用程序服务器。
1. 在编辑器中打开&#x200B;*[appserver root]*/bin/run.bat(Windows)或run.sh（Linux或UNIX），并根据需要以`-Dproperty=value`格式添加任何Java选项。
1. 重新启动服务器。

**将Java选项添加到WebLogic**

1. 在Web浏览器中键入`https://[host name]:[port]/console`以启动WebLogic管理控制台。
1. 键入您为WebLogic Server域创建的用户名和密码，然后单击“更改中心”下的“日志”，然后单击“锁定并编辑”。
1. 在“域结构”下，单击“环境”>“服务器”，然后在右窗格中，单击受控服务器名称。
1. 在下一个屏幕上，单击“配置”选项卡>“服务器开始”选项卡。
1. 在参数框中，将所需的参数附加到当前内容的末尾。 例如，要禁用运行状况监视器，请添加：

   `-Dadobe.healthmonitor.enabled=false` 禁用运行状况监视器。

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

**将Java选项添加到WebSphere**

1. 在WebSphere管理控制台导航树中，单击“服务器”>“服务器类型”>“WebSphere应用程序服务器”。
1. 在右窗格中，单击服务器名称。
1. 在“服务器基础架构”下，单击Java和表单工作流>进程定义。
1. 在“其他属性”下，单击“Java虚拟机”。
1. 在“通用JVM参数”框中，键入所需的参数。
1. 单击确定或应用，然后单击直接保存到主控配置。
