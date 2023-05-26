---
title: Oak索引疑难解答
seo-title: Troubleshooting Oak Indexes
description: 如何检测和修复缓慢的重新索引问题。
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 1%

---

# Oak索引疑难解答{#troubleshooting-oak-indexes}

## 重新索引缓慢  {#slow-re-indexing}

AEM内部重新索引过程会收集存储库数据并将其存储在Oak索引中，以支持内容的性能查询。 在特殊情况下，这一过程可能会变得缓慢甚至停滞。 本页作为疑难解答指南，可帮助确定索引速度是否较慢、找到原因并解决问题。

区分需要花费不恰当的长时间的重新索引和需要很长的时间的重新索引很重要，因为重新索引需要大量内容的索引。 例如，为内容编制索引所需的时间会随着内容量的增加而扩展，因此大型生产存储库重新编制索引所需的时间比小型开发存储库更长。

请参阅 [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md) 有关何时以及如何重新索引内容的更多信息。

## 初始检测 {#initial-detection}

初始检测慢索引需要查看 `IndexStats` JMX MBean。 在受影响的AEM实例上，执行以下操作：

1. 打开Web控制台，然后单击JMX选项卡或转到https://&lt;host>：&lt;port>/system/console/jmx (例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))。
1. 导航到 `IndexStats` 姆比安。
1. 打开 `IndexStats` “ ”的MBean `async`“ ”和“ ” `fulltext-async`“。

1. 对于两个MBean，检查 **完成** 时间戳和 **LastIndexTime** 时间戳距当前时间不到45分钟。

1. 对于任一MBean，如果时间值(**完成** 或 **LastIndexedTime**)的时间大于当前时间的45分钟，则索引作业会失败或花费太长时间。 此问题会导致异步索引过时。

## 索引在强制关闭后暂停 {#indexing-is-paused-after-a-forced-shutdown}

强制关闭导致AEM在重新启动后暂停异步索引长达30分钟。 此外，通常还需要15分钟才能完成第一次重新索引传递，总共大约需要45分钟(链接回 [初始检测](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 时间范围（45分钟）。 如果索引在强制关闭后暂停：

1. 首先，确定AEM实例是否以强制方式关闭(AEM进程被强制终止，或发生电源故障)，然后重新启动。

   * [AEM日志记录](/help/sites-deploying/configure-logging.md) 可以针对此目的进行审查。

1. 如果强制关闭，则在重新启动时，AEM会自动暂停重新索引长达30分钟。
1. 大约等待45分钟，以便AEM恢复正常的异步索引操作。

## 线程池过载 {#thread-pool-overloaded}

>[!NOTE]
>
>对于AEM 6.1，请确保 [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans) 已安装。

在特殊情况下，用于管理异步索引的线程池可能会变得过载。 为了隔离索引过程，可以配置线程池以防止其他AEM工作干扰Oak及时索引内容的能力。 在这种情况下，请执行以下操作：

1. 为Apache Sling Scheduler定义新的独立线程池以用于异步索引：

   * 在受影响的AEM实例上，导航到AEM OSGi Web Console>OSGi>配置>Apache Sling调度程序，或转到https://&lt;host>：&lt;port>/system/console/configMgr (例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 在“允许的线程池”字段中添加一个值为“oak”的条目。
   * 要保存更改，请单击 **保存** 右下角的。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 验证新的Apache Sling计划程序线程池是否已注册，并显示在Apache Sling计划程序状态Web控制台中。

   * 导航到AEM OSGi Web控制台>“状态”>“Sling调度程序”或转到https://&lt;host>：&lt;port>/system/console/status-slingscheduler (例如， [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 验证以下池条目是否存在：

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 观察队列已满 {#observation-queue-is-full}

如果在短时间内对存储库进行了太多更改和提交，则索引可能会由于观察队列已满而延迟。 首先，确定观察队列是否已满：

1. 转到Web控制台，然后单击JMX选项卡或转到https://&lt;host>：&lt;port>/system/console/jmx (例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. 打开Oak存储库统计数据MBean并确定是否存在 `ObservationQueueMaxLength` 值大于10,000。

   * 在正常操作中，此最大值最终必须减少到零(尤其是在 `per second` 部分)，因此请验证 `ObservationQueueMaxLength`的秒数指标为0。
   * 如果值为10,000或更多，并且稳步增加，则表示至少一个（可能更多）队列的处理速度无法与新更改（提交）发生时一样快。
   * 每个观察队列都有一个限制（默认为10,000），如果队列点击了该限制，则其处理会降级。
   * 使用MongoMK时，随着队列长度增大，内部Oak缓存性能会降低。 这种相关性可以体现在增加中 `missRate` 对于 `DocChildren` 中的缓存 `Consolidated Cache` 统计数据MBean。

1. 为避免超出可接受的观察队列限制，建议执行以下操作：

   * 降低提交固定速率。 承诺量出现短峰值是可以接受的，但应降低固定比率。
   * 增加的大小 `DiffCache` 如中所述 [性能调整提示> Mongo存储调整>文档缓存大小](/help/sites-deploying/configuring-performance.md).

## 识别和修复停滞的重新索引过程 {#identifying-and-remediating-a-stuck-re-indexing-process}

在以下两种情况下，可以认为重新索引被“完全卡住”：

* 重新索引过程很慢，以至于日志文件未报告有关遍历的节点数的显着进展。

   * 例如，如果一小时内没有消息，或者进度太慢以至于需要一周或更长时间才能完成。

* 如果日志文件中出现重复的异常(例如， `OutOfMemoryException`)时，不会将反向链接计算两次。 日志中重复出现一个或多个相同的异常，表示Oak尝试重复索引相同的内容，但在同一问题上失败。

要识别和修复停滞的重新索引过程，请执行以下操作：

1. 要确定索引卡住的原因，必须收集以下信息：

   * 收集5分钟的线程转储，每2秒转储一个线程转储。
   * [为附加器设置DEBUG级别和日志](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 从异步收集数据 `IndexStats` MBean：

      * 导航至AEM OSGi Web Console>Main>JMX>IndexStat>async

         或转到 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * 使用 [oak-run.jar的控制台模式](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) 以收集下存在的内容的详细信息* `/:async`*节点。
   * 使用收集存储库检查点的列表 `CheckpointManager` MBean：

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

         或转到 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. 收集步骤1中列出的所有信息后，重新启动AEM。

   * 如果存在高并发负载（观察队列溢出或类似情况），重新启动AEM可能会解决问题。
   * 如果重启不能解决问题，请打开问题 [Adobe客户关怀](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 并提供在步骤1中收集的所有信息。

## 安全地中止异步重新索引 {#safely-aborting-asynchronous-re-indexing}

可以通过安全地中止重新索引（在完成之前停止） `async, async-reindex`和f `ulltext-async` 索引通道( `IndexStats` Mbean)。 有关更多信息，另请参阅有关的Apache Oak文档 [如何中止重新索引](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). 此外，请考虑以下事项：

* Lucene和Lucene属性索引的重新索引可以中止，因为它们是自然异步的。
* 只有通过启动重新索引，才能中止Oak属性索引的重新索引。 `PropertyIndexAsyncReindexMBean`.

要安全地中止重新索引，请执行以下步骤：

1. 确定控制必须停止的重新索引通道的IndexStats MBean。

   * 通过JMX控制台导航到相应的IndexStats MBean，方法是转到AEM OSGi Web Console>Main>JMX或https://&lt;host>：&lt;port>/system/console/jmx (例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 根据要停止的重新索引通道打开IndexStats MBean( `async`， `async-reindex`，或 `fulltext-async`)

      * 要识别适当的通道，从而识别IndexStats MBean实例，请查看Oak索引“异步”属性。 “async”属性包含通道名称： `async`， `async-reindex`，或 `fulltext-async`.
      * 通过访问“异步”列中的AEM索引管理器，还可以访问该通道。 要访问索引管理器，请导航到“操作”>“诊断”>“索引管理器”。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 调用 `abortAndPause()` 命令(位于相应的 `IndexStats` MBean。
1. 正确标记Oak索引定义，以防止在索引通道恢复时恢复重新索引。

   * 重新索引时 **现有** 索引，将reindex属性设置为false

      * `/oak:index/someExistingIndex@reindex=false`
   * 否则，对于 **新** 索引，可以：

      * 将type属性设置为禁用

         * `/oak:index/someNewIndex@type=disabled`
      * 或完全删除索引定义

   完成后，将更改提交到存储库。

1. 最后，恢复对中止索引车道上的异步索引。

   * 在 `IndexStats` 发出 `abortAndPause()` 命令，在步骤2中调用 `resume()`命令。

## 防止缓慢重新索引 {#preventing-slow-re-indexing}

最好在静默期（例如，不在大型内容提取期间）重新索引，最好在已知并控制AEM加载的维护时段重新索引。 此外，请确保在其他维护活动中不会重新编制索引。
