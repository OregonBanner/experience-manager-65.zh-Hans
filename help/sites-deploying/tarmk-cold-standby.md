---
title: 如何在TarMK冷待机状态下运行AEM
description: 了解如何创建、配置和维护TarMK冷备用设置。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '2671'
ht-degree: 0%

---

# 如何在TarMK冷待机状态下运行AEM{#how-to-run-aem-with-tarmk-cold-standby}

## 简介 {#introduction}

Tar微内核的冷备用容量允许一个或多个备用Adobe Experience Manager (AEM)实例连接到主实例。 同步过程只是单向的，这意味着它只能从主实例到备用实例完成。

备用实例的目的是保证主存储库的实时数据副本，并在主存储库因任何原因不可用时确保快速切换而不会丢失数据。

内容在主实例和备用实例之间线性同步，无需对文件或存储库损坏进行任何完整性检查。 由于此设计，备用实例是主实例的精确副本，并且无法帮助缓解主实例上的不一致。

>[!NOTE]
>
>冷待机功能旨在保护以下情况下需要的高可用性： **作者** 实例。 对于在上需要高可用性的情况 **Publish** 使用Tar微内核的实例，Adobe建议使用发布场。
>
>有关更多可用部署的信息，请参阅 [建议的部署](/help/sites-deploying/recommended-deploys.md) 页面。

>[!NOTE]
>
>设置备用实例或从主节点派生备用实例时，它仅允许访问以下控制台（用于与管理相关的活动）：
>
>* OSGI Web控制台
>
>无法访问其他控制台。

## 工作原理 {#how-it-works}

在主AEM实例上， TCP端口已打开并正在侦听传入消息。 目前，奴隶向主用户发送两种类型的消息：

* 请求当前标头的区段ID的消息
* 请求具有指定ID的区段数据的消息

待机周期性地请求主设备的当前头的段ID。 如果该区段在本地未知，则会检索它。 如果数据段已存在，则会比较数据段，并在必要时请求引用的数据段。

>[!NOTE]
>
>备用实例未收到任何类型的请求，因为它们以仅同步模式运行。 备用实例上唯一可用的部分是Web控制台，以便于配置捆绑包和服务。

典型的TarMK冷备用部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特征 {#other-characteristics}

### 稳健性 {#robustness}

数据流旨在自动检测并处理连接和网络相关问题。 所有数据包都绑定了校验和，当连接出现问题或损坏的数据包时，将触发重试机制。

#### 性能 {#performance}

在主实例上启用TarMK冷备用对性能几乎没有可衡量的影响。 额外的CPU占用率很低，额外的硬盘和网络IO应该不会产生性能问题。

在待机状态下，在同步过程中可能会出现高CPU消耗。 由于该过程不是多线程的，因此不能通过使用多个内核来加速该过程。 如果未更改或传输任何数据，则不存在可衡量的活动。 连接速度因硬件和网络环境而异，但并不取决于存储库的大小或SSL的使用。 在估计初始同步所需的时间或在主节点上同时更改许多数据时，请记住这一点。

#### 安全性 {#security}

假定所有实例都运行在同一个内联网安全区域中，安全漏洞的风险就会大大降低。 但是，可以通过启用从进程和主进程之间的SSL连接来添加额外的安全层。 这样做可以降低数据被中间人破坏的可能性。

此外，您还可以通过限制传入请求的IP地址来指定允许连接的备用实例。 这应该有助于保证内部网中的任何人都无法复制存储库。

>[!NOTE]
>
>建议在Dispatcher和冷备用设置中的服务器之间添加负载平衡器。 负载平衡器应配置为仅将用户流量定向到 **主要** 实例。 这是确保一致性并防止通过冷备用机制以外的其他方式在备用实例上复制内容所必需的。

## 创建AEM TarMK冷备用设置 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>与先前版本相比，AEM 6.3中区段节点存储和备用存储服务的PID发生了更改，如下所示：
>
>* 从org.apache.jackrabbit.oak.**插件**.segment.standby.store.StandbyStoreService到org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* 从org.apache.jackrabbit.oak.**插件**.segment.SegmentNodeStoreService到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>进行必要的配置调整，以便它们反映此更改。

要创建TarMK冷备用设置，首先要通过将主服务器的整个安装文件夹的文件系统复制到新位置来创建备用实例。 然后，您可以使用指定其角色的运行模式来启动每个实例( `primary` 或 `standby`)。

以下是创建具有一个主实例和一个备用实例的安装程序必须遵循的过程：

1. 安装AEM。

1. 关闭实例，并将其安装文件夹复制到冷备用实例运行所在的位置。 即使从不同的计算机运行，请确保为每个文件夹提供一个描述性名称(例如 *aem-primary* 或 *aem-standby*)以区分实例。
1. 转到主实例的安装文件夹并：

   1. 检查并删除您之前可能拥有的任何OSGi配置 `aem-primary/crx-quickstart/install`

   1. 创建名为的文件夹 `install.primary` 下 `aem-primary/crx-quickstart/install`

   1. 为下的首选节点存储和数据存储创建所需的配置 `aem-primary/crx-quickstart/install/install.primary`
   1. 创建名为的文件 `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` 在同一位置，并相应地对其进行配置。 有关配置选项的详细信息，请参阅 [配置](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. 如果您将AEM TarMK实例与外部数据存储一起使用，请创建名为的文件夹 `crx3` 下 `aem-primary/crx-quickstart/install` 已命名 `crx3`

   1. 将数据存储配置文件放入 `crx3` 文件夹。

   例如，如果您运行的是具有外部文件数据存储的AEM TarMK实例，则需要以下配置文件：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   在下面查找主实例的示例配置：

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

1. 为创建Apache Sling日志记录器 **org.apache.jackrabbit.oak.segment** 包。 将日志级别设置为“Debug”，并将其日志输出指向单独的日志文件，如 */logs/tarmk-coldstandby.log*. 有关更多信息，请参阅 [记录](/help/sites-deploying/configure-logging.md).
1. 转到 **待机** 通过运行jar启动该实例。
1. 创建与主数据库相同的日志记录配置。 然后，停止该实例。
1. 接下来，准备备用实例。 为此，您可以执行与主实例相同的步骤：

   1. 删除下可能包含的任何文件 `aem-standby/crx-quickstart/install`.
   1. 创建名为的文件夹 `install.standby` 下 `aem-standby/crx-quickstart/install`

   1. 创建两个名为的配置文件：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. 创建名为的文件夹 `crx3` 下 `aem-standby/crx-quickstart/install`

   1. 创建数据存储配置并将其放在 `aem-standby/crx-quickstart/install/crx3`. 在本例中，必须创建的文件是：

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. 编辑文件并创建必要的配置。

   以下是典型备用实例的配置文件示例：

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

1. 启动 **待机** 使用备用运行模式运行实例：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

该服务还可以通过Web控制台进行配置，方法是：

1. 转到位于以下位置的Web控制台： *https://serveraddress:serverport/system/console/configMgr*
1. 正在查找名为的服务 **Apache Jackrabbit Oak区段Tar冷备用服务** 并双击以编辑设置。
1. 保存设置并重新启动实例，以便新设置生效。

>[!NOTE]
>
>您可以随时通过检查是否存在 **主要** 或 **待机** 在Sling设置Web控制台中运行模式。
>
>这可以通过转到 *https://localhost:4502/system/console/status-slingsettings* 并检查 **“运行模式”** 行。

## 首次同步 {#first-time-synchronization}

在准备完成且首次启动待机后，当待机状态到达主状态时，实例之间将出现大量的网络流量。 您可以查阅日志以观察同步的状态。

待机 *tarmk-coldstandby.log*，您可以看到以下条目：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

待命时间 *error.log*，您应该会看到如下条目：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述日志片段中， *10.20.30.40* 是主节点的IP地址。

在 **主要** *tarmk-coldstandby.log*，您会看到以下条目：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message 's.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd' from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在这种情况下，日志中提到的“客户端”是 **待机** 实例。

一旦这些条目停止显示在日志中，就可以放心地假定同步过程已完成。

虽然上述条目显示轮询机制运行正常，但了解是否在轮询时同步任何数据通常很有用。 为此，请查找以下条目：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，在与非共享对象一起运行时 `FileDataStore`，如下消息确认正在正确传输二进制文件：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 配置 {#configuration}

以下OSGi设置可用于冷备用服务：

* **保留配置：** 如果启用，这会将配置存储在存储库中，而不是传统的OSGi配置文件中。 Adobe建议在生产系统上保持禁用此设置，以便主配置不被待机模式提取。

* **模式(`mode`)：** 这会选择实例的运行模式。

* **端口（端口）：** 用于通信的端口。 默认为 `8023`。

* **主主机(`primary.host`)：**  — 主实例的主机。 此设置仅适用于待机。
* **同步间隔(`interval`)：**  — 此设置确定同步请求之间的间隔，并且仅适用于备用实例。

* **允许的IP范围(`primary.allowed-client-ip-ranges`)：**  — 主服务器允许从其进行连接的IP范围。
* **安全(`secure`)：** 启用SSL加密。 要使用此设置，必须在所有实例上启用它。
* **待机读取超时(`standby.readtimeout`)：** 从备用实例发出的请求超时（以毫秒为单位）。 使用的默认值为60000（一分钟）。

* **待机自动清理(`standby.autoclean`)：** 如果存储的大小在同步周期中增加，则调用清理方法。

>[!NOTE]
>
>Adobe建议主资料库和备用资料库具有不同的资料库ID，以便它们可分别用于卸载等服务。
>
>确保涵盖此范围的最佳方法是，删除 *sling.id* 待机，然后重新启动实例。

## 故障切换过程 {#failover-procedures}

如果主实例由于任何原因失败，可以通过更改启动运行模式将其中一个备用实例设置为承担主实例的角色，如下所述：

>[!NOTE]
>
>编辑配置文件，使其匹配用于主实例的设置。

1. 转到备用实例的安装位置，然后停止该实例。

1. 如果您有使用设置配置的负载平衡器，则可以在此时从负载平衡器的配置中删除主服务器。
1. 备份 `crx-quickstart` 来自备用安装文件夹的文件夹。 它可以用作设置新待机时的起点。

1. 使用重新启动实例 `primary` 运行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 将新主节点添加到负载平衡器。
1. 创建并启动新的备用实例。 有关详细信息，请参阅上面的步骤 [创建AEM TarMK冷备用设置](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## 将修补程序应用于冷备用设置 {#applying-hotfixes-to-a-cold-standby-setup}

将修补程序应用到冷备用设置的推荐方法是：将修补程序安装到主实例，然后将其克隆到安装了修补程序的新的冷备用实例中。

您可以按照以下列出的步骤执行此操作：

1. 转到JMX控制台并使用**org.apache.jackrabbit.oak： Status (&quot;Standby&quot;)**bean停止冷备用实例上的同步过程。 有关如何执行此操作的更多信息，请参阅 [监控](#monitoring).
1. 停止冷备用实例。
1. 在主实例上安装修补程序。 有关如何安装修补程序的更多详细信息，请参阅 [如何使用包](/help/sites-administering/package-manager.md).
1. 安装后，测试实例是否存在问题。
1. 通过删除冷备用实例的安装文件夹来删除该实例。
1. 停止主实例，并通过将其整个安装文件夹的文件系统复制到冷备用位置来克隆该实例。
1. 重新配置新创建的克隆，使其充当冷备用实例。 请参阅 [创建AEM TarMK冷备用设置。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 启动主实例和冷备用实例。

## 监测 {#monitoring}

该功能使用JMX或MBean公开信息。 这样，您就可以使用 [JMX控制台](/help/sites-administering/jmx-console.md). 此信息可以在一个MBean中找到，地址为 `type org.apache.jackrabbit.oak:type="Standby"`已命名 `Status`.

**待机**

观察待机实例时，会公开一个节点。 ID通常是通用UUID。

此节点具有五个只读属性：

* `Running:` 布尔值，指示同步进程是否正在运行。

* `Mode:` 客户端：后跟用于标识实例的UUID。 每次更新配置时，此UUID都会更改。

* `Status:` 当前状态的文本表示形式(如 `running` 或 `stopped`)。

* `FailedRequests:`连续错误数。
* `SecondsSinceLastSuccess:` 自上次与服务器成功通信以来经过的秒数。 它显示 `-1` 如果未成功通信。

还有三种可调用方法：

* `start():` 启动同步过程。
* `stop():` 停止同步进程。
* `cleanup():` 在待机时运行清理操作。

**主要**

通过一个MBean（其ID值是TarMK备用服务正在使用的端口号，默认端口号为8023）来观察主节点，从而公开一些常规信息。 大多数方法和属性与待机相同，但有些不同：

* `Mode:` 始终显示值 `primary`.

此外，可以检索与主设备连接的多达10个客户端（备用实例）的信息。 MBean ID是实例的UUID。 这些MBean没有可调用方法，但有一些有用的只读属性：

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
>如果您运行 [在线修订版清理](/help/sites-deploying/revision-cleanup.md) 对于主要实例，无需执行以下手动步骤。 此外，如果您正在使用“在线修订版清理”，则 `cleanup ()` 对备用实例的操作是自动执行的。

>[!NOTE]
>
>请勿在待机时运行脱机修订版清理。 它不是必需的，并且不会减小区段存储大小。

Adobe建议定期运行维护以防止存储库随时间推移过度增长。 要手动执行冷备用存储库维护，请执行以下步骤：

1. 转到JMX控制台并使用 **org.apache.jackrabbit.oak：状态（“待机”）** 豆子。 有关如何执行此操作的更多信息，请参阅上面的部分，地址为 [监控](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. 停止主AEM实例。
1. 在主实例上运行Oak压缩工具。 有关更多详细信息，请参阅 [维护存储库](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. 启动主实例。
1. 使用第一步中所述的相同JMX Bean在备用实例上启动备用进程。
1. 观察日志并等待同步完成。 当前备用存储库中可能会出现大幅增长。
1. 运行 `cleanup()` 使用第一步中所述的相同JMX Bean对备用实例进行操作。

备用实例完成与主实例的同步可能需要比平常更长的时间，因为离线压缩会有效地重写存储库历史记录，从而使存储库中的更改计算花费更多时间。 此过程完成后，备用存储库的大小与主存储库的大小大致相同。

作为替代方法，在主存储库上运行压缩后，可以手动将主存储库复制到备用存储库，实际上每次压缩运行时都会重建备用存储库。

### 数据存储垃圾收集 {#data-store-garbage-collection}

不时必须对文件数据存储实例运行垃圾收集，否则，已删除的二进制文件将保留在文件系统上，最终将填满驱动器。 要运行垃圾回收，请按照以下步骤操作：

1. 按照一节中的说明运行冷备用存储库维护 [以上](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. 完成维护过程并重新启动实例后：

   * 在主计算机上，通过相关JMX Bean运行数据存储垃圾收集，如中所述 [本文](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * 在待机状态下，数据存储垃圾收集仅通过 **BlobGarbageCollection** MBean - `startBlobGC()`. 此 **存储库管理** MBean在待机状态下不可用。

   >[!NOTE]
   >
   >如果您不使用共享数据存储，请首先在主系统上运行垃圾回收，然后在备用系统上运行垃圾回收。
