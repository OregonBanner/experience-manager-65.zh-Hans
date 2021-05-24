---
title: 如何使用TarMK冷备用运行AEM
seo-title: 如何使用TarMK冷备用运行AEM
description: 了解如何创建、配置和维护TarMK冷备用设置。
seo-description: 了解如何创建、配置和维护TarMK冷备用设置。
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: 配置
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: d9565be9183bd4485036d99869585a79999be54b
workflow-type: tm+mt
source-wordcount: '2719'
ht-degree: 0%

---

# 如何使用TarMK冷备用运行AEM{#how-to-run-aem-with-tarmk-cold-standby}

## 简介 {#introduction}

Tar微内核的冷备用容量允许一个或多个备用AEM实例连接到主实例。 同步过程只意味着它只从主实例到备用实例完成。

备用实例的目的是保证主控存储库的Live Data Copy，并确保在主控因任何原因不可用时快速切换，而不会丢失数据。

内容在主实例和备用实例之间线性同步，而无需进行任何完整性检查文件或存储库损坏。 由于这种设计，备用实例是主实例的精确副本，无法帮助缓解主实例上的不一致问题。

>[!NOTE]
>
>“冷备用”功能用于保护&#x200B;**author**&#x200B;实例上需要高可用性的情况。 如果在使用Tar微内核的&#x200B;**publish**&#x200B;实例上需要高可用性，则Adobe建议使用发布场。
>
>有关更多可用部署的信息，请参阅[推荐部署](/help/sites-deploying/recommended-deploys.md)页面。

## 工作原理{#how-it-works}

在主AEM实例上，打开一个TCP端口，该端口正在侦听传入消息。 目前，奴隶将向主控发送两种类型的消息：

* 请求当前头的分段ID的消息
* 请求具有指定ID的区段数据的消息

备用设备定期请求主设备当前头的段ID。 如果区段在本地未知，则将检索该区段。 如果已存在，则会比较区段，并在必要时也会请求引用的区段。

>[!NOTE]
>
>待机实例无法接收任何类型的请求，因为它们仅在同步模式下运行。 备用实例上唯一可用的部分是Web控制台，以便于进行捆绑和服务配置。

典型的TarMK冷备用部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特征{#other-characteristics}

### 稳健性 {#robustness}

数据流设计用于自动检测和处理连接和网络相关问题。 所有数据包都与校验和捆绑在一起，一旦连接或损坏数据包发生重试机制问题，就会立即触发。

#### 演出 {#performance}

在主实例上启用TarMK冷备用对性能几乎没有可衡量的影响。 额外的CPU消耗非常低，额外的硬盘和网络IO不应产生和性能问题。

在待机状态下，在同步过程中，CPU消耗可能会很高。 由于该过程不是多线程的，因此无法通过使用多个内核来加速。 如果没有数据发生更改或传输，则将没有可衡量的活动。 连接速度将因硬件和网络环境而异，但不取决于存储库的大小或SSL的使用情况。 在估算初始同步所需的时间或在主节点上同时更改了大量数据时，应牢记这一点。

#### 安全 {#security}

假设所有实例都在同一内部网安全区域中运行，则安全违规的风险大大降低。 但是，您可以通过启用从服务器与主控之间的SSL连接来添加额外的安全层。 这样做可以降低中间人对数据造成损害的可能性。

此外，您还可以通过限制传入请求的IP地址来指定允许连接的备用实例。 这应有助于确保内联网中的任何人都无法复制存储库。

>[!NOTE]
>
>建议在调度程序与作为Coldy Standby设置一部分的服务器之间添加负载平衡器。 应将负载平衡器配置为仅将用户流量定向到&#x200B;**primary**&#x200B;实例，以确保一致性，并防止内容通过Cold Standby机制以外的其他方式在备用实例上复制。

## 创建AEM TarMK冷备用设置{#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>与以前的版本相比，AEM 6.3中段节点存储和备用存储服务的PID发生了以下更改：
>
>* 来自org.apache.jackrabbit.oak。**plugins**.segment.standby.store.StandbyStoreService到org.apache.jackrabbit.oak.segment.standby.StandbyStoreService
>* 来自org.apache.jackrabbit.oak。**plugins**.segment.SegmentNodeStoreService到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService

>
>
确保进行必要的配置调整以反映此更改。

要创建TarMK冷备用安装，首先需要通过执行主安装文件夹的整个文件系统副本到新位置来创建备用实例。 然后，您可以使用将指定其角色（`primary`或`standby`）的运行模式来启动每个实例。

以下是创建具有一个主控实例和一个备用实例的设置时需要遵循的过程：

1. 安装AEM。

1. 关闭实例，并将其安装文件夹复制到冷备用实例将从的位置。 即使从不同的计算机运行，也应确保为每个文件夹提供一个描述性名称（如&#x200B;*aem-primary*&#x200B;或&#x200B;*aem-standby*），以区分实例。
1. 转到主实例的安装文件夹，然后：

   1. 检查并删除您可能在`aem-primary/crx-quickstart/install`下拥有的任何以前的OSGi配置

   1. 在`aem-primary/crx-quickstart/install`下创建名为`install.primary`的文件夹

   1. 在`aem-primary/crx-quickstart/install/install.primary`下为首选节点存储和数据存储创建所需的配置
   1. 在同一位置创建名为`org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`的文件，并相应地对其进行配置。 有关配置选项的更多信息，请参阅[配置](/help/sites-deploying/tarmk-cold-standby.md#configuration)。

   1. 如果将AEM TarMK实例与外部数据存储一起使用，请在`aem-primary/crx-quickstart/install`下创建名为`crx3`的文件夹，名称为`crx3`

   1. 将数据存储配置文件放入`crx3`文件夹中。

   例如，如果您正在通过外部文件数据存储运行AEM TarMK实例，则需要以下配置文件：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   下面将找到主实例的示例配置：

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

1. 启动主运行模式，确保指定主运行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 为&#x200B;**org.apache.jackrabbit.oak.segment**&#x200B;包创建新的Apache Sling日志记录记录器。 将日志级别设置为“Debug”，并将其日志输出指向单独的日志文件，如&#x200B;*/logs/tarmk-coldstandby.log*。 有关更多信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。
1. 转到&#x200B;**standby**&#x200B;实例的位置，然后通过运行jar启动该实例。
1. 创建与主日志记录配置相同的日志记录配置。 然后，停止实例。
1. 接下来，准备备用实例。 为此，您可以执行与主实例相同的步骤：

   1. 删除您可能在`aem-standby/crx-quickstart/install`下拥有的任何文件。
   1. 在`aem-standby/crx-quickstart/install`下创建一个名为`install.standby`的新文件夹

   1. 创建两个名为的配置文件：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. 在`aem-standby/crx-quickstart/install`下创建一个名为`crx3`的新文件夹

   1. 创建数据存储配置，并将其放在`aem-standby/crx-quickstart/install/crx3`下。 在本例中，您需要创建的文件是：

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

1. 使用备用运行模式启动&#x200B;**standby**&#x200B;实例：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

该服务也可以通过以下方式通过Web控制台进行配置：

1. 转到Web控制台：*https://serveraddress:serverport/system/console/configMgr*
1. 正在查找名为&#x200B;**Apache Jackrabbit Oak Segment Tar Cold Standby Service**&#x200B;的服务，并双击该服务以编辑设置。
1. 保存设置并重新启动实例，以便新设置生效。

>[!NOTE]
>
>您可以随时检查实例的角色，方法是在Sling设置Web控制台中检查存在&#x200B;**primary**&#x200B;或&#x200B;**standby**&#x200B;运行模式。
>
>可以通过转到&#x200B;*https://localhost:4502/system/console/status-slingsettings*&#x200B;并检查&#x200B;**&quot;Run Modes&quot;**&#x200B;行来完成此操作。

## 首次同步{#first-time-synchronization}

准备完成并首次启动备用后，当备用赶上主备用时，实例之间将会有大量网络流量。 您可以查阅日志来观察同步的状态。

在备用&#x200B;*tarmk-coldstandby.log*&#x200B;中，您将看到如下条目：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

在备用的&#x200B;*error.log*&#x200B;中，您应会看到如下条目：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述日志代码片段中， *10.20.30.40*&#x200B;是主代码的IP地址。

在&#x200B;**primary** *tarmk-coldstandby.log*&#x200B;中，您将看到如下条目：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在这种情况下，日志中提到的“client”是&#x200B;**standby**&#x200B;实例。

在这些条目停止在日志中显示后，您可以安全地假定同步过程已完成。

虽然上述条目显示轮询机制运行正常，但在发生轮询时了解是否有任何数据正在同步通常非常有用。 为此，请查找如下条目：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，当使用非共享`FileDataStore`运行时，如下消息将确认正确传输二进制文件：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 配置 {#configuration}

以下OSGi设置可用于冷备用服务：

* **保留配置：** 如果启用，则会将配置存储在存储库中，而不是传统的OSGi配置文件中。建议在生产系统上禁用此设置，以便备用系统不会拉取主配置。

* **模式(`mode`):** 这将选择实例的运行模式。

* **端口（端口）：** 用于通信的端口。默认为 `8023`.

* **主主机(`primary.host`):**  — 主实例的主机。此设置仅适用于备用设备。
* **同步间隔(`interval`):**  — 此设置确定同步请求之间的间隔，并且仅适用于备用实例。

* **允许的IP范围(`primary.allowed-client-ip-ranges`):**  — 主要允许从中进行连接的IP范围。
* **安全(`secure`):** 启用SSL加密。要使用此设置，必须在所有实例上启用此设置。
* **备用读取超时(`standby.readtimeout`):** 从备用实例发出的请求超时（以毫秒为单位）。使用的默认值为60000（一分钟）。

* **备用自动清理(`standby.autoclean`):** 如果存储的大小在同步周期中增加，则调用清理方法。

>[!NOTE]
>
>强烈建议主存储库ID和备用存储库ID不同，以便它们对于卸载等服务可单独不可识别。
>
>确保覆盖此内容的最佳方法是删除备用文件上的&#x200B;*sling.id*&#x200B;文件并重新启动实例。

## 故障转移过程{#failover-procedures}

如果主实例因任何原因失败，您可以设置其中一个备用实例，通过更改启动运行模式来承担主实例的角色，如下所述：

>[!NOTE]
>
>还需要修改配置文件，以便它们与主实例使用的设置匹配。

1. 转到安装备用实例的位置，然后停止该实例。

1. 如果已使用设置配置了负载平衡器，则可以在此时从负载平衡器的配置中删除主。
1. 从备用安装文件夹备份`crx-quickstart`文件夹。 在设置新待机时，可以将其用作起点。

1. 使用`primary`运行模式重新启动实例：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 向负载平衡器中添加新的主。
1. 创建并启动新的备用实例。 有关更多信息，请参阅上面创建AEM TarMK冷备用设置](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)中的过程。[

## 对冷备用设置{#applying-hotfixes-to-a-cold-standby-setup}应用修补程序

将修补程序应用到冷备用安装程序的推荐方法是：将它们安装到主实例，然后将其克隆到新的冷备用实例，并安装修补程序。

您可以按照以下步骤操作：

1. 通过转到JMX控制台并使用**org.apache.jackrabbit.oak来停止冷备用实例上的同步过程：状态（“备用”）**bean。 有关如何执行此操作的更多信息，请参阅[Monitoring](#monitoring)上的部分。
1. 停止冷备用实例。
1. 在主实例上安装修补程序。 有关如何安装修补程序的更多详细信息，请参阅[如何使用包](/help/sites-administering/package-manager.md)。
1. 在安装后测试实例以了解问题。
1. 通过删除其安装文件夹来删除冷备用实例。
1. 停止主实例并克隆该实例，方法是将其整个安装文件夹的文件系统副本复制到冷备用位置。
1. 重新配置新创建的克隆以充当冷备用实例。 有关更多详细信息，请参阅[创建AEM TarMK冷备用设置。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 启动主实例和冷备用实例。

## 监测 {#monitoring}

该功能使用JMX或MBean公开信息。 这样，您可以使用[JMX控制台](/help/sites-administering/jmx-console.md)检查备用和主控的当前状态。 该信息可在名为`Status`的`type org.apache.jackrabbit.oak:type="Standby"`的MBean中找到。

**备用**

观察备用实例时，您将公开一个节点。 ID通常是通用UUID。

此节点具有五个只读属性：

* `Running:` 布尔值，指示同步进程是否正在运行。

* `Mode:` 客户：后跟用于标识实例的UUID。请注意，每次更新配置时，此UUID都会发生更改。

* `Status:` 当前状态的文本表示形式( `running` 如 `stopped`或)。

* `FailedRequests:`连续错误的数量。
* `SecondsSinceLastSuccess:` 自上次与服务器成功通信后经过的秒数。如果未成功进行通信，则将显示`-1`。

还有三种可调用的方法：

* `start():` 启动同步过程。
* `stop():` 停止同步过程。
* `cleanup():` 在待机上运行清理操作。

**主要**

观察主设备会通过ID值为TarMK备用服务所使用的端口号的MBean公开一些常规信息（默认为8023）。 大多数方法和属性与备用方法相同，但有些方法和属性不同：

* `Mode:` 将始终显示值 `primary`。

此外，可检索与主控连接的多达10个客户端（备用实例）的信息。 MBean ID是实例的UUID。 这些MBean没有可调用的方法，但有一些非常有用的只读属性：

* `Name:` 客户端的ID。
* `LastSeenTimestamp:` 文本表示形式中最后一个请求的时间戳。
* `LastRequest:` 客户端的最后一个请求。
* `RemoteAddress:` 客户端的IP地址。
* `RemotePort:` 客户端用于最后一个请求的端口。
* `TransferredSegments:` 传输到此客户端的区段总数。
* `TransferredSegmentBytes:`传输到此客户端的总字节数。

## 冷备用存储库维护{#cold-standby-repository-maintenance}

### 修订版清理 {#revision-clean}

>[!NOTE]
>
>如果在主实例上运行[联机修订版清理](/help/sites-deploying/revision-cleanup.md)，则不需要执行下面介绍的手动过程。 此外，如果您使用联机修订版清理，则将自动对备用实例执行`cleanup ()`操作。

>[!NOTE]
>
>请勿在备用系统上运行脱机修订版清理。 不需要它，也不会减小segmentstore大小。

Adobe建议定期运行维护，以防止存储库随时间的推移而过度增长。 要手动执行冷备用存储库维护，请执行以下步骤：

1. 通过转到JMX控制台并使用&#x200B;**org.apache.jackrabbit.oak ，停止备用实例上的备用进程：状态(&quot;Standby&quot;)** bean。 有关如何执行此操作的更多信息，请参阅上述[Monitoring](/help/sites-deploying/tarmk-cold-standby.md#monitoring)部分。

1. 停止主AEM实例。
1. 在主实例上运行oak压缩工具。 有关更多详细信息，请参阅[维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)。
1. 启动主实例。
1. 使用第一步中所述的相同JMX Bean在备用实例上启动备用进程。
1. 观看日志并等待同步完成。 此时，备用存储库可能会大幅增长。
1. 使用第一步中所述的相同JMX Bean，在备用实例上运行`cleanup()`操作。

备用实例完成与主实例的同步可能比通常花费的时间长，因为离线压缩会有效地重写存储库历史记录，从而使计算存储库中的更改需要更长时间。 还应指出，此过程完成后，备用存储库的大小将与主存储库上的存储库的大小大致相同。

作为替代方法，在主存储库上运行压缩后，可以手动将主存储库复制到备用存储库，实际上每次压缩运行时都会重建备用存储库。

### 数据存储垃圾收集 {#data-store-garbage-collection}

对文件数据存储实例不时运行垃圾收集很重要，否则，已删除的二进制文件将保留在文件系统上，最终填满驱动器。 要运行垃圾收集，请按照以下步骤操作：

1. 按照上面](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance)部分[中所述，运行冷备用存储库维护。
1. 在维护过程完成且实例重新启动后：

   * 在主服务器上，通过相关的JMX Bean运行数据存储垃圾收集，如[本文](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console)中所述。
   * 在待机状态下，数据存储垃圾收集只能通过&#x200B;**BlobGarbageCollection** MBean - `startBlobGC()`进行。 备用时**RepositoryManagement **MBean不可用。

   >[!NOTE]
   >
   >如果您未使用共享数据存储，则垃圾收集首先必须在主存储器上运行，然后在备用存储器上运行。
