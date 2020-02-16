---
title: AEM 6.4中的RDBMS支持
seo-title: AEM 6.4中的RDBMS支持
description: 了解AEM 6.4中的关系数据库持久性支持以及可用的配置选项。
seo-description: 了解AEM 6.4中的关系数据库持久性支持以及可用的配置选项。
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e

---


# AEM 6.4中的RDBMS支持{#rdbms-support-in-aem}

## 概述 {#overview}

使用Document Microkernel实现了对AEM中关系数据库持久性的支持。 文档微内核是实现MongoDB持久性的基础。

它由一个基于Mongo Java API的Java API组成。 还提供了BlobStore API的实现。 默认情况下，blob存储在数据库中。

有关实施详细信息，请参阅 [RDBDocumentStore和](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) RDBBlobStore [](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) 文档。

>[!NOTE]
>
>还提 **供对PostgreSQL 9.4的支持** ，但仅用于演示目的。 它不适用于生产环境。

## 支持的数据库 {#supported-databases}

有关AEM中关系型数据库支持级别的详细信息，请参阅技 [术要求页](/help/sites-deploying/technical-requirements.md)。

## 配置步骤 {#configuration-steps}

通过配置OSGi服务创建存 `DocumentNodeStoreService` 储库。 除MongoDB外，它还经过扩展以支持关系数据库持久性。

为使其正常工作，需要使用AEM配置数据源。 这通过文件完 `org.apache.sling.datasource.DataSourceFactory.config` 成。 相应数据库的JDBC驱动程序需要作为本地配置中的OSGi包单独提供。

有关创建用于JDBC驱动程序的OSGi捆绑包的步骤，请参阅 [Apache Sling网站](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) 上的此文档。

捆绑包到位后，请按照以下步骤配置AEM的RDB持久性：

1. 确保数据库守护程序已启动，并且您有一个活动的数据库供AEM使用。
1. 将AEM 6.3jar复制到安装目录中。
1. 在安装目录中 `crx-quickstart\install` 创建一个名为的文件夹。
1. 通过在目录中创建具有以下名称的配置文件，配置文档节点存 `crx-quickstart\install` 储区：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 通过在文件夹中创建另一个具有以下名称的配置文件，配置数据源和JDBC `crx-quickstart\install` 参数：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >有关每个支持的数据库的数据源配置的详细信息，请参阅 [数据源配置选项](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)。

1. 接下来，准备要与AEM一起使用的JDBC OSGi包：

   1. 在该文 `crx-quickstart/install` 件夹中，创建一个名为的文件夹 `9`。

   1. 将JDBCjar放在新文件夹中。

1. 最后，使用和运行模式 `crx3` 启动 `crx3rdb` AEM:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 数据源配置选项 {#data-source-configuration-options}

OSGi配 `org.apache.sling.datasource.DataSourceFactory-oak.config` 置用于配置AEM与数据库持久层之间通信所需的参数。

以下配置选项可用：

* `datasource.name:` 数据源名称。 默认为 `oak`.

* `url:` 需要与JDBC一起使用的数据库的URL字符串。 每个数据库类型都有其自己的URL字符串格式。 有关详细信息，请参 [阅下面的URL字符串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) 。

* `driverClassName:` JDBC驱动程序类名。 这会因您要使用的数据库而异，随后会因连接到数据库所需的驱动程序而异。 以下是AEM支持的所有数据库的类名：

   * `org.postgresql.Driver` for PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` 对于Oracle;
   * `com.mysql.jdbc.Driver` 用于MySQL和MariaDB（实验性）;
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server（实验性）。

* `username:` 数据库运行的用户名。

* `password:` 数据库口令。

### URL字符串格式 {#url-string-formats}

数据源配置中使用不同的URL字符串格式，具体取决于需要使用的数据库类型。 以下是AEM当前支持的数据库的格式列表：

* `jdbc:postgresql:databasename` for PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` 对于Oracle;
* `jdbc:mysql://localhost:3306/databasename` 用于MySQL和MariaDB（实验性）;
* `jdbc:sqlserver://localhost:1453;databaseName=name` for Microsoft SQL Server（实验）。

## 已知限制 {#known-limitations}

虽然RDBMS持久性支持将多个AEM实例与单个数据库一起并发使用，但并发安装不支持。

要解决此问题，请确保先使用单个成员运行安装，然后在完成安装后添加其他成员。

