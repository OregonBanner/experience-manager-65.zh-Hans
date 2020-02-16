---
title: DSRP —— 关系数据库存储资源提供程序
seo-title: DSRP —— 关系数据库存储资源提供程序
description: 设置AEM Communities以使用关系数据库作为其公用存储
seo-description: 设置AEM Communities以使用关系数据库作为其公用存储
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: b7c790681034e9950aa43738310f7af8b1dd0085

---


# DSRP —— 关系数据库存储资源提供程序 {#dsrp-relational-database-storage-resource-provider}

## 关于DSRP {#about-dsrp}

将AEM Communities配置为使用关系数据库作为其公用存储时，用户生成的内容(UGC)可从所有作者和发布实例访问，无需同步或复制。

另请参 [阅SRP选项的特性](working-with-srp.md#characteristics-of-srp-options) 和建 [议的拓扑](topologies.md)。

## 要求 {#requirements}

* [MySQL](#mysql-configuration)，关系数据库
* [Apache Solr](#solr-configuration)，一个搜索平台

>[!NOTE]
>
>默认存储配置现在存储在conf路径(`/conf/global/settings/community/srpc/defaultconfiguration`)中，而不是etc路径(`/etc/socialconfig/srpc/defaultconfiguration`)中。 建议您按照迁移步 [骤](#zerodt-migration-steps) ，使默认更新工作正常。


## 关系数据库配置 {#relational-database-configuration}

### MySQL配置 {#mysql-configuration}

MySQL安装可以通过使用不同的数据库（架构）名称和不同的连接（服务器：端口）在同一连接池内的启用功能和公用存储(DSRP)之间共享。

有关安装和配置详细信息，请参 [阅MySQL Configuration for DSRP](dsrp-mysql.md)。

### Solr 配置 {#solr-configuration}

通过使用不同集合可以在节点存储(Oak)和公共存储(SRP)之间共享Solr安装。

如果Oak和SRP集合都被集中使用，则可能出于性能原因安装第二个Solr。

对于生产环境，SolrCloud模式比独立模式（单个本地Solr设置）提供了改进的性能。

有关安装和配置详细信息，请参 [阅SRP的Solr配置](solr.md)。

### 选择DSRP {#select-dsrp}

“存 [储配置”控制台允许选择默认存储配置](srp-config.md) ，该配置标识要使用的SRP的实现。

在创作时，要访问“存储配置”控制台

* 使用管理员权限登录
* 从主 **菜单**

   * 选择 **[!UICONTROL 工具]** （从左侧窗格中）
   * 选择社 **[!UICONTROL 区]**
   * 选择 **[!UICONTROL 存储配置]**

      * 例如，生成的位置是： [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >默认存储配置现在存储在conf路径(`/conf/global/settings/community/srpc/defaultconfiguration`)中，而不是etc路径(`/etc/socialconfig/srpc/defaultconfiguration`)中。 建议您按照迁移步 [骤](#zerodt-migration-steps) ，使默认更新工作正常。

![chlimage_1-128](assets/chlimage_1-128.png)

* Select **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **数据库配置**

   * **[!UICONTROL JDBC 数据源名称]**

      为MySQL连接提供的名称必须与在 [JDBC OSGi配置中输入的名称相同](dsrp-mysql.md#configurejdbcconnections)

      *default*:社区

   * **[!UICONTROL 数据库名称]**

      在 [init_schema.sql脚本中为架构提供的名称](dsrp-mysql.md#obtain-the-sql-script)

      *default*:社区

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 主机&#x200B;**

      如果使用内部ZooKeeper运行Solr，则将此值留空。 否则，当在 [SolrCloud模式中运行外部ZooKeeper时](solr.md#solrcloud-mode) ，将此值设置为ZooKeeper的URI，如 *my.server.com:80*

      *default*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *default*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 收藏集]**

      *default*:collection1

* 选择&#x200B;**[!UICONTROL 提交]**。

### 默认SRP的零停机迁移步骤 {#zerodt-migration-steps}

请按照以下步骤确保默认的srp页 [面](http://localhost:4502/communities/admin/defaultsrp) http://localhost:4502/communities/admin/defaultsrp工作正常：

1. 将路径重命名 `/etc/socialconfig` 为， `/etc/socialconfig_old`以便系统配置返回至jsrp（默认）。
1. 转到默认的 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)，其中配置了jsrp。 单击“提 **[!UICONTROL 交]** ”按钮，以在上创建新的默认配置节点 `/conf/global/settings/community/srpc`。
1. 删除创建的默认配置 `/conf/global/settings/community/srpc/defaultconfiguration`。
1. 复制旧配置 `/etc/socialconfig_old/srpc/defaultconfiguration` 以代替上一步中已删除的节`/conf/global/settings/community/srpc/defaultconfiguration`点()。
1. 删除旧的等节点 `/etc/socialconfig_old`。

## 发布配置 {#publishing-the-configuration}

DSRP必须被标识为所有作者实例和发布实例上的公用商店。

要在发布环境中提供相同的配置，请执行以下操作：

* 作者：

   * 从主菜单导航到工具> **[!UICONTROL 操作>复制]**
   * Double-click **Activate Tree **
   * **开始路径:**

      * 浏览到 `/etc/socialconfig/srpc/`
   * 确 `Only Modified` 保未选择。
   * 选择激 **[!UICONTROL 活]**


## 管理用户数据 {#managing-user-data}

有关用户、用 *户配置文件**和用户* 组(通常在发布环境中输入 **)的信息，请访问

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

## 为DSRP重新构建索引解决方案 {#reindexing-solr-for-dsrp}

要重新索引DSRP Solr，请按照文档重新 [索引MSRP](msrp.md#msrp-reindex-tool)，但是，在为DSRP重新索引时，请改用此URL: **/services/social/datastore/rdb/reindex**

例如，用于重新索引DSRP的curl命令如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

