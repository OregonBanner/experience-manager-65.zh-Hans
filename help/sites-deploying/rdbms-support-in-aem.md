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
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# AEM 6.4{#rdbms-support-in-aem}中的RDBMS支持

## 概述 {#overview}

使用文档Microkernel实现了对AEM中关系数据库持久性的支持。 文档微内核是实现MongoDB持久性的基础。

它包含一个基于Mongo Java API的Java API。 还提供了BlobStore API的实现。 默认情况下，blob存储在数据库中。

有关实现详细信息，请参阅[RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html)和[RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html)文档。

>[!NOTE]
>
>还提供对&#x200B;**PostgreSQL 9.4**&#x200B;的支持，但仅用于演示目的。 它不适用于生产环境。

## 支持的数据库{#supported-databases}

有关AEM中关系数据库支持级别的详细信息，请参见[技术要求页](/help/sites-deploying/technical-requirements.md)。

## 配置步骤{#configuration-steps}

通过配置`DocumentNodeStoreService` OSGi服务创建存储库。 除了MongoDB，它还扩展了它以支持关系数据库持久性。

要使数据源正常工作，需要使用AEM配置数据源。 这通过`org.apache.sling.datasource.DataSourceFactory.config`文件完成。 相应数据库的JDBC驱动程序需要作为OSGi绑定在本地配置中单独提供。

有关为JDBC驱动程序创建OSGi捆绑包的步骤，请参阅Apache Sling网站上的此[文档](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)。

捆绑包到位后，请按照以下步骤配置AEM和RDB持久性：

1. 确保数据库守护程序已启动，并且您有一个活动数据库可与AEM一起使用。
1. 将AEM 6.3 jar复制到安装目录中。
1. 在安装目录中创建名为`crx-quickstart\install`的文件夹。
1. 通过在`crx-quickstart\install`目录中创建具有以下名称的配置文件，配置文档节点存储：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 通过在`crx-quickstart\install`文件夹中创建另一个具有以下名称的配置文件，配置数据源和JDBC参数：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >有关每个受支持数据库的数据源配置的详细信息，请参见[数据源配置选项](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)。

1. 接下来，准备要与AEM一起使用的JDBC OSGi包：

   1. 在`crx-quickstart/install`文件夹中，创建一个名为`9`的文件夹。

   1. 将JDBC jar放在新文件夹中。

1. 最后，开始AEM并使用`crx3`和`crx3rdb`运行模式：

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 数据源配置选项{#data-source-configuration-options}

`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi配置用于配置AEM与数据库持久性层之间通信所需的参数。

提供以下配置选项：

* `datasource.name:` 数据源名称。默认为 `oak`.

* `url:` 需要与JDBC一起使用的数据库的URL字符串。每个数据库类型都有其自己的URL字符串格式。 有关详细信息，请参阅下面的[URL字符串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)。

* `driverClassName:` JDBC驱动程序类名。这会因您要使用的数据库以及随后连接到数据库所需的驱动程序而异。 以下是AEM支持的所有数据库的类名：

   * `org.postgresql.Driver` PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` oracle;
   * `com.mysql.jdbc.Driver` 用于MySQL和MariaDB（实验）;
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server（实验）。

* `username:` 数据库运行的用户名。

* `password:` 数据库密码。

### URL字符串格式{#url-string-formats}

数据源配置中使用不同的URL字符串格式，具体取决于需要使用的数据库类型。 下面是AEM当前支持的列表库的格式：

* `jdbc:postgresql:databasename` PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` oracle;
* `jdbc:mysql://localhost:3306/databasename` 用于MySQL和MariaDB（实验）;
* `jdbc:sqlserver://localhost:1453;databaseName=name` （实验）。

## 已知限制{#known-limitations}

RDBMS持久性支持将多个AEM实例与单个数据库同时使用，但并发安装则不支持。

要解决此问题，请确保先使用单个成员运行安装，并在第一个成员完成安装后添加其他成员。

