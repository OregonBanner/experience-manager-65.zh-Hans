---
title: 使用記錄檔
seo-title: Working with Logs
description: 瞭解如何使用記錄檔來疑難排解AEM。
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 3%

---

# 使用記錄檔{#working-with-logs}

本節包含可協助您進行疑難排解的記錄檔詳細資訊。

CRX記錄詳細記錄。 拆開包裝並啟動「快速入門」後，您可在下列位置找到記錄檔：

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## 啟動DEBUG記錄層級 {#activating-the-debug-log-level}

預設記錄層級為INFO，亦即DEBUG訊息不會被記錄。

若要啟用DEBUG記錄層級，請使用CRX explorer設定

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

要偵錯的屬性。 請勿讓記錄在DEBUG記錄層級保留超過必要的時間，因為它會產生許多記錄。

偵錯檔案中的某一行通常以DEBUG開頭，然後提供記錄層級、安裝程式動作和記錄訊息。 例如：

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

記錄層級如下：

| 0 | 嚴重錯誤 | 動作失敗，安裝程式無法繼續。 |
|---|---|---|
| 1 | 错误 | 動作已失敗。 安裝會繼續，但部分CRX未正確安裝且將無法運作。 |
| 2 | 警告 | 動作已成功，但發生問題。 CRX不一定能正常運作。 |
| 3 | 信息 | 動作已成功。 |

## 用於疑難排解的詳細選項 {#verbose-option-used-for-troubleshooting}

啟動CRX時，您可以將 — v （詳細）選項新增到命令列，如下所示：

` java -jar crx-<*version*>-<*edition*>.jar -v`

使用詳細選項進行疑難排解，因為此選項會在主控台上顯示一些快速入門記錄輸出。
