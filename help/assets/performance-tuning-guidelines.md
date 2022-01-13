---
title: 性能调整 [!DNL Assets].
description: 关于 [!DNL Experience Manager] 配置、对硬件、软件和网络组件的更改，以消除瓶颈并优化 [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '2741'
ht-degree: 0%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 性能优化指南 {#assets-performance-tuning-guide}

安 [!DNL Experience Manager Assets] 安装程序包含许多硬件、软件和网络组件。 根据您的部署方案，您可能需要对硬件、软件和网络组件进行特定配置更改，以消除性能瓶颈。

此外，确定并遵守某些硬件和软件优化准则有助于建立良好的基础，使您的 [!DNL Experience Manager Assets] 部署以满足对性能、可扩展性和可靠性的期望。

在 [!DNL Experience Manager Assets] 会影响用户在交互式性能、资产处理、下载速度等方面的体验。

事实上，性能优化是您在为任何项目建立目标量度之前执行的一项基本任务。

以下是一些关键焦点区域，您可以围绕这些区域发现并修复性能问题，然后才能对用户产生影响。

## 平台 {#platform}

虽然Experience Manager在许多平台上受支持，但Adobe在Linux和Windows上发现对本机工具的最大支持，这有助于获得最佳性能并简化实施。 理想情况下，您应部署64位操作系统，以满足 [!DNL Experience Manager Assets] 部署。 与任何Experience Manager部署一样，您应尽可能实施TarMK。 虽然TarMK无法扩展到单个创作实例之外，但发现它的性能优于MongoMK。 您可以添加TarMK卸载实例，以提高您的 [!DNL Experience Manager Assets] 部署。

### 临时文件夹 {#temp-folder}

要缩短资产上传时间，请对Java临时目录使用高性能存储。 在Linux和Windows上，可使用RAM驱动器或SSD。 在基于云的环境中，可以使用等效的高速存储类型。 例如，在Amazon EC2中， [短暂驱动](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) 驱动器可用于临时文件夹。

假设服务器有充足的内存，请配置RAM驱动器。 在Linux上，运行以下命令以创建一个8 GB RAM驱动器：

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

在Windows操作系统上，使用第三方驱动程序创建RAM驱动器或仅使用高性能存储（如SSD）。

高性能临时卷准备就绪后，设置JVM参数 `-Djava.io.tmpdir`. 例如，您可以将下面的JVM参数添加到 `CQ_JVM_OPTS` 变量 `bin/start` 脚本 [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java配置 {#java-configuration}

### Java版本 {#java-version}

Adobe建议部署 [!DNL Experience Manager Assets] 在Java 8上优化性能。

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

建议所有 [!DNL Experience Manager Assets] 用户。 此外，配置 `maxCachedBinarySize` 和 `cacheSizeInMB` 参数有助于最大限度地提高性能。 已设置 `maxCachedBinarySize` 到可保存在缓存中的最小文件大小。 指定用于内存中数据存储的内存内缓存大小 `cacheSizeInMB`. Adobe建议将此值设置为堆总大小的2-10%之间。 但是，负载/性能测试有助于确定理想的设置。

### 配置缓冲的图像缓存的最大大小 {#configure-the-maximum-size-of-the-buffered-image-cache}

在将大量资产上传到 [!DNL Adobe Experience Manager]，为了允许内存消耗出现意外峰值并防止JVM在出现OutOfMemoryErrors时失败，请减小已缓冲图像缓存的已配置最大大小。 假设您的系统具有最大堆(- `Xmx`参数),5 GB为Oak BlobCache，1 GB为文档缓存，2 GB为文档缓存。 在这种情况下，缓冲的缓存将最大占用1.25 GB和内存，这将仅保留0.75 GB的内存，以备出现意外峰值。

在OSGi Web控制台中配置缓冲的缓存大小。 At `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`，请设置属性 `cq.dam.image.cache.max.memory` 字节。 例如，1073741824为1 GB(1024 x 1024 x 1024 = 1 GB)。

从Experience Manager6.1 SP1开始，如果您使用 `sling:osgiConfig` 用于配置此属性的节点，请确保将数据类型设置为Long。 有关更多详细信息，请参阅 [CQBufferedImageCache在资产上传期间会消耗堆](https://helpx.adobe.com/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### 共享数据存储 {#shared-data-stores}

实施S3或共享文件数据存储有助于在大规模实施中节省磁盘空间并提高网络吞吐量。 有关使用共享数据存储的利弊的更多信息，请参阅 [资产大小调整指南](/help/assets/assets-sizing-guide.md).

### S3数据存储 {#s-data-store}

以下S3数据存储配置( `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`)帮助Adobe将12.8 TB的二进制大对象(BLOB)从现有文件数据存储区提取到客户站点的S3数据存储区：

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

Adobe建议启用HTTPS，因为许多公司都有可嗅探HTTP流量的防火墙，这会对上传和损坏文件造成不利影响。 对于大文件上传，请确保用户已通过有线连接连接到网络，因为WiFi网络会迅速饱和。 有关确定网络瓶颈的准则，请参阅 [资产大小调整指南](/help/assets/assets-sizing-guide.md). 要通过分析网络拓扑来评估网络性能，请参阅 [资产网络注意事项](/help/assets/assets-network-considerations.md).

网络优化策略主要取决于可用带宽的数量和您的 [!DNL Experience Manager] 实例。 常用配置选项（包括防火墙或代理）可帮助提高网络性能。 请牢记以下要点：

* 根据您的实例类型（小、中、大），确保您的Experience Manager实例有足够的网络带宽。 如果 [!DNL Experience Manager] 托管在AWS上。
* 如果 [!DNL Experience Manager] 实例托管在AWS上，通过使用通用的缩放策略，您将受益。 如果用户期望获得高负载，请更新实例的大小。 为适中/低负载减小其大小。
* HTTPS:大多数用户具有可嗅探HTTP流量的防火墙，这可能会对上传操作期间文件的上传甚至文件损坏产生不利影响。
* 大文件上传：确保用户有与网络的有线连接（WiFi连接快速饱和）。

## 工作流 {#workflows}

### 瞬态工作流 {#transient-workflows}

尽可能将 [!UICONTROL DAM更新资产] 工作流到临时。 该设置可显着减少处理工作流所需的开销，因为在这种情况下，工作流不需要通过常规的跟踪和存档流程。

1. 导航到 `/miscadmin` 在 [!DNL Experience Manager] 部署 `https://[aem_server]:[port]/miscadmin`.

1. 展开 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]** > **[!UICONTROL dam]**.

1. 打开 **[!UICONTROL DAM更新资产]**. 从浮动工具面板，切换到 **[!UICONTROL 页面]** ，然后单击 **[!UICONTROL 页面属性]**.

1. 选择 **[!UICONTROL 瞬态工作流]** 单击 **[!UICONTROL 确定]**.

   >[!NOTE]
   >
   >某些功能不支持临时工作流。 如果 [!DNL Assets] 部署需要这些功能，请勿配置临时工作流。

如果不能使用临时工作流，请定期运行工作流清除以删除已存档的工作流 [!UICONTROL DAM更新资产] 工作流，以确保系统性能不会下降。

通常，每周执行清除工作流。 但是，在资源密集型场景（例如在大规模资产摄取期间）中，您可以更频繁地执行该操作。

要配置工作流清除，请通过OSGi控制台添加新的AdobeGranite工作流清除配置。 接下来，在每周维护窗口中配置并计划工作流。

如果清除运行过长，则会超时。 因此，您应确保清除作业已完成，以避免由于工作流数量过多而无法完成清除工作流的情况。

例如，在执行大量非瞬态工作流（创建工作流实例节点）后，您可以执行 [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) 临时分析。 它会立即删除冗余的已完成工作流实例，而不是等待AdobeGranite工作流清除计划程序运行。

### 最大并行作业数 {#maximum-parallel-jobs}

默认情况下， [!DNL Experience Manager] 运行与服务器上处理器数量相等的最大并行作业数。 此设置的问题在于，在负载过重时，所有处理器都被 [!UICONTROL DAM更新资产] 工作流，减慢UI响应速度并防止 [!DNL Experience Manager] 运行其他可保护服务器性能和稳定性的进程。 最好通过执行以下步骤将此值设置为服务器上可用处理器的一半：

1. 开 [!DNL Experience Manager] 创作，访问 `https://[aem_server]:[port]/system/console/slingevent`.

1. 单击 **[!UICONTROL 编辑]** （例如，在与您的实施相关的每个工作流队列上） **[!UICONTROL Granite Transient工作流队列]**.

1. 更新的值 **[!UICONTROL 最大并行作业数]** 单击 **[!UICONTROL 保存]**.

将队列设置到一半的可用处理器是一个可行的解决方案。 但是，您可能必须增加或减少此数量，才能实现最大吞吐量，并按环境进行调整。 临时工作流和非临时工作流以及其他进程（如外部工作流）有单独的队列。 如果多个队列设置为50%的处理器同时处于活动状态，则系统可以快速过载。 大量使用的队列在各个用户实施中有很大差异。 因此，您可能必须仔细配置它们以实现最高效率，而不牺牲服务器稳定性。

### DAM更新资产配置 {#dam-update-asset-configuration}

的 [!UICONTROL DAM更新资产] 工作流包含为任务(如Dynamic Media PTIFF生成和)配置的完整步骤 [!DNL Adobe InDesign Server] 集成。 但是，大多数用户可能不需要执行其中的几个步骤。 Adobe建议您创建 [!UICONTROL DAM更新资产] 工作流模型，并删除任何不必要的步骤。 在这种情况下，请更新 [!UICONTROL DAM更新资产] 指向新模型。

运行 [!UICONTROL DAM更新资产] 工作流会集中地大幅增加文件数据存储的大小。 通过Adobe进行的实验结果表明，如果在8小时内执行大约5500个工作流，则数据存储大小可以增加大约400 GB。

这是临时增加，在您运行数据存储垃圾收集任务后，数据存储将恢复到其原始大小。

通常，数据存储垃圾收集任务与其他计划维护任务一起每周运行。

如果磁盘空间有限，则运行 [!UICONTROL DAM更新资产] 工作流集中，考虑更频繁地调度垃圾收集任务。

#### 运行时呈现版本生成 {#runtime-rendition-generation}

客户在其网站中使用各种大小和格式的图像，或将其分发给业务合作伙伴。 由于每个演绎版都会增加资产在存储库中的占用空间，因此Adobe建议谨慎使用此功能。 为了减少处理和存储图像所需的资源量，您可以在运行时生成这些图像，而不是在摄取期间作为演绎版生成这些图像。

许多Sites客户实施了一个图像Servlet，在请求时调整图像大小并裁剪图像，这会对发布实例造成额外负载。 但是，只要可以缓存这些图像，挑战就可以缓解。

另一种方法是使用Dynamic Media技术完全切换图像处理。 此外，您还可以部署Brand Portal，它不仅负责 [!DNL Experience Manager] 基础架构，以及整个发布层。

#### ImageMagick {#imagemagick}

如果您自定义 [!UICONTROL DAM更新资产] 使用ImageMagick生成演绎版的工作流，Adobe建议您修改 `policy.xml` 文件位置 `/etc/ImageMagick/`. 默认情况下， ImageMagick使用操作系统卷上的整个可用磁盘空间和可用内存。 在 `policymap` 部分 `policy.xml` 来限制这些资源。

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

此外，在 `configure.xml` 文件(或通过设置环境变量 `MAGIC_TEMPORARY_PATH`)到具有足够空间和IOPS的磁盘分区。

>[!CAUTION]
>
>如果ImageMagick使用所有可用磁盘空间，则配置不当可能会使服务器不稳定。 使用ImageMagick处理大型文件所需的策略更改可能会影响 [!DNL Experience Manager] 性能。 有关更多信息，请参阅 [安装和配置ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` 和 `configure.xml` 文件可在 `/usr/lib64/ImageMagick-&#42;/config/` 而不是 `/etc/ImageMagick/`.请参阅 [ImageMagick文档](https://www.imagemagick.org/script/resources.php) ，以了解配置文件的位置。

如果您使用 [!DNL Experience Manager] 在Adobe Managed Services(AMS)上，如果您计划处理大量大型PSD或PSB文件，请联系Adobe客户支持。 与Adobe客户支持代表合作，为您的AMS部署实施这些最佳实践，并为Adobe的专有格式选择尽可能最好的工具和模型。 [!DNL Experience Manager] 可能无法处理超过30000 x 23000像素的高分辨率PSB文件。

### XMP写回 {#xmp-writeback}

XMP写回会在 [!DNL Experience Manager]，这会导致以下结果：

* 资产本身已修改
* 此时会创建资产的版本
* [!UICONTROL DAM更新资产] 针对资产运行

所列结果消耗了大量资源。 因此，Adobe建议 [禁用XMP写回](https://helpx.adobe.com/experience-manager/kb/disable-xmp-writeback.html)，如果不需要。

如果选中了运行工作流标志，则导入大量元数据可能会导致资源密集型XMP写回活动。 在精益服务器使用期间规划此类导入，以便不影响其他用户的性能。

## 复制 {#replication}

在将资产复制到大量发布实例（例如在Sites实施中）时，Adobe建议您使用链复制。 在这种情况下，创作实例会复制到单个发布实例，而该实例又会复制到其他发布实例，从而释放创作实例。

### 配置链复制 {#configure-chain-replication}

1. 选择要将复制链接到的发布实例
1. 在该发布实例上，添加指向其他发布实例的复制代理
1. 在每个复制代理上，在“触发器”选项卡上启用“接收时”

>[!NOTE]
>
>Adobe不建议自动激活资产。 但是，如果需要，Adobe建议将此操作作为工作流的最后一步，通常是DAM更新资产。

## 搜索索引 {#search-indexes}

安装 [最新的Service Pack](/help/release-notes/release-notes.md) 和与性能相关的修补程序，因为这些修补程序通常包括对系统索引的更新。 请参阅 [性能调整提示](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) ，用于某些索引优化。

为经常运行的查询创建自定义索引。 有关详细信息，请参阅 [分析慢速查询的方法](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) 和 [编制自定义索引](/help/sites-deploying/queries-and-indexing.md). 有关查询和索引最佳实践的其他分析，请参阅 [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene索引配置 {#lucene-index-configurations}

可以对Oak索引配置进行一些优化，以帮助改进 [!DNL Experience Manager Assets] 性能。 更新索引配置以缩短重新索引的时间：

1. 打开CRXDe `/crx/de/index.jsp` 并以管理用户身份登录。
1. 浏览到 `/oak:index/lucene`.
1. 添加 `String[]` 属性 `excludedPaths` 带值 `/var`, `/etc/workflow/instances`和 `/etc/replication`.
1. 浏览到 `/oak:index/damAssetLucene`. 添加 `String[]` 属性 `includedPaths` 具有值 `/content/dam`. 保存更改。

如果您的用户不需要对资产进行全文搜索，例如，在PDF文档中通过文本进行搜索，则会禁用该功能。 您可以通过禁用全文索引来提高索引性能。 禁用 [!DNL Apache Lucene] 文本提取，请执行以下步骤：

1. 在 [!DNL Experience Manager] 界面，访问 [!UICONTROL 包管理器].
1. 上载并安装包(位于 [disable_indexingbinarytexttraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### 猜测总计 {#guess-total}

创建生成大结果集的查询时，请使用 `guessTotal` 参数，以避免在运行时内存占用过大。

## 已知问题 {#known-issues}

### 大文件 {#large-files}

在 [!DNL Experience Manager]. 当文件大小超过2 GB时，冷备用同步可能会出现内存不足的情况。 在某些情况下，它会阻止备用同步运行。 在其他情况下，它会导致主实例崩溃。 此方案适用于 [!DNL Experience Manager] 大于2 GB，包括内容包。

同样，当文件在使用共享的S3数据存储时达到2 GB大小时，文件从缓存完全保留到文件系统可能需要一些时间。 因此，在使用无二进制复制时，可能在复制完成之前没有保留二进制数据。 这种情况可能会导致问题，特别是在数据可用性很重要的情况下。

## 性能测试 {#performance-testing}

每 [!DNL Experience Manager] 部署、建立性能测试机制，以便快速发现和解决瓶颈。 以下是需要重点关注的一些关键方面。

### 网络测试 {#network-testing}

对于客户涉及的所有网络性能问题，请执行以下任务：

* 从客户网络内部测试网络性能
* 从Adobe网络内测试网络性能。 对于AMS客户，请与您的CSE一起从Adobe网络内进行测试。
* 从另一个接入点测试网络性能
* 使用网络基准工具
* 针对调度程序进行测试

### [!DNL Experience Manager] 部署测试 {#aem-deployment-testing}

为了通过高效的CPU利用率和负载共享来最大限度地减少延迟并实现高吞吐量，请监控您的 [!DNL Experience Manager] 定期部署。 特别是：

* 针对 [!DNL Experience Manager] 部署。
* 监控上传性能和UI响应性。

## [!DNL Experience Manager Assets] 资产管理任务的性能清单和影响 {#checklist}

* 启用HTTPS以绕过任何公司HTTP流量探查器。
* 使用有线连接上传大量资产。
* 在Java 8上部署。
* 设置最佳JVM参数。
* 配置文件系统数据存储或S3数据存储。
* 禁用子资产生成。 如果启用了该功能，AEM工作流会为多页面资产中的每个页面创建一个单独的资产。 其中每个页面都是单个资产，会占用额外的磁盘空间，需要进行版本控制，以及进行额外的工作流处理。 如果不需要单独的页面，请禁用子资产生成和页面提取活动。
* 启用临时工作流。
* 调整Granite工作流队列以限制并发作业。
* 配置 [!DNL ImageMagick] 以限制资源消耗。
* 从 [!UICONTROL DAM更新资产] 工作流。
* 配置工作流和版本清除。
* 使用最新的Service Pack和修补程序优化索引。 请咨询Adobe客户支持，以了解可能提供的任何其他索引优化。
* 使用guessTotal优化查询性能。
* 如果配置 [!DNL Experience Manager] 从文件内容中检测文件类型(通过启用 **[!UICONTROL Day CQ DAM Mime类型服务]** 在 **[!UICONTROL AEM Web Console]**)，则在非高峰时间批量上传许多文件，因为它占用大量资源。
