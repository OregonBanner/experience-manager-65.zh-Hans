---
title: SRP — 社群內容儲存
seo-title: SRP - Community Content Storage
description: 自AEM Communities 6.1起，使用者產生的內容(UGC)會儲存在儲存資源提供者(SRP)提供的單一通用存放區中
seo-description: As of AEM Communities 6.1, user generated content (UGC) is stored in a single, common store provided by a storage resource provider (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# SRP — 社群內容儲存 {#srp-community-content-storage}

## 简介 {#introduction}

自AEM Communities 6.1起，使用者產生的內容(UGC)會儲存在儲存資源提供者(SRP)提供的單一通用存放區中。 有數個SRP選項可供選擇，例如ASRP、MSRP和JSRP。

與舊版不同，UGC不會跨AEM執行個體進行反向/正向復寫。 SRP會讓UGC可從所有製作和發佈執行個體中直接存取建立、讀取、更新和刪除(CRUD)操作，但JSRP除外。

以下是 [每個SRP選項的特性](#characteristics-of-srp-options)，在選擇適當的SRP和時，這對決策程式至關重要 [基礎部署](/help/communities/topologies.md).

如需有關使用SRP for UGC的詳細資訊，請參閱 [儲存資源提供者概觀](/help/communities/srp.md).

>[!NOTE]
>
>SRP僅適用於社群內容。 它不會影響網站內容的儲存位置([節點存放區](/help/sites-deploying/data-store-config.md))，且不會影響AEM執行個體之間使用者註冊、使用者設定檔和使用者群組的安全處理(另請參閱 [管理使用者資料](#managing-user-data))。

>[!CAUTION]
>
>自AEM 6.1起， [從未復寫UGC](#ugc-never-replicated).
>
>當部署不包含通用存放區（例如預設值）時 [JSRP](/help/communities/topologies.md#jsrp) 拓朴，UGC只會顯示在輸入它的AEM發佈或作者執行個體上。 只有當拓撲包含發佈叢集時，才能在任何發佈執行個體上看到UGC。

## SRP選項的特性 {#characteristics-of-srp-options}

[ASRP -Adobe儲存資源提供者](/help/communities/asrp.md)

透過此選項，UGC會從遠端儲存在由Adobe託管和管理的雲端服務中。 它需要額外的授權，並與帳戶代表合作，為該特定授權布建帳戶。 ASRP需要：

* Adobe提供並支援的相關雲端服務，可儲存社群內容。
* 在特定地區（美國、歐洲、中東及非洲、亞太地區）選擇資料中心。

* 所有對UGC的程式設計存取權都是透過SRP API進行。

ASRP適合：

* 適用於TarMK發佈陣列。
* 當無意投資本機儲存時。

>[!NOTE]
>
>在ASRP中，將附件上傳至貼文（或註解）有一項限制，即50 MB。

[MSRP - MongoDB儲存資源提供者](/help/communities/msrp.md)

透過此選項，UGC會直接保留在本機MongoDB執行個體中。

MSRP需要：

* MongoDB的本機、授權安裝以儲存社群內容。
* Apache Solr的本機安裝。
* 所有對UGC的程式設計存取權都是透過SRP API進行。

ASRP適合：

* 適用於現有的TarMK發佈陣列。
* MongoMK或RdbMK叢集。
* 預期會有大量社群內容時。

[DSRP — 關聯式資料庫儲存資源提供者](/help/communities/dsrp.md)

使用此選項，UGC會直接保留在本機MySQL資料庫執行個體中。

DSRP需要：

* 本機安裝的MySQL以儲存社群內容。
* Apache Solr的本機安裝。
* 所有對UGC的程式設計存取權都是透過SRP API進行。

DSRP適合：

* 適用於現有的TarMK發佈陣列。
* MongoMK或RdbMK叢集。
* 預期會有大量社群內容時。

[JSRP - JCR儲存資源提供者](/help/communities/jsrp.md)

使用預設選項時，沒有通用存放區。 UGC只會保留在與輸入它的AEM執行個體相同的JCR存放庫中。

JSRP：

* 將社群內容儲存在AEM作者或發佈執行個體的JCR存放庫中。
* 需要透過SRP API以程式設計方式存取UGC。
* 如果部署了多個發佈執行個體，則需要發佈叢集（TarMK陣列中的發佈執行個體之間沒有復寫機制）。
* 稽核僅在發佈環境中執行（製作和發佈之間沒有反向/正向復寫機制）。
* 最適合用於開發、示範和訓練。

## 設定SRP {#configuring-srp}

根據基礎部署，指定預設儲存選項是透過 [儲存設定主控台](/help/communities/srp-config.md).

如需每個選項的組態詳細資訊，請參閱：

* [ASRP -Adobe儲存資源提供者](/help/communities/asrp.md)
* [MSRP - MongoDB儲存資源提供者](/help/communities/msrp.md)
* [DSRP — 關聯式資料庫儲存資源提供者](/help/communities/dsrp.md)
* [JSRP - JCR儲存資源提供者](/help/communities/jsrp.md)

如果未主動選取儲存體選項，預設會啟用JSRP。

## 附加信息 {#additional-information}

### 從未復寫UGC {#ugc-never-replicated}

在作者環境中，作者會建立頁面內容並將其複製到發佈環境。 當頁面包含互動式AEM Communities功能（例如評論、評論、論壇、部落格或QnA）時，成員（已登入網站訪客）在發佈執行個體上的互動會導致使用者產生的內容(UGC)進入發佈環境。

之前，系統會將此社群內容反向復寫至製作執行個體，並將製作內容反向復寫至發佈執行個體。 使用反向和正向復寫來維護AEM執行個體之間的一致性有問題。

從AEM Communities 6.1開始，如上所述，透過針對UGC使用共用儲存空間，消除了複製UGC的需求。

複製網站內容時，絕不會複製UGC。

### 管理使用者資料 {#managing-user-data}

社群感興趣的還有 [*使用者*， *使用者群組*、和 *使用者設定檔*](/help/communities/users.md). 當拓朴為時，在發佈環境中建立和更新此使用者相關資料時，必須可供其他發佈執行個體使用 [發佈陣列](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

自AEM Communities 6.1起，使用Sling發佈（而非復寫）來同步使用者相關資料。 如需詳細資訊，請造訪 [使用者同步](/help/communities/sync.md).

### 升級至AEM Communities 6.5 {#upgrading-to-aem-communities}

升級至AEM 6.5 Communities時，如果需要保留既有的UGC，則應該根據AEM 5.6.1或AEM 6.0社群使用的是Adobe隨選儲存還是內部部署UGC儲存，採取步驟。

如需詳細資訊，請造訪 [升級至AEM Communities 6.5](/help/communities/upgrade.md).
