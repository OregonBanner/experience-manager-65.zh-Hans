---
title: 修订版清理
seo-title: 修订版清理
description: 了解如何使用AEM 6.3中的“修订清理”功能。
seo-description: 了解如何使用AEM 6.3中的“修订清理”功能。
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '5917'
ht-degree: 0%

---


# 修订版清理{#revision-cleanup}

## 简介 {#introduction}

对存储库的每次更新都会创建新的内容修订。 因此，每次更新时，存储库的大小都会增大。 为避免存储库增长失控，需要清理旧版本以释放磁盘资源。 此维护功能称为“修订清理”。 自AEM 6.0以来，它已作为脱机例程可用。

在AEM 6.3中，引入了名为“在线修订清理”的该功能的在线版本。 与必须关闭AEM实例的脱机修订清理相比，在AEM实例处于联机状态时，可以运行联机修订清理。 默认情况下，联机修订清理处于打开状态，这是执行修订清理的推荐方式。

**注意**: [有关介](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) 绍以及如何使用联机修订清理的视频，请参阅视频。

修订清理过程包括三个阶段：**估计**、**压缩**&#x200B;和&#x200B;**清理**。 估计根据可能收集的垃圾量确定是否运行下一阶段（压缩）。 在压缩阶段期间，将重写段和tar文件，以保留任何未使用的内容。 清理阶段随后将删除旧段，包括它们可能包含的任何垃圾。 脱机模式通常可以回收更多空间，因为联机模式需要考虑AEM工作集，这会保留收集的额外段。

有关“修订清理”的详细信息，请参阅以下链接：

* [如何运行联机修订清理](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [联机修订清理常见问题](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [如何运行脱机修订清理](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

此外，您还可以阅读[官方Oak文档。](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### 何时使用联机修订清理而不是脱机修订清理？{#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**建议使用“联机修订清理”来执行修订清理。** 脱机修订清理应仅在例外情况下使用 — 例如，在迁移到新存储格式之前，或者Adobe客户服务部门要求您这样做时。

## 如何运行联机修订清理{#how-to-run-online-revision-cleanup}

默认情况下，联机修订清理配置为在AEM作者实例和发布实例上每天自动运行一次。 您只需在用户活动最少的时间段内定义维护窗口。 您可以配置“联机修订清理”任务，如下所示：

1. 在主AEM窗口中，转到&#x200B;**工具 — 操作 — 仪表板 — 维护**&#x200B;或将浏览器指向：`https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 将指针悬停在&#x200B;**每日维护窗口**&#x200B;上，然后单击&#x200B;**设置**&#x200B;图标。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 输入所需的值(循环、开始时间、结束时间)，然后单击&#x200B;**保存**。

   ![chlimage_1-92](assets/chlimage_1-92.png)

或者，如果要手动运行修订清理任务，您可以：

1. 转到&#x200B;**工具 — 操作 — 仪表板 — 维护**&#x200B;或直接浏览到`https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 单击&#x200B;**每日维护窗口**。
1. 将指针悬停在&#x200B;**修订清理**&#x200B;图标上。
1. 单击&#x200B;**运行**。

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 在脱机修订清理后运行联机修订清理{#running-online-revision-cleanup-after-offline-revision-cleanup}

修订清理过程按代代回收旧修订。 这意味着每次运行修订清理时，都会在磁盘上创建并保留新一代。 但是，两种类型的修订清理之间存在差异：脱机修订清理保留一代，而联机修订清理保留两代。 因此，当运行联机修订清理&#x200B;**在**&#x200B;脱机修订清理之后时，会发生以下情况：

1. 在第一次联机修订清理后，系统信息库将多次大小。 这是因为现在有两代存储在磁盘上。
1. 在后续运行期间，在创建新一代时，存储库将临时增大，然后稳定回第一次运行后的大小，因为在线修订清理过程将恢复上一代。

另外，请记住，根据提交的类型和数量，与前一代相比，每代的大小可能有所不同，因此最终大小可能因运行而异。

由于这一情况，建议将磁盘的大小至少比最初估计的存储库大小大两三倍。

## 完全和尾部压缩模式{#full-and-tail-compaction-modes}

**AEM 6.5引** 入了 **“在** 线修订 **** 清理”过程紧凑阶段的两个新模式：

* **完全压缩**&#x200B;模式将重写整个存储库中的所有段和tar文件。 随后的清理阶段因此可以删除整个存储库中的最大垃圾量。 由于完全压缩影响整个存储库，因此需要大量系统资源和时间才能完成。 完全压实与AEM 6.3中的压实阶段相对应。
* **尾部压缩**&#x200B;模式只会重写存储库中最近的段和tar文件。 最近添加的段和tar文件是自上次完全压缩或尾部压缩运行以来添加的。 随后的清理阶段因此只能删除存储库最近部分包含的垃圾。 由于尾部压缩只影响存储库的一部分，因此完成所需的系统资源和时间比完全压缩要少得多。

这些压缩方式构成了效率和资源消耗之间的权衡：尾部压实效果较差，对系统正常运行影响较小。 相比之下，全压实效果更好，但对系统正常运行影响更大。

AEM 6.5还在压缩过程中引入了更高效的内容外部重复数据删除机制，这进一步减少了存储库的磁盘空间占用。

下面两张图表显示了内部实验室测试的结果，这些测试说明与AEM 6.3相比，AEM 6.5中磁盘的平均执行时间和平均占用空间有所减少：

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 如何配置完全和尾部压缩{#how-to-configure-full-and-tail-compaction}

默认配置在周天运行尾部压缩，在周日运行完全压缩。 可以使用`RevisionCleanupTask` [维护任务](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)的新配置值`full.gc.days`更改默认配置。

配置`full.gc.days`值时，请注意，完全压缩将在值中定义的日期运行，而尾部压缩将在值中未定义的日期运行。 例如，如果将完全压缩配置为在星期日运行，则尾部压缩将在星期一至星期六运行。 例如，如果配置完全压缩以在每周的每一天运行，则尾部压缩将根本不运行。

另外，考虑到：

* **尾部** 紧凑效果差，对正常系统运行影响小。因此，计划于营业日内运行。
* **全紧** 缩更有效，但对正常系统操作也有更大的影响。因此，计划在营业日后使用。
* 尾部压实和完全压实都应安排在非高峰时段运行。

### 疑难解答 {#troubleshooting}

使用新的压缩模式时，请牢记以下几点：

* 您可以监视输入/输出(I/O)活动，例如：I/O操作、等待IO的CPU、提交队列大小。 这有助于确定系统是否正在绑定到I/O并需要更新大小。
* `RevisionCleanupTaskHealthCheck`表示联机修订清理的整体运行状况。 它的工作方式与AEM 6.3中相同，不区分全压和尾压。
* 日志消息传递关于压缩模式的相关信息。 例如，当“联机修订清理”开始时，相应的日志消息将指示压缩模式。 此外，在某些情况下，系统将在计划运行尾部压缩时恢复到完全压缩，而日志消息将指示此更改。 下面的日志样本表明压实模式和从尾部到完全压实的变化：

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 已知限制{#known-limitations}

在某些情况下，尾部和完全压实模式之间的交替延迟了清理过程。 更准确地说，在完全压缩后，存储库将会扩大(其大小将多次)。 额外空间将在随后的尾部压缩中回收，此时库将降到低于预完全压缩大小。 还应避免并行维护任务执行。

**建议将磁盘的大小至少比最初估计的存储库大小大两三倍。**

## 联机修订清理常见问题{#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5升级注意事项{#aem-upgrade-considerations}

<table>
 <tbody>
  <tr>
   <td>问题 </td>
   <td>答案</td>
  </tr>
  <tr>
   <td>升级到AEM 6.5时，应该注意什么？</td>
   <td><p>TarMK的持久性格式将随AEM 6.5而更改。这些更改不需要主动迁移步骤。 现有存储库将进行滚动迁移，这对用户是透明的。 迁移过程在AEM 6.5（或相关工具）首次访问存储库时启动。</p> <p><strong>迁移到AEM 6.5持久性格式后，存储库将无法恢复为之前的AEM 6.3持久性格式。</strong></p> </td>
  </tr>
 </tbody>
</table>

### 迁移到Oak区段Tar {#migrating-to-oak-segment-tar}

<table>
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为什么需要迁移存储库？</strong></td>
   <td><p>在AEM 6.3中，需要更改存储格式，特别是为了改进“在线修订清理”的性能和效果。 这些更改不向后兼容，必须使用旧Oak区段(AEM 6.2和之前版本)创建的存储库必须进行迁移。</p> <p>更改存储格式的其他优势：</p>
    <ul>
     <li>更好的可伸缩性（优化的细分大小）。</li>
     <li>更快的<a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">数据存储垃圾收集</a>。<br /> </li>
     <li>为未来的增强功能做准备。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否仍支持以前的Tar格式？</strong></td>
   <td>只有新的Oak Segment Tar受AEM 6.3支持。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>内容迁移是否始终是强制性的？</strong></td>
   <td>是. 除非您使用新实例进行开始，否则您始终必须迁移内容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>我是否可以升级到6.3并稍后进行迁移（例如，使用另一个维护窗口）？</strong></td>
   <td>否，如上所述，内容迁移是强制的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>迁移时能避免停机吗？</strong></td>
   <td>否. 这是一次性工作，无法对正在运行的实例执行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果我意外针对错误的存储库格式运行，会出现什么情况？</strong></td>
   <td>如果尝试针对oak-segment-tar存储库运行oak-segment模块（反之亦然），则启动将失败，并显示<em> IllegalStateException</em>消息“Invalid segment format”。 不会发生数据损坏。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否需要重新索引搜索索引？</strong></td>
   <td>否. 从Oak-segment迁移到Oak-segment-tar将引入容器格式的更改。 包含的数据不受影响，不会被修改。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最好地计算迁移期间和迁移后所需的预期磁盘空间？</strong></td>
   <td>迁移相当于以新格式重新创建区段存储。 这可用于估计迁移过程中需要的额外磁盘空间。 迁移后，可删除旧区段存储以回收空间。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最好地估计迁移的持续时间？</strong></td>
   <td>如果在迁移之前执行<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">脱机修订清理</a>，则迁移性能可以大大改善。 建议所有客户作为升级过程的先决条件执行它。 通常，迁移的持续时间应与脱机修订清理任务的持续时间相似，前提是脱机修订清理任务已在迁移之前执行。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 运行联机修订清理{#running-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>应执行联机修订清理的频率是多少？</strong></td>
   <td>每日一次. 这是“操作”仪表板中的默认配置。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何配置联机修订清理维护任务的开始时间？</strong></td>
   <td>请参阅<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">如何运行联机修订清理</a>部分。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>联机修订清理是否存在不应超过的最大频率？</strong></td>
   <td>建议按照默认配置每天运行一次联机修订清理。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些关键指示符决定了运行联机修订清理的频率？</strong></td>
   <td>无需确定将“在线修订清理”配置为维护任务并每天自动运行的频率。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为什么首次运行时联机修订清理不会回收任何空间？</strong></td>
   <td>联机修订清理按代回收旧修订。 每次运行修订清理时，都会生成新生成。 只有至少两代的内容才会被回收，这意味着在第一轮中，没有什么可回收的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为什么第一个联机修订清理在脱机修订清理后运行时不会回收任何空间？</strong></td>
   <td><p>“脱机修订清理”可回收除最新一代之外的所有内容，而“联机修订清理”可回收两代。 对于新存储库，联机修订清理在脱机修订清理之后第一次执行时不会回收任何空间，因为没有足够旧的代可以回收。</p> <p>此外，请阅读本章<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup"></a>的“脱机修订清理后运行联机修订清理”部分。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>“作者”和“发布”通常具有不同的“联机修订清理”窗口吗？</strong></td>
   <td>这取决于办公时间和客户在线状态的流量模式。 维护窗口应配置在主生产时间之外，以获得最佳清理效果。 对于多个AEM发布实例（TarMK场），联机修订清理的维护窗口应交错。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行联机修订清理之前是否有任何先决条件？</strong></td>
   <td><p>联机修订清理仅在AEM 6.3和更高版本中可用。 此外，如果您使用的是旧版AEM，则需要迁移到新的<a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak区段Tar</a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>决定联机修订清理持续时间的因素有哪些？</strong></td>
   <td>因素有：<br />
    <ul>
     <li>存储库大小</li>
     <li>在系统上加载（每分钟请求，特别是写入操作）</li>
     <li>活动模式（读取与写入）</li>
     <li>硬件规格（CPU性能、内存、IOPS）</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在“联机修订清理”运行时，作者是否仍能工作？</strong></td>
   <td>是的，联机修订清理可以处理并发写入。 但是，“在线修订清理”工作更快、更高效，无需并发写入事务。 建议将“在线修订清理”维护任务计划到相对安静的时间，而不需要大量流量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行联机修订清理时对磁盘空间和堆内存的最低要求是什么？</strong></td>
   <td><p>在“联机修订清理”期间持续监视磁盘空间。 如果可用磁盘空间降至关键值以下，将取消该过程。 关键值是存储库当前磁盘占用量的25%，不可配置。</p> <p><strong>建议将磁盘的大小至少比最初估计的存储库大小大两三倍。</strong></p> <p>在清除过程中，会持续监视可用堆空间。 如果可用堆空间降至关键值以下，则取消该进程。 关键值是通过org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD配置的。 默认值为15%。</p> <p>Recommendations的最小压缩堆大小调整不会与AEM内存大小调整建议分开。 一般来说：<strong>如果AEM实例的大小足够大，足以处理使用情况和预期的负载，则清除过程将获得足够的内存。</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行联机修订清理时预期的性能影响是什么？</strong></td>
   <td>联机修订清理是一个后台进程，它同时从存储库读取和写入到常规系统操作。 特别是，它可能需要在短时间内获得对存储库的独占访问，从而防止其他线程写入存储库。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>“在线修订清理”预期运行多长时间？</strong></td>
   <td>根据我们内部执行的最新性能测试，执行该测试不应超过2小时。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果“在线修订清理”需要更长时间，该怎么办？</strong></td>
   <td>
    <ul>
     <li>确保每天执行。<br /> </li>
     <li>通过相应地在“操作”仪表板中配置维护窗口，确保在最小的存储库活动下执行该操作。</li>
     <li>扩展系统资源（CPU、内存、I/O）。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果“联机修订清理”超出配置的维护窗口，会出现什么情况？</strong></td>
   <td>确保其他维护任务不会延迟其执行。 如果在同一维护窗口中执行的维护任务比联机修订清理的维护数更多，则可能会出现这种情况。 请注意，维护任务是按顺序执行的，不需要可配置的订单。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为何跳过修订垃圾收集？</strong></td>
   <td><p>“修订清理”依赖于评估阶段来确定是否有足够的垃圾需要清理。 估计器将当前大小与上次压缩后存储库的大小进行比较。 如果大小超过配置的增量，将运行清理。 大小增量设置为1 GB。 这实际上意味着，如果自上次清理运行以来存储库大小未增长1 GB，则将跳过新的修订清理小版本。 </p> <p>以下是估计阶段的相关日志条目：</p>
    <ul>
     <li>版本GC将运行：<em>大小增量为N%或N/N（N/N字节），因此运行压缩</em></li>
     <li>修订版GC将<strong>不</strong>运行：<em>大小增量为N%或N/N（N/N字节），因此现在跳过压缩</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果性能影响太大，是否可以安全地中止自动压缩？</strong></td>
   <td>是. 由于AEM 6.3，它可以通过“操作”仪表板中的“维护任务”窗口或通过JMX安全地停止。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果AEM实例在计划清理任务期间关闭，进程是安全中止，还是在压缩完成之前关闭？</strong></td>
   <td>版本清理将中断，存储库将安全关闭。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在联机修订清理期间系统崩溃时会发生什么情况？</strong></td>
   <td>此类情况下不存在数据损坏的风险。 垃圾剩菜将被后续的运行清理。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>未运行联机修订清理会产生什么影响？</strong></td>
   <td>随着时间的推移，性能会降低。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>正在收集哪些修订？</strong></td>
   <td>默认情况下，“在线修订清理”只收集至少有24小时的修订。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果并发写入存储库造成过多干扰，会出现什么情况？</strong></td>
   <td><p>如果系统上存在写并发，则联机修订清理可能需要独占写访问才能在压缩周期结束时提交更改。 如<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">oak文档</a>中更详细的说明，系统将进入<strong>forceCompact模式</strong>。 在强制压缩期间，获得独占写锁定以便最终提交更改而不产生任何并发写入干扰。 要限制对响应时间的影响，可以定义超时值。 默认情况下，此值设置为1分钟，这意味着如果强制压缩在1分钟内未完成，则压缩过程将中止，而有利于并发提交。</p> <p>力压缩的持续时间取决于以下因素：</p>
    <ul>
     <li>硬件：特别是IOPS。 持续时间随IOPS的增加而减少。</li>
     <li>区段存储大小：持续时间随区段存储的大小而增加。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何对待机实例执行联机修订清理？</strong></p> </td>
   <td><p>在冷备用设置中，只需将主实例配置为运行联机修订清理。 在备用实例上，无需专门计划联机修订清理。</p> <p>备用实例上的相应操作是“自动清理” — 这对应于“联机修订清理”的清理阶段。 在主实例上执行联机修订清理之后，自动清理将在备用实例上运行。</p> <p>在备用实例上不运行估计和压缩阶段。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>“脱机修订清理”是否可释放比“联机修订清理”更多的磁盘空间？</strong></td>
   <td><p>脱机修订清理可以立即删除旧修订，而联机修订清理需要考虑应用程序堆栈仍引用的旧修订。 前者因此可以比后者更积极地去除垃圾，而后者在少数垃圾收集周期期间会对效果进行摊销。</p> <p>此外，请阅读本章<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup"></a>的“脱机修订清理后运行联机修订清理”部分。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>是否考虑内存映射文件操作？</td>
   <td>
    <ul>
     <li><strong>在Windows环境中</strong>，始终强制执行常规文件访问，因此不使用内存映射访问。作为一般建议，应将所有可用RAM分配给堆，并增加segmentCache大小。 通过向org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config(例如，segmentCache.size=20480)中添加segmentCache。 请记住为操作系统和其他进程保留一些内存。</li>
     <li><strong>在非Windows环境上</strong>，增加物理内存的大小以改进存储库的内存映射。</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 监视联机修订清理{#monitoring-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>在联机修订清理期间需要监视哪些内容？</strong></td>
   <td>
    <ul>
     <li>启用“联机修订清理”时，应监视磁盘空间。 清理将不运行，或在磁盘空间不足时以抢占方式终止。</li>
     <li>检查日志中的联机修订清理完成时间。 不得超过2小时。</li>
     <li>检查点数。 如果压缩运行时有3个以上的检查点，则建议清除这些检查点。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检查联机修订清理是否成功完成？</strong></td>
   <td><p>您可以通过检查日志来检查联机修订清理是否成功完成。</p> <p>例如，“<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>”表示压缩步骤成功完成，除非消息“<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>”前面出现，这表示并发负载过多。</p> <p>相应地，清理步骤成功完成时会显示消息“<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>”。</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>在哪里可以找到上次联机修订清理执行的统计信息？</strong></td>
   <td><p>状态、进度和统计信息通过JMX(<code>SegmentRevisionGarbageCollection</code> MBean)公开。 有关<code>SegmentRevisionGarbageCollection</code> MBean的详细信息，请阅读下面的<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">段落</a>。</p> <p>可以通过<code>EstimatedRevisionGCCompletion</code> <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>可以使用<code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>获取MBean的引用。</p> <p>请注意，统计信息仅在上次系统开始后可用。 可以利用外部监控工具使数据超出AEM正常运行时间。 请参阅<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">将运行状况检查附加到Nagios的AEM文档，作为外部监视工具</a>的示例。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些相关日志条目？</strong></td>
   <td>
    <ul>
     <li>联机修订清理已启动/停止
      <ul>
       <li>“在线修订清理”分为三个阶段：估计、压缩和清理。 如果存储库未包含足够的垃圾，估计可能会强制压缩和清除以跳过。 在最新版AEM中，消息“<code>TarMK GC #{}: estimation started</code>”标记估计开始，“<code>TarMK GC #{}: compaction started, strategy={}</code>”标记压缩开始，“T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>”标记清理开始。</li>
      </ul> </li>
     <li>修订清理获取的磁盘空间
      <ul>
       <li>仅当清除阶段完成时才会回收空间。 清理阶段的完成由日志消息“T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>”标记。 后期清理大小为{}（{}字节），空间回收{}（{}字节）。 压缩映射权重/深度为{}/{}({} bytes/{})。"</li>
      </ul> </li>
     <li>修订清理期间出现问题
      <ul>
       <li>有许多故障情况，所有这些情况都标有“TarMK GC”开头的WARN或ERROR日志消息。</li>
      </ul> </li>
    </ul> <p>另请参阅下面的<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">基于错误消息的疑难解答</a>部分。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检查在“在线修订清理”完成后回收了多少空间？</strong></td>
   <td>清理周期结束时，日志中会显示一条消息：“<code>TarMK GC #3: cleanup completed</code>”，包括存储库的大小和回收的垃圾量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在联机修订清理完成后如何检查存储库的完整性？</strong></td>
   <td><p>在联机修订清除之后，不需要检查存储库完整性。 </p> <p>但是，您可以执行以下操作，以在清除后检查存储库状态：</p>
    <ul>
     <li>存储库<a href="/help/sites-deploying/consistency-check.md" target="_blank">遍历检查</a></li>
     <li>在清理过程完成后使用oak-run工具检查不一致。 有关如何执行此操作的更多信息，请查看<a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache文档。</a> 您无需关闭AEM即可运行工具。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检测联机修订清理是否失败，以及要恢复的步骤是什么？</strong></td>
   <td>失败条件由以“TarMK GC”开头的WARN或ERROR日志消息标记。 另请参阅下面的<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">基于错误消息的疑难解答</a>部分。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>修订清理运行状况检查中会显示哪些信息？ 它们如何以及何时对颜色编码状态级别有贡献？ </strong></td>
   <td><p>修订清理运行状况检查是<a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">操作仪表板</a>的一部分。<br /> </p> <p>如果上次成功执行联机修订清理维护任务，状态将为<strong>GREEN</strong>。</p> <p>如果“联机修订清理”维护任务取消一次，则它将为<strong>YELLOW</strong>。<br /> </p> <p>如果“联机修订清理”维护任务已在一行中取消三次，则它将为<strong>RED</strong>。 <strong>在这种情况下，需要手动</strong> 交互，否则联机修订清理可能再次失败。有关详细信息，请阅读下面的<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">疑难解答</a>部分。<br /> </p> <p>另请注意，系统重新启动后将重置运行状况检查状态。 因此，新重新启动的实例在“修订清理运行状况检查”上将显示绿色状态。 可以利用外部监控工具使数据超出AEM正常运行时间。 请参阅<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">将运行状况检查附加到Nagios的AEM文档，作为外部监视工具</a>的示例。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何监视待机实例上的自动清理？</strong></p> </td>
   <td><p>状态、进度和统计信息通过JMX使用<code>SegmentRevisionGarbageCollection</code> MBean公开。 另请参见以下<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak文档</a>。 </p> <p>可以使用<code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>获取MBean的引用。</p> <p>请注意，统计信息仅在上次系统开始后可用。 可以利用外部监控工具使数据超出AEM正常运行时间。 另请参阅<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">将运行状况检查附加到Nagios的AEM文档，作为外部监视工具</a>的示例。</p> <p>日志文件还可用于检查自动清理的状态、进度和统计信息。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>在待机实例的“自动清理”过程中需要监视哪些内容？</strong></p> </td>
   <td>
    <ul>
     <li>运行“Automatic Cleanup（自动清理）”时，应监视磁盘空间。</li>
     <li>完成时间（通过日志），以确保不超过2小时。</li>
     <li>运行“自动清理”后，段存储大小。 备用实例上的segmentstore大小应与主实例上的segmentstore大小大致相同。</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 联机修订清理{#troubleshooting-online-revision-cleanup}疑难解答

<table>
 <tbody>
  <tr>
   <td><strong>如果不运行“在线修订清理”，最坏的情况会是什么？</strong></td>
   <td>AEM实例将耗尽磁盘空间，这将导致生产中断。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在发布实例上运行联机修订清理时，高用户流量是否有问题？</strong></td>
   <td>高用户流量会影响压缩阶段是否能成功完成。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>根据运行状况检查和日志条目，联机修订清理未在一行中成功完成三次。 要成功完成联机修订清理，需要什么？</strong></td>
   <td>您可以采取多个步骤来查找并修复问题：<br />
    <ul>
     <li>首先，检查日志条目<br /> </li>
     <li>根据日志中的信息，采取相应的操作：
      <ul>
       <li>如果日志在<code>forceCompact</code>周期中显示五个丢失的压缩周期和超时，则将维护窗口计划到存储库写入量低时的安静时间。 您可以在位于<em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em>的存储库量度监视工具中检查存储库写入</li>
       <li>如果清理在维护窗口的末尾停止，请确保维护任务用户界面中维护窗口的配置足够大</li>
       <li>如果可用堆内存不足，请确保实例具有足够的内存。</li>
       <li>如果反应迟钝，则分段存储可能会增长过多，以致于“在线修订清理”甚至在较长的维护窗口中无法完成。 例如，如果上周未完成成功的联机修订清理，则建议计划脱机维护并执行脱机修订清理，以使区段存储恢复为可管理的大小。</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>打开运行状况检查警报后需要执行什么操作？</strong></td>
   <td>请参阅上一点。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果在计划的维护窗口中联机修订清理超时，会出现什么情况？</strong></td>
   <td>将取消联机修订清理，并删除剩余内容。 下次计划维护窗口时，它将再次开始。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>什么导致<code>SegmentNotFoundException</code>实例记录在<code>error.log</code>中，如何恢复？</strong></td>
   <td><p>当TarMK尝试访问它找不到的存储单元（段）时，将记录<code>SegmentNotFoundException</code>。 有三种情况可能导致此问题：</p>
    <ol>
     <li>规避建议的访问机制（如Sling和JCR API）并使用较低级别的API/SPI访问存储库，然后超过区段保留时间的应用程序。 也就是说，它会将对实体的引用保留时间延长到“在线修订清理”允许的保留时间（默认为24小时）。 此案件是暂时的，不会导致数据损坏。 要恢复，应使用oak-run工具确认异常的暂时性（oak-run检查不应报告任何错误）。 为此，需要脱机并在之后重新启动实例。</li>
     <li>外部事件导致磁盘上的数据损坏。 这可能是磁盘故障、磁盘空间不足或意外修改所需数据文件。 在这种情况下，需要使实例脱机并使用橡树运行检查进行修复。 有关如何执行oak-run检查的详细信息，请阅读以下<a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache文档</a>。</li>
     <li>所有其他事件都应通过<a href="https://helpx.adobe.com/cn/marketing-cloud/contact-support.html" target="_blank">Adobe客户关怀</a>解决。</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 基于错误消息{#troubleshooting-based-on-error-messages}的疑难解答

如果在联机修订清除过程中发生意外，error.log将是详细的。 以下矩阵旨在说明最常见的消息并提供可能的解决方案：

| **相位** | **日志消息** | **解释** | **后续步骤** |
|---|---|---|---|
|  |  |  |  |
| 估计 | TarMK GC #2:由于压缩暂停而跳过 | 当通过配置在系统上禁用压缩时跳过估计阶段。 | 启用联机修订清理。 |
|  | TarMK GC #2:估计中断：${REASON}。 跳过压缩。 | 估计阶段提前终止。 一些可能中断估计阶段的事件示例：主机系统上的内存或磁盘空间不足。 | 这取决于给定的原因。 |
| 压实 | TarMK GC #2:压缩暂停 | 只要按配置暂停压缩阶段，则不执行估计阶段和压缩阶段。 | 启用联机修订清理。 |
|  | TarMK GC #2:压缩已取消：${REASON}。 | 压缩阶段提前终止。 可能中断压缩阶段的事件示例：主机系统上的内存或磁盘空间不足。 此外，还可以通过关闭系统或通过管理接口（如操作功能板中的维护窗口）显式取消压缩来取消压缩。 | 这取决于给定的原因。 |
|  | TarMK GC #2:压实在32.902分钟(1974140毫秒)后失败，5次循环 | 此消息并不表示存在不可恢复的错误，但只表示经过一定的尝试后，压缩终止。 另请阅读下面的[段](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)。 | 请阅读以下[Oak文档](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)和[运行在线修订清理](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup)部分的最后一个问题。 |
| 清理 | TarMK GC #2:清理中断 | 通过关闭存储库已取消清理。 预计不会影响一致性。 此外，磁盘空间很可能不会完全回收。 它将在下一个修订清理周期中回收。 | 调查为什么存储库已关闭，并且今后尝试避免在维护窗口期间关闭存储库。 |

## 如何运行脱机修订清理{#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>需要使用不同版本的Oak-run工具，具体取决于您在AEM安装中使用的Oak版本。 在使用该工具之前，请检查以下版本要求列表:
>
>* 对于Oak版本&#x200B;**1.0.0至1.0.11**&#x200B;或&#x200B;**1.1.0至1.1.6**，请使用Oak-run版本** 1.0.11**
   >
   >
* 对于比上述&#x200B;**版本更新的Oak版本**，请使用与AEM安装的Oak核心相匹配的Oak-run版本。

>



Adobe提供了一个名为&#x200B;**Oak-run**&#x200B;的工具，用于执行修订清理。 可在以下位置下载：

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

此工具是可运行的jar，可手动运行以压缩存储库。 该过程称为脱机修订清理，因为需要关闭存储库才能正确运行该工具。 确保根据您的维护窗口规划清理。

有关如何提高清理过程性能的提示，请参阅[提高脱机修订清理的性能](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup)。

>[!NOTE]
>
>您还可以在进行维护之前清除旧的检查点（下面步骤中的步骤2和步骤3）。 建议仅对具有100个以上检查点的实例使用此选项。

1. 请务必确保您有AEM实例的最近备份。

   关闭AEM。

1. （可选）使用该工具查找旧检查点：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. （可选）然后，删除未引用的检查点：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. 运行压缩并等待完成：

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### 提高脱机修订清理的性能{#increasing-the-performance-of-offline-revision-cleanup}

橡树运行工具引入了一些功能，旨在提高修订清理过程的性能并尽可能减少维护窗口。

该列表包括若干命令行参数，如下所述：

* **-mmap。** 您可以将其设置为true或false。如果设置为true，则使用内存映射访问。 如果设置为false，则使用文件访问。 如果未指定，则在64位系统上使用内存映射访问，在32位系统上使用文件访问。 在Windows上，始终强制执行常规文件访问，并忽略此选项。 **此参数已替换 — Dtar.memoryMapped参数。**

* **-Dupdate.limit**。定义将临时事务刷新到磁盘的阈值。 默认值为 10000。

* **-Dcompress-interval**。压缩当前映射之前要保留的压缩映射条目数。 默认为 1000000。如果有足够的堆内存可用，您应该将此值增加到更高的数值，以提高吞吐量。 **此参数已在Oak版本1.6中删除，无效。**

* **-Dcompytion-progress-log**。将记录的已压缩节点数。 默认值为150000，这意味着在操作过程中将记录150000个压缩的节点。 结合下面介绍的下一个参数使用。

* **-Dtar.PersistComponityMap。** 将此参数设置为true可使用磁盘空间而不是堆内存来压缩映射持久性。需要oak-run工具&#x200B;**版本1.4**&#x200B;及更高版本。 有关更多详细信息，请参阅[脱机修订清理常见问题部分中的问题3。 ](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions)**此参数已在Oak版本1.6中删除，无效。**

* **-force。** 强制压缩并忽略不匹配的段存储版本。

>[!CAUTION]
>
>使用`--force`参数将区段存储升级到最新版本，该版本与旧版Oak版本不兼容。 此外，还要考虑到，不可能降级。 通常，您应谨慎使用这些参数，并且仅当您对如何使用这些参数有知识时。

使用中的参数示例：

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 触发修订清除的其他方法{#additional-methods-of-triggering-revision-cleanup}

除了上述方法之外，您还可以使用JMX控制台触发修订清除机制，如下所示：

1. 转到[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)打开JMX控制台
1. 单击&#x200B;**RevisionGarbageCollection** MBean。
1. 在下一个窗口中，单击&#x200B;**startRevisionGC()**，然后单击&#x200B;**调用**&#x200B;以开始修订垃圾收集作业。

### 脱机修订清理常见问题解答{#offline-revision-cleanup-frequently-asked-questions}

<table>
 <tbody>
  <tr>
   <td><strong>决定脱机修订清理持续时间的因素有哪些？</strong></td>
   <td><p>存储库大小和需要清理的修订量决定了清理的持续时间。</p> </td>
  </tr>
  <tr>
   <td><strong>修订版和页面版本之间有何差异？</strong></td>
   <td>
    <ul>
     <li><strong>Oak修订版：</strong> Oak将所有内容组织在一个由节点和属性组成的大树层次结构中。此内容树的每个快照或修订都是不可变的，对该树所做的更改将表示为新修订的序列。 通常，每次内容修改都会触发新的修订。 另请参阅<a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank">跟踪链接</a>。</li>
     <li><strong>页面版本：</strong> 版本控制创建页面在特定时间点的“快照”。通常，在激活页面时会创建新版本。 有关详细信息，请参阅<a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">使用页面版本</a>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>如果脱机修订清理任务在8小时内未完成，如何加快该操作？</strong></td>
   <td>如果修订版任务在8小时内未完成，且<a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">线程转储</a>显示主热点为<code>InMemoryCompactionMap.findEntry</code>，请对oak-run工具<strong>版本1.4 </strong>或更高版本使用以下参数：<code>-Dtar.PersistCompactionMap=true</code>。 请注意，<code>-Dtar.PersistCompactionMap</code>参数已在Oak版本1.6中删除。</td>
  </tr>
 </tbody>
</table>

