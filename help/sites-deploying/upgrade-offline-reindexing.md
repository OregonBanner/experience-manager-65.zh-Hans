---
title: 使用離線重新索引以減少升級期間的停機時間
description: 瞭解如何使用離線重新索引方法，以減少執行AEM升級時的系統停機時間。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 1%

---

# 使用離線重新索引以減少升級期間的停機時間 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 简介 {#introduction}

升級Adobe Experience Manager的主要挑戰之一，是執行就地升級時與作者環境相關的停機時間。 內容作者在升級期間將無法存取環境。 因此，最好將執行升級所需的時間減至最少。 對於大型存放庫，尤其是AEM Assets專案，通常具有大型資料存放區和每小時高水準的資產上傳，重新索引Oak索引需要很大一部分升級時間。

本節說明如何使用Oak-run工具來重新索引儲存區域 **早於** 執行升級，進而減少實際升級期間的停機時間。 顯示的步驟可套用至 [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) AEM 6.4及更高版本的索引。

## 概述 {#overview}

新版本的AEM會在功能集展開時引入Oak索引定義的變更。 Oak索引的變更會在升級AEM執行個體時強制重新索引。 由於資產中的文字（例如PDF檔案中的文字）會被擷取並編制索引，因此重新索引對於資產部署而言會很昂貴。 使用MongoMK存放庫時，資料會透過網路持續存在，進一步增加重新索引所需的時間。

大多數客戶在升級期間面臨的問題是縮短停機時間。 解決方案是 **略過** 在升級期間重新索引活動。 這可以透過建立新索引來達成 **上一個** 以執行升級，然後在升級期間直接匯入它們。

## 方針 {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

其想法是在升級之前建立索引，以使用目標AEM版本的索引定義 [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) 工具。 上圖顯示離線重新索引方法。

此外，這是步驟的順序，如方法所述：

1. 系統會先擷取二進位檔中的文字
2. 目標索引定義已建立
3. 已建立離線索引
4. 然後在升級過程中匯入索引

### 文本提取 {#text-extraction}

若要在AEM中啟用完整索引，會擷取二進位檔(例如PDF)的文字，並將其新增至索引。 在索引過程中，這通常是代價高昂的步驟。 文字擷取是提倡的最佳化步驟，特別是當資產存放庫儲存大量二進位檔時，建議重新索引資產存放庫。

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

使用包含Tika程式庫的Oak-run工具，可擷取儲存在系統中的二進位檔文字。 您可以在升級前複製生產系統，並可用於此文字擷取程式。 此程式接著會透過下列步驟建立文字存放區：

**1. 周遊儲存區域並收集二進位檔的詳細資訊**

此步驟會產生一個包含二進位檔案元組的CSV檔案，其中包含路徑和blob id。

從要建立索引的目錄執行下列命令。 以下範例假設是存放庫主目錄。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

位置 `nodestore path` 是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

使用 `--fake-ds-path=temp` 引數而非 `–fds-path` 以加速處理作業。

**2. 重複使用現有索引中可用的二進位文字存放區**

從現有系統傾印索引資料並擷取文字存放區。

您可以使用以下命令傾印現有的索引資料：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

位置 `nodestore path` 是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

然後，使用上述索引傾印來填入存放區：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

位置 `oak-index-name` 是全文檢索索引的名稱，例如&quot;lucene&quot;。

**3. 針對上述步驟中遺漏的二進位檔案，使用Tika程式庫執行文字擷取程式**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

位置 `datastore path` 是二進位資料存放區的路徑。

建立的文字存放區可以更新，並可在未來重新索引情境時使用。

如需有關文字擷取程式的詳細資訊，請參閱 [Oak-run檔案](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### 離線重新索引 {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升級前離線建立Lucene索引。 若使用MongoMK，建議直接在其中一個MongoMk節點上執行，以避免網路負荷。

若要離線建立索引，請遵循下列步驟：

**1. 產生目標AEM版本的Oak Lucene索引定義**

傾印現有的索引定義。 發生變更的索引定義是使用目標AEM版本和Oak-run的AdobeGranite存放庫套件組合產生的。

若要從傾印索引定義 **source** AEM執行個體，執行此命令：

>[!NOTE]
>
>如需有關轉儲索引定義的詳細資訊，請參閱 [Oak檔案](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

位置 `datastore path` 和 `nodestore path` 來自 **source** AEM執行個體。

然後，從產生索引定義 **目標** 使用目標版本的Granite存放庫套件組合的AEM版本。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>上述索引定義建立程式僅支援來自 `oak-run-1.12.0` 版本以後。 目標定位可使用Granite存放庫套件組合完成 `com.adobe.granite.repository-x.x.xx.jar`.

上述步驟會建立名為的JSON檔案 `merge-index-definitions_target.json` 索引定義。

**2. 在存放庫中建立查核點**

在生產環境中建立查核點 **source** 具有長生命週期的AEM執行個體。 這應在複製存放庫之前完成。

透過位於「 」的JMX主控台 `http://serveraddress:serverport/system/console/jmx`，前往 `CheckpointMBean` 並建立具有足夠長生命週期（例如200天）的查核點。 對此，呼叫 `CheckpointMBean#createCheckpoint` 替換為 `17280000000` 作為期限持續時間（毫秒）的引數。

完成此操作後，複製新建立的查核點ID並使用JMX驗證存留期 `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
>稍後匯入索引時，會刪除此查核點。

如需詳細資訊，請參閱 [建立查核點](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) 從Oak檔案。

**為產生的索引定義執行離線索引**

可以使用oak-run離線完成Lucene重新索引。 此程式會在下方的磁碟中建立索引資料 `indexing-result/indexes`. 確實如此 **not** 寫入存放庫，因此不需要停止正在執行的AEM執行個體。 建立的文字存放區會饋送至此程式：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

的使用方式 `--doc-traversal-mode` 引數適用於MongoMK安裝，因為藉由將存放庫內容多工緩衝到本機一般檔案，可大幅改善重新索引時間。 不過，它需要儲存庫大小兩倍的額外磁碟空間。

在MongoMK的案例中，如果這個步驟是在更接近MongoDB執行個體的執行個體中執行，則可以加速這個程式。 如果在同一台電腦上執行，可以避免網路負荷。

如需其他技術詳細資訊，請參閱 [索引的Oak-run檔案](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### 匯入索引 {#importing-indexes}

使用AEM 6.4及更新版本時，AEM具有在啟動順序從磁碟匯入索引的內建功能。 資料夾 `<repository>/indexing-result/indexes` 啟動期間會觀察索引資料是否存在。 您可以在「 」期間將預先建立的索引複製到上述位置 [升級程式](in-place-upgrade.md#performing-the-upgrade) 開始使用新版的 **目標** AEM jar。 AEM會將其匯入存放庫，並從系統中移除對應的查核點。 因此，完全避免重新索引。

## 其他秘訣和疑難排解 {#troubleshooting}

在下方，您會找到一些實用的提示和疑難排解指示。

### 減少對即時生產系統的影響 {#reduce-the-impact-on-the-live-production-system}

建議複製生產系統，並使用複製建立離線索引。 如此可消除對生產系統的任何潛在影響。 不過，匯入索引所需的查核點必須存在於生產系統中。 因此，在複製前先建立查核點非常重要。

### 準備Runbook並試用執行 {#prepare-a-runbook-and-trial-run}

建議準備 [runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) 並在生產環境執行升級之前，執行一些試驗。

### 具有離線索引的檔案周遊模式 {#doc-traversal-mode-with-offline-indexing}

離線索引需要遍歷整個存放庫。 透過MongoMK安裝，可透過網路存取存放庫，影響索引程式的效能。 一個選項是在MongoDB復本本身執行離線索引程式，這將消除網路負荷。 另一個選項是使用檔案周遊模式。

可以透過新增命令列引數來套用檔案周遊模式 `—doc-traversal` 至離線索引的oak-run命令。 此模式會將本機磁碟中整個存放庫的復本多工緩衝為平面檔案，並使用它來執行索引。
