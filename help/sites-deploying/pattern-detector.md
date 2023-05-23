---
title: 使用模式偵測器評估升級複雜性
seo-title: Assessing the Upgrade Complexity with the Pattern Detector
description: 瞭解如何使用模式偵測器來評估升級的複雜性。
seo-description: Learn how to use the Pattern Detector to assess the complexity of your upgrade.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
feature: Upgrading
exl-id: c42373e9-712e-4c11-adbb-4e3626e0b217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 使用模式偵測器評估升級複雜性

## 概述 {#overview}

此功能可讓您透過偵測使用中的模式來檢查現有AEM執行個體的可升級性，這些模式包括：

1. 違反特定規則，並在將受升級影響或覆寫的區域執行
1. 使用AEM 6.x功能或AEM 6.5上無法回溯相容、且在升級後可能會中斷的API。

這可作為升級到AEM 6.5相關開發工作的評估。

## 如何设置 {#how-to-set-up}

模式偵測器會單獨發行，做為 [一個套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) 正在處理目標為AEM 6.5升級的任何來源AEM 6.1到6.5版本。 它可使用以下工具安裝： [封裝管理員](/help/sites-administering/package-manager.md).

## 使用方法 {#how-to-use}

>[!NOTE]
>
>模式偵測器可在任何環境中執行，包括本機開發執行個體。 不過，為了：
>
>* 增加偵測率
>* 避免業務關鍵執行個體速度減慢
>
>建議兩者同時執行 **在中繼環境中** 儘可能接近使用者應用程式、內容和設定領域的生產環境。

您可以使用數種方法來檢查「模式偵測器」輸出：

* **透過Felix詳細目錄主控台：**

1. 瀏覽至，前往AEM Web Console *https://serveraddress:serverport/system/console/configMgr*
1. 選取 **狀態 — 模式偵測器** 如下圖所示：

   ![screenshot-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **透過互動式文字型或一般JSON介面**
* **透過反應式JSON行介面，**可在每行中產生個別JSON檔案。

這兩種方法的詳細資訊如下：

## 反應式介面 {#reactive-interface}

反應式介面允許在偵測到可疑時立即處理違規報告。

目前可在2個URL下取得輸出：

1. 純文字介面
1. JSON介面

## 處理純文字介面 {#handling-the-plain-text-interface}

輸出中的資訊會格式化為一系列事件專案。 有兩個管道 — 一個用於發佈違規，另一個用於發佈目前的進度。

可使用下列指令來取得：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

輸出將如下所示：

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

您可以使用以下專案篩選進度 `grep` 命令：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

這會產生以下輸出：

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## 處理JSON介面 {#handling-the-json-interface}

同樣地，JSON的處理方式也可使用 [jq工具](https://stedolan.github.io/jq/) 一經發佈。

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

透過輸出：

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

每5秒會報告一次進度，而且可以透過排除標籤為懷疑的訊息以外的其他訊息來擷取進度：

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

透過輸出：

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>建議的方法是將curl的整個輸出儲存到檔案中，然後透過處理 `jq` 或 `grep` 以篩選資訊型別。

## 偵測範圍 {#scope}

目前的模式偵測器允許檢查：

* OSGi套件組合匯出和匯入不相符
* Sling資源型別和超級型別（具有搜尋路徑內容覆蓋圖）使用過量
* Oak索引的定義（相容性）
* VLT封裝（使用過度）
* rep：User節點相容性（在OAuth設定的內容中）

>[!NOTE]
>
>請注意，模式偵測器會嘗試準確預測升級警告。 但是，在某些情況下，它可能會產生誤報。
