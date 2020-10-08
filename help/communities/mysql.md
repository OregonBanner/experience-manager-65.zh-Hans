---
title: MySQL Configuration for Enablement Features
seo-title: MySQL Configuration for Enablement Features
description: 连接MySQL服务器
seo-description: 连接MySQL服务器
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 3%

---


# MySQL Configuration for Enablement Features {#mysql-configuration-for-enablement-features}

MySQL是关系报告库，主要用于SCORM跟踪和启用资源的数据。 其中包括跟踪视频暂停／恢复等其他功能的表。

这些说明描述了如何连接到MySQL服务器、建立启用数据库以及使用初始数据填充数据库。

## 要求 {#requirements}

在配置MySQL for Communities的启用功能之前，请确保

* 安 [装MySQL](https://dev.mysql.com/downloads/mysql/) Server Community Server 5.6版：
   * SCORM不支持版本5.7。
   * 服务器可能与作者AEM实例相同。
* 在所有AEM实例上，安装MySQL的 [正式JDBC驱动程序](deploy-communities.md#jdbc-driver-for-mysql)。
* 安 [装MySQL工作台](https://dev.mysql.com/downloads/tools/workbench/)。
* 在所有AEM实例上，安 [装SCORM包](enablement.md#scorm)。

## 安装MySQL {#installing-mysql}

应按照目标操作系统的说明下载并安装MySQL。

### 小写表名 {#lower-case-table-names}

由于SQL不区分大小写，因此对于区分大小写的操作系统，必须包含一个将所有表名都小写的设置。

例如，要指定Linux OS上的所有小写表名称：

* 编辑文件 `/etc/my.cnf`
* 在部 `[mysqld]` 分中，添加以下行： `lower_case_table_names = 1`

### UTF8字符集 {#utf-character-set}

要提供更好的多语言支持，必须使用UTF8字符集。

将MySQL更改为以UTF8作为其字符集：
* mysql >设置名称“utf8”;

将MySQL数据库更改为默认的UTF8:
* 编辑文件 `/etc/my.cnf`
* 在部分 `[client]` 中，添加： `default-character-set=utf8`
* 在部分 `[mysqld]` 中，添加： `character-set-server=utf8`

## 安装MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供了用于执行SQL脚本的UI，这些脚本安装模式和初始数据。

应按照目标操作系统的说明下载并安装MySQL Workbench。

## Enablement Connection {#enablement-connection}

首次启动MySQL Workbench时（除非已用于其他用途），它尚不显示任何连接：

![mysqlconnection](assets/mysqlconnection.png)

### 新建连接设置 {#new-connection-settings}

1. 选择右侧的“+”图标 `MySQL Connections`。
1. 在对话 `Setup New Connection`框中，输入适用于您的平台以进行演示的值，并在同一服务器上输入作者AEM实例和MySQL:
   * 连接名称： `Enablement`
   * 连接方法： `Standard (TCP/IP)`
   * Hostname: `127.0.0.1`
   * 用户名: `root`
   * 密码: `no password by default`
   * 默认模式: `leave blank`
1. 选 `Test Connection` 择以验证与正在运行的MySQL服务的连接。

**注释**:
* 默认端口为 `3306`。
* 在 `Connection Name` JDBC OSGi配置中，选 `datasource` 择的 [名称被输入](#configure-jdbc-connections)。

#### 连接成功 {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### 新的Enablement Connection {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## 数据库设置 {#database-setup}

打开新的Enablement连接时，请注意存在测试模式和默认用户帐户。

![数据库设置](assets/database-setup.png)

### 获取SQL脚本 {#obtain-sql-scripts}

SQL脚本是使用创作实例上的CRXDE Lite获取的。 必 [须安装](deploy-communities.md#scorm) SCORM包：

1. 浏览至CRXDE Lite:
   * 例如， [http://localhost:4503/crx/de](http://localhost:4502/crx/de)
1. 展开文件 `/libs/social/config/scorm/` 夹
1. 下载 `database_scormengine.sql`
1. 下载 `database_scorm_integration.sql`

![sqlscript](assets/sqlscripts.png)

下载模式的一种方法是：

* 为sql `jcr:content` 文件选择节点。
* 请注意，该属性 `jcr:data` 的值是视图链接。
* 选择视图链接以将数据保存到本地文件。

### 创建SCORM数据库 {#create-scorm-database}

要创建的Enablement SCORM数据库为：

* 名称: `ScormEngineDB`
* 从脚本创建：
   * 架构: `database_scormengine.sql`
   * data: `database_scorm_integration.sql`
Follow the steps below (
[打开](#step-open-sql-file)、执 [行](#step-execute-sql-script))以安装每 [个SQL脚本](#obtain-sql-scripts) 。 [必要时](#refresh) ，请进行刷新，以查看脚本执行的结果。

安装模式之前，请务必安装数据。

>[!CAUTION]
>
>如果数据库名称已更改，请确保在以下位置正确指定它：
>
>* [JDBC配置](#configure-jdbc-connections)
>* [SCORM配置](#configure-scorm)


#### 第1步：打开SQL文件 {#step-open-sql-file}

在MySQL Workbench中

* 从“文件”下拉菜单
* 选择 `Open SQL Script ...`
* 按此顺序，选择下列选项之一：
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scrom-database](assets/scrom-database.png)

#### 第2步：执行SQL脚本 {#step-execute-sql-script}

在“工作台”窗口中，对于在步骤1中打开的文件，选择 `lightening (flash) icon` 要执行脚本的文件。

请注意，创建SCORM `database_scormengine.sql` 数据库的脚本执行可能需要一分钟时间。

![scrom-database1](assets/scrom-database1.png)

#### 刷新 {#refresh}

执行脚本后，必须刷新该 `SCHEMAS` 部分， `Navigator` 才能看到新数据库。 使用“模式”右侧的刷新图标：

![scrom-database2](assets/scrom-database2.png)

#### 结果：scormingedb {#result-scormenginedb}

安装和刷新模式后， `scormenginedb` 将显示该内容。

![scrom-database3](assets/scrom-database3.png)

## 配置JDBC连接 {#configure-jdbc-connections}

Day Commons JDBC连接 **池的OSGi配置** ，配置MySQL JDBC驱动程序。

所有发布和作者AEM实例都应指向同一个MySQL服务器。

当MySQL运行于与AEM不同的服务器上时，必须在JDBC连接器（填充ScormEngine配置）中指定服务器主机名来代替“ [localhost](#configurescormengineservice) ”。

* 在每个作者和发布AEM实例上
* 以管理员权限登录
* 访问Web [控制台](../../help/sites-deploying/configuring-osgi.md)
   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* 找到 `Day Commons JDBC Connections Pool`
* 选择图 `+` 标以创建新配置

   ![jdbcconnection1](assets/jdbcconnection1.png)

* 输入以下值：
   * **[!UICONTROL JDBC驱动程序类]**: `com.mysql.jdbc.Driver`
   * **DBC connection URIJ**: `jdbc:mysql://localhost:3306/aem63reporting` 如果MySQL服务器与“this” AEM服务器不相同，则指定服务器代替localhost。
   * **[!UICONTROL 用户名]**:为MySQL服务器输入已配置的用户名（如果不是“root”）或根。
   * **[!UICONTROL 密码]**:如果没有为MySQL设置口令，请清除此字段，否则，请输入MySQL用户名的已配置口令。
   * **[!UICONTROL 数据源名称]**:为MySQL连接 [输入的名](#new-connection-settings)称，例如“enablement”。
* 选择&#x200B;**[!UICONTROL 保存]**。

## 配置Scorm {#configure-scorm}

### AEM CommunitiesScormEngine服务 {#aem-communities-scormengine-service}

AEM CommunitiesScormEngine服 **务的OSGi配置** ，为启用社区使用MySQL服务器配置SCORM。

安装SCORM包时 [存在此配](deploy-communities.md#scorm-package) 置。

所有发布和作者实例都指向同一个MySQL服务器。

当MySQL在AEM以外的服务器上运行时，必须在ScormEngine服务中指定服务器主机名，而不是“localhost”，该服务通常从JDBC连接配 [置中填充](#configure-jdbc-connections) 。

* 在每个作者和发布AEM实例上
* 以管理员权限登录
* 访问Web [控制台](../../help/sites-deploying/configuring-osgi.md)
   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* 找到 `AEM Communities ScormEngine Service`
* 选择编辑图标

   ![chlimage_1-337](assets/chlimage_1-337.png)

* 验证以下参数值是否与JDBC连接 [配置一致](#configurejdbcconnectionspool) :
   * **[!UICONTROL JDBC连接URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB` *ScormEngineDB是* SQL脚本中的默认数据库名称
   * **[!UICONTROL 用户名]**:Root或输入MySQL服务器的已配置用户名（如果不是“root”）
   * **[!UICONTROL 密码]**:如果没有为MySQL设置口令，请清除此字段，否则，请输入为MySQL用户名配置的口令
* 关于以下参数：
   * **[!UICONTROL Scorm用户密码]**:不编辑

      仅供内部使用：它供AEM Communities使用的特殊服务用户与scorm引擎通信。
* Select **[!UICONTROL Save]**

### Adobe花岗石CSRF滤池 {#adobe-granite-csrf-filter}

要确保启用课程在所有浏览器中正常工作，必须将Mozilla添加为CSRF过滤器未检查的用户代理。

* 以管理员权限登录AEM发布实例。
* 访问Web [控制台](../../help/sites-deploying/configuring-osgi.md)
   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* 找到 `Adobe Granite CSRF Filter`。
* 选择编辑图标。

   ![jdbcconnection2](assets/jdbcconnection2.png)

* 选择图 `[+]` 标以添加安全用户代理。
* Enter `Mozilla/*`.
* 选择&#x200B;**[!UICONTROL 保存]**。

