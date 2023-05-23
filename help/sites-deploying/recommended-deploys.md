---
title: 建議的部署
seo-title: Recommended Deployments
description: 本文說明AEM的建議拓撲。
seo-description: This article describes the recommended topologies for AEM.
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 0%

---

# 建議的部署{#recommended-deployments}

>[!NOTE]
>
>本頁面說明AEM的建議拓撲。 如需叢集功能及設定方式的詳細資訊，請參閱 [Apache Sling Discovery API檔案](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html).

從AEM 6.2開始，MicroKernels會充當持續性管理員。選擇符合您需求的部署型別，取決於執行個體的用途以及您考慮的部署型別。

以下範例旨在指出最常見的AEM設定中，建議使用哪些功能。

## 部署案例 {#deployment-scenarios}

### 單一TarMK執行個體 {#single-tarmk-instance}

在此案例中，單一TarMK執行個體在單一伺服器上執行。

**這是作者執行個體的預設部署。**

![chlimage_1-15](assets/chlimage_1-15.png)

優點：

* 简单
* 輕鬆維護
* 效能優異

缺點：

* 無法擴充至超出伺服器容量限制
* 無容錯移轉容量

### TarMK冷待命 {#tarmk-cold-standby}

一個TarMK執行個體作為主要執行個體。 從主要儲存庫複製到待命容錯移轉系統。

冷待命機制也可以用作備份，因為完整的存放庫會持續複製到容錯移轉伺服器。 容錯移轉伺服器正在冷待命模式下執行，這表示只有執行個體的HttpReceiver在執行。

![chlimage_1-16](assets/chlimage_1-16.png)

優點：

* 簡單性
* 可維護性
* 效能
* 容錯移轉

缺點：

* 無法擴充至超出伺服器容量限制
* 一部伺服器大部分時間處於閒置狀態
* 容錯移轉不是自動的。 必須先在外部偵測到它，容錯移轉系統才能開始處理要求。

>[!NOTE]
>
>如需如何設定AEM與TarMK冷待命的詳細資訊，請參閱 [此](/help/sites-deploying/tarmk-cold-standby.md) 文章。

>[!NOTE]
>
>這個TarMK範例中的「冷待命」部署要求主要和待命執行個體都要分別授權，因為容錯移轉伺服器會持續進行復寫。 如需有關授權的詳細資訊，請參閱 [Adobe一般授權條款](https://www.adobe.com/legal/terms/enterprise-licensing.html).

### TarMK陣列 {#tarmk-farm}

多個Oak執行個體使用一個TarMK執行個體來執行。 TarMK存放庫是獨立的，需要保持同步。

製作伺服器會向每個伺服器陣列成員發佈相同的內容，因此可以保持存放庫同步。 如需詳細資訊，請參閱 [復寫](/help/sites-deploying/replication.md).

對於AEM Communities，永遠不會復寫使用者產生的內容(UGC)。 如需在TarMK伺服器陣列上支援UGC，請參閱 [AEM Communities的考量事項](#considerations-for-aem-communities).

**這是發佈環境的預設部署。**

![chlimage_1-17](assets/chlimage_1-17.png)

優點：

* 效能
* 讀取存取的擴充性
* 容錯移轉

### Oak叢集搭配MongoMK容錯移轉，可在單一資料中心提供高可用性 {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

此方法表示多個Oak執行個體在單一資料中心記憶體取MongoDB復本集，實際上為AEM製作環境建立主動 — 主動叢集。 MongoDB中的復本集用於在硬體或網路故障時提供高可用性和備援。

![chlimage_1-18](assets/chlimage_1-18.png)

優點：

* 能夠使用新的AEM編寫執行個體水平縮放
* 資料層的高可用性、備援及自動容錯移轉

缺點：

* 在某些情況下，效能可能低於TarMK

### Oak叢集搭配MongoMK容錯移轉功能，可跨多個資料中心運作 {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

此方法表示多個Oak執行個體可跨多個資料中心存取MongoDB復本集，實際上會為AEM製作環境建立主動 — 主動叢集。 MongoDB復寫功能具有多個資料中心，提供相同的高可用性和備援能力，但現在包括處理資料中心中斷的能力。

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

優點：

* 能夠使用新的AEM編寫執行個體水平縮放
* 資料層的高可用性、備援及自動容錯移轉（包括資料中心中斷）

>[!NOTE]
>
>在上圖中，假設資料中心2的AEM伺服器與資料中心1的MongoDB主要節點之間的網路延遲高於記錄的需求，AEM Server 3和AEM Server 4會顯示非使用中狀態 [此處](/help/sites-deploying/aem-with-mongodb.md#checklists). 如果最大延遲符合需求（例如透過使用可用區域），則資料中心2中的AEM伺服器也可以作用中，以建立跨多個資料中心作用中 — 作用中AEM叢集。

>[!NOTE]
>
>如需本節所述的MongoDB架構概念的其他資訊，請參閱 [MongoDB復寫](https://docs.mongodb.org/manual/replication/).

## 微核心：使用哪一個 {#microkernels-which-one-to-use}

在兩個可用的微核心之間進行選擇時，需要考慮的基本規則是，TarMK是針對效能而設計，而MongoMK則是針對擴充性而設計。

您可以使用這些決策矩陣，以建立適合您需求的最佳部署型別。

Adobe強烈建議客戶在AEM Author和Publish例項的所有部署情境中，將TarMK設為預設持續性技術，但下列使用案例除外。

### 在製作執行個體上選擇AEM MongoMK而非TarMK的例外情況 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

選擇MongoMK持續性後端而非TarMK的主要原因是要水平縮放執行個體。 這表示需讓兩個或多個作用中的製作執行個體隨時執行，並使用MongoDB作為持續性儲存系統。 執行多個製作執行個體的需求通常源自於單一伺服器的CPU和記憶體容量（支援所有並行製作活動）已無法持續。

幾乎無法預測新網站上線後確切的並行模式。 因此，Adobe建議您在評估是否使用MongoMK和兩個或更多「創作」作用中節點時，考慮以下標準：

1. 一天內連線的已命名使用者數目：以千或更多。
1. 同時使用者人數：以百計或更多。
1. 每日資產擷取量：數十萬或更多。
1. 每日頁面編輯量：數十萬或更多（例如透過多網站管理員或新聞摘要擷取進行的自動更新）。
1. 每日搜尋量：以萬或更多。

>[!NOTE]
>
>在部署硬體設定的情況下，可使用嚴苛日來評估客戶應用程式的效能。 有關此工具的更多資訊，請檢視 [此處](/help/sites-developing/tough-day.md).

使用MongoDB的最低部署通常涉及以下拓撲：

* MongoDB復本集包含一個主要節點、兩個次要節點，每個MongoDB執行個體都在可用性區域中執行，每個節點的延遲時間少於15毫秒；
* 一個作者執行個體叢集，具有一個領導節點、一個非領導節點，且兩者均一直處於作用中狀態，每個作者執行個體會在每個資料中心中執行，而MongoDB主要和次要執行個體會在其中執行。

此外，強烈建議您在共用檔案系統或Amazon S3上設定資料存放區，好讓資產或二進位檔不會儲存在MongoDB中。 這將確保部署中的最佳效能。

部署具有兩個或多個製作執行個體叢集的MongoDB復本集的額外優點之一，是在製作執行個體、MongoDB復本或完整資料中心故障的情況下，具有自動化復原案例，停機時間最短。 儘管如此，選擇MongoMK而非TarMK不應完全由復原需求所驅動，因為TarMK也可以提供具備受控容錯移轉機制的最小停機解決方案。

如果在部署的前18個月中不符合上述標準，建議先使用TarMK部署AEM，稍後當上述標準適用時重新評估您的設定，最後決定是否留在TarMK上或移轉至MongoMK。

### 在發佈執行個體上選擇AEM MongoMK而非TarMK的例外情況 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

不建議為發佈執行個體部署MongoMK。 部署的發佈層級幾乎總是部署為執行TarMK的完全獨立發佈執行個體的陣列，透過從製作執行個體複製內容來保持同步。 這種「不共用」架構適用於發佈執行個體，可讓發佈層級的部署以線性方式水準擴展。 伺服器陣列拓撲還提供滾動式套用任何更新或升級至發佈執行個體的優點，因此對發佈層級的任何變更都不需要停機。

只要有一個以上的發佈者，這不適用於在發佈層級上使用MongoMK叢集的AEM Communities。 若選擇JSRP (請參閱 [社群內容儲存](/help/communities/working-with-srp.md))，則MongoMK叢集將是合適的，就像任何已選擇MK的發佈端叢集（例如MongoDB或RDB）一樣。

### 使用MongoMK部署AEM時的先決條件和Recommendations {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

如果您考慮使用AEM的MongoMK部署，有一組必要條件和建議可供使用：

**MongoDB部署的必要先決條件：**

1. MongoDB部署架構和規模調整必須是專案實作的一部分，並需要熟悉AEM的Adobe諮詢或MongoDB架構師的協助；
1. 合作夥伴或客戶團隊中必須具備MongoDB專業知識，才能有信心維持和維護現有或新的MongoDB環境；
1. 您可以選擇部署商業或開放原始碼版本的MongoDB (AEM同時支援兩者)，但必須直接從MongoDB Inc購買MongoDB維護和支援合約；
1. 整體AEM和MongoDB架構和基礎建設應由AdobeAEM架構師明確定義及驗證；
1. 您必須檢閱包含MongoDB的AEM部署的支援模型。

**MongoDB部署的強大建議：**

* 參閱Adobe Experience Manager的MongoDB [文章](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)；
* 檢閱MongoDB生產環境 [檢查清單](https://docs.mongodb.org/manual/administration/production-checklist/)；
* 參加線上提供的MongoDB認證課程 [此處](https://university.mongodb.com/).

>[!NOTE]
>
>如需這些指引、先決條件和建議的所有其他問題，請聯絡 [Adobe客戶服務](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html).

### AEM Communities的考量事項 {#considerations-for-aem-communities}

針對計畫部署的網站 [AEM Communities](/help/communities/overview.md)，建議 [選擇部署](/help/communities/working-with-srp.md#characteristicsofstorageoptions) 針對處理發佈環境中的社群成員張貼的UGC進行最佳化。

透過使用 [公用存放區](/help/communities/working-with-srp.md)，不需要在作者和其他發佈執行個體之間復寫UGC就能取得UGC的一致檢視。

以下是一組決策矩陣，可協助您為部署選擇最佳型別的持續性：

#### 選擇作者執行個體的部署型別 {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### 選擇發佈執行個體的部署型別 {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB是協力廠商軟體，未包含在AEM授權套件中。 如需詳細資訊，請參閱 [MongoDB授權原則](https://www.mongodb.org/about/licensing/) 頁面。
>
>為了充分利用AEM部署，Adobe建議授權MongoDB Enterprise版本，以受益於專業支援。
>
>授權包含標準復本集，該復本集由一個主要和兩個次要執行個體組成，可用於作者或發佈部署。
>
>如果您想要在MongoDB上同時執行author和publish，則需要購買兩個不同的授權。
>
>如需詳細資訊，請參閱 [適用於Adobe Experience Manager的MongoDB頁面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
