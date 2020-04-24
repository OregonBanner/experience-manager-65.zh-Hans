---
title: MSRP - MongoDB存储资源提供商
seo-title: MSRP - MongoDB存储资源提供商
description: 设置AEM Communities以使用关系数据库作为其公用存储
seo-description: 设置AEM Communities以使用关系数据库作为其公用存储
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# MSRP - MongoDB存储资源提供商 {#msrp-mongodb-storage-resource-provider}

## 关于MSRP {#about-msrp}

将AEM Communities配置为使用MSRP作为其公用存储时，用户生成的内容(UGC)可从所有作者和发布实例访问，无需同步或复制。

另请参 [阅SRP选项的特性](working-with-srp.md#characteristics-of-srp-options) 和建 [议的拓扑](topologies.md)。

## 要求 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * 版本2.6或更高版本
   * 无需配置蒙古或共享
   * 强烈建议使用复制 [副本集](#mongoreplicaset)
   * 可以与AEM在同一主机上运行或远程运行

* [Apache Solr](https://lucene.apache.org/solr/):

   * 4.10版或5版
   * Solr需要Java 1.7或更高版本
   * 无需服务
   * 运行模式的选择：
      * 独立模式
      * [SolrCloud模式](solr.md#solrcloud-mode) (建议用于生产环境)
   * 多语言搜索选择(MLS)
      * [安装标准MLS](solr.md#installing-standard-mls)
      * [安装高级MLS](solr.md#installing-advanced-mls)

## MongoDB Configuration {#mongodb-configuration}

### 选择MSRP {#select-msrp}

存储配 [置控制台允许选择默认存储配置](srp-config.md) ，该配置标识要使用的SRP的实现。

在创作时，要访问“存储配置”控制台：

* 从全局导航中，选择 **[!UICONTROL 工具]** >社区 **[!UICONTROL >]** 存储配置 ****。

![chlimage_1-28](assets/chlimage_1-28.png)

* Select **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**
* **[!UICONTROL mongoDB 配置]**

   * **[!UICONTROL mongoDB URI]**

      *default*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB 数据库]**

      *default*:社区

   * **[!UICONTROL mongoDB UGC 收藏集]**

      *default*:内容

   * **[!UICONTROL mongoDB 附件收藏集]**

      *default*:附件

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper 主机&#x200B;**

      当在 [SolrCloud模式中运行外部ZooKeeper时](solr.md#solrcloud-mode) ，将此值设置为ZooKeeper的值， `HOST:PORT`*如my.server.com:2181*

      对于ZooKeeper Ensemble，输入以逗号分 `HOST:PORT` 隔的值，如 *host1:2181,host2:2181*

      如果使用内部ZooKeeper在独立模式下运行Solr，请将其留空。
      *默认*: *&lt;blank>*

      * **[!UICONTROL Solr URL]**在独立模式下与Solr通信时使用的URL。
如果在SolrCloud模式下运行，则留空。
         *默认*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr集合]**Solr集合名称。
         *默认*:collection1

* Select **[!UICONTROL Submit]**

>[!NOTE]
>
>默认为名称的mongoDB数据库 `communities`不应设置为用于节点存储或数据（二进制）存 [储的数据库的名称](../../help/sites-deploying/data-store-config.md)。 另请参阅 [AEM 6.5中的存储元素](../../help/sites-deploying/storage-elements-in-aem-6.md)。


### MongoDB复制副本集 {#mongodb-replica-set}

对于生产环境，强烈建议设置一个复制副本集，即MongoDB服务器群集，该群集实现主从复制和自动故障切换。

要进一步了解复制集，请访问MongoDB的复制 [文档](https://docs.mongodb.org/manual/replication/) 。

要使用复制集并了解如何定义应用程序与MongoDB实例之间的连接，请访问MongoDB的 [Connection String URI格式文档](https://docs.mongodb.org/manual/reference/connection-string/) 。

#### 连接到复制副本集的示例Url {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 配置 {#solr-configuration}

通过使用不同集合可以在节点存储(Oak)和公共存储(MSRP)之间共享Solr安装。

如果Oak和MSRP集合都被集中使用，则可能出于性能原因安装第二个Solr。

对于生产环境, [SolrCloud模式比独立模式](solr.md#solrcloud-mode) （单一的本地Solr设置）提供更高的性能。

有关配置详细信息，请参 [阅SRP的Solr配置](solr.md)。

### 升级 {#upgrading}

如果从配置了MSRP的早期版本升级，则必须：

1. 执行 [到AEM Communities的升级](upgrade.md)
1. 安装新的Solr配置文件
   * 对于 [标准MLS](solr.md#installing-standard-mls)
   * 对于 [高级MLS](solr.md#installing-advanced-mls)
1. 重新索引MSRPSee部分 [MSRP重新索引工具](#msrp-reindex-tool)

## 发布配置 {#publishing-the-configuration}

MSRP必须被标识为所有作者实例和发布实例上的公用商店。

要在发布环境中提供相同的配置，请登录到您的创作实例，然后按照以下步骤操作：

* 从主菜单导航到工 **[!UICONTROL 具]** >操 **[!UICONTROL 作]** >复 **[!UICONTROL 制]**。
* 选择 **[!UICONTROL 激活树]**
* **[!UICONTROL 开始路径]**:
   * 浏览到 `/etc/socialconfig/srpc/`
* 选择激 **[!UICONTROL 活]**

## 管理用户数据 {#managing-user-data}

有关用户、用 *户用户档案****、用户*&#x200B;环境和用户组的信息，请访问

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

## MSRP重新索引工具 {#msrp-reindex-tool}

在安装新配置文件或修复损坏的Solr索引时，有一个HTTP端点用于为MSRP重新构建索引。

MongoDB是管理系统更新项目的真 *相* ;只需对MongoDB进行备份。

可以重新索引整个UGC树，或者仅索引特定子树，如*path *data参数所指定。

此工具可以使用cURL或任何其他HTTP工具从命令行运行。

重新索引时，内存和性能之间会由*batchSize *data参数控制，该参数指定每批重新索引多少UGC记录。

合理的默认值是5000:

* 如果内存是问题，请指定较小的数字
* 如果速度是问题，请指定更大的数字以提高速度

### 使用cURL命令运行MSRP重新索引工具 {#running-msrp-reindex-tool-using-curl-command}

以下cURL命令显示HTTP请求重新索引存储在MSRP中的UGC的必要条件。

基本格式为：

cURL -u *签名* -d *data**reindex-url*

*signin* = administrator-id:password例如：admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* =每个操作重新索引的UGC条目数`/content/usergenerated/asi/mongo/`

*path* =要重新索引的UGC树的根位置

* 要重新索引所有UGC，请指定 `asipath`的
   `/etc/socialconfig/srpc/defaultconfiguration`
* 要将索引限制为某些UGC，请指定 `asipath`

*reindex-url* = SRP重新索引的端点`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>如果要重新 [索引DSRP Solr](dsrp.md)，则URL为 **/services/social/datastore/rdb/reindex**


### MSRP重新索引示例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## 如何演示MSRP {#how-to-demo-msrp}

要为演示或开发环境设置MSRP，请参阅 [HowTo Setup MongoDB for Demo](demo-mongo.md)。

## 疑难解答 {#troubleshooting}

### UGC在MongoDB中不可见 {#ugc-not-visible-in-mongodb}

通过检查存储选项的配置，确保MSRP已配置为默认提供者。 默认情况下，存储资源提供者为JSRP。

在所有作者和发布AEM实例上，重新访问 [存储配置控制台](srp-config.md) ，或检查AEM存储库：

* 在JCR中，if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 不包含 [srpc节点](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ，它表示存储提供者是JSRP。
   * 如果srpc节点存在并包含节点 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，则默认配置的属性应将MSRP定义为默认提供者。

### 升级后UGC消失 {#ugc-disappears-after-upgrade}

如果从现有AEM Communities 6.0站点升级，则升级到AEM Communities 6.3后，任何预先存在的UGC必须转换为符合 [SRP](srp.md) API所需的结构。

GitHub上提供了一个开放源代码工具，用于：

* [AEM Communities UGC迁移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

可以自定义迁移工具，以从AEM社交社区的早期版本中导出UGC，以便导入AEM Communities 6.1或更高版本。

### 错误——未定义字段provider_id {#error-undefined-field-provider-id}

如果日志中显示以下错误，则表示Solr模式文件配置不正确。

#### JsonMappingException:undefined field provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

要解决该错误，请按照安装标准MLS的 [说明操作](solr.md#installing-standard-mls)，确保：

* XML配置文件被复制到正确的Solr位置。
* 新配置文件替换现有配置文件后，Solr重新启动。

### 与MongoDB的安全连接失败 {#secure-connection-to-mongodb-fails}

如果由于缺少类定义而尝试与MongoDB服务器建立安全连接失败，则必须更新MongoDB驱动程序包（可从公共主存储库获得） `mongo-java-driver`。

1. 从https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar(版本2. [13](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) .2或更高版本)下载驱动程序。
1. 将捆绑包复制到AEM实例的“crx-quickstart/install”文件夹中。
1. 重新启动AEM实例。

## 资源 {#resources}

* [AEM with MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB文档](https://docs.mongodb.org/)

