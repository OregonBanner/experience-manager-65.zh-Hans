---
title: MSRP - MongoDB存储资源提供程序
seo-title: MSRP - MongoDB存储资源提供程序
description: 设置AEM Communities以使用关系数据库作为其公共存储
seo-description: 设置AEM Communities以使用关系数据库作为其公共存储
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
role: Administrator
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# MSRP - MongoDB存储资源提供程序{#msrp-mongodb-storage-resource-provider}

## 关于MSRP {#about-msrp}

当AEM Communities配置为使用MSRP作为其公共存储时，用户生成的内容(UGC)可以从所有创作和发布实例访问，而无需同步或复制。

另请参阅[SRP选项的特性](working-with-srp.md#characteristics-of-srp-options)和[推荐的拓扑](topologies.md)。

## 要求 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * 版本2.6或更高版本
   * 无需配置mongo或sharding
   * 强烈建议使用[复制副本集](#mongoreplicaset)
   * 可以在与AEM相同的主机上运行或远程运行

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr版本7.0
   * Solr需要Java 1.7或更高版本
   * 不需要任何服务
   * 运行模式的选择：
      * 独立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) （建议用于生产环境）
   * 多语言搜索(MLS)选择：
      * [安装标准MLS](solr.md#installing-standard-mls)
      * [安装高级MLS](solr.md#installing-advanced-mls)

## MongoDB配置{#mongodb-configuration}

### 选择MSRP {#select-msrp}

[存储配置控制台](srp-config.md)允许选择默认存储配置，该配置标识要使用的SRP实施。

在创作时，要访问存储配置控制台，请执行以下操作：

* 从全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 存储配置]**。

![msrp](assets/msrp.png)

* 选择&#x200B;**[!UICONTROL MongoDB存储资源提供程序(MSRP)]**
* **[!UICONTROL mongoDB 配置]**

   * **[!UICONTROL mongoDB URI]**

      *默认*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB 数据库]**

      *默认*:社区

   * **[!UICONTROL mongoDB UGC 收藏集]**

      *默认*:内容

   * **[!UICONTROL mongoDB 附件收藏集]**

      *默认*:附件

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 主机**

      在具有外部ZooKeeper的[SolrCloud模式](solr.md#solrcloud-mode)中运行时，将此值设置为ZooKeeper的`HOST:PORT`，如&#x200B;*my.server.com:2181*

      对于ZooKeeper Ensemble，输入逗号分隔的`HOST:PORT`值，如&#x200B;*host1:2181,host2:2181*

      如果使用内部ZooKeeper以独立模式运行Solr，则保留为空。
      *默认*:  *&lt;blank>*

      * **[!UICONTROL Solr URL]**
用于在独立模式下与Solr通信的URL。如果在SolrCloud模式下运行，则留空。

         *默认*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr集]**
合Solr集合名称。

         *默认*:collection1

* 选择&#x200B;**[!UICONTROL Submit]**

>[!NOTE]
>
>mongoDB数据库默认为名称`communities`，不应将其设置为用于[节点存储或数据（二进制）存储](../../help/sites-deploying/data-store-config.md)的数据库名称。 另请参阅AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md)中的[存储元素。

### MongoDB副本集{#mongodb-replica-set}

对于生产环境，强烈建议设置一个复制副本集（MongoDB服务器群集，用于实施主次复制和自动故障切换）。

要了解有关副本集的更多信息，请访问MongoDB的[Replication](https://docs.mongodb.org/manual/replication/)文档。

要使用副本集并了解如何定义应用程序与MongoDB实例之间的连接，请访问MongoDB的[连接字符串URI格式](https://docs.mongodb.org/manual/reference/connection-string/)文档。

#### 用于连接到副本集{#example-url-for-connecting-to-a-replica-set}的示例Url

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 配置 {#solr-configuration}

Solr安装可以通过使用不同的集合在节点存储(Oak)和公共存储(MSRP)之间共享。

如果Oak和MSRP集合都被集中使用，则出于性能原因，可能会安装第二个Solr。

对于生产环境，[SolrCloud模式](solr.md#solrcloud-mode)比独立模式（单个本地Solr设置）提高了性能。

有关配置详细信息，请参阅[SRP](solr.md)的Solr配置。

### 升级 {#upgrading}

如果从配置了MSRP的早期版本升级，则需要：

1. 执行[升级到AEM Communities](upgrade.md)
1. 安装新的Solr配置文件
   * 对于[标准MLS](solr.md#installing-standard-mls)
   * 对于[高级MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRP
请参阅[MSRP重新索引工具](#msrp-reindex-tool)部分

## 发布配置{#publishing-the-configuration}

MSRP必须被标识为所有创作实例和发布实例上的公共存储。

要使相同配置在发布环境中可用，请登录到您的创作实例，然后按照以下步骤操作：

* 从主菜单导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 复制]**。
* 选择&#x200B;**[!UICONTROL 激活树]**
* **[!UICONTROL 开始路径]**:
   * 浏览到`/etc/socialconfig/srpc/`
* 选择&#x200B;**[!UICONTROL 激活]**

## 管理用户数据{#managing-user-data}

有关&#x200B;*用户*、*用户配置文件*&#x200B;和&#x200B;*用户组*&#x200B;的信息，请访问

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

## MSRP重新编入索引工具{#msrp-reindex-tool}

在安装新配置文件或修复损坏的Solr索引时，有一个用于为MSRP重新编制Solr索引的HTTP端点。

使用此工具，MongoDB是MSRP的&#x200B;*truth*&#x200B;的源；只需备份MongoDB即可。

整个UGC树可能会重新编入索引，或者只能按照*path *data参数指定的特定子树进行索引。

此工具可以使用cURL或任何其他HTTP工具从命令行运行。

重新索引时，在内存与*batchSize *data参数控制的性能之间存在权衡，该参数指定每批重新索引多少个UGC记录。

合理的违约为5000:

* 如果内存是问题，请指定一个较小的数字
* 如果速度是问题，请指定更大的数字以提高速度

### 使用cURL命令{#running-msrp-reindex-tool-using-curl-command}运行MSRP重新索引工具

以下cURL命令显示HTTP请求重新索引存储在MSRP中的UGC所需的内容。

基本格式为：

cURL -u *signin* -d *data* *reindex-url*

*signin*  = administrator-id:password例如：管理员：管理员

*data*  = &quot;batchSize=*size*&amp;path=*path&quot;*

*size*  =每个操作要重新索引的UGC条目数 
`/content/usergenerated/asi/mongo/`

*path*  =要重新索引的UGC树的根位置

* 要重新索引所有UGC，请指定`asipath`
   `/etc/socialconfig/srpc/defaultconfiguration`
* 要将索引限制为某些UGC，请指定`asipath`的子树

*reindex-url*  = SRP的重新索引端点 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果您正在[重新索引DSRP Solr](dsrp.md)，则URL为&#x200B;**/services/social/datastore/rdb/reindex**

### MSRP重新索引示例{#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何演示MSRP {#how-to-demo-msrp}

要为演示或开发环境设置MSRP，请参阅[HowTo Setup MongoDB for Demo](demo-mongo.md)。

## 疑难解答 {#troubleshooting}

### UGC在MongoDB {#ugc-not-visible-in-mongodb}中不可见

通过检查存储选项的配置，确保MSRP配置为默认提供程序。 默认情况下，存储资源提供程序为JSRP。

在所有创作和发布AEM实例上，重新访问[存储配置控制台](srp-config.md)或检查AEM存储库：

* 在JCR中，如果[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)节点，表示存储提供程序是JSRP。
   * 如果srpc节点存在并包含节点[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，则默认配置的属性应将MSRP定义为默认提供程序。

### 升级{#ugc-disappears-after-upgrade}后UGC消失

如果从现有的AEM Communities 6.0站点升级，则必须转换任何预先存在的UGC，以符合升级到AEM Communities 6.3后[ SRP](srp.md) API所需的结构。

GitHub上提供了一个开源工具，用于此目的：

* [AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

可以自定义迁移工具，以将UGC从AEM社交社区的早期版本导出，以导入AEM Communities 6.1或更高版本。

### 错误 — 未定义的字段provider_id {#error-undefined-field-provider-id}

如果日志中出现以下错误，则表示Solr架构文件配置不正确。

#### JsonMappingException:未定义的字段provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

要解决该错误，请按照[安装标准MLS](solr.md#installing-standard-mls)的说明进行操作，确保：

* XML配置文件已复制到正确的Solr位置。
* Solr在新配置文件替换现有配置文件后重新启动。

### 与MongoDB的安全连接失败{#secure-connection-to-mongodb-fails}

如果由于缺少类定义而尝试与MongoDB服务器建立安全连接失败，则必须更新公共Maven存储库中提供的MongoDB驱动程序包`mongo-java-driver`。

1. 从[https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar)(版本2.13.2或更高版本)下载驱动程序。
1. 将包复制到AEM实例的“crx-quickstart/install”文件夹中。
1. 重新启动AEM实例。

## 资源 {#resources}

* [AEM with MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB文档](https://docs.mongodb.org/)
