---
title: 通过Oak-run jar构建索引
seo-title: 通过Oak-run jar构建索引
description: 了解如何通过Oak-run Jar执行索引。
seo-description: 了解如何通过Oak-run Jar执行索引。
uuid: 09a83ab9-92ec-4b55-8d24-2302f28fc2e4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c8a505ab-a075-47da-8007-43645a8c3ce5
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# 通过Oak-run jar构建索引 {#indexing-via-the-oak-run-jar}

Oak-run支持命令行上的所有索引使用案例，无需从JMX级别操作。 Oak-run方法的优势在于：

1. 它是AEM 6.4的新索引编制工具集
1. 它缩短了重新索引的时间，这有益地影响了大型资料库的重新索引时间
1. 它减少了在AEM中重新索引期间的资源消耗，从而提高了其他AEM活动的系统性能
1. Oak-run提供带外支持：如果生产条件不允许在生产实例上运行重新索引，则可以使用克隆的环境进行重新索引以避免关键性能影响。

在下面，您将找到一个使用案例列表，通过该工具执行索引编制操作时可利用这些 `oak-run` 案例。

## 索引一致性检查 {#indexconsistencychecks}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅使用案例1 —— 索引一致性检查](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck)。

* `oak-run.jar`快速确定lucene oak索引是否损坏。
* 在使用中的AEM实例上运行一致性检查级别1和2是安全的。

![screen_shot_2017-12-14at135758](assets/screen_shot_2017-12-14at135758.png)

## 索引统计 {#indexstatistics}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅使用案例2 —— 索引统计](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` 为脱机分析转储所有索引定义、重要索引统计数据和索引内容。
* 在使用中的AEM实例上执行是安全的。

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## 再索引方法决策树 {#reindexingapproachdecisiontree}

此图是决定何时使用各种重新索引方法的决策树。

![oak_-_赖因辛基威特奥克](assets/oak_-_reindexingwithoak-run.png)

## 重新索引MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅使用案例3 —— 重新构建索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)。

### SegmentNodeStore和DocumentNodeStore的文本预提取 {#textpre-extraction}

[文本预提取](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) （AEM 6.3中已存在的一项功能）可用于缩短重新索引的时间。 文本预提取可以与所有重新索引方法结合使用。

根据索引 `oak-run.jar` 方法的不同，在下图的“执行重新索引”步骤的两侧将执行各种步骤。

![4](assets/4.png)

>[!NOTE]
>
>橙色表示AEM必须位于维护窗口中的活动。

### 使用oak-run.jar为MongoMK或RDBMK在线重新构建索引 {#onlinere-indexingformongomk}

>[!NOTE]
>
>有关此方案的详细信息，请参 [阅重新索引- DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore)。

这是重新索引MongoMK（和RDBMK）AEM安装的推荐方法。 不应使用其他方法。

此进程只需对群集中的单个AEM实例执行。

![5](assets/5.png)

## 重新索引TarMK {#re-indexingtarmk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅重新索引- SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore)。

* **Cold Standby注意事项(TarMK)**

   * Cold Standby没有特别的考虑；cold Standby实例将像往常一样同步更改。

* **AEM发布场（AE发布场应始终为TarMK）**

   * 对于发布场，需要为所有对象完成此操作，或在单个发布上执行步骤，然后为其他对象克隆设置(在克隆AEM实例时执行所有常规操作；sling.id —— 应链接到此处的内容)

### TarMK的在线索引 {#onlinere-indexingfortarmk}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅在线重新索引- SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore)。

这是介绍oak-run.jar的新索引功能之前使用的方法。 它可以通过在Oak索引上 `reindex=true` 设置属性来完成。

如果客户可以接受索引的时间和性能影响，则可以使用此方法。 中小型AEM安装通常是这种情况。

![6](assets/6.png)

### 使用oak-run.jar在线重新索引TarMK {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅在线重新索引- SegmentNodeStore - AEM实例正在运行](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning)。

TarMK的在线索引比上面描述的在线TarkMK重新索引更快。 但是，它还需要在维护窗口期间执行，其方法是窗口将更短，并且执行重新索引需要更多步骤。

>[!NOTE]
>
>橙色表示在维护期内必须执行AEM的操作。

![7](assets/7.png)

### 使用oak-run.jar对TarMK进行脱机重新索引 {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅在线重新索引- SegmentNodeStore - AEM实例已关闭](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown)。

TarMK的脱机重新索引是TarMK最简单 `oak-run.jar` 的基于重新索引的方法，因为它需要单个注 `oak-run.jar` 释。 但是，它需要关闭AEM实例。

>[!NOTE]
>
>红色表示必须关闭AEM的操作。

![8](assets/8.png)

### 使用oak-run.jar在带外重新索引TarMK {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅带外重新索引- SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore)。

带外重新索引将重新索引对使用中的AEM实例的影响降至最低。

>[!NOTE]
>
>红色表示AEM可能关闭的操作。

![9](assets/9.png)

## 更新索引定义 {#updatingindexingdefinitions}

>[!NOTE]
>
>有关此方案的更多详细信息，请参 [阅使用案例4 —— 更新索引定义](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions)。

### 使用ACS Ensure Index在TarMK上创建和更新索引定义 {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Ensure index是社区支持的项目，Adobe支持部门不支持它。

这允许通过内容包进行索引定义，稍后通过将重新索引标志设置为来重新索引将导致重新索引 `true`。 这适用于重新构建索引不需要很长时间的较小设置。

有关详细信息，请参阅 [ACS Ensure Index文档](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 。

### 使用oak-run.jar在TarMK上创建和更新索引定义 {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

如果使用非方法重新索引的时间或性能影响过 `oak-run.jar` 大，则可以使用以下基于方法 `oak-run.jar` 来导入和重新索引基于TarMK的AEM安装中的Lucene索引定义。

![10](assets/10.png)

### 使用oak-run.jar在MonogMK上创建和更新索引定义 {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

如果使用非方法重新索引的时间或性能影响 `oak-run.jar``oak-run.jar` 过大，则可以使用以下基于方法来导入和重新索引基于MongoMK的AEM安装中的Lucene索引定义。

![11](assets/11.png)

