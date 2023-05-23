---
title: 部署最佳實務
seo-title: Deploying Best Practices
description: 部署及維護最佳實務。
seo-description: Deploying and maintaining best practices.
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 9%

---

# 部署最佳實務{#deploying-best-practices}

部署最佳實務說明如何以最有效率且最有效的方式部署或維護AEM。 這份不斷增加的主題清單包括AEM中的各種領域。

下列區域已有關於部署和維護最佳實務和建議的說明檔案：

* [OAK](#oak)
* [社区](#communities)
* [UI](#ui)
* [效能](#performance)

如需管理、開發或撰寫的最佳實務，請參閱下列其中一項：

* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [開發最佳實務](/help/sites-developing/best-practices.md)
* [製作最佳實務](/help/sites-authoring/best-practices.md)

以下表格中會說明並連結特定檔案。

## OAK {#oak}

[Oak](/help/sites-deploying/platform.md) 是可擴充且具備優異效能的階層式內容存放庫，是AEM的基礎。

<table>
 <tbody>
  <tr>
   <td><p>擴充性、效能與災難回覆</p> </td>
   <td><a href="/help/sites-deploying/performance.md">效能與擴充性</a></td>
   <td>提供一份白皮書，討論技術靈敏度、高效能及健全的災難回覆功能</td>
  </tr>
  <tr>
   <td>建議的OAK部署</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">建議的部署</a></td>
   <td>說明部署案例</td>
  </tr>
  <tr>
   <td>Mongo拓撲</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo拓撲最佳實務</a></td>
   <td>說明mongo拓撲 — 何時使用哪個拓撲。</td>
  </tr>
  <tr>
   <td>資料存放區選項</td>
   <td><a href="/help/sites-deploying/data-store-config.md">設定節點和資料存放區</a></td>
   <td>本檔案說明有關儲存二進位資料和內容節點的最佳實務。 包括使用Amazon S3資料存放區的資訊。</td>
  </tr>
  <tr>
   <td>在OAK中搜尋</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">查詢和建立索引的最佳實務</a><br /> </td>
   <td>說明如何為內容建立索引的最佳實務。</td>
  </tr>
 </tbody>
</table>

## 社区 {#communities}

AEM Communities可簡化內部部署社群的建立和管理。 以下說明AEM Communities的最佳實務：

[社群內容存放區](/help/communities/working-with-srp.md)  — 討論使用者產生內容(UGC)的新共用儲存功能，以及選擇基礎內容的考量事項 [拓撲](/help/communities/topologies.md).

[社群建議部署](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities)  — 說明Communities的建議部署。 |

## UI {#ui}

以下說明使用者介面的最佳實務：

[客戶適用的使用者介面Recommendations](/help/sites-deploying/ui-recommendations.md)

AEM目前有兩個UI：相同版本中的傳統和觸控最佳化UI。 因此，客戶必須在專案實作期間決定使用哪一個。 本檔案旨在協助您找到正確的選擇。

## 效能 {#performance}

以下列出效能相關的最佳實務：

<table>
 <tbody>
  <tr>
   <td>品質保證的最佳實務</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">品質保證的最佳實務</a></td>
   <td>對定義測試概念所涉及問題的標準化概觀，專門用於您的電腦上的效能測試。 <em>發佈</em> 環境。 這主要是QA工程師、專案經理和系統管理員的興趣。</td>
  </tr>
  <tr>
   <td>将 Dispatcher 与 CDN 结合使用</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">将 Dispatcher 与 CDN 结合使用</a></td>
   <td>内容交付网络 (CDN)（如 Akamai Edge Delivery 或 Amazon Cloud Front）从距离最终用户较近的站点交付内容。</td>
  </tr>
  <tr>
   <td>效能最佳化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">效能最佳化</a></td>
   <td>關鍵問題是您的網站回應訪客請求所花的時間。</td>
  </tr>
  <tr>
   <td>性能测试</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">效能測試的最佳實務</a></td>
   <td>說明在AEM部署上執行效能測試的最佳實務。<br /> </td>
  </tr>
 </tbody>
</table>
