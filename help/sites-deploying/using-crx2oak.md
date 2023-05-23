---
title: 使用CRX2Oak移轉工具
seo-title: Using the CRX2Oak Migration Tool
description: 瞭解如何使用CRX2Oak移轉工具。
seo-description: Learn how to use the CRX2Oak migration tool.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# 使用CRX2Oak移轉工具{#using-the-crx-oak-migration-tool}

## 简介 {#introduction}

CRX2Oak是一種工具，專為在不同存放庫之間遷移資料而設計。

它可用來將資料從以Apache Jackrabbit 2為基礎的舊CQ版本移轉至Oak，也可用來在Oak存放庫之間複製資料。

您可以從公共Adobe存放庫下載最新版本的crx2oak，網址為：
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

>[!NOTE]
>
>如需Apache Oak和AEM持續性的重要概念的詳細資訊，請參閱 [AEM平台簡介](/help/sites-deploying/platform.md).

## 移轉使用案例 {#migration-use-cases}

此工具可用於：

* 從較舊的CQ 5版本移轉至AEM 6
* 在多個Oak存放庫之間複製資料
* 在不同的Oak MicroKernel實作之間轉換資料。

對於使用外部Blob存放區（通常稱為資料存放區）移轉存放庫的支援以不同的組合提供。 一個可能的移轉路徑來自使用外部的CRX2存放庫 `FileDataStore` 使用至Oak存放庫 `S3DataStore`.

下圖說明CRX2Oak支援的所有可能移轉組合：

![chlimage_1-151](assets/chlimage_1-151.png)

## 功能 {#features}

CRX2Oak是在AEM升級期間以使用者可以指定預先定義的移轉設定檔的方式來呼叫，以自動重新設定持續性模式。 這稱為快速入門模式。

如果需要更多自訂，也可以單獨執行。 不過，請注意，在此模式中，變更只會針對存放庫進行，而且需要手動執行任何額外的AEM重新配置。 這稱為獨立模式。

另外需要注意的是，若使用獨立模式中的預設設定，則只會移轉節點存放區，而新的存放庫會重複使用舊的二進位存放區。

### 自動快速入門模式 {#automated-quickstart-mode}

自AEM 6.3起，CRX2Oak就能夠處理使用者定義的移轉設定檔，這些設定檔可設定所有可用的移轉選項。 這樣既可擁有更高的靈活性，又可自動設定AEM，這些功能在獨立模式下使用工具時不可用。

若要將CRX2Oak切換為快速啟動模式，您需要透過此作業系統環境變數在AEM安裝目錄中定義crx-quickstart資料夾的路徑：

**對於基於UNIX的系統和macOS：**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**對於Windows：**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### 恢复支持 {#resume-support}

移轉作業可隨時中斷，之後可繼續進行。

#### 可自訂的升級邏輯 {#customizable-upgrade-logic}

自訂Java邏輯也可以使用來實作 `CommitHooks`. 自訂 `RepositoryInitializer` 類別可以實作，以便使用自訂值初始化存放庫。

#### 支援記憶體對應作業 {#support-for-memory-mapped-operations}

CRX2Oak預設也支援記憶體對應作業。 記憶體對應可大幅提升效能，應儘可能使用。

>[!CAUTION]
>
>但是請注意，Windows平台不支援記憶體對應作業。 因此，建議新增 **—disable-mmap** 在Windows上執行移轉時的引數。

#### 選擇性移轉內容 {#selective-migration-of-content}

依預設，工具會移轉以下專案下的整個存放庫 `"/"` 路徑。 不過，您可以完全控制應該移轉哪些內容。

如果新執行個體上有不需要的內容任何部分，您可以使用 `--exclude-path` 用於排除內容並最佳化升級程式的引數。

#### 路徑合併 {#path-merging}

如果需要在兩個存放庫之間複製資料，且您的內容路徑在兩個執行個體上不同，您可以在以下位置定義該資料： `--merge-path` 引數。 完成後，CRX2Oak只會將新節點複製到目的地存放庫，並保留舊節點。

![chlimage_1-152](assets/chlimage_1-152.png)

#### 版本支援 {#version-support}

依預設，AEM會建立每個要修改的節點或頁面的版本，並將其儲存在存放庫中。 然後可以使用版本將頁面還原到先前的狀態。

不過，即使刪除原始頁面，系統也不會清除這些版本。 處理已運作很久的存放庫時，移轉可能需要處理大量由孤立版本造成的重複資料。

對於這些型別的情況來說，一個有用的功能是新增 `--copy-versions` 引數。 它可用來在移轉或存放庫複製期間略過版本節點。

您也可以選擇是否要透過新增來複製孤立版本 `--copy-orphaned-versions=true`.

這兩個引數也支援 `YYYY-MM-DD` 日期格式，以備您在不遲於特定日期復製版本時使用。

![chlimage_1-153](assets/chlimage_1-153.png)

#### 開放原始碼版本 {#open-source-version}

CRX2Oak的開放原始碼版本以Oak-upgrade的形式提供。 除了以下功能外，支援其他所有功能：

* CRX2支援
* 移轉設定檔支援
* 支援自動化AEM重新配置

請參閱 [Apache檔案](https://jackrabbit.apache.org/oak/docs/migration.html) 以取得詳細資訊。

## 参数 {#parameters}

### 節點存放區選項 {#node-store-options}

* `--cache`：快取大小（預設為MB） `256`)

* `--mmap`：啟用區段存放區的記憶體對應檔案存取
* `--src-password:` 來源RDB資料庫密碼

* `--src-user:` 來源RDB的使用者

* `--user`：目標RDB的使用者

* `--password`：目標RDB的密碼。

### 移轉選項 {#migration-options}

* `--early-shutdown`：在複製節點後和套用認可掛接前關閉來源JCR2存放庫
* `--fail-on-error`：如果無法從來源存放庫讀取節點，則強制移轉失敗。
* `--ldap`：將LDAP使用者從CQ 5.x執行個體移轉至Oak型執行個體。 為了讓此功能發揮作用，Oak設定中的身分提供者必須命名為ldap。 如需詳細資訊，請參閱 [LDAP檔案](/help/sites-administering/ldap-config.md).

* `--ldap-config:` 請將此與 `--ldap` 使用多個LDAP伺服器進行驗證的CQ 5.x存放庫引數。 您可以使用它指向CQ 5.x `ldap_login.conf` 或 `jaas.conf` 組態檔。 格式為 `--ldapconfig=path/to/ldap_login.conf`.

### 版本存放區選項 {#version-store-options}

* `--copy-orphaned-versions`：略過複製孤立版本。 支援的引數包括： `true`， `false` 和 `yyyy-mm-dd`. 默认为 `true`.

* `--copy-versions:` 復製版本儲存空間。 引數： `true`， `false`， `yyyy-mm-dd`. 默认为 `true`.

#### 路徑選項 {#path-options}

* `--include-paths:` 複製期間要包含的以逗號分隔的路徑清單
* `--merge-paths`：複製期間要合併的逗號分隔路徑清單
* `--exclude-paths:` 複製期間要排除的逗號分隔路徑清單。

### 來源Blob存放區選項 {#source-blob-store-options}

* `--src-datastore:` 要作為來源使用的資料存放區目錄 `FileDataStore`

* `--src-fileblobstore`：要當作來源使用的資料存放區目錄 `FileBlobStore`

* `--src-s3datastore`：要用於來源的資料存放區目錄 `S3DataStore`

* `--src-s3config`：來源的設定檔 `S3DataStore`.

### 目的地BlobStore選項 {#destination-blobstore-options}

* `--datastore:` 用作目標的資料存放區目錄 `FileDataStore`

* `--fileblobstore:` 用作目標的資料存放區目錄 `FileBlobStore`

* `--s3datastore`：用於目標的資料存放區目錄 `S3DataStore`

* `--s3config`：目標的設定檔案 `S3DataStore`.

### 說明選項 {#help-options}

* `-?, -h, --help:` 顯示說明資訊。

## 调试 {#debugging}

您也可以啟用移轉程式的偵錯資訊，以便疑難排解程式期間可能出現的任何問題。 您可以根據您想要在其中執行工具的模式來採取不同的做法：

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak模式</strong></td>
   <td><strong>操作</strong></td>
  </tr>
  <tr>
   <td>快速入門模式</td>
   <td>您可以新增 <strong> — 記錄層級TRACE</strong> 或 <strong> — 記錄層級DEBUG </strong>執行CRX2Oak時命令列的選項。 在此模式中，記錄檔會自動重新導向至 <strong>upgrade.log檔案</strong>.</td>
  </tr>
  <tr>
   <td>獨立模式</td>
   <td><p>新增 <strong>—trace</strong> CRX2Oak命令列的選項，以在標準輸出上顯示TRACE事件（您需要使用重新導向字元：'&gt;'或'tee'命令自行重新導向記錄，以供稍後檢查）。</p> </td>
  </tr>
 </tbody>
</table>

## 其他考量 {#other-considerations}

移轉至MongoDB復本集時，請務必將 `WriteConcern` 引數至 `2` 與Mongo資料庫的所有連線。

您可以新增 `w=2` 連線字串結尾的引數，如下所示：

```xml
java -Xmx4092m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>如需詳細資訊，請參閱MongoDB連線字串檔案，網址為 [撰寫關注事項](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).
