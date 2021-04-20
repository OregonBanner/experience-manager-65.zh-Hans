---
title: 如何使用TarMK冷备用运行AEM
seo-title: 如何使用TarMK冷备用运行AEM
description: 了解如何创建、配置和维护TarMK Cold Standby设置。
seo-description: 了解如何创建、配置和维护TarMK Cold Standby设置。
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2732'
ht-degree: 0%

---


# 如何使用TarMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}运行AEM

## 简介 {#introduction}

Tar Micro Kernel的冷备用容量允许一个或多个备用AEM实例连接到主实例。 同步过程只是一种方式，即它只从主实例到备用实例完成。

备用实例的目的是保证主控存储库的Live Data Copy，并确保在主控因任何原因不可用时快速切换，而不丢失数据。

内容在主实例和备用实例之间线性同步，无需对文件或存储库损坏进行任何完整性检查。 由于这种设计，备用实例是主实例的精确副本，无法帮助减轻主实例的不一致。

>[!NOTE]
>
>“冷备用”功能用于保护&#x200B;**author**&#x200B;实例上需要高可用性的场景。 对于使用Tar微内核的&#x200B;**publish**&#x200B;实例需要高可用性的情况，Adobe建议使用发布场。
>
>有关更多可用部署的信息，请参阅[推荐的部署](/help/sites-deploying/recommended-deploys.md)页。

## 工作原理{#how-it-works}

在主AEM实例上，将打开一个TCP端口并侦听传入消息。 目前，奴隶将向主控发送两种类型的消息：

* 请求当前头段ID的消息
* 请求具有指定ID的区段数据的消息

备用设备定期请求主设备当前头的段ID。 如果区段在本地未知，则将检索该区段。 如果已经存在，则会比较区段，并会根据需要请求引用的区段。

>[!NOTE]
>
>待机实例不会接收任何类型的请求，因为它们以仅同步模式运行。 备用实例上唯一可用的部分是Web控制台，以便于捆绑和服务配置。

典型的TarMK冷备用部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特征{#other-characteristics}

### 稳健性{#robustness}

数据流设计用于自动检测和处理连接和网络相关问题。 所有数据包都与校验和捆绑在一起，一旦连接或损坏数据包发生问题，将触发重试机制。

#### 演出 {#performance}

在主实例上启用TarMK冷备用对性能几乎没有可衡量的影响。 额外的CPU消耗非常低，额外的硬盘和网络IO不应产生和性能问题。

在待机状态下，您会期望在同步过程中有较高的CPU消耗。 由于该过程不是多线程的，因此无法通过使用多个内核来加速它。 如果没有更改或传输任何数据，则不会有可衡量的活动。 连接速度将因硬件和网络环境而异，但不取决于存储库的大小或SSL使用情况。 在估计初始同步所需的时间或在主节点上同时更改了大量数据时，应牢记这一点。

#### 安全 {#security}

假设所有实例都运行在同一内部网安全区域中，则安全漏洞的风险将大大降低。 但是，您可以通过启用从服务器和主控之间的SSL连接来添加额外的安全层。 这样做会降低数据被中间人破坏的可能性。

此外，您还可以通过限制传入请求的IP地址来指定允许连接的备用实例。 这应有助于确保内部网中的任何人都无法复制存储库。

>[!NOTE]
>
>建议在调度程序和作为Coldy Standby设置一部分的服务器之间添加负载平衡器。 应将负载平衡器配置为仅将用户流量引导到&#x200B;**primary**&#x200B;实例，以确保一致性，并防止通过除Cold Standby机制之外的其他方式在备用实例上复制内容。

## 创建AEM TarMK Cold Standby设置{#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>在AEM 6.3中，段节点存储和备用存储服务的PID与先前版本相比发生了更改，如下所示：
>
>* 来自org.apache.jackrabbit.oak。**plugins**.segment.standby.store.StandbyStoreService到org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* 来自org.apache.jackrabbit.oak。**plugins**.segment.SegmentNodeStoreService到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService

>
>
请确保进行必要的配置调整以反映此更改。

要创建TarMK冷备用安装，您首先需要通过执行主安装文件夹的整个安装文件夹到新位置的文件系统副本来创建备用实例。 然后，您可以使用将指定其角色（`primary`或`standby`）的运行模式开始每个实例。

下面是创建具有一个主控实例和一个备用实例的设置时需要遵循的过程：

1. 安装AEM。

1. 关闭实例，并将其安装文件夹复制到冷备用实例的运行位置。 即使从不同的计算机运行，也要确保为每个文件夹提供一个描述性名称（如&#x200B;*aem-primary*&#x200B;或&#x200B;*aem-standby*）以区分不同的实例。
1. 转到主实例的安装文件夹，并：

   1. 检查并删除您可能在`aem-primary/crx-quickstart/install`下拥有的任何以前的OSGi配置

   1. 在`aem-primary/crx-quickstart/install`下创建名为`install.primary`的文件夹

   1. 在`aem-primary/crx-quickstart/install/install.primary`下为首选节点存储和数据存储创建所需的配置
   1. 在同一位置创建名为`org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`的文件，并相应配置它。 有关配置选项的详细信息，请参阅[Configuration](/help/sites-deploying/tarmk-cold-standby.md#configuration)。

   1. 如果将AEM TarMK实例与外部数据存储一起使用，请在`aem-primary/crx-quickstart/install`下创建一个名为`crx3`的文件夹，该文件夹名为`crx3`

   1. 将数据存储配置文件放在`crx3`文件夹中。

   例如，如果您正在与外部文件数据存储一起运行AEM TarMK实例，则需要以下配置文件：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   在下面，您将找到主实例的示例配置：

   **示** **例oforg.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config的示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config的示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 开始主模式，确保指定主运行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 为&#x200B;**org.apache.jackrabbit.oak.segment**&#x200B;包创建新的Apache Sling日志记录记录器。 将日志级别设置为“调试”，并将其日志输出指向单独的日志文件，如&#x200B;*/logs/tarmk-coldstandby.log*。 有关详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。
1. 转到&#x200B;**standby**&#x200B;实例的位置，并通过运行jar开始它。
1. 创建与主日志记录配置相同的日志记录配置。 然后，停止实例。
1. 接下来，准备备用实例。 通过执行与主实例相同的步骤，可以执行以下操作：

   1. 删除您可能位于`aem-standby/crx-quickstart/install`下的任何文件。
   1. 在`aem-standby/crx-quickstart/install`下新建一个名为`install.standby`的文件夹

   1. 创建两个配置文件，名为：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. 在`aem-standby/crx-quickstart/install`下新建一个名为`crx3`的文件夹

   1. 创建数据存储配置并将其放置在`aem-standby/crx-quickstart/install/crx3`下。 在此示例中，您需要创建的文件是：

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. 编辑文件并创建必要的配置。

   以下是典型备用实例的示例配置文件：

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config的示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config的示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config的示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 使用备用运行模式开始&#x200B;**standby**&#x200B;实例：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

此服务也可以通过以下方式通过Web控制台进行配置：

1. 转至Web控制台：*https://serveraddress:serverport/system/console/configMgr*
1. 正在查找名为&#x200B;**Apache Jackrabbit Oak Segment Tar Cold Standby Service**&#x200B;的服务，多次单击它以编辑设置。
1. 保存设置并重新启动实例，以便新设置生效。

>[!NOTE]
>
>您可以随时检查实例的角色，方法是检查Sling设置Web控制台中是否存在&#x200B;**primary**&#x200B;或&#x200B;**standby**&#x200B;运行模式。
>
>这可以通过转到&#x200B;*https://localhost:4502/system/console/status-slingsettings*&#x200B;并检查&#x200B;**&quot;Run Modes&quot;**&#x200B;行来完成。

## 首次同步{#first-time-synchronization}

在准备完成并首次启动备用后，当备用接近主备时，实例之间将会有大量网络流量。 您可以参考日志来观察同步的状态。

在备用&#x200B;*tarmk-coldstandby.log*&#x200B;中，您将看到以下条目：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

在备用的&#x200B;*error.log*&#x200B;中，应当看到如下条目：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述日志片段中，*10.20.30.40*&#x200B;是主IP地址。

在&#x200B;**primary** *tarmk-coldstandby.log*&#x200B;中，您将看到以下条目：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在这种情况下，日志中提到的“客户端”是&#x200B;**standby**&#x200B;实例。

在这些条目停止显示在日志中后，您可以安全地假定同步过程已完成。

尽管上述条目显示轮询机制正常工作，但通常有必要了解在轮询发生时是否同步了任何数据。 要执行此操作，请查找如下条目：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，当使用非共享`FileDataStore`运行时，如下消息将确认二进制文件正在正确传输：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 配置 {#configuration}

Cold Standby服务提供以下OSGi设置：

* **持久配置：** 如果启用，则会将配置存储在存储库中，而不是传统的OSGi配置文件中。建议在生产系统上禁用此设置，以便备用系统不会拉取主配置。

* **模式(`mode`)：这** 将选择实例的运行模式。

* **端口（端口）：** 用于通信的端口。默认为 `8023`.

* **主主机(`primary.host`):**  — 主实例的主机。此设置仅适用于备用设备。
* **同步间隔(`interval`):**  — 此设置确定同步请求之间的间隔，并且仅适用于备用实例。

* **允许的IP范围(`primary.allowed-client-ip-ranges`):**  — 主要允许连接的IP范围。
* **安全(`secure`)：启** 用SSL加密。要利用此设置，必须在所有实例中启用它。
* **待机读取超时(`standby.readtimeout`)：从** 待机实例发出的请求超时（以毫秒为单位）。建议的超时设置为43200000。 通常建议您将超时值设置为至少12小时。

* **备用自动清`standby.autoclean`理():** 如果存储的大小在同步周期上增加，请调用清除方法。

>[!NOTE]
>
>强烈建议主和备用系统具有不同的存储库ID，以便它们对于卸载等服务可单独区分。
>
>确保覆盖此问题的最佳方法是删除待机设备上的&#x200B;*sling.id*&#x200B;文件，然后重新启动实例。

## 故障转移过程{#failover-procedures}

如果主实例因任何原因失败，您可以通过更改开始运行模式来设置其中一个备用实例以充当主实例的角色，具体如下所述：

>[!NOTE]
>
>还需要修改配置文件，使其与用于主实例的设置相匹配。

1. 转到安装备用实例的位置，然后停止它。

1. 如果您已使用安装程序配置了负载平衡器，则此时可以从负载平衡器的配置中删除主要。
1. 从备用安装文件夹备份`crx-quickstart`文件夹。 在设置新待机时，可以将其用作起点。

1. 使用`primary`运行模式重新启动实例：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 向负载平衡器添加新的主要。
1. 创建并开始新的备用实例。 有关详细信息，请参阅上面的“创建AEM TarMK冷备用设置](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)”中的过程。[

## 将修补程序应用到冷备用设置{#applying-hotfixes-to-a-cold-standby-setup}

将修补程序应用到冷实例设置的建议方法是将它们安装到主实例，然后将其克隆到安装了修补程序的新冷备用实例中。

您可以按照以下步骤操作：

1. 转到JMX控制台并使用**org.apache.jackrabbit.oak停止冷备用实例上的同步过程：状态（“待机”）**bean。 有关如何执行此操作的详细信息，请参阅[监视](#monitoring)一节。
1. 停止冷备用实例。
1. 在主实例上安装修补程序。 有关如何安装修补程序的详细信息，请参阅[如何使用程序包](/help/sites-administering/package-manager.md)。
1. 在安装后测试实例中是否存在问题。
1. 通过删除冷备用实例的安装文件夹来删除它。
1. 停止主实例并克隆它，方法是将其整个安装文件夹的文件系统副本复制到冷备用位置。
1. 重新配置新创建的克隆以充当冷备用实例。 有关其他详细信息，请参阅[创建AEM TarMK冷备用设置。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 开始主实例和冷备用实例。

## 监测 {#monitoring}

该功能使用JMX或MBean公开信息。 这样，您就可以使用[JMX控制台](/help/sites-administering/jmx-console.md)检查备用和主控的当前状态。 可以在名为`Status`的`type org.apache.jackrabbit.oak:type="Standby"`的MBean中找到该信息。

**待机**

观察待机实例时，您将公开一个节点。 ID通常是通用UUID。

此节点有五个只读属性：

* `Running:` 布尔值，指示同步进程是否正在运行。

* `Mode:` 客户端：后跟用于标识实例的UUID。请注意，每次更新配置时，此UUID都会更改。

* `Status:` 当前状态（如或）的文 `running` 本表 `stopped`示。

* `FailedRequests:`连续错误的数量。
* `SecondsSinceLastSuccess:` 自上次成功与服务器通信以来的秒数。如果未成功通信，则显示`-1`。

还有三种可调用的方法：

* `start():` 开始同步过程。
* `stop():` 停止同步过程。
* `cleanup():` 在待机设备上运行清理操作。

**主要**

观察主要信息会通过MBean公开一些一般信息，其ID值为TarMK备用服务使用的端口号（默认为8023）。 大多数方法和属性与待机方法和属性相同，但有些方法和属性不同：

* `Mode:` 将始终显示值 `primary`

此外，可检索与主控连接的多达10个客户机（备用实例）的信息。 MBean ID是实例的UUID。 这些MBean没有可调用的方法，但有一些非常有用的只读属性：

* `Name:` 客户端的ID。
* `LastSeenTimestamp:` 文本表示形式中最后一个请求的时间戳。
* `LastRequest:` 客户端的最后一个请求。
* `RemoteAddress:` 客户端的IP地址。
* `RemotePort:` 客户端用于上次请求的端口。
* `TransferredSegments:` 转让给此客户端的区段总数。
* `TransferredSegmentBytes:`传输到此客户端的字节总数。

## 冷备用存储库维护{#cold-standby-repository-maintenance}

### 修订版清理 {#revision-clean}

>[!NOTE]
>
>如果在主实例上运行[联机修订清理](/help/sites-deploying/revision-cleanup.md)，则不需要下面介绍的手动过程。 此外，如果您使用“联机修订清理”，则将自动对备用实例执行`cleanup ()`操作。

>[!NOTE]
>
>不要在备用系统上运行脱机修订清理。 它不需要，也不会减小分段存储的大小。

Adobe建议定期运行维护，以防止随着时间的推移存储库出现过度增长。 要手动执行冷备用存储库维护，请执行以下步骤：

1. 转到JMX控制台并使用&#x200B;**org.apache.jackrabbit.oak停止备用实例上的备用进程：状态（“待机”）** bean。 有关如何执行此操作的详细信息，请参阅上面关于[Monitoring](/help/sites-deploying/tarmk-cold-standby.md#monitoring)的一节。

1. 停止主AEM实例。
1. 在主实例上运行橡木压实工具。 有关详细信息，请参阅[维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
1. 开始主实例。
1. 开始备用实例上的备用进程，使用第一步中所述的相同JMX bean。
1. 观看日志并等待同步完成。 此时，备用储存库可能会大幅增长。
1. 使用第一步中所述的相同JMX bean对备用实例运行`cleanup()`操作。

备用实例完成与主同步的脱机压缩可能比通常需要更长的时间，这会有效地重写存储库历史记录，从而使计算存储库中的更改花费更多时间。 还应指出，此过程完成后，备用存储库的大小将与主存储库的大小大致相同。

作为替代方法，在主存储库上运行压缩后，可以手动将主存储库复制到备用存储库，实际上是在每次压缩运行时重建备用存储库。

### 数据存储垃圾收集 {#data-store-garbage-collection}

在文件数据存储实例上不时运行垃圾收集很重要，否则，已删除的二进制文件将保留在文件系统中，最终填满驱动器。 要运行垃圾回收，请按照以下步骤操作：

1. 按照以上](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance)部分[所述运行冷备用存储库维护。
1. 在维护过程完成并重新启动实例之后：

   * 在主卷上，通过相关的JMX bean运行数据存储垃圾收集，如本文[](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)中所述。
   * 在待机状态下，数据存储垃圾收集只能通过&#x200B;**BlobGarbageCollection** MBean - `startBlobGC()`使用。 **RepositoryManagement **MBean在待机状态下不可用。

   >[!NOTE]
   >
   >如果您未使用共享数据存储，垃圾收集首先必须在主数据库上运行，然后在备用数据库上运行。

