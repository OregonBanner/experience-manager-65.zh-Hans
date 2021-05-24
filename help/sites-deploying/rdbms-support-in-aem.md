---
title: AEM 6.4中的RDBMS支持
seo-title: AEM 6.4中的RDBMS支持
description: 了解AEM 6.4中的关系数据库持久性支持和可用的配置选项。
seo-description: 了解AEM 6.4中的关系数据库持久性支持和可用的配置选项。
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: 配置
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# AEM 6.4{#rdbms-support-in-aem}中的RDBMS支持

## 概述 {#overview}

使用文档微内核实现了对AEM中关系数据库持久性的支持。 文档微内核是用于实现MongoDB持久性的基础。

它包含一个基于Mongo Java API的Java API。 还提供了BlobStore API的实现。 默认情况下，Blob存储在数据库中。

有关实施详细信息的更多信息，请参阅[RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html)和[RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html)文档。

>[!NOTE]
>
>此外，还提供了对&#x200B;**PostgreSQL 9.4**&#x200B;的支持，但仅用于演示目的。 它将不适用于生产环境。

## 支持的数据库{#supported-databases}

有关AEM中关系数据库支持级别的详细信息，请参阅[技术要求页面](/help/sites-deploying/technical-requirements.md)。

## 配置步骤{#configuration-steps}

通过配置`DocumentNodeStoreService` OSGi服务创建存储库。 除MongoDB外，它还扩展了以支持关系数据库持久性。

要使其正常工作，需要使用AEM配置数据源。 这是通过`org.apache.sling.datasource.DataSourceFactory.config`文件完成的。 相应数据库的JDBC驱动程序需要作为OSGi包在本地配置中单独提供。

有关为JDBC驱动程序创建OSGi包的步骤，请参阅Apache Sling网站上的此[文档](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)。

包到位后，请按照以下步骤配置具有RDB持久性的AEM:

1. 确保数据库守护程序已启动，并且您有一个可与AEM一起使用的活动数据库。
1. 将AEM 6.3 jar复制到安装目录中。
1. 在安装目录中创建名为`crx-quickstart\install`的文件夹。
1. 通过在`crx-quickstart\install`目录中创建具有以下名称的配置文件来配置文档节点存储：

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. 通过在`crx-quickstart\install`文件夹中创建另一个具有以下名称的配置文件，配置数据源和JDBC参数：

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >有关每个受支持数据库的数据源配置的详细信息，请参阅[数据源配置选项](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)。

1. 接下来，准备要与AEM一起使用的JDBC OSGi包：

   1. 在`crx-quickstart/install`文件夹中，创建一个名为`9`的文件夹。

   1. 将JDBC jar放在新文件夹中。

1. 最后，以`crx3`和`crx3rdb`运行模式启动AEM:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## 数据源配置选项{#data-source-configuration-options}

`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi配置用于配置AEM与数据库持久层之间通信所需的参数。

以下配置选项可用：

* `datasource.name:` 数据源名称。默认为 `oak`.

* `url:` 需要与JDBC一起使用的数据库的URL字符串。每种数据库类型都有其自己的URL字符串格式。 有关更多信息，请参阅下面的[URL字符串格式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)。

* `driverClassName:` JDBC驱动程序类名。这将因您要使用的数据库而异，随后取决于连接到该数据库所需的驱动程序。 以下是AEM支持的所有数据库的类名称：

   * `org.postgresql.Driver` （对于PostgreSQL）；
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` oracle;
   * `com.mysql.jdbc.Driver` （用于MySQL和MariaDB）；
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server（实验）。

* `username:` 数据库运行的用户名。

* `password:` 数据库密码。

### URL字符串格式{#url-string-formats}

数据源配置中使用的URL字符串格式不同，具体取决于需要使用的数据库类型。 以下是AEM当前支持的数据库格式列表：

* `jdbc:postgresql:databasename` （对于PostgreSQL）；
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` oracle;
* `jdbc:mysql://localhost:3306/databasename` （用于MySQL和MariaDB）；
* `jdbc:sqlserver://localhost:1453;databaseName=name` （实验）。

## 已知限制{#known-limitations}

虽然RDBMS持久性支持将多个AEM实例与单个数据库并发使用，但不支持并发安装。

为了解决此问题，请确保先使用单个成员运行安装，然后在完成安装后添加其他成员。
