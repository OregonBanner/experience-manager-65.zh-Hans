---
title: 如何在JEE服务器群集中配置AEM Forms并进行故障排除？
description: 了解如何在JEE服务器群集中配置AEM Forms并对其进行故障排除
exl-id: 230fc2f1-e6e5-4622-9950-dae9449ed3f6
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '4032'
ht-degree: 0%

---

# 在JEE服务器群集中配置AEM Forms并对其进行故障排除 {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 必备知识 {#prerequisites}

熟悉JEE、JBoss、WebSphere和Webogic应用程序服务器、Red Hat Linux、SUSE Linux、Microsoft Windows、IBM AIX或Sun Solaris操作系统、Oracle、IBM DB2或SQL Server数据库服务器以及Web环境上的AEM Forms。

## 用户级别 {#user-level}

高级

JEE群集上的AEM Forms是一种拓扑，旨在使JEE上的AEM Forms能够抵御群集节点的故障，并扩展超出单个节点能力的系统容量。 群集将多个节点合并到一个逻辑系统中，该逻辑系统共享数据，并允许事务在执行中跨越多个节点。 集群是在JEE上扩展AEM Forms的最常见方式，因为可以支持处理任何工作负载组合的任何服务组合。 JEE群集上的AEM Forms不一定最适合所有类型的部署，特别是在许多情况下，非群集服务器负载平衡体系结构可能更合适。

本文档旨在讨论在JEE集群上使用AEM Forms时可能遇到的具体配置要求和潜在问题领域。

## 聚类中有什么？ {#what-is-in-cluster}

JEE群集节点上的AEM Forms相互通信并共享信息，以使整个群集具有单个一致的配置和应用程序状态。 集群内的信息共享是以多种不同的方式同时完成的，这些方式在不同的上下文中使用。 基本的信息共享方法如下图所示：

![应用程序服务器群集](assets/application-server-cluster.jpg)

### 应用程序服务器群集 {#application-server-cluster}

JEE群集上的AEM Forms依赖于底层应用程序服务器的群集功能。 应用程序服务器群集使群集配置能够作为一个整体进行管理，并提供低级别的群集服务(如Java命名和目录接口(JNDI))，使软件组件能够在群集内相互查找。 群集服务的复杂性和应用程序服务器所依赖的底层技术依赖性依赖于应用程序服务器。 WebSphere和WebLogic具有完善的群集管理功能，而JBoss具有非常基本的方法。

### GemFire缓存 {#gemfire-cache}

GemFire缓存是在每个群集节点中实现的分布式缓存机制。 节点之间相互查找并建立单个逻辑缓存，使节点之间保持一致性。 发现彼此的节点会连接在一起，以维护图1中显示为云的单个概念性缓存。 与GDS和数据库不同，缓存是一个纯概念实体。 实际缓存的内容存储在内存和 `LC_TEMP` 每个群集节点上的目录。

### 数据库 {#database}

JEE上的AEM Forms数据库（通过JDBC数据源IDP_DS、EDC_DS和其他数据源访问）由群集中的所有节点共享。 有关AEM Forms on JEE状态的大多数持久性数据（例如正在进行的交易、与正在进行的交易关联的用户数据、有关如何设置系统设置的数据等）都位于此数据库中。

### 全局文档存储 {#global-document-storage}

Global Document Storage (GDS)是AEM Forms on JEE中Document Manager （IDPDocument类）使用的基于文件系统的存储区域。 GDS存储了所有群集节点都必须可访问的短期和长期文件。

### 其他项目 {#other-items}

除了这些主要的共享资源之外，还有具有特定群集行为的其他项目，例如Quartz。 Quartz是AEM Forms在JEE上使用的一个调度程序子系统，它使用数据库表来保存有关已调度的内容和正在运行的已调度活动的知识。 对于单节点安装和群集，Quartz必须采用不同的配置，并且它在JEE设置上从其他AEM Forms获得提示。

## 常见配置问题 {#common-configuration}

维护JEE群集上的AEM Forms或对其进行故障排除最令人沮丧的事情之一是，没有单一位置可以积极确认群集运行正常。 为了确认群集中的一切正常，进行了一些调查和分析，根据群集配置出了什么问题，群集操作存在几种故障模式。 下图说明了一个配置错误的群集，其中多个共享资源被错误地共享。

![配置错误的群集](assets/bad-configuration-cluster.png)

要记住一件有趣而重要的事情，即您需要熟悉集群的工作方式以及要在集群中查找和验证的内容类型，即使您不打算在集群中的JEE上运行AEM Forms也是如此。 这是因为JEE上AEM Forms的某些部分可能会根据它们的提示，在集群中错误地操作，并出现您不期望的集群行为。

那么，上图中的共享配置有什么问题呢？ 以下各节描述了问题：

### (1) GemFire群集配置 {#gemfire-cluster-configuration}

Gemfire缓存可能会出现一些问题。 两种典型情况是：

* 本应能够相互查找的节点无法执行此操作。

* 不应加入集群的节点会相互查找并在不应加入集群时共享缓存。

如果您有要群集的节点，它们必须在网络上找到彼此。 默认情况下，它们通过多播UDP消息实现此目的。 每个节点发送广播消息通告其存在，并且任何接收此类消息的节点开始与其找到的其他节点通信。 这种自动发现的方法非常普遍，许多类型的软件和设备都这样做。

自动发现的一个常见问题是，多播消息可能作为网络策略的一部分或者由于软件防火墙规则而被网络过滤，或者可能只是不能通过存在于节点之间的网络进行路由。 由于让UDP自动发现在复杂网络中工作的一般困难，生产部署通常使用替代发现方法：TCP定位器。 有关TCP定位器的一般讨论可在参考资料中找到。

**如何知道我使用的是定位器还是UDP？**

以下JVM属性控制GemFire缓存用于查找其他节点的方法。

多播设置：

* `adobe.cache.multicast-port`：用于与分布式系统的其他成员进行通信的多播端口。 如果将此值设置为零，则对成员发现和分发都禁用多播。

* `gemfire.mcast-address` （可选）：覆盖Gemfire使用的默认IP地址。

TCP定位器设置：

* `adobe.cache.cluster-locators`：系统成员用于与正在运行的定位器通信的所有定位器的TCP定位器和TCP定位器端口的IP地址/主机名。

该列表必须包含当前正在使用的所有定位器，并且必须为群集系统的每个成员一致地配置。

如果TCP定位器列表为空，则不使用定位器，而是使用多播方法。

**如何检查我的TCP定位器是否正在运行？**

首先，如果正在使用TCP定位器，则在所有群集节点上的以下JVM属性中应列出您的TCP定位器：

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

无需在JEE群集节点上的AEM Forms上运行定位器，如果需要，它们可以在独立于群集的其他系统上运行。 多个系统可以运行定位器，通常认为最佳实践是将定位器运行在两个位置，而单个定位器故障可能会导致群集重启问题。 在每个运行定位器的系统上，您应该能够使用下列命令来验证它们是否正在运行：

`netstat -an | grep 22345`

预期的响应应为：

`tcp 0 0 *.22345 *.* LISTEN`

另一个验证命令是：

`ps -ef | grep gemfire`

预期的响应应如下所示：

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**如何查看GemFire认为群集中有哪些节点？**

GemFire生成日志记录信息，这些信息可用于诊断GemFire缓存已找到并采用的群集成员。 这可用于验证是否找到了所有正确的群集成员，以及是否未发现额外或不正确的群集节点。 GemFire的日志文件位于配置的AEM Forms on JEE临时目录中：

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

之后的数字字符串 `adobeZZ_` 对于服务器节点是唯一的，因此您必须搜索临时目录的实际内容。 后面的两个字符 `adobe` 取决于应用程序服务器类型： `wl`， `jb`，或 `ws`.

以下示例日志显示了当双节点群集发现自身时会发生什么情况。

在第一个节点AP-HP8上：

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

在另一节点上，AP-HP7：

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**如果GemFire找到不应找到的节点，该怎么办？**

共享公司网络的每个不同的群集应使用单独的TCP位置集（如果使用TCP位置），或使用单独的UDP端口号（如果使用多播UDP配置）。 由于UDP自动发现是JEE上AEM Forms的默认配置，并且多个群集可能正在使用相同的默认端口33456，因此，不应尝试通信的群集可能会意外地这样做 — 例如，生产群集和QA群集应保持独立，但可通过UDP多播相互连接。

在GemFire不正确群集的网络中发现重复端口时，最常见的情况是在群集的引导过程中。 您可能会发现，引导过程失败的原因不明确。 通常，会看到以下错误：

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

在这种情况下，引导程序将与GemFire一起访问所需的表，并且通过JDBC访问的表与GemFire返回的缓存表信息之间存在不一致，缓存表信息来自具有不同基础数据库的不同集群。

虽然在引导过程中经常会明显出现重复端口，但这种情况有可能在稍后出现，例如，当某个群集在关闭后重新启动时，发生另一个群集的引导时，或者当网络配置更改为使之前为多播目的而隔离的群集彼此可见时。

要诊断这些情况，最好查看GemFire日志，并仔细考虑是否仅找到预期的节点。 要更正此问题，必须更改

`adobe.cache.multicast-port`

属性到不同值的一个或两个群集。

### 2) GDS共享 {#gds-sharing}

GDS共享是在JEE本身的AEM Forms之外的O/S级别配置的，在该级别上，您必须安排相同的共享目录结构可供所有群集节点使用。 在Windows类型系统上，这通常是通过设置文件共享来实现的，从一个节点到另一个节点，或从远程文件系统（如NAS设备）到所有节点。 在UNIX系统上， GDS共享通常通过NFS文件共享来完成，同样也可以从一个节点到另一个节点，或通过NAS应用装置实现。

群集的故障模式可能是此远程文件共享变得不可用或有细微的问题。 由于网络问题、安全设置或不正确的配置，远程装载可能会失败。 系统重新启动可能会导致在数天或数周前进行的配置更改生效，这可能会导致意外情况。

**如果NFS共享无法装载，会发生什么情况？**

在UNIX上，NFS装载映射到目录结构的方式可允许明显可用的GDS目录可用，即使装载失败也是如此。 请考虑：

* NAS服务器： NFS共享文件夹/u01/iapply/livecycle_gds
* 节点1：指向共享文件夹（托管在数据库服务器上）的装入点，该文件夹位于此处： /u01/iapply/livecycle_gds
* 节点2：指向共享文件夹（托管在数据库服务器上）的装入点，该文件夹位于以下位置：/u01/iapply/livecycle_gds

* LCES指定GDS的路径： /u01/iapply/livecycle_gds

如果节点1上的装载失败，则目录结构仍将包含到空装载点的路径/u01/iapply/livecycle_gds ，并且节点看起来可以正常运行。 但是，由于GDS内容实际上并未与其他节点共享，因此群集将无法正常运行。 这种情况可能也会发生，而且确实会发生，结果是群集以神秘的方式失败。

最佳做法是安排一些操作，以便不使用Linux挂载点作为GDS的根，而是使用其中某个目录作为GDS根：

* 如果您有NFS服务器，则它可能有目录：/some/storage/lc_cluster_dev/LC_GDS
* 在群集节点上，有一个挂载点： /u01/iapply/shared
* 挂载nfs_server： /some/storage/lc_cluster_dev/u01/iapply/shared
* 将GDS指向/u01/iapply/shared/LC_GDS

现在，如果由于某种原因装载不成功，裸装载点将不包含LC_GDS目录，并且您的群集将按预期失败，因为它根本找不到任何GDS。

**如何验证所有节点是否都看到相同的GDS并具有权限？**

验证GDS访问和共享的最佳方式是作为交互式用户访问每个节点，或者通过SSH或telnet访问UNIX节点，或者通过远程桌面访问Windows系统。 您应该能够导航到每个节点上配置的GDS目录或文件系统，并从所有其他节点中可见的每个节点创建测试文件。

注意AEM Forms on JEE中运行的用户ID。 在Windows统包安装中，此用户是本地管理员。 在UNIX上，它可能是启动脚本或应用程序服务器配置中配置的特定服务用户。 此用户ID必须能够在所有节点上平等地创建和处理GDS文件。

在UNIX系统上， NFS配置通常默认为不信任对文件和对象的根所有权或根访问权限。 如果您以root用户身份运行应用程序服务器，则主要发现您需要在NFS服务器上指定选项，指定装载文件的节点，或者指定这两个选项，以允许对一个节点创建的并由另一个节点访问的文件进行双边访问和控制。

### (3)数据库共享 {#database-sharing}

为使群集正常工作，所有群集成员必须共享同一数据库。 出现这种错误的范围大致是：

* 意外地在单独的群集节点上以不同的方式设置IDP_DS、EDC_DS、AdobeDefaultSA_DS或其他所需的数据源，以便这些节点指向不同的数据库。
* 意外设置了多个单独的节点来共享一个数据库，而这些节点不应共享。

根据您的应用程序服务器，在群集作用域中定义JDBC连接是很自然的事，因此在不同的节点上不可能有不同的定义。 但是，在Jboss上，完全可以设置一些内容，以便数据源（如IDP_DS）指向节点1上的一个数据库，而指向节点2上的其他数据库。

实际上，反向问题更常见，也就是说，JEE节点上的多个独立（或群集）AEM Forms意外指向同一架构，而它们并非故意指向该架构。 这种情况通常发生在DBA无意中向开发和QA设置团队提供单个AEM Forms on JEE数据库的连接信息时，这些设置团队都没有意识到DEV和QA实例需要单独的数据库。

## 应用程序服务器群集 {#application-server-cluster-1}

要在JEE群集上成功AEM Forms，必须配置应用程序服务器并将其作为群集正确运行。 在WebSphere和Weblogic中，这是一个简单明了且有充分说明的流程。 在Jboss中，群集配置需要更多的操作，而确保将节点配置为充当群集，并且实际上可以相互查找和通信，可能是一项挑战。 JBoss在内部依赖于JGroups，后者使用UDP多播来查找对等节点并与之协调，而GemFire中提到的一些问题可能会发生，例如节点在应该查找时无法相互查找，或者在不应该查找时相互查找。

引用:

* [通过JBoss群集提供高可用性企业服务](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [oracleWebLogic Server — 使用群集](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### 如何检查JBoss是否正确聚类？ {#check-jboss-clustering}

当JBoss启动时，在发现群集成员时，有关加入群集的节点的INFO级别消息将记录到日志文件/控制台。

如果在运行时通过 — g命令行选项指定了群集名称，您将看到与以下内容类似的消息：

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Quartz计划程序 {#quartz-scheduler}

在大多数情况下，AEM Forms on JEE在集群中使用内部Quartz调度程序是为了在一般情况下自动遵循AEM Forms on JEE的全局集群配置。 但是，存在一个错误#2794033，如果将TCP定位器用于Gemfire而不是多播自动发现，则会导致Quartz的自动群集配置失败。 在这种情况下，Quartz将错误地以非群集模式运行。 这将在Quartz表中产生死锁和数据损坏。 8.2.x版比9.0版的副作用更严重，因为石英用量较少，但仍存在。

此问题的修复如下所示：8.2.1.2 QF2.143和9.0.0.2 QF2.44。

还有一个解决方法，即设置这两个属性：

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

请注意，一个设置使用“cluster”和“locators”之间的句点，而另一个设置使用连字符。 与应用软件补丁相比，它易于实施，风险也较低，但需要人为地创建其他令人困惑的错误命名配置设置。

### 如何检查Quartz是否作为单个节点或群集运行？ {#check-quartz}

要确定Quartz如何配置自身，必须查看AEM Forms on JEE计划程序服务在启动期间生成的消息。 这些消息以INFO严重性生成，可能需要调整日志级别并重新启动以获取消息。 在AEM Forms on JEE启动序列中，Quartz初始化从以下行开始：

信息  `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPchedulerService onLoad在日志中定位第一行很重要，因为某些应用程序服务器也使用Quartz，并且其Quartz实例不应与AEM Forms on JEE Scheduler服务所使用的实例混淆。 这是调度程序服务正在启动的指示，其后面的行将告诉您调度程序服务是否以群集模式正确启动。 此序列中会显示多条消息，这是显示如何配置Quartz的最后一条“已启动”消息：

此处给出Quartz实例的名称： `IDPSchedulerService_$_ap-hp8.ottperflab.adobe.com1312883903975`. 调度程序的Quartz实例的名称将始终以字符串开头 `IDPSchedulerService_$_`. 附加到此末尾的字符串可告知您Quartz是否以群集模式运行。 从节点的主机名和长字符串数字生成的长唯一标识符，此处 `ap-hp8.ottperflab.adobe.com1312883903975`，表示它正在群集中运行。 如果它作为单个节点运行，则标识符将是一个两位数“20”：

信息  `[org.quartz.core.QuartzScheduler]` 调度程序 `IDPSchedulerService_$_20` 已启动。
此检查必须单独在所有群集节点上完成，因为每个节点的调度程序都独立决定是否以群集模式运行。

### 如果Quartz在错误模式下运行，会产生什么样的问题？ {#quartz-running-in-wrong-mode}

如果将Quartz设置为作为单个节点运行，但实际上它在群集中运行并与其他节点共享Quartz数据库表，这将导致AEM Forms在JEE计划程序服务上的运行不可靠，并且通常会伴有数据库死锁。 这是相当典型的栈栈跟踪，在此情况下您可能会看到这种跟踪：

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Couldn't remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### 如何同步群集中的系统时钟？ {#ynchronize-system-clocks-cluster}

为了使群集能够顺利运行，必须使所有群集节点上的时钟紧密同步。 这不能靠人工来完成，必须由定期运行的某种形式的时间同步服务来完成。 所有节点上的时钟必须位于彼此的一秒内。 最佳实践不仅要求群集节点，还要求负载平衡器、数据库服务器、 GDS NAS服务器以及任何其他组件都同步。

Windows时间同步倾向于到域控制器。 UNIX系统可以使用NTP同步到不同的时间源。 如果可能，最好将所有系统(包括JEE节点上的AEM Forms和其他系统组件)同步到同一源。

即使是在最临时性的测试环境中，手动设置节点上的时钟也绝对不够。 手动设置时钟无法提供足够的精确同步，两个节点上的时钟不可避免地会相互漂移，即使在一天的时间段内也是如此。 主动的时间同步机制是机群可靠运行的关键。

### 负载平衡器 {#load-balancer}

提供用户交互服务的群集的典型要求是将跨群集分发HTTP请求的HTTP负载平衡器。 在JEE群集上成功将负载平衡器与AEM Forms结合使用时，需要配置以下内容：

* 会话粘性

* URL重写规则

* 节点运行状况检查

### 我应如何执行负载平衡器运行状况检查功能？ {#load-balancer-health-check}

某些负载平衡器可以配置为对要负载平衡的节点执行定期运行状况检查。 通常，这是负载平衡器将尝试访问的应用程序函数的URL。 如果加载成功，则假定节点处于健康状态，并将其保留在负载平衡集中。 如果URL加载失败，则假定该节点有故障，并从集合中删除。 通常，运行状况检查URL只连接到JEE AdminUI登录页面上的AEM Forms 。 这不是群集成员的理想运行状况检查，最好实施一个短期进程，并使用REST API URL作为运行状况检查功能。

## 临时文件路径和类似的群集设置 {#temporary-file-path-cluster-settings}

JEE上的AEM Forms中的某些文件路径设置在群集范围内建立，并在每个节点上具有相同的有效设置，但在每个节点上单独进行解释以引用本地文件。 要考虑的关键因素是字体路径设置和临时目录设置。 转到AdminUI核心配置屏幕（主页>设置>核心系统>核心配置）

应检查以下设置：

1. 临时目录的位置
1. Adobe服务器字体目录的位置
1. Customer Fonts目录的位置
1. System Fonts目录的位置
1. 数据服务配置文件的位置

群集中的每一个配置设置只有一个路径。 例如，您的Temp目录位置可能是 `/home/project/QA2/LC_TEMP`. 在群集中，每个节点都必须能够实际访问此特定路径。 如果一个节点具有预期的临时文件路径，而另一个节点没有该路径，则无法正常运行的节点。

虽然这些文件和路径可以在节点之间共享、单独放置或在远程文件系统上共享，但通常最佳做法是将这些文件和路径作为本地节点磁盘存储上的本地副本。

特别是，不应在节点之间共享临时目录路径。 应使用与验证GDS的过程类似的过程来验证临时目录是否未共享：转到每个节点，在路径设置指示的路径中创建临时文件，然后验证其他节点是否未共享该文件。 临时目录路径应该引用每个节点上的本地磁盘存储（如果可能），并且应该检查。

对于每个路径设置，请确保该路径确实存在，并且可以使用AEM Forms on JEE运行时所使用的有效使用身份从群集中的每个节点访问。 字体目录内容必须是可读的。 临时目录必须允许读取、写入和控制。
