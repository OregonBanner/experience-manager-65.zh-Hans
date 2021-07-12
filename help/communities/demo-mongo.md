---
title: 如何为演示设置MongoDB
seo-title: 如何为演示设置MongoDB
description: 如何为一个创作实例和一个发布实例设置MSRP
seo-description: 如何为一个创作实例和一个发布实例设置MSRP
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# 如何为演示设置MongoDB {#how-to-setup-mongodb-for-demo}

## 简介 {#introduction}

本教程介绍如何为&#x200B;*一个author*&#x200B;实例和&#x200B;*一个publish*&#x200B;实例设置[MSRP](msrp.md)。

通过此设置，可以从创作和发布环境访问社区内容，而无需转发或反向复制用户生成的内容(UGC)。

此配置适用于&#x200B;*非生产*&#x200B;环境，例如用于开发和/或演示。

**生产 ** 环境应：**

* 使用复制副本集运行MongoDB
* 使用SolrCloud
* 包含多个发布者实例

## MongoDB {#mongodb}

### 安装MongoDB {#install-mongodb}

* 从[https://www.mongodb.org/](https://www.mongodb.org/)下载MongoDB

   * 操作系统选择：

      * Linux
      * Mac 10.8
      * Windows 7
   * 版本选择：

      * 至少使用版本2.6


* 基本配置

   * 按照MongoDB安装说明操作。
   * 为mongod配置：

      * 无需配置mongo或sharding。
   * 已安装的MongoDB文件夹将称为&lt;mongo-install>。
   * 定义的数据目录路径将称为&lt;mongo-dbpath>。


* MongoDB可以在与AEM相同的主机上运行或远程运行。

### 启动MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath  &lt;mongo-dbpath>

这将使用默认端口27017启动MongoDB服务器。

* 对于Mac，使用开始arg &#39;ulimit -n 2048&#39;增加上限

>[!NOTE]
>
>如果在&#x200B;*AEM之后启动MongoDB*，则&#x200B;**重新启动**&#x200B;所有&#x200B;**AEM**&#x200B;实例，以便它们正确连接到MongoDB。

### 演示制作选项：设置MongoDB复制副本集 {#demo-production-option-setup-mongodb-replica-set}

以下命令是在本地主机上设置具有3个节点的复制副本集的示例：

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### 安装Solr {#install-solr}

* 从[Apache Lucene](https://archive.apache.org/dist/lucene/solr/)下载Solr:

   * 适用于任何操作系统。
   * Solr版本7.0。
   * Solr需要Java 1.7或更高版本。

* 基本配置

   * 遵循“示例”Solr设置。
   * 不需要任何服务。
   * 已安装的Solr文件夹将称为&lt;solr-install>。

### 为AEM Communities配置Solr {#configure-solr-for-aem-communities}

要为演示配置MSRP的Solr集合，需要做出两项决策（选择主文档的链接以了解详细信息）：

1. 在独立模式或[SolrCloud模式](msrp.md#solrcloudmode)中运行Solr。
1. 安装[标准](msrp.md#installingstandardmls)或[高级](msrp.md#installingadvancedmls)多语言搜索(MLS)。

### 独立解决方案 {#standalone-solr}

运行Solr的方法可能因安装版本和方式而异。 [Solr参考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/)是权威文档。

为简单起见，以版本4.10为例，在独立模式下启动Solr:

* cd到&lt;solrinstall>/example
* java -jar start.jar

这将使用默认端口8983启动Solr HTTP服务器。 您可以浏览到Solr控制台以获取Solr控制台进行测试。

* 默认Solr控制台：[http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr Console不可用，请检查&lt;solrinstall>/example/logs下的日志。 查看SOLR是否尝试绑定到无法解析的特定主机名(例如，“user-macbook-pro”)。
如果是，则使用此主机名的新条目（例如127.0.0.1 user-macbook-pro）更新etc/hosts文件，并且Solr将正常启动。

### SolrCloud {#solrcloud}

要运行非常基本（而非生产）的solrCloud设置，请从以下内容开始解决：

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## 将MongoDB标识为公用存储 {#identify-mongodb-as-common-store}

根据需要启动创作和发布AEM实例。

如果AEM在启动MongoDB之前运行，则需要重新启动AEM实例。

按照主文档页面上的说明操作：[MSRP - MongoDB公用存储](msrp.md)

## 测试 {#test}

要测试和验证MongoDB公用存储，请在发布实例上发布评论，并在创作实例上查看该评论，以及在MongoDB和Solr中查看UGC:

1. 在发布实例上，浏览到[社区组件指南](http://localhost:4503/content/community-components/en/comments.html)页面，然后选择注释组件。
1. 登录以发布评论：
1. 在评论文本输入框中输入文本，然后单击&#x200B;**[!UICONTROL Post]**

   ![帖子评论](assets/post-comment.png)

1. 只需在[author实例](http://localhost:4502/content/community-components/en/comments.html)上查看注释即可（可能仍以管理员/管理员身份登录）。

   ![view-comment](assets/view-comment.png)

   注意：虽然作者的&#x200B;*asipath*&#x200B;下有JCR节点，但这些节点适用于SCF框架。 实际UGC不在JCR中，而在MongoDB中。

1. 在mongodb **[!UICONTROL Communities]** > **[!UICONTROL Collections]** > **[!UICONTROL Content]**&#x200B;中查看UGC

   ![ugc-content](assets/ugc-content.png)

1. 在Solr中查看UGC:

   * 浏览至Solr功能板：[http://localhost:8983/solr/](http://localhost:8983/solr/)。
   * 用户`core selector`选择`collection1`。
   * 选择 `Query`.
   * 选择 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## 疑难解答 {#troubleshooting}

### 未显示UGC {#no-ugc-appears}

1. 确保MongoDB已安装并正常运行。

1. 确保MSRP已配置为默认提供程序：

   * 在所有创作和发布AEM实例上，重新访问[存储配置控制台](srp-config.md)或检查AEM存储库：

   * 在JCR中，如果[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)节点，则表示存储提供程序是JSRP。
   * 如果srpc节点存在并包含节点[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，则默认配置的属性应将MSRP定义为默认提供程序。

1. 确保在选择MSRP后重新启动AEM。
