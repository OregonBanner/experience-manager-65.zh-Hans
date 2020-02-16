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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DSRP的MySQL配置 {#mysql-configuration-for-dsrp}

MySQL是一个关系数据库，可用于存储用户生成的内容(UGC)。

这些说明描述了如何连接到MySQL服务器并建立UGC数据库。

## 要求 {#requirements}

* [最新社区功能包](deploy-communities.md#latestfeaturepack)
* [MySQL的JDBC驱动程序](deploy-communities.md#jdbc-driver-for-mysql)
* 关系数据库：

   * [MySQL Server](https://dev.mysql.com/downloads/mysql/) Community server版本5.6或更高版本

      * 可以与AEM在同一主机上运行或远程运行
   * [MySQL工作台](https://dev.mysql.com/downloads/tools/workbench/)


## 安装MySQL {#installing-mysql}

[应按照目标OS的说明下载并安装MySQL](https://dev.mysql.com/downloads/mysql/) 。

### 小写表名 {#lower-case-table-names}

由于SQL不区分大小写，因此对于区分大小写的操作系统，必须包含一个将所有表名都小写的设置。

例如，要指定Linux OS上的所有小写表名称：

* 编辑文件 `/etc/my.cnf`
* 在部 `[mysqld]` 分中，添加以下行：

   `lower_case_table_names = 1`

### UTF8字符集 {#utf-character-set}

要提供更好的多语言支持，必须使用UTF8字符集。

将MySQL更改为以UTF8作为字符集：

* mysql>设置名称“utf8”;

将MySQL数据库更改为默认的UTF8:

* 编辑文件 `/etc/my.cnf`
* 在部 `[client]` 分中，添加以下行：

   `default-character-set=utf8`

* 在部 `[mysqld]` 分中，添加以下行：

   `character-set-server=utf8`

## 安装MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供了用于执行SQL脚本的UI，这些脚本安装了架构和初始数据。

应按照目标操作系统的说明下载并安装MySQL Workbench。

## 社区连接 {#communities-connection}

首次启动MySQL Workbench时，除非已用于其他用途，否则它尚不显示任何连接：

![chlimage_1-104](assets/chlimage_1-104.png)

### 新连接设置 {#new-connection-settings}

1. 选择 `+` 右侧的图标 `MySQL Connections`。
1. 在对话框 `Setup New Connection`中，输入适合您的平台的值

   出于演示目的，将作者AEM实例和MySQL放在同一台服务器上：

   * 连接名称： `Communities`
   * 连接方法： `Standard (TCP/IP)`
   * Hostname: `127.0.0.1`
   * 用户名: `root`
   * 密码: `no password by default`
   * 默认架构： `leave blank`

1. 选 `Test Connection` 择以验证与正在运行的MySQL服务的连接

**注释**:

* 默认端口为 `3306`
* 在 [JDBC OSGi配置中，选择的连接名称作为数据源名称输入](#configurejdbcconnections)

#### 新社区连接 {#new-communities-connection}

![chlimage_1-105](assets/chlimage_1-105.png)

## 数据库设置 {#database-setup}

打开Communities连接以安装数据库。

![chlimage_1-106](assets/chlimage_1-106.png)

### 获取SQL脚本 {#obtain-the-sql-script}

SQL脚本从AEM存储库获取：

1. 浏览到CRXDE Lite

   * 例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. 选择/libs/social/config/datastore/dsrp/schema文件夹
1. 下载 `init-schema.sql`

![chlimage_1-107](assets/chlimage_1-107.png)

下载架构的一种方法是

* 为sql `jcr:content`文件选择节点
* 注意，该属性的 `jcr:data`值是一个视图链接

* 选择视图链接以将数据保存到本地文件

### 创建DSRP数据库 {#create-the-dsrp-database}

请按照以下步骤安装数据库。 数据库的默认名称为 `communities`。

如果脚本中的数据库名称已更改，请务必在 [JDBC配置中更改它](#configurejdbcconnections)。

#### 第1步：打开SQL文件 {#step-open-sql-file}

在MySQL Workbench中

* 从“文件”下拉菜单
* 选择下载的 `init_schema.sql`

![chlimage_1-108](assets/chlimage_1-108.png)

#### 第2步：执行SQL Script {#step-execute-sql-script}

在“工作台”窗口中，对于在步骤1中打开的文件，选择 `lightening (flash) icon` 要执行脚本的文件。

在以下图像中，文 `init_schema.sql` 件已准备好执行：

![chlimage_1-109](assets/chlimage_1-109.png)

#### 刷新 {#refresh}

执行脚本后，必须刷新该部分 `SCHEMAS`才能看 `Navigator` 到新数据库。 使用“架构”右侧的刷新图标：

![chlimage_1-110](assets/chlimage_1-110.png)

## 配置JDBC连接 {#configure-jdbc-connection}

Day Commons JDBC连接池 **的OSGi配置配置** MySQL JDBC驱动程序。

所有发布和作者AEM实例都应指向同一MySQL服务器。

当MySQL在与AEM不同的服务器上运行时，必须在JDBC连接器中指定服务器主机名以代替“localhost”。

* 在每个作者上和发布AEM实例
* 以管理员权限登录
* 访问Web [控制台](../../help/sites-deploying/configuring-osgi.md)

   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* 找到 `Day Commons JDBC Connections Pool`
* 选择图 `+` 标以创建新的连接配置

![chlimage_1-111](assets/chlimage_1-111.png)

* 输入以下值：

   * **[!UICONTROL JDBC驱动程序类]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC连接URI]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      如果MySQL服务器与“this”AEM服务器不同，则指定服务器代替localhost

      *communities* 是默认数据库（架构）名称

   * **[!UICONTROL 用户名]**: `root`

      或者，如果不是“root”，则输入MySQL服务器的已配置用户名

   * **[!UICONTROL 密码]**:

      如果MySQL未设置密码，请清除此字段，

      else输入MySQL用户名的配置口令
   * **[!UICONTROL 数据源名称]**:为 [MySQL连接输入的名称](#new-connection-settings)，例如“communities”

* Select **[!UICONTROL Save]**

