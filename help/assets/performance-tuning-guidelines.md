---
title: 性能调整 [!DNL Assets].
description: 关于以下内容的建议和指导 [!DNL Experience Manager] 配置，更改硬件、软件和网络组件，以消除瓶颈并优化性能 [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 性能调整指南 {#assets-performance-tuning-guide}

An [!DNL Experience Manager Assets] 安装程序包含许多硬件、软件和网络组件。 根据您的部署方案，您可能需要对硬件、软件和网络组件进行特定的配置更改以消除性能瓶颈。

此外，确定并遵守某些硬件和软件优化准则有助于奠定坚实的基础，从而帮助您 [!DNL Experience Manager Assets] 满足性能、可扩展性和可靠性方面的期望。

中的性能不佳 [!DNL Experience Manager Assets] 可能会影响用户关于交互性能、资产处理、下载速度和其他方面的体验。

事实上，在为任何项目建立目标指标之前，您都要执行性能优化这一基本任务。

下面是一些关键重点领域，在这些领域中，您可以发现并修复性能问题，以免它们对用户产生影响。

## Platform {#platform}

虽然Experience Manager在多个平台上都受支持，但Adobe发现对Linux和Windows上的本机工具支持度最高，这有助于实现最佳性能和易用性。 理想情况下，您应该部署64位操作系统以满足 [!DNL Experience Manager Assets] 部署。 与任何Experience Manager部署一样，您应尽可能实施TarMK。 虽然TarMK不能扩展至超过单个创作实例，但发现其性能优于MongoMK。 您可以添加TarMK卸载实例以提高的工作流处理能力 [!DNL Experience Manager Assets] 部署。

### 临时文件夹 {#temp-folder}

要缩短资源上传时间，请为Java临时目录使用高性能存储。 在Linux和Windows上，可以使用RAM驱动器或固态硬盘。 在基于云的环境中，可以使用等效的高速存储类型。 例如，在Amazon EC2中， [临时驱动器](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 驱动器可用于临时文件夹。

假定服务器内存充足，请配置RAM驱动器。 在Linux上，运行以下命令以创建8 GB RAM驱动器：

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows操作系统上，使用第三方驱动程序创建RAM驱动器，或者只使用高性能存储（如SSD）。

高性能临时卷就绪后，设置JVM参数 `-Djava.io.tmpdir`. 例如，您可以将下面的JVM参数添加到 `CQ_JVM_OPTS` 中的变量 `bin/start` 脚本 [!DNL Experience Manager]：

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置 {#java-configuration}

### Java版本 {#java-version}

Adobe建议部署 [!DNL Experience Manager Assets] 在Java 8上实现最佳性能。

<!-- TBD: Link to the latest official word around Java.
-->

### JVM参数 {#jvm-parameters}

设置以下JVM参数：

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 数据存储和内存配置 {#data-store-and-memory-configuration}

### 文件数据存储配置 {#file-data-store-configuration}

建议所有用户都将数据存储区与区段存储区分开 [!DNL Experience Manager Assets] 用户。 此外，配置 `maxCachedBinarySize` 和 `cacheSizeInMB` 参数可以帮助最大化性能。 设置 `maxCachedBinarySize` 可保存在缓存中的最小文件大小。 指定内存中缓存的大小，用于内的数据存储 `cacheSizeInMB`. Adobe建议将此值设置为占栈总大小的2-10%。 但是，负载/性能测试可以帮助确定理想的设置。

### 配置缓冲图像缓存的最大大小 {#configure-the-maximum-size-of-the-buffered-image-cache}

将大量资产上传到时 [!DNL Adobe Experience Manager]，为了允许内存消耗意外达到峰值，并防止JVM因OutOfMemoryErrors而失败，请减小所配置的缓冲图像缓存的最大值。 假设您有一个最大栈的系统(- `Xmx`参数)、设置为1 GB的Oak BlobCache和设置为2 GB的文档缓存。 在这种情况下，缓冲缓存将最多占用1.25 GB和内存，对于意外的峰值，仅留下0.75 GB的内存。

在OSGi Web控制台中配置缓冲缓存大小。 在 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，设置属性 `cq.dam.image.cache.max.memory` 以字节为单位。 例如，1073741824为1 GB(1024 x 1024 x 1024 = 1 GB)。

从Experience Manager6.1 SP1 ，如果您使用 `sling:osgiConfig` 配置此属性的节点，确保将数据类型设置为Long。 有关更多详细信息，请参阅 [CQBufferedImageCache在资产上传期间占用栈](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### 共享的数据存储 {#shared-data-stores}

在大规模实施中实施S3或共享文件数据存储区有助于节省磁盘空间并提高网络吞吐量。 有关使用共享数据存储的利弊的更多信息，请参阅 [Assets大小调整指南](/help/assets/assets-sizing-guide.md).

### S3数据存储 {#s-data-store}

以下S3数据存储配置( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)帮助Adobe将12.8 TB的二进制大对象(BLOB)从现有文件数据存储提取到客户站点的S3数据存储中：

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## 网络优化 {#network-optimization}

Adobe建议启用HTTPS，因为许多公司都有监听HTTP流量的防火墙，这会给上载和损坏文件带来负面影响。 对于大型文件上传，请确保用户已用有线方式连接到网络，因为WiFi网络会很快饱和。 有关确定网络瓶颈的准则，请参见 [Assets大小调整指南](/help/assets/assets-sizing-guide.md). 要通过分析网络拓扑来评估网络性能，请参见 [Assets网络注意事项](/help/assets/assets-network-considerations.md).

首先，您的网络优化策略取决于可用带宽量和您的负载。 [!DNL Experience Manager] 实例。 常见的配置选项（包括防火墙或代理）有助于提高网络性能。 请牢记以下要点：

* 根据实例类型（小、中、大），确保您有足够的网络带宽来支持Experience Manager实例。 在以下情况下，充足的带宽分配尤其重要 [!DNL Experience Manager] 托管在AWS上。
* 如果您的 [!DNL Experience Manager] 实例托管在AWS上，您可以受益于通用的扩展策略。 如果用户期望高负载，则放大实例。 在中/低负载时缩减其大小。
* HTTPS：大多数用户都设有拦截HTTP流量的防火墙，这可能会在上传操作期间对文件上传产生不利影响，甚至损坏文件。
* 大文件上传：确保用户已用有线方式连接到网络（WiFi连接快速饱和）。

## 工作流 {#workflows}

### 瞬态工作流 {#transient-workflows}

如有可能，请将 [!UICONTROL DAM更新资产] 工作流转换为临时。 该设置显着减少了处理工作流所需的开销，因为在这种情况下，工作流不需要经过正常的跟踪和存档过程。

1. 导航到 `/miscadmin` 在 [!DNL Experience Manager] 部署位置 `https://[aem_server]:[port]/miscadmin`.

1. 展开 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]** > **[!UICONTROL dam]**.

1. 打开 **[!UICONTROL DAM更新资产]**. 从浮动工具面板切换到 **[!UICONTROL 页面]** 选项卡，然后单击 **[!UICONTROL 页面属性]**.

1. 选择 **[!UICONTROL 瞬态工作流]** 并单击 **[!UICONTROL 确定]**.

   >[!NOTE]
   >
   >某些功能不支持临时工作流。 如果您的 [!DNL Assets] 部署需要这些功能，请勿配置临时工作流。

如果无法使用临时工作流，请定期运行工作流清除以删除已存档的 [!UICONTROL DAM更新资产] 工作流可确保系统性能不会降低。

通常，每周执行清除工作流。 但是，在资源密集型场景中（如在大规模资产摄取期间），您可以更频繁地执行该操作。

要配置工作流清除，请通过OSGi控制台添加新的AdobeGranite工作流清除配置。 接下来，在每周维护时段中配置和计划工作流。

如果清除时间过长，则会超时。 因此，您应确保完成清除作业，以避免由于大量工作流而导致清除工作流无法完成的情况。

例如，在执行大量非临时工作流（创建工作流实例节点）后，您可以执行 [ACS AEM Commons工作流移除程序](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 临时性的。 它立即删除多余的已完成工作流实例，而不是等待AdobeGranite工作流清除计划程序运行。

### 最大并行作业数 {#maximum-parallel-jobs}

默认情况下， [!DNL Experience Manager] 运行的最大并行作业数等于服务器上的处理器数。 此设置的问题在于，在重负载期间，所有处理器都被 [!UICONTROL DAM更新资产] 工作流，降低UI响应速度并防止 [!DNL Experience Manager] 防止运行其他进程，从而保护服务器的性能和稳定性。 最佳做法是，通过执行以下步骤，将此值设置为服务器上可用处理器的一半：

1. 日期 [!DNL Experience Manager] 作者，访问 `https://[aem_server]:[port]/system/console/slingevent`.

1. 单击 **[!UICONTROL 编辑]** ，例如，与您的实施相关的每个工作流队列中的 **[!UICONTROL Granite Transient工作流队列]**.

1. 更新值 **[!UICONTROL 最大并行作业数]** 并单击 **[!UICONTROL 保存]**.

首先，将队列设置为一半可用处理器是一种可行的解决方案。 但是，您可能必须增加或减少此数字才能达到最大吞吐量并根据环境对其进行调整。 瞬态和非瞬态工作流以及其他进程（如外部工作流）有单独的队列。 如果多个队列同时设置为50%的处理器处于活动状态，则系统可能会快速过载。 大量使用的队列因用户实施而异。 因此，您可能必须仔细配置这些服务器以最大限度地提高效率，而又不能牺牲服务器的稳定性。

### DAM更新资产配置 {#dam-update-asset-configuration}

此 [!UICONTROL DAM更新资产] 工作流包含为任务配置的一整套步骤，例如Dynamic Media PTIFF生成和 [!DNL Adobe InDesign Server] 集成。 但是，大多数用户可能不需要执行以下几个步骤。 Adobe建议您创建 [!UICONTROL DAM更新资产] 工作流模型，并删除任何不必要的步骤。 在这种情况下，请更新以下项的启动器 [!UICONTROL DAM更新资产] 指向新模型。

运行 [!UICONTROL DAM更新资产] 工作流会显着增加文件数据存储的大小。 通过Adobe进行的实验表明，如果在8小时内执行约5500个工作流，则数据存储大小可以增加约400 GB。

这是临时增加，运行数据存储垃圾收集任务后，数据存储将恢复到其原始大小。

通常，数据存储垃圾收集任务与其他计划维护任务一起每周运行。

如果磁盘空间有限并运行 [!UICONTROL DAM更新资产] 工作流中，请考虑更频繁地安排垃圾收集任务。

#### 运行时演绎版生成 {#runtime-rendition-generation}

客户在其网站中使用各种大小和格式的图像，或将其分发给业务合作伙伴。 由于每个演绎版都会增加资源在存储库中的占地面积，因此Adobe建议谨慎使用此功能。 要减少处理和存储图像所需的资源量，您可以在运行时生成这些图像，而不是在摄取期间生成演绎版。

许多Sites客户都实施一个图像servlet，该图像可在请求图像时调整大小和裁剪图像，这会对发布实例施加额外的负载。 但是，只要可以缓存这些图像，挑战就可以减轻。

另一种方法是使用Dynamic Media技术完全放弃图像操作。 此外，您可以部署不仅从以下位置接管节目生成职责的Brand Portal： [!DNL Experience Manager] 基础架构，以及整个发布层。

#### ImageMagick {#imagemagick}

如果您自定义 [!UICONTROL DAM更新资产] 此工作流用于使用ImageMagick生成演绎版，Adobe建议您修改 `policy.xml` 文件位置 `/etc/ImageMagick/`. 默认情况下， ImageMagick使用操作系统卷上的全部可用磁盘空间和可用内存。 在中进行以下配置更改 `policymap` 部分 `policy.xml` 以限制这些资源。

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

此外，还将ImageMagick临时文件夹的路径设置为 `configure.xml` 文件(或通过设置环境变量 `MAGICK_TEMPORARY_PATH`)到具有足够空间和IOPS的磁盘分区。

>[!CAUTION]
>
>如果ImageMagick使用所有可用磁盘空间，错误配置可能会使服务器不稳定。 使用ImageMagick处理大型文件所需的策略更改可能会影响 [!DNL Experience Manager] 性能。 有关更多信息，请参阅 [安装和配置ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` 和 `configure.xml` 文件位于 `/usr/lib64/ImageMagick-&#42;/config/` 而不是 `/etc/ImageMagick/`请参见 [ImageMagick文档](https://www.imagemagick.org/script/resources.php) 用于配置文件的位置。

如果您使用 [!DNL Experience Manager] 如果您计划处理大量大型PSD或PSB文件，请在Adobe Managed Services (AMS)上联系Adobe客户支持。 与Adobe客户支持代表合作，为您的AMS部署实施这些最佳实践，并为Adobe的专有格式选择最佳工具和模型。 [!DNL Experience Manager] 可能无法处理超过 30000 x 23000 像素的高分辨率 PSB 文件。

### XMP写回 {#xmp-writeback}

每当在中修改元数据时，XMP写回都会更新原始资源 [!DNL Experience Manager]，从而导致出现以下情况：

* 资源本身已修改
* 已创建资源的版本
* [!UICONTROL DAM更新资产] 针对资产运行

所列成果消耗了相当多的资源。 因此，如果不需要回写，Adobe建议禁用XMP。 有关更多信息，请参阅 [XMP写回](/help/assets/xmp-writeback.md).

如果选中运行工作流标志，则导入大量元数据可能会导致资源密集的XMP写回活动。 在精益服务器使用期间规划此类导入，以便其他用户的性能不会受到影响。

## 复制 {#replication}

在将资源复制到大量发布实例（例如在Sites实施中）时，Adobe建议您使用链复制。 在这种情况下，创作实例将复制到单个发布实例，然后复制到其他发布实例，从而释放创作实例。

### 配置链复制 {#configure-chain-replication}

1. 选择要用于链接复制的发布实例
1. 在该发布实例上添加指向其他发布实例的复制代理
1. 在每个复制代理上，在“触发器”选项卡上启用“接收时”

>[!NOTE]
>
>Adobe不建议自动激活资源。 但是，如有必要，Adobe建议将此作为工作流中的最后一步，通常是DAM更新资源。

## 搜索索引 {#search-indexes}

安装 [最新Service Pack](/help/release-notes/release-notes.md) 和性能相关的修补程序，因为这些修补程序通常包括系统索引的更新。 参见 [性能调整提示](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) 进行一些索引优化。

为经常运行的查询创建自定义索引。 有关详细信息，请参阅 [分析慢查询的方法](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 和 [编制自定义索引](/help/sites-deploying/queries-and-indexing.md). 有关查询和索引最佳实践的其他见解，请参阅 [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene索引配置 {#lucene-index-configurations}

可以对Oak索引配置进行一些优化，以帮助改进 [!DNL Experience Manager Assets] 性能。 更新索引配置以缩短重新索引时间：

1. 打开CRXDe `/crx/de/index.jsp` 并以管理用户身份登录。
1. 浏览到 `/oak:index/lucene`.
1. 添加 `String[]` 属性 `excludedPaths` 具有值 `/var`， `/etc/workflow/instances`、和 `/etc/replication`.
1. 浏览到 `/oak:index/damAssetLucene`. 添加 `String[]` 属性 `includedPaths` 带值 `/content/dam`. 保存更改。

如果您的用户不需要对资源进行全文搜索，例如，搜索PDF文档中的文本，然后禁用它。 您可以通过禁用全文索引来提高索引性能。 禁用 [!DNL Apache Lucene] 文本提取，请执行以下步骤：

1. In [!DNL Experience Manager] 界面，访问 [!UICONTROL 包管理器].
1. 上传并安装可在以下位置找到的包： [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### 猜测总数 {#guess-total}

在创建可生成大型结果集的查询时，请使用 `guessTotal` 参数，以避免在运行这些参数时内存使用率过高。

## 已知问题 {#known-issues}

### 大文件 {#large-files}

存在两个与中的大型文件相关的主要已知问题 [!DNL Experience Manager]. 当文件大小大于2 GB时，冷备用同步可能会出现内存不足的情况。 在某些情况下，它会阻止备用同步运行。 在其他情况下，它会导致主实例崩溃。 此方案适用于中的任何文件 [!DNL Experience Manager] 大于2GB，包括内容包。

同样，当文件在使用共享S3数据存储时的大小达到2 GB时，可能需要一些时间才能将文件从缓存完全保存到文件系统。 因此，在使用无二进制复制时，可能会在复制完成之前未保留二进制数据。 这种情况可能导致一些问题，尤其是当数据的可用性很重要时。

## 性能测试 {#performance-testing}

每 [!DNL Experience Manager] 部署，建立能够快速发现并解决瓶颈的性能测试机制。 以下是一些需要重点关注的关键领域。

### 网络测试 {#network-testing}

对于客户的所有网络性能问题，请执行以下任务：

* 从客户网络内部测试网络性能
* 在Adobe网络中测试网络性能。 对于AMS客户，请与您的CSE合作，从Adobe网络中进行测试。
* 从另一个接入点测试网络性能
* 使用网络基准测试工具
* 针对Dispatcher进行测试

### [!DNL Experience Manager] 部署测试 {#aem-deployment-testing}

要通过高效的CPU利用率和负载共享将延迟降至最低并实现高吞吐量，请监控您的服务器性能， [!DNL Experience Manager] 定期部署。 特别是：

* 针对运行负载测试 [!DNL Experience Manager] 部署。
* 监控上传性能和UI响应性。

## [!DNL Experience Manager Assets] 性能核对清单和资产管理任务的影响 {#checklist}

* 启用HTTPS以绕过任何公司HTTP流量探查器。
* 使用有线连接上传大量资产。
* 在Java 8上部署。
* 设置最佳JVM参数。
* 配置文件系统数据存储或S3数据存储。
* 禁用子资源生成。 如果启用，AEM Workflow将为多页资源中的每个页面创建单独的资源。 这些页面中的每一个页面都是一个单独的资产，它占用了额外的磁盘空间，需要进行版本控制和额外的工作流处理。 如果您不需要单独的页面，请禁用子资产生成和页面提取活动。
* 启用瞬态工作流。
* 调整Granite工作流队列以限制并发作业。
* 配置 [!DNL ImageMagick] 以限制资源消耗。
* 从删除不必要的步骤 [!UICONTROL DAM更新资产] 工作流。
* 配置工作流和版本清除。
* 使用最新的Service Pack和修补程序优化索引。 请联系Adobe客户支持部门，了解可能提供的任何其他索引优化。
* 使用guessTotal优化查询性能。
* 如果您配置 [!DNL Experience Manager] 从文件内容中检测文件类型(通过启用 **[!UICONTROL Day CQ DAM Mime类型服务]** 在 **[!UICONTROL AEM Web控制台]**)，在非高峰时间批量上传许多文件，因为它占用大量资源。
