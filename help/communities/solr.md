---
title: SRP的Solr配置
seo-title: SRP的Solr配置
description: Apache Solr安装可以通过使用不同集合在节点存储(Oak)和公用存储(SRP)之间共享
seo-description: Apache Solr安装可以通过使用不同集合在节点存储(Oak)和公用存储(SRP)之间共享
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: 94bc3550a7e18b9203e7a0d495d195d7b798e012
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 2%

---


# SRP的Solr配置 {#solr-configuration-for-srp}

## AEM Platform的Solr {#solr-for-aem-platform}

Apache [Solr](https://lucene.apache.org/solr/) (Aak)安装可通过使用不同 [的集合在节](../../help/sites-deploying/data-store-config.md) 点存储(Oak [)和公共存](working-with-srp.md) 储(SRP)之间共享。

如果Oak和SRP集合都被集中使用，则可能出于性能原因安装第二个Solr。

对于生产环境, [SolrCloud模式比独立模式](#solrcloud-mode) （单个本地Solr设置）提供更高的性能。

### 要求 {#requirements}

下载和安装Apache Solr:

* [版本 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr需要Java 1.7或更高版本
* 无需服务
* 运行模式的选择：

   * 独立模式
   * [SolrCloud模式](#solrcloud-mode) (建议用于生产环境)

* 多语言搜索选择(MLS)

   * [安装标准MLS](#installing-standard-mls)
   * [安装高级MLS](#installing-advanced-mls)

## SolrCloud模式 {#solrcloud-mode}

[建议对](https://cwiki.apache.org/confluence/display/solr/SolrCloud) “生产”环境使用SolrCloud模式。 在SolrCloud模式下运行时，必须先安装并配置SolrCloud，然后再安装多语言搜索(MLS)。

建议按照SolrCloud说明进行安装：

* 3 SolrCloud节点位于同一服务器上。
* 外部的阿帕奇动物园守护者。

还建议配置JVM以调整内存使用和垃圾收集。

### JVM配置示例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud设置命令 {#solrcloud-setup-commands}

在SolrCloud模式下运行时，在安装MLS之前，必须使用并了解以下SolrCloud设置命令。

#### 1.将配置上传到ZooKeeper {#upload-a-configuration-to-zookeeper}

参考：[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

用法：sh./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confidr *config-dir*

#### 2.创建集合 {#create-a-collection}

参考：[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

使用:
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p端 *口*\
-s *碎片数* \
-rf *复制副本数*

#### 3.将集合链接到配置集 {#link-a-collection-to-a-configuration-set}

将集合链接到已上传到ZooKeeper的配置。

参考：[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

用法：sh./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-configname *myconfig-name*

### 标准与高级MLS的比较 {#comparison-of-standard-and-advanced-mls}

AEM Communities的多语言搜索(MLS)是为Solr平台构建的，旨在提供跨所有支持语言（包括英语）的改进搜索。

AEM社区的MLS可以作为标准MLS或高级MLS提供。 标准MLS仅包括Solr配置设置，并且不包括任何插件或资源文件。 高级MLS是更全面的解决方案，包括Solr配置设置以及插件和相关资源

标准MLS包括对以下语言的内容搜索的增强：

* 英语：改进了用于尝试匹配字派生的调整器。
* 日语：改进了半角字符的日文标记。

高级MLS包括对以下语言的内容搜索的增强：

* 英语：用旅鼠代替了训练员。
* 德语：添加了反编译程序。
* 法语：添加了版本处理。
* 简体中文：添加了更智能的令牌。
* 各种语言：添加了更简单、停止单词列表和正常化符。

高级MLS支持以下33种语言。

| 阿拉伯语 | 德语 | 挪威语 |
|---|---|---|
| 保加利亚语 | 希腊语 | 波兰语 |
| 中文（简体） | 海地克里奥尔 | 葡萄牙语 |
| 中文（繁体） | 希伯来语 | 罗马尼亚语 |
| 捷克语 | 匈牙利语 | 俄语 |
| 丹麦语 | 印尼语 | 斯洛伐克语 |
| 荷兰语 | 意大利语 | 斯洛文尼亚语 |
| 英语 | 日语 | 西班牙语 |
| 爱沙尼亚语 | 韩语 | 瑞典语 |
| 芬兰语 | 拉脱维亚语 | 泰语 |
| 法语 | 立陶宛语 | 土耳其语 |

#### AEM 6.1 Solr搜索、标准MLS和高级MLS的比较 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**注意**:AEM 6.1指AEM 6.1 Communities FP3及更早版本。

![compare-solr-mls](assets/compare-solr-mls.png)

### 安装标准MLS {#installing-standard-mls}

对于SRP集合（MSRP或DSRP），要支持标准多语言搜索(MLS)，必须修改两个Solr的配置文件：

* **模式.xml**
* **solrconfig.xml**

Solr 4.10的标准MLS文件(模式.xml、solrconfig.xml)。

适用于Solr 5.x的标准MLS文件(模式.xml、solrconfig.xml)。

标准MLS文件存储在AEM存储库中。

**注意**:Solr文件存储在msrp/文件夹中，也用于DSRP（无需更改）。

**下载说明**:替换为 `solrX` 或 `solr4` 根据需要 `solr5` 进行替换。

1. 使用CRXDE|Lite，找到：

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. 下载到部署了Solr的本地服务器。

   * 找到 `jcr:content` 节点的属 `jcr:data` 性。
   * 选择 `view` 以开始下载。
   * 确保文件以适当的名称和编码(UTF8)进行保存。

1. 按照独立或SolrCloud模式的安装说明操作。

#### SolrCloud模式——标准MLS {#solrcloud-mode-standard-mls}

1. 在SolrCloud模式下安装和配置Solr。
1. 准备新配置：

   1. 创建new-config-dir*，如 `solr-install-dir*/myconfig/`

   1. 将现有Solr配置目录的内容复 *制到new-config-dir*

      * 对于Solr4:复制 `solr-install-dir/example/solr/collection1/conf/`
      * 对于Solr5:复制 `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 将下载的 **模式.xml****和solrconfig.xml** 复制 *到new-config-dir* ，以覆盖现有文件。


1. [将新配置上传](#upload-a-configuration-to-zookeeper) 到ZooKeeper。
1. [创建指定必](#create-a-collection) 要参数的集合，如分片数、副本数和配置名称。
1. 如果在创建集合时*未*提供配置名称，请将此新 [创建的集合与上传到ZooKeeper](#link-a-collection-to-a-configuration-set) 的配置链接起来。

1. 对于MSRP，请运 [行MSRP重新索引工具](msrp.md#msrp-reindex-tool)，除非这是新安装。

#### 独立模式——标准MLS {#standalone-mode-standard-mls}

1. 以独立模式安装Solr。
1. 如果运行Solr5，请创建集合1（与Solr4相似）:

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. 备份 **Solr配置****目录中的** 模式.xml和solrconfig.xml，如：

   * 对于Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * 为Solr5创建： `solr-install-dir/server/solr/collection1/conf/`

1. 将下载的 **模式** .xml **和solrconfig.xml复制到** 同一目录。

1. 重新启动Solr。
1. 对于MSRP，请运 [行MSRP重新索引工具](#msrpreindextool)，除非这是新安装。

### 安装高级MLS {#installing-advanced-mls}

要支持高级MLS的SRP集合（MSRP或DSRP），除了自定义模式和Solr配置外，还需要新的Solr插件。 所有必需项目都打包到一个可下载的zip文件中。 此外，在独立模式下部署Solr时，还包含一个安装脚本。

要获取高级MLS包，请参 [阅文档的](deploy-communities.md#aem-advanced-mls) “部署”部分中的AEM Advanced MLS。

要开始安装SolrCloud或独立模式，请执行以下操作：

* 将AEM-SOLR-MLS zip存档下载到承载Solr的服务器。
* 解包存档。

#### SolrCloud模式——高级MLS {#solrcloud-mode-advanced-mls}

安装说明——注意Solr4和Solr5的几点区别：

1. 在SolrCloud模式下安装和配置Solr。
1. 将高级MLS包的内容解压到磁盘。 内容应包括：

   * **模式.xml**
   * **solrconfig.xml**
   * **stopwords/文件夹**
   * **用户档案/** 文件夹
   * **extra-libs/** folder

1. 准备新配置：

   1. 创建 *新配置目录*

      * 例如 `solr-install-dir/myconfig/`
      * 创建子文件夹 `stopwords/` 和 `lang/`
   1. 将现有Solr配置目录的内容复 *制到new-config-dir*

      * 对于Solr4:复制 `solr-install-dir/example/solr/collection1/conf/`
      * 对于Solr5:复制 `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 将提取 **的模式** .xml **和solrconfig.xml** 复制 *到new-config-dir* ，以覆盖现有文件。
   1. 对于Solr5:复制 `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` 到 `new-config-dir/lang/`
   1. 将提取的 **秒词** /文件 *夹复制到new-config-dir* ，导致 `new-config-dir/stopwords/*.txt`



1. [将新配置上传](#upload-a-configuration-to-zookeeper) 到ZooKeeper
1. 复制新 **用户档案** /文件夹……

   * 对于Solr4:复制到每个节点的资源／文件夹
   * 对于Solr5:复制到每个Solr安装的服务器／资源／文件夹。 如果所有节点都位于同一Solr安装目录中，则此步骤仅执行一次。

1. 在SolrCloud **中** 每个节点的solr-home目录（包含solr.xml）中创建一个lib/文件夹。 将以下位置的jar复制到每个节点上的新lib/文件夹：

   * **从高级MLS包** 中提取的extra-libs/
   * *solr-install-dir/contrib/提取/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/* jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/* jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/* jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/分析-extras/lib/*.jar
   * *solr-install-dir/contrib/分析-extras/lucene-libs/*.jar

1. [创建指定必](#create-a-collection) 要参数的集合，如分片数、副本数和配置名称。
1. 如果创建集合时 *未提* 供配置名称，请将此新 [创建的集合与上传到ZooKeeper的](#link-a-collection-to-a-configuration-set) 配置相链接。

1. 对于MSRP，请运 [行MSRP重新索引工具](#msrpreindextool)，除非这是新安装。

#### 独立模式——高级MLS {#standalone-mode-advanced-mls}

高级MLS包中包含安装脚本。

将包的内容解压缩到承载独立Solr服务器的服务器后，只需执行安装脚本即可安装必要的资源和配置文件。

* 以独立模式安装Solr。
* 如果运行Solr5，请创建集合1（与Solr4相似）:

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* 运行安装脚本：安 [装-v 4|5] - [d solrhome] -c集合 [路径]:

   * -d solhome

      Solr安装目录

   * -c集合路径

      Solr中的集合路径

   * --帮助

      打印命令行选项

   * -v [4|5]

      为solr设置版本

* Solr 4.10.4的示例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0的示例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**注意**:

* 安装脚本将先备份模式.xml和solrconfig.xml，然后再通过附加“.orig”来安装新版本

### 关于solrconfig.xml {#about-solrconfig-xml}

solrconfig. **xml文件控制** “自动提交”间隔和搜索可见性，并且需要测试和调整。

`<autoCommit>`:默认情况下，自动提交间隔(即对稳定存储的硬提交)设置为15秒。 搜索可见性默认为使用预提交索引。

要将搜索更改为使用已更新的索引来反映由于提交而发生的更改，请将包含的内容更 `openSearcher` 改为true。

`autoSoftCommit`:“soft”提交可确保更改可见（索引已更新），但不确保更改同步到稳定存储（硬提交）。 结果是性能得到改进。 默认情况 `autoSoftCommit` 下，包含的设置 `maxTime` 为-1时禁用。
