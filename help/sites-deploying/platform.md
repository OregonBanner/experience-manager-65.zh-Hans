---
title: AEM平台簡介
seo-title: Introduction to the AEM Platform
description: 本文提供AEM平台及其最重要元件的概述。
seo-description: This article provides a general overview of the AEM platform and its most important components.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# AEM平台簡介{#introduction-to-the-aem-platform}

AEM 6中的AEM平台以Apache Jackrabbit Oak為基礎。

Apache Jackrabbit Oak致力於實作可擴展且高效能的階層式內容存放庫，以作為現代世界級網站和其他高要求內容應用程式的基礎。

它是Jackrabbit 2的後續版本，並由AEM 6用作其內容存放庫CRX的預設後端。

## 設計原則和目標 {#design-principles-and-goals}

Oak實作 [JSR-283](https://jcp.org/en/jsr/detail?id=283) (JCR 2.0)規格 其主要設計目標為：

* 為大型存放庫提供更好的支援
* 多重分散式叢集節點，提供高可用性
* 更優異的效能
* 支援許多子節點和存取控制層級

## 架構概念 {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### 存储 {#storage}

儲存層的用途是：

* 實作樹狀模型
* 讓儲存裝置可插拔
* 提供叢集機制

### Oak Core {#oak-core}

Oak Core會將數個圖層新增至儲存層：

* 存取層級控制
* 搜尋和建立索引
* 觀察

### Oak JCR {#oak-jcr}

Oak JCR的主要目標是將JCR語意轉換成樹狀作業。 它也負責：

* 實作JCR API
* 包含實作JCR限制的認可掛接

此外，非Java實作現在是可行的，並且是Oak JCR概念的一部分。

## 儲存空間概覽 {#storage-overview}

Oak儲存層提供抽象層，用於實際儲存內容。

目前，AEM6提供兩種儲存實作： **Tar儲存** 和 **MongoDB儲存**.

### Tar儲存 {#tar-storage}

Tar儲存體使用tar檔案。 它會將內容儲存為較大區段中的各種記錄型別。 分錄用於追蹤存放庫的最新狀態。

建置它時圍繞幾個關鍵設計原則：

* **不可變區段**

內容會儲存在最多256 KB的區段中。 這些區段不可變動，因此可輕鬆快取經常存取的區段，並減少可能損毀存放庫的系統錯誤。

每個區段都由唯一識別碼(UUID)識別，並包含內容樹狀結構的連續子集。 此外，區段可參考其他內容。 每個區段都會保留其他參考區段的UUID清單。

* **地區**

節點及其直接子系等相關記錄會儲存在相同的區段中。 如此一來，對於每個工作階段存取多個相關節點的一般使用者端，就能快速搜尋存放庫並避免大部分的快取遺漏。

* **緊實度**

記錄格式已針對大小最佳化，以降低IO成本，並儘可能在快取中容納更多內容。

### Mongo儲存 {#mongo-storage}

MongoDB儲存體使用MongoDB進行共用和叢集。 存放庫樹狀結構會保留在一個MongoDB資料庫中，其中每個節點都是一個單獨的檔案。

它有幾個特性：

* 修訂版本

對於內容的每次更新（認可），都會建立新的修訂版本。 修訂基本上是一個字串，包含三個元素：

1. 從產生時間戳記的電腦系統時間衍生出的時間戳記
1. 用於區分使用相同時間戳記建立的修訂版本的計數器
1. 建立修訂版本的叢集節點ID

* 分支

支援分支，這可讓使用者端暫存多個變更，並在單一合併呼叫時顯示變更。

* 先前的檔案

MongoDB儲存體會在每次修改時新增資料至檔案。 不過，它只會刪除明確觸發清理的資料。 當達到特定臨界值時，就會移動舊資料。 先前檔案僅包含不可變資料，這表示它們僅包含已認可和合併的修訂版本。

* 叢集節點中繼資料

有關使用中和非使用中叢集節點的資料會保留在資料庫中，以方便叢集作業。

使用MongoDB儲存裝置的典型AEM叢集設定：

![chlimage_1-85](assets/chlimage_1-85.png)

## Jackrabbit 2有何不同？ {#what-is-different-from-jackrabbit}

由於Oak可回溯相容於JCR 1.0標準，使用者層級幾乎沒有任何變更。 不過，在設定以Oak為基礎的AEM安裝時，有一些您必須注意的差異：

* Oak不會自動建立索引。 因此，必要時必須建立自訂索引。
* 不同於Jackrabbit 2，其工作階段一律反映存放庫的最新狀態，而Oak工作階段反映從取得工作階段時起存放庫的穩定檢視。 原因在於Oak所依據的MVCC模型。
* Oak不支援相同名稱的同層級(SNS)。

## 其他平台相關檔案 {#other-platform-related-documentation}

如需AEM平台的詳細資訊，請查閱以下文章：

* [在AEM 6中設定節點存放區和資料存放區](/help/sites-deploying/data-store-config.md)
* [Oak查詢和索引](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6中的儲存元素](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM與MongoDB](/help/sites-deploying/aem-with-mongodb.md)
