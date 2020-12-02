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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---


# 如何为演示{#how-to-setup-mongodb-for-demo}设置MongoDB

## 简介 {#introduction}

本教程介绍如何为&#x200B;*一个author*&#x200B;实例和&#x200B;*一个publish*&#x200B;实例设置[MSRP](msrp.md)。

通过此设置，可以从创作和发布环境访问社区内容，无需前进或反向复制用户生成的内容(UGC)。

此配置适用于&#x200B;*非生产*&#x200B;环境，如开发和／或演示。

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

   * 按照MongoDB安装说明进行操作。
   * 根据mongod配置：

      * 无需配置猫鼬或共享。
   * 已安装的MongoDB文件夹将称为&lt;mongo-install>。
   * 定义的数据目录路径将称为&lt;mongo-dbpath>。


* MongoDB可以与AEM运行在同一台主机上，也可以远程运行。

### 开始MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath  &lt;mongo-dbpath>

这将使用默认端口27017开始MongoDB服务器。

* 对于Mac，使用开始arg &#39;ulimit -n 2048&#39;增加上限

>[!NOTE]
>
>如果在&#x200B;*AEM之后启动* MongoDB，则&#x200B;**重新启动**&#x200B;所有&#x200B;**AEM**&#x200B;实例，以便它们正确连接到MongoDB。

### 演示制作选项：设置MongoDB副本集{#demo-production-option-setup-mongodb-replica-set}

以下命令是在localhost上设置具有3个节点的复制副本集的示例：

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

   * 按照“示例”Solr设置操作。
   * 无需任何服务。
   * 已安装的Solr文件夹将称为&lt;solr-install>。

### 为AEM Communities配置Solr {#configure-solr-for-aem-communities}

要为演示配置Solr集合，需要做出以下两项决定（选择主文档的链接以了解详细信息）:

1. 以独立模式或[SolrCloud模式](msrp.md#solrcloudmode)运行Solr。
1. 安装[标准](msrp.md#installingstandardmls)或[高级](msrp.md#installingadvancedmls)多语言搜索(MLS)。

### 独立Solr {#standalone-solr}

运行Solr的方法可能因安装版本和方式而异。 [Solr参考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/)是权威文档。

为简单起见，以4.10版为例，在独立模式下开始Solr:

* cd到&lt;solrinstall>/example
* java -jar开始.jar

这将使用默认端口8983开始Solr HTTP服务器。 您可以浏览至Solr控制台，获取Solr控制台进行测试。

* 默认Solr控制台：[http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr控制台不可用，请检查&lt;solrinstall>/example/logs下的日志。 查看SOLR是否尝试绑定到无法解析的特定主机名(例如，“user-macbook-pro”)。
如果是，则使用此主机名的新条目（如127.0.0.1 user-macbook-pro）更新etc/hosts文件，Solr将正确开始。

### SolrCloud {#solrcloud}

要运行非常基本（非生产）的solrCloud设置，开始solr具有：

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## 将MongoDB标识为公用存储{#identify-mongodb-as-common-store}

如有必要，启动作者实例并发布AEM实例。

如果AEM在启动MongoDB之前运行，则需要重新启动AEM实例。

按照主文档页上的说明操作：[MSRP - MongoDB公用存储](msrp.md)

## 测试 {#test}

要测试和验证MongoDB公用商店，请发布发布实例的注释并将其视图到创作实例，并在MongoDB和Solr中视图UGC:

1. 在发布实例上，浏览至[社区组件指南](http://localhost:4503/content/community-components/en/comments.html)页面，然后选择评论组件。
1. 登录以发布评论：
1. 在注释文本输入框中输入文本，然后单击&#x200B;**[!UICONTROL 发布]**

   ![置评后](assets/post-comment.png)

1. 只需视图[作者实例](http://localhost:4502/content/community-components/en/comments.html)上的评论（可能仍以管理员／管理员身份登录）。

   ![视图注释](assets/view-comment.png)

   注意：虽然作者&#x200B;*asipath*&#x200B;下有JCR节点，但这些节点适用于SCF框架。 实际UGC不在JCR中，而在MongoDB中。

1. 视图mongodb **[!UICONTROL Communities]** > **[!UICONTROL 集合]** > **[!UICONTROL 内容]**&#x200B;中的UGC

   ![ugc内容](assets/ugc-content.png)

1. 视图Solr中的UGC:

   * 浏览至Solr仪表板:[http://localhost:8983/solr/](http://localhost:8983/solr/)。
   * 用户`core selector`可选择`collection1`。
   * 选择 `Query`.
   * 选择 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## 疑难解答 {#troubleshooting}

### 未显示UGC {#no-ugc-appears}

1. 确保MongoDB已安装并正常运行。

1. 确保MSRP已配置为默认提供程序：

   * 在所有作者和发布AEM实例上，重新访问[存储配置控制台](srp-config.md)或检查AEM存储库：

   * 在JCR中，如果[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)不包含[srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)节点，则表示存储提供程序是JSRP。
   * 如果srpc节点存在并包含节点[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，则defaultconfiguration的属性应将MSRP定义为默认提供程序。

1. 确保在选择MSRP后重新启动AEM。
