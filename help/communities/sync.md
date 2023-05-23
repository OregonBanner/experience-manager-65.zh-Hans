---
title: Communities使用者同步
seo-title: Communities User Synchronization
description: 使用者同步化的運作方式
seo-description: How user synchronization works
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 2%

---

# Communities使用者同步 {#communities-user-synchronization}

## 简介 {#introduction}

在AEM Communities中，從發佈環境（取決於設定的許可權）， *網站訪客* 可能會變成 *成員*，建立 *使用者群組*，並編輯其 *成員設定檔* .

*使用者資料* 是用來指稱的術語 *使用者*， *使用者設定檔* 和 *使用者群組*.

*成員* 是用來指稱的術語 *使用者* 在發佈環境中註冊，與在作者環境中註冊的使用者不同。

如需使用者資料的詳細資訊，請造訪 [管理使用者和使用者群組](/help/communities/users.md).

## 在發佈伺服器陣列間同步使用者 {#synchronizing-users-across-a-publish-farm}

根據設計，在發佈環境中建立的使用者資料不會出現在製作環境中。

在製作環境中建立的大多數使用者資料旨在保留在製作環境中，不會同步或複製到發佈執行個體。

當 [拓撲](/help/communities/topologies.md) 是 [發佈陣列](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，對一個發佈執行個體進行的註冊和修改需要與其他發佈執行個體同步。 成員必須能夠登入並在任何發佈節點上檢視其資料。

啟用使用者同步時，系統會自動在伺服器陣列中的發佈執行個體之間同步使用者資料。

### 使用者同步設定指示 {#user-sync-setup-instructions}

如需如何跨發佈伺服器陣列啟用同步化的詳細逐步指示，請參閱：

* [使用者同步](/help/sites-administering/sync.md)

## 使用者在背景同步  {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt封裝**

   這是包含發佈商上完成的所有變更的zip檔案，這些變更需要跨發佈商分發。 發行者上的變更會產生由變更事件接聽程式挑選的事件。 這會建立包含所有變更的vlt套裝程式。

* **發佈套件**

   它包含Sling的分發資訊。 這是需要發佈內容的地點以及上次發佈時間的相關資訊。

## 當……發生什麼情況？ {#what-happens-when}

### 從社群網站主控台發佈網站 {#publish-site-from-communities-sites-console}

對作者而言，當社群網站從以下來源發佈時： [社群網站主控台](/help/communities/sites-console.md)，效果為 [復寫](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) 相關頁面和Sling會分配動態建立的社群使用者群組，包括其成員資格。

### 發佈時已建立或編輯使用者設定檔 {#user-is-created-or-edits-profile-on-publish}

依設計，在發佈環境中建立的使用者和設定檔（例如透過自我註冊、社交登入、LDAP驗證）不會出現在製作環境中。

當拓撲為 [發佈陣列](/help/communities/topologies.md) 且使用者同步已正確設定， *使用者* 和 *使用者設定檔* 會使用Sling發佈跨發佈伺服器陣列進行同步。

### 發佈時建立新的社群群組 {#new-community-group-is-created-on-publish}

雖然社群群組的建立是從發佈執行個體開始的，但實際上會在作者執行個體上發生，這會產生新的網站頁面和新使用者群組。

在程式中，新網站頁面會復寫至所有發佈執行個體。 動態建立的社群使用者群組及其成員資格會由Sling散發至所有發佈執行個體。

### 使用者或使用者群組是使用安全性主控台建立 {#users-or-user-groups-are-created-using-security-console}

根據設計，在發佈環境中建立的使用者資料不會出現在製作環境中，反之亦然。

當 [使用者管理與安全性](/help/sites-administering/security.md) console用於在發佈環境中新增使用者，使用者同步會在必要時同步新使用者及其群組成員資格到其他發佈執行個體。 使用者同步也會同步透過安全性主控台建立的使用者群組。

### 使用者發佈內容時貼文 {#user-posts-content-on-publish}

針對使用者產生的內容(UGC)，透過以下存取方式存取在發佈執行個體上輸入的資料： [已設定的SRP](/help/communities/srp-config.md).

## 最佳實務 {#bestpractices}

依預設，使用者同步為 **已停用**. 啟用使用者同步涉及修改 *現有* OSGi設定。 啟用使用者同步處理後，不應新增任何設定。

即使使用者資料並非建立於作者，使用者同步仍仰賴作者環境管理使用者資料分佈。

**前提条件**

1. 如果使用者和使用者群組已在一個發佈者上建立，建議您 [手動同步](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) 設定和啟用使用者同步之前，將使用者資料傳送給所有發行者。

   啟用使用者同步後，只會同步新建立的使用者和群組。

1. 確保已安裝最新的程式碼：

   * [AEM平台更新](https://helpx.adobe.com/cn/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

若要在AEM Communities上啟用使用者同步化，需進行下列設定。 確保這些設定正確無誤，以避免Sling內容發佈失敗。

### Apache Sling散發代理程式 — 同步代理程式工廠 {#apache-sling-distribution-agent-sync-agents-factory}

此設定會擷取要在發佈商之間同步的內容。 設定位於作者執行個體上。 作者必須追蹤所有存在的發行者以及同步所有資訊的位置。

設定中的預設值適用於單一發佈執行個體。 由於使用者同步對於同步多個發佈執行個體很有用（例如發佈伺服器陣列），因此需要向設定新增其他發佈執行個體。

**內容如何同步？**

製作執行個體ping發行者的匯出工具端點。 每當在特定發行者(n)上建立或更新使用者時，作者都會從其匯出工具端點取得內容，並且 [推送內容](/help/communities/sync.md#main-pars-image-1413756164) 至其他發佈者（n-1，與從中擷取內容的發佈者不同）。

若要設定Apache Sling同步代理程式設定：

1. 以管理員許可權登入您的AEM編寫執行個體。
1. 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 尋找 **Apache Sling散發代理程式 — 同步代理程式工廠**.

   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

      驗證名稱： **socialpubsync。**

   * 选中&#x200B;**启用**&#x200B;复选框。
   * 選取 **使用多個佇列。**
   * 指定 **匯出工具端點** 和 **匯入工具端點** （您可以新增更多匯出工具與匯入工具端點）。

      這些端點會定義您要從何處取得內容，以及您要推送內容的位置。 作者會從指定的匯出工具端點擷取內容，並將內容推送至發行者（而非從中擷取內容的發行者）。
   ![sync-agent-fact](assets/sync-agent-fact.png)

### AdobeGranite發佈 — 加密的密碼傳輸機密提供者 {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

它可讓作者識別授權的使用者，因為具有從作者同步使用者資料到發佈的許可權。

此 [已建立授權使用者](/help/sites-administering/sync.md#createauthuser) 在所有發佈執行個體上協助發佈者與作者連線並在作者上設定Sling發佈。 此授權使用者擁有所有必要條件 [ACL](/help/sites-administering/sync.md#howtoaddacl).

每當要在發行者上安裝或從發行者擷取資料時，作者就會使用此設定中設定的認證（使用者名稱和密碼）與發行者連線。

若要使用授權使用者將作者與發佈者連線：

1. 以管理員許可權登入您的AEM編寫執行個體。
1. 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 尋找 **AdobeGranite發佈 — 加密的密碼傳輸機密提供者。**
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證屬性 **socialpubsync** - **publishUser。**

1. 將使用者名稱和密碼設定為 [授權使用者](/help/sites-administering/sync.md#createauthorizeduser).

   例如， **usersync — 管理員**

![granite-passwrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling散發代理程式 — 佇列代理程式工廠 {#apache-sling-distribution-agent-queue-agents-factory}

此設定用於設定您要跨發行者同步的資料。 在指定的路徑中建立/更新資料時 **允許的根**，會啟動「var/community/distribution/diff」，而建立的復寫器會從發行者擷取資料，並安裝在其他發行者上。

若要設定要同步的資料（節點路徑）：

1. 以管理員許可權登入您的發佈執行個體。
1. 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. 尋找 **Apache Sling散發代理程式 — 佇列代理程式工廠**.
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證名稱： **socialpubsync -reverse**

1. 選取 **已啟用** 核取方塊並儲存。
1. 指定要復寫的節點路徑 **允許的根**.
1. 針對每個專案重複 **發佈** 執行個體。

   ![queue-agents-fact](assets/queue-agents-fact.png)

### AdobeGranite發佈 — 觀察者工廠差異 {#adobe-granite-distribution-diff-observer-factory}

此設定會同步發佈者之間的群組成員資格。
如果變更一個發行者中群組的成員資格，並不會更新其他發行者的成員資格，請確定 **ref ：members** 新增至 **已檢視的屬性名稱**.

若要確保成員同步化：

1. 以管理員許可權登入您的發佈執行個體。
1. 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. 尋找 **AdobeGranite發佈 — 觀察者工廠差異**.
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證 **代理程式名稱： socialpubsync -reverse**.

1. 选中&#x200B;**启用**&#x200B;复选框。
1. 指定 **rep：members** 作為propertyName的說明，在 **已檢視的屬性名稱**，並儲存。

   ![diff-obs](assets/diff-obs.png)

### Apache Sling散發觸發程式 — 排程觸發程式Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

此設定可讓您設定輪詢間隔（之後發佈者會被釘選且作者會提取變更），以便在發佈者之間同步變更。

作者每30秒輪詢發佈者（預設）。 如果資料夾中存在任何套件 `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`，然後它會擷取這些套件，並安裝在其他發行者上。

變更輪詢間隔：

1. 以管理員許可權登入您的AEM編寫執行個體。
1. 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md)例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 尋找 **Apache Sling散發觸發程式 — 排程觸發程式Factory**

   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

      驗證 **socialpubsync -scheduled-trigger**

   * 將「間隔」（以秒為單位）設定為所需的間隔，然後儲存。

   ![排程觸發程式](assets/scheduled-trigger.png)

### AEM Communities使用者同步接聽程式 {#aem-communities-user-sync-listener}

針對Sling發佈中訂閱和所關注內容不一致的問題，檢查中是否有下列屬性 **AEM Communities使用者同步接聽程式** 設定已設定：

* 節點型別
* Ignorableproperties
* IgnorableNodes
* DistributedFolders

若要同步訂閱、追蹤和通知

在每個AEM發佈執行個體上：

1. 以管理員許可權登入。
1. 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. 尋找 **AEM Communities使用者同步接聽程式**.
1. 選取現有設定以開啟以進行編輯（鉛筆圖示）

   驗證名稱： **socialpubsync -scheduled-trigger**

1. 設定下列專案 **節點型別**：

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   此屬性中指定的節點型別將會同步，而且通知資訊（後續的部落格和設定）會在不同的發行者之間同步。

1. 新增要在其中同步處理的所有資料夾 **DistributedFolders**. 例如，

   `segments/scoring`

   `social/relationships`

   `activities`

1. 設定 **ignorablenodes** 至：

   `.tokens`

   `system`

   `rep:cache` （由於我們使用粘性工作階段，因此不需要將此節點同步至不同的發佈者）。

   ![user-sync-listner](assets/user-sync-listner.png)

### 唯一的Sling ID {#unique-sling-id}

AEM作者執行個體會使用Sling ID來識別資料的來源以及需要（或不需要）將套件傳回到的發行者。

請確定發佈伺服器陣列中的所有發佈者都有唯一的Sling ID。 如果發佈伺服器陣列中多個發佈執行個體的Sling ID相同，則使用者同步將會失敗。 由於作者不知道從何處擷取套件以及在何處安裝套件。

若要確保發佈伺服器陣列中發佈者的唯一Sling ID，請在每個發佈執行個體上：

1. 瀏覽至 [https://_host：port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. 檢查值 **Sling ID**.

   ![slingid](assets/slingid.png)

   如果發佈執行個體的Sling ID符合任何其他發佈執行個體的Sling ID，則：

1. 停止具有相符的Sling ID的其中一個發佈執行個體。
1. 在 `crx-quickstart/launchpad/felix` 目錄，搜尋並刪除名為的檔案 *sling.id.file.*

   例如，在Linux系統上：

   `rm -i $(find . -type f -name sling.id.file)`

   例如，在Windows系統上：

   使用Windows檔案總管並搜尋 `sling.id.file`

1. 啟動發佈執行個體。 啟動時，系統會為其指派新的Sling ID。
1. 驗證 **Sling ID** 現在是唯一的。

重複這些步驟，直到所有發佈執行個體都具備唯一的Sling ID為止。

### Vault Package Builder工廠 {#vault-package-builder-factory}

若要正確同步更新，必須修改儲存庫封裝產生器以方便使用者同步。
在 `/home/users`， a `*/rep:cache` 節點已建立。 它是快取，用來尋找如果我們查詢節點的主體名稱，則可以直接使用此快取。

若發生下列情況，使用者同步處理可以停止： `rep :cache` 節點會在發佈者之間同步。

若要確保跨發行者正確同步更新，請在每個AEM發佈執行個體上：

1. 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md)

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. 找到 **Apache Sling Distribution Packaging - Vault Package Builder Factory**

   產生器名稱： socialpubsync-vlt。

1. 選取編輯圖示。
1. 新增兩個套件節點篩選器：
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. 原則處理
   * 若要以新節點覆寫現有的rep ：policy節點，請新增第三個套件篩選器： `/home/users|+.*/rep:policy`
   * 若要防止散佈原則，請設定： `Acl Handling: IGNORE`

   ![Vault封裝產生器原廠](assets/vault-package-builder-factory.png)

## 疑難排解AEM Communities中的Sling發佈 {#troubleshoot-sling-distribution-in-aem-communities}

如果Sling發佈失敗，請嘗試以下偵錯步驟：

1. **檢查 [不適當地新增設定](/help/sites-administering/sync.md#improperconfig)**

   確保未新增或編輯多個設定，而是應編輯現有的預設設定。
1. **檢查設定**

   確定所有 [設定](/help/communities/sync.md#bestpractices) 已在您的AEM Author例項中適當設定，如 [最佳實務](/help/communities/sync.md#main-pars-header-863110628).

1. **檢查授權的使用者許可權**

   如果套件未正確安裝，請檢查 [授權使用者](/help/sites-administering/sync.md#createauthuser) 在第一個發佈執行個體中建立的ACL是正確的。

   若要驗證此專案，請避免驗證 [已建立授權使用者](/help/sites-administering/sync.md#createauthuser) 變更 [AdobeGranite發佈 — 加密的密碼傳輸機密提供者](/help/sites-administering/sync.md#adobegraniteencpasswrd) 作者執行個體的設定，以使用管理員使用者認證。 現在，請嘗試重新安裝套件。 如果使用者同步處理可順利與管理員憑證搭配使用，則表示已建立的發佈使用者沒有適當的ACL。

1. **檢查Diff Observer Factory設定**

   如果只有特定節點未跨發佈伺服器陣列同步（例如，群組成員未同步），則請確定 [AdobeGranite發佈 — 觀察者工廠差異](/help/sites-administering/sync.md#diffobserver) 設定已啟用且 **rep： members** 設定於 **已檢視的屬性名稱**.

1. **檢查AEM Communities使用者同步接聽程式設定。** 如果建立的使用者已同步，但訂閱和後續內容無法運作，請確定AEM Communities使用者同步接聽程式設定已：

   * 節點型別 — 設為 **rep：User， nt：unstructured**， **nt：resource**， **rep：ACL**， **sling：Folder**、和 **sling：OrderedFolder**.
   * 可忽略的節點 — 設為 **.tokens**， **系統**、和 **rep：cache**.
   * 分散式資料夾 — 設定為您要分散式資料夾。

1. **檢查在發佈執行個體上建立使用者時產生的記錄**

   如果上述設定已適當設定，但使用者同步無法運作，請檢查使用者建立時產生的記錄。

   檢查記錄檔的順序是否相同，如下所示：

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

若要偵錯：

1. 停用使用者同步化：
1. 在AEM編寫執行個體上，使用管理員許可權登入。

   1. 存取 [網頁主控台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 找到設定 **Apache Sling散發代理程式 — 同步代理程式工廠**.
   1. 取消選取 **已啟用** 核取方塊。

      在製作執行個體上停用使用者同步時，（匯出工具和匯入工具）端點會停用，而且製作執行個體是靜態的。 此 **vlt** 作者不會擷取或擷取套件。

      現在，如果在發佈執行個體上建立使用者， **vlt** 封裝建立於 */var/sling/distribution/packages/ socialpubsync - vlt /data* 節點。 以及作者是否將這些套件推送至其他服務。 您可以下載並解壓縮此資料，以檢查所有屬性推送至其他服務的內容。

1. 前往發行者，並在發行者上建立使用者。 因此，會建立事件。
1. 檢查 [記錄順序](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)，於使用者建立時建立。
1. 檢查是否 **vlt** 套件建立於 **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. 現在，請在AEM編寫執行個體上啟用使用者同步。
1. 在發佈者上，變更中的匯出工具或匯入工具端點 **Apache Sling散發代理程式 — 同步代理程式工廠**.
我們可以下載並擷取套件資料，以檢查哪些所有屬性已推送至其他發佈者，以及哪些資料會遺失。
