---
title: 修订版清理
seo-title: 修订版清理
description: 了解如何使用AEM 6.3中的修订清理功能。
seo-description: 了解如何使用AEM 6.3中的修订清理功能。
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
feature: 配置
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5917'
ht-degree: 0%

---

# 修订版清理{#revision-cleanup}

## 简介 {#introduction}

对存储库的每次更新都会创建新的内容修订版本。 因此，每次更新时，存储库的大小都会增大。 为避免存储库增长失控，需要清理旧的修订版本以释放磁盘资源。 此维护功能称为修订清理。 它自AEM 6.0起便已作为离线例程使用。

在AEM 6.3中，引入了此功能的在线版本“在线修订清理”。 与必须关闭AEM实例的离线修订版清理相比，在AEM实例处于在线状态时可以运行在线修订版清理。 默认情况下，联机修订版清理处于打开状态，这是执行修订版清理的推荐方式。

**注意**: [有关介](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) 绍和如何使用在线修订清理，请参阅视频。

修订清理过程包含三个阶段：**估计**、**压缩**&#x200B;和&#x200B;**清理**。 估计根据可能收集的垃圾量确定是否运行下一阶段（压缩）。 在压缩阶段期间，区段和tar文件将被重写，留下任何未使用的内容。 清理阶段随后删除旧段，包括它们可能包含的任何垃圾。 脱机模式通常可以节省更多空间，因为联机模式需要考虑AEM工作集，该工作集会保留未收集的额外区段。

有关修订清理的更多详细信息，请参阅以下链接：

* [如何运行在线修订清理](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [在线修订清理常见问题解答](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [如何运行脱机修订版清理](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

此外，您还可以阅读[官方Oak文档。](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### 何时使用在线修订清理而不是离线修订清理？{#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**联机修订版清理是执行修订版清理的推荐方法。** 脱机修订版清理应仅在特殊情况下使用 — 例如，在迁移到新存储格式之前，或者如果Adobe客户关怀部门要求您执行此操作，则应使用此清理。

## 如何运行联机修订版清理{#how-to-run-online-revision-cleanup}

默认情况下，联机修订版清理配置为在AEM创作实例和发布实例上每天自动运行一次。 您只需定义在用户活动最少的时段内的维护窗口即可。 可以按如下方式配置联机修订版清理任务：

1. 在主AEM窗口中，转到&#x200B;**工具 — 操作 — 功能板 — 维护**，或将您的浏览器指向：`https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 将鼠标悬停在&#x200B;**每日维护窗口**&#x200B;上，然后单击&#x200B;**设置**&#x200B;图标。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 输入所需的值（循环、开始时间、结束时间），然后单击&#x200B;**Save**。

   ![chlimage_1-92](assets/chlimage_1-92.png)

或者，如果要手动运行修订清理任务，则可以：

1. 转到&#x200B;**工具 — 操作 — 功能板 — 维护**&#x200B;或直接浏览到`https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 单击&#x200B;**每日维护窗口**。
1. 将鼠标悬停在&#x200B;**修订版清理**&#x200B;图标上。
1. 单击&#x200B;**运行**。

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 脱机修订版清理后运行联机修订版清理{#running-online-revision-cleanup-after-offline-revision-cleanup}

修订清理过程按代回收旧的修订。 这意味着每次运行修订清理时，都会在磁盘上创建并保留新一代。 但是，两种类型的修订清理之间存在差异：脱机修订版清理保留一代，而联机修订版清理保留两代。 因此，在&#x200B;**离线修订清理之后运行在线修订清理**&#x200B;时，会发生以下情况：

1. 首次联机修订版清理后，运行存储库的大小将翻倍。 之所以会出现这种情况，是因为现在有两代存储在磁盘上。
1. 在后续运行期间，在创建新一代存储库时，存储库将暂时增长，然后稳定回到在首次运行后所具有的大小，因为在线修订清理过程会回收上一代存储库。

此外，请记住，根据提交的类型和数量，每代提交的大小与上一代提交的大小不同，因此最终大小可能会因运行而异。

因此，建议将磁盘的大小至少比最初估计的存储库大小大2或3倍。

## 完全和尾部压缩模式{#full-and-tail-compaction-modes}

**AEM 6.5** 为在线 **修订** 清理过 **** 程的压缩阶段引入了两个新模型：

* **完全压缩**&#x200B;模式会重写整个存储库中的所有区段和tar文件。 因此，后续清理阶段可以删除整个存储库中最大垃圾量。 由于完全压缩会影响整个存储库，因此需要大量系统资源和时间才能完成。 完全压缩对应于AEM 6.3中的压缩阶段。
* **尾部压缩**&#x200B;模式只会重写存储库中最近的区段和tar文件。 最近的区段和tar文件是自上次运行完全压缩或尾压缩后添加的区段和tar文件。 因此，后续的清理阶段只能删除存储库最近部分中包含的垃圾。 由于尾部压缩仅影响存储库的一部分，因此完成尾部压缩所需的系统资源和时间比完全压缩要少得多。

这些压缩模式在效率和资源消耗之间构成了权衡：尾部压实效果较差，对正常系统运行影响较小。 相比之下，完全压实效果更好，但对系统正常运行的影响更大。

AEM 6.5还在压缩期间引入了更高效的内容重复数据删除机制，这进一步减少了存储库的磁盘空间占用。

下图显示了AEM 6.5中平均执行时间和磁盘平均占用空间比AEM 6.3减少的内部实验室测试结果：

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 如何配置完整和尾压缩{#how-to-configure-full-and-tail-compaction}

默认配置在周天运行尾部压缩，在周日运行完全压缩。 使用`RevisionCleanupTask` [维护任务](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)的新配置值`full.gc.days`可以更改默认配置。

配置`full.gc.days`值时，请注意，完全压缩将在值中定义的日期期间运行，而尾部压缩将在值中未定义的日期期间运行。 例如，如果将完全压缩配置为在星期日运行，则尾部压缩将在星期一到星期六运行。 例如，如果将完全压缩配置为在一周的每一天运行，则尾部压缩根本不会运行。

此外，还考虑到：

* **尾部** 紧缩效果差，对正常系统运行影响小。因此，计划在工作日期间运行。
* **完全** 压缩更有效，但对正常系统操作的影响也更大。因此，本计划在工作日使用。
* 尾部压缩和完全压缩应安排在非高峰时段运行。

### 疑难解答 {#troubleshooting}

使用新的压缩模式时，请记住以下事项：

* 您可以监视输入/输出(I/O)活动，例如：I/O操作、等待IO的CPU、提交队列大小。 这有助于确定系统是否绑定了I/O，并且需要更新大小。
* `RevisionCleanupTaskHealthCheck`表示联机修订版清理的整体运行状况状态。 它的工作方式与AEM 6.3中相同，不区分完整压缩和尾部压缩。
* 日志消息包含有关压缩模式的相关信息。 例如，当联机修订版清理启动时，相应的日志消息将指示压缩模式。 此外，在某些情况下，系统将在计划运行尾部压缩时还原为完全压缩，而日志消息将指示此更改。 下面的日志示例指示了压缩模式以及从尾到完全压缩的变化：

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 已知限制{#known-limitations}

在某些情况下，尾部和完全压缩模式之间的交替会延迟清理过程。 更准确地说，在完全压缩后，存储库将会增加（其大小将翻倍）。 当存储库将降低到预完全压缩大小以下时，将在后续尾部压缩中回收额外空间。 还应避免并行维护任务执行。

**建议将磁盘的大小至少比最初估计的存储库大小大2或3倍。**

## 在线修订清理常见问题解答{#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5升级注意事项{#aem-upgrade-considerations}

<table>
 <tbody>
  <tr>
   <td>问题 </td>
   <td>答案</td>
  </tr>
  <tr>
   <td>升级到AEM 6.5时，我应该注意什么？</td>
   <td><p>AEM 6.5将更改TarMK的持久性格式。这些更改不需要主动迁移步骤。 现有存储库将进行滚动迁移，该迁移对用户是透明的。 在AEM 6.5（或相关工具）首次访问存储库时，将启动迁移过程。</p> <p><strong>迁移到AEM 6.5持久性格式后，存储库将无法还原为之前的AEM 6.3持久性格式。</strong></p> </td>
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
   <td><strong>为何需要迁移存储库？</strong></td>
   <td><p>在AEM 6.3中，需要更改存储格式，特别是为了提高在线修订清理的性能和功效。 这些更改不向后兼容，因此必须使用旧Oak区段(AEM 6.2及更早版本)创建的存储库必须进行迁移。</p> <p>更改存储格式的其他好处：</p>
    <ul>
     <li>更好的可扩展性（优化了区段大小）。</li>
     <li>更快的<a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">数据存储垃圾收集</a>。<br /> </li>
     <li>未来增强功能的基础工作。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否仍支持以前的Tar格式？</strong></td>
   <td>AEM 6.3仅支持新的Oak区段Tar。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>内容迁移是否始终是强制性的？</strong></td>
   <td>是. 除非您从新实例开始，否则您将始终必须迁移内容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>我是否可以升级到6.3并稍后进行迁移（例如，使用另一个维护窗口）？</strong></td>
   <td>否，如上所述，内容迁移是强制性的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>迁移时能避免停机吗？</strong></td>
   <td>否. 这是一次性工作，无法对正在运行的实例执行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果意外针对错误的存储库格式运行，会发生什么情况？</strong></td>
   <td>如果您尝试针对oak-segment-tar存储库（反之亦然）运行oak-segment模块，启动将失败，出现<em>IllegalStateException</em>消息，并显示“区段格式无效”。 不会发生数据损坏。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否需要重新索引搜索索引？</strong></td>
   <td>否. 从oak-segment迁移到oak-segment-tar会引入容器格式的更改。 包含的数据不会受到影响，也不会进行修改。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最好地计算迁移期间和之后所需的预期磁盘空间？</strong></td>
   <td>迁移相当于以新格式重新创建区段存储。 这可用于估计迁移期间所需的额外磁盘空间。 迁移后，可以删除旧区段存储以回收空间。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最好地估计迁移的持续时间？</strong></td>
   <td>如果在迁移之前执行<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">离线修订清理</a>，则迁移性能会得到显着提高。 建议所有客户将其作为升级过程的先决条件执行。 通常，迁移的持续时间应类似于脱机修订版清理任务的持续时间，假定脱机修订版清理任务已在迁移之前执行。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 运行联机修订版清理{#running-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>应该执行多久一次联机修订版清理？</strong></td>
   <td>每日一次. 这是“操作功能板”中的默认配置。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何配置联机修订版清理维护任务的开始时间？</strong></td>
   <td>请参阅<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">如何运行在线修订版清理</a>部分。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>联机修订版清理是否有不应超出的最大频率？</strong></td>
   <td>建议按照默认配置，每天运行一次联机修订版清理。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些关键指标可确定应运行在线修订清理的频率？</strong></td>
   <td>无需确定频率，因为联机修订版清理已配置为维护任务，并且每天自动运行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为什么联机修订版清理在首次运行时没有回收任何空间？</strong></td>
   <td>在线修订清理按代回收旧修订。 每次运行修订清理时，都会生成新的生成。 只有至少两代的内容才会被回收，这意味着在第一次运行中，没有什么可回收的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为什么在脱机修订版清理后运行第一个联机修订版清理后没有回收任何空间？</strong></td>
   <td><p>离线修订版清理正在回收除最新一代之外的所有内容，而在线修订版清理则是将最新的两代进行比较。 对于新存储库，在脱机修订版清理后首次执行联机修订版清理时，不会回收任何空间，因为没有足够旧的可回收空间。</p> <p>此外，请阅读本章<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">的“脱机修订版清理后运行联机修订版清理”部分。</a></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>创作和发布通常具有不同的在线修订版清理窗口吗？</strong></td>
   <td>这取决于客户在线状态的办公时间和流量模式。 维护窗口应在主生产时间之外进行配置，以达到最佳清理效果。 对于多个AEM发布实例（TarMK场），联机修订版清理的维护窗口应该交错。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行在线修订清理之前是否存在任何先决条件？</strong></td>
   <td><p>联机修订版清理仅在AEM 6.3及更高版本中可用。 此外，如果您使用的是旧版AEM，则需要迁移到新的<a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak区段Tar</a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些因素决定了在线修订清理的持续时间？</strong></td>
   <td>因素包括：<br />
    <ul>
     <li>存储库大小</li>
     <li>在系统上加载（每分钟请求数，特别是写操作）</li>
     <li>活动模式（读取与写入）</li>
     <li>硬件规格（CPU性能、内存、IOPS）</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在运行联机修订版清理时，作者是否仍可以工作？</strong></td>
   <td>是的，联机修订版清理可以处理并发写入。 但是，在线修订清理工作可以更快、更高效地进行，而无需并发写入事务。 建议将“在线修订清理”维护任务安排在相对安静的时间，而没有大量流量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行联机修订版清理时，对磁盘空间和堆内存的最低要求是什么？</strong></td>
   <td><p>在联机修订版清理期间持续监视磁盘空间。 如果可用磁盘空间降至临界值以下，则该过程将被取消。 关键值是存储库当前磁盘占用量的25%，且不可配置。</p> <p><strong>建议将磁盘的大小至少比最初估计的存储库大小大2或3倍。</strong></p> <p>在清理过程中，会持续监控空闲堆空间。 如果可用堆空间降至临界值以下，则取消该进程。 临界值通过org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD进行配置。 默认值为15%。</p> <p>Recommendations用于最小压缩堆大小调整建议与AEM内存大小调整建议之间没有分隔。 一般规则是：<strong>如果AEM实例的大小足够大，足以处理用例和预期的负载，则清理过程将获得足够的内存。</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行在线修订清理时预期的性能影响是什么？</strong></td>
   <td>联机修订版清理是从存储库同时读取并写入到正常系统操作的后台进程。 特别是，它可能需要在短时间内获得对存储库的独占访问权限，以防止其他线程写入存储库。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>预期联机修订版清理将运行多长时间？</strong></td>
   <td>根据我们在内部执行的最新性能测试，执行该测试不应超过2小时。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果联机修订版清理需要较长时间，应该怎么做？</strong></td>
   <td>
    <ul>
     <li>确保每天执行一次。<br /> </li>
     <li>通过相应地在Operations Dashboard中配置维护窗口，确保在最小的存储库活动期间执行该操作。</li>
     <li>扩展系统资源（CPU、内存、I/O）。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果联机修订版清理超出配置的维护窗口，会发生什么情况？</strong></td>
   <td>确保其他维护任务不会延迟其执行。 如果在同一维护窗口中执行的维护任务比联机修订版清理要多，则可能会出现这种情况。 请注意，维护任务是按顺序执行的，而不需要可配置的顺序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为何会跳过修订垃圾收集？</strong></td>
   <td><p>修订清理依赖于评估阶段来确定是否有足够的垃圾需要清理。 估算器会将当前大小与上次压缩后存储库的大小进行比较。 如果大小超过配置的增量，则将运行清理。 大小增量设置为1 GB。 这实际上意味着，如果自上次清理运行以来存储库大小没有增加1 GB，则将跳过新的修订清理迭代。 </p> <p>以下是估计阶段的相关日志条目：</p>
    <ul>
     <li>版本GC将运行：<em>大小增量为N%或N/N（N/N字节），因此运行压缩</em></li>
     <li>修订版GC将<strong>不</strong>运行：<em>大小增量为N%或N/N（N/N字节），因此现在跳过压缩</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果性能影响过大，是否可以安全地中止自动压缩？</strong></td>
   <td>是. 自AEM 6.3起，可通过操作仪表板中的维护任务窗口或通过JMX安全地停止它。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果AEM实例在计划的清理任务期间关闭，进程是否会安全中止，还是在压缩完成之前会阻止关闭？</strong></td>
   <td>修订清理将中断，并且存储库将安全关闭。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在联机修订版清理期间系统崩溃时会发生什么情况？</strong></td>
   <td>在此类情况下，不存在数据损坏的风险。 垃圾剩料将通过后续运行进行清理。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>未运行在线修订清理会产生什么影响？</strong></td>
   <td>性能会随着时间的推移而下降。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>要收集哪些修订？</strong></td>
   <td>默认情况下，联机修订版清理仅收集至少24小时之前的修订。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果并发写入存储库造成过多干扰，会出现什么情况？</strong></td>
   <td><p>如果系统上存在写并发，则联机修订版清理可能需要独占写访问才能在压缩周期结束时提交更改。 系统将进入<strong>forceCompact模式</strong>，如<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">oak文档</a>中详细说明。 在强制紧凑期间，获取独占写锁定以最终提交更改而不产生任何并发写入干扰。 要限制对响应时间的影响，可定义超时值。 默认情况下，此值设置为1分钟，这意味着如果强制压缩在1分钟内未完成，则压缩过程将中止，以支持并发提交。</p> <p>紧凑力的持续时间取决于以下因素：</p>
    <ul>
     <li>硬件：特别是IOPS。 持续时间会随着IOPS的增加而减少。</li>
     <li>区段存储大小：持续时间会随区段存储的大小而增加。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何在备用实例上执行联机修订版清理？</strong></p> </td>
   <td><p>在冷备用设置中，只需要将主实例配置为运行联机修订版清理。 在备用实例上，无需专门计划联机修订版清理。</p> <p>备用实例上的相应操作是自动清理 — 它对应于联机修订版清理的清理阶段。 在主实例上执行在线修订版清理后，将在备用实例上运行自动清理。</p> <p>估计阶段和压缩阶段将不会在备用实例上运行。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>脱机修订版清理是否能够释放比联机修订版清理更多的磁盘空间？</strong></td>
   <td><p>脱机修订版清理可以立即删除旧修订版，而联机修订版清理需要考虑应用程序堆栈仍引用的旧修订版。 因此，前者比后者更积极地去除垃圾，后者在几个垃圾收集周期期间对其效果进行摊销。</p> <p>此外，请阅读本章<a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">的“脱机修订版清理后运行联机修订版清理”部分。</a></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>有关内存映射文件操作的任何注意事项？</td>
   <td>
    <ul>
     <li><strong>在Windows环境中</strong>，始终强制执行常规文件访问，因此不使用内存映射访问。一般建议，应将所有可用的RAM分配给堆，并增加segmentCache大小。 通过将segmentCache.size选项添加到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config(例如segmentCache.size=20480)，可增加segmentCache。 请记住为操作系统和其他进程保留一些RAM。</li>
     <li><strong>在非Windows环境中</strong>，增加物理内存的大小以改进存储库的内存映射。</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 监视在线修订清理{#monitoring-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>在联机修订清理期间需要监控哪些内容？</strong></td>
   <td>
    <ul>
     <li>启用“联机修订版清理”后，应监视磁盘空间。 清理将不会运行，或者在磁盘空间不足时会抢先终止。</li>
     <li>检查日志中在线修订清理的完成时间。 最长不得超过2小时。</li>
     <li>检查点数。 如果压缩运行时有3个以上的检查点，则建议清理检查点。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检查联机修订版清理是否成功完成？</strong></td>
   <td><p>您可以通过检查日志来检查联机修订版清理是否成功完成。</p> <p>例如，“<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>”表示压缩步骤成功完成，除非出现消息“<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>”，这表示并发负载过多。</p> <p>相应地，出现消息“<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>”，表示清理步骤的成功完成。</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>在哪里可以找到上次在线修订清理执行的统计信息？</strong></td>
   <td><p>状态、进度和统计信息通过JMX(<code>SegmentRevisionGarbageCollection</code> MBean)公开。 有关<code>SegmentRevisionGarbageCollection</code> MBean的更多详细信息，请阅读<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">下段</a>。</p> <p>可通过<code>EstimatedRevisionGCCompletion</code> <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>可以使用<code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>获取MBean的引用。</p> <p>请注意，统计信息仅在上次系统启动后才可用。 利用外部监控工具，可让数据超出AEM正常运行时间。 请参阅<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">将运行状况检查附加到Nagios的AEM文档，作为外部监控工具</a>的示例。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>相关的日志条目是什么？</strong></td>
   <td>
    <ul>
     <li>联机修订版清理已启动/已停止
      <ul>
       <li>在线修订清理包含三个阶段：估计、压缩和清理。 如果存储库不包含足够的垃圾，则估计可能会强制压缩和清理跳过。 在最新版本的AEM中，消息“<code>TarMK GC #{}: estimation started</code>”标记估计的开始，“<code>TarMK GC #{}: compaction started, strategy={}</code>”标记压缩的开始，“T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>”标记清理的开始。</li>
      </ul> </li>
     <li>修订清理获得的磁盘空间
      <ul>
       <li>仅当清理阶段完成时，才会回收空间。 清理阶段的结束由日志消息“T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>”标记。 后清理大小为{}（{}字节），空间已回收{}（{}字节）。 压缩映射的重量/深度为{}/{}（{}字节/{}）。”</li>
      </ul> </li>
     <li>修订清理期间出现问题
      <ul>
       <li>出现许多故障情况，所有故障都标有“警告”或“错误日志”消息，以“TarMK GC”开头。</li>
      </ul> </li>
    </ul> <p>另请参阅下面的<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">根据错误消息进行疑难解答</a>部分。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检查在线修订清理完成后回收了多少空间？</strong></td>
   <td>清理周期结束时，日志中会显示一条消息：“<code>TarMK GC #3: cleanup completed</code>”，其中包括存储库的大小和回收垃圾的数量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在线修订清理完成后如何检查存储库的完整性？</strong></td>
   <td><p>在联机修订清理之后，无需检查存储库完整性。 </p> <p>但是，您可以执行以下操作，以在清理后检查存储库状态：</p>
    <ul>
     <li>存储库<a href="/help/sites-deploying/consistency-check.md" target="_blank">遍历检查</a></li>
     <li>清理过程完成后，使用oak-run工具检查是否不一致。 有关如何执行此操作的更多信息，请查看<a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache文档。</a> 您无需关闭AEM即可运行该工具。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检测联机修订版清理是否失败以及要恢复的步骤是什么？</strong></td>
   <td>失败条件标有以“TarMK GC”开头的“警告”或“错误日志”消息。 另请参阅下面的<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">根据错误消息进行疑难解答</a>部分。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>修订清理运行状况检查中会显示哪些信息？ 它们如何以及何时对颜色编码状态级别做出贡献？ </strong></td>
   <td><p>修订版清理运行状况检查是<a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">操作功能板</a>的一部分。<br /> </p> <p>如果上次成功执行联机修订版清理维护任务，则状态将为<strong>GREEN</strong>。</p> <p>如果“在线修订清理”维护任务被取消一次，则该任务将为<strong>YELLOW</strong>。<br /> </p> <p>如果“在线修订版清理”维护任务已连续三次取消，则该任务将为<strong>RED</strong>。 <strong>在这种情况下，需要手动</strong> 交互，否则在线修订清理可能再次失败。有关更多信息，请阅读下面的<a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">疑难解答</a>部分。<br /> </p> <p>另请注意，系统重新启动后将重置“运行状况检查”状态。 因此，新重新启动的实例在修订清理运行状况检查中将显示绿色状态。 利用外部监控工具，可让数据超出AEM正常运行时间。 请参阅<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">将运行状况检查附加到Nagios的AEM文档，作为外部监控工具</a>的示例。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何在备用实例上监视自动清理？</strong></p> </td>
   <td><p>使用<code>SegmentRevisionGarbageCollection</code> MBean通过JMX公开状态、进度和统计信息。 另请参阅以下<a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak文档</a>。 </p> <p>可以使用<code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>获取MBean的引用。</p> <p>请注意，统计信息仅在上次系统启动后才可用。 利用外部监控工具，可让数据超出AEM正常运行时间。 另请参阅<a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">有关将运行状况检查附加到Nagios的AEM文档，以作为外部监控工具</a>的示例。</p> <p>日志文件还可用于检查自动清理的状态、进度和统计信息。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>在备用实例上执行自动清理期间需要监控哪些内容？</strong></p> </td>
   <td>
    <ul>
     <li>运行自动清理时应监视磁盘空间。</li>
     <li>完成时间（通过日志），以确保不会超过2小时。</li>
     <li>运行自动清理后的Segmentstore大小。 备用实例上的segmentstore的大小应与主实例上的大小大致相同。</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 联机修订版清理疑难解答{#troubleshooting-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>如果不运行在线修订清理，最坏的情况是什么？</strong></td>
   <td>AEM实例将耗尽磁盘空间，这将导致生产中断。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在发布实例上运行在线修订版清理时，高用户流量是否存在问题？</strong></td>
   <td>高用户流量会影响压缩阶段是否能够成功完成。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>根据运行状况检查和日志条目，联机修订版清理未成功完成一行三次。 要成功完成在线修订清理，需要执行哪些操作？</strong></td>
   <td>您可以采取多个步骤来查找并修复问题：<br />
    <ul>
     <li>首先，检查日志条目<br /> </li>
     <li>根据日志中的信息，采取相应的操作：
      <ul>
       <li>如果日志显示5个缺少的紧凑周期和<code>forceCompact</code>周期的超时，则在存储库写入量较低时，将维护窗口安排为静默时间。 您可以在位于<em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em>的存储库量度监控工具中检查存储库写入</li>
       <li>如果清理在维护窗口的末尾停止，请确保维护任务用户界面中维护窗口的配置足够大</li>
       <li>如果可用堆内存不足，请确保实例具有足够的内存。</li>
       <li>如果反应迟钝，则segmentstore可能会增长过多，以致于在线修订清理无法在较长的维护时间范围内完成。 例如，如果上周未成功完成在线修订清理，则建议规划离线维护并执行离线修订清理，以便将区段存储恢复到可管理的大小。</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>开启“运行状况检查”警报后需要执行哪些操作？</strong></td>
   <td>请参阅上一点。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果在计划维护时段内联机修订版清理已用完时间，会发生什么情况？</strong></td>
   <td>将取消在线修订清理，并删除剩菜。 下次计划维护时间时，它将重新启动。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>什么原因导致<code>SegmentNotFoundException</code>实例记录在<code>error.log</code>中，如何恢复？</strong></td>
   <td><p>当TarMK尝试访问它找不到的存储单元（区段）时，会记录<code>SegmentNotFoundException</code>。 有三种情况可能会导致此问题：</p>
    <ol>
     <li>一种应用程序，它绕过推荐的访问机制（如Sling和JCR API），使用较低级别的API/SPI访问存储库，然后超过区段的保留时间。 也就是说，它会保留对实体的引用时间超过在线修订清理所允许的保留时间（默认为24小时）。 此案例是暂时性的，不会导致数据损坏。 要恢复，应使用oak-run工具确认异常的瞬态性质（oak-run检查不应报告任何错误）。 为此，需要使实例脱机并在之后重新启动。</li>
     <li>外部事件导致磁盘上的数据损坏。 这可能是磁盘故障、磁盘空间不足或所需数据文件的意外修改。 在这种情况下，实例需要脱机并使用oak-run检查进行修复。 有关如何执行oak-run检查的更多详细信息，请阅读以下<a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache文档</a>。</li>
     <li>所有其他事件都应通过<a href="https://helpx.adobe.com/cn/marketing-cloud/contact-support.html" target="_blank">Adobe客户关怀</a>解决。</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 根据错误消息进行故障排除{#troubleshooting-based-on-error-messages}

如果在在线修订清理过程中发生事件，error.log将是详细的。 下表旨在说明最常见的报文并提供可能的解决方案：

| **阶段** | **日志消息** | **说明** | **后续步骤** |
|---|---|---|---|
|  |  |  |  |
| 估计 | TarMK GC #2:由于压缩暂停，因此跳过了估计 | 当通过配置在系统上禁用压缩时，会跳过估计阶段。 | 启用联机修订版清理。 |
|  | TarMK GC #2:估计中断：${REASON}。 正在跳过压缩。 | 估计阶段提前终止。 可能会中断估计阶段的事件的一些示例：主机系统内存或磁盘空间不足。 | 取决于给定的原因。 |
| 压缩 | TarMK GC #2:压缩暂停 | 只要按配置暂停压缩阶段，就不会执行估计阶段或压缩阶段。 | 启用联机修订版清理。 |
|  | TarMK GC #2:压缩已取消：${REASON}。 | 压缩阶段提前终止。 可能会中断压缩阶段的事件的一些示例：主机系统内存或磁盘空间不足。 此外，还可以通过关闭系统或通过管理界面（如操作仪表板中的维护窗口）明确取消压缩来取消压缩。 | 取决于给定的原因。 |
|  | TarMK GC #2:5次循环后，压实在32.902分钟(1974140毫秒)内失败 | 此消息并不表示存在无法恢复的错误，但只有经过一定的尝试后才终止压缩。 另请阅读[下段](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)。 | 请阅读以下[Oak文档](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes)以及[运行在线修订清理](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup)部分的最后一个问题。 |
| 清理 | TarMK GC #2:清理中断 | 通过关闭存储库已取消清理。 预计不会影响一致性。 此外，磁盘空间很可能不会完全回收。 它将在下一个修订清理周期中回收。 | 调查为何关闭了存储库，并在以后尝试避免在维护时段关闭存储库。 |

## 如何运行脱机修订版清理{#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>需要使用不同版本的Oak-run工具，具体取决于您在AEM安装中使用的Oak版本。 在使用该工具之前，请查看下面的版本要求列表：
>
>* 对于Oak版本&#x200B;**1.0.0至1.0.11**&#x200B;或&#x200B;**1.1.0至1.1.6**，请使用Oak-run版本** 1.0.11**
   >
   >
* 对于比上述&#x200B;**更新的Oak版本**，请使用与AEM安装的Oak核心相匹配的Oak-run版本。

>



Adobe提供了一个名为&#x200B;**Oak-run**&#x200B;的工具，用于执行修订清理。 可在以下位置下载该文件：

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

该工具是一个可运行的Jar，可手动运行以压缩存储库。 该过程称为脱机修订版清理，因为需要关闭存储库才能正确运行该工具。 确保根据维护窗口规划清理。

有关如何提高清理过程性能的提示，请参阅[提高脱机修订版清理的性能](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup)。

>[!NOTE]
>
>您还可以在进行维护之前清除旧的检查点（下面步骤中的步骤2和3）。 仅建议对于具有100个以上检查点的实例执行此操作。

1. 请务必确保您最近备份了AEM实例。

   关闭AEM。

1. （可选）使用工具查找旧检查点：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. （可选）然后，删除未引用的检查点：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. 运行压缩并等待其完成：

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### 提高脱机修订版清理的性能{#increasing-the-performance-of-offline-revision-cleanup}

oak-run工具引入了几项功能，旨在提高修订清理过程的性能，并尽可能减少维护时间。

该列表包括若干命令行参数，如下所述：

* **-mmap。** 您可以将其设置为true或false。如果设置为true，则使用内存映射访问。 如果设置为false，则使用文件访问。 如果未指定，则在64位系统上使用内存映射访问，在32位系统上使用文件访问。 在Windows上，将始终强制执行常规文件访问，并忽略此选项。 **此参数已替换 — Dtar.memoryMapped参数。**

* **-Dupdate.limit**。定义将临时事务刷新到磁盘的阈值。 默认值为 10000。

* **-Dcompress-interval**。压缩当前映射之前要保留的压缩映射条目数。 默认为 1000000。如果有足够的堆内存可用，则应将此值增加到更高的数字，以便提高吞吐量。 **此参数已在Oak版本1.6中删除，但无效。**

* **-Dcompytion-progress-log**.将记录的压缩节点数。 默认值为150000，这表示在操作期间将记录150000紧的节点。 将此参数与下面介绍的下一个参数结合使用。

* **-Dtar.PersistCompontationMap。** 将此参数设置为true可使用磁盘空间而不是堆内存来保留压缩映射。需要oak-run工具&#x200B;**版本1.4**&#x200B;及更高版本。 有关更多详细信息，请参阅[脱机修订版清理常见问题解答](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions)部分中的问题3。 **此参数已在Oak版本1.6中删除，但无效。**

* **-force。** 强制压缩并忽略不匹配的区段存储版本。

>[!CAUTION]
>
>使用`--force`参数会将区段存储升级到最新版本，该版本与旧版Oak不兼容。 此外，还要考虑到，不可能降级。 通常，您应谨慎使用这些参数，并且仅当您知道如何使用这些参数时才应如此。

正在使用的参数的示例：

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 触发修订清理的其他方法{#additional-methods-of-triggering-revision-cleanup}

除了上述方法之外，您还可以使用JMX控制台触发修订清理机制，如下所示：

1. 转到[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)打开JMX控制台
1. 单击&#x200B;**RevisionGarbageCollection** MBean。
1. 在下一个窗口中，单击&#x200B;**startRevisionGC()**，然后单击&#x200B;**调用**&#x200B;以启动修订版垃圾收集作业。

### 脱机修订版清理常见问题解答{#offline-revision-cleanup-frequently-asked-questions}

<table>
 <tbody>
  <tr>
   <td><strong>哪些因素决定了离线修订清理的持续时间？</strong></td>
   <td><p>存储库大小和需要清理的修订量决定了清理的持续时间。</p> </td>
  </tr>
  <tr>
   <td><strong>修订版本与页面版本之间有何区别？</strong></td>
   <td>
    <ul>
     <li><strong>Oak修订版本：</strong> Oak将所有内容组织在一个由节点和属性组成的大型树层次结构中。此内容树的每个快照或修订都不可更改，并且对该树所做的更改将以新修订的序列表示。 通常，每次内容修改都会触发新修订。 另请参阅<a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank">跟踪链接</a>。</li>
     <li><strong>页面版本：</strong> 版本控制可创建页面在特定时间点的“快照”。通常，在激活页面时会创建新版本。 有关更多信息，请参阅<a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">使用页面版本</a>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>如果脱机修订版清理任务在8小时内未完成，如何加速该任务？</strong></td>
   <td>如果修订任务在8小时内未完成，且<a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">线程转储</a>显示主热点为<code>InMemoryCompactionMap.findEntry</code>，请在oak-run工具<strong>版本1.4 </strong>或更高版本中使用以下参数：<code>-Dtar.PersistCompactionMap=true</code>。 请注意，<code>-Dtar.PersistCompactionMap</code>参数已在Oak版本1.6中删除。</td>
  </tr>
 </tbody>
</table>
