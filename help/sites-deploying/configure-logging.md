---
title: 日志记录
seo-title: Logging
description: 瞭解如何設定中央記錄服務的全域引數、個別服務的特定設定，或如何請求資料記錄。
seo-description: Learn how to configure global parameters for the central logging service, specific settings for the individual services or how to request data logging.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 日志记录{#logging}

AEM可讓您設定：

* 中央記錄服務的全域引數
* 請求資料記錄；請求資訊的專用記錄設定
* 個別服務的特定設定；例如，個別記錄檔和記錄訊息的格式

這些都是 [OSGi設定](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>AEM中的登入是根據Sling原則所制定。 另請參閱 [Sling記錄](https://sling.apache.org/site/logging.html) 以取得進一步資訊。

## 全域記錄 {#global-logging}

[Apache Sling記錄設定](/help/sites-deploying/osgi-configuration-settings.md) 用於設定根記錄器。 這會定義登入AEM的全域設定：

* 記錄層級
* 中央記錄檔的位置
* 要保留的版本數量
* 版本輪換；大小上限或時間間隔
* 寫入記錄訊息時要使用的格式

>[!NOTE]
>
>此 [知識庫文章](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) 說明如何輪換request.log和access.log檔案。

## 個別服務的記錄器及寫入器 {#loggers-and-writers-for-individual-services}

除了全域記錄設定，AEM還允許您為個別服務設定特定設定：

* 特定記錄層級
* 個別記錄檔的位置
* 要保留的版本數量
* 版本輪換；大小上限或時間間隔
* 寫入記錄訊息時要使用的格式
* 記錄器（提供記錄訊息的OSGi服務）

這可讓您將單一服務的記錄訊息通道化為個別檔案。 這在開發或測試期間特別有用；例如，當您需要針對特定服務提高記錄層級時。

AEM會使用以下專案將記錄訊息寫入檔案：

1. 一個 **OSGi服務** （記錄器）寫入記錄訊息。
1. A **記錄記錄器** 會擷取此訊息，並根據您的規格將其格式化。
1. A **記錄寫入者** 會將所有這些訊息寫入您定義的實體檔案中。

這些元素由適當元素的下列引數連結：

* **記錄器（記錄器）**

   定義產生訊息的服務。

* **記錄檔（記錄記錄器）**

   定義儲存記錄訊息的實體檔案。

   這可用來將記錄記錄器連結至記錄寫入器。 值必須與記錄寫入器設定中的相同引數相同，才能建立連線。

* **記錄檔（記錄寫入器）**

   定義將寫入記錄訊息的實體檔案。

   這必須與記錄寫入器設定中的相同引數相同，否則將無法進行比對。 如果沒有相符專案，則會使用預設設定（每日記錄輪換）建立隱含的Writer。

### 標準記錄器及寫入器 {#standard-loggers-and-writers}

標準AEM安裝包含特定記錄器及寫入器。

第一個是特殊情況，因為它同時控制兩個 `request.log` 和 `access.log` 檔案：

* 記錄器：

   * Apache Sling可自訂請求資料記錄器

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 將請求內容的相關訊息寫入 `request.log`.

* 連結至：

   * Apache Sling請求記錄器

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 將訊息寫入 `request.log` 或 `access.log`.

如有需要，可以自訂這些設定，但標準設定適用於大多數安裝。

其他配對則遵循標準設定：

* 記錄器：

   * Apache Sling記錄記錄器設定

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 寫入 `Information` 訊息收件者 `logs/error.log`.

* 寫入器的連結：

   * Apache Sling記錄寫入器設定

      (org.apache.sling.commons.log.LogManager.factory.writer)

* 記錄器：

   * Apache Sling記錄記錄器設定(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 寫入 `Warning` 訊息收件者 `../logs/error.log` 服務 `org.apache.pdfbox`.

* 不會連結至特定寫入器，因此會建立並使用具有預設設定（每日記錄輪換）的隱含寫入器。

### 建立自己的記錄器和寫入器 {#creating-your-own-loggers-and-writers}

您可以定義自己的記錄器/寫入器配對：

1. 建立Factory組態的新執行個體 [Apache Sling記錄記錄器設定](/help/sites-deploying/osgi-configuration-settings.md).

   1. 指定記錄檔。
   1. 指定記錄器。
   1. 視需要設定其他引數。

1. 建立Factory組態的新執行個體 [Apache Sling記錄寫入器設定](/help/sites-deploying/osgi-configuration-settings.md).

   1. 指定記錄檔 — 這必須符合為記錄器指定的記錄檔。
   1. 視需要設定其他引數。

>[!NOTE]
>
>在某些情況下，您可能想要建立 [自訂記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
