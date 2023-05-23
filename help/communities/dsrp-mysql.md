---
title: DSRP的MySQL組態
seo-title: MySQL Configuration for DSRP
description: 如何連線至MySQL伺服器並建立UGC資料庫
seo-description: How to connect to the MySQL server and establish the UGC database
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# DSRP的MySQL組態 {#mysql-configuration-for-dsrp}

MySQL是關聯式資料庫，可用來儲存使用者產生的內容(UGC)。

這些指示說明如何連線至MySQL伺服器及建立UGC資料庫。

## 要求 {#requirements}

* [最新Communities Feature Pack](deploy-communities.md#latestfeaturepack)
* [MySQL的JDBC驅動程式](deploy-communities.md#jdbc-driver-for-mysql)
* 關聯式資料庫：

   * [MySQL伺服器](https://dev.mysql.com/downloads/mysql/) Community Server 5.6版或更新版本

      * 可在與AEM相同的主機上執行或遠端執行
   * [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)


## 安裝MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) 應該依照目標作業系統的指示下載和安裝。

### 小寫表格名稱 {#lower-case-table-names}

由於SQL不區分大小寫，因此對於區分大小寫的作業系統，必須包含設定以小寫顯示所有資料表名稱。

例如，若要指定Linux作業系統上的所有小寫表格名稱：

* 編輯檔案 `/etc/my.cnf`
* 在 `[mysqld]` 區段，新增下列行：

   `lower_case_table_names = 1`

### UTF8字元集 {#utf-character-set}

若要提供更優異的多語言支援，必須使用UTF8字元集。

變更MySQL以以UTF8作為其字元集：

* mysql >設定名稱&#39;utf8&#39;；

將MySQL資料庫變更為預設的UTF8：

* 編輯檔案 `/etc/my.cnf`
* 在 `[client]` 區段，新增下列行：

   `default-character-set=utf8`

* 在 `[mysqld]` 區段，新增下列行：

   `character-set-server=utf8`

## 安裝MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供UI來執行安裝結構描述和初始資料的SQL指令碼。

MySQL Workbench應按照目標作業系統的指示下載及安裝。

## 社群連線 {#communities-connection}

MySQL Workbench首次啟動時，除非已用於其他用途，否則將不會顯示任何連線：

![mysqlconnection](assets/mysqlconnection.png)

### 新連線設定 {#new-connection-settings}

1. 選取 `+` 圖示右側 `MySQL Connections`.
1. 在對話方塊中 `Setup New Connection`，輸入適合您平台的值

   為了示範，將作者AEM執行個體和MySQL放在同一部伺服器上：

   * 連線名稱： `Communities`
   * 連線方法： `Standard (TCP/IP)`
   * 主機名稱： `127.0.0.1`
   * 用户名: `root`
   * 密码: `no password by default`
   * 預設結構描述： `leave blank`

1. 選取 `Test Connection` 驗證與執行中MySQL服務的連線

**注释**:

* 預設連線埠為 `3306`
* 所選擇的「連線名稱」會輸入為中的資料來源名稱 [JDBC OSGi設定](#configurejdbcconnections)

#### 新社群連線 {#new-communities-connection}

![community-connection](assets/community-connection.png)

## 資料庫設定 {#database-setup}

開啟Communities連線以安裝資料庫。

![install-data](assets/install-database.png)

### 取得SQL指令碼 {#obtain-the-sql-script}

SQL指令碼是從AEM存放庫取得：

1. 瀏覽至CRXDE Lite

   * 例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 選取/libs/social/config/datastore/dsrp/schema資料夾
1. 下载 `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

下載結構描述的一種方法是：

* 選取 `jcr:content` sql檔案的節點
* 請注意 `jcr:data` 屬性是一個檢視連結

* 選取檢視連結以將資料儲存至本機檔案

### 建立DSRP資料庫 {#create-the-dsrp-database}

請依照下列步驟安裝資料庫。 資料庫的預設名稱為 `communities`.

如果指令碼中的資料庫名稱已變更，請務必在 [JDBC設定](#configurejdbcconnections).

#### 步驟1：開啟SQL檔案 {#step-open-sql-file}

在MySQL Workbench

* 從「檔案」下拉式選單中，選取 **[!UICONTROL 開啟SQL指令碼]** option
* 選取下載的 `init_schema.sql` 指令碼

![select-sql-script](assets/select-sql-script.png)

#### 步驟2：執行SQL指令碼 {#step-execute-sql-script}

在「工作台」視窗中，針對在步驟1中開啟的檔案，選取 `lightening (flash) icon` 以執行指令碼。

在下圖中， `init_schema.sql` 檔案已準備好執行：

![execute-sql-script](assets/execute-sql-script.png)

#### 刷新 {#refresh}

執行指令碼後，必須重新整理 `SCHEMAS` 部分 `Navigator` 以便檢視新資料庫。 使用「結構描述」右側的重新整理圖示：

![refresh-schema](assets/refresh-schema.png)

## 設定JDBC連線 {#configure-jdbc-connection}

的OSGi設定 **Day Commons JDBC連線集區** 設定MySQL JDBC驅動程式。

所有發佈和編寫AEM執行個體都應指向相同的MySQL伺服器。

當MySQL在與AEM不同的伺服器上執行時，必須指定伺服器主機名稱來取代JDBC聯結器中的&#39;localhost&#39;。

* 在每個Author和Publish AEM例項上。
* 以管理員許可權登入。
* 存取 [網頁主控台](../../help/sites-deploying/configuring-osgi.md).

   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* 找到 `Day Commons JDBC Connections Pool`
* 選取 `+` 圖示來建立新的連線設定。

   ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* 輸入下列值：

   * **[!UICONTROL JDBC驅動程式類別]**： `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC連線URI]**： `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      如果MySQL伺服器與&#39;this&#39; AEM伺服器不同，請指定伺服器來取代localhost *社群* 是預設資料庫（綱要）名稱。

   * **[!UICONTROL 使用者名稱]**： `root`

      或者，如果不是&#39;root&#39;，請輸入MySQL伺服器的設定使用者名稱。

   * **[!UICONTROL 密码]**:

      如果沒有為MySQL設定密碼，請清除此欄位，

      否則請輸入MySQL使用者名稱的設定密碼。

   * **[!UICONTROL 資料來源名稱]**：為輸入的名稱 [MySQL連線](#new-connection-settings)例如，「communities」。

* 選取 **[!UICONTROL 儲存]**
