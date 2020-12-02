---
title: 增强应用程序服务器性能
seo-title: 增强应用程序服务器性能
description: 本文档描述了可配置的可选设置，以改进AEM forms应用程序服务器的性能。
seo-description: 本文档描述了可配置的可选设置，以改进AEM forms应用程序服务器的性能。
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
translation-type: tm+mt
source-git-commit: a26bc4e4ea10370dd2fc3403500004b9e378c418
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---


# 增强应用程序服务器性能{#enhancing-application-server-performance}

本内容介绍了可配置的可选设置，以提高AEM forms应用程序服务器的性能。

## 配置应用程序服务器数据源{#configuring-application-server-data-sources}

AEM forms使用AEM forms存储库作为其数据源。 AEM表单存储库存储应用程序资产，在运行时，服务可以从存储库检索资产，作为完成自动化业务流程的一部分。

对数据源的访问量可能很大，具体取决于您正在运行的AEM表单模块数量和访问应用程序的并发用户数。 数据源访问可以使用连接池进行优化。 *连接* 池是一种技术，用于避免每次应用程序或服务器对象需要访问数据库时建立新数据库连接的开销。连接池通常在基于Web和企业的应用程序中使用，通常由应用程序服务器处理，但不限于。

正确配置连接池参数非常重要，这样连接就永远不会用完，这可能导致应用程序性能恶化。

要正确配置连接池设置，应用程序服务器管理员必须在一天的高峰时间监视连接池。 监控可确保应用程序和用户始终能够使用足够的连接。 大多数应用程序服务器都包含监视工具。

可以使用WebLogic服务器管理控制台监视域中每个JDBC数据源实例的各种统计信息。 有关详细信息，请参阅WebLogic文档。

当应用程序服务器管理员确定正确的连接池设置时，该人员必须将此信息告知数据库管理员。 数据库管理员需要此信息，因为数据库连接数等于数据源连接池中的连接数。 然后，按照下面所述完成为应用程序服务器和数据源类型配置连接池设置的步骤。

### 为Oracle和MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}的WebLogic配置连接池设置

1. 在“域结构”下，单击“服务”>“JDBC”>“数据源”，在右窗格中单击IDP_DS。
1. 在下一个屏幕上，单击“配置”>“连接池”选项卡，并在以下框中输入值：

   * 初始容量
   * 最大容量
   * 容量增量
   * 语句缓存大小

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

### 为SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}的WebLogic配置连接池设置

1. 在“更改中心”下，单击“锁定并编辑”。
1. 在“域结构”下，单击“服务”>“JDBC”>“数据源”，在右窗格中单击“EDC_DS”。
1. 在下一个屏幕上，单击“配置”>“连接池”选项卡，并在以下框中输入值：

   * 初始容量
   * 最大容量
   * 容量增量
   * 语句缓存大小

1. 单击保存，然后单击激活更改。
1. 重新启动WebLogic托管服务器。

### 为DB2 {#configure-connection-pool-settings-for-websphere-for-db2}配置WebSphere的连接池设置

1. 在导航树中，单击“资源”>“JDBC”>“JDBC提供程序”。 在右窗格中，单击您创建的数据源，即DB2通用JDBC驱动程序提供程序或LiveCycle- db2 - IDP_DS。
1. 在“其他属性”下，单击“数据源”，然后选择IDP_DS。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，并在“最大连接数”框和“最小连接数”框中输入值。
1. 单击“确定”或“应用”，然后单击“直接保存到主控配置”。

### 为Oracle{#configure-connection-pool-settings-for-websphere-for-oracle}的WebSphere配置连接池设置

1. 在导航树中，单击“资源”>“JDBC”>“JDBC提供程序”。 在右窗格中，单击您创建的OracleJDBC驱动程序数据源。
1. 在“其他属性”下，单击“数据源”，然后选择IDP_DS。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，并在“最大连接数”框和“最小连接数”框中输入值。
1. 单击“确定”或“应用”，然后单击“直接保存到主控配置”。

### 为SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}的WebSphere配置连接池设置

1. 在导航树中，单击“资源”>“JDBC”>“JDBC提供程序”，在右窗格中单击您创建的用户定义JDBC驱动程序数据源。
1. 在“其他属性”下，单击“数据源”，然后选择IDP_DS。
1. 在下一个屏幕的“其他属性”下，单击“连接池属性”，并在“最大连接数”框和“最小连接数”框中输入值：
1. 单击“确定”或“应用”，然后单击“直接保存到主控配置”。

## 优化内联文档并对JVM内存{#optimizing-inline-documents-and-impact-on-jvm-memory}的影响

如果您通常处理的文档相对较小，则可以提高与文档传输速度和存储空间相关的性能。 为此，请实施以下AEM表单产品配置：

* 增加AEM表单的默认文档最大内联大小，使其大于大多数文档的大小。
* 要处理较大的文件，请指定高速磁盘系统或RAM磁盘上的存储目录。

在管理控制台中配置了最大内联大小和存储目录(AEM forms临时文件目录和GDS目录)。

### 文档大小和最大内联大小{#document-size-and-maximum-inline-size}

当AEM表单发送的用于处理的文档小于或等于默认的文档最大内联大小时，该文档内联存储在服务器上，并将该文档序列化为Adobe文档对象。 在线存储文档可以带来显着的性能优势。 但是，如果您使用表单工作流，则内容也可能存储在数据库中以用于跟踪目的。 因此，增加最大内联大小可能会影响数据库大小。

大于最大内联大小的文档存储在本地文件系统上。 传输到服务器和从服务器传输的Adobe文档对象只是指向该文件的指针。

当文档内容内嵌（即小于最大内嵌大小）时，该内容会作为文档序列化负载的一部分存储在数据库中。 因此，增加最大内联大小会影响数据库大小。

**更改最大内联大小**

1. 在管理控制台中，单击设置>核心系统设置>配置。
1. 在“默认文档最大内联大小”框中输入值，然后单击“确定”。

   >[!NOTE]
   >
   >对于JEE文档上的AEM Forms和OSGi捆绑包上的AEM Forms,JEE环境上的AEM Forms,Max Inline Size属性的值必须相同。 此步骤仅更新了AEM Forms在JEE环境中的价值，而AEM Forms在OSGi捆绑中的价值，包括AEM Forms在JEE环境中的价值。

1. 使用以下系统属性重新启动应用程序服务器：

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >上述系统属性覆盖为JEE环境上的AEM Forms和OSGi捆绑上的AEM Forms设置的文档最大内联大小属性的值，JEE环境上的AEM Forms包括这些系统属性。

>[!NOTE]
>
>默认的最大内联大小为65536字节。

### JVM最大堆大小{#jvm-maximum-heap-size}

增加最大内联大小需要更多内存来存储序列化文档。 因此，它通常还要求增加JVM最大堆大小。

处理多个文档的重载系统可以快速使JVM堆内存饱和。 要避免OutOfMemoryError，请将JVM最大堆大小增加一个与内联文档的大小相对应的数量乘以通常在任何给定时间执行的文档数。

JVM最大堆大小增加=(内联文档大小)x(处理的平均文档数)。

**计算JVM最大堆大小**

在此示例中，当前JVM最大堆设置为512 MB，最大内联大小设置为64 KB。 必须为服务器配置10个作业同时运行，每个作业有9个输入文件和1个结果文件（每个作业总共10个文件，同时处理100个文件）。 所有文件的大小都在512 KB以下。

要内联存储所有文件，请将最大内联大小设置为至少512 KB。

使用以下公式计算JVM最大堆大小所需的增加：

(512 KB)x(100)= 51200 KB，或50 MB

JVM最大堆大小必须增加50 MB，总共需要562 MB。

**考虑堆碎片**

将内联文档的大小设置为大值会增加在容易发生堆碎片的系统上发生OutOfMemoryError的风险。 要在行中存储文档,JVM堆内存必须具有足够的连续空间。 某些操作系统、JVM和垃圾收集算法容易产生堆碎片。 碎片会减少连续堆空间的数量，并且即使存在足够的总可用空间，也可能导致OutOfMemoryError。

例如，应用程序服务器上以前的操作使JVM堆处于碎片状态，垃圾收集器无法充分压缩堆以重新获得大块的可用空间。 即使JVM最大堆大小已调整以增加最大内联大小，也会发生OutOfMemoryError。

要考虑堆碎片，内联文档大小不能设置为高于总堆大小的0.1%。 例如，JVM最大堆大小为512 MB时，最大内联大小可支持512 MB x 0.001 = 0.512 MB，或512 KB。

## WebSphere Application Server增强功能{#websphere-application-server-enhancements}

本节介绍WebSphere应用程序服务器环境的特定设置。

### 增加分配给JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}的最大内存

如果运行Configuration Manager或尝试使用命令行实用程序&#x200B;*ejbdeploy*&#x200B;生成Enterprise JavaBeans(EJB)部署代码，并出现OutOfMemory错误，请增加分配给JVM的内存量。

1. 在&#x200B;*[appserver root]*/deploytool/itp/目录中编辑ejbdeploy脚本：

   * (Windows) `ejbdeploy.bat`
   * （Linux和UNIX）`ejbdeploy.sh`

1. 找到`-Xmx256M`参数并将其更改为更高的值，如`-Xmx1024M`。
1. 保存文件。
1. 运行`ejbdeploy`命令或使用Configuration Manager重新部署。

## 使用LDAP {#improving-windows-server-2003-performance-with-ldap}改善Windows Server 2003性能

此内容描述Microsoft Windows Server 2003操作系统环境的特定设置。

在搜索连接上使用连接池可将所需端口数减少50%。 这是因为该连接始终对给定域使用相同的凭据，并且显式关闭上下文和相关对象。

### 为连接池{#configure-your-windows-server-for-connection-pooling}配置Windows服务器

1. 单击“开始”>“运行”以开始注册表编辑器，并在“打开”框中键入`regedit`并单击“确定”。
1. 转到注册表项`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. 在注册表编辑器的右窗格中，找到TcpTimedWaitDelay值名称。 如果名称未显示，请从菜单栏中选择“编辑”>“新建”>“DWORD值”以添加该名称。
1. 在“名称”框中，键入`TcpTimedWaitDelay`

   >[!NOTE]
   >
   >如果框中未看到闪烁的光标和`New Value #`，请在右侧面板中右键单击，选择“重命名”，在“名称”框中键入&#x200B;`TcpTimedWaitDelay`*。*

1. 对值名称MaxUserPort、MaxHashTableSize和MaxFreeTcbs重复第4步。
1. 多次在右侧窗格中单击以设置TcpTimedWaitDelay值。 在“基”下，选择“小数”，在“值”框中键入`30`。
1. 多次在右窗格中单击以设置MaxUserPort值。 在“基”下，选择“小数”，在“值”框中键入`65534`。
1. 多次在右窗格中单击以设置MaxHashTableSize值。 在“基”下，选择“小数”，在“值”框中键入`65536`。
1. 多次在右窗格中单击以设置MaxFreeTcbs值。 在“基”下，选择“小数”，在“值”框中键入`16000`。

>[!NOTE]
>
>如果使用注册表编辑器或使用其他方法错误地修改了注册表，则可能会出现严重问题。 这些问题可能需要重新安装操作系统。 自行修改注册表。

