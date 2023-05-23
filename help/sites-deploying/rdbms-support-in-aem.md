---
title: AEM 6.4中的RDBMS支援
seo-title: RDBMS Support in AEM 6.4
description: 瞭解AEM 6.4中的關聯式資料庫持續性支援，以及可用的設定選項。
seo-description: Learn about the relational database persistence support in AEM 6.4 and the available configuration options.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: Configuring
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# AEM 6.4中的RDBMS支援{#rdbms-support-in-aem}

## 概述 {#overview}

使用Document Microkernel在AEM中支援關聯式資料庫持續性。 Document Microkernel是實施MongoDB持續性的基礎。

它包含以Mongo Java API為基礎的Java API。 也提供BlobStore API的實作。 根據預設，Blob會儲存在資料庫中。

如需實作詳細資訊的詳細資訊，請參閱 [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) 和 [Rdblobstore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) 說明檔案。

>[!NOTE]
>
>支援 **PostgreSQL 9.4** 也提供，但僅供示範用途。 它將不適用於生產環境。

## 支援的資料庫 {#supported-databases}

如需AEM中關聯式資料庫支援層級的詳細資訊，請參閱 [技術需求頁面](/help/sites-deploying/technical-requirements.md).

## 設定步驟 {#configuration-steps}

存放庫是透過設定 `DocumentNodeStoreService` OSGi服務。 除了MongoDB之外，還延伸支援關聯式資料庫持續性。

資料來源必須設定為AEM，才能正常運作。 這是透過 `org.apache.sling.datasource.DataSourceFactory.config` 檔案。 個別資料庫的JDBC驅動程式需要在本機設定中作為OSGi套件組合單獨提供。

如需建立JDBC驅動程式OSGi套件組合的相關步驟，請參閱此 [檔案](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) Apache Sling網站上的資訊。

套件組合準備就緒後，請依照下列步驟操作，以使用RDB持續性設定AEM：

1. 請確定資料庫協助程式已啟動，而且您有可與AEM搭配使用的作用中資料庫。
1. 將AEM 6.3 jar複製到安裝目錄中。
1. 建立名為的資料夾 `crx-quickstart\install` 安裝目錄中的。
1. 透過在中建立具有以下名稱的設定檔案來設定檔案節點存放區 `crx-quickstart\install` 目錄：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 藉由在「 」中建立另一個名稱如下的組態檔來設定資料來源和JDBC引數 `crx-quickstart\install` 資料夾：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >如需每個支援之資料庫的資料來源組態詳細資訊，請參閱 [資料來源組態選項](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. 接下來，準備要與AEM搭配使用的JDBC OSGi套件組合：

   1. 在 `crx-quickstart/install` 資料夾，建立名為的資料夾 `9`.

   1. 將JDBC jar放在新資料夾中。

1. 最後，從AEM開始 `crx3` 和 `crx3rdb` 執行模式：

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 資料來源組態選項 {#data-source-configuration-options}

此 `org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi設定用於設定AEM和資料庫持續層之間通訊所需的引數。

下列組態選項可供使用：

* `datasource.name:` 資料來源名稱。 默认为 `oak`。

* `url:` 需要與JDBC搭配使用的資料庫URL字串。 每種資料庫型別都有自己的URL字串格式。 如需詳細資訊，請參閱 [URL字串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) 下方的。

* `driverClassName:` JDBC驅動程式類別名稱。 根據您要使用的資料庫，以及隨後連線至資料庫所需的驅動程式，這會有所不同。 以下是AEM支援之所有資料庫的類別名稱：

   * `org.postgresql.Driver` 適用於PostgreSQL；
   * `com.ibm.db2.jcc.DB2Driver` 適用於DB2；
   * `oracle.jdbc.OracleDriver` 用於Oracle；
   * `com.mysql.jdbc.Driver` 適用於MySQL和MariaDB （實驗性）；
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` 適用於Microsoft SQL Server （實驗性）。

* `username:` 執行資料庫的使用者名稱。

* `password:` 資料庫密碼。

### URL字串格式 {#url-string-formats}

在資料來源設定中使用不同的URL字串格式，視需要使用的資料庫型別而定。 以下是AEM目前支援之資料庫的格式清單：

* `jdbc:postgresql:databasename` 適用於PostgreSQL；
* `jdbc:db2://localhost:port/databasename` 適用於DB2；
* `jdbc:oracle:thin:localhost:port:SID` 用於Oracle；
* `jdbc:mysql://localhost:3306/databasename` 適用於MySQL和MariaDB （實驗性）；
* `jdbc:sqlserver://localhost:1453;databaseName=name` 適用於Microsoft SQL Server （實驗性）。

## 已知限制 {#known-limitations}

雖然RDBMS持續性支援同時使用具有單一資料庫的多個AEM執行個體，但並不支援同時安裝。

為了解決這個問題，請務必先使用單一成員執行安裝，並在第一個成員完成安裝後新增其他成員。
