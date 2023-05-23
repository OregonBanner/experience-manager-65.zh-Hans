---
title: Oak-run.jar索引使用案例
seo-title: Oak-run.jar Indexing Use Cases
description: 瞭解使用Oak-run工具執行索引的各種使用者案例。
seo-description: Learn about the various user cases for performing indexing with the Oak-run tool.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Oak-run.jar索引使用案例{#oak-run-jar-indexing-use-cases}

Oak-run支援在命令列上索引使用案例，不必透過AEM JMX主控台協調這些使用案例的執行。

使用oak-run.jar index命令方法來管理Oak索引的總體優點包括：

1. Oak-run index指令為AEM 6.4提供新的索引工具集。
1. Oak-run可減少重新索引的時間，進而減少大型存放庫重新索引的時間。
1. Oak-run可減少在AEM中重新索引時的資源消耗，導致整體更佳的系統效能。
1. Oak-run提供頻外重新索引，支援必須提供生產環境的情況，而且無法忍受維護或停機，否則需要重新索引。

以下各節將提供範例指令。 oak-run index命令支援所有NodeStore和BlobStore設定。 以下提供的範例是關於具有FileDataStore和SegmentNodeStore的設定。

## 使用案例1 — 索引一致性檢查 {#usercase1indexconsistencycheck}

這是與索引損毀相關的使用案例。 在某些情況下，無法判斷哪些索引已損毀。 因此，Adobe提供的工具可以：

1. 對所有索引執行索引一致性檢查，並提供關於哪些索引有效哪些索引無效的報告；
1. 即使AEM無法存取，該工具仍可使用；
1. 使用方便。

檢查損壞的索引可以透過 `--index-consistency-check` 作業：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

這會在以下位置產生報告： `indexing-result/index-consistency-check-report.txt`. 如需範例報表，請參閱下文：

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### 好处 {#uc1benefits}

支援和系統管理員現在可以使用此工具來快速判斷哪些索引已損毀，然後重新索引它們。

## 使用案例2 — 索引統計資料 {#usecase2indexstatistics}

為了診斷查詢效能Adobe的某些案例，通常需要現有的索引定義，來自客戶設定的索引相關統計資料。 到目前為止，這些資訊分散於多種資源。 為了更輕鬆進行疑難排解，Adobe已建立具有以下功能的工具：

1. 將系統上存在的所有索引定義傾印在單個JSON檔案中；

1. 從現有索引傾印重要統計資料；

1. 傾印索引內容以供離線分析；

1. 即使AEM無法存取，仍可使用

您現在可以透過下列操作索引指令完成上述操作：

* `--index-info`  — 收集並傾印與索引相關的各種統計資料

* `--index-definitions`  — 收集並傾印索引定義

* `--index-dump`  — 傾印索引內容

請參閱以下指令實際運作方式的範例：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

報表產生位置為 `indexing-result/index-info.txt` 和 `indexing-result/index-definitions.json`

此外，相同的詳細資訊會透過Web主控台提供，並會成為設定傾印zip的一部分。 它們可在下列位置存取：

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 好处 {#uc2benefits}

此工具可讓您快速收集與索引或查詢問題相關的所有必要詳細資訊，並減少擷取此資訊所花費的時間。

## 使用案例3 — 重新索引 {#usecase3reindexing}

根據 [情境](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)，某些情況下需要執行重新索引。 目前，重新索引是透過設定 `reindex` 標幟到 `true` 透過CRXDE或透過Index Manager使用者介面在索引定義節點中建立。 設定標幟後，會以非同步方式完成重新索引。

關於重新索引的一些要注意的事項：

* 重新索引速度較慢，在 `DocumentNodeStore` 設定比較對象 `SegmentNodeStore` 設定所有內容為本機；

* 在目前設計中，當重新索引時，非同步索引器會遭到封鎖，而所有其他非同步索引會變得陳舊，並且在索引期間不會更新。 因此，如果系統正在使用中，使用者可能無法看到最新結果；
* 重新索引涉及周遊整個存放庫，這可能對AEM設定造成高負載，從而影響一般使用者體驗；
* 對於 `DocumentNodeStore` 在其中重新索引可能需要相當長的時間的安裝，如果與Mongo資料庫的連線在作業期間失敗，則必須從頭開始重新索引；

* 在某些情況下，由於文字擷取，重新索引可能需要很長時間。 這主要是針對具有許多PDF檔案的設定，其中花費在文字擷取上的時間可能會影響索引時間。

為了達到這些目標，Oak-run索引工具支援可視需要使用的不同重新索引模式。 oak-run index指令提供下列優點：

* **頻外重新索引** - oak-run重新索引可以與正在執行的AEM設定分開完成，因此可將對正在使用的AEM執行個體的影響降至最低；

* **越區重新索引**  — 重新索引不影響索引操作。 這表示非同步索引器可以繼續索引其他索引；

* **DocumentNodeStore安裝的簡化重新索引** - （適用於） `DocumentNodeStore` 安裝，重新索引可以使用單一命令完成，以確保重新索引以最佳方式完成；

* **支援更新索引定義和引入新索引定義**

### 重新索引 — DocumentNodeStore {#reindexdocumentnodestore}

對象 `DocumentNodeStore` 安裝可透過單一oak-run命令完成重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

這提供下列優點

* 對執行AEM執行個體影響極小。 大部分的讀取可以從次要伺服器完成，而且執行AEM快取不會因為重新索引所需的所有周遊而受到不良影響；
* 使用者也可以透過以下方式提供新索引或更新索引的JSON： `--index-definitions-file` 選項。

### 重新索引 — SegmentNodeStore {#reindexsegmentnodestore}

對象 `SegmentNodeStore` 安裝可透過下列其中一種方式完成重新索引：

#### 線上重新索引 — 區段節點存放區 {#onlinereindexsegmentnodestore}

遵循既定方式，透過設定完成重新索引 `reindex` 標幟。

#### 線上重新索引 — SegmentNodeStore - AEM執行個體正在執行 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

對象 `SegmentNodeStore` 安裝中只有一個處理程式可以在讀寫模式下存取區段檔案。 因此，Oak-run索引中的一些操作需要執行額外的手動步驟。

這將涉及以下內容：

1. 步驟文字
1. 連線 `oak-run` 到AEM以唯讀模式使用的相同存放庫，並執行索引。 如何達成此目標的範例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最後，透過以下匯入建立的索引檔案： `IndexerMBean#importIndex` oak-run在執行上述命令後儲存索引檔案的路徑中的操作。

在此案例中，您不必停止AEM伺服器或布建任何新執行個體。 但是，由於索引涉及遍歷整個存放庫，這會增加安裝上的I/O負載，對執行階段效能產生負面影響。

#### 線上重新索引 — SegmentNodeStore - AEM執行個體已關閉 {#onlinereindexsegmentnodestoreaeminstanceisdown}

對象 `SegmentNodeStore` 安裝重新索引可透過單一oak-run命令完成。 不過，AEM執行個體必須關閉。

您可以使用以下命令觸發重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

此方法與上述方法的區別在於，查核點建立和索引匯入會自動完成。 不利的一面是AEM在此過程中需要關閉。

#### 頻外重新索引 — SegmentNodeStore {#outofbandreindexsegmentnodestore}

在此使用案例中，您可以在複製的設定上執行重新索引，以將對正在執行的AEM執行個體造成的影響降至最低：

1. 透過JMX操作建立查核點。 您可以前往 [JMX主控台](/help/sites-administering/jmx-console.md) 並搜尋 `CheckpointManager`. 然後，按一下 **createCheckpoint(long p1)** 以秒為單位的高過期值作業(例如， **2592000**)。
1. 複製 `crx-quickstart` 資料夾至新電腦
1. 透過oak-run index命令執行重新索引

1. 將產生的索引檔案複製到AEM伺服器

1. 透過JMX匯入索引檔案。

在此使用案例中，我們假設資料存放區可在其他執行個體上存取，但若有下列情況，則可能無法存取： `FileDataStore` 會放置在雲端型儲存解決方案（例如EBS）上。 這排除了以下情況 `FileDataStore` 也會被複製。 如果索引定義未執行全文檢索，則存取 `DataStore` 非必要。

## 使用案例4 — 更新索引定義 {#usecase4updatingindexdefinitions}

目前，您可以透過以下方式傳送索引定義變更： [ACS確認索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 封裝。 這允許透過內容套件傳送索引定義，之後需要透過設定執行重新索引。 `reindex` 標幟到 `true`.

這項操作適用於重新索引時間不長的小型安裝。 不過，對於非常大的存放庫，重新索引將在相當長的時間內完成。 對於這類情況，我們現在可以使用oak-run索引工具。

Oak-run現在支援以JSON格式提供索引定義，以及在即時執行個體未執行任何變更的情況下，以頻外模式建立索引。

針對此使用案例，您需要考慮的流程為：

1. 開發人員會更新本機執行個體上的索引定義，然後透過產生索引定義JSON檔案 `--index-definitions` option

1. 更新後的JSON會提供給系統管理員
1. 系統管理員遵循頻外方法，在不同的安裝上準備索引
1. 完成此操作後，將在執行中的AEM安裝中匯入產生的索引檔案。
