---
title: 如何在TarMK冷备用模式下运行AEM
seo-title: How to Run AEM with TarMK Cold Standby
description: 了解如何创建、配置和维护TarMK冷备用设置。
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 0%

---

# 如何在TarMK冷备用模式下运行AEM{#how-to-run-aem-with-tarmk-cold-standby}

## 简介 {#introduction}

Tar微内核的冷备用容量允许一个或多个备用AEM实例连接到主实例。 同步过程只是单向的，这意味着同步过程只能从主实例到备用实例完成。

备用实例的目的是保证主控存储库的实时数据副本，并确保在主控由于任何原因不可用时快速切换数据而不会丢失。

内容在主实例和备用实例之间线性同步，无需对文件或存储库损坏进行任何完整性检查。 由于此设计，备用实例是主实例的精确副本，不能帮助缓解主实例上的不一致。

>[!NOTE]
>
>冷备用功能旨在保护以下情况下需要高可用性的环境： **作者** 实例。 对于在上需要高可用性的情况 **发布** 在使用Tar微内核的实例中，Adobe建议使用发布场。
>
>有关更多可用部署的信息，请参阅 [建议的部署](/help/sites-deploying/recommended-deploys.md) 页面。

>[!NOTE]
>
>设置备用实例或从主节点派生备用实例时，它仅允许访问以下控制台（用于管理相关活动）：
>
>* OSGI Web控制台
>
>无法访问其他控制台。

## 工作原理 {#how-it-works}

在主AEM实例上， TCP端口已打开并正在侦听传入消息。 目前，奴隶将向主控发送两种类型的消息：

* 请求当前标头的段ID的消息
* 请求具有指定ID的区段数据的消息

待机周期性地请求主设备的当前头的段ID。 如果该区段在本地未知，则将检索它。 如果数据段已存在，则会比较数据段，并根据需要请求引用的数据段。

>[!NOTE]
>
>备用实例未收到任何类型的请求，因为它们以仅同步模式运行。 备用实例上唯一可用的部分是Web控制台，以便于配置捆绑包和服务。

典型的TarMK冷备用部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特征 {#other-characteristics}

### 稳健性 {#robustness}

数据流被设计为自动检测并处理连接和网络相关问题。 所有数据包都绑定了校验和，一旦连接出现问题或损坏的数据包触发重试机制。

#### 演出 {#performance}

在主实例上启用TarMK冷备用对性能几乎没有可衡量的影响。 额外的CPU消耗非常低，额外的硬盘和网络IO应该不会产生和性能问题。

在待机状态下，您可以在同步过程中预期高的CPU消耗。 由于该过程不是多线程的，因此无法通过使用多个内核来加速该过程。 如果未更改或传输任何数据，则不会有可衡量的活动。 连接速度会因硬件和网络环境而异，但并不取决于存储库的大小或SSL的使用。 在估计初始同步所需的时间或在主节点上同时更改了大量数据时，您应该记住这一点。

#### 安全性 {#security}

假定所有实例都运行在同一个内联网安全区域中，安全漏洞的风险将大大降低。 但是，您可以通过启用从进程和主控进程之间的SSL连接来添加额外的安全层。 这样做可降低数据被中间人破坏的可能性。

此外，您还可以通过限制传入请求的IP地址来指定允许连接的备用实例。 这应该有助于确保内部网中的任何人都不能复制存储库。

>[!NOTE]
>
>建议在Dispatcher和冷备用设置中的服务器之间添加负载平衡器。 负载平衡器应配置为仅将用户流量定向到 **主要** 实例来确保一致性，并防止通过冷备用机制以外的方式在备用实例上复制内容。

## 创建AEM TarMK冷备用设置 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>与先前版本相比，AEM 6.3中区段节点存储和备用存储服务的PID发生了更改，如下所示：
>
>* 从org.apache.jackrabbit.oak.**插件**.segment.standby.store.StandbyStoreService到org.apache.jackrabbit.oak.segment.standby.standby.store.StandbyStoreService
>* 从org.apache.jackrabbit.oak.**插件**.segment.SegmentNodeStoreService到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>确保进行必要的配置调整以反映此更改。

要创建TarMK冷备用设置，您首先需要通过将主服务器的整个安装文件夹的文件系统复制到新位置来创建备用实例。 然后，您可以使用运行模式启动每个实例，该运行模式将指定其角色( `primary` 或 `standby`)。

以下是创建一个主控和一个备用实例的设置时需要遵循的过程：

1. 安装AEM。

1. 关闭实例，并将其安装文件夹复制到冷备用实例运行所在的位置。 即使从不同的计算机运行，请确保为每个文件夹提供一个描述性名称(例如 *aem-primary* 或 *aem-standby*)以区分实例。
1. 转到主实例的安装文件夹并：

   1. 检查并删除下可能存在的任何先前OSGi配置 `aem-primary/crx-quickstart/install`

   1. 创建名为的文件夹 `install.primary` 下 `aem-primary/crx-quickstart/install`

   1. 为下的首选节点存储和数据存储创建所需的配置 `aem-primary/crx-quickstart/install/install.primary`
   1. 创建一个名为的文件 `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` 并相应地对其进行配置。 有关配置选项的详细信息，请参阅 [配置](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. 如果您正在将AEM TarMK实例与外部数据存储一起使用，请创建一个名为的文件夹 `crx3` 下 `aem-primary/crx-quickstart/install` 已命名 `crx3`

   1. 将数据存储配置文件放入 `crx3` 文件夹。

   例如，如果您运行的是具有外部文件数据存储的AEM TarMK实例，则需要以下配置文件：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   在下方，您将找到主实例的示例配置：

   **示例** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 启动主运行模式，确保指定主运行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 为创建新的Apache Sling日志记录器 **org.apache.jackrabbit.oak.segment** 包。 将日志级别设置为“Debug”，并将其日志输出指向单独的日志文件，如 */logs/tarmk-coldstandby.log*. 有关更多信息，请参阅 [日志记录](/help/sites-deploying/configure-logging.md).
1. 转到 **待机** 实例并通过运行jar启动它。
1. 创建与主数据库相同的日志记录配置。 然后，停止实例。
1. 接下来，准备备用实例。 为此，您可以执行与对主实例相同的步骤：

   1. 删除下可能有的任何文件 `aem-standby/crx-quickstart/install`.
   1. 创建一个名为的新文件夹 `install.standby` 下 `aem-standby/crx-quickstart/install`

   1. 创建两个名为的配置文件：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. 创建一个名为的新文件夹 `crx3` 下 `aem-standby/crx-quickstart/install`

   1. 创建数据存储配置并将其放在 `aem-standby/crx-quickstart/install/crx3`. 对于此示例，您需要创建的文件是：

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. 编辑文件并创建必要的配置。

   以下是典型备用实例的示例配置文件：

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config示例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 启动 **待机** 实例（通过使用备用运行模式）：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

也可以通过Web控制台通过以下方式配置该服务：

1. 转到位于以下位置的Web控制台： *https://serveraddress:serverport/system/console/configMgr*
1. 正在查找名为的服务 **Apache Jackrabbit Oak Segment Tar冷备用服务** 并双击以编辑设置。
1. 保存设置，然后重新启动实例，以使新设置生效。

>[!NOTE]
>
>您可以随时通过检查是否存在 **主要** 或 **待机** Sling设置Web控制台中的运行模式。
>
>这可以通过转到 *https://localhost:4502/system/console/status-slingsettings* 并检查 **“运行模式”** 行。

## 首次同步 {#first-time-synchronization}

完成准备并首次启动待机后，当待机状态恢复到主状态时，实例之间将出现大量网络流量。 您可以查阅日志以观察同步的状态。

待机 *tarmk-coldstandby.log*，您将看到如下条目：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

待命时间 *error.log*，您应会看到如下所示的条目：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述日志片段中， *10.20.30.40* 是主节点的IP地址。

在 **主要** *tarmk-coldstandby.log*，您将看到如下条目：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在这种情况下，日志中提到的“客户端”是 **待机** 实例。

一旦这些条目停止显示在日志中，就可以安全地假定同步过程已完成。

虽然上述条目表明轮询机制运行正常，但了解是否在轮询时同步任何数据通常很有用。 为此，请查找以下条目：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，使用非共享运行时 `FileDataStore`，如下消息将确认正确传输了二进制文件：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 配置 {#configuration}

冷备用服务有以下OSGi设置可用：

* **保留配置：** 如果启用，这会将配置存储在存储库中，而不是传统的OSGi配置文件中。 建议在生产系统上保持禁用此设置，以便主配置不会被待机提取。

* **模式(`mode`)：** 这将选择实例的运行模式。

* **端口（端口）：** 用于通信的端口。 默认为 `8023`。

* **主主机(`primary.host`)：**  — 主实例的主机。 此设置仅适用于待机。
* **同步间隔(`interval`)：**  — 此设置确定同步请求之间的间隔，并且仅适用于备用实例。

* **允许的IP范围(`primary.allowed-client-ip-ranges`)：**  — 主服务器将允许来自该IP范围的连接的IP范围。
* **安全(`secure`)：** 启用SSL加密。 要使用此设置，必须在所有实例上启用它。
* **待机读取超时(`standby.readtimeout`)：** 从备用实例发出的请求的超时（以毫秒为单位）。 使用的默认值为60000（1分钟）。

* **待机自动清理(`standby.autoclean`)：** 如果存储大小在同步周期中增加，则调用清理方法。

>[!NOTE]
>
>强烈建议主存储库和备用存储库具有不同的存储库ID，以便分别确定它们是否可用于卸载等服务。
>
>确保这一点得到覆盖的最佳方法是删除 *sling.id* 文件，然后重新启动实例。

## 故障切换过程 {#failover-procedures}

如果主实例由于任何原因失败，可以通过更改启动运行模式将其中一个备用实例设置为承担主实例角色，如下所述：

>[!NOTE]
>
>配置文件也需要修改，以便与用于主实例的设置匹配。

1. 转到备用实例的安装位置并停止。

1. 如果您有使用设置配置的负载平衡器，则可以在此时从负载平衡器的配置中删除主要负载平衡器。
1. 备份 `crx-quickstart` 备用安装文件夹中的文件夹。 它可用作设置新待机时的起点。

1. 使用重新启动实例 `primary` 运行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 将新主节点添加到负载平衡器。
1. 创建并启动新的备用实例。 有关更多信息，请参阅上述步骤。 [创建AEM TarMK冷备用设置](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## 将修补程序应用于冷备用设置 {#applying-hotfixes-to-a-cold-standby-setup}

将修补程序应用到冷备用安装程序的推荐方法是将这些修补程序安装到主实例，然后将其克隆到安装了修补程序的新的冷备用实例中。

您可以按照以下列出的步骤执行此操作：

1. 转到JMX控制台并使用**org.apache.jackrabbit.oak： Status (&quot;Standby&quot;)**bean停止冷备用实例上的同步过程。 有关如何执行此操作的更多信息，请参阅 [监测](#monitoring).
1. 停止冷备用实例。
1. 在主实例上安装修补程序。 有关如何安装修补程序的更多详细信息，请参阅 [如何使用包](/help/sites-administering/package-manager.md).
1. 安装后测试实例是否存在问题。
1. 通过删除冷备用实例的安装文件夹来删除该实例。
1. 停止主实例，并通过将其整个安装文件夹的文件系统副本复制到冷备用的位置来克隆该实例。
1. 重新配置新创建的克隆以用作冷备用实例。 有关其他详细信息，请参阅 [创建AEM TarMK冷备用设置。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 启动主实例和冷备用实例。

## 监测 {#monitoring}

该功能会使用JMX或MBean公开信息。 这样，您就可以使用检查待机和主控的当前状态 [JMX控制台](/help/sites-administering/jmx-console.md). 此信息可以在一个MBean中找到，其中 `type org.apache.jackrabbit.oak:type="Standby"`已命名 `Status`.

**待机**

观察备用实例时，您将公开一个节点。 ID通常是通用的UUID。

此节点具有五个只读属性：

* `Running:` 布尔值，指示同步进程是否正在运行。

* `Mode:` 客户端：后跟用于标识实例的UUID。 请注意，每次更新配置时，此UUID都会更改。

* `Status:` 当前状态的文本表示形式(例如 `running` 或 `stopped`)。

* `FailedRequests:`连续错误的次数。
* `SecondsSinceLastSuccess:` 自上次与服务器成功通信以来经过的秒数。 它将显示为 `-1` 如果未进行任何成功的通信。

还有三种可调用方法：

* `start():` 启动同步过程。
* `stop():` 停止同步过程。
* `cleanup():` 在待机模式下运行清理操作。

**主要**

通过一个MBean（其ID值是TarMK备用服务正在使用的端口号，默认情况下为8023）观察主服务器，会公开一些常规信息。 大多数方法和属性与备用磁盘相同，但有些不同：

* `Mode:` 将始终显示值 `primary`.

此外，可以检索多达10个连接到主控的客户端（备用实例）的信息。 MBean ID是实例的UUID。 这些MBean没有可调用的方法，但有一些非常有用的只读属性：

* `Name:` 客户端的ID。
* `LastSeenTimestamp:` 文本表示中最后一个请求的时间戳。
* `LastRequest:` 客户端的最后一个请求。
* `RemoteAddress:` 客户端的IP地址。
* `RemotePort:` 客户端用于上次请求的端口。
* `TransferredSegments:` 传输到此客户端的区段总数。
* `TransferredSegmentBytes:`传输到此客户端的字节总数。

## 冷备用存储库维护 {#cold-standby-repository-maintenance}

### 修订版清理 {#revision-clean}

>[!NOTE]
>
>如果您运行 [在线修订版清理](/help/sites-deploying/revision-cleanup.md) 对于主要实例，无需执行下面列出的手动过程。 此外，如果您正在使用“联机修订版清理”，则 `cleanup ()` 对备用实例的操作将自动执行。

>[!NOTE]
>
>请勿在待机时运行离线修订清理。 它不是必需的，并且不会减小区段存储大小。

Adobe建议定期运行维护，以防止随着时间的推移存储库过度增长。 要手动执行冷备用存储库维护，请执行以下步骤：

1. 转到JMX控制台并使用 **org.apache.jackrabbit.oak：状态（“待机”）** 豆子。 有关如何执行此操作的更多信息，请参阅上面的部分，地址为 [监测](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. 停止主AEM实例。
1. 在主实例上运行Oak压缩工具。 有关更多详细信息，请参阅 [维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. 启动主实例。
1. 使用第一步中所述的相同JMX Bean在备用实例上启动备用进程。
1. 观察日志并等待同步完成。 此时备用存储库可能会出现大幅增长。
1. 运行 `cleanup()` 使用第一步中所述的相同JMX Bean对备用实例进行操作。

备用实例完成与主实例的同步所需的时间可能比正常时间长，因为离线压缩会有效重写存储库历史记录，从而使存储库中的更改计算花费的时间更多。 还应注意，此过程完成后，备用存储库的大小将与主存储库的大小大致相同。

作为替代方法，在主存储库上运行压缩后，可以手动将主存储库复制到备用存储库，实际上每次运行压缩时都会重建备用存储库。

### 数据存储垃圾收集 {#data-store-garbage-collection}

请务必对文件数据存储实例不时运行垃圾收集，否则，已删除的二进制文件将保留在文件系统上，最终将填满驱动器。 要运行垃圾收集，请执行以下步骤：

1. 运行冷备用存储库维护，如一节中所述 [以上](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. 完成维护过程并重新启动实例后：

   * 在主服务器上，通过相关的JMX Bean运行数据存储垃圾收集，如中所述 [本文](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * 在待机模式下，数据存储垃圾收集只能通过 **BlobGarbageCollection** MBean - `startBlobGC()`. **RepositoryManagement **MBean在待机模式下不可用。

   >[!NOTE]
   >
   >如果您未使用共享数据存储，则垃圾收集必须首先在主节点上运行，然后在备用节点上运行。
