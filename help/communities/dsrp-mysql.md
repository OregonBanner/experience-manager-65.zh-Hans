---
title: 用于DSRP的MySQL配置
seo-title: MySQL Configuration for DSRP
description: 如何连接到MySQL服务器并建立UGC数据库
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

# 用于DSRP的MySQL配置 {#mysql-configuration-for-dsrp}

MySQL是用于存储用户生成内容(UGC)的关系数据库。

这些说明描述了如何连接到MySQL服务器和建立UGC数据库。

## 要求 {#requirements}

* [最新的Communities功能包](deploy-communities.md#latestfeaturepack)
* [适用于MySQL的JDBC驱动程序](deploy-communities.md#jdbc-driver-for-mysql)
* 关系数据库：

   * [MySQL服务器](https://dev.mysql.com/downloads/mysql/) Community Server版本5.6或更高版本

      * 可以在与AEM相同的主机上运行或远程运行
   * [MySQL工作台](https://dev.mysql.com/downloads/tools/workbench/)


## 安装MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) 应按照针对目标操作系统的说明下载并安装。

### 小写表名称 {#lower-case-table-names}

由于SQL不区分大小写，因此对于区分大小写的操作系统，必须包含设置为所有表名都使用小写。

例如，要在Linux操作系统上指定所有小写表名，请执行以下操作：

* 编辑文件 `/etc/my.cnf`
* 在 `[mysqld]` 部分，添加以下行：

   `lower_case_table_names = 1`

### UTF8字符集 {#utf-character-set}

要提供更好的多语言支持，必须使用UTF8字符集。

将MySQL更改为将UTF8作为其字符集：

* mysql >设置名称&#39;utf8&#39;；

将MySQL数据库更改为默认的UTF8：

* 编辑文件 `/etc/my.cnf`
* 在 `[client]` 部分，添加以下行：

   `default-character-set=utf8`

* 在 `[mysqld]` 部分，添加以下行：

   `character-set-server=utf8`

## 安装MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供了一个用于执行安装架构和初始数据的SQL脚本的UI。

应按照针对目标操作系统的说明下载和安装MySQL Workbench。

## Communities连接 {#communities-connection}

首次启动MySQL Workbench时，除非已将其用于其他目的，否则它尚未显示任何连接：

![mysqlconnection](assets/mysqlconnection.png)

### 新连接设置 {#new-connection-settings}

1. 选择 `+` 图标右侧 `MySQL Connections`.
1. 在对话框中 `Setup New Connection`，输入适用于您的平台的值

   出于演示目的，将创作AEM实例和MySQL放在同一服务器上：

   * 连接名称： `Communities`
   * 连接方法： `Standard (TCP/IP)`
   * 主机名： `127.0.0.1`
   * 用户名: `root`
   * 密码: `no password by default`
   * 默认架构： `leave blank`

1. 选择 `Test Connection` 验证与正在运行的MySQL服务的连接

**注释**:

* 默认端口为 `3306`
* 在中，将选定的连接名称作为数据源名称输入 [JDBC OSGi配置](#configurejdbcconnections)

#### 新建社区连接 {#new-communities-connection}

![社区连接](assets/community-connection.png)

## 数据库设置 {#database-setup}

打开Communities连接以安装数据库。

![install-database](assets/install-database.png)

### 获取SQL脚本 {#obtain-the-sql-script}

SQL脚本从AEM存储库获取：

1. 浏览到CRXDE Lite

   * 例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 选择/libs/social/config/datastore/dsrp/schema文件夹
1. 下载 `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

下载架构的一种方法是：

* 选择 `jcr:content` sql文件的节点
* 请注意的值 `jcr:data` 属性是一个视图链接

* 选择查看链接以将数据保存到本地文件

### 创建DSRP数据库 {#create-the-dsrp-database}

按照以下步骤安装数据库。 数据库的默认名称为 `communities`.

如果更改了脚本中的数据库名称，请务必也在 [JDBC配置](#configurejdbcconnections).

#### 步骤1：打开SQL文件 {#step-open-sql-file}

在MySQL工作台中

* 从“文件”下拉菜单中，选择 **[!UICONTROL 打开SQL脚本]** option
* 选择下载的 `init_schema.sql` 脚本

![select-sql-script](assets/select-sql-script.png)

#### 步骤2：执行SQL脚本 {#step-execute-sql-script}

在Workbench窗口中，为在Step 1中打开的文件选择 `lightening (flash) icon` 执行脚本。

在下图中， `init_schema.sql` 文件已准备好执行：

![execute-sql-script](assets/execute-sql-script.png)

#### 刷新 {#refresh}

执行脚本后，必须刷新 `SCHEMAS` 部分 `Navigator` 以便查看新数据库。 使用“架构”右侧的刷新图标：

![refresh-schema](assets/refresh-schema.png)

## 配置JDBC连接 {#configure-jdbc-connection}

的OSGi配置 **Day Commons JDBC连接池** 配置MySQL JDBC驱动程序。

所有发布和创作AEM实例都应指向同一个MySQL服务器。

当MySQL在与AEM不同的服务器上运行时，必须指定服务器主机名来代替JDBC连接器中的“localhost”。

* 在每个创作和发布AEM实例上。
* 已使用管理员权限登录。
* 访问 [Web控制台](../../help/sites-deploying/configuring-osgi.md).

   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* 找到 `Day Commons JDBC Connections Pool`
* 选择 `+` 图标来创建新的连接配置。

   ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* 输入以下值：

   * **[!UICONTROL JDBC驱动程序类]**： `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC连接URI]**： `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      如果MySQL服务器与“此”AEM服务器不同，请指定服务器来代替localhost *社区* 是默认数据库（架构）名称。

   * **[!UICONTROL 用户名]**： `root`

      或者输入为MySQL服务器配置的用户名（如果不是“root”）。

   * **[!UICONTROL 密码]**:

      如果没有为MySQL设置密码，则清除此字段，

      否则，请为MySQL用户名输入配置的密码。

   * **[!UICONTROL 数据源名称]**：为输入的名称 [MySQL连接](#new-connection-settings)例如，“communities”。

* 选择 **[!UICONTROL 保存]**
