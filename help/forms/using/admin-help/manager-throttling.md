---
title: Work Manager和调节
seo-title: Work Manager和调节
description: 本文档提供有关Work Manager的背景信息，并提供有关配置Work Manager限制选项的说明。
seo-description: 本文档提供有关Work Manager的背景信息，并提供有关配置Work Manager限制选项的说明。
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Work Manager和调节{#work-manager-and-throttling}

AEM表单（及更早版本）使用JMS队列异步执行操作。 在AEM表单中，JMS队列已被Work Manager替换。 本文档提供有关Work Manager的背景信息，并提供有关配置Work Manager限制选项的说明。

## 关于长期（异步）操作 {#about-long-lived-asynchronous-operations}

在AEM表单中，由服务执行的操作可以是短期（同步）或长期（异步）操作。 短时间操作在从中调用它们的同一线程上同步完成。 这些操作在继续之前等待响应。

长期运营可能会跨系统，甚至延伸到组织之外，例如，客户必须填写并提交贷款申请表，作为集成多个自动化和人力任务的大型解决方案的一部分。 此类行动必须在等待答复时继续进行。 长期业务以异步方式完成其基础工作，允许在等待完成时以其他方式参与资源。 与短期操作不同，一旦调用长期操作，Work Manager就不会认为该操作已完成。 必须出现外部触发器，例如请求对同一服务执行另一操作的系统或提交表单的用户，以完成该操作。

## 关于Work Manager {#about-work-manager}

AEM表单（及更早版本）使用JMS队列异步执行操作。 AEM表单使用Work Manager通过受管线程计划和执行异步操作。

异步操作以下列方式处理：

1. Work Manager接收要执行的工作项。
1. Work Manager将工作项存储在数据库表中，并为工作项分配唯一标识符。 数据库记录包含执行工作项所需的所有信息。
1. 当线程空闲时，Work Manager线程会拉入工作项。 在提取工作项之前，线程可以检查所需服务是否已启动，是否有足够的堆大小来拉入下一个工作项，以及是否有足够的CPU周期来处理工作项。 Oracle Work Manager还会在计划执行工作项时评估其属性（如其优先级）。

AEM表单管理员可以使用运行状况监视程序检查Work Manager统计信息，如队列中的工作项数量及其状态。 您还可以使用运行状况监视器暂停、恢复、重试或删除工作项。 (请参阅 [与Work Manager相关的视图统计信息](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)。)

## 配置Work Manager限制选项 {#configuring-work-manager-throttling-options}

您可以为Work Manager配置限制，以便仅在有足够的可用内存资源时才计划工作项。 通过在应用程序服务器中设置以下JVM选项来配置限制。

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
   <td><p>指定Work Manager在其队列中检查新项目时使用的时间间隔（以毫秒为单位）。</p><p>此选项的值是整数。 默认值是毫 <code>1000</code> 秒（1秒）。 </p><p>如果异步调用量较低，则可以增加此值。 例如，您可以将它增加到2000到5000（2到5秒）之间。 </p><p>如果异步调用量较大，则默认值应足够，但您可以根据需要使用较小的值。 将此值减少太多（例如，低于50，导致轮询频率为每秒20次）会导致系统的大量开销。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>将此选项设置为 <code>true</code> 启用调试模式，或将其设置为false以禁用。 </p><p>在调试模式下，将记录有关违反Work Manager策略和Work Manager暂停／恢复操作的消息。 仅在进行疑难解答时，将此选项设置为true。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>将此选项设 <code>true</code> 置为根据下面所述的内存控制设置启用限制，或禁 <code>false</code> 用限制。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>指定在Work Manager限制传入作业之前可以使用的最大内存百分比。</p><p>此选项的默认值是 <code>95</code>。 对于大多数系统，此值应是合适的。 仅在系统需要达到其最大容量时增加它。 但请注意，随着此值的增加，内存不足问题的风险也会增加。</p><p>如果在群集环境中运行AEM表单，您可能希望在群集的不同节点上以不同方式设置内存控制限制设置。 例如，您可以对节点A和B设置较低的上限，这些节点在负载平衡器中编写，用于交互工作。 您可以对节点C和D设置较高的上限，这些限制不由负载平衡器使用，但保留用于异步工作。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>指定在Work Manager停止限制传入作业之前可以使用的最大内存百分比。</p><p>此选项的默认值是 <code>20</code>。 对于大多数系统，此值应是合适的。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>指定Workmanager的最大批量大小。 默认批大小为10。</p><p>如果即使在完成任务后，Workmanager中进程的状态也未更新，则将批大小设置为1。</p></td>
  </tr>
 </tbody>
</table>

**向JBoss添加Java选项**

1. 停止JBoss应用程序服务器。
1. 在编辑 *[器中打开appserver root]*/bin/run.bat(Windows)或run.sh（Linux或UNIX），并根据需要以格式添加任何Java选项 `-Dproperty=value`。
1. 重新启动服务器。

**将Java选项添加到WebLogic**

1. 开始WebLogic管理控制台，方法是在Web `https://[host name]:[port]/console` 浏览器中键入内容。
1. 键入您为WebLogic服务器域创建的用户名和密码，然后单击“更改中心”下的“日志”，然后单击“锁定并编辑”。
1. 在“域结构”下，单击“环境”>“服务器”，然后在右侧窗格中单击受控服务器名称。
1. 在下一个屏幕上，单击“配置”选项卡>“服务器开始”选项卡。
1. 在“参数”框中，将所需的参数追加到当前内容的末尾。 例如，要禁用健康监视器，请添加：

   `-Dadobe.healthmonitor.enabled=false` 禁用健康监视器。

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

**将Java选项添加到WebSphere**

1. 在WebSphere管理控制台导航树中，单击“服务器”>“服务器类型”>“WebSphere应用程序服务器”。
1. 在右窗格中，单击服务器名称。
1. 在“服务器基础结构”下，单击“Java”和“表单工作流”>“进程定义”。
1. 在“其他属性”下，单击“Java虚拟机”。
1. 在“通用JVM参数”框中，键入所需的参数。
1. 单击“确定”或“应用”，然后单击“直接保存到主配置”。

