---
title: 要监控的最佳实践 [!DNL Assets] 部署
description: 监控环境和性能的最佳实践 [!DNL Adobe Experience Manager] 部署后部署。
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# 要监控的最佳实践 [!DNL Adobe Experience Manager Assets] 部署 {#assets-monitoring-best-practices}

从 [!DNL Experience Manager Assets] 从这一点来看，监测应包括观察和报告以下进程和技术：

* 系统CPU
* 系统内存使用
* 系统磁盘IO和IO等待时间
* 系统网络IO
* 栈利用和异步进程（如工作流）的JMX MBean
* OSGi控制台运行状况检查

通常， [!DNL Experience Manager Assets] 监测方式有两种：实时监测和长期监测。

## 实时监控 {#live-monitoring}

您应在开发的性能测试阶段或高负载情况下执行实时监控，以了解环境的性能特征。 通常，应使用一套工具执行实时监控。 以下是一些建议：

* [Visual VM](https://visualvm.github.io/)：可视虚拟机允许您查看详细的Java VM信息，包括CPU使用率、Java内存使用率。 此外，它还允许您对部署上运行的代码进行示例和评估。
* [顶部](https://man7.org/linux/man-pages/man1/top.1.html)：Top是一个Linux命令，它打开一个仪表板，其中显示使用情况统计数据，包括CPU、内存和IO使用情况。 它提供了实例上所发生情况的高级概述。
* [Htop](https://hisham.hm/htop/)：Htop是一种交互式流程查看器。 除了Top可以提供的内容外，它还提供了详细的CPU和内存使用率。 Htop可以使用安装在大多数Linux系统上 `yum install htop` 或 `apt-get install htop`.

* Iotop： Iotop是磁盘IO使用情况的详细仪表板。 它显示一些条形和计量器，这些条形和计量器描述了使用磁盘IO的进程及其使用的数量。 Iotop可以使用安装在大多数Linux系统上 `yum install iotop` 或 `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/)： Iftop显示有关以太网/网络使用的详细信息。 Iftop显示使用以太网的实体的每个通信信道统计数据及其使用的带宽量。 Iftop可以使用安装在大多数Linux系统上 `yum install iftop` 或 `apt-get install iftop`.

* Java Flight Recorder (JFR)：Oracle中的一种商用工具，您可以在非生产环境中自由使用。 有关更多详细信息，请参阅 [如何使用Java Flight Recorder诊断CQ运行时问题](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` 文件：您可以调查 [!DNL Experience Manager] `error.log` 文件以了解系统中记录的错误的详细信息。 使用命令 `tail -F quickstart/logs/error.log` 以找出要调查的错误。
* [工作流控制台](/help/sites-administering/workflows.md)：利用工作流控制台监控滞后或卡住的工作流。

通常，您会使用这些工具来全面了解您的应用程序的 [!DNL Experience Manager] 部署。

>[!NOTE]
>
>这些工具是标准工具，不受Adobe直接支持。 它们不需要额外的许可证。

![chlimage_1-33](assets/chlimage_1-143.png)

*图：使用Visual VM工具进行实时监控。*

![chlimage_1-32](assets/chlimage_1-142.png)

## 长期监测 {#long-term-monitoring}

长期监测 [!DNL Experience Manager] 部署涉及对实时监控的相同部分进行更长时间的监控。 它还包括定义特定于您环境的警报。

### 日志聚合和报告 {#log-aggregation-and-reporting}

有多种工具可用于聚合日志，例如Splunk(TM)和Elastic Search、Logstash和Kabana (ELK)。 要评估贵机构的正常运行时间 [!DNL Experience Manager] 部署时，了解特定于系统的日志事件并根据这些事件创建警报非常重要。 对开发和操作实践的良好了解可以帮助您更好地了解如何调整日志聚合过程以生成关键警报。

### 环境监测 {#environment-monitoring}

环境监控包括监控以下内容：

* 网络吞吐量
* 磁盘IO
* 内存
* CPU利用率
* JMX MBean
* 外部网站

您需要外部工具(如NewRelic(TM)和AppDynamics(TM))来监视每个项目。 使用这些工具，您可以定义特定于您的系统的警报，例如高系统利用率、工作流备份、运行状况检查失败或对您网站的未经身份验证的访问。 Adobe并不推荐使用任何优于其他工具的工具。 找到适合您的工具，并利用它来监控讨论的项目。

#### 内部应用程序监控 {#internal-application-monitoring}

内部应用程序监控包括监控组成应用程序组件的 [!DNL Experience Manager] 栈栈，包括JVM、内容存储库以及通过基于平台构建的自定义应用程序代码进行监控。 通常，它通过JMX Mbeans执行，可由许多流行的监控解决方案直接监控，如SolarWinds (TM)、HP OpenView (TM)、Hyperic (TM)、Zabbix (TM)等。 对于不支持直接连接到JMX的系统，您可以编写shell脚本来提取JMX数据，并以这些系统本地理解的格式将其公开给这些系统。

默认情况下不启用对JMX Mbean的远程访问。 有关通过JMX进行监控的详细信息，请参见 [使用JMX技术进行监控和管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

在许多情况下，需要基线来有效地监视统计信息。 要创建基线，请在正常工作条件下观察系统预定时间段，然后识别正常量度。

**JVM监控**

与任何基于Java的应用程序栈栈一样， [!DNL Experience Manager] 取决于通过底层Java虚拟机向其提供的资源。 您可以通过JVM公开的Platform MXBean监控许多这些资源的状态。 有关MXBean的详细信息，请参见 [使用Platform MBean服务器和Platform MXBean](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

以下是您可以为JVM监视的一些基线参数：

内存

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* 实例：所有服务器
* 警报阈值：当栈或非栈内存利用率超过相应最大内存的75%时。
* 警报定义：可能是系统内存不足，或者代码中存在内存泄漏。 分析线程转储以得出定义。

>[!NOTE]
>
>此Bean提供的信息以字节表示。

线程

* MBean： `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* 实例：所有服务器
* 警报阈值：当线程数大于基线的150%时。
* 警报定义：要么是一个活动的失控过程，要么是低效的操作占用了大量资源。 分析线程转储以得出定义。

**监测[!DNL Experience Manager]**

[!DNL Experience Manager] 还会通过JMX公开一组统计信息和操作。 这些功能有助于评估系统运行状况并在潜在问题影响用户之前发现它们。 有关更多信息，请参阅 [文档](/help/sites-administering/jmx-console.md) 日期 [!DNL Experience Manager] JMX MBean。

以下是一些可以监视的基线参数 [!DNL Experience Manager]：

复制代理

* MBean： `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* 实例：一个创作实例和所有发布实例（用于刷新代理）
* 警报阈值：当 `QueueBlocked` 是 `true` 或的值 `QueueNumEntries` 大于基线的150%。

* 警报定义：系统中存在阻塞的队列，指示复制目标已关闭或无法访问。 通常，网络或基础架构问题会导致过多条目排队，从而对系统性能产生负面影响。

>[!NOTE]
>
>对于MBean和URL参数，请替换 `<AGENT_NAME>` ，其中包含要监视的复制代理的名称。

会话计数器

* MBean： `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL： */system/console/jmx/org.apache.jackrabbit.oak：id=7，name=&quot;OakRepository Statistics&quot;，type*=&quot;RepositoryStats&quot;
* 实例：所有服务器
* 警报阈值：当打开的会话超过基线50%以上时。
* 警报定义：会话可以通过一段代码打开，但永远不会关闭。 随着时间的推移，这种情况可能会慢慢发生，并最终导致系统中的内存泄漏。 虽然会话的数量应在系统中波动，但不应持续增加。

运行状况检查

中可用的运行状况检查 [操作仪表板](/help/sites-administering/operations-dashboard.md#health-reports) 具有相应的JMX MBean用于监视。 但是，您可以编写自定义运行状况检查来公开其他系统统计信息。

以下是一些现成的运行状况检查，这些检查对监控很有帮助：

* 系统检查
   * MBean： `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：其中一个量度的状态为WARN或CRITICAL。 检查日志属性以了解有关问题原因的更多信息。

* 复制队列

   * MBean： `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：其中一个量度的状态为WARN或CRITICAL。 检查日志属性，以了解有关导致问题的队列的更多信息。

* 响应性能

   * MBean： `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * 实例：所有服务器
   * 警报持续时间：当状态不是“正常”时
   * 警报定义：其中一个量度的状态为WARN或CRITICAL。 检查日志属性，以了解有关导致问题的队列的更多信息。

* 查询性能

   * MBean： `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * 实例：一个作者，所有发布服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：一个或多个查询在系统中运行缓慢。 有关导致问题的查询的更多信息，请查看log属性。

* 活动包

   * MBean： `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * 实例：所有服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：系统中存在不活动或未解析的OSGi包。 有关导致问题的捆绑包的更多信息，请检查log属性。

* 日志错误

   * MBean： `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * 实例：所有服务器
   * 警报阈值：当状态不是“正常”时
   * 警报定义：日志文件中有错误。 检查日志属性以了解有关问题原因的更多信息。

## 常见问题和解决方法  {#common-issues-and-resolutions}

在监控过程中，如果您遇到问题，可以执行以下一些故障排除任务来解决的常见问题 [!DNL Experience Manager] 部署：

* 如果使用TarMK，请经常运行Tar压缩。 有关更多详细信息，请参阅 [维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Check `OutOfMemoryError` 日志。 有关更多信息，请参阅 [分析内存问题](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).

* 检查日志中是否包含对未索引查询、树遍历或索引遍历的任何引用。 这些指示未索引的查询或索引不足的查询。 有关优化查询和索引性能的最佳实践，请参阅 [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* 使用工作流控制台验证您的工作流是否按预期执行。 如果可能，请将多个工作流合并到单个工作流中。
* 重新访问实时监控，并查找任何特定资源的其他瓶颈或高占用率。
* 调查从客户端网络的入口点以及入口点到 [!DNL Experience Manager] 部署网络，包括Dispatcher。 这些通常是瓶颈领域。 有关更多信息，请参阅 [Assets网络注意事项](/help/assets/assets-network-considerations.md).
* 放大您的 [!DNL Experience Manager] 服务器。 您的帐户可能不够大， [!DNL Experience Manager] 部署。 Adobe客户支持可以帮助您确定服务器是否过小。
* 检查 `access.log` 和 `error.log` 出错时输入的文件。 查找可能指示自定义代码异常的模式。 将它们添加到您监视的事件列表中。
