---
title: DSRP的MySQL配置
seo-title: DSRP的MySQL配置
description: 如何连接到MySQL服务器并建立UGC数据库
seo-description: 如何连接到MySQL服务器并建立UGC数据库
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Administrator
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# DSRP {#mysql-configuration-for-dsrp}的MySQL配置

MySQL是一个关系数据库，可用于存储用户生成的内容(UGC)。

这些说明说明如何连接到MySQL Server并建立UGC数据库。

## 要求 {#requirements}

* [最新社区功能包](deploy-communities.md#latestfeaturepack)
* [MySQL的JDBC驱动程序](deploy-communities.md#jdbc-driver-for-mysql)
* 关系数据库：

   * [MySQL ](https://dev.mysql.com/downloads/mysql/) serverCommunity Server版本5.6或更高版本

      * 可以在与AEM相同的主机上运行或远程运行
   * [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)


## 安装MySQL {#installing-mysql}

[](https://dev.mysql.com/downloads/mysql/) 应按照目标操作系统的说明下载和安装MySQL。

### 小写表名称{#lower-case-table-names}

由于SQL不区分大小写，因此对于区分大小写的操作系统，必须包含一个设置，以使所有表名称都小写。

例如，要在Linux操作系统中指定所有小写表名：

* 编辑文件`/etc/my.cnf`
* 在`[mysqld]`部分中，添加以下行：

   `lower_case_table_names = 1`

### UTF8字符集{#utf-character-set}

要提供更好的多语言支持，必须使用UTF8字符集。

将MySQL更改为将UTF8作为其字符集：

* mysql > SET NAMES &#39;utf8&#39;;

将MySQL数据库更改为默认UTF8:

* 编辑文件`/etc/my.cnf`
* 在`[client]`部分中，添加以下行：

   `default-character-set=utf8`

* 在`[mysqld]`部分中，添加以下行：

   `character-set-server=utf8`

## 安装MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供了用于执行SQL脚本的UI，这些脚本安装了架构和初始数据。

应按照目标操作系统的说明下载和安装MySQL Workbench。

## 社区连接{#communities-connection}

首次启动MySQL Workbench时，除非该MySQL Workbench已用于其他目的，否则它尚不显示任何连接：

![mysqlconnection](assets/mysqlconnection.png)

### 新的连接设置{#new-connection-settings}

1. 选择`MySQL Connections`右侧的`+`图标。
1. 在对话框`Setup New Connection`中，输入适合您平台的值

   出于演示目的，将创作AEM实例和MySQL放在同一服务器上：

   * 连接名称：`Communities`
   * 连接方法：`Standard (TCP/IP)`
   * 主机名：`127.0.0.1`
   * 用户名: `root`
   * 密码: `no password by default`
   * 默认架构：`leave blank`

1. 选择`Test Connection`以验证与正在运行的MySQL服务的连接

**注释**:

* 默认端口为`3306`
* 选择的连接名称将作为数据源名称输入到[JDBC OSGi配置](#configurejdbcconnections)中

#### 新建社区连接{#new-communities-connection}

![社区连接](assets/community-connection.png)

## 数据库设置{#database-setup}

打开Communities连接以安装数据库。

![install-database](assets/install-database.png)

### 获取SQL脚本{#obtain-the-sql-script}

SQL脚本从AEM存储库获取：

1. 浏览到CRXDE Lite

   * 例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 选择/libs/social/config/datastore/dsrp/schema文件夹
1. 下载 `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

下载模式的一种方法是：

* 为sql文件选择`jcr:content`节点
* 请注意`jcr:data`属性的值是一个视图链接

* 选择视图链接以将数据保存到本地文件

### 创建DSRP数据库{#create-the-dsrp-database}

按照以下步骤安装数据库。 数据库的默认名称为`communities`。

如果在脚本中更改了数据库名称，请务必在[JDBC配置](#configurejdbcconnections)中更改数据库名称。

#### 步骤1:打开SQL文件{#step-open-sql-file}

在MySQL Workbench中

* 从“文件”下拉菜单中，选择&#x200B;**[!UICONTROL 打开SQL脚本]**&#x200B;选项
* 选择下载的`init_schema.sql`脚本

![select-sql-script](assets/select-sql-script.png)

#### 步骤2:执行SQL脚本{#step-execute-sql-script}

在步骤1中打开的文件的Workbench窗口中，选择`lightening (flash) icon`以执行脚本。

在下图中，`init_schema.sql`文件已准备就绪，可供执行：

![execute-sql-script](assets/execute-sql-script.png)

#### 刷新 {#refresh}

执行脚本后，需要刷新`Navigator`的`SCHEMAS`部分，才能查看新数据库。 使用“架构”右侧的刷新图标：

![刷新模式](assets/refresh-schema.png)

## 配置JDBC连接{#configure-jdbc-connection}

**Day Commons JDBC连接池**&#x200B;的OSGi配置配置MySQL JDBC驱动程序。

所有发布和创作AEM实例都应指向同一MySQL服务器。

当MySQL在与AEM不同的服务器上运行时，必须在JDBC连接器中指定服务器主机名代替“localhost”。

* 在每个创作和发布AEM实例上。
* 已使用管理员权限登录。
* 访问[Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* 找到`Day Commons JDBC Connections Pool`
* 选择`+`图标以创建新的连接配置。

   ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* 输入以下值：

   * **[!UICONTROL JDBC驱动程序类]**:  `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC连接URI]**:  `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      如果MySQL Server与&#39;this&#39; AEM Server *communities*&#x200B;是默认数据库（架构）名称，请指定服务器代替localhost。

   * **[!UICONTROL 用户名]**:  `root`

      或者输入MySQL Server的配置用户名（如果不是“root”）。

   * **[!UICONTROL 密码]**:

      如果未为MySQL设置密码，请清除此字段，

      否则，输入为MySQL用户名配置的密码。

   * **[!UICONTROL 数据源名称]**:为MySQL连 [接](#new-connection-settings)输入的名称，例如“communities”。

* 选择&#x200B;**[!UICONTROL Save]**
