---
title: 如何为演示设置MongoDB
seo-title: 如何为演示设置MongoDB
description: 如何为一个作者实例和一个发布实例设置MSRP
seo-description: 如何为一个作者实例和一个发布实例设置MSRP
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 如何为演示设置MongoDB {#how-to-setup-mongodb-for-demo}

## 简介 {#introduction}

本教程介绍如何为一个 [作者实例和一个发布实例](msrp.md) 设置 *MSRP*** 。

通过此设置，可以从创作和发布环境访问社区内容，而无需前进或反向复制用户生成的内容(UGC)。

此配置适用于 *非生产环境* ，例如开发和／或演示。

**生产&#x200B;*环境*应：**

* 使用复制副本集运行MongoDB
* 使用SolrCloud
* 包含多个发布者实例

## MongoDB {#mongodb}

### 安装MongoDB {#install-mongodb}

* 从https://www.mongodb.org/下载MongoDB [](https://www.mongodb.org/)

   * 操作系统选择：

      * Linux
      * Mac 10.8
      * Windows 7
   * 版本选择：

      * 至少使用版本2.6


* 基本配置

   * 按照MongoDB安装说明操作
   * 按月配置

      * 无需配置蒙古或共享
   * 已安装的MongoDB文件夹将称为&lt;mongo-install>
   * 定义的数据目录路径将称为&lt;mongo-dbpath>


* MongoDB可能与AEM在同一主机上运行，或远程运行

### 启动MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

这将使用默认端口27017启动MongoDB服务器。

* 对于Mac，使用开头arg &#39;ulimit -n 2048&#39;增加ulimit

>[!NOTE]
>
>如果MongoDB在*AEM之后*启动，**重新启动**所有**AEM **实例，这样它们就可以正确连接到MongoDB。

### 演示制作选项：设置MongoDB复制副本集 {#demo-production-option-setup-mongodb-replica-set}

以下命令是在localhost上设置具有3个节点的复制副本集的示例：

* bin/mongod —port 27017 —dbpath data —replSet rs0&amp;
* bin/mongo

   * cfg = {&quot;_id&quot;:&quot;rs0&quot;,&quot;version&quot;:1,&quot;members&quot;: [{&quot;_id&quot;:0,&quot;host&quot;:“127.0.0.1:27017”}]}
   * rs.initiate(cfg)

* bin/mongod —port 27018 —dbpath data1 —replSet rs0&amp;
* bin/mongod —port 27019 —dbpath data2 —replSet rs0&amp;
* bin/mongo

   * rs.add(&quot;127.0.0.1:27018&quot;)
   * rs.add(&quot;127.0.0.1:27019&quot;)
   * rs.status()

## Solr {#solr}

### 安装Solr {#install-solr}

* 从 [Apache Lucene下载Solr](https://archive.apache.org/dist/lucene/solr/):

   * 适用于任何操作系统
   * 使用版本4.10或版本5
   * Solr需要Java 1.7或更高版本

* 基本配置

   * 按照“示例”设置操作
   * 无需服务
   * 已安装的Solr文件夹将称为&lt;solr-install>

### 为AEM Communities配置Solr {#configure-solr-for-aem-communities}

要为MSRP进行演示配置Solr集合，需要做出两项决定（选择指向主文档的链接以了解详细信息）:

1. 在独立模式或 [SolrCloud模式下运行Solr](msrp.md#solrcloudmode)
1. 安 [装标准](msrp.md#installingstandardmls)[或高级多语言搜](msrp.md#installingadvancedmls) 索(MLS)

### 独立Solr {#standalone-solr}

运行Solr的方法可能因安装版本和方式而异。 Solr参 [考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/) ，是权威文档。

为简单起见，以版本4.10为例，在独立模式下启动Solr:

* cd到&lt;solrinstall>/example
* java -jar start.jar

这将使用默认端口8983启动Solr HTTP服务器。 您可以浏览至Solr控制台以获取Solr控制台进行测试。

* 默认Solr控制台： [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr Console不可用，请检查&lt;solrinstall>/example/logs下的日志。 查看SOLR是否尝试绑定到无法解析的特定主机名(例如，“user-macbook-pro”)。
如果是，则使用此主机名（如127.0.0.1 user-macbook-pro）的新条目更新etc/hosts文件，Solr将正确启动。

### SolrCloud {#solrcloud}

要运行非常基本（非生产）的solrCloud设置，请从以下位置开始：

* java -Dbootstrap_confdir=。/solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar

## 将MongoDB标识为公用商店 {#identify-mongodb-as-common-store}

如有必要，启动作者并发布AEM实例。

如果AEM在启动MongoDB之前运行，则需要重新启动AEM实例。

按照主文档页面上的说明操作： [MSRP - MongoDB公用商店](msrp.md)

## 测试 {#test}

要测试和验证MongoDB公用商店，请发布发布实例的注释并在创作实例上查看它，以及在MongoDB和Solr中查看UGC:

1. 在发布实例上，浏览至“社区组 [件指南”页](http://localhost:4503/content/community-components/en/comments.html) ，然后选择“注释”组件。
1. 登录以发布评论：
1. 在注释文本输入框中输入文本，然后单击“发 **[!UICONTROL 布”]**

   ![chlimage_1-191](assets/chlimage_1-191.png)

1. 只需查看作者实例的评 [论](http://localhost:4502/content/community-components/en/comments.html) （可能仍以管理员／管理员身份登录）。

   ![chlimage_1-192](assets/chlimage_1-192.png)

   注意：虽然作者在asipath下有JCR节 *点* ，但这些节点是用于SCF框架的。 实际UGC不在JCR中，而在MongoDB中。

1. 在“蒙古社区”>“集 **[!UICONTROL 合”>“内容”中查看UGC]**

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. 在Solr中查看UGC:

   * 浏览到Solr功能板： [http://localhost:8983/solr/](http://localhost:8983/solr/)
   * 要选 `core selector` 择的用户 `collection1`
   * 选择 `Query`
   * 选择 `Execute Query`
   ![chlimage_1-194](assets/chlimage_1-194.png)

## 疑难解答 {#troubleshooting}

### 不显示UGC {#no-ugc-appears}

1. 确保MongoDB已正确安装并运行。

1. 确保MSRP已配置为默认提供者：

   * 在所有作者和发布AEM实例上，重新访问存储配 [置控制台](srp-config.md)
   或检查AEM存储库：

   * 在JCR中，if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

      * 不包含srpc节 [点](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ，这意味着存储提供者是JSRP
      * 如果srpc节点存在并包含节点 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，则默认配置的属性应将MSRP定义为默认提供者


1. 确保在选择MSRP后重新启动AEM。
