---
title: 修订版清理
description: 了解如何使用Adobe Experience Manager 6.5中的修订清理功能。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
feature: Configuring
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '5811'
ht-degree: 0%

---

# 修订版清理{#revision-cleanup}

## 简介 {#introduction}

存储库的每次更新都会创建一个内容修订版本。 因此，每次更新后，存储库的大小都会增大。 必须清理旧修订版本以释放磁盘资源 — 这对于避免不受控制的存储库增长非常重要。 此维护功能称为修订版清理。 自Adobe Experience Manager (AEM) 6.0起，它就作为离线例程提供。

在AEM 6.3及更高版本中，引入了此功能的在线版本，称为“在线修订清理”。 与必须关闭AEM实例的“脱机修订版清理”相比，在AEM实例处于联机状态时，可以运行“联机修订版清理”。 默认情况下，“联机修订清理”处于打开状态，建议使用此方式执行修订清理。

**注意**： [观看视频](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/administration/use-online-revision-clean-up.html?lang=en) 介绍以及如何使用在线修订清理。

修订清理过程包括三个阶段： **估计**， **压缩**、和 **clean up**. 估算根据可能收集到的垃圾量来确定是否运行下一阶段（压缩）。 在压缩阶段，区段和tar文件被重写，而没有任何未使用的内容。 然后，清理阶段将删除旧区段，包括这些区段可能包含的任何垃圾。 脱机模式通常可以回收更多空间，因为联机模式必须考虑AEM工作集，该工作集不会收集额外的区段。

有关修订版清理的更多详细信息，请参阅以下链接：

* [如何运行联机修订清理](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [联机修订清理常见问题解答](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [如何运行脱机修订版清理](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

此外，您还可以阅读 [Oak官方文档](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html).

### 何时使用联机修订版清理，而不是脱机修订版清理？ {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**建议使用“联机修订版清理”来执行修订版清理。** 离线修订清理只能在例外情况下使用，例如，在迁移到新存储格式之前，或者如果Adobe客户关怀部门要求您这样做时。

## 如何运行联机修订清理 {#how-to-run-online-revision-cleanup}

默认情况下，在线修订清理配置为在AEM Author和Publish实例上每天自动运行一次。 您只需在用户活动最少的时段内定义维护时段。 您可以按如下方式配置“联机修订版清理”任务：

1. 在AEM主窗口中，转到 **工具 — 操作 — 功能板 — 维护** 或将浏览器指向： `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 将鼠标悬停在 **每日维护窗口** 然后单击 **设置** 图标。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 输入所需的值（重复周期、开始时间、结束时间），然后单击 **保存**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

或者，如果要手动运行修订清理任务，您可以：

1. 转到 **工具 — 操作 — 功能板 — 维护** 或直接浏览到 `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 单击 **每日维护窗口**.
1. 将鼠标悬停在 **修订版清理** 图标。
1. 单击 **运行**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 在脱机修订版清理后运行联机修订版清理 {#running-online-revision-cleanup-after-offline-revision-cleanup}

修订清理过程按层代回收旧修订。 这意味着每次运行修订清理时，都会在磁盘上创建并保留新一代。 但是，这两种类型的修订清理之间存在区别：脱机修订清理保留一代，而联机修订清理保留两代。 因此，当您运行在线修订清理时 **之后** 离线修订清理：

1. 在首次运行联机修订版清理后，存储库大小会翻倍。 之所以会出现这种情况，是因为现在磁盘上保留了两代数据。
1. 在后续运行期间，存储库将在创建新一代时暂时增大，然后稳定到首次运行后的大小，因为在线修订清理过程将回收前一代版本。

此外，请记住，根据提交的类型和数量，每一代都可以与上一代相比大小不同，因此最终大小可以因运行而异。

因此，建议磁盘大小至少比最初估计的存储库大小大两到三倍。

## 全压实模式和尾压实模式  {#full-and-tail-compaction-modes}

**AEM 6.5** 介绍 **两种新模式** 对于 **压缩** 在线修订版清理流程的阶段：

* 此 **完全压缩** 模式会重写整个存储库中的所有区段和tar文件。 因此，后续清理阶段可以清除整个存储库中的最大垃圾量。 由于完全压缩会影响整个存储库，因此它需要大量系统资源和时间才能完成。 完全压实对应于AEM 6.3中的压实阶段。
* 此 **尾压缩** 模式仅重写存储库中最近的区段和tar文件。 最新的区段和tar文件是自上次运行完全或尾部压缩以来添加的区段。 因此，随后的清理阶段只能清除存储库最近部分中包含的垃圾。 由于尾部压缩仅影响存储库的一部分，因此它比完全压缩需要更少的系统资源和完成时间。

这些压实方式构成了效率与资源消耗之间的权衡：尾压实效果较差，对系统正常运行的影响也较小。 相比之下，完全压实更有效，但对系统正常运行的影响更大。

AEM 6.5还在压缩期间引入了更有效的内容去重机制，从而进一步减少了存储库在磁盘上的占用空间。

以下两张图表显示了内部实验室测试的结果，这些结果说明了与AEM 6.3相比，AEM 6.5中减少了平均执行时间以及磁盘上的平均占用空间：

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 如何配置完全压缩和尾压缩 {#how-to-configure-full-and-tail-compaction}

默认配置在工作日运行尾压缩，在星期日运行完全压缩。 可以使用新的配置值更改默认配置 `full.gc.days` 的 `RevisionCleanupTask` [维护任务](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

当您配置 `full.gc.days` 值，完全压缩在值中定义的天数内运行，尾压缩在值中未定义的天数内运行。 例如，如果将完全压缩配置为在星期日运行，则尾压缩从星期一到星期六运行。 例如，如果将完全压缩配置为一周的每天运行，则尾部压缩根本不会运行。

此外，请考虑：

* **尾压缩** 效率较低，且对系统正常运行的影响较小。 因此，它打算在工作日运行。
* **完全压缩** 不仅效率较高，而且对系统正常运行的影响也较大。 因此打算在工作日使用。
* 尾部压缩和完全压缩都应安排在非高峰时段运行。

### 疑难解答 {#troubleshooting}

使用新的压缩模式时，请牢记以下事项：

* 您可以监视输入/输出(I/O)活动，例如：I/O操作、等待IO的CPU、提交队列大小。 这有助于确定系统是否正在进行I/O绑定并需要升级。
* 此 `RevisionCleanupTaskHealthCheck` 指示联机修订版清理的整体运行状况状态。 它的工作方式与AEM 6.3中相同，并且不区分完全压实和尾压实。
* 日志消息包含有关压缩模式的相关信息。 例如，当“联机修订清理”启动时，相应的日志消息将指示压缩模式。 此外，在某些角落情况下，当计划运行尾压缩时，系统恢复为完全压缩，并且日志消息指示此更改。 以下日志示例指示压缩模式以及从尾到完全压缩的更改：

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 已知限制 {#known-limitations}

有时候，在尾部模式和完全压实模式之间切换会延迟清理过程。 更准确地说，存储库在完全压缩（其大小翻了一番）后将会增长。 当存储库低于完全压缩前的大小时，在后续的尾压缩中回收额外的空间。 还应避免执行并行维护任务。

**建议磁盘大小至少比最初估计的存储库大小大两到三倍。**

## 联机修订清理常见问题解答 {#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5升级注意事项 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>问题 </td>
   <td>答案</td>
  </tr>
  <tr>
   <td>升级到AEM 6.5时应该了解什么？</td>
   <td><p>TarMK的持久性格式随AEM 6.5而变化。这些更改不需要主动迁移步骤。 现有存储库会经历滚动迁移，这对于用户是透明的。 首次访问AEM 6.5（或相关工具）存储库时，将启动迁移过程。</p> <p><strong>迁移到AEM 6.5持久性格式后，存储库无法恢复为以前的AEM 6.3持久性格式。</strong></p> </td>
  </tr>
 </tbody>
</table>

### 迁移到Oak区段Tar {#migrating-to-oak-segment-tar}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为什么需要迁移存储库？</strong></td>
   <td><p>在AEM 6.3中，需要对存储格式进行更改，特别是为了提高在线修订清理的性能和效率。 这些更改无法向后兼容，必须迁移使用旧Oak区段(AEM 6.2及更低版本)创建的存储库。</p> <p>更改存储格式的其他好处：</p>
    <ul>
     <li>更好的可扩展性（优化的区段大小）。</li>
     <li>更快 <a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">数据存储垃圾收集</a>.<br /> </li>
     <li>为未来的增强功能做基础工作。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否仍支持以前的Tar格式？</strong></td>
   <td>AEM 6.3或更高版本仅支持新的Oak区段Tar。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>内容迁移是否始终是强制性的？</strong></td>
   <td>是。除非从新的实例开始，否则将始终需要迁移内容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>我是否可以升级到6.3或更高版本，并稍后进行迁移（例如，使用其他维护时段）？</strong></td>
   <td>否，如上所述，内容迁移是强制性的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>迁移时能否避免停机？</strong></td>
   <td>否. 这是一次性工作，无法在正在运行的实例上完成。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果意外地针对错误的存储库格式运行，会发生什么情况？</strong></td>
   <td>如果您尝试对oak-segment-tar存储库运行oak-segment模块（或反之），启动会失败 <em>IllegalstateException</em> 并显示“区段格式无效”消息。 没有发生数据损坏。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否需要重新索引搜索索引？</strong></td>
   <td>否. 从oak-segment迁移到oak-segment-tar会引入容器格式的更改。 包含的数据不受影响，也不会被修改。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最好地计算迁移期间和迁移后所需的预期磁盘空间？</strong></td>
   <td>迁移等同于以新格式重新创建区段存储。 这可用于估计迁移期间所需的额外磁盘空间。 迁移后，可以删除旧区段存储以回收空间。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最好地估计迁移的持续时间？</strong></td>
   <td>在以下情况下，迁移性能可大大提高 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">脱机修订版清理</a> 在迁移之前执行。 建议所有客户在升级过程中先执行此步骤。 通常，迁移的持续时间应与脱机修订清除任务的持续时间相似，假定已在迁移之前执行了脱机修订清除任务。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 正在运行联机修订版清理 {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>问题</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>应多久执行一次联机修订清理？</strong></td>
   <td>每日一次. 这是操作功能板中的默认配置。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何配置联机修订清理维护任务的开始时间？</strong></td>
   <td>请参阅 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">如何运行联机修订清理</a> 部分。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否存在不应当超出联机修订版清理的最大频率？</strong></td>
   <td>建议每天运行一次在线修订清理，如默认配置。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些关键指标决定了运行联机修订清除的频率？</strong></td>
   <td>无需确定频率，因为“在线修订清理”配置为维护任务，并且每天自动运行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>首次运行联机修订清理时，为何不回收任何空间？</strong></td>
   <td>联机修订版清理可按层代回收旧修订版。 每次运行修订清理时都会生成新的生成。 只有至少两代的内容才会被回收，这意味着，第一次回收时没有任何可回收的内容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在脱机修订版清理后运行首次联机修订版清理时，为何不回收任何空间？</strong></td>
   <td><p>脱机修订清理正在回收除最新一代以外的所有内容，而联机修订清理则使用最新两代。 如果存在新的存储库，则联机修订版清理在脱机修订版清理后首次执行时不会回收任何空间，因为没有足够旧的层代可以回收。</p> <p>此外，请参阅的“脱机修订版清理后运行联机修订版清理”部分 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">本章</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>“创作”和“发布”通常会有不同的“在线修订清理”窗口吗？</strong></td>
   <td>这取决于办公时间和客户在线状态的流量模式。 维护窗口应在主生产时间之外进行配置，以实现最佳的清理效果。 对于多个AEM Publish实例（TarMK场），用于在线修订版清理的维护窗口应交错进行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行在线修订版清理之前是否有任何先决条件？</strong></td>
   <td><p>只有AEM 6.3及更高版本才提供联机修订版清理。 此外，如果您使用的是较低版本的AEM，则必须迁移到新的 <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak段Tar</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些因素决定了联机修订版清理的持续时间？</strong></td>
   <td>这些因素包括：<br />
    <ul>
     <li>存储库大小</li>
     <li>在系统上加载（每分钟请求数，特别是写操作）</li>
     <li>活动模式（读取与写入）</li>
     <li>硬件规格（CPU性能、内存、IOPS）</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行在线修订清理时，作者是否仍可工作？</strong></td>
   <td>可以，联机修订清理可以处理并发写入。 但是，“在线修订清理”无需并发写入事务即可更快速、更高效地工作。 Adobe建议将“在线修订清理”维护任务安排在相对安静的时间，不会有大量流量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行联机修订清理时，对磁盘空间和栈内存的最低要求是什么？</strong></td>
   <td><p>在联机修订清理期间，会持续监视磁盘空间。 如果可用磁盘空间下降到临界值以下，则该过程将取消。 关键值是存储库当前磁盘占用空间的25%，无法对其进行配置。</p> <p><strong>Adobe建议磁盘大小至少比最初估计的存储库大小大两到三倍。</strong></p> <p>在清理过程中，会持续监控可用栈空间。 如果可用栈空间下降到临界值以下，则取消该进程。 临界值通过org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD配置。 默认值为15%。</p> <p>Recommendations的最小压缩栈大小与AEM内存大小调整建议没有区分。 一般而言： <strong>如果AEM实例的大小足以处理用例及其上的预期有效负载，则清理过程将获得足够的内存。</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>运行联机修订清理时预期的性能影响是什么？</strong></td>
   <td>在线修订版清理是一个后台进程，它同时从存储库读取和写入到正常系统操作。 特别是，它可能需要在短时间内获得对存储库的独占访问权限，以防止其他线程写入存储库。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>预计联机修订清理运行多长时间？</strong></td>
   <td>根据内部执行的最新性能测试Adobe，运行时间不应超过两个小时。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果在线修订清理需要较长时间，应该怎么做？</strong></td>
   <td>
    <ul>
     <li>确保每天执行该语句。<br /> </li>
     <li>通过相应地配置操作仪表板中的维护窗口，确保在最小的存储库活动期间执行该操作。</li>
     <li>扩展系统资源（CPU、内存、I/O）。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果联机修订清理超出配置的维护窗口，会发生什么情况？</strong></td>
   <td>确保其他维护任务不会延迟执行。 如果在同一维护窗口中执行比“联机修订清理”更多的维护任务，则可能会出现这种情况。 维护任务按顺序运行，没有可配置的顺序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>为何跳过修订垃圾收集？</strong></td>
   <td><p>修订清理依赖估计阶段来确定是否有足够的垃圾要清理。 估算器将当前大小与上次压缩后的存储库大小进行比较。 如果大小超过配置的增量，则运行清理。 大小增量设置为1 GB。 这实际上意味着，如果自上次清理运行以来，存储库大小没有增加1 GB，则会跳过新的修订版清理迭代。 </p> <p>以下为估计阶段的相关日志条目：</p>
    <ul>
     <li>修订版GC运行： <em>大小增量为N%或N/N （N/N字节），因此正在运行压缩</em></li>
     <li>修订GC会 <strong>非</strong> 运行： <em>大小增量为N%或N/N （N/N字节），因此现在将跳过压缩</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果性能影响太大，是否可以安全地中止自动压缩？</strong></td>
   <td>是。自AEM 6.3起，可通过“操作功能板”中的“维护任务窗口”或通过JMX安全地停止它。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果AEM实例在计划的清理任务期间关闭，进程是否安全中止，或者是否在压缩完成之前阻止关闭？</strong></td>
   <td>修订清理被中断，存储库将安全关闭。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在联机修订版清理期间系统崩溃时会发生什么情况？</strong></td>
   <td>在这种情况下，不存在数据损坏的风险。 后续运行将清理垃圾剩余。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>不运行联机修订清理会有什么影响？</strong></td>
   <td>性能会随着时间的推移而降低。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>正在收集哪些修订？</strong></td>
   <td>默认情况下，“联机修订清理”仅收集至少24小时之前的修订。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果并行写入存储库的干扰过多，会发生什么情况？</strong></td>
   <td><p>如果系统中存在写并发，联机修订版清理可能需要独占写入权限，才能在压缩周期结束时提交更改。 系统进入 <strong>forceCompact模式</strong>，详见 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">Oak文档</a>. 在强制压缩期间，获得排他性写锁定以最终提交更改，而不受任何并行写干扰。 要限制对响应时间的影响，可以定义超时值。 默认情况下，此值设置为1分钟，这意味着如果强制压缩未在一分钟内完成，则压缩过程将中止，以支持并发提交。</p> <p>力压缩的持续时间取决于以下因素：</p>
    <ul>
     <li>硬件：特定于IOPS。 持续时间会随着IOPS的增加而缩短。</li>
     <li>区段存储大小：持续时间会随着区段存储的大小而增加。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何在备用实例上执行联机修订清理？</strong></p> </td>
   <td><p>在冷备用设置中，只有主实例必须配置为运行在线修订清理。 在备用实例上，无需特别计划联机修订版清理。</p> <p>备用实例上的相应操作是“自动清理” — 这与“在线修订清理”的清理阶段相对应。 在主实例上执行联机修订版清理后，在备用实例上运行自动清理。</p> <p>估算和压缩阶段不会在备用实例上运行。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>脱机修订版清理是否可以比“联机修订版清理”释放更多的磁盘空间？</strong></td>
   <td><p>脱机修订版清理可以立即删除旧修订，而联机修订版清理必须考虑应用程序栈栈仍在引用的旧修订。 因此，前者可以比后者更积极地去除垃圾，其效果在几个垃圾收集循环过程中被摊销。</p> <p>此外，请参阅的“脱机修订版清理后运行联机修订版清理”部分 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">本章</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>有关内存映射文件操作的任何注意事项？</td>
   <td>
    <ul>
     <li><strong>在Windows环境中</strong>，将始终强制进行常规文件访问，以免使用内存映射访问。 作为一般建议，应将所有可用的RAM分配给栈，并增加segmentCache大小。 您可以通过将segmentCache.size选项添加到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config来增加segmentCache(例如，segmentCache.size=20480)。 切记不要为操作系统和其他进程留出一些RAM。</li>
     <li><strong>在非Windows环境中</strong>，增加物理内存的大小以改进存储库的内存映射。</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 监视联机修订版清理 {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>在联机修订清理期间必须监视哪些内容？</strong></td>
   <td>
    <ul>
     <li>启用“联机修订清理”后，应监视磁盘空间。 清理不会运行，或者在磁盘空间不足时提前终止。</li>
     <li>检查联机修订版清理的完成时间日志。 此过程不应超过2个小时。</li>
     <li>检查点数。 如果在压缩运行时有3个以上的检查点，建议清理检查点。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检查联机修订清理是否已成功完成？</strong></td>
   <td><p>您可以通过检查日志来检查联机修订清理是否成功完成。</p> <p>例如，“<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>“表示压缩步骤已成功完成，除非在消息前面”<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>“，这意味着并发负载过多。</p> <p>相应地，还有一条消息“<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>”表示成功完成清理步骤。</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>可在何处找到上次联机修订清理执行的统计信息？</strong></td>
   <td><p>状态、进度和统计信息通过JMX公开(<code>SegmentRevisionGarbageCollection</code> MBean)。 欲知关于 <code>SegmentRevisionGarbageCollection</code> MBean，阅读 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">以下段落</a>.</p> <p>可以通过跟踪进度 <code>EstimatedRevisionGCCompletion</code> 的属性 <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>可以使用获取MBean的引用 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>统计信息仅在上次系统启动后可用。 可以使用外部监控工具将数据保留在AEM正常运行时间之外。 请参阅 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">有关将运行状况检查附加到Nagios的AEM文档，作为外部监控工具的示例</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些是相关的日志条目？</strong></td>
   <td>
    <ul>
     <li>联机修订清理已启动/停止
      <ul>
       <li>在线修订清理由三个阶段组成：估算、压缩和清理。 如果存储库未包含足够的垃圾，则估算可能会强制跳过压缩和清理。 在最新版本的AEM中，消息为“<code>TarMK GC #{}: estimation started</code>”标记估算的开头，“<code>TarMK GC #{}: compaction started, strategy={}</code>”表示压缩的开头，而“T”<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>”标记清理的开始。</li>
      </ul> </li>
     <li>通过修订清理获得的磁盘空间
      <ul>
       <li>仅在清理阶段完成时才回收空间。 清理阶段的结束用日志消息“T”标记<code>arMK GC #{}: cleanup completed in {} ({} ms</code>“。 后清理大小为 {} ({} 字节)和回收的空间 {} ({} 字节)。 压缩图粗细/深度为 {}/{} ({} 字节/{})。”。</li>
      </ul> </li>
     <li>修订清理期间出现问题
      <ul>
       <li>有许多故障情况，它们都标有WARN或ERROR日志消息，以“TarMK GC”开头。</li>
      </ul> </li>
    </ul> <p>另外，请参见 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">基于错误消息的故障排除</a> 部分。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检查联机修订清理完成后回收了多少空间？</strong></td>
   <td>在清理周期结束时，日志中会显示一条消息：“<code>TarMK GC #3: cleanup completed</code>”包括存储库的大小和回收的垃圾量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在线修订清理完成后，如何检查存储库的完整性？</strong></td>
   <td><p>联机修订清理后不需要存储库完整性检查。 </p> <p>但是，您可以执行以下操作来检查清理后的存储库状态：</p>
    <ul>
     <li>存储库 <a href="/help/sites-deploying/consistency-check.md" target="_blank">遍历检查</a></li>
     <li>在清理过程完成后使用oak-run工具检查是否存在不一致。 有关如何执行此操作的更多信息，请查看 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache文档。</a> 您无需关闭AEM即可运行该工具。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何检测联机修订清理是否失败，以及要恢复的步骤是什么？</strong></td>
   <td>故障情况由以“TarMK GC”开头的WARN或ERROR日志消息标记。 另外，请参见 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">基于错误消息的故障排除</a> 部分。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>修订清理运行状况检查中会公开哪些信息？ 它们如何以及何时对颜色编码状态级别作出贡献？ </strong></td>
   <td><p>修订清理运行状况检查是 <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">操作功能板</a>.<br /> </p> <p>状态为 <strong>绿色</strong> 上次执行联机修订清除维护任务是否成功完成。</p> <p>它是 <strong>黄色</strong> 如果联机修订版清理维护任务被取消一次。<br /> </p> <p>它是 <strong>红色</strong> 如果连续三次取消了“联机修订清理”维护任务。 <strong>在这种情况下，需要手动交互</strong> 或者，联机修订清理可能会再次失败。 欲知更多信息，请参阅 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">疑难解答</a> 部分。<br /> </p> <p>此外，系统重新启动后，运行状况检查状态也会重置。 因此，新重新启动的实例在修订清理运行状况检查中显示绿色状态。 可以使用外部监控工具将数据保留在AEM正常运行时间之外。 请参阅 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">有关将运行状况检查附加到Nagios的AEM文档，作为外部监控工具的示例</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何在备用实例上监视自动清理？</strong></p> </td>
   <td><p>使用通过JMX公开状态、进度和统计信息 <code>SegmentRevisionGarbageCollection</code> MBean。 另请参阅以下内容 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak文档</a>. </p> <p>可以使用获取MBean的引用 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>统计信息仅自上次系统启动后可用。 可以使用外部监控工具将数据保留在AEM正常运行时间之外。 另请参阅 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">有关将运行状况检查附加到Nagios的AEM文档，作为外部监控工具的示例</a>.</p> <p>日志文件还可用于检查自动清理的状态、进度和统计信息。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>在自动清理待机实例期间必须监视哪些内容？</strong></p> </td>
   <td>
    <ul>
     <li>运行自动清理时应监视磁盘空间。</li>
     <li>完成时间（通过日志）以确保不超过2小时。</li>
     <li>运行自动清理后的区段存储大小。 备用实例上的段存储大小应该与主实例上的段存储大小大致相同。</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 联机修订版清理疑难解答 {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>如果不运行联机修订清理，会出现什么最坏的情况？</strong></td>
   <td>AEM实例的磁盘空间不足，这会导致生产中断。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在发布实例上运行在线修订清理时，高用户流量是否会造成问题？</strong></td>
   <td>高用户流量会影响压缩阶段是否能够成功完成。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>根据运行状况检查和日志条目，联机修订清理连续三次未成功完成。 成功完成联机修订清理需要什么条件？</strong></td>
   <td>您可以采取几个步骤来查找并修复问题：<br />
    <ul>
     <li>首先，检查日志条目<br /> </li>
     <li>根据日志中的信息，采取适当措施：
      <ul>
       <li>如果日志显示五个错过的压缩周期和一个超时，则 <code>forceCompact</code> 周期，将维护时段安排在存储库写入量较少时的安静时间。 您可以在存储库量度监控工具中检查存储库写入，网址为 <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>如果清理在维护时段结束时停止，请确保维护任务用户界面中维护时段的配置足够大</li>
       <li>如果可用的栈内存不足，请确保实例有足够的内存。</li>
       <li>如果反应较晚，则区段存储可能会增长太多，以致于线上修订清理无法在较长的维护时段内完成。 例如，如果上周未成功完成在线修订清理，则建议计划离线维护，并运行离线修订清理，以将区段存储恢复到可管理的大小。</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>启用Healthcheck警报时必须执行哪些操作？</strong></td>
   <td>请参阅上一点。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果在线修订清理在计划的维护时段内超时，会发生什么情况？</strong></td>
   <td>在线修订版清理已取消，剩余的修订版将被删除。 下次安排维护时段时，它将再次启动。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>导致原因 <code>SegmentNotFoundException</code> 要登录的实例 <code>error.log</code> 我该如何恢复？</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> 当TarMK尝试访问其无法找到的存储单元（区段）时，会记录该日志。 有三种情况可能会导致此问题：</p>
    <ol>
     <li>一种应用程序，可绕过建议的访问机制（如Sling和JCR API），使用较低级别的API/SPI访问存储库，然后超过区段的保留时间。 也就是说，它保留对实体的引用，保留时间超过在线修订版清理所允许的保留时间（默认为24小时）。 此案例是暂时性的，不会导致数据损坏。 要恢复，应使用oak-run工具确认异常的瞬态性质（oak-run检查不应报告任何错误）。 为此，实例必须离线并在之后重新启动。</li>
     <li>外部事件导致磁盘上的数据损坏。 这可以是磁盘故障、磁盘空间不足或意外修改所需的数据文件。 在这种情况下，实例必须离线并使用oak-run检查进行修复。 有关如何执行oak-run检查的更多详细信息，请阅读以下内容 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache文档</a>.</li>
     <li>通过，解决所有其他问题 <a href="https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support" target="_blank">Adobe客户关怀</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 基于错误消息的故障排除 {#troubleshooting-based-on-error-messages}

如果在联机修订清理过程中发生事件，则error.log为详细。 以下列表旨在解释最常见的报文并提供可能的解决方案：

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message doesn't mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
| Cleanup |TarMK GC #2: cleanup interrupted |Cleanup has been cancelled by shutting down the repository. No impact on consistency is expected. Also, disk space is most likely not reclaimed to full extent. It will be reclaimed during next revision cleanup cycle. |Investigate why repository has been shut down and going forward try to avoid shutting down the repository during maintenance windows. |-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>阶段</th>
    <th>日志消息</th>
    <th>解释</th>
    <th>后续步骤</th>
  </tr>  
  <tr>
    <td>估计</td>
    <td>TarMK GC #2：由于压缩已暂停，因此跳过了估计。</td>
    <td>当配置在系统上禁用压缩时，将跳过估计阶段。</td>
    <td>启用联机修订版清理。</td>
  </td>
  </tr>
  <tr>
    <td>不适用</td>
    <td>TarMK GC #2：估计中断： ${REASON}. 正在跳过压缩。</td>
    <td>估计阶段提前终止。 可能中断估计阶段的一些事件示例：主机系统上的内存或磁盘空间不足。</td>
    <td>这取决于具体的原因。</td>
  </td>
  </tr>
  <tr>
    <td>压缩</td>
    <td>TarMK GC #2：压缩已暂停。</td>
    <td>只要压实阶段被配置暂停，估计阶段和压实阶段都不会运行。</td>
    <td>启用联机修订清理。</td>
  </td>
  </tr>
   <tr>
    <td>不适用</td>
    <td>TarMK GC #2：压缩已取消： ${REASON}.</td>
    <td>压缩阶段提前结束。 可能中断压缩阶段的一些事件示例：主机系统上的内存或磁盘空间不足。 此外，还可以通过关闭系统或通过管理界面（如操作仪表板中的维护窗口）显式取消系统来取消压缩。</td>
    <td>这取决于具体的原因。</td>
  </td>
  </tr>
  <tr>
    <td>不适用</td>
    <td>TarMK GC #2：经过5次循环，压实时间为32.902 min(1974140 ms)。</td>
    <td>此消息并不表示存在不可恢复的错误，但仅表示压缩在尝试一段时间后终止。 此外，请阅读 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">下段落。</a></td>
    <td>阅读以下内容 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">Oak文档</a>，以及运行联机修订清理部分的最后一个问题。</a></td>
  </td>
  </tr>
  <tr>
    <td>清理</td>
    <td>TarMK GC #2：清理已中断。</td>
    <td>通过关闭存储库已取消清理。 预计一致性不会受到影响。 此外，磁盘空间很可能无法完全回收。 它将在下一个修订版清理周期中被回收。</td>
    <td>调查存储库被关闭的原因，并在以后尝试避免在维护时段关闭存储库。</td>
  </td>
  </tr>
  </tbody>
</table>

## 如何运行脱机修订版清理 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>使用与AEM安装的Oak核心版本匹配的版本号（主要和次要）的Oak-run工具版本。 例如，如果您的AEM实例具有Oak核心版本1.22.x，则您应使用最新版本的Oak-run tool 1.22.x。

Adobe提供了一个工具，名为 **Oak-run** 执行修订清理。 可在以下位置下载它：

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

该工具是一个可运行的jar，可以手动运行以压缩存储库。 此过程称为脱机修订版清理，因为必须关闭存储库才能正确运行该工具。 请确保根据您的维护时段计划清理。

有关如何提高清理过程性能的提示，请参阅 [提高脱机修订清理的性能](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>您还可以在进行维护之前清除旧检查点（以下过程中的步骤2和3）。 建议仅对具有100个以上检查点的实例执行此操作。

1. 始终确保您有AEM实例的最新备份。

   关闭AEM。

1. （可选）使用该工具查找旧检查点：

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

### 提高脱机修订清理的性能 {#increasing-the-performance-of-offline-revision-cleanup}

oak-run工具引入了多种功能，旨在提高修订清理过程的性能，并尽可能减少维护窗口。

该列表包括几个命令行参数，如下所述：

* **-mmap。** 您可以将此参数设置为true或false。 如果设置为true，则使用内存映射访问。 如果设置为false，则使用文件访问权限。 如果未指定，则在64位系统上使用内存映射访问，在32位系统上使用文件访问。 在Windows上，始终强制定期访问文件，并且此选项被忽略。 **此参数已替换 — Dtar.memoryMapped参数。**

* **-Dupdate.limit**. 定义将临时事务刷新到磁盘的阈值。 默认值为 10000。

* **-Dcompress间隔**. 在压缩当前映射之前要保留的压缩映射条目数。 默认值为1000000。 如果有足够的栈内存可用，则应该将此值增加到更高的数值，以便提高吞吐量。 **此参数已在Oak版本1.6中删除，没有任何效果。**

* **-Dcompaction-progress-log**. 记录的压缩节点数。 默认值为150000，这意味着在操作期间记录前150000个压缩节点。 将此参数和下面记录的下一个参数一起使用。

* **-Dtar.PersistCompactionMap。** 将此参数设置为true可使用磁盘空间而不是栈内存来保持压缩映射持久性。 需要oak-run工具 **版本1.4** 和更高。 欲知更多详情，请参见 [脱机修订版清理常见问题解答](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) 部分。 **此参数已在Oak版本1.6中删除，没有任何效果。**

* **— 强制。** 强制压缩并忽略不匹配的区段存储版本。

>[!CAUTION]
>
>使用 `--force` 参数可将区段存储升级到最新版本，这与旧版Oak不兼容。 此外，请考虑一下，降级是不可能的。 通常，您应该谨慎使用这些参数，并且仅在您了解如何使用它们时才使用。

正在使用的参数示例：

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 触发修订清理的其他方法 {#additional-methods-of-triggering-revision-cleanup}

除了上述方法之外，您还可以使用JMX控制台触发修订清除机制，如下所示：

1. 打开JMX控制台，方法是： [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. 单击 **RevisionGarbageCollection** MBean。
1. 在下一个窗口中，单击 **startRevisionGC()** 然后 **调用** 以启动修订垃圾收集作业。

### 脱机修订版清理常见问题解答 {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>决定离线修订版清理持续时间的因素是什么？</strong></td>
   <td><p>存储库大小和必须清理的修订版本数决定了清理的持续时间。</p> </td>
  </tr>
  <tr>
   <td><strong>修订版本和页面版本之间有何区别？</strong></td>
   <td>
    <ul>
     <li><strong>Oak修订版：</strong> Oak在由节点和属性组成的大型树层次结构中组织所有内容。 此内容树的每个快照或修订版本都是不可变的，对树所做的更改以一系列新修订版本表示。 通常，每次内容修改都会触发新的修订。 另请参阅 <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> 关注链接</a>.</li>
     <li><strong>页面版本：</strong> 版本控制可在特定的时间点创建页面的“快照”。 通常，在激活页面时会创建新版本。 有关更多信息，请参阅 <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">处理页面版本</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>如果“离线修订清理”任务未在8小时内完成，如何加快该任务的速度？</strong></td>
   <td>如果修订任务未在8小时内完成，并且 <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">线程转储</a> 揭示出主要的热点为 <code>InMemoryCompactionMap.findEntry</code>，在oak-run工具中使用以下参数 <strong>版本1.4 </strong>或更高版本： <code>-Dtar.PersistCompactionMap=true</code>. 此 <code>-Dtar.PersistCompactionMap</code> 参数已在Oak版本1.6中删除。</td>
  </tr>
 </tbody>
</table>
