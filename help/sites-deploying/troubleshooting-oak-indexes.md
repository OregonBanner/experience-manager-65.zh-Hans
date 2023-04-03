---
title: Oak索引疑难解答
seo-title: Troubleshooting Oak Indexes
description: 如何检测和修复慢速重新索引。
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 2%

---

# Oak索引疑难解答{#troubleshooting-oak-indexes}

## 慢速重新索引  {#slow-re-indexing}

AEM内部重新索引过程会收集存储库数据并将其存储在Oak索引中，以支持对内容的性能查询。 在特殊情况下，该过程可能会变得缓慢甚至停滞。 本页作为疑难解答指南，可帮助确定索引速度是否慢、查找原因并解决问题。

区分需要不适当长时间的重新索引和需要很长时间的重新索引是很重要的，因为它正在索引大量的内容。 例如，索引内容所需的时间会随内容量而扩展，因此大型生产存储库重新索引的时间要比小型开发存储库花费的时间长。

请参阅 [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md) 有关何时以及如何重新索引内容的其他信息。

## 初始检测 {#initial-detection}

初始检测慢速索引需要检查 `IndexStats` JMX MBean。 在受影响的AEM实例上，执行以下操作：

1. 打开Web控制台，然后单击JMX选项卡或转到https://&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))。
1. 导航到 `IndexStats` 姆班斯。
1. 打开 `IndexStats` “”的MBean `async`&quot;和&quot; `fulltext-async`&quot;

1. 对于这两个MBean，检查 **完成** 时间戳和 **LastIndexTime** 时间戳距当前时间不到45分钟。

1. 对于任一MBean，如果时间值(**完成** 或 **LastIndexedTime**)从当前时间开始超过45分钟，则索引作业会失败或用时过长。 此问题会导致异步索引失效。

## 强制关闭后，索引暂停 {#indexing-is-paused-after-a-forced-shutdown}

强制关闭会导致AEM在重新启动后将异步索引挂起长达30分钟。 而且，通常还需要15分钟才能完成第一个重新索引传递，总共大约45分钟(与 [初始检测](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) 45分钟)。 如果在强制关闭后暂停索引：

1. 首先，确定AEM实例是否以强制方式关闭(AEM进程被强制终止，或电源故障发生)，然后重新启动。

   * [AEM日志记录](/help/sites-deploying/configure-logging.md) 可以为此目的进行审核。

1. 如果发生强制关闭，则在重新启动时，AEM会自动暂停重新索引长达30分钟。
1. 大约需要等待45分钟，AEM才能恢复正常的异步索引操作。

## 线程池重载 {#thread-pool-overloaded}

>[!NOTE]
>
>对于AEM 6.1，请确保 [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans) 已安装。

在特殊情况下，用于管理异步索引的线程池可能会变得过载。 为了隔离索引过程，可以配置线程池来防止其他AEM工作干扰Oak及时索引内容的能力。 在这种情况下，请执行以下操作：

1. 为Apache Sling调度程序定义一个用于异步索引的新的独立线程池：

   * 在受影响的AEM实例上，导航到AEM OSGi Web Console > OSGi >配置>Apache Sling调度程序或转到https://&lt;host>:&lt;port>/system/console/configMgr(例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * 在“允许的线程池”字段中添加一个值为“oak”的条目。
   * 要保存更改，请单击 **保存** 在右下方。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 确认已注册新的Apache Sling调度程序线程池，并在Apache Sling调度程序状态Web控制台中显示该线程池。

   * 导航到AEM OSGi Web控制台>状态> Sling调度程序，或转到https://&lt;host>:&lt;port>/system/console/status-slischeduler(例如， [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * 确认存在以下池条目：

      * 阿帕奇斯林戈阿克
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 观察队已满 {#observation-queue-is-full}

如果在短时间内对存储库进行了太多更改和提交，则索引可能会因完整观察队列而延迟。 首先，确定观察队列是否已满：

1. 转到Web控制台并单击JMX选项卡或转到https://&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. 打开Oak存储库统计信息MBean并确定是否有 `ObservationQueueMaxLength` 值大于10,000。

   * 在正常操作中，此最大值必须始终减小到零(尤其是在 `per second` 部分)，以验证 `ObservationQueueMaxLength`秒量度为0。
   * 如果值为10,000或更大，并且持续增加，则表示在发生新更改（提交）时，至少一个（可能更多）队列无法像快速处理一样快。
   * 每个观察队列都有一个限制（默认为10,000），如果队列达到该限制，其处理会降低。
   * 使用MongoMK时，随着队列长度增大，内部Oak缓存性能降低。 这种关联可以通过 `missRate` 对于 `DocChildren` 缓存 `Consolidated Cache` 统计信息MBean。

1. 为避免超出可接受的观察队列限制，建议执行以下操作：

   * 降低提交的恒定速率。 提交的短峰值是可以接受的，但应该降低恒定速率。
   * 增加 `DiffCache` 如 [性能调整提示> Mongo Storage Tuning >文档缓存大小](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/configuring/configuring-performance.html?lang=zh-Hans).

## 识别和修复停滞的重新索引过程 {#identifying-and-remediating-a-stuck-re-indexing-process}

在以下两种情况下，重新编制索引可以被视为“完全停滞”：

* 重新索引的速度很慢，到日志文件中没有报告有关已遍历的节点数的显着进度为止。

   * 例如，如果在一小时内没有消息，或者进度太慢，需要一周或更长时间才能完成。

* 如果日志文件中出现重复的异常，则重新索引会陷入无休止循环(例如， `OutOfMemoryException`)。 在日志中重复出现一个或多个相同的例外，表明Oak尝试重复对同一内容进行索引，但在同一问题上失败。

要识别并修复卡住的重新索引过程，请执行以下操作：

1. 要确定索引卡住的原因，必须收集以下信息：

   * 收集5分钟线程转储，每2秒收集一个线程转储。
   * [为附加器设置DEBUG级别和日志](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.asyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 从异步收集数据 `IndexStats` MBean:

      * 导航至AEM OSGi Web控制台>主>JMX > IndexStat >异步

         或转到 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * 使用 [oak-run.jar的控制台模式](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) 收集* `/:async`*节点。
   * 使用 `CheckpointManager` MBean:

      * AEM OSGi Web Console > Main>JMX >CheckpointManager >listCheckpoints()

         或转到 [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. 在收集步骤1中列出的所有信息后，重新启动AEM。

   * 如果并发负载较高（观察队列溢出或类似情况），则重新启动AEM可能会解决此问题。
   * 如果重新启动无法解决问题，请打开 [Adobe客户关怀](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support) 并提供步骤1中收集的所有信息。

## 安全中止异步重新索引 {#safely-aborting-asynchronous-re-indexing}

可以通过 `async, async-reindex`和f `ulltext-async` 索引通道( `IndexStats` Mbean)。 有关更多信息，另请参阅 [如何中止重新索引](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). 此外，请考虑以下事项：

* Lucene和Lucene属性索引的重新索引可能会中止，因为它们是自然异步的。
* 只有通过 `PropertyIndexAsyncReindexMBean`.

要安全中止重新索引，请执行以下步骤：

1. 识别控制必须停止的重新索引通道的IndexStats MBean。

   * 通过JMX控制台导航到相应的IndexStats MBean，方法是转到AEM OSGi Web控制台>主>JMX或https://&lt;host>:&lt;port>/system/console/jmx(例如， [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * 根据要停止的重新索引通道( `async`, `async-reindex`或 `fulltext-async`)

      * 要识别相应的通道以及IndexStats MBean实例，请查看Oak索引“异步”属性。 “async”属性包含车道名称： `async`, `async-reindex`或 `fulltext-async`.
      * 通过访问“异步”列中的AEM Index Manager，也可以访问通道。 要访问索引管理器，请导航至操作>诊断>索引管理器。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 调用 `abortAndPause()` 命令 `IndexStats` MBean。
1. 正确标记Oak索引定义，以防止在索引通道恢复时恢复重新索引。

   * 重新索引 **现有** index，请将reindex属性设置为false

      * `/oak:index/someExistingIndex@reindex=false`
   * 或者，对于 **新建** 索引：

      * 将type属性设置为disabled

         * `/oak:index/someNewIndex@type=disabled`
      * 或完全删除索引定义

   完成后，将更改提交到存储库。

1. 最后，在已中止的索引通道上恢复异步索引。

   * 在 `IndexStats` 发出 `abortAndPause()` 命令，调用 `resume()`命令。

## 防止慢速重新索引 {#preventing-slow-re-indexing}

最好在静默时段（例如，不是在大内容摄取期间）重新编入索引，最好在已知并控制AEM加载的维护时段重新编入索引。 另外，请确保在其他维护活动期间不进行重新索引。
