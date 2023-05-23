---
title: 搜尋Essentials
seo-title: Search Essentials
description: 在社群中搜尋
seo-description: Search in Communities
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 4%

---

# 搜尋Essentials {#search-essentials}

## 概述 {#overview}

搜尋功能是AEM Communities的重要功能。 除了 [AEM平台搜尋](../../help/sites-deploying/queries-and-indexing.md) 功能，AEM Communities提供 [UGC搜尋API](#ugc-search-api) ，用於搜尋使用者產生的內容(UGC)。 UGC有唯一屬性，因為它與其他AEM內容和使用者資料分開輸入和儲存。

針對Communities，通常會搜尋兩個專案：

* 社群成員張貼的內容

   * 使用AEM Communities的UGC搜尋API。

* 使用者和使用者群組（使用者資料）

   * 使用AEM平台搜尋功能。

建立自訂元件以建立或管理UGC的開發人員可能會對說明檔案的此區段感興趣。

## 安全性與陰影節點 {#security-and-shadow-nodes}

對於自訂元件，必須使用 [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) 方法。 建立和搜尋UGC的公用程式方法將建立所需的 [陰影節點](srp.md#about-shadow-nodes-in-jcr) 並確保成員擁有請求的正確許可權。

不透過SRP公用程式管理的專案為與仲裁相關的屬性。

另請參閱 [SRP和UGC Essentials](srp-and-ugc.md) 有關用於存取UGC和ACL陰影節點的公用程式方法的資訊。

## UGC搜尋API {#ugc-search-api}

此 [UGC公用存放區](working-with-srp.md) 由各種儲存資源提供者(SRP)之一提供，每個提供者都可能有不同的原生查詢語言。 因此，無論選擇的SRP為何，自訂程式碼都應使用來自 [UGC API套件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*)會叫用適用於所選SRP的查詢語言。

### ASRP搜尋 {#asrp-searches}

對象 [ASRP](asrp.md)，UGC會儲存在Adobe雲端。 雖然CRX中未顯示UGC， [稽核](moderate-ugc.md) 可在作者和發佈環境中使用。 使用 [UGC搜尋API](#ugc-search-api) ASRP的運作方式與其他SRP相同。

目前沒有管理ASRP搜尋的工具。

建立可搜尋的自訂屬性時，必須遵守 [命名需求](#naming-of-custom-properties).

### MSRP搜尋 {#msrp-searches}

對象 [MSRP](msrp.md)，UGC儲存在MongoDB中，且已設定為使用Solr進行搜尋。 CRX中不會顯示UGC，但 [稽核](moderate-ugc.md) 可在作者和發佈環境中使用。

關於MSRP和Solr：

* AEM平台的內嵌Solr不用於MSRP。
* 如果為AEM平台使用遠端Solr，則可與MSRP共用，但應使用不同的集合。
* Solr可設定為標準搜尋或多語言搜尋(MLS)。
* 如需設定詳細資訊，請參閱 [Solr設定](msrp.md#solr-configuration) 用於MSRP。

自訂搜尋功能應使用 [UGC搜尋API](#ugc-search-api).

建立可搜尋的自訂屬性時，必須遵守 [命名需求](#naming-of-custom-properties).

### JSRP搜尋 {#jsrp-searches}

對象 [JSRP](jsrp.md)，UGC儲存在 [Oak](../../help/sites-deploying/platform.md) 和僅會顯示在輸入它的AEM作者或發佈執行個體的存放庫中。

由於UGC通常輸入在發佈環境中，對於多發佈者生產系統，有必要配置 [發佈叢集](topologies.md)，而非發佈陣列，因此所有發佈者都能看到輸入的內容。

對於JSRP，在發佈環境中輸入的UGC永遠不會顯示在製作環境中。 因此，所有 [稽核](moderate-ugc.md) 工作會在發佈環境中進行。

自訂搜尋功能應使用 [UGC搜尋API](#ugc-search-api).

#### Oak索引 {#oak-indexing}

雖然系統不會自動為AEM平台搜尋建立Oak索引，但自AEM 6.2起，已為AEM Communities新增這些索引，以改善效能並在顯示UGC搜尋結果時支援分頁。

如果使用自訂屬性且搜尋緩慢，則需要為自訂屬性建立其他索引，以提高其效能。 若要保持可攜性，請遵守 [命名需求](#naming-of-custom-properties) 建立可搜尋的自訂屬性時。

若要修改現有索引或建立自訂索引，請參閱 [Oak查詢和索引](../../help/sites-deploying/queries-and-indexing.md).

此 [Oak索引管理員](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) 可從ACS AEM Commons取得。 它提供：

* 現有索引的檢視。
* 啟動重新索引的功能。

檢視現有Oak索引的方式 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)，位置為：

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## 索引搜尋屬性 {#indexed-search-properties}

### 預設搜尋屬性 {#default-search-properties}

以下是用於各種Communities功能的一些可搜尋屬性：

| **属性** | **数据类型** |
|---|---|
| isFlagged | *布尔型* |
| isSpam | *布尔型* |
| 讀取 | *布尔型* |
| 影響 | *布尔型* |
| 附件 | *布尔型* |
| 情緒 | *长整型* |
| 已標幟 | *布尔型* |
| 已添加 | *日期* |
| modifieddate | *日期* |
| 状态 | *字符串* |
| 使用者識別碼 | *字符串* |
| 回覆 | *长整型* |
| jcr:title | *字符串* |
| jcr：description | *字符串* |
| sling:resourceType | *字符串* |
| allowThreadedReply | *布尔型* |
| isDraft | *布尔型* |
| publishDate | *日期* |
| publishJobId | *字符串* |
| 已回复 | *布尔型* |
| chosenanswered | *布尔型* |
| 標籤 | *字符串* |
| cq：Tag | *字符串* |
| author_display_name | *字符串* |
| location_t | *字符串* |
| 父路徑 | *字符串* |
| parentTitle | *字符串* |

### 命名自訂屬性 {#naming-of-custom-properties}

新增自訂屬性時，為了讓使用「 」建立的排序和搜尋能夠看見這些屬性 [UGC搜尋API](#ugc-search-api)，它是 *必填* 以新增字尾至屬性名稱。

尾碼適用於使用結構的查詢語言：

* 它會將屬性識別為可搜尋。
* 它可識別資料型別。

Solr是使用結構描述的查詢語言範例。

| **后缀** | **数据类型** |
|---|---|
| _b | *布尔型* |
| _dt | *日程表* |
| _d | *双精度型* |
| _tl | *长整型* |
| _s | *字符串* |
| _t | *文本* |

**注释:**

* *文字* 是標籤字串， *字串* 不是。 使用 *文字* 用於模糊（類似於）搜尋。

* 對於多值型別，請將&#39;s&#39;新增至尾碼，例如：

   * `viewDate_dt`：單一日期屬性
   * `viewDates_dts`：日期屬性清單

## 过滤器 {#filters}

包含 [評論系統](essentials-comments.md) 支援將篩選引數新增至其端點。

AND和OR邏輯的篩選語法如下（在URL編碼前顯示）：

* 若要指定OR或使用包含逗號分隔值的篩選引數：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 若要指定AND並使用多個篩選引數，請執行下列動作：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

的預設實施 [搜尋元件](search.md) 會使用此語法，如同在下列位置開啟搜尋結果頁面的URL中所見： [社群元件指南](components-guide.md). 若要實驗，請瀏覽至 [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

篩選器運運算元包括：

| EQ | 等于 |
|---|---|
| NE | 不等於 |
| LT | 小於 |
| LTE | 小於或等於 |
| GE | 大於 |
| GTE | 大於或等於 |
| 按讚 | 模糊比對 |

URL務必參考Communities元件（資源），而非元件所在的頁面：

* 正確：論壇元件
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 不正確：論壇頁面
   * `/content/community-components/en/forum.social.json`

## SRP工具 {#srp-tools}

有一個Adobe Marketing Cloud GitHub專案，其中包含：

[AEM Communities SRP工具](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

此存放庫包含用於管理SRP中資料的工具。

目前，有一個servlet提供從任何SRP刪除所有UGC的功能。

例如，若要刪除ASRP中的所有UGC：

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## 疑难解答 {#troubleshooting}

### Solr查詢 {#solr-query}

若要協助疑難排解Solr查詢的問題，請啟用DEBUG記錄

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

實際Solr查詢將顯示在偵錯記錄檔中編碼的URL：

要查詢的solr為： `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

的值 `q` 引數為查詢。 解碼URL編碼後，即可將查詢傳遞到Solr管理查詢工具，以便進一步偵錯。

## 相关资源 {#related-resources}

* [社群內容儲存](working-with-srp.md)  — 討論UGC一般存放區的可用SRP選擇。
* [儲存資源提供者概觀](srp.md)  — 簡介和存放庫使用概述。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 程式碼指南。
* [SocialUtils重構](socialutils.md)  — 取代SocialUtils的SRP公用程式方法。
* [搜尋和搜尋結果元件](search.md)  — 將UGC搜尋功能新增至範本。
