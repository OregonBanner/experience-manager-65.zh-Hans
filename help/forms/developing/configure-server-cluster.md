---
title: 如何在JEE服务器群集上配置AEM Forms并执行故障诊断？
description: 了解如何在JEE服务器群集上配置AEM Forms并执行故障诊断
source-git-commit: 8502e0227819372db4120d3995fba51c7401d944
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 0%

---

# 在JEE服务器群集上配置AEM Forms并对其进行故障诊断 {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## 先决知识 {#prerequisites}

熟悉JEE、JBoss、WebSphere和Webogic应用程序服务器、Red Hat Linux、SUSE Linux、Microsoft Windows、IBM AIX或Sun Solaris操作系统、Oracle、IBM DB2或SQL Server数据库服务器和Web环境上的AEM Forms。

## 用户级别 {#user-level}

高级

JEE群集上的AEM Forms是一种拓扑，旨在使JEE上的AEM Forms能够抵御群集节点的故障，并扩展系统容量以超出单个节点的能力。 群集将多个节点合并为一个共享数据的逻辑系统，并允许事务在执行时跨多个节点。 群集是在JEE上扩展AEM Forms的最常见方法，因为可以支持处理任意工作负载组合的任何服务组合。 JEE群集上的AEM Forms不一定最适合所有类型的部署，特别是，非群集服务器负载平衡架构在很多情况下可能非常合适。

本文档旨在讨论您在JEE群集上与AEM Forms之间可能遇到的特定配置要求和潜在问题。

## 群集中有什么？ {#what-is-in-cluster}

JEE群集节点上的AEM Forms相互通信并共享信息，以使群集作为一个整体具有单一一致的配置和应用程序状态。 在群集内共享信息以多种不同方式同时完成，这些方式在不同的环境中使用。 下图说明了基本的信息共享方法：

![应用程序服务器群集](assets/application-server-cluster.jpg)

### 应用程序服务器群集 {#application-server-cluster}

JEE群集上的AEM Forms依赖于底层应用程序服务器的群集功能。 应用程序服务器群集允许将群集配置作为一个整体进行管理，并提供诸如Java命名和目录接口(JNDI)之类的低级群集服务，这些服务允许软件组件在群集中相互查找。 应用服务器依赖于应用程序服务器的群集服务的复杂程度和底层技术依赖关系。 WebSphere和WebLogic具有复杂的群集管理功能，而JBoss则具有非常基本的方法。

### GemFire缓存 {#gemfire-cache}

GemFire缓存是在每个群集节点中实现的分布式缓存机制。 节点之间相互查找并构建单个逻辑缓存，该缓存在节点之间保持一致。 相互查找的节点连接在一起，以维护图1中显示为云的单个名义缓存。 与GDS和数据库不同，缓存是纯粹的概念实体。 实际的缓存内容存储在内存中，并存储在每个群集节点的`LC_TEMP`目录中。

### 数据库 {#database}

JEE上的AEM Forms（通过JDBC数据源IDP_DS、EDC_DS等）数据库被群集的所有节点共享。 关于JEE上AEM Forms状态的大多数永久数据，例如正在进行的事务、与正在进行的事务相关联的用户数据、关于系统设置如何设置的数据等，都位于此数据库中。

### 全局文档存储 {#global-document-storage}

全局文档存储(GDS)是基于文件系统的存储区域，由JEE上的AEM Forms中的文档管理器（IDPDocument类）使用。 GDS存储了群集所有节点必须能够访问的短生命周期和长生命周期文件。

### 其他项目 {#other-items}

除了这些主要共享资源之外，还有其他一些项目具有特定的群集行为，如Quartz。 Quartz是AEM Forms在JEE上使用的调度程序子系统，它使用数据库表来保存其对已调度的内容以及正在运行的计划活动的了解。 对于单节点安装和群集，Quartz必须进行不同的配置，并且它会从JEE设置中的其他AEM Forms中得到提示。

## 常见配置问题 {#common-configuration}

在JEE群集上维护或疑难解答AEM Forms最令人沮丧的一件事是，没有一个位置可以肯定地确认群集是否正常。 为了确认集群中的所有设备都运行良好，需要进行一些调查和分析，并根据集群配置的错误情况，对集群操作存在多种故障模式。 下图说明了一个配置不当的群集，其中多个共享资源被错误地共享。

![配置不正确的群集](assets/bad-configuration-cluster.png)

要记住的一个有趣且重要的事项是，您需要熟悉群集的工作方式以及在群集中查找和验证的内容类型，即使您不打算在群集中的JEE上运行AEM Forms。 这是因为JEE上AEM Forms的某些部分可能会获取他们在群集中操作不正确的提示，并采取您不期待的群集行为。

那么，上图中的共享配置有什么问题？ 以下各节介绍了问题：

### (1)GemFire群集配置 {#gemfire-cluster-configuration}

Gemfire缓存可能会出现一些问题。 两种典型情况是：

* 应该能够相互查找的节点无法这样做。

* 不应被群集的节点相互查找，并在不应该时共享缓存。

如果您有要群集的节点，则必须在网络上相互查找。 默认情况下，它们通过多播UDP消息来执行此操作。 每个节点都发出广播消息，通告其存在，任何接收此类消息的节点都开始与它找到的其他节点通信。 这种自动发现方法非常普遍，许多类型的软件和设备都这样做。

自动发现的一个常见问题是，多播消息可能被网络作为网络策略的一部分或由于软件防火墙规则而过滤，或者可能根本无法通过节点之间存在的网络进行路由。 由于在复杂网络中使UDP自动发现工作通常比较困难，生产部署通常使用替代发现方法：TCP定位器。 有关TCP定位器的一般性讨论，请参见。

**如何知道我使用的是定位器还是UDP?**

以下JVM属性控制GemFire缓存用于查找其他节点的方法。

多播设置：

* `adobe.cache.multicast-port`:用于与分布式系统的其他成员通信的多播端口。如果将此值设置为零，则对于成员发现和分发都禁用多播。

* `gemfire.mcast-address` （可选）：覆盖Gemfire使用的默认IP地址。

TCP定位器设置：

* `adobe.cache.cluster-locators`:TCP定位器和TCP定位器端口的IP地址/主机名，用于系统成员用来与运行的定位器通信的所有定位器。

该列表必须包括当前正在使用的所有定位器，并且必须为群集系统的每个成员都始终如一地配置。

如果TCP定位器列表为空，则不使用定位器，而是使用多播方法。

**如何检查我的TCP定位器是否正在运行？**

首先，如果TCP定位器正在使用，您应将TCP定位器列在所有群集节点上的以下JVM属性中：

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

无需在JEE群集节点上的AEM Forms上运行定位程序，如果需要，可以在与群集分离的其他系统上运行定位程序。 多个系统可以运行定位器，通常最好在两个位置运行定位器，以防定位器单次故障可能导致群集重新启动问题。 在运行定位器的每个系统上，您应该能够在这些计算机上使用以下命令来验证它们是否正在运行：

`netstat -an | grep 22345`

预期响应应为：

`tcp 0 0 *.22345 *.* LISTEN`

另一个验证命令是：

`ps -ef | grep gemfire`

预期响应应如下所示：

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**如何查看GemFire认为群集中包含的节点？**

GemFire会生成日志信息，该信息可用于诊断GemFire缓存发现和采用的群集成员。 这可用于验证是否找到所有正确的群集成员，以及是否没有发生额外的或错误的群集节点发现。 GemFire的日志文件位于JEE临时目录上配置的AEM Forms中：

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

`adobeZZ_`后面的数字字符串对服务器节点是唯一的，因此您必须搜索临时目录的实际内容。 `adobe`后面的两个字符取决于应用程序服务类型：`wl`、`jb`或`ws`。

以下示例日志显示了当两节点群集找到自身时会发生什么情况。

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

在另一个节点AP-HP7上：

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**如果GemFire正在找到它不应该找到的节点，该怎么办？**

共享公司网络的每个不同群集应使用一组单独的TCP定位器（如果使用TCP定位器），或使用多播UDP配置时使用一个单独的UDP端口号。 由于UDP自动发现是JEE上AEM Forms的默认配置，且同一默认端口33456可能被多个群集使用，因此不应尝试通信的群集可能会意外地这样做 — 例如，生产群集和QA群集应保持独立，但可能通过UDP多播彼此连接。

在GemFire群集不正确的网络中，您可能发现重复端口的最常见情况是在群集引导期间。 您可能会发现引导过程失败，但原因不明。 通常，会出现如下错误：

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

在这种情况下，引导程序正在与GemFire合作以访问所需的表，并且通过JDBC访问的表与GemFire返回的缓存表信息之间存在不一致，GemFire来自具有不同基础数据库的不同群集。

虽然在引导期间经常会出现重复端口，但是以后可能会出现这种情况，即当某个群集在启动另一个群集后关闭后重新启动时，或者当网络配置被更改为使先前被隔离的群集（用于多播目的）彼此可见时。

要诊断这些情况，最好查看GemFire日志并仔细考虑是否只找到预期的节点。 要纠正问题，必须更改

`adobe.cache.multicast-port`

属性到一个或两个群集上的不同值。

### 2)GDS共享 {#gds-sharing}

GDS共享在JEE的AEM Forms外部配置，在O/S级别，您必须安排相同的共享目录结构才能用于所有群集节点。 在Windows类型系统上，通常通过设置从一个节点到另一个节点的文件共享或从远程文件系统（如NAS设备）到所有节点的文件共享来完成。 在UNIX系统上， GDS共享通常通过NFS文件共享来完成，这同样是从一个节点到另一个节点，或从NAS设备实现的。

如果此远程文件共享变得不可用或存在细微问题，则群集可能出现故障模式。 远程装载可能因网络问题、安全设置或配置不正确而失败。 系统重新启动可能会导致事先几天或几周所做的配置更改生效，并且这可能会导致意外。

**如果NFS共享无法装载，会发生什么情况？**

在UNIX上，NFS装载映射到目录结构的方式可以使显然可用的GDS目录可用，即使装载失败也是如此。 请考虑：

* NAS服务器：NFS共享文件夹/u01/iapply/livecycle_gds
* 节点1:指向共享文件夹（托管在数据库服务器上）的装载点，位于此处：/u01/iapply/livecycle_gds
* 节点2:指向共享文件夹（托管在数据库服务器上）的装载点，位于此处：/u01/iapply/livecycle_gds

* LCES指定GDS的路径：/u01/iapply/livecycle_gds

如果Node 1上的装载失败，目录结构仍将包含到空装载点的路径/u01/iapply/livecycle_gds ，并且该节点将显示为正确运行。 但是，由于GDS内容实际上并未与其他节点共享，因此群集将无法正常运行。 这可以而且确实发生，结果是群集以神秘的方式失败。

最佳做法是排列事项，以便Linux装载点不用作GDS的根，而是用作GDS根的某些目录：

* 如果您有NFS服务器，则它可能有一个目录：/some/storage/lc_cluster_dev/LC_GDS
* 在您的群集节点上，您有一个装载点：/u01/iapply/shared
* 装载nfs服务器：/some/storage/lc_cluster_dev/u01/iapply/shared
* 将您的GDS指向/u01/iapply/shared/LC_GDS

现在，如果由于某些原因装载未成功，则裸机装载点不包含LC_GDS目录，并且您的群集将可预测地失败，因为它根本找不到任何GDS。

**如何验证所有节点是否都看到相同的GDS并拥有权限？**

通过SSH或telnet到UNIX节点，或通过远程桌面访问Windows系统，以交互式用户身份访问每个节点，最好验证GDS访问和共享。 您应该能够导航到每个节点上配置的GDS目录或文件系统，并从所有其他节点中可见的每个节点创建测试文件。

请注意JEE上AEM Forms运行时所在的用户ID。 在Windows统包安装上，这是本地管理员。 在UNIX上，它可以是在启动脚本或应用程序服务器配置中配置的特定服务用户。 此用户ID必须能够在所有节点上均等地创建和处理GDS文件。

在UNIX系统上，NFS配置通常默认不信任对文件和对象的根所有权或根访问权限。 如果您以根用户身份运行应用程序服务器，则主要会发现您需要在NFS服务器上指定选项、装载文件的节点，或者同时指定两者，以允许对一个节点创建并由另一个节点访问的文件进行双边访问和控制。

### （三）数据库共享 {#database-sharing}

为使群集正常工作，所有群集成员必须共享同一数据库。 大致来说，这个错误的出现范围是：

* 意外地在单独的群集节点上以不同方式设置IDP_DS、EDC_DS、AdobeDefaultSA_DS或其他必需的数据源，以便节点指向不同的数据库。
* 意外地设置了多个不同的节点，以共享不应共享的数据库。

根据您的应用程序服务器，JDBC连接在群集范围中定义可能是自然的，因此不同节点上不能有不同的定义。 但是，在Jboss上完全可以设置事项，以便数据源（如IDP_DS）指向节点1上的一个数据库，但指向节点2上的其他数据库。

相反的问题实际上更为常见，即JEE节点上的多个独立（或群集）AEM Forms意外指向了不打算这样做的同一架构。 当DBA无意中将JEE数据库上的单个AEM Forms的连接信息提供给开发和QA设置团队时，这种情况通常发生，他们中没有一个意识到开发和QA实例需要单独的数据库。

## 应用程序服务器群集 {#application-server-cluster-1}

要在JEE群集上成功实现AEM Forms，必须配置应用程序服务器并将其作为群集正常运行。 在WebSphere和Weblogic中，这是一个简单、记录详实的过程。 在Jboss中，群集配置更易操作，而确保节点配置为充当群集，并且实际上可以相互查找和通信，这可能是一个挑战。 JBoss内部依赖于JGroup，JGroup使用UDP多播来查找并与对等节点协调，而GemFire中提到的一些问题可能会发生，例如节点在应该时无法相互查找，或者在不应该时相互查找。

引用:

* [通过JBoss群集提供高可用性企业服务](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [OracleWebLogic服务器 — 使用群集](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### 如何检查JBoss是否正确聚类？ {#check-jboss-clustering}

当JBoss启动时，当发现群集成员时，有关加入群集的节点的信息级别消息将记录到日志文件/控制台。

如果在运行时通过 — g命令行选项指定了群集名称，您将看到类似以下消息：

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### 石英调度器 {#quartz-scheduler}

在大多数情况下，JEE上的AEM Forms在群集中使用内部Quartz调度程序，通常意在自动遵循JEE上AEM Forms的全局群集配置。 但是，存在一个错误#2794033，当TCP定位器用于Gemfire而不是组播自动发现时，该错误会导致Quartz的自动群集配置失败。 在这种情况下，Quartz将在非群集模式下错误运行。 这将在Quartz表中产生死锁和数据损坏。 8.2.x版的副作用比9.0版更差，因为石英不是太多，但仍然存在。

针对此问题，可进行以下修复：8.2.1.2 QF2.143和9.0.0.2 QF2.44。

还有一个解决方法，即设置以下两个属性：

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

请注意，一个设置使用“cluster”和“locators”之间的句点，而另一个设置使用连字符。 这比应用软件修补程序容易实施，风险也小，但是它涉及人为地创建一个令人困惑的、名称错误的额外配置设置。

### 如何检查Quartz是否作为单个节点或群集运行？ {#check-quartz}

要确定Quartz如何配置自身，您必须查看AEM Forms on JEE调度程序服务在启动期间生成的消息。 这些消息在“信息”严重性下生成，可能需要调整日志级别并重新启动才能获取消息。 在JEE启动序列上的AEM Forms中， Quartz初始化从以下行开始：

信息`[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPShedulerService onLoad
在日志中查找第一行很重要，因为某些应用程序服务器也使用Quartz，并且其Quartz实例不应与AEM Forms在JEE调度程序服务上使用的实例混淆。 这表示调度程序服务正在启动，其后的线路将告诉您它是否在群集模式下正确启动。 此序列中会显示多条消息，这是显示Quartz配置方式的最后一个“已启动”消息：

这里给出了Quartz实例的名称：`IDPSchedulerService_$_ap-hp8.ottperflab.corp.adobe.com1312883903975`。 调度程序的Quartz实例的名称将始终以字符串`IDPSchedulerService_$_`开头。 附加到此末尾的字符串可告知您石英是否在群集模式下运行。 节点的主机名和长位数字符串（此处为`ap-hp8.ottperflab.corp.adobe.com1312883903975`）生成的长唯一标识符表示该节点在群集中运行。 如果它以单个节点的形式运行，则标识符将为两位数“20”：

信息`[org.quartz.core.QuartzScheduler]`调度程序`IDPSchedulerService_$_20`已启动。
必须对所有群集节点单独进行此检查，因为每个节点的调度程序单独确定是否在群集模式下运行。

### 如果Quartz以错误的模式运行，会产生哪些问题？ {#quartz-running-in-wrong-mode}

如果Quartz设置为作为单个节点运行，但实际在群集中运行，并与其他节点共享Quartz数据库表，这将导致AEM Forms在JEE调度程序服务上的不可靠操作，并且通常伴有数据库死锁。 在这种情况下，您可能会看到一个相当典型的堆栈跟踪：

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

为了使集群平稳运行，所有集群节点上的时钟必须紧密同步。 手工操作无法充分完成，必须通过非常定期运行的某种形式的时间同步服务来完成。 所有节点上的时钟必须彼此在一秒内。 最佳做法要求不仅同步群集节点，还同步负载平衡器、数据库服务器、GDS NAS服务器和任何其他组件。

Windows时间同步通常是到域控制器。 UNIX系统可以使用NTP同步到其他时间源。 如果可能，最好是所有系统(包括JEE节点上的AEM Forms和其他系统组件)同步到同一源。

即使在最临时的测试环境中，在节点上手动设置时钟也绝对不够。 手动设置时钟不会提供足够精确的同步，而且两个节点上的时钟不可避免地会彼此相互漂移，即使只在一天的时间内。 主动时间同步机制对于可靠的群集操作至关重要。

### 负载平衡器 {#load-balancer}

提供用户交互式服务的群集的典型要求是HTTP负载平衡器，该负载平衡器将在整个群集中分发HTTP请求。 在JEE群集上成功将负载平衡器与AEM Forms结合使用时，需要配置以下内容：

* 会话粘性

* URL重写规则

* 节点运行状况检查

### 我该如何处理负载平衡器运行状况检查功能？ {#load-balancer-health-check}

可以将某些负载平衡器配置为对负载平衡的节点执行定期运行状况检查。 通常，这是负载平衡器将尝试访问的应用程序函数的URL。 如果负载成功，则假定节点是正常的，并保留在负载平衡集中。 如果URL加载失败，则假定节点存在错误，并从集中删除该节点。 通常，运行状况检查URL只是连接到JEE AdminUI登录页面上的AEM Forms。 对于群集成员来说，这不是理想的运行状况检查，最好实施短期流程，并将REST API URL用作运行状况检查函数。

## 临时文件路径和类似的群集设置 {#temporary-file-path-cluster-settings}

JEE上AEM Forms中的某些文件路径设置在群集范围内建立，并且在每个节点上具有相同的有效设置，但在每个节点上单独解释为引用本地文件。 需要考虑的关键是字体路径设置和临时目录设置。 转到AdminUI核心配置屏幕（主页>设置>核心系统>核心配置）

应选中以下设置：

1. 临时目录的位置
1. Adobe服务器字体目录的位置
1. Customer Fonts目录的位置
1. System Fonts目录的位置
1. 数据服务配置文件的位置

群集中每个配置设置只有一个路径设置。 例如，Temp目录位置可能为`/home/project/QA2/LC_TEMP`。 在群集中，每个节点必须实际具有此特定路径可访问。 如果一个节点具有预期的临时文件路径，而另一个节点没有，则无法正常运行的节点。

虽然这些文件和路径可以在节点之间共享或单独放置，或在远程文件系统上共享，但通常最佳做法是它们是本地节点磁盘存储上的本地副本。

特别是，节点之间不应共享临时目录路径。 应使用类似于所述验证GDS的过程来验证临时目录是否未共享：转到每个节点，在路径设置所指示的路径中创建临时文件，然后验证其他节点是否不共享该文件。 临时目录路径应引用每个节点上的本地磁盘存储（如果可能），并且应当进行检查。

对于每个路径设置，请确保该路径实际存在，并且可从群集中的每个节点访问，并使用JEE上运行AEM Forms的有效使用标识。 字体目录内容必须可读。 临时目录必须允许读取、写入和控制。
















