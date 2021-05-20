---
title: 提高应用程序服务器性能
seo-title: 提高应用程序服务器性能
description: 本文档介绍了可配置的可选设置，以提高AEM Forms应用程序服务器的性能。
seo-description: 本文档介绍了可配置的可选设置，以提高AEM Forms应用程序服务器的性能。
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---

# 提高应用程序服务器性能{#enhancing-application-server-performance}

本内容介绍了可选设置，您可以配置这些设置来提高AEM Forms应用程序服务器的性能。

## 配置应用程序服务器数据源{#configuring-application-server-data-sources}

AEM Forms使用AEM Forms存储库作为数据源。 AEM表单存储库存储应用程序资产，并且在运行时，服务可以在完成自动化业务流程的过程中从存储库中检索资产。

根据您运行的AEM表单模块数量和访问应用程序的并发用户数，对数据源的访问可能会很重要。 使用连接池可以优化数据源访问。 *连接* 池技术用于避免每次应用程序或服务器对象需要访问数据库时都建立新数据库连接的开销。连接池通常在基于Web的应用程序和企业应用程序中使用，通常由应用程序服务器处理，但不限于。

正确配置连接池参数，以便您永远不会耗尽连接，这可能导致应用程序性能恶化，这一点非常重要。

要正确配置连接池设置，应用程序服务器管理员必须在一天的高峰时间监视连接池。 监控可确保应用程序和用户始终有足够的连接。 大多数应用程序服务器都包含监控工具。

您可以使用WebLogic服务器管理控制台监视域中每个JDBC数据源实例的各种统计信息。 有关详细信息，请参阅WebLogic文档。

当应用程序服务器管理员确定正确的连接池设置时，该人员必须将此信息告知数据库管理员。 数据库管理员需要此信息，因为数据库连接的数量等于数据源的连接池中的连接数量。 然后，按照以下所述，完成配置应用程序服务器和数据源类型的连接池设置的步骤。

### 为WebLogic配置连接池设置以用于Oracle和MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 在“域结构”下，单击“服务”>“JDBC”>“数据源”，然后在右窗格中单击“IDP_DS”。
1. 在下一个屏幕中，单击配置>连接池选项卡，然后在以下框中输入一个值：

   * 初始容量
   * 最大容量
   * 容量增量
   * 语句缓存大小

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

### 为SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}的WebLogic配置连接池设置

1. 在“更改中心”(Change Center)下，单击“锁定并编辑”(Lock &amp; Edit)。
1. 在“域结构”下，单击“服务”>“JDBC”>“数据源”，然后在右窗格中单击“EDC_DS”。
1. 在下一个屏幕中，单击配置>连接池选项卡，然后在以下框中输入一个值：

   * 初始容量
   * 最大容量
   * 容量增量
   * 语句缓存大小

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

### 为DB2 {#configure-connection-pool-settings-for-websphere-for-db2}配置WebSphere的连接池设置

1. 在导航树中，单击“资源”>“JDBC”>“JDBC提供程序”。 在右侧窗格中，单击您创建的数据源(DB2通用JDBC驱动程序提供程序或LiveCycle- db2 - IDP_DS)。
1. 在“其他属性”下，单击数据源，然后选择IDP_DS。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，然后在“最大连接”框和“最小连接”框中输入一个值。
1. 单击确定或应用，然后单击直接保存到主控配置。

### 为Oracle{#configure-connection-pool-settings-for-websphere-for-oracle}配置WebSphere的连接池设置

1. 在导航树中，单击“资源”>“JDBC”>“JDBC提供程序”。 在右窗格中，单击您创建的OracleJDBC驱动程序数据源。
1. 在“其他属性”下，单击数据源，然后选择IDP_DS。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，然后在“最大连接”框和“最小连接”框中输入一个值。
1. 单击确定或应用，然后单击直接保存到主控配置。

### 为SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}配置WebSphere的连接池设置

1. 在导航树中，单击“资源”>“JDBC”>“JDBC提供程序”，然后在右窗格中，单击您创建的“用户定义的JDBC驱动程序”数据源。
1. 在“其他属性”下，单击数据源，然后选择IDP_DS。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，然后在“最大连接数”框和“最小连接数”框中输入一个值：
1. 单击确定或应用，然后单击直接保存到主控配置。

## 优化内联文档并对JVM内存{#optimizing-inline-documents-and-impact-on-jvm-memory}的影响

如果您通常处理的文档大小相对较小，则可以提高与文档传输速度和存储空间相关的性能。 为此，请实施以下AEM Forms产品配置：

* 增加AEM表单的默认文档最大内联大小，使其大于大多数文档的大小。
* 要处理较大的文件，请指定高速磁盘系统或RAM磁盘上的存储目录。

在管理控制台中配置了最大内联大小和存储目录(AEM forms临时文件目录和GDS目录)。

### 文档大小和最大内联大小{#document-size-and-maximum-inline-size}

当由AEM表单发送以供处理的文档小于或等于默认的最大内联大小文档时，该文档将内联存储在服务器上，并且该文档将序列化为Adobe文档对象。 在内联存储文档可以显着提高性能。 但是，如果您使用表单工作流，则出于跟踪目的，内容也可能存储在数据库中。 因此，增加最大内联大小可能会影响数据库大小。

大于最大内联大小的文档存储在本地文件系统上。 传输到服务器和从服务器传输的Adobe文档对象只是指向该文件的指针。

当文档内容内嵌（即小于最大内嵌大小）时，内容将作为文档序列化有效负载的一部分存储在数据库中。 因此，增加最大内联大小可能会影响数据库大小。

**更改最大内联大小**

1. 在管理控制台中，单击设置>核心系统设置>配置。
1. 在“默认文档最大内联大小”框中输入一个值，然后单击“确定”。

   >[!NOTE]
   >
   >对于JEE环境中的AEM Forms和JEE环境中包含的AEM Forms的OSGi包中的AEM Forms，文档最大内联大小属性的值必须相同。 此步骤仅更新了JEE环境中的AEM Forms的值，而不更新了JEE环境中包含的AEM Forms的OSGi包中的AEM Forms的值。

1. 使用以下系统属性重新启动应用程序服务器：

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >上述系统属性覆盖为JEE环境中的AEM Forms和OSGi包中的AEM Forms设置的Document Max Inline Size属性的值。

>[!NOTE]
>
>默认的最大内联大小为65536字节。

### JVM最大堆大小{#jvm-maximum-heap-size}

增加最大内联大小需要更多内存来存储序列化文档。 因此，它通常还要求增加JVM最大堆大小。

处理许多文档的负载较重的系统可快速使JVM堆内存饱和。 为避免OutOfMemoryError，请将JVM最大堆大小乘以与内联文档大小相对应的数量乘以通常在任何给定时间执行的文档数量。

JVM堆大小最大增加=（内联文档大小）x（处理的文档平均数）。

**计算JVM最大堆大小**

在此示例中，当前JVM最大堆设置为512 MB，最大内联大小设置为64 KB。 必须为同时运行10个作业、每个作业有9个输入文件和1个结果文件（每个作业总共有10个文件，同时处理100个文件）的情况配置服务器。 所有文件的大小都在512 KB以下。

要内联存储所有文件，请将内联最大大小设置为至少512 KB。

JVM最大堆大小的所需增加使用以下公式计算：

(512 KB)x(100)= 51200 KB或50 MB

JVM最大堆大小必须增加50 MB，总容量为562 MB。

**考虑堆碎片**

将内联文档的大小设置为较大值会在容易发生堆碎片的系统上引发OutOfMemoryError风险。 要内联存储文档，JVM堆内存必须具有足够的连续空间。 某些操作系统、JVM和垃圾收集算法容易出现堆碎片。 碎片会减少连续堆空间的数量，并且即使存在足够的总可用空间，也会导致OutOfMemoryError。

例如，应用程序服务器上的先前操作使JVM堆处于碎片状态，而垃圾收集器无法充分压缩堆以重新获得大块可用空间。 即使JVM最大堆大小已针对最大内联大小的增加进行了调整，OutOfMemoryError也会发生。

要考虑堆碎片，内联文档大小不得设置为大于堆总大小的0.1%。 例如，JVM堆最大大小为512 MB时，最大内联大小为512 MB x 0.001 = 0.512 MB或512 KB。

## WebSphere应用程序服务器增强功能{#websphere-application-server-enhancements}

本节介绍特定于WebSphere应用程序服务器环境的设置。

### 增加分配给JVM的最大内存{#increasing-the-maximum-memory-allocated-to-the-jvm}

如果运行Configuration Manager或尝试使用命令行实用程序&#x200B;*ejbdeploy*&#x200B;生成企业JavaBeans(EJB)部署代码，并出现OutOfMemory错误，请增加分配给JVM的内存量。

1. 在&#x200B;*[appserver根]*/deploytool/itp/目录中编辑ejbdeploy脚本：

   * (Windows) `ejbdeploy.bat`
   * （Linux和UNIX）`ejbdeploy.sh`

1. 找到`-Xmx256M`参数并将其更改为更高的值，如`-Xmx1024M`。
1. 保存文件。
1. 运行`ejbdeploy`命令或使用配置管理器重新部署。

## 使用LDAP {#improving-windows-server-2003-performance-with-ldap}提高Windows Server 2003性能

本内容介绍特定于Microsoft Windows Server 2003操作系统环境的设置。

在搜索连接上使用连接池可将所需端口数量减少50%。 这是因为该连接始终对给定域使用相同的凭据，并且上下文和相关对象被显式关闭。

### 配置Windows服务器以进行连接池{#configure-your-windows-server-for-connection-pooling}

1. 单击开始>运行以启动注册表编辑器，然后在打开框中键入`regedit`并单击确定。
1. 转到注册表项`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. 在注册表编辑器的右窗格中，找到TcpTimedWaitDelay值名称。 如果名称未显示，请从菜单栏中选择编辑>新建> DWORD值以添加名称。
1. 在“Name（名称）”框中，键入`TcpTimedWaitDelay`

   >[!NOTE]
   >
   >如果框内未看到光标闪烁，且`New Value #`在右侧面板内单击鼠标右键，选择“重命名”，然后在“名称”框中键入&#x200B;`TcpTimedWaitDelay`*。*

1. 对值名称MaxUserPort、MaxHashTableSize和MaxFreeTcbs重复步骤4。
1. 在右窗格中双击以设置TcpTimedWaitDelay值。 在“基本”(Base)下，选择“小数”(Decimal)，然后在“值”(Value)框中，键入`30`。
1. 在右窗格中双击以设置MaxUserPort值。 在“基本”(Base)下，选择“小数”(Decimal)，然后在“值”(Value)框中，键入`65534`。
1. 在右窗格内双击以设置MaxHashTableSize值。 在“基本”(Base)下，选择“小数”(Decimal)，然后在“值”(Value)框中，键入`65536`。
1. 在右窗格中双击以设置MaxFreeTcbs值。 在“基本”(Base)下，选择“小数”(Decimal)，然后在“值”(Value)框中，键入`16000`。

>[!NOTE]
>
>如果使用注册表编辑器或使用其他方法错误地修改注册表，则可能会出现严重问题。 这些问题可能需要重新安装操作系统。 自行修改注册表。
