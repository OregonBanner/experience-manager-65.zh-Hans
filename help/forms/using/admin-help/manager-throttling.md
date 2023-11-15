---
title: 工作管理器和限制
description: 本文档提供了有关工作管理器的背景信息，并提供了有关配置工作管理器限制选项的说明。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# 工作管理器和限制{#work-manager-and-throttling}

AEM表单（及更早版本）使用JMS队列异步执行操作。 在AEM表单中，JMS队列已由工作管理器取代。 本文档提供了有关工作管理器的背景信息，并提供了有关配置工作管理器限制选项的说明。

## 关于长期（异步）操作 {#about-long-lived-asynchronous-operations}

在AEM表单中，服务执行的操作可以是短期的（同步），也可以是长期的（异步）。 短期操作在从中调用它们的同一线程上同步完成。 这些操作在继续之前会等待响应。

长期运营可能跨多个系统，甚至可能扩展到组织之外，例如，客户必须填写并提交贷款申请表，作为集成多个自动化和人工任务的较大解决方案的一部分。 在等待回应的同时，这种行动必须继续进行。 长寿运营以异步方式执行其基础工作，从而允许资源在等待完成时以其他方式参与。 与短期操作不同，工作管理器在调用长期操作后并不认为该操作已完成。 必须发生外部触发器（如请求对同一服务执行其他操作的系统或提交表单的用户）才能完成操作。

## 关于工作管理器 {#about-work-manager}

AEM表单（及更早版本）使用JMS队列异步执行操作。 AEM Forms使用工作管理器通过托管线程来计划和执行异步操作。

异步操作按以下方式处理：

1. 工作管理器接收要执行的工作项。
1. 工作管理器将工作项存储在数据库表中，并为工作项分配唯一标识符。 数据库记录包含执行工作项所需的所有信息。
1. 当线程空闲时，工作管理器线程拉入工作项。 在拉入工作项之前，线程可以检查所需的服务是否已启动，是否有足够的栈大小来拉入下一个工作项，以及是否有足够的CPU周期来处理该工作项。 在安排执行时，工作管理器还会评估工作项的属性（如优先级）。

AEM forms管理员可以使用运行状况监视器检查Work Manager统计信息，例如队列中的工作项数及其状态。 您还可以使用运行状况监视器暂停、继续、重试或删除工作项。 (请参阅 [查看与工作管理器相关的统计信息](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## 配置工作管理器限制选项 {#configuring-work-manager-throttling-options}

您可以为工作管理器配置限制，以便仅在有足够的可用内存资源时计划工作项。 您可通过在应用程序服务器中设置以下JVM选项来配置限制。

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
   <td><p>指定工作管理器在检查其队列中的新项目时使用的时间间隔（以毫秒为单位）。</p><p>此选项的值是一个整数。 默认值为 <code>1000</code> 毫秒（1秒）。 </p><p>如果异步调用的数量较少，则可以增加此值。 例如，您可以将其增加到2000到5000（2-5秒）之间的某个值。 </p><p>如果异步调用的数量很大，则默认值应就足够了，但如有必要，您可以使用较低的值。 过多地降低此值（例如，低于50，这会导致轮询频率为每秒20次）会导致系统产生大量开销。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>将此选项设置为 <code>true</code> 启用调试模式，或设置为false禁用调试模式。 </p><p>在调试模式下，将记录有关Work Manager策略违规和Work Manager暂停/恢复操作的消息。 仅在进行故障诊断时将此选项设置为true。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>将此选项设置为 <code>true</code> 启用基于下述内存控制设置的限制，或者 <code>false</code> 以禁用限制。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>指定工作管理器限制传入作业之前可以使用的最大内存百分比。</p><p>此选项的默认值为 <code>95</code>. 该值对于大多数系统应该都是合适的。 仅当您的系统需要推送到其最大容量时才增加容量。 但请注意，随着此值的增加，内存不足问题的风险也会增加。</p><p>如果在群集环境中运行AEM表单，则可能需要在群集的不同节点上以不同的方式设置内存控制限制设置。 例如，节点A和B的上限可能较低，这两个节点均在负载平衡器中编程以用于交互式工作。 此外，您还可以在节点C和D上设置更高的高限制，负载平衡器不使用这些节点，而是将其保留用于异步工作。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>指定工作管理器停止限制传入作业之前可以使用的最大内存百分比。</p><p>此选项的默认值为 <code>20</code>. 该值对于大多数系统应该都是合适的。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>指定Workmanager的最大批次大小。 默认批次大小为10。</p><p>如果即使在任务完成后，Workmanager中进程的状态也未更新，则将批次大小设置为1。</p></td>
  </tr>
 </tbody>
</table>

**将Java选项添加到JBoss**

1. 停止JBoss应用程序服务器。
1. 打开 *[appserver根]*/bin/run.bat (Windows)或run.sh （Linux或UNIX），并根据需要以格式添加任何Java选项 `-Dproperty=value`.
1. 重新启动服务器。

**将Java选项添加到WebLogic**

1. 通过键入以下内容启动WebLogic管理控制台 `https://[host name]:[port]/console` 在Web浏览器中。
1. 键入为WebLogic Server域创建的用户名和密码，然后单击“更改中心”下的“日志”，然后单击“锁定和编辑”。
1. 在“域结构”下，单击“环境”>“服务器”，然后在右窗格中单击受控服务器名称。
1. 在下一个屏幕上，单击Configuration选项卡> Server Start选项卡。
1. 在“参数”框中，将所需的参数附加到当前内容的末尾。 例如，要禁用运行状况监视器，请添加：

   `-Dadobe.healthmonitor.enabled=false` 禁用运行状况监视器。

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

**将Java选项添加到WebSphere**

1. 在WebSphere管理控制台导航树中，单击“服务器”>“服务器类型”>“WebSphere应用程序服务器”。
1. 在右窗格中，单击服务器名称。
1. 在“服务器基础架构”下，单击“Java和表单工作流”>“进程定义”。
1. 在“其他属性”下，单击“Java虚拟机”。
1. 在“通用JVM参数”框中，键入所需的参数。
1. 单击确定或应用，然后单击直接保存到主配置。
