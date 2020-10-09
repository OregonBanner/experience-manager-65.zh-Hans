---
title: 监控部署的最 [!DNL Assets] 佳实践
description: 监视部署部署部署在部署后 [!DNL Adobe Experience Manager] 的环境和性能的最佳实践。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 1%

---


# 监控部署的最佳 [!DNL Adobe Experience Manager Assets] 实践 {#assets-monitoring-best-practices}

从立场 [!DNL Experience Manager Assets] 看，监测应包括观察和报告下列进程和技术：

* 系统CPU
* 系统内存使用
* 系统磁盘IO和IO等待时间
* 系统网络IO
* 用于堆利用和异步进程(如工作流)的JMX MBean
* OSGi控制台运行状况检查

通常， [!DNL Experience Manager Assets] 可以通过两种方式进行监控：实时监控和长期监控。

## 实时监视 {#live-monitoring}

您应在开发的性能测试阶段或高负载情况下执行实时监视，以了解环境的性能特性。 通常，应使用一套工具执行实时监视。 以下是一些建议：

* [可视VM](https://visualvm.github.io/):Visual VM使您能够视图详细的Java VM信息，包括CPU使用、Java内存使用。 此外，它还允许您对在部署上运行的代码进行采样和评估。
* [顶部](https://man7.org/linux/man-pages/man1/top.1.html):顶部是打开仪表板的Linux命令，显示使用情况统计信息，包括CPU、内存和IO使用情况。 它提供了实例中所发生情况的高级概述。
* [顶部](https://hisham.hm/htop/):Htop是一个交互式流程查看器。 除了Top可以提供的功能外，它还提供详细的CPU和内存使用。 Htop可以使用或安装在大多数Linux系 `yum install htop` 统上 `apt-get install htop`。

* [Iotop](https://guichaz.free.fr/iotop/):Iotop是磁盘IO使用情况的详细仪表板。 它显示描述使用磁盘IO的进程及其使用量的栏和表。 Iotop可以使用或安装在大多数Linux系 `yum install iotop` 统上 `apt-get install iotop`。

* [Iftop](https://www.ex-parrot.com/pdw/iftop/):Iftop显示有关以太网／网络使用的详细信息。 Iftop显示使用以太网的实体的每个通信渠道统计信息以及它们使用的带宽量。 Iftop可以使用或安装在大多数Linux系 `yum install iftop` 统上 `apt-get install iftop`。

* Java Flight Recorder(JFR):Oracle提供的一种商业工具，您可以在非生产环境中自由使用。 有关详细信息，请 [参阅如何使用Java飞行记录器诊断CQ运行时问题](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq)。
* [!DNL Experience Manager] `error.log` 文件：您可以调查文 [!DNL Experience Manager] 件，了 `error.log` 解系统中记录的错误的详细信息。 使用命令 `tail -F quickstart/logs/error.log` 识别要调查的错误。
* [工作流控制台](/help/sites-administering/workflows.md):利用工作流控制台监视滞后或卡住的工作流。

通常，您可以结合使用这些工具来全面了解部署的 [!DNL Experience Manager] 性能。

>[!NOTE]
>
>这些工具是标准工具，不直接受Adobe支持。 他们不需要额外的许可证。

![chlimage_1-33](assets/chlimage_1-143.png)

*图：使用Visual VM工具进行实时监视。*

![chlimage_1-32](assets/chlimage_1-142.png)

## 长期监测 {#long-term-monitoring}

对部署的长期监 [!DNL Experience Manager] 控包括对实时监视的相同部分进行更长时间的监控。 它还包括定义特定于您的环境的警报。

### 日志聚合和报告 {#log-aggregation-and-reporting}

聚合日志有多种可用工具，例如Splunk(TM)和Elastic Search、Logstash和Kabana(ELK)。 要评估部署的正常 [!DNL Experience Manager] 运行时间，您必须了解特定于系统的日志事件并根据它们创建警报。 了解您的开发和操作实践可以帮助您更好地了解如何调整日志聚合过程以生成关键警报。

### 环境监控 {#environment-monitoring}

环境监控包括监控以下内容：

* 网络吞吐量
* 磁盘IO
* 内存
* CPU利用率
* JMX MBean
* 外部网站

您需要NewRelic(TM)和AppDynamics(TM)等外部工具来监视每个项目。 使用这些工具，您可以定义特定于您系统的警报，例如高系统利用率、工作流备份、运行状况检查失败或未经身份验证的网站访问。 Adobe不推荐任何特定工具。 找到适合您的工具，并利用它来监视讨论的项目。

#### 内部应用程序监控 {#internal-application-monitoring}

内部应用程序监视包括通过在平台上构建的自定义 [!DNL Experience Manager] 应用程序代码监视构成堆栈的应用程序组件，包括JVM、内容存储库。 通常，它通过JMX Mbeans执行，可由许多流行的监控解决方案直接进行监控，如SolarWinds(TM),HP OpenView(TM),Hyperic(TM),Zabbix(TM)等。 对于不支持直接连接到JMX的系统，您可以编写外壳脚本以提取JMX数据，并以它们本身理解的格式将其呈现给这些系统。

默认情况下，不启用对JMX Mbeans的远程访问。 有关通过JMX进行监视的详细信息，请参 [阅使用JMX技术的监视和管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html)。

在许多情况下，需要基线来有效地监视统计。 要创建基线，在预定时间段内观察系统在正常工作条件下，然后识别正常度量。

**JVM监视**

与任何基于Java的应用程序堆栈一样， [!DNL Experience Manager] 这取决于通过基础Java虚拟机提供给它的资源。 您可以通过JVM公开的平台MXBean来监视其中许多资源的状态。 有关MXBean的详细信息，请参 [阅使用平台MBean服务器和平台MXBean](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)。

以下是一些可以监视JVM的基准参数：

内存

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* 实例：所有服务器
* 警报阈值：当堆或非堆内存利用率超过相应最大内存的75%时。
* 警报定义：系统内存不足，或代码中有内存泄漏。 分析线程转储以得出定义。

>[!NOTE]
>
>此Bean提供的信息以字节表示。

线程

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* 实例：所有服务器
* 警报阈值：当线程数大于基线的150%时。
* 警报定义：要么存在一个活动失控的过程，要么效率低下的操作消耗大量资源。 分析线程转储以得出定义。

**监视器[!DNL Experience Manager]**

[!DNL Experience Manager] 还通过JMX公开一组统计和操作。 这些功能有助于评估系统运行状况，并在潜在问题影响用户之前找出它们。 有关详细信息，请参 [阅JMX](/help/sites-administering/jmx-console.md) MBean [!DNL Experience Manager] 相关文档。

以下是您可以监视的一些基线参数 [!DNL Experience Manager]:

复制代理

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* 实例：一个作者实例和所有发布实例（适用于刷新代理）
* 警报阈值：当值为 `QueueBlocked` 或 `true` 值大于 `QueueNumEntries` 基线的150%时。

* 警报定义：系统中存在阻止的队列，表明复制目标已关闭或不可到达。 通常，网络或基础架构问题会导致过多条目排队，从而对系统性能产生不利影响。

>[!NOTE]
>
>对于MBean和URL参数， `<AGENT_NAME>` 替换为要监视的复制代理的名称。

会话计数器

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository统计信息&quot;,type*=&quot;RepositoryStats&quot;
* 实例：所有服务器
* 警报阈值：当打开的会话超过基线超过50%时。
* 警报定义：会话可以通过一段代码打开，并且永不关闭。 这可能会随着时间推移缓慢发生，并最终导致系统中的内存泄漏。 虽然系统上的会话数应有所波动，但不应持续增加。

运行状况检查

操作仪表板中提供的运行状况 [检查具](/help/sites-administering/operations-dashboard.md#health-reports) 有相应的JMX MBean进行监视。 但是，您可以编写自定义运行状况检查来显示其他系统统计信息。

以下是一些现成运行状况检查，它们有助于监控：

* 系统检查
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：状态不正常时
   * 警报定义：其中一个指标的状态为“警告”或“关键”。 检查日志属性以了解有关问题原因的更多信息。

* 复制队列

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：状态不正常时
   * 警报定义：其中一个指标的状态为“警告”或“关键”。 检查日志属性以了解有关导致此问题的队列的详细信息。

* 响应性能

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 实例：所有服务器
   * 警报持续时间：状态不正常时
   * 警报定义：其中一个度量的状态为“警告”或“关键”状态。 检查日志属性以了解有关导致此问题的队列的详细信息。

* 查询性能

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：状态不正常时
   * 警报定义：一个或多个查询在系统中运行缓慢。 检查日志属性，以了解有关导致此问题的查询的更多信息。

* 活动包

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 实例：所有服务器
   * 警报阈值：状态不正常时
   * 警报定义：系统上存在非活动或未解析的OSGi捆绑包。 有关导致此问题的捆绑包的详细信息，请查看log属性。

* 日志错误

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 实例：所有服务器
   * 警报阈值：状态不正常时
   * 警报定义：日志文件中有错误。 检查日志属性以了解有关问题原因的更多信息。

## 共同问题和决议  {#common-issues-and-resolutions}

在监视过程中，如果遇到问题，您可以执行以下一些疑难解答任务来解决部署中的常见问 [!DNL Experience Manager] 题：

* 如果使用TarMK，请经常运行Tar压缩。 有关详细信息，请参 [阅维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
* 检查 `OutOfMemoryError` 日志。 有关详细信息，请参阅 [分析内存问题](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)。

* 检查日志中是否有对未索引查询、树遍历或索引遍历的引用。 这表示未编制索引的查询或索引不足的查询。 有关优化查询和索引性能的最佳实践，请参 [阅查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。
* 使用工作流控制台验证工作流是否按预期方式执行。 如果可能，将多个工作流浓缩为单个工作流。
* 重新访问实时监控，并寻找任何特定资源的其他瓶颈或高消费者。
* 调查客户端网络的出口点和部署网络(包括调 [!DNL Experience Manager] 度程序)的入口点。 这些往往是瓶颈领域。 有关详细信息，请参阅 [资产网络注意事项](/help/assets/assets-network-considerations.md)。
* 调整服务器 [!DNL Experience Manager] 大小。 您的部署可能规模不 [!DNL Experience Manager] 足。 Adobe客户关怀团队可以帮助您确定您的服务器是否规模不足。
* 检查 `access.log` 和文 `error.log` 件是否在出错时输入项。 查找可能指示自定义代码异常的模式。 将它们添加到您监视的事件列表。
