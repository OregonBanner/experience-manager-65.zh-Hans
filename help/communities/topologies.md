---
title: 社群適用的建議拓撲
seo-title: Recommended Topologies for Communities
description: 如何處理使用者產生的內容(UGC)
seo-description: How to approach the handling of user-generated content (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 社群適用的建議拓撲 {#recommended-topologies-for-communities}

自AEM Communities 6.1起，已採用獨特方法來處理網站訪客（成員）從發佈環境提交的使用者產生內容(UGC)。

此方法與AEM平台處理網站內容的方式截然不同，網站內容通常是由製作環境管理。

AEM平台使用節點存放區，將網站內容從製作者複製到發佈者，而AEM Communities則使用單一、通用存放區，用於永不複製的UGC。

對於常見的UGC存放區，必須選擇 [儲存資源提供者(SRP)](working-with-srp.md). 建議的選項包括：

* [DSRP — 關聯式資料庫儲存資源提供者](dsrp.md)
* [MSRP - MongoDB儲存資源提供者](msrp.md)
* [ASRP -Adobe儲存資源提供者](asrp.md)

一個其他SRP選項， [JSRP - JCR儲存資源提供者](jsrp.md)不支援作者和發佈環境共同的UGC存放區以存取。

需要共用存放區會導致下列建議拓撲。

>[!NOTE]
>
>若為AEM Communities， [從未復寫UGC](working-with-srp.md#ugc-never-replicated).
>
>當部署不包含 [公用存放區](working-with-srp.md)，UGC只會顯示在輸入它的AEM發佈或作者執行個體上。

>[!NOTE]
>
>如需AEM平台的詳細資訊，請參閱 [建議的部署](../../help/sites-deploying/recommended-deploys.md) 和 [AEM平台簡介](../../help/sites-deploying/data-store-config.md).

## 用於生產 {#for-production}

為UGC建立共用存放區至關重要，因此基礎部署取決於其支援共用存放區的能力。

兩個範例：

1. 如果UGC的預期數量很高，而且可以建立本機MongoDB執行個體，則選項會是 [MSRP](msrp.md).

1. 為獲得頁面內容的最佳效能，請選擇 [發佈陣列](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) 和 [ASRP](asrp.md) 會以相對直接的操作，提供最佳的UGC規模調整。

對於這兩者，部署可能基於任何OAK微核心。

若要選擇適當的通用存放區，請仔細考慮唯一的 [特性](working-with-srp.md#characteristics-of-srp-options) 每個。

如需Oak微核心的詳細資訊，請造訪 [建議的部署](../../help/sites-deploying/recommended-deploys.md).

### TarMK發佈陣列 {#tarmk-publish-farm}

當拓撲為發佈伺服器陣列時，重要的相關主題為：

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

### 建議：DSRP、MSRP或ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | 網站內容存放庫 | 使用者產生的CONTENTREPOSITORY | 儲存資源提供者 | 公用存放區 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任何 | JCR | MySQL | DSRP | 是 |
| 任何 | JCR | MongoDB | MSRP | 是 |
| 任何 | JCR | Adobe隨需儲存空間 | ASRP | 是 |

### JSRP {#jsrp}


| 部署 | 網站內容存放庫 | 使用者產生的CONTENTREPOSITORY | 儲存資源提供者 | 公用存放區 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK陣列（預設） | JCR | JCR | JSRP | 否 |
| Oak叢集 | JCR | JCR | JSRP | 僅用於發佈環境 |

## 適用於開發 {#for-development}

對於非生產環境， [JSRP](jsrp.md) 提供簡易功能，讓您輕鬆設定具有一個製作執行個體和一個發佈執行個體的開發環境。

若選擇 [ASRP](asrp.md)， [DSRP](dsrp.md) 或 [MSRP](msrp.md) 對於生產環境，也可以使用Adobe隨選儲存或MongoDB來設定類似的開發環境。 如需範例，請參閱 [如何設定MongoDB以進行示範](demo-mongo.md).

## 引用 {#references}

* [使用者同步](sync.md)

   討論發佈伺服器陣列執行個體之間的使用者資料同步化。

* [管理使用者和使用者群組](users.md)

   討論使用者和使用者群組在製作和發佈環境中的角色。

* UGC [公用存放區](working-with-srp.md)

   說明與網站內容分開的社群內容儲存。

* [節點存放區和資料存放區](../../help/sites-deploying/data-store-config.md)

   網站內容基本上會儲存在節點存放區中。 對於資產，資料存放區可設定為儲存二進位資料。 對於Communities，必須設定通用存放區以選取SRP。

* [儲存體元素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   說明兩個節點儲存實作：Tar和MongoDB。
