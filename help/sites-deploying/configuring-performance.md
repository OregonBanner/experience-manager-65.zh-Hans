---
title: 效能最佳化
description: 瞭解如何設定AEM的某些方面以最佳化效能。
uuid: a4d9fde4-a4c7-4ee5-99b6-29b0ee7dc35b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 80118cd1-73e1-4675-bbdf-85d66d150abc
feature: Configuring
exl-id: 5b0c9a8c-0f5f-46ee-a455-adb9b9d27270
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6503'
ht-degree: 12%

---

# 效能最佳化 {#performance-optimization}

>[!NOTE]
>
>如需效能的一般准則，請閱讀 [效能准則](/help/sites-deploying/performance-guidelines.md) 頁面。
>
>如需疑難排解和修正效能問題的詳細資訊，另請參閱 [效能樹狀結構](/help/sites-deploying/performance-tree.md).
>
>此外，您也可以檢閱知識庫文章，網址為 [效能調整秘訣](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hans).

關鍵問題是您的網站回應訪客請求所花的時間。 雖然此值會因每個請求而異，但您可以定義平均目標值。 一旦這個值被證實既可達到又可維持，就可用它來監控網站的效能並指示潛在問題的發展。

您針對的回應時間在製作和發佈環境上有所不同，這反映了目標對象的不同特性：

## 创作环境 {#author-environment}

輸入和更新內容的作者會使用此環境。 它必須迎合個別使用者在更新內容頁面及這些頁面上的個別元素時，各自產生大量效能密集型請求的需求。

## 发布环境 {#publish-environment}

此環境包含可供使用者使用的內容。 在這裡，要求數量更多，速度也同樣重要。 但由於要求的本質不是那麼動態，可以套用額外的效能增強機制；例如快取內容或負載平衡。

>[!NOTE]
>
>* 針對效能最佳化進行設定後，請遵循下列程式： [艱難的一天](/help/sites-developing/tough-day.md) 在重負載下測試環境。
>* 另請參閱 [效能調整秘訣。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hans)


## 效能最佳化方法 {#performance-optimization-methodology}

AEM專案的效能最佳化方法可歸納為五個簡單的規則，從一開始就可避免效能問題：

1. [最佳化規劃](#planning-for-optimization)
1. [模擬現實](#simulate-reality)
1. [建立堅實的目標](#establish-solid-goals)
1. [保持相關性](#stay-relevant)
1. [敏捷反複專案週期](#agile-iteration-cycles)

這些規則通常適用於Web專案，並與專案經理和系統管理員相關，以確保他們的專案在啟動時不會面臨效能挑戰。

### 最佳化規劃 {#planning-for-optimization}

![chlimage_1-3](assets/chlimage_1-3.jpeg)

針對效能最佳化階段規劃約10%的專案工作量。 實際的效能最佳化需求取決於專案的複雜程度及開發團隊的經驗。 雖然您的專案可能（最終）不需要分配的時間，但最好一律在建議區域規劃效能最佳化。

如有可能，專案應先軟性推出給有限的對象，以收集現實生活體驗並執行進一步的最佳化，而不受完整公告之後的額外壓力。

「即時」後，效能最佳化並未結束。 此時您會在系統上體驗「真實」負載。 在啟動後，請務必規劃其他調整。

由於您的系統負載會變更，而且系統的效能設定檔會隨著時間而改變，因此效能「調校」或「健康狀態檢查」應以6-12個月的間隔排程。

### 模擬現實 {#simulate-reality}

![chlimage_1-4](assets/chlimage_1-4.jpeg)

如果您使用網站，然後在啟動後發現您遇到效能問題，可能是因為您的負載和效能測試未充分模擬現實。

模擬現實很困難，您想要投入多少精力才能變得「真實」取決於專案的性質。 「真實」不僅表示「真實的程式碼」和「真實的流量」，也表示「真實的內容」，尤其是關於內容大小和結構。 您的範本可能會根據存放庫的大小和結構而表現出不同的行為。

### 建立堅實的目標 {#establish-solid-goals}

![chlimage_1-5](assets/chlimage_1-5.jpeg)

正確建立績效目標的重要性不可低估。 通常，在人們專注於特定績效目標後，即使這些目標基於假設，也很難在之後改變這些目標。

建立良好、堅實的效能目標確實是最困難的領域之一。 通常最好從可比較的網站（例如新網站的前身）收集真實生活記錄和基準。

### 保持相關性 {#stay-relevant}

![chlimage_1-6](assets/chlimage_1-6.jpeg)

一次最佳化一個瓶頸是很重要的。 如果您嘗試同時執行一些事情而未驗證單一最佳化的影響，您可能會無法追蹤哪個最佳化措施有所幫助。

### 敏捷反複專案週期 {#agile-iteration-cycles}

![chlimage_1-7](assets/chlimage_1-7.jpeg)

效能調整是一個反複進行的過程，涉及測量、分析、最佳化和驗證，直到達到目標為止。 考慮到這一點，請在最佳化階段實施敏捷的驗證程式，而不是在每個反複專案後實施更沈重的測試程式。

此焦點表示實作最佳化的開發人員應可快速判斷最佳化是否已達成目標。 此資訊很有價值，因為達到目標時，最佳化即告結束。

## 基本效能准則 {#basic-performance-guidelines}

一般而言，將未快取的html要求保留在100毫秒內。 更具體地說，以下內容可作為指引：

* 70%的頁面要求應在少於100毫秒內回應。
* 25%的頁面要求應會在100毫秒 — 300毫秒內獲得回應。
* 4%的頁面要求應會在300毫秒 — 500毫秒內獲得回應。
* 1%的頁面要求應會在500毫秒 — 1000毫秒內獲得回應。
* 沒有任何頁面的回應速度應小於1秒。

上述數字假設以下條件：

* 在發佈時測量（沒有與製作環境相關的製造費用）
* 在伺服器上測量（沒有網路負荷）
* 未快取(無AEM輸出快取，無Dispatcher快取)
* 僅適用於具有許多相依性的複雜專案(HTML、JS、PDF...)
* 系統上沒有其他載入

有些問題經常會導致效能問題，其中包括：

* Dispatcher快取效率低下
* 在一般顯示範本中使用查詢。

JVM和OS層級調整通常不會導致效能大幅提升，因此應該在最佳化週期的最後階段執行。

內容存放庫的結構方式也會影響效能。 為獲得最佳效能，附加至內容存放庫中個別節點的子節點數量不應超過1,000 （依規則）。

在平時的效能最佳化練習中，您最好的朋友是：

* 不为目标组件考虑 `request.log`
* 元件式計時
* Java™效能分析工具。

### 載入和編輯數位資產時的效能 {#performance-when-loading-and-editing-digital-assets}

由於載入和編輯數位資產時涉及大量資料，效能可能會成為一個問題。

影響效能的因素有二：

* CPU — 多重核心可在轉碼時讓工作更順暢
* 硬碟 — 平行RAID磁碟可達到相同效果

若要改善效能，請考量下列事項：

* 每天將上傳多少資產？ 一個好的估計可以基於：

![chlimage_1-77](assets/chlimage_1-77.png)

* 進行編輯的時間範圍（通常是工作日的長度，對國際作業來說更重要）。
* 已上傳影像的平均大小（以及每個影像產生的轉譯大小），以MB為單位。
* 決定平均資料速率：

![chlimage_1-78](assets/chlimage_1-78.png)

* 所有編輯中的80%都是在20%的時間中進行，所以在尖峰時間，您的資料速率是平均資料速率的四倍。 這樣的效能是您的目標。

## 性能监控 {#performance-monitoring}

效能（或缺乏效能）是使用者最先注意到的事項之一，因此對於任何具有使用者介面的應用程式而言，效能至關重要。 若要最佳化AEM安裝的效能，請監視執行個體的各種屬性及其行為。

如需有關如何執行效能監督的資訊，請參閱 [監控效能](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance).

造成效能問題的問題通常很難追蹤，即使這些問題的影響很容易看清。

基本起點是系統正常運作時對系統的良好瞭解。 除非您知道您的環境在正確執行時「外觀」和「行為」如何，否則在效能降低時很難找出問題。 請花時間調查您的系統是否順利運作，並確保收集效能資訊是一項持續的工作。 如此一來，您就有了比較效能的基礎。

下圖說明對AEM內容的請求可以採取的路徑，以及可能影響效能的不同元素數量。

![chlimage_1-79](assets/chlimage_1-79.png)

效能也是數量與容量之間的平衡：

* **音量**  — 系統處理和傳遞的輸出量。
* **容量**  — 系統傳送磁碟區的能力。

效能可於整個網路鏈的不同位置加以說明。

![chlimage_1-80](assets/chlimage_1-80.png)

影響效能的常見功能領域包括：

* 缓存
* 應用程式（您的專案）程式碼
* 搜尋功能

### 有關效能的基本規則 {#basic-rules-regarding-performance}

最佳化效能時，請謹記下列特定規則：

* 效能調整 *必須* 成為每個專案的一部分。
* 請勿在開發週期初期進行最佳化。
* 效能只和最弱的連結一樣好。
* 請一律考量容量與數量。
* 先最佳化重要事項。
* 永遠不要最佳化，不要 *逼真* 目標。

>[!NOTE]
>
>請記住，您用來測量效能的機制通常會精確影響您嘗試測量的內容。 請試著解決這些差異，並儘可能消除其影響；尤其是應儘可能停用瀏覽器外掛程式。

## 設定效能 {#configuring-for-performance}

AEM的某些方面（和/或基礎存放庫）可以設定為最佳化效能。 以下是一些可能性和建議，在進行變更之前，您必須確定您是否（或如何）使用相關功能。

>[!NOTE]
>
>另請參閱 [效能最佳化](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hans).

### 搜尋索引 {#search-indexing}

從AEM 6.0開始，Adobe Experience Manager使用Oak型存放庫架構。

您可以在這裡找到更新的索引資訊：

* [查詢和建立索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md)
* [查詢和索引](/help/sites-deploying/queries-and-indexing.md)

### 並行工作流程處理 {#concurrent-workflow-processing}

若要改善效能，請限制同時執行的工作流程數量。 依預設，工作流程引擎同時處理的工作流程，數量與Java™ VM可用的處理器數量相同。 當工作流程步驟需要大量處理資源（RAM或CPU）時，同時執行多個工作流程可能會對可用的伺服器資源造成高需求。

例如，上傳影像（或一般DAM資產）時，工作流程會自動將影像匯入DAM。 影像通常具有高解析度，可以輕鬆消耗數百MB的棧積以進行處理。 平行處理這些影像會在記憶體子系統和記憶體回收器上造成高負載。

工作流程引擎使用Apache Sling工作佇列來處理和排程工作專案處理。 預設已從Apache Sling工作佇列設定服務處理站建立下列工作佇列服務，以處理工作流程工作：

* Granite工作流程佇列：大部分的工作流程步驟（例如處理DAM資產的步驟）都會使用Granite工作流程佇列服務。
* Granite工作流程外部程式工作佇列：此服務用於特殊外部工作流程步驟，通常用於連絡外部系統和輪詢結果。 例如，「InDesign媒體提取程式」步驟會實作為外部程式。 工作流程引擎會使用外部佇列來處理輪詢。 (請參閱 [com.day.cq.workflow.exec.WorkflowExternalProcess](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/WorkflowExternalProcess.html).)

設定這些服務以限制同時執行的工作流程數量上限。

>[!NOTE]
>
>除非您已為特定工作流程模型建立工作佇列，否則設定這些工作佇列會影響所有工作流程(請參閱 [設定特定工作流程模型的佇列](/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow) 下)。

#### 存放庫中的設定 {#configuration-in-the-repo}

如果您正在設定服務 [使用sling：OsgiConfig節點](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)，您必須找到現有服務的PID，例如： org.apache.sling.event.jobs.QueueConfiguration.370aad73-d01b-4a0b-abe4-20198d85f705。 您可以使用Web主控台探索PID。

設定名為的屬性 `queue.maxparallel`.

#### Web主控台中的設定 {#configuration-in-the-web-console}

若要設定這些服務 [使用Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，找出Apache Sling工作佇列設定服務工廠下方的現有設定專案。

設定名為Maximum Parallel Jobs的屬性。

### 設定特定工作流程的佇列 {#configure-the-queue-for-a-specific-workflow}

為特定工作流程模型建立工作佇列，以便您可以為該工作流程模型設定工作處理。 如此一來，您的設定會影響特定工作流程的處理，而預設Granite工作流程佇列的設定會控制其他工作流程的處理。

工作流程模型執行時，會為特定主題建立Sling作業。 依預設，主題會符合為一般Granite工作流程佇列或Granite工作流程外部程式工作佇列設定的主題：

* `com/adobe/granite/workflow/job*`
* `com/adobe/granite/workflow/external/job*`

工作流程模型產生的實際工作主題包括模型特定的尾碼。 例如， **DAM更新資產** 工作流程模型會產生具有下列主題的工作：

`com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`

因此，您可以為符合工作流程模型之工作主題的主題建立工作佇列。 設定佇列的效能相關屬性，只會影響產生符合佇列主題之工作的工作流程模型。

下列程式會使用建立工作流程的工作佇列 **DAM更新資產** 以工作流程為例。

1. 執行您要建立工作佇列的工作流程模型，以便產生主題統計資料。 例如，將影像新增至資產以執行 **DAM更新資產** 工作流程。
1. 開啟Sling工作主控台(`https://<host>:<port>/system/console/slingevent`)。
1. 探索主控台中與工作流程相關的主題。 針對DAM更新資產，可找到下列主題：

   * `com/adobe/granite/workflow/external/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam/update_asset/jcr_content/model`
   * `com/adobe/granite/workflow/job/etc/workflow/models/dam-xmp-writeback/jcr_content/model`

1. 為每個主題建立一個工作佇列。 若要建立工作佇列，請為Apache Sling工作佇列Factory服務建立Factory設定。

   Factory設定類似於Granite工作流程佇列（如所述） [並行工作流程處理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)，但Topics屬性符合工作流程作業的主題除外。

### AEM DAM Asset Synchronization Service {#cq-dam-asset-synchronization-service}

此 `AssetSynchronizationService` 用於同步來自已掛載存放庫(包括LiveLink、Documentum®等)的資產。 根據預設，此同步會每300秒（5分鐘）進行定期檢查，因此如果您不使用掛載的存放庫，則可以停用此服務。

停用服務的完成者： [設定OSGi服務](/help/sites-deploying/configuring-osgi.md) **CQ DAM資產同步服務** 以設定 **同步處理期間** ( `scheduler.period`)至（最少）一年（以秒為單位定義）。

### 多個DAM例項 {#multiple-dam-instances}

舉例來說，部署多個DAM例項有助於改善效能：

* 由於您定期上傳許多作者環境的資產，因此您的負載很高；此處有一個單獨的DAM例項專門用於為作者提供服務。
* 您在全球各地擁有多個團隊（例如，美國、歐洲、亞洲）。

其他考量事項包括：

* 將作者上的「進行中的工作」與發佈上的「最終」分開
* 將作者上的內部使用者與外部訪客/發佈上的使用者（例如，代理、新聞代表、客戶和學生）分開。

## 品質保證的最佳實務 {#best-practices-for-quality-assurance}

效能對您的發佈環境至關重要。 因此，在實作專案時，您必須仔細規劃及分析您為發佈環境進行的效能測試。

本節旨在提供標準化概述，說明在定義測試概念時所涉及的問題，專門針對您的電腦上的效能測試， *發佈* 環境。 QA工程師、專案經理和系統管理員對這些資訊感興趣。

以下說明在「 」上，針對AEM應用程式進行效能測試的標準化方法 *發佈* 環境。 此效能測試包含下列五個階段：

* [知識驗證](#verification-of-knowledge)
* [範圍的定義](#scope-definition)
* [測試方法](#test-methodologies)
* [效能目標的定義](#defining-the-performance-goals)
* [最佳化](#optimization)

控制是額外、全方位程式 — 必要但不限於測試。

### 知識驗證 {#verification-of-knowledge}

第一步是記錄開始測試前您必須知道的基礎資訊：

* 測試環境的架構
* 詳細說明需要測試的內部元素的應用程式對應（包括單獨和組合）

#### 測試架構 {#test-architecture}

記錄用於效能測試的測試環境架構。

您需要重製您的計畫生產發佈環境，以及Dispatcher和負載平衡器。

#### 應用程式對應 {#application-map}

取得清楚的概觀，您可從其中建立整個應用程式的對應（您可能已在作者環境的測試中取得此對應）。

以圖表呈現應用程式的內部元素，可概略說明測試需求；使用色彩編碼也可作為報告的基礎。

### 範圍定義 {#scope-definition}

應用程式通常有多種使用案例。 有些使用案例很重要，有些則不重要。

為了將效能測試的範圍集中在發佈上，Adobe建議您定義以下內容：

* 最重要的業務使用案例
* 最關鍵的技術使用案例

使用案例的數量取決於您，但應限制在易於管理的數量（例如，5到10個）。

選取主要使用案例後，即可針對每個案例定義關鍵績效指標(KPI)和用於測量它們的工具。 常見KPI的範例包括：

* 端對端回應時間
* Servlet回應時間
* 單一元件的回應時間
* 服務的回應時間
* 執行緒集區中的閒置執行緒數目
* 可用連線數目
* 系統資源，例如CPU和I/O存取

### 測試方法 {#test-methodologies}

此概念有四種情境用於定義和測試效能目標：

* 單一元件測試
* 組合的元件測試
* *上線* 情境
* 錯誤案例

根據下列原則。

#### 元件中斷點 {#component-breakpoints}

* 與效能相關時，每個元件都有特定的中斷點。 換言之，元件可顯示良好的效能，直到達到特定點為止，之後效能會迅速下降。
* 若要取得應用程式的完整概觀，您必須先驗證元件，以判斷何時達到每個元件的中斷點。
* 若要尋找您可以執行負載測試的中斷點，您可以在一段時間內增加使用者人數，以建立增加的負載。 透過監控此負載和元件的回應，您會在達到元件的中斷點時遇到特定的效能行為。 可依每秒並行交易數以及並行使用者數（如果元件對此KPI敏感）來限定該點。
* 然後，此資訊可作為改善的基準，指出所使用的測量效率，並幫助定義測試案例。

#### 交易 {#transactions}

* transaction一詞用於表示完整網頁的請求，包括頁面本身和所有後續呼叫。 也就是頁面要求、任何AJAX呼叫、影像和其他物件 **請求深入研究**.
* 若要完全分析每個請求，您可以表示呼叫棧疊的每個元素，然後合計每個請求的平均處理時間。

### 定義效能目標 {#defining-the-performance-goals}

定義範圍和相關KPI後，就會設定特定的效能目標。 此程式包括設計測試案例和目標值。

在平均和尖峰狀況下測試效能。 此外，您還需要上線情境測試，以確保您的網站在首次提供時能夠滿足日益增長的興趣。

您可能從現有網站收集到的任何體驗或統計資料，也可用於決定未來的目標。 例如，來自已上線網站的熱門流量。

#### 單一元件測試 {#single-component-tests}

關鍵元件必須在平均和尖峰狀況下進行測試。

在這兩種情況下，當預先定義數量的使用者使用系統時，您都可以定義每秒的預期交易數。

| 组件 | 測試型別 | 否. 個使用者的 | Tx/秒（預期） | Tx/秒（已測試） | 描述 |
|---|---|---|---|---|---|
| 首頁單一使用者 | 平均 | 1 | 1 |  |  |
|  | 尖峰 | 1 | 3 |  |  |
| 首頁100位使用者 | 平均 | 100 | 3 |  |  |
|  | 尖峰 | 100 | 3 |  |

#### 組合元件測試 {#combined-component-tests}

組合測試元件可更密切地反映應用程式行為。 必須再次測試平均值和尖峰狀況。

| 情境 | 组件 | 否. 個使用者的 | Tx/秒（預期） | Tx/秒（已測試） | 描述 |
|---|---|---|---|---|---|
| 混合平均 | 主页 | 10 | 1 |  |  |
|  | 搜索 | 10 | 1 |  |  |
|  | 新闻 | 10 | 2 |  |  |
|  | 事件 | 10 | 1 |  |  |
|  | 啟用 | 10 | 3 |  | 作者行為的模擬。 |
| 混合尖峰 | 主页 | 100 | 5 |  |  |
|  | 搜索 | 50 | 5 |  |  |
|  | 新闻 | 100 | 10 |  |  |
|  | 事件 | 100 | 10 |  |  |
|  | 啟用 | 20 | 20 |  | 作者行為的模擬。 |

#### 上線測試 {#going-live-tests}

在您網站推出後的前幾天，您可能會對內容更感興趣。 此情境甚至大於您正在測試的峰值。 Adobe建議您測試「上線」情境，以確保系統能夠滿足這種情況。

| 情境 | 測試型別 | 否. 個使用者的 | Tx/秒（預期） | Tx/秒（已測試） | 描述 |
|---|---|---|---|---|---|
| 即將上線，尖峰 | 主页 | 200 | 20 |  |  |
|  | 搜索 | 100 | 10 |  |  |
|  | 新闻 | 200 | 20 |  |  |
|  | 事件 | 200 | 20 |  |  |
|  | 啟用 | 20 | 20 |  | 作者行為的模擬。 |

#### 錯誤案例測試 {#error-scenario-tests}

測試錯誤案例以確保系統正確且適當地反應。 不僅在於如何處理錯誤本身，而且可能影響效能。 例如：

* 當使用者嘗試在搜尋方塊中輸入無效的搜尋字詞時會發生什麼情況
* 當搜尋字詞過於籠統，以至於傳回的結果數量過多時，會發生什麼情況

設計這些測試時，請記住，並非所有情景都會定期發生。 不過，它們對整個系統的影響很重要。

| 錯誤案例 | 错误类型 | 否. 個使用者的 | Tx/秒（預期） | Tx/秒（已測試） | 描述 |
|---|---|---|---|---|---|
| 搜尋元件超載 | 搜尋全域萬用字元（星號） | 10 | 1 |  | 只搜尋&amp;ast；&amp;ast；&amp;ast；。 |
|  | 停用詞 | 20 | 2 |  | 搜尋停用詞。 |
|  | 空字串 | 10 | 1 |  | 正在搜尋空字串。 |
|  | 特殊字元 | 10 | 1 |  | 搜尋特殊字元。 |

#### 耐力測試 {#endurance-tests}

系統持續執行一段時間（小時或天）後，才會發生某些問題。 耐力測試是用來測試一段時間內固定的平均負載。 然後可以分析任何效能降低。

| 情境 | 測試型別 | 否. 個使用者的 | Tx/秒（預期） | Tx/秒（已測試） | 描述 |
|---|---|---|---|---|---|
| 耐力測試（72小時） | 主页 | 10 | 1 |  |  |
|  | 搜索 | 10 | 1 |  |  |
|  | 新闻 | 20 | 2 |  |  |
|  | 事件 | 10 | 1 |  |  |
|  | 啟用 | 1 | 3 |  | 作者行為的模擬。 |

### 最佳化 {#optimization}

在實作的後期階段，請最佳化應用程式以達成並最大化效能目標。

所做的任何最佳化都必須進行測試，以確保其具備：

* 不影響功能
* 已在發行之前通過負載測試驗證

您可使用一系列工具來協助您進行負載產生、效能監控和結果分析。 其中有些工具包含下列專案：

* [Jmeter](https://jmeter.apache.org/)
* [載入執行器](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview)
* [紅外線](https://www.infraredsoftware.com/)
* [Java™互動式設定檔](https://jiprof.sourceforge.net/)

最佳化後，請再次測試以確認影響。

### 报告 {#reporting}

持續報告可讓每個人都知道狀態。 如先前在色彩編碼中所述，架構圖可用於此狀態。

完成所有測試後，報告以下內容：

* 遇到任何嚴重錯誤
* 仍需進一步調查的非嚴重問題
* 測試期間所做的任何假設
* 任何因測試而產生的建議

## 使用Dispatcher時最佳化效能 {#optimizing-performance-when-using-the-dispatcher}

此 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 是Adobe的快取和/或負載平衡工具。 使用Dispatcher時，請考慮將您的網站快取效能最佳化。

>[!NOTE]
>
>虽然 Dispatcher 版本独立于 AEM，但 Dispatcher 文档会嵌入到 AEM 文档中。始终使用嵌入到最新版本的 AEM 文档中的 Dispatcher 文档。
>
>您可能是在单击以前版本的 AEM 文档中嵌入的 Dispatcher 文档链接后重定向到此页面。

Dispatcher提供數種內建機制，如果您的網站利用這些機制來最佳化效能。 此部分介绍了如何设计您的网站以最大限度地提高缓存优势。

>[!NOTE]
>
>Dispatcher 将缓存存储在标准 Web 服务器上，记住这一点可能会对您有所帮助。瞭解此資訊表示您可以快取可以儲存為頁面並使用URL請求的所有內容。 此外，您無法儲存Cookie、工作階段資料和表單資料等其他資料。
>
>一般而言，許多快取策略都涉及選取良好URL以及避免依賴這些額外資料。
>
>有了Dispatcher版本4.1.11，您也可以快取回應標題，請參閱 [快取HTTP回應標頭](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache).

### 計算Dispatcher快取比率 {#calculating-the-dispatcher-cache-ratio}

快取比率公式會估計快取處理的要求佔進入系統的要求總數的百分比。 若要計算快取比率，您需要下列專案：

* 要求總數。 此資訊可在Apache中取得 `access.log`. 如需詳細資訊，請參閱 [Apache官方檔案](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

* Publish執行個體服務的要求數目。 此資訊可在以下網址取得： `request.log` 執行個體的。 如需詳細資訊，請參閱 [解譯request.log](/help/sites-deploying/monitoring-and-maintaining.md#interpreting-the-request-log) 和 [尋找記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#finding-the-log-files).

計算快取比率的公式為：

* (要求總數 **減號** Publish上的要求數目) **已分割** 依要求總數計算。

例如，如果要求總數為129491，而Publish執行個體提供的要求數58959為，則快取比率為： **(129491 - 58959)/129491= 54.5%**.

如果您沒有一對一的發佈者/Dispatcher配對，請將所有Dispatcher和發佈者的請求新增在一起，以獲得精確的測量。 另請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>為獲得最佳效能，Adobe建議快取比率為90%至95%。

#### 使用一致的页面编码 {#using-consistent-page-encoding}

有了Dispatcher版本4.1.11，您可以快取回應標頭。 如果您沒有在Dispatcher上快取回應標頭，如果您將頁面編碼資訊儲存在標頭中，可能會發生問題。 在此情况下，当 Dispatcher 从缓存中提供一个页面时，Web 服务器的默认编码将用于该页面。可通过两种方式避免此问题：

* 如果您只使用一种编码，请确保 Web 服务器上使用的编码与 AEM 网站的默认编码相同。
* 若要設定編碼，請使用 `<META>` 標籤中的HTML `head` 區段，如下列範例所示：

```xml
        <META http-equiv="Content-Type" content="text/html; charset=EUC-JP">
```

#### 消除 URL 参数 {#avoid-url-parameters}

如果可能，请消除要缓存的页面的 URL 参数。例如，如果您有一个图片库，则绝不会缓存以下 URL（除非对 Dispatcher 进行[相应配置](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache)）：

```xml
www.myCompany.com/pictures/gallery.html?event=christmas&amp;page=1
```

不过，您可以将这些参数放入页面 URL 中，如下所示：

```xml
www.myCompany.com/pictures/gallery.christmas.1.html
```

>[!NOTE]
>
>此URL會呼叫與相同的頁面和相同的範本 `gallery.html`. 在模板定义中，您可以指定用于渲染页面的脚本，也可以对所有页面使用同一脚本。

#### 按 URL 进行自定义  {#customize-by-url}

如果您允许用户更改字体大小（或任何其他版面自定义设置），请确保各种自定义设置都反映在 URL 中。

例如，由于不会缓存 cookie，因此如果您将字体大小存储在 cookie（或类似机制）中，则不会为缓存的页面保留字体大小。因此，Dispatcher 会随机返回任意字体大小的文档。

在 URL 中包含字体大小作为选择器可避免出现此问题：

```xml
www.myCompany.com/news/main.large.html
```

>[!NOTE]
>
>對於大多數版面方面，也可以使用樣式表或使用者端指令碼，或同時使用兩者。 這些工具適用於快取。
>
>此策略對於列印版本也很實用，您可以在其中使用URL，例如：
>
>`www.myCompany.com/news/main.print.html`
>
>通过使用模板定义的脚本通配，您可以指定单独的脚本来渲染打印页面。

#### 使用作标题的图像文件失效 {#invalidating-image-files-used-as-titles}

如果您将页面标题或其他文本渲染为图片，建议您存储文件，以便在更新页面内容时将其删除：

1. 将图像文件放入与页面相同的文件夹中。
1. 对图像文件使用以下命名格式：

   `<page file name>.<image file name>`

例如，您可以儲存頁面的標題 `myPage.html` 在 `file myPage.title.gif`. 由于此文件会在页面更新时自动被删除，因此对页面标题进行的任何更改都会自动反映在缓存中。

>[!NOTE]
>
>图像文件不一定会实际存在于 AEM 实例上。您可以使用动态创建图像文件的脚本。随后，Dispatcher 会将文件存储在 Web 服务器上。

#### 使用于导航的图像文件失效 {#invalidating-image-files-used-for-navigation}

如果您將圖片用於導覽專案，方法基本上與標題相同，但稍微複雜一些。 将所有导航图像与目标页面一起存储。如果将两张图片用于一般或活动场景，则可以使用以下脚本：

* 一个正常显示页面的脚本。
* 一个处理“.normal”请求并返回正常图片的脚本。
* 一个处理“.active”请求并返回活动图片的脚本。

請務必使用與頁面相同的命名控制代碼來建立這些圖片，以確保內容更新會刪除這些圖片和頁面。

對於未修改的頁面，圖片會保留在快取中，儘管頁面本身會自動失效。

#### 个性化 {#personalization}

建議您將個人化限制在必要的地方。 原因如下：

* 如果您使用可随意自定义的开始页面，则用户每次请求该页面时都必须对它进行编辑。
* 相反地，如果您提供10個不同起始頁面的選擇，您可以快取每個起始頁面，進而改善效能。

>[!TIP]
>如需設定Dispatcher快取的詳細資訊，請參閱 [AEM Dispatcher快取教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/overview.html) 及其區段於 [快取受保護內容。](https://experienceleague.adobe.com/docs/experience-manager-learn/dispatcher-tutorial/chapter-1.html#dispatcher-tips-and-tricks)

如果您將使用者名稱放入標題列來個人化每個頁面（例如），則會影響效能。

>[!TIP]
>如需快取安全內容的相關資訊，請參閱 [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hans) 在Dispatcher指南中。

關於在單一頁面上混合受限制和公開內容，請考慮以下策略：使用Dispatcher中的伺服器端包含，或瀏覽器中透過Ajax的使用者端包含。

>[!TIP]
>
>如需處理混合的公開和受限制內容，請參閱 [設定Sling動態包含。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-sling-dynamic-include.html)

#### 粘性连接 {#sticky-connections}

[粘性连接](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=en#the-benefits-of-load-balancing)可确保同一个用户的文档全部在同一服务器上撰写。如果用户在退出此文件夹不久后返回，则此连接仍保持粘性。若要保留所有需要網站的粘性連線的檔案，請定義一個資料夾。 尽量不要在该文件夹中放入其他文件。如果您使用個人化頁面和工作階段資料，此案例會影響負載平衡。

#### MIME 类型 {#mime-types}

浏览器可通过两种方式确定文件的类型：

1. 透過其副檔名(例如 `.html`， `.gif`、和 `.jpg`)。
1. 按服务器随文件一起发送的 MIME 类型。

对于大多数文件，MIME 类型隐含在文件扩展名中。也就是說，

1. 透過其副檔名(例如 `.html`， `.gif`、和 `.jpg`)。
1. 按服务器随文件一起发送的 MIME 类型。

如果文件名没有扩展名，则以纯文本形式显示。

有了Dispatcher版本4.1.11，您可以快取回應標頭。 如果您沒有在Dispatcher上快取回應標頭，則MIME型別是HTTP標頭的一部分。 因此，如果您的AEM應用程式傳回的檔案沒有可辨識的檔案結尾，而是依賴MIME型別，這些檔案可能無法正確顯示。

要确保正确缓存文件，请遵循以下准则：

* 确保文件始终具有正确的扩展名。
* 避免使用具有下列URL的通用檔案服務指令碼： `download.jsp?file=2214`. 若要使用包含檔案規格的URL，請重寫指令碼。 在上一個範例中，此重寫為 `download.2214.pdf`.

## 備份效能 {#backup-performance}

本節提供一系列基準，用於評估AEM備份的效能，以及備份活動對應用程式效能的影響。 AEM備份會在系統執行時對其造成重大負載，而Adobe會測量此影響，以及嘗試調整這些效果的備份延遲設定所造成的影響。 目的是提供有關備份在真實設定中的預期效能和生產資料數量的參考資料，並提供如何估計計畫系統備份時間的指引。

### 參考環境 {#reference-environment}

#### 實體系統 {#physical-system}

本檔案中所報告的結果是從基準環境中執行的、具有下列設定的基準中取得。 此設定類似於資料中心的典型生產環境：

* HP ProLiant DL380 G6,8顆CPU x 2.533 GHz
* 序列連線SCSI 300 GB，10,000 RPM磁碟機
* 硬體RAID控制器；RAID0+5陣列中的八個磁碟機
* VMware影像CPU x 2 Intel Xeon® E5540 2.53 GHz
* Red Hat® Linux® 2.6.18-194.el5；Java™ 1.6.0_29
* 單一作者執行個體

此伺服器上的磁碟子系統速度很快，代表可用於生產伺服器的高效能RAID組態。 備份效能可能會對磁碟效能有所影響，而此環境中的結果會反映快速RAID設定的效能。 VMWare映像設定為在RAID陣列上有實體位於本機磁碟儲存區的單一大型磁碟區。

AEM設定會將存放庫和資料存放區放置在相同的邏輯磁碟區上，以及作業系統和AEM軟體。 備份的目標目錄也位於此邏輯檔案系統上。

#### 資料量 {#data-volumes}

下表說明備份效能標竿中使用的資料磁碟區大小。 首先安裝初始基準內容，然後新增其他已知數量的資料以增加備份內容的大小。 以特定增量建立備份，以表示內容大幅增加，以及一天內可能會產生的內容。 內容（頁面、影像、標籤）的分佈會大致根據實際生產資產構成。 頁面、影像和標籤限製為最多800個子頁面。 每個頁面都包含標題、Flash、文字/影像、視訊、投影片、表單、表格、雲端和轉盤元件。 影像會從大小從37 KB到594 KB的400個不重複檔案集區上傳。

| 内容 | 節點 | 页面 | 图像 | 标记 |
|---|---|---|---|---|
| 基本安裝 | 69 610 | 562 | 256 | 237 |
| 用於增量備份的小型內容 |  | +100 | +2 | +2 |
| 完整備份的大型內容 |  | +10 000 | +100 | +100 |

備份基準會重複，每次重複時都會新增其他內容集。

#### 基準案例 {#benchmark-scenarios}

備份基準涵蓋兩種主要情況：系統負載較重時進行備份，以及系統閒置時進行備份。 雖然一般建議在AEM儘可能閒置時執行備份，但在某些情況下，當系統負載不足時，必須執行備份。

* **閒置狀態**  — 在AEM上執行備份時不會執行其他活動。
* **負載不足**  — 系統從線上程式載入不到80%時執行備份。 備份延遲可依負載的不同而有所差異。

備份時間和產生的備份大小可從AEM伺服器記錄中取得。 通常建議將備份排程在AEM閒置時（例如午夜）的關閉時間。 此案例代表建議的方法。

載入由建立的頁面、刪除的頁面、周遊和查詢組成，其中大部分載入來自頁面周遊和查詢。 新增和移除太多頁面會持續增加工作區的大小，並阻礙備份完成。 指令碼使用的載入分佈是75%的頁面周遊、24%的查詢，以及1%的頁面建立（沒有巢狀子頁面的單一層級）。 閒置系統上的每秒平均交易尖峰是透過四個並行執行緒實現的，這會在測試負載下的備份時使用。

負載對備份效能的影響可藉由此應用程式負載與沒有此應用程式負載時的效能差異來估計。 備份對應用程式輸送量的影響，可透過比較每小時異動案例輸送量（有或沒有進行中的同時備份），以及備份以不同「備份延遲」設定運作的情形來找出。

* **延遲設定**  — 在數個案例中，備份延遲設定也有所變動，使用10毫秒（預設）、1毫秒和0毫秒的值來探索此設定如何影響備份效能。
* **備份型別**  — 所有備份都是存放庫的外部備份，在不建立zip檔案的情況下備份到備份目錄，除了在直接使用tar指令的比較案例中。 由於無法將增量備份建立至zip檔案，或是先前的完整備份為zip檔案，因此備份目錄方法最常用於生產環境。

### 結果摘要 {#summary-of-results}

#### 備份時間和傳輸量 {#backup-time-and-throughput}

這些基準測試的主要結果，是顯示備份時間隨備份型別和整體資料量的變化。 下圖顯示使用預裝置份組態取得的備份時間（以總頁數為函式）。

![chlimage_1-81](assets/chlimage_1-81.png)

閒置執行個體的備份時間相當一致，平均每秒0.608 MB，無論完整或增量備份為何（請參閱下圖）。 備份時間只是備份資料量的函式。 完成完整備份的時間會隨著總頁數明顯增加。 完成增量備份的時間也會隨著總頁數而增加，但速度會低很多。 由於要備份的資料量相對較少，完成增量備份所需的時間會短很多。

產生的備份大小是完成備份所需時間的主要決定因素。 下列圖表顯示作為最終備份大小函式所花費的時間。

![chlimage_1-82](assets/chlimage_1-82.png)

此圖表說明增量備份與完整備份都遵循簡單的大小與時間模式，而Adobe可以測量為傳輸量。 閒置執行個體的備份時間相當一致，平均每秒0.61 MB，無論基準環境上的完整或增量備份為何。

#### 備份延遲 {#backup-delay}

提供備份延遲引數是為了限製備份可能干擾生產工作負荷的程度。 引數會指定等待時間（以毫秒為單位），此等待時間會逐個檔案散佈到備份作業中。 整體效果部分取決於受影響檔案的大小。 測量備份效能（以MB/秒為單位）可提供一個合理的方式來比較延遲對備份的影響。

* 同時執行備份與一般應用程式載入會對一般載入的輸送量產生負面影響。
* 影響可能是輕微的（只有5%）或顯著的，導致處理量下降高達75%。 這很可能取決於應用程式。
* 備份不會對CPU造成沈重的負載，因此CPU密集的生產工作負荷受備份的影響會比I/O密集的生產工作負荷小。

![chlimage_1-83](assets/chlimage_1-83.png)

若要比較，可使用檔案系統備份(&#39;tar&#39;)來備份相同的存放庫檔案所獲得的輸送量。 tar的效能相當，但稍微高於延遲設定為零的備份。 即使設定很小的延遲，也會大幅減少備份傳輸量，而預設延遲10毫秒會導致傳輸量大幅降低。 在整體應用程式使用量低或應用程式可能閒置時可排定備份的情況下，請將延遲降低至預設值以下，讓備份能夠更快速地進行。

進行中備份的應用程式輸送量的實際影響，確實取決於應用程式和基礎建設的詳細資訊。 延遲值的選擇應該透過應用程式的實證分析進行，但應儘可能選擇較小的值，以便備份可以儘快完成。 由於延遲值的選擇與對應用程式輸送量的影響之間只有弱相關性，因此延遲的選擇應有利於縮短整體備份時間，以將備份的整體影響降至最低。 需要8小時才能完成備份，但影響傳輸量–20%的備份，其整體影響可能比需要2小時才能完成，但影響傳輸量–30%的備份更大。

### 引用 {#references}

* [管理 — 備份與還原](/help/sites-administering/backup-and-restore.md)
* [管理 — 容量與數量](/help/managing/best-practices-further-reference.md#capacity-and-volume)
