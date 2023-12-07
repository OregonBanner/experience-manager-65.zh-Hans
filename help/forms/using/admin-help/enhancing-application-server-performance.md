---
title: 增强应用程序服务器性能
description: 本文档介绍了可配置以提高AEM Forms应用程序服务器性能的可选设置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 0%

---

# 增强应用程序服务器性能{#enhancing-application-server-performance}

本内容介绍可配置以提高AEM表单应用程序服务器性能的可选设置。

## 配置应用程序服务器数据源 {#configuring-application-server-data-sources}

AEM forms使用AEM forms存储库作为其数据源。 AEM表单存储库存储应用程序资产，并且在运行时，服务可以在完成自动化业务流程的过程中从存储库中检索资产。

对数据源的访问权限可能会非常大，具体取决于您运行的AEM表单模块数量以及访问应用程序的并发用户数量。 可以使用连接池优化数据源访问。 *连接池* 是一种技术，用于避免每次应用程序或服务器对象需要访问数据库时建立新数据库连接的开销。 连接池通常用于基于Web的应用程序和企业应用程序中，并且通常由应用程序服务器处理（但不限于）。

正确配置连接池参数非常重要，这样您就永远不会用尽连接，这可能会导致应用程序性能下降。

要正确配置连接池设置，应用程序服务器管理员必须在一天中的高峰时段监视连接池。 监控功能可确保应用程序和用户始终有足够的连接可用。 大多数应用程序服务器都包含监控工具。

可以使用WebLogic服务器管理控制台监视域中每个JDBC数据源实例的各种统计信息。 有关详细信息，请参阅WebLogic文档。

当应用程序服务器管理员确定正确的连接池设置时，该人员必须将此信息传达给数据库管理员。 数据库管理员需要此信息，因为数据库连接数等于数据源的连接池中的连接数。 然后，按照如下所述完成为应用程序服务器和数据源类型配置连接池设置的步骤。

### 为WebLogic配置Oracle和MySQL的连接池设置 {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 在“域结构”下，单击“服务”>“JDBC”>“数据源”，然后在右窗格中单击“IDP_DS”。
1. 在下一个屏幕上，单击Configuration > Connection Pool选项卡，然后在以下框中输入一个值：

   * 初始容量
   * 最大容量
   * 容量增量
   * 语句高速缓存大小

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

### 为SQLServer的WebLogic配置连接池设置 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. 在“更改中心”下，单击“锁定和编辑”。
1. 在域结构下，单击服务> JDBC >数据源，然后在右窗格中单击EDC_DS。
1. 在下一个屏幕上，单击Configuration > Connection Pool选项卡，然后在以下框中输入一个值：

   * 初始容量
   * 最大容量
   * 容量增量
   * 语句高速缓存大小

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

### 为WebSphere for DB2配置连接池设置 {#configure-connection-pool-settings-for-websphere-for-db2}

1. 在导航树中，单击资源> JDBC > JDBC提供程序。 在右窗格中，单击您创建的数据源：DB2 Universal JDBC Driver Provider或LiveCycle- db2 - IDP_DS。
1. 在“其他属性”下，单击“数据源”，然后选择“IDP_DS”。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，然后在“最大连接数”框和“最小连接数”框中输入一个值。
1. 单击确定或应用，然后单击直接保存到主配置。

### 为WebSphere配置连接池设置以进行Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. 在导航树中，单击资源> JDBC > JDBC提供程序。 在右窗格中，单击您创建的OracleJDBC驱动程序数据源。
1. 在“其他属性”下，单击“数据源”，然后选择“IDP_DS”。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，然后在“最大连接数”框和“最小连接数”框中输入一个值。
1. 单击确定或应用，然后单击直接保存到主配置。

### 为WebSphere for SqlServer配置连接池设置 {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. 在导航树中，单击“资源”>“JDBC”>“JDBC提供程序”，然后在右窗格中单击您创建的“用户定义的JDBC驱动程序”数据源。
1. 在“其他属性”下，单击“数据源”，然后选择“IDP_DS”。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，然后在“最大连接数”框和“最小连接数”框中输入一个值：
1. 单击确定或应用，然后单击直接保存到主配置。

## 优化内联文档以及对JVM内存的影响 {#optimizing-inline-documents-and-impact-on-jvm-memory}

如果您通常处理相对较小的文档，则可以改善与文档传输速度和存储空间相关的性能。 为此，请实施以下AEM Forms产品配置：

* 增加AEM表单的默认文档最大内联大小，使其大于大多数文档的大小。
* 若要处理较大的文件，请指定位于高速磁盘系统或RAM磁盘上的存储目录。

最大内联大小和存储目录(AEM forms临时文件目录和GDS目录)在管理控制台中进行配置。

### 文档大小和最大内联大小 {#document-size-and-maximum-inline-size}

当由AEM Forms发送以进行处理的文档小于或等于默认文档最大内联大小，该文档将存储在服务器内联上，并且文档被序列化为Adobe文档对象。 内联存储文档可以显着提升性能。 但是，如果您使用的是表单工作流，则内容也可能存储在数据库中以进行跟踪。 因此，增加最大内联大小可能会影响数据库大小。

大于最大内联大小的文档存储在本地文件系统中。 传输到服务器或从服务器传输的Adobe文档对象只是指向该文件的指针。

当文档内容内联（即小于最大内联大小）时，内容将作为文档的序列化有效负载的一部分存储在数据库中。 因此，增加最大内联大小可能会影响数据库大小。

**更改最大内联大小**

1. 在管理控制台中，单击设置>核心系统设置>配置。
1. 在“默认文档最大内联大小”框中输入一个值，然后单击“确定”。

   >[!NOTE]
   >
   >对于JEE环境上的AEM Forms和JEE环境中包含的OSGi包上的AEM Forms，Document Max Inline Size属性的值必须相同AEM Forms 。 此步骤仅更新了JEE环境上的AEM Forms的值，而不更新了JEE环境上的AEM Forms on OSGi捆绑包中包含的AEM Forms的值。

1. 使用以下系统属性重新启动应用程序服务器：

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >上述system属性将覆盖JEE环境上的AEM Forms和JEE环境上的OSGi捆绑包中包含的AEM FormsAEM Forms所设置的Document Max Inline Size属性的值。

>[!NOTE]
>
>默认的最大内联大小为65536字节。

### JVM最大栈大小 {#jvm-maximum-heap-size}

增加最大内联大小需要更多内存来存储序列化文档。 因此，通常还需要增加JVM最大栈大小。

一个处理许多文档的重载系统可快速使JVM栈内存饱和。 要避免OutOfMemoryError，请将JVM最大栈大小增加一个量，该量对应于内联文档的大小乘以通常在任何给定时间执行的文档数。

JVM最大栈大小增加= （内联文档大小）x （处理的文档平均数量）。

**正在计算JVM最大栈大小**

在此示例中，当前JVM最大栈设置为512 MB，最大内联大小为64 KB。 服务器必须针对以下情形进行配置：同时运行10个作业，每个作业包含9个输入文件和1个结果文件（每个作业共有10个文件，同时处理100个文件）。 所有文件的大小都在512 KB以下。

要内联存储所有文件，请将最大内联大小设置为至少512 KB。

使用以下公式计算JVM最大栈大小所需的增加：

(512 KB) x (100) = 51200 KB或50 MB

JVM最大栈大小必须增加50 MB，总大小为562 MB。

**考虑栈碎片**

将内联文档的大小设置为较大的值会增加容易出现栈碎片的系统出现OutOfMemoryError的风险。 要内联存储文档，JVM栈内存必须具有足够的连续空间。 某些操作系统、JVM和垃圾收集算法容易出现栈碎片。 碎片化会减少连续的栈空间量，即使存在足够的总可用空间，也会导致OutOfMemoryError。

例如，先前在应用程序服务器上的操作使JVM栈处于碎片状态，垃圾回收器无法充分压缩栈以重新获得较大的可用空间块。 即使已调整JVM最大栈大小以增加最大内联大小，也可能出现OutOfMemoryError。

要解决栈碎片，内联文档大小不能设置为大于栈总大小的0.1%。 例如，JVM最大栈大小512 MB可以支持最大内联大小512 MB x 0.001 = 0.512 MB或512 KB。

## WebSphere应用程序服务器增强功能 {#websphere-application-server-enhancements}

本节介绍特定于WebSphere应用程序服务器环境的设置。

### 增加分配给JVM的最大内存 {#increasing-the-maximum-memory-allocated-to-the-jvm}

如果正在运行Configuration Manager或尝试使用命令行实用程序生成Enterprise JavaBeans (EJB)部署代码 *ejbdeploy* 出现OutOfMemory错误，请增加分配给JVM的内存量。

1. 在中编辑ejbdeploy脚本 *[appserver根]*/deploytool/itp/目录：

   * (Windows) `ejbdeploy.bat`
   * （Linux和UNIX） `ejbdeploy.sh`

1. 查找 `-Xmx256M` 参数并将其更改为更高的值，例如 `-Xmx1024M`.
1. 保存文件。
1. 运行 `ejbdeploy` 命令或使用Configuration Manager重新部署。

## 使用LDAP提高Windows Server 2003性能 {#improving-windows-server-2003-performance-with-ldap}

本内容介绍特定于Microsoft Windows Server 2003操作系统环境的设置。

在搜索连接上使用连接池最多可将所需的端口数减少50%。 这是因为该连接始终为给定域使用相同的凭据，并且上下文和相关对象被显式关闭。

### 配置Windows Server以进行连接池 {#configure-your-windows-server-for-connection-pooling}

1. 单击开始>运行以启动注册表编辑器，然后在“打开”框中键入 `regedit` 并单击“确定”。
1. 转到注册表项 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. 在注册表编辑器的右侧窗格中，找到TcpTimedWaitDelay值名称。 如果未显示该名称，请从菜单栏中选择“编辑”>“新建”>“DWORD值”以添加该名称。
1. 在“名称”框中，键入 `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >如果您看不到闪烁的光标，并且 `New Value #` 在框中，右键单击右侧面板，选择“重命名”，然后在“名称”框中键入 `TcpTimedWaitDelay`*.*

1. 对值名称MaxUserPort、MaxHashTableSize和MaxFreeTcbs重复步骤4。
1. 双击右窗格以设置TcpTimedWaitDelay值。 在“基本”下，选择“小数”，然后在“值”框中键入 `30`.
1. 在右窗格中双击以设置MaxUserPort值。 在“基本”下，选择“小数”，然后在“值”框中键入 `65534`.
1. 在右窗格中双击以设置MaxHashTableSize值。 在“基本”下，选择“小数”，然后在“值”框中键入 `65536`.
1. 在右窗格中双击以设置MaxFreeTcbs值。 在“基本”下，选择“小数”，然后在“值”框中键入 `16000`.

>[!NOTE]
>
>如果使用注册表编辑器或使用其他方法错误地修改注册表，则可能会出现严重问题。 这些问题可能需要重新安装操作系统。 修改注册表需要自行承担风险。
