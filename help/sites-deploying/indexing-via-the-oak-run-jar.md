---
title: 通过Oak-run Jar索引
seo-title: Indexing via the Oak-run Jar
description: 了解如何通过Oak-run Jar执行索引。
seo-description: Learn how to perform indexing via the Oak-run Jar.
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
source-git-commit: c61bf629e35db848c3f2f88c6c7e1dd3b7074b1c
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# 通过Oak-run Jar索引 {#indexing-via-the-oak-run-jar}

Oak-run支持命令行上的所有索引用例，而无需从JMX级别操作。 Oak-run方法的优点是：

1. 它是适用于AEM 6.4的新索引工具集
1. 它缩短了重新索引的时间，这有益地影响了大型存储库的重新索引时间
1. 它减少了在AEM中重新索引期间的资源消耗，从而为其他AEM活动带来更好的系统性能
1. Oak-run提供带外支持：如果生产条件不允许在生产实例上运行重新索引，则可以使用克隆的环境进行重新索引，以避免对性能产生关键影响。

在下面，您将找到在通过执行索引操作时可利用的用例列表 `oak-run` 工具。

## 索引一致性检查 {#indexconsistencychecks}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [用例1 — 索引一致性检查](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`快速确定Lucene oak索引是否已损坏。
* 在使用中的AEM实例上运行以进行一致性检查级别1和2是安全的。

![索引一致性检查](assets/screen_shot_2017-12-14at135758.png)

## 索引统计 {#indexstatistics}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [用例2 — 索引统计](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` 转储用于离线分析的所有索引定义、重要索引统计资料和索引内容。
* 在使用中的AEM实例上执行安全。

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## 重新索引方法决策树 {#reindexingapproachdecisiontree}

此图表是一个决策树，用于确定何时使用各种重新索引方法。

![oak_-_riendingwithoak run](assets/oak_-_reindexingwithoak-run.png)

## 重新索引MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [用例3 — 重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### SegmentNodeStore和DocumentNodeStore的文本预提取 {#textpre-extraction}

[文本预提取](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (AEM 6.3中已有的一项功能)可用于缩短重新编入索引的时间。 文本预提取可以与所有重新索引方法结合使用。

根据 `oak-run.jar` 索引方法在下图中的“执行重新索引”步骤的任一侧都有各种步骤。

![SegmentNodeStore和DocumentNodeStore的文本预提取](assets/4.png)

>[!NOTE]
>
>橙色表示AEM必须位于维护窗口中的活动。

### 使用oak-run.jar为MongoMK或RDBMK联机重新索引 {#onlinere-indexingformongomk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [重新索引 — DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

这是重新索引MongoMK（和RDBMK）AEM安装的推荐方法。 不应使用其他方法。

此进程只需对群集中的单个AEM实例执行。

![使用oak-run.jar为MongoMK或RDBMK联机重新索引](assets/5.png)

## 重新索引TarMK {#re-indexingtarmk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **冷备用注意事项(TarMK)**

   * 冷备无特殊考虑；冷备用实例将照常同步更改。

* **AEM发布场（AE发布场应始终为TarMK）**

   * 对于发布场，需要对所有OR执行步骤，然后在单个发布上为其他OR执行设置(在克隆AEM实例时采取所有常规步骤);sling.id — 应链接到此处的某些内容)

### TarMK的在线索引 {#onlinere-indexingfortarmk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [联机重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

这是引入oak-run.jar的新索引功能之前使用的方法。 可以通过设置 `reindex=true` 属性。

如果客户可以接受索引的时间和性能影响，则可以使用此方法。 中小型AEM安装通常会出现这种情况。

![TarMK的在线索引](assets/6.png)

### 使用oak-run.jar在线重新索引TarMK {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [联机重新索引 — SegmentNodeStore -AEM实例正在运行](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

使用oak-run.jar在线重新索引TarMK的速度比 [TarMK的在线索引](#onlinere-indexingfortarmk) 如上所述。 但是，在维护时段内也需要执行；提及窗口将缩短，需要执行更多步骤来重新索引。

>[!NOTE]
>
>橙色表示必须在维护期间执行AEM的操作。

![使用oak-run.jar在线重新索引TarMK](assets/7.png)

### 使用oak-run.jar离线重新索引TarMK {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [联机重新索引 — SegmentNodeStore - AEM实例已关闭](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

离线重新索引TarMK是最简单的方法 `oak-run.jar` 基于索引的TarMK方法，因为它需要单个 `oak-run.jar` 注释。 但是，它要求关闭AEM实例。

>[!NOTE]
>
>红色表示必须关闭AEM的操作。

![使用oak-run.jar离线重新索引TarMK](assets/8.png)

### 使用oak-run.jar在带外重新索引TarMK  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [带外重新索引 — SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

带外重新索引可最大限度地减少重新索引对使用中AEM实例的影响。

>[!NOTE]
>
>红色表示AEM可能被关闭的操作。

![使用oak-run.jar在带外重新索引TarMK](assets/9.png)

## 更新索引定义 {#updatingindexingdefinitions}

>[!NOTE]
>
>有关此方案的更多详细信息，请参阅 [用例4 — 更新索引定义](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### 在TarMK上使用ACS Ensure Index创建和更新索引定义 {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Ensure Index是社区支持的项目，不受Adobe支持。

这允许通过内容包发送索引定义，稍后会通过将重新索引标记设置为 `true`. 这适用于重新索引不需要很长时间的较小设置。

有关更多信息，请参阅 [ACS Ensure Index文档](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 以了解详细信息。

### 使用oak-run.jar在TarMK上创建和更新索引定义 {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

如果使用非索引重新索引的时间或性能影响 `oak-run.jar` 方法过高，请执行以下操作 `oak-run.jar` 基于的方法可用于在基于TarMK的AEM安装中导入和重新索引Lucene索引定义。

![使用oak-run.jar在TarMK上创建和更新索引定义](assets/10.png)

### 使用oak-run.jar在MonogMK上创建和更新索引定义 {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

如果使用非索引重新索引的时间或性能影响 `oak-run.jar` 方法过高，请执行以下操作 `oak-run.jar` 在基于MongoMK的AEM安装中，可使用基于的方法导入和重新索引Lucene索引定义。

![使用oak-run.jar在MonogMK上创建和更新索引定义](assets/11.png)
