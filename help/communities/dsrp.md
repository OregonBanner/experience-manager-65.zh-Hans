---
title: DSRP — 關聯式資料庫儲存資源提供者
seo-title: DSRP - Relational Database Storage Resource Provider
description: 設定AEM Communities以使用關聯式資料庫作為其一般存放區
seo-description: Set up AEM Communities to use a relational database as its common store
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# DSRP — 關聯式資料庫儲存資源提供者 {#dsrp-relational-database-storage-resource-provider}

## 關於DSRP {#about-dsrp}

當AEM Communities設定為使用關聯式資料庫作為其通用存放區時，使用者產生的內容(UGC)可從所有製作和發佈執行個體存取，而不需要同步或復寫。

另請參閱 [SRP選項的特性](working-with-srp.md#characteristics-of-srp-options) 和 [建議的拓撲](topologies.md).

## 要求 {#requirements}

* [MySQL](#mysql-configuration)，關聯式資料庫。
* [Apache Solr](#solr-configuration)，搜尋平台。

>[!NOTE]
>
>預設儲存設定現在儲存在conf path(`/conf/global/settings/community/srpc/defaultconfiguration`)而非etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)。 建議您遵循 [移轉步驟](#zerodt-migration-steps) 讓defaultsrp如預期運作。

## 關聯式資料庫組態 {#relational-database-configuration}

### MySQL設定 {#mysql-configuration}

MySQL安裝可以使用不同的資料庫（綱要）名稱以及不同的連線（伺服器：連線埠），在啟用功能與相同連線集區內的通用存放區(DSRP)之間共用。

如需安裝和設定詳細資訊，請參閱 [DSRP的MySQL組態](dsrp-mysql.md).

### Solr 配置 {#solr-configuration}

可以使用不同的集合，在節點存放區(Oak)與共用存放區(SRP)之間共用Solr安裝。

如果同時大量使用Oak和SRP集合，則可能會基於效能原因安裝第二個Solr。

對於生產環境，SolrCloud模式比獨立模式（單一本機Solr設定）提供更優異的效能。

如需安裝和設定詳細資訊，請參閱 [SRP的Solr設定](solr.md).

### 選取DSRP {#select-dsrp}

此 [儲存設定主控台](srp-config.md) 允許選取預設儲存設定，以識別要使用的SRP實作。

在作者上，存取「儲存設定」主控台

* 以管理員許可權登入
* 從 **主功能表**

   * 選取 **[!UICONTROL 工具]** （從左側窗格）
   * 選取 **[!UICONTROL Communities]**
   * 選取 **[!UICONTROL 儲存設定]**

      * 例如，產生的位置為： [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >預設儲存設定現在儲存在conf path(`/conf/global/settings/community/srpc/defaultconfiguration`)而非etc路徑(`/etc/socialconfig/srpc/defaultconfiguration`)。 建議您遵循 [移轉步驟](#zerodt-migration-steps) 讓defaultsrp如預期運作。
   ![dsrp-config](assets/dsrp-config.png)

* 選取 **[!UICONTROL 資料庫儲存體資源提供者(DSRP)]**
* **数据库配置**

   * **[!UICONTROL JDBC 数据源名称]**

      指定給MySQL連線的名稱必須與輸入名稱相同 [JDBC OSGi設定](dsrp-mysql.md#configurejdbcconnections)

      *預設*：社群

   * **[!UICONTROL 数据库名称]**

      為中的結構描述提供的名稱 [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) 指令碼

      *預設*：社群

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 主机**

      如果使用內部ZooKeeper執行Solr，請將此值留空。 否則，在中執行時 [SolrCloud模式](solr.md#solrcloud-mode) 使用外部ZooKeeper，將此值設定為ZooKeeper的URI，例如 *my.server.com:80*

      *預設*： *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *預設*： https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 收藏集]**

      *預設*：collection1

* 選取 **[!UICONTROL 提交]**.

### Defaultsrp的零停機移轉步驟 {#zerodt-migration-steps}

請依照下列步驟，確認defaultsrp頁面 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) 如預期運作：

1. 將路徑重新命名為 `/etc/socialconfig` 至 `/etc/socialconfig_old`，以便系統設定回覆為jsrp （預設）。
1. 移至defaultsrp頁面 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)，其中已設定jsrp。 按一下 **[!UICONTROL 提交]** 按鈕，以便在以下位置建立新的預設設定節點 `/conf/global/settings/community/srpc`.
1. 刪除建立的預設設定 `/conf/global/settings/community/srpc/defaultconfiguration`.
1. 複製舊設定 `/etc/socialconfig_old/srpc/defaultconfiguration` 取代已刪除的節點(`/conf/global/settings/community/srpc/defaultconfiguration`)。
1. 刪除舊的etc節點 `/etc/socialconfig_old`.

## 發佈設定 {#publishing-the-configuration}

DSRP必須識別為所有製作和發佈執行個體上的通用存放區。

若要讓發佈環境中可使用相同的設定：

* 在作者上：

   * 從主要功能表瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 復寫]**
   * 按兩下 **[!UICONTROL 啟動樹狀結構]**
   * **开始路径**:

      * 瀏覽至 `/etc/socialconfig/srpc/`
   * 確定 `Only Modified` 未選取。
   * 選取 **[!UICONTROL 啟動]**.


## 管理使用者資料 {#managing-user-data}

有關以下專案的資訊： *使用者*， *使用者設定檔* 和 *使用者群組*，通常輸入發佈環境中，請造訪：

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

## 為DSRP重新索引Solr {#reindexing-solr-for-dsrp}

若要重新索引DSRP Solr，請遵循以下檔案： [重新索引MSRP](msrp.md#msrp-reindex-tool)，但重新索引DSRP時，請改用此URL： **/services/social/datastore/rdb/reindex**

例如，重新索引DSRP的curl命令如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
