---
title: DSRP — 关系数据库存储资源提供程序
seo-title: DSRP — 关系数据库存储资源提供程序
description: 设置AEM Communities以使用关系数据库作为其公共存储
seo-description: 设置AEM Communities以使用关系数据库作为其公共存储
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---

# DSRP — 关系数据库存储资源提供程序 {#dsrp-relational-database-storage-resource-provider}

## 关于DSRP {#about-dsrp}

当AEM Communities配置为使用关系数据库作为其公共存储时，可以从所有创作和发布实例访问用户生成的内容(UGC)，而无需同步或复制。

另请参阅[SRP选项的特性](working-with-srp.md#characteristics-of-srp-options)和[推荐的拓扑](topologies.md)。

## 要求 {#requirements}

* [MySQL](#mysql-configuration)，关系数据库。
* [Apache Solr](#solr-configuration)，搜索平台。

>[!NOTE]
>
>默认存储配置现在存储在conf路径(`/conf/global/settings/community/srpc/defaultconfiguration`)中，而不是etc路径(`/etc/socialconfig/srpc/defaultconfiguration`)中。 建议您按照[迁移步骤](#zerodt-migration-steps)来使defaultsrp按预期工作。

## 关系数据库配置 {#relational-database-configuration}

### MySQL配置 {#mysql-configuration}

MySQL安装可以通过使用不同的数据库（模式）名称以及不同的连接（服务器：端口）在同一连接池内的启用功能和公共存储(DSRP)之间共享。

有关安装和配置的详细信息，请参阅[MySQL Configuration for DSRP](dsrp-mysql.md)。

### Solr 配置 {#solr-configuration}

Solr安装可以通过使用不同的集合在节点存储(Oak)和公共存储(SRP)之间共享。

如果Oak和SRP集合都得到了集中使用，则出于性能原因，可能会安装第二个Solr。

对于生产环境，SolrCloud模式比独立模式（单个本地Solr设置）提供了更好的性能。

有关安装和配置详细信息，请参阅[SRP](solr.md)的Solr配置。

### 选择DSRP {#select-dsrp}

[存储配置控制台](srp-config.md)允许选择默认存储配置，该配置标识要使用的SRP实施。

在创作时，访问存储配置控制台

* 使用管理员权限登录
* 从&#x200B;**主菜单**

   * 选择&#x200B;**[!UICONTROL 工具]**（从左侧窗格中）
   * 选择&#x200B;**[!UICONTROL Communities]**
   * 选择&#x200B;**[!UICONTROL 存储配置]**

      * 例如，生成的位置为：[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >默认存储配置现在存储在conf路径(`/conf/global/settings/community/srpc/defaultconfiguration`)中      而不是etc路径(`/etc/socialconfig/srpc/defaultconfiguration`)。 建议您按照[迁移步骤](#zerodt-migration-steps)来使defaultsrp按预期工作。
   ![dsrp-config](assets/dsrp-config.png)

* 选择&#x200B;**[!UICONTROL 数据库存储资源提供程序(DSRP)]**
* **数据库配置**

   * **[!UICONTROL JDBC 数据源名称]**

      给MySQL连接的名称必须与在[JDBC OSGi配置](dsrp-mysql.md#configurejdbcconnections)中输入的名称相同

      *默认*:社区

   * **[!UICONTROL 数据库名称]**

      在[init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)脚本中为架构提供的名称

      *默认*:社区

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 主机**

      如果使用内部ZooKeeper运行Solr，则将此值留空。 否则，如果使用外部ZooKeeper在[SolrCloud模式](solr.md#solrcloud-mode)中运行，则将此值设置为ZooKeeper的URI，如&#x200B;*my.server.com:80*

      *默认*:  *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *默认*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr 收藏集]**

      *默认*:collection1

* 选择&#x200B;**[!UICONTROL 提交]**。

### 默认SRP的零停机时间迁移步骤 {#zerodt-migration-steps}

请按照以下步骤确保默认srp页面[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)按预期工作：

1. 将`/etc/socialconfig`的路径重命名为`/etc/socialconfig_old`，以便系统配置返回至jsrp（默认）。
1. 转到默认srp页面[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)，其中配置了jsrp。 单击&#x200B;**[!UICONTROL submit]**&#x200B;按钮，以便在`/conf/global/settings/community/srpc`创建新的默认配置节点。
1. 删除创建的默认配置`/conf/global/settings/community/srpc/defaultconfiguration`。
1. 复制旧配置`/etc/socialconfig_old/srpc/defaultconfiguration`，以替代上一步中已删除的节点(`/conf/global/settings/community/srpc/defaultconfiguration`)。
1. 删除旧等节点`/etc/socialconfig_old`。

## 发布配置 {#publishing-the-configuration}

DSRP必须被标识为所有创作实例和发布实例上的公共存储。

要使相同的配置在发布环境中可用，请执行以下操作：

* 作者：

   * 从主菜单导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复制]**
   * 双击&#x200B;**[!UICONTROL 激活树]**
   * **开始路径**:

      * 浏览到`/etc/socialconfig/srpc/`
   * 确保未选择`Only Modified`。
   * 选择&#x200B;**[!UICONTROL 激活]**。


## 管理用户数据 {#managing-user-data}

有关&#x200B;*用户*、*用户配置文件*&#x200B;和&#x200B;*用户组*&#x200B;的信息，请访问：

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

## 为DSRP重新索引解决方案 {#reindexing-solr-for-dsrp}

要重新编入DSRP Solr索引，请按照[重新编入MSRP](msrp.md#msrp-reindex-tool)索引的文档进行操作，但在为DSRP重新编入索引时，请改用此URL:**/services/social/datastore/rdb/reindex**

例如，用于为DSRP重新编入索引的curl命令将如下所示：

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
