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
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# MySQL Configuration for Enablement Features {#mysql-configuration-for-enablement-features}

MySQL是关系数据库，主要用于SCORM跟踪和报告支持资源的数据。 其中包含用于跟踪视频暂停／恢复等其他功能的表。

这些说明描述了如何连接到MySQL服务器、建立启用数据库以及使用初始数据填充数据库。

## 要求 {#requirements}

在配置MySQL for Communities的启用功能之前，请务必

* 安 [装MySQL server](https://dev.mysql.com/downloads/mysql/) Community Server版本5.6:
   * SCORM不支持版本5.7。
   * 可以与作者AEM实例使用相同的服务器。
* 在所有AEM实例上，安装MySQL的正 [式JDBC驱动程序](deploy-communities.md#jdbc-driver-for-mysql)。
* 安装 [MySQL工作台](https://dev.mysql.com/downloads/tools/workbench/)。
* 在所有AEM实例上，安装 [SCORM包](enablement.md#scorm)。

## 安装MySQL {#installing-mysql}

应按照目标OS的说明下载并安装MySQL。

### 小写表名 {#lower-case-table-names}

由于SQL不区分大小写，因此对于区分大小写的操作系统，必须包含一个将所有表名都小写的设置。

例如，要指定Linux OS上的所有小写表名称：

* 编辑文件 `/etc/my.cnf`
* 在部 `[mysqld]` 分中，添加以下行： `lower_case_table_names = 1`

### UTF8字符集 {#utf-character-set}

要提供更好的多语言支持，必须使用UTF8字符集。

将MySQL更改为以UTF8作为字符集：
* mysql >设置名称“utf8”;

将MySQL数据库更改为默认的UTF8:
* 编辑文件 `/etc/my.cnf`
* 在部分 `[client]` 中，添加： `default-character-set=utf8`
* 在部分 `[mysqld]` 中，添加： `character-set-server=utf8`

## 安装MySQL Workbench {#installing-mysql-workbench}

MySQL Workbench提供了用于执行SQL脚本的UI，这些脚本安装模式和初始数据。

应按照目标OS的说明下载并安装MySQL Workbench。

## Enablement Connection {#enablement-connection}

首次启动MySQL Workbench时，除非已用于其他用途，否则它尚不显示任何连接：

![chlimage_1-327](assets/chlimage_1-327.png)

### 新连接设置 {#new-connection-settings}

1. 选择右侧的“+”图标 `MySQL Connections`。
1. 在对话框 `Setup New Connection`中，为演示目的输入适合您的平台的值，作者AEM实例和MySQL位于同一台服务器上：
   * 连接名称： `Enablement`
   * 连接方法： `Standard (TCP/IP)`
   * Hostname: `127.0.0.1`
   * 用户名: `root`
   * 密码: `no password by default`
   * 默认模式: `leave blank`
1. 选 `Test Connection` 择以验证与正在运行的MySQL服务的连接。

**注释**:
* 默认端口为 `3306`。
* 在 `Connection Name` JDBC OSGi配置中，选择 `datasource` 的名 [称是输入的](#configure-jdbc-connections)。

#### 成功连接 {#successful-connection}

![chlimage_1-328](assets/chlimage_1-328.png)

#### 新的Enablement Connection {#new-enablement-connection}

![chlimage_1-329](assets/chlimage_1-329.png)

## 数据库设置 {#database-setup}

打开新的Enablement连接时，请注意存在测试模式和默认用户帐户。

![chlimage_1-330](assets/chlimage_1-330.png)

### 获取SQL脚本 {#obtain-sql-scripts}

SQL脚本是使用创作实例上的CRXDE Lite获取的。 必 [须安装SCORM包](deploy-communities.md#scorm) :

1. 浏览到CRXDE Lite:
   * 例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. 展开文件 `/libs/social/config/scorm/` 夹
1. 下载 `database_scormengine.sql`
1. 下载 `database_scorm_integration.sql`

![chlimage_1-331](assets/chlimage_1-331.png)

下载模式的一种方法是

* 为sql `jcr:content`文件选择节点。
* 请注意，该属性的 `jcr:data`值是视图链接。
* 选择视图链接以将数据保存到本地文件。

### 创建SCORM数据库 {#create-scorm-database}

要创建的Enablement SCORM数据库是：

* 名称: `ScormEngineDB`
* 从脚本创建：
   * 架构: `database_scormengine.sql`
   * 数据：按 `database_scorm_integration.sql`照以下步骤([打开](#step-open-sql-file), [执行](#step-execute-sql-script))安装每 [个SQL脚本](#obtain-sql-scripts) 。 [根据需要](#refresh) ，刷新以查看脚本执行的结果。

安装数据之前，请务必安装模式。

>[!CAUTION]
>
>如果数据库名称已更改，请确保在以下位置正确指定它：
>
>* [JDBC配置](#configure-jdbc-connections)
>* [SCORM配置](#configure-scorm)
>



#### 第1步：打开SQL文件 {#step-open-sql-file}

在MySQL Workbench中

* 从“文件”下拉菜单
* 选择 `Open SQL Script ...`
* 在此顺序中，选择以下任一选项：
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![chlimage_1-332](assets/chlimage_1-332.png)

#### 第2步：执行SQL Script {#step-execute-sql-script}

在“工作台”窗口中，对于在步骤1中打开的文件，选择 `lightening (flash) icon` 要执行脚本的文件。

请注意，执行创 `database_scormengine.sql` 建SCORM数据库的脚本可能需要一分钟。

![chlimage_1-333](assets/chlimage_1-333.png)

#### 刷新 {#refresh}

执行脚本后，必须刷新该部分 `SCHEMAS` 才能看 `Navigator` 到新数据库。 使用“模式”右侧的刷新图标：

![chlimage_1-334](assets/chlimage_1-334.png)

#### 结果：scormenginedb {#result-scormenginedb}

安装和刷新模式后， `scormenginedb` 将显示。

![chlimage_1-335](assets/chlimage_1-335.png)

## 配置JDBC连接 {#configure-jdbc-connections}

Day Commons JDBC连接池 **的OSGi配置配置** MySQL JDBC驱动程序。

所有发布和作者AEM实例都应指向同一MySQL服务器。

当MySQL在与AEM不同的服务器上运行时，必须在JDBC连接器(填充 [](#configurescormengineservice) ScormEngine配置)中指定服务器主机名以代替“localhost”。

* 在每个作者上和发布AEM实例
* 以管理员权限登录
* 访问Web [控制台](../../help/sites-deploying/configuring-osgi.md)
   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* 找到 `Day Commons JDBC Connections Pool`
* 选择图 `+` 标以创建新配置

![chlimage_1-336](assets/chlimage_1-336.png)

* 输入以下值：
   * **[!UICONTROL JDBC驱动程序类]**: `com.mysql.jdbc.Driver`
   * **DBC connection URIJ **:如`jdbc:mysql://localhost:3306/aem63reporting`果MySQL服务器与“this”AEM服务器不同，则指定服务器代替localhost。
   * **[!UICONTROL 用户名]**:为MySQL服务器输入已配置的用户名（如果不是“root”）或根。
   * **[!UICONTROL 密码]**:如果未为MySQL设置口令，请清除此字段，否则，请输入为MySQL用户名配置的口令。
   * **[!UICONTROL 数据源名称]**:为 [MySQL连接输入的名称](#new-connection-settings)，例如，“enablement”。
* 选择&#x200B;**[!UICONTROL 保存]**。

## 配置Scorm {#configure-scorm}

### AEM Communities ScormEngine Service {#aem-communities-scormengine-service}

AEM Communities ScormEngine Service的OSGi配置 **** ，配置SCORM以使支持社区使用MySQL服务器。

安装 [SCORM包时存在此配置](deploy-communities.md#scorm-package) 。

所有发布和作者实例都指向同一个MySQL服务器。

当MySQL在与AEM不同的服务器上运行时，必须在ScormEngine服务中指定服务器主机名，而不是“localhost”，该服务通常从 [JDBC连接配置中填充](#configure-jdbc-connections) 。

* 在每个作者上和发布AEM实例
* 以管理员权限登录
* 访问Web [控制台](../../help/sites-deploying/configuring-osgi.md)
   * 例如， [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* 找到 `AEM Communities ScormEngine Service`
* 选择编辑图标
   ![chlimage_1-337](assets/chlimage_1-337.png)
* 验证以下参数值是否与 [JDBC连接配置一致](#configurejdbcconnectionspool) :
   * **[!UICONTROL JDBC连接URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB`*ScormEngineDB* 是SQL脚本中的默认数据库名
   * **[!UICONTROL 用户名]**:Root或输入MySQL服务器的已配置用户名（如果不是“root”）
   * **[!UICONTROL 密码]**:如果未为MySQL设置口令，请清除此字段，否则，请输入为MySQL用户名配置的口令
* 关于以下参数：
   * **[!UICONTROL Scorm用户密码]**:请勿编辑

      仅供内部使用：它是供AEM Communities使用的特殊服务用户与scorm引擎通信的。
* Select **[!UICONTROL Save]**

### Adobe Granite CSRF滤镜 {#adobe-granite-csrf-filter}

要确保启用课程在所有浏览器中正常工作，必须将Mozilla添加为CSRF过滤器未选中的用户代理。

* 以管理员权限登录AEM发布实例。
* 访问Web [控制台](../../help/sites-deploying/configuring-osgi.md)
   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* 找到 `Adobe Granite CSRF Filter`。
* 选择编辑图标。

   ![chlimage_1-338](assets/chlimage_1-338.png)

* 选择该 `[+]` 图标以添加安全用户代理。
* Enter `Mozilla/*`.
* 选择&#x200B;**[!UICONTROL 保存]**。

