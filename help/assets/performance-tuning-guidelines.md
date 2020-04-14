---
title: 资产性能调整指南
description: 有关AEM配置、硬件、软件和网络组件更改以消除瓶颈和优化AEM资产性能的建议和指导。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


<!-- TBD: Formatting using backticks. Add UICONTROL tag. Redundant info as reviewed by engineering. -->

# 资产性能调整指南 {#assets-performance-tuning-guide}

Adobe Experience Manager(AEM)资产设置包含许多硬件、软件和网络组件。 根据部署方案，您可能需要对硬件、软件和网络组件进行特定配置更改以消除性能瓶颈。

此外，确定并遵守特定硬件和软件优化指南有助于建立可靠的基础，使您的AEM资产部署能够满足性能、可伸缩性和可靠性方面的期望。

AEM资产性能不佳可能会影响用户在交互性能、资产处理、下载速度等方面的体验。

事实上，性能优化是您在为任何项目建立任务指标之前执行的基本目标。

以下是某些关键重点领域，您可以围绕这些领域发现和修复性能问题，然后才会对用户产生影响。

## 平台 {#platform}

虽然AEM在许多平台上受支持，但Adobe在Linux和Windows上发现对本机工具的最大支持，这有助于实现最佳性能并简化实施。 理想情况下，您应部署64位操作系统以满足AEM资产部署的高内存要求。 与任何AEM部署一样，您应尽可能实施TarMK。 虽然TarMK无法扩展到单个作者实例之外，但发现它的性能比MongoMK好。 您可以添加TarMK卸载实例，以提高AEM资产部署的工作流处理能力。

### 临时文件夹 {#temp-folder}

要缩短资产上传时间，请对Java临时目录使用高性能存储。 在Linux和Windows上，可以使用RAM驱动器或SSD。 在基于云的环境中，可以使用等效的高速存储类型。 例如，在Amazon EC2中， [“短暂的驱动器”](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) “驱动器”可用于临时文件夹。

假定服务器具有足够的内存，请配置RAM驱动器。 在Linux上，运行以下命令以创建一个8 GB内存驱动器：

```
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows操作系统上，使用第三方驱动程序创建RAM驱动器或仅使用高性能存储（如SSD）。

高性能临时卷准备就绪后，请设置JVM参数 `-Djava.io.tmpdir`。 例如，您可以将以下JVM参数添加到AEM `CQ_JVM_OPTS` 脚本中 `bin/start` 的变量：

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置 {#java-configuration}

### Java版本 {#java-version}

Adobe建议在Java 8上部署AEM资产以获得最佳性能。

>[!NOTE]
>
>Oracle从2015年4月起停止发布Java 7的更新。

### JVM参数 {#jvm-parameters}

应设置以下JVM参数：

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## 数据存储和内存配置 {#data-store-and-memory-configuration}

### 文件数据存储配置 {#file-data-store-configuration}

建议所有AEM资产用户将数据存储与区段存储分离。 此外，配置和参 `maxCachedBinarySize` 数可 `cacheSizeInMB` 帮助最大化性能。 设 `maxCachedBinarySize` 置为可保存在缓存中的最小文件大小。 指定内存中缓存的大小，以用于中的数据存储 `cacheSizeInMB`。 Adobe建议您将此值设置为总堆大小的2-10%之间。 但是，负载／性能测试有助于确定理想的设置。

### 配置缓冲的图像缓存的最大大小 {#configure-the-maximum-size-of-the-buffered-image-cache}

在将大量资产上传到Adobe Experience Manager时，为了允许意外的内存消耗高峰，并防止JVM在OutOfMemoryErrors中失败，请减小已缓冲映像缓存的已配置最大大小。 例如，您有一个系统，其最大堆(- `Xmx`param)为5 GB,Oak BlobCache设置为1 GB,文档缓存设置为2 GB。 在这种情况下，缓冲的缓存将最大需要1.25 GB内存，这将仅为意外尖峰保留0.75 GB内存。

在OSGi Web控制台中配置缓冲的缓存大小。 在 `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，设置属性(以字 `cq.dam.image.cache.max.memory` 节为单位)。 例如，1073741824为1 GB(1024 x 1024 x 1024 = 1 GB)。

从AEM 6.1 SP1中，如果您使用节点来配 `sling:osgiConfig` 置此属性，请确保将数据类型设置为“长”。 有关详细信息，请参 [阅CQBufferedImageCache在资产上传期间消耗堆](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)。

### 共享数据存储 {#shared-data-stores}

实施S3或共享文件数据存储有助于在大规模实施中节省磁盘空间和增加网络吞吐量。 有关使用共享数据存储的利弊的详细信息，请参阅资产 [大小调整指南](/help/assets/assets-sizing-guide.md)。

### S3 data store {#s-data-store}

以下S3数据存储配置( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)帮助Adobe从现有文件数据存储中提取12.8 TB的二进制大对象(BLOB)到客户站点的S3数据存储中：

```
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

Adobe建议启用HTTPS，因为许多公司都有防火墙来监听HTTP通信，这会对上传和损坏文件产生不利影响。 对于大型文件上传，请确保用户已有连接到网络的有线连接，因为WiFi网络会迅速饱和。 有关确定网络瓶颈的准则，请参阅资产 [规模调整指南](/help/assets/assets-sizing-guide.md)。 要通过分析网络拓扑来评估网络性能，请参 [阅资产网络注意事项](/help/assets/assets-network-considerations.md)。

主要是，您的网络优化策略取决于可用带宽的数量和AEM实例的负载。 包括防火墙或代理在内的常见配置选项有助于提高网络性能。 以下是需要牢记的关键点：

* 根据您的实例类型（小、中、大），确保您的AEM实例具有足够的网络带宽。 如果AEM托管在AWS上，则适当的带宽分配尤为重要。
* 如果您的AEM实例托管在AWS上，您可以通过使用通用型扩展策略受益。 如果用户期望高负载，请升级实例。 对其进行缩小以适中／低负载。
* HTTPS:大多数用户都有防火墙来监听HTTP通信，这可能会对上传操作期间文件的上传甚至损坏文件产生不利影响。
* 大文件上传：确保用户有有线网络连接到网络（WiFi连接快速饱和）。

## 工作流 {#workflows}

### 临时工作流 {#transient-workflows}

尽可能将“ [!UICONTROL DAM更新资产”工作流设置为] “临时”。 该设置显着减少了处理工作流所需的开销，因为在这种情况下，工作流无需通过正常的跟踪和存档过程。

>[!NOTE]
>
>在AEM 6.3中，默认情况下， [!UICONTROL DAM更新资产工作流程设置为] “临时”。在这种情况下，您可以跳过以下过程。

1. 导航到 `/miscadmin` 位于的AEM实例中 `https://[aem_server]:[port]/miscadmin`。
1. 展开“ **[!UICONTROL 工具]** ”>“工 **[!UICONTROL 作流]** ” **[!UICONTROL >“模]** 型” **[!UICONTROL >“dam]**”。
1. 打开 **[!UICONTROL DAM更新资产]**。 从浮动工具面板中，切换到“页 **[!UICONTROL 面]** ”选项卡，然后单击“页 **[!UICONTROL 面属性”]**。
1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >某些功能不支持临时工作流。 如果您的AEM资产部署需要这些功能，请勿配置临时工作流。

如果无法使用临时工作流，请定期运行工作流清除以删除存档的  DAM更新资产工作流，以确保系统性能不会降低。

通常，每周执行清除工作流。 但是，在资源密集型场景中（例如在大规模资产摄取期间），您可以更频繁地执行它。

要配置工作流清除，请通过OSGi控制台添加新的Adobe Granite工作流清除配置。 接下来，在每周维护窗口中配置和计划工作流。

如果清除时间过长，就会超时。 因此，您应确保清除作业完成，以避免由于工作流数量过多而无法完成清除工作流的情况。

例如，在执行大量非临时工作流（创建工作流实例节点）后，您可以在临时基础上运行 [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 。 它会立即删除冗余的已完成工作流实例，而不是等待Adobe Granite Workflow Purge调度程序运行。

### 最大并行作业数 {#maximum-parallel-jobs}

默认情况下，AEM运行的最大并行作业数等于服务器上的处理器数。 此设置的问题是，在负载较重的期间，所有处理器都被  DAM更新资产工作流占用，这会降低UI响应速度并阻止AEM运行其他可保护服务器性能和稳定性的进程。 作为最佳实践，请通过执行以下步骤将此值设置为服务器上可用处理器的一半：

1. 在AEM作者上，转到 `https://[aem_server]:[port]/system/console/slingevent`。
1. 单击 **[!UICONTROL 与您的实施相关的每个工作流队列上的“编辑]** ”(Edit **[!UICONTROL )，例如]** Granite临时工作流队列。
1. 更新“最大并行作 **[!UICONTROL 业数”的值]** ，然后单击“ **[!UICONTROL 保存”]**。

将队列设置到一半的可用处理器是与之开始的可行解决方案。 但是，您可能必须增加或减少此数量才能实现最大吞吐量并按环境调整它。 对于瞬态和非瞬态工作流以及诸如外部工作流等其他过程，存在单独的队列。 如果将多个队列设置为50%的处理器同时处于活动状态，则系统可以快速过载。 大量使用的队列在用户实现中差别很大。 因此，您可能必须仔细配置它们以获得最高效率，同时不牺牲服务器稳定性。

### DAM更新资产配置 {#dam-update-asset-configuration}

 DAM更新资产工作流包含为任务配置的全套步骤，如Scene7 PTIFF生成和InDesign Server集成。 但是，大多数用户可能不需要执行以下几个步骤。 Adobe建议您创建 [!UICONTROL DAM更新资产工作流模型的自定义副本] ，并删除任何不必要的步骤。 在这种情况下，请更新 [!UICONTROL DAM更新资产的启动程序] ，以指向新模型。

集中运 [!UICONTROL 行DAM更新资产工作流] ，可以大幅增加文件数据存储的大小。 Adobe进行的试验结果表明，如果在8小时内执行约5500次工作流，则数据存储大小可以增加约400 GB。

这是临时增加，在您运行数据存储垃圾收集任务后，数据存储将恢复为其原始大小。

通常，数据存储垃圾收集任务与其他计划维护任务一起每周运行。

如果您的磁盘空间有限，并集中运行 [!UICONTROL DAM更新资产工作流] ，请考虑更频繁地安排垃圾收集任务。

#### 运行时再现生成 {#runtime-rendition-generation}

客户在其网站中使用各种大小和格式的图像，或分发给业务合作伙伴。 由于每个再现都会添加到存储库中资产的占用空间，因此Adobe建议谨慎地使用此功能。 要减少处理和存储图像所需的资源量，您可以在运行时生成这些图像，而不是在摄取期间作为再现。

许多站点客户实现了一个图像Servlet，它在请求图像时调整图像大小和裁切图像，这会给发布实例带来额外的负载。 但是，只要可以缓存这些图像，挑战就可以缓解。

另一种方法是使用Scene7技术完全移交图像处理。 此外，您还可以部署Brand Portal，它不仅从AEM基础结构接管再现生成责任，而且接管整个发布层。

#### ImageMagick {#imagemagick}

如果您自定义 [!UICONTROL DAM更新资产工作流以使用ImageMagick生成再现] ，则Adobe建议您在上修改 `policy.xml` 该文件 `/etc/ImageMagick/`。 默认情况下，ImageMagick使用操作系统卷上的整个可用磁盘空间和可用内存。 在的部分中进行以下配置更 `policymap` 改以 `policy.xml` 限制这些资源。

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

此外，将文件中ImageMagick的临时文件夹的路径(或通过设置环境变量 `configure.xml``MAGIC_TEMPORARY_PATH`)设置为具有足够空间和IOPS的磁盘分区。

>[!CAUTION]
>
>如果ImageMagick使用了所有可用磁盘空间，则错误配置可能会使服务器不稳定。
>
>使用ImageMagick处理大型文件所需的策略更改可能会影响AEM性能。 有关详细信息，请参 [阅安装和配置ImageMagick](/help/assets/best-practices-for-imagemagick.md)。

>[!NOTE]
>
>ImageMagick和 `policy.xml` 文件可 `configure.xml` 从获得，而不 `/usr/lib64/ImageMagick-&#42;/config/` 是。有关配置文件的位置，请参 `/etc/ImageMagick/`阅 [ImageMagick文档](https://www.imagemagick.org/script/resources.php) 。

>[!TIP]
>
>如果您在Adobe Managed Services(AMS)上使用Experience Manager，则如果您计划处理大量大型PSD或PSB文件，请联系Adobe支持部门。 与Adobe客户关怀代表合作，为您的AMS部署实施这些最佳实践，并为Adobe专有格式选择最佳的工具和模型。

### XMP writeback {#xmp-writeback}

每当在AEM中修改元数据时，XMP写回会更新原始资产，这会导致以下情况：

* 资产本身已修改
* 此时会创建资产的某个版本
* [!UICONTROL DAM更新资产] ，会针对资产运行

所列成果消耗了大量资源。 因此，如果不 [需要XMP写回](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html),Adobe建议禁用它。

如果选中了运行工作流标志，导入大量元数据可能会导致资源密集型XMP写回活动。 在精简服务器使用期间计划此类导入，以便不影响其他用户的性能。

## 复制 {#replication}

在将资源复制到大量发布实例（例如，在站点实施中）时，Adobe建议您使用链复制。 在这种情况下，作者实例复制到单个发布实例，而该实例又复制到其他发布实例，从而释放了作者实例。

### 配置链复制 {#configure-chain-replication}

1. 选择要用于将复制链接到
1. 在该发布实例上，添加指向其他发布实例的复制代理
1. 在每个复制代理上，在“触发器”选项卡上启用“接收时”

>[!NOTE]
>
>Adobe不建议自动激活资产。 但是，如果需要，Adobe建议将此操作作为工作流的最后一步，通常是DAM更新资产。

## 搜索索引 {#search-indexes}

确保实施最新的服务包和与性能相关的修补程序，因为它们通常包括对系统索引的更新。 有关某些 [索引优化](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) ，请参阅性能调整提示。

为您经常运行的查询创建自定义索引。 有关详细信息，请参 [阅分析慢速查询和制作自定](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 义索 [引的方法](/help/sites-deploying/queries-and-indexing.md)。 有关查询和索引最佳实践的更多洞察，请参 [阅查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### Lucene索引配置 {#lucene-index-configurations}

可以对Oak索引配置进行一些优化，以帮助提高AEM Assets性能。 更新索引配置以缩短重新构建索引的时间：

1. 打开CRXDe `/crx/de/index.jsp` 并以管理用户身份登录
1. 浏览到 `/oak:index/lucene`
1. 添加一个String[] 属 `excludedPaths` 性， `/var`其值、 `/etc/workflow/instances`和 `/etc/replication`。
1. 浏览至 `/oak:index/damAssetLucene`。 添加带 `String[]` 值 `includedPaths` 的属性 `/content/dam`。
1. 保存.

（仅限AEM6.1和6.2）更新ntBaseLucene索引以改进资产删除和移动性能：

1. 浏览到 `/oak:index/ntBaseLucene/indexRules/nt:base/properties`
1. 添加两个nt:unstructured节点， `slingResource` 并在 `damResolvedPath` 下 `/oak:index/ntBaseLucene/indexRules/nt:base/properties`
1. 在节点上设置以下属性(其中 `ordered` 和 `propertyIndex` 属性的类型为 `Boolean`:

   ```
   slingResource
   name="sling:resource"
   ordered=false
   propertyIndex= true
   type="String"
   damResolvedPath
   name="dam:resolvedPath"
   ordered=false
   propertyIndex=true
   type="String"
   ```

1. 在节 `/oak:index/ntBaseLucene` 点上，设置属性 `reindex=true`。 单击“ **[!UICONTROL 全部保存]**”。
1. 监视error.log以查看何时完成索引：已为索引完成重新索引： [/oak:index/ntBaseLucene]
1. 您还可以看到，通过刷新CRXDe中的/oak:index/ntBaseLucene节点完成索引，因为重新索引属性将返回false
1. 完成索引后，返回CRXDe并将这两个索引上的“type”属性设置为disabled

   * */oak:index/slingResource*
   * */oak:index/damResolvedPath*

1. 单击“全部保存”

禁用Lucene文本提取:

如果用户无需搜索资产内容(例如，搜索PDF文档中包含的文本)，则可以通过禁用此功能来提高索引性能。

1. 转到AEM包管理器/crx/packmgr/index.jsp
1. 上传并安装以下包

[获取文件](assets/disable_indexingbinarytextextraction-10.zip)

### 猜测总数 {#guess-total}

创建生成大结果集的查询时，请使用该 `guessTotal` 参数以避免在运行这些结果集时占用大量内存。

## 已知问题 {#known-issues}

### 大文件 {#large-files}

在AEM中存在两个与大文件相关的主要已知问题。 当文件大小超过2 GB时，冷待机同步可能会出现内存不足的情况。 在某些情况下，它会阻止待机同步运行。 在其他情况下，它会导致主实例崩溃。 此方案适用于AEM中大于2GB的任何文件，包括内容包。

同样，当使用共享S3数据存储时，文件大小达到2 GB时，文件从缓存完全保留到文件系统可能需要一些时间。 因此，在使用无二进制复制时，可能在复制完成之前没有保留二进制数据。 这种情况可能导致问题，特别是当数据的可用性很重要时。

## 性能测试 {#performance-testing}

对于每个AEM部署，建立一个性能测试机制，以快速识别和解决瓶颈。 以下是需要重点关注的一些关键领域。

### 网络测试 {#network-testing}

对于客户关心的所有网络性能问题，请执行以下任务:

* 从客户网络中测试网络性能
* 从Adobe网络中测试网络性能。 对于AMS客户，请与CSE协作，在Adobe网络中进行测试。
* 从另一个接入点测试网络性能
* 使用网络基准工具
* 针对调度程序进行测试

### AEM实例测试 {#aem-instance-testing}

要通过高效的CPU利用率和负载共享将延迟降至最低并实现高吞吐量，请定期监控AEM实例的性能。 特别是：

* 对AEM实例运行加载测试
* 监控上传性能和UI响应性

## AEM Assets绩效核对清单和资产管理任务的影响 {#checklist}

* 使HTTPS能够绕过任何企业HTTP流量侦听器
* 使用有线连接上传大量资产
* 部署到Java 8。
* 设置最佳JVM参数
* 配置文件系统数据存储或S3数据存储
* 启用临时工作流
* 调整Granite工作流队列以限制并发作业
* 配置ImageMagick以限制资源消耗
* 从 [!UICONTROL DAM更新资产工作流中删除不必要的步骤]
* 配置工作流和版本清除
* 使用最新的服务包和修补程序优化索引。 请咨询Adobe支持部门，了解是否有其他可用的索引优化。
* 使用guessTotal优化查询性能。
* 如果将 AEM 配置为从文件内容中检测文件类型（通过在 **[!UICONTROL AEM Web Console]** 中启用 **[!UICONTROL Day CQ DAM Mime Type Service]**），则在非高峰时间会批量上传许多文件，因为它占用大量资源。
