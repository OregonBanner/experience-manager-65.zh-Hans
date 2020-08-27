---
title: 性能调整 [!DNL Adobe Experience Manager Assets]。
description: 有关配置、 [!DNL Experience Manager] 对硬件、软件和网络组件进行更改以消除瓶颈并优化性能的建议和指导 [!DNL Experience Manager Assets]。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 5a421c66930d8c7a9eb633c707b4b51d4549b303
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 0%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 性能调整指南 {#assets-performance-tuning-guide}

安 [!DNL Experience Manager Assets] 装程序包含许多硬件、软件和网络组件。 根据部署方案，您可能需要对硬件、软件和网络组件进行特定配置更改以消除性能瓶颈。

此外，确定并遵守某些硬件和软件优化指南有助于建立可靠的基础，使您的部署能 [!DNL Experience Manager Assets] 够满足性能、可伸缩性和可靠性方面的期望。

低性能可 [!DNL Experience Manager Assets] 能影响用户在交互性能、资产处理、下载速度等方面的体验。

事实上，性能优化是您在为任何项目建立任务指标之前执行的一项基本目标。

以下是您在对用户产生影响之前发现并修复性能问题的一些关键重点区域。

## 平台 {#platform}

虽然Experience Manager在许多平台上都受支持，但Adobe在Linux和Windows上对本机工具的支持最强，这有助于实现最佳性能并简化实施。 理想情况下，您应部署64位操作系统以满足部署的高内存 [!DNL Experience Manager Assets] 要求。 与任何Experience Manager部署一样，您应尽可能实施TarMK。 虽然TarMK无法扩展到单个作者实例之外，但其性能比MongoMK更好。 您可以添加TarMK卸载实例，以提高部署的工作流处理 [!DNL Experience Manager Assets] 能力。

### 临时文件夹 {#temp-folder}

要缩短资产上传时间，请对Java临时目录使用高性能存储。 在Linux和Windows上，可以使用RAM驱动器或SSD。 在基于云的环境中，可以使用等效的高速存储类型。 例如，在AmazonEC2中，临 [时驱动器](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 可用于临时文件夹。

假定服务器内存充足，请配置RAM驱动器。 在Linux上，运行以下命令以创建8 GB RAM驱动器：

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows操作系统上，使用第三方驱动程序创建RAM驱动器或只使用高性能存储（如SSD）。

高性能临时卷准备就绪后，请设置JVM参数 `-Djava.io.tmpdir`。 例如，您可以将以下JVM参数添加 `CQ_JVM_OPTS` 到以下脚本 `bin/start` 中的变量 [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置 {#java-configuration}

### Java版本 {#java-version}

Adobe建议 [!DNL Experience Manager Assets] 在Java 8上部署以获得最佳性能。

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

建议所有用户将数据存储区与区段存储区分 [!DNL Experience Manager Assets] 开。 此外，配置和参 `maxCachedBinarySize` 数可 `cacheSizeInMB` 以帮助最大化性能。 设 `maxCachedBinarySize` 置为可保存在缓存中的最小文件大小。 指定用于中数据存储的内存中缓存的大小 `cacheSizeInMB`。 Adobe建议将此值设置为总堆大小的2-10%。 但是，负载／性能测试有助于确定理想的设置。

### 配置缓冲的图像缓存的最大大小 {#configure-the-maximum-size-of-the-buffered-image-cache}

将大量资产上传到时， [!DNL Adobe Experience Manager]为了允许意外的内存消耗高峰，并防止JVM因OutOfMemoryError而失败，请减小已缓冲的映像缓存的已配置最大大小。 例如，您有一个系统，其最大堆(- `Xmx`参数)为5 GB,Oak BlobCache设置为1 GB,文档缓存设置为2 GB。 在这种情况下，缓冲的缓存将最大占用1.25 GB内存，这将仅保留0.75 GB内存，以防意外的峰值。

在OSGi Web控制台中配置缓冲的缓存大小。 在 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，以字节为单 `cq.dam.image.cache.max.memory` 位设置属性。 例如，1073741824为1 GB(1024 x 1024 x 1024 = 1 GB)。

从Experience Manager6.1 SP1中，如果您使用节点 `sling:osgiConfig` 配置此属性，请确保将数据类型设置为长。 有关详细信息，请参 [阅CQBufferedImageCache在资产上传过程中消耗堆](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)。

### 共享数据存储 {#shared-data-stores}

实施S3或共享文件数据存储有助于在大规模实施中节省磁盘空间和增加网络吞吐量。 有关使用共享数据存储的利弊的更多信息，请参阅资产 [大小调整指南](/help/assets/assets-sizing-guide.md)。

### S3 data store {#s-data-store}

以下S3数据存储配置( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)帮助Adobe从现有文件数据存储中提取12.8 TB的二进制大对象(BLOB)到客户站点的S3数据存储中：

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

Adobe建议启用HTTPS，因为许多公司都有防火墙来监听HTTP通信，这会对上传和损坏文件产生不利影响。 对于大文件上传，请确保用户已连接到网络，因为WiFi网络很快达到饱和。 有关确定网络瓶颈的指南，请参 [阅资产规模指南](/help/assets/assets-sizing-guide.md)。 要通过分析网络拓扑来评估网络性能，请参 [阅资产网络注意事项](/help/assets/assets-network-considerations.md)。

主要是，网络优化策略取决于可用带宽量和实例的负 [!DNL Experience Manager] 载。 包括防火墙或代理在内的常见配置选项有助于提高网络性能。 以下是需要牢记的一些要点：

* 根据您的实例类型（小、中、大），确保您的Experience Manager实例具有足够的网络带宽。 如果在AWS上托管，则适当的 [!DNL Experience Manager] 带宽分配尤为重要。
* 如果您 [!DNL Experience Manager] 的实例托管在AWS上，您可以通过采用通用扩展策略受益。 如果用户期望负载较高，请升级实例。 缩小它以适中／低负载。
* HTTPS:大多数用户都有防火墙来嗅探HTTP通信，这可能会对上载文件或在上载操作期间损坏文件产生不利影响。
* 大文件上传：确保用户有有线网络连接到网络（WiFi连接快速饱和）。

## 工作流 {#workflows}

### 临时工作流 {#transient-workflows}

尽可能将DAM更新资产 [!UICONTROL 工作流设置为] “临时”。 该设置显着减少了处理工作流所需的开销，因为在这种情况下，工作流无需通过正常的跟踪和存档过程。

1. 在部 `/miscadmin` 署中 [!DNL Experience Manager] 导航到 `https://[aem_server]:[port]/miscadmin`。

1. 展开 **[!UICONTROL 工具]** >工 **[!UICONTROL 作流]** > **[!UICONTROL 模型]** > **[!UICONTROL dam]**。

1. 打开 **[!UICONTROL DAM更新资产]**。 从浮动工具面板中，切换到“页 **[!UICONTROL 面]** ”选项卡，然后单 **[!UICONTROL 击“页面属性]**”。

1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >某些功能不支持临时工作流。 如果您 [!DNL Assets] 的部署需要这些功能，请不要配置临时工作流。

如果无法使用临时工作流，请定期运行工作流清除以删除已存档 [!UICONTROL 的DAM更新资产] 工作流，以确保系统性能不会降低。

通常，每周执行清除工作流。 但是，在资源密集型情况（如在大规模资产摄取期间）中，您可以更频繁地执行它。

要配置工作流清除，请通过OSGi控制台添加新的AdobeGranite工作流清除配置。 接下来，在每周维护窗口中配置和计划工作流。

如果清除时间过长，就会超时。 因此，您应确保清除作业完成，以避免由于工作流数量过多而无法完成清除工作流的情况。

例如，在执行大量非临时工作流（创建工作流实例节点）后，您可以在 [点对点基础上执行ACS AEM](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) Commons Workflow Remover。 它会立即删除冗余的已完成工作流实例，而不是等待AdobeGranite工作流清除调度程序运行。

### 最大并行作业数 {#maximum-parallel-jobs}

默认情况 [!DNL Experience Manager] 下，运行与服务器上处理器数相等的最大并行作业数。 此设置的问题在于，在负载较重的时期，所有处理器都被DAM更新资产 [!UICONTROL 工作流占用] ，从而减缓UI响应速度，并阻止运行其 [!DNL Experience Manager] 他可保护服务器性能和稳定性的进程。 最好通过执行以下步骤将此值设置为服务器上可用处理器的一半：

1. 在创 [!DNL Experience Manager] 作时，访问 `https://[aem_server]:[port]/system/console/slingevent`。

1. 单击 **[!UICONTROL 与您]** 的实现相关的每个工作流队列上的“编辑”(Edit), **[!UICONTROL 例如“Granite Transient Workflow队列”]**。

1. 更新“最大并行作 **[!UICONTROL 业数”的值]** ，然后单 **[!UICONTROL 击“保存”]**。

将队列设置到一半可用处理器是开始的可行解决方案。 但是，您可能必须增加或减少此数量，才能实现最大吞吐量并按环境调整它。 对于临时工作流和非临时工作流以及其他进程（如外部），存在单独的队列。 如果设置为50%的处理器同时处于活动状态，则系统会迅速过载。 大量使用的队列在用户实现中差别很大。 因此，您可能必须仔细配置它们以获得最高效率，而不牺牲服务器稳定性。

### DAM更新资产配置 {#dam-update-asset-configuration}

DAM [!UICONTROL 更新资产工作流] ，包含为任务配置的完整步骤套件，如Scene7PTIFF生成和 [!DNL Adobe InDesign Server] 集成。 但是，大多数用户可能不需要执行以下几个步骤。 Adobe建议您创建DAM更新资产工 [!UICONTROL 作流模型的自定] 义副本，并删除任何不必要的步骤。 在这种情况下，请更新DAM更 [!UICONTROL 新资产的启动器] ，以指向新模型。

集中运 [!UICONTROL 行DAM更新资产] ，可以大幅增加文件数据存储的大小。 通过Adobe进行的试验表明，如果在8小时内执行约5500个工作流，则数据存储大小可以增加约400 GB。

它是临时增加，在您运行数据存储垃圾收集任务后，数据存储恢复为其原始大小。

通常，数据存储垃圾收集任务与其他计划维护任务一起每周运行。

如果您的磁盘空间有限，并集中运 [!UICONTROL 行DAM更新资产工作流] ，请考虑更频繁地安排垃圾收集任务。

#### 运行时再现生成 {#runtime-rendition-generation}

客户在其网站中使用各种大小和格式的图像，或分发给业务合作伙伴。 由于每个再现都会添加到存储库中资产的占用空间，因此Adobe建议谨慎使用此功能。 要减少处理和存储图像所需的资源量，您可以在运行时生成这些图像，而不是在摄取期间生成再现。

许多站点客户实现一个图像servlet，在请求图像时调整大小和裁切图像，这会给发布实例增加额外的负载。 但是，只要可以缓存这些图像，挑战就可以缓解。

另一种方法是使用Scene7技术完全放弃图像处理。 此外，您还可以部署Brand Portal，它不仅负责从基础结构生成再现， [!DNL Experience Manager] 而且负责整个发布层。

#### ImageMagick {#imagemagick}

如果您自定义DAM [!UICONTROL 更新资产工作流] ，以使用ImageMagick生成再现，Adobe建议您在 `policy.xml` 修改文件 `/etc/ImageMagick/`。 默认情况下，ImageMagick使用操作系统卷上的整个可用磁盘空间和可用内存。 在的部分中进行以下配置 `policymap` 更改以 `policy.xml` 限制这些资源。

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

此外，将文件中ImageMagick的临时文件夹的路径( `configure.xml` 或通过设置环境变量)设置为具有足够空 `MAGIC_TEMPORARY_PATH`间和IOPS的磁盘分区。

>[!CAUTION]
>
>如果ImageMagick使用所有可用磁盘空间，则错误配置可能会使服务器不稳定。 使用ImageMagick处理大型文件所需的策略更改可能会影响 [!DNLEExperience Manager] 性能。 有关详细信息，请参 [阅安装和配置ImageMagick](/help/assets/best-practices-for-imagemagick.md)。

>[!NOTE]
>
>ImageMagick和 `policy.xml` 文件 `configure.xml` 可从中获取， `/usr/lib64/ImageMagick-&#42;/config/` 而不 `/etc/ImageMagick/`是。有关配置文 [件的位置，请](https://www.imagemagick.org/script/resources.php) 参阅ImageMagick文档。

如果您使 [!DNL Experience Manager] 用的是Adobe Managed Services(AMS)，如果您计划处理大量大型PSD或PSB文件，请联系Adobe客户服务中心。 与Adobe客户关怀代表合作，为您的AMS部署实施这些最佳实践，并为Adobe的专有格式选择尽可能最好的工具和模型。 [!DNL Experience Manager] 可能无法处理超过30000 x 23000像素的高分辨率PSB文件。

### XMP writeback {#xmp-writeback}

XMP writeback在中修改元数据时会更新原始 [!DNL Experience Manager]资产，这会导致：

* 资产本身已修改
* 此时会创建资产的某个版本
* [!UICONTROL DAM更新资产] ，会针对资产运行

所列结果消耗了大量资源。 因此，Adobe建 [议禁用XMP写回](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)（如果不需要）。

如果选中了运行工作流标志，导入大量元数据可能会导致资源密集型的XMP写回活动。 在精益服务器使用期间计划此类导入，以便不影响其他用户的性能。

## 复制 {#replication}

当将资产复制到大量发布实例（例如，在站点实施中）时，Adobe建议您使用链复制。 在这种情况下，作者实例复制到单个发布实例，而该实例又复制到其他发布实例，从而释放了作者实例。

### 配置链复制 {#configure-chain-replication}

1. 选择要将复制链接到的发布实例
1. 在该发布实例上添加指向其他发布实例的复制代理
1. 在这些复制代理中，在“触发器”选项卡上启用“接收时”

>[!NOTE]
>
>Adobe不建议自动激活资产。 但是，如果需要，Adobe建议将此操作作为工作流的最后一步，通常是DAM更新资产。

## 搜索索引 {#search-indexes}

请确保实施最新的Service Pack和与性能相关的修补程序，因为它们通常包含对系统索引的更新。 请参 [阅某些索引优化](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) 的性能调整提示。

为经常运行的查询创建自定义索引。 有关详细信息，请参 [阅分析慢速查询和制作自定](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 义索 [引的方法](/help/sites-deploying/queries-and-indexing.md)。 有关查询和索引最佳实践的更多见解，请参 [阅查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### Lucene索引配置 {#lucene-index-configurations}

对Oak索引配置可进行一些优化，以帮助提高 [!DNL Experience Manager Assets] 性能。 更新索引配置以缩短重新索引的时间：

1. 打开CRXDe `/crx/de/index.jsp` 并以管理用户身份登录。
1. 浏览至 `/oak:index/lucene`。
1. 添加具 `String[]` 有 `excludedPaths` 值、 `/var`和的 `/etc/workflow/instances`属性 `/etc/replication`。
1. 浏览至 `/oak:index/damAssetLucene`。 添加具 `String[]` 有值 `includedPaths` 的属性 `/content/dam`。 保存更改。

如果您的用户不需要对资产进行全文搜索(例如，在PDF文档中搜索文本)，请禁用它。 通过禁用全文索引，可提高索引性能。 要禁用文 [!DNL Apache Lucene] 本提取，请执行以下步骤：

1. 在界 [!DNL Experience Manager] 面中，访问 [!UICONTROL 包管理器]。
1. 上传并安装可从 [disable_indexingbinarytexttraction-10.zip获得的包](assets/disable_indexingbinarytextextraction-10.zip)。

### 猜测总数 {#guess-total}

创建生成大结果集的查询时，请使 `guessTotal` 用该参数以避免在运行它们时占用大量内存。

## 已知问题 {#known-issues}

### 大文件 {#large-files}

中有两个与大文件相关的主要已知问题 [!DNL Experience Manager]。 当文件大小超过2 GB时，冷待机同步可能会出现内存不足的情况。 在某些情况下，它会阻止待机同步运行。 在其他情况下，它会导致主实例崩溃。 此方案适用于大于2GB [!DNL Experience Manager] 的任何文件，包括内容包。

同样，当使用共享S3数据存储时文件大小达到2 GB时，可能需要一些时间才能将文件从缓存完全保留到文件系统。 因此，在使用无二进制复制时，可能在复制完成之前没有保留二进制数据。 这种情况可能导致问题，特别是当数据的可用性很重要时。

## 性能测试 {#performance-testing}

对于每 [!DNL Experience Manager] 个部署，建立一个性能测试机制，快速发现并解决瓶颈。 以下是需要关注的一些关键领域。

### 网络测试 {#network-testing}

对于客户提出的所有网络性能问题，请执行以下任务:

* 从客户网络内测试网络性能
* 从Adobe网络中测试网络性能。 对于AMS客户，请与CSE协作，在Adobe网络中进行测试。
* 从另一个接入点测试网络性能
* 使用网络基准工具
* 针对调度程序进行测试

### [!DNL Experience Manager] 部署测试 {#aem-deployment-testing}

要通过高效的CPU利用率和负载共享将延迟降至最低并实现高吞吐量，请定期监控部署 [!DNL Experience Manager] 的性能。 特别是：

* 对部署运行负载 [!DNL Experience Manager] 测试。
* 监控上传性能和UI响应。

## [!DNL Experience Manager Assets] 绩效清单和资产管理任务 {#checklist}

* 使HTTPS能够绕过任何企业HTTP流量侦听器。
* 使用有线连接上传大量资产。
* 在Java 8上部署。
* 设置最佳JVM参数。
* 配置文件系统数据存储或S3数据存储。
* 禁用子资产生成。 如果启用此功能，AEM工作流会为多页资产中的每个页面创建单独的资产。 这些页中的每个页都是一个单独的资产，它占用额外的磁盘空间，需要版本控制，以及额外的工作流处理。 如果不需要单独的页面，请禁用子资产生成和页面提取活动。
* 启用临时工作流。
* 调整Granite工作流队列以限制并发作业。
* 配置 [!DNL ImageMagick] 以限制资源消耗。
* 从DAM更新资产工作流 [!UICONTROL 中删除不必要的步] 骤。
* 配置工作流和版本清除。
* 使用最新的服务包和修补程序优化索引。 请咨询Adobe客户关怀部门，了解是否有其他可用的索引优化。
* 使用guessTotal优化查询性能。
* If you configure [!DNL Experience Manager] to detect file types from the content of the files (by enabling **[!UICONTROL Day CQ DAM Mime Type Service]** in the **[!UICONTROL AEM Web Console]**), upload many files in bulk during non-peak hours as it is resource-intensive.
