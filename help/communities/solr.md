---
title: SRP的Solr配置
seo-title: SRP的Solr配置
description: Apache Solr安装可以通过使用不同集合在节点存储(Oak)和公共存储(SRP)之间共享
seo-description: Apache Solr安装可以通过使用不同集合在节点存储(Oak)和公共存储(SRP)之间共享
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# SRP的Solr配置 {#solr-configuration-for-srp}

## 适用于AEM平台的Solr {#solr-for-aem-platform}

通过 [使用不同集合](https://lucene.apache.org/solr/) ，可以在节点存储 [(Oak)和公用存储(SRP)之间共享Apache Solr](../../help/sites-deploying/data-store-config.md)[](working-with-srp.md) 安装。

如果Oak和SRP集合都被集中使用，则可能出于性能原因安装第二个Solr。

对于生产环境, [SolrCloud模式比独立模式](#solrcloud-mode) （单一的本地Solr设置）提供更高的性能。

### 要求 {#requirements}

下载和安装Apache Solr:

* [4.10版](https://archive.apache.org/dist/lucene/solr/4.10.4/) 或5. [x版](https://archive.apache.org/dist/lucene/solr/5.5.3/)

* Solr需要Java 1.7或更高版本
* 无需服务
* 运行模式的选择：

   * 独立模式
   * [SolrCloud模式](#solrcloud-mode) (建议用于生产环境)

* 多语言搜索选择(MLS)

   * [安装标准MLS](#installing-standard-mls)
   * [安装高级MLS](#installing-advanced-mls)

## SolrCloud模式 {#solrcloud-mode}

[建议对于生产环境](https://cwiki.apache.org/confluence/display/solr/SolrCloud) ，使用SolrCloud模式。 在SolrCloud模式下运行时，必须先安装并配置SolrCloud，然后再安装多语言搜索(MLS)。

建议按照SolrCloud说明安装：

* 3 SolrCloud节点位于同一台服务器上。
* 外部的Apache ZooKeeper。

还建议将JVM配置为调整内存使用和垃圾收集。

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
-configname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

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

将集合链接到已上载到ZooKeeper的配置。

参考：[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

用法：sh./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-configname *myconfig-name*

### 标准与高级MLS的比较 {#comparison-of-standard-and-advanced-mls}

针对AEM Communities的多语言搜索(MLS)专为Solr平台构建，可跨所有支持的语言（包括英语）提供改进的搜索功能。

适用于AEM社区的MLS可作为标准MLS或高级MLS提供。 标准MLS仅包括Solr配置设置，并且不包括任何插件或资源文件。 高级MLS是更全面的解决方案，包括Solr配置设置以及插件和相关资源

标准MLS包含对以下语言的内容搜索的增强：

* 英语：改进了用于尝试匹配单词派生的修正器。
* 日语：改进了半角字符的日文标记化。

高级MLS包括对以下语言的内容搜索的增强：

* 英语：用旅鼠代替了训练员。
* 德语：添加了反编译程序。
* 法语：添加了版本处理。
* 简体中文：添加了更智能的令牌。
* 各种语言：添加了更稳定、停止单词列表和标准化器。

总之，高级MLS支持以下33种语言。

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

![chlimage_1-283](assets/chlimage_1-283.png)

### 安装标准MLS {#installing-standard-mls}

对于SRP集合（MSRP或DSRP），要支持标准多语言搜索(MLS)，必须修改两个Solr的配置文件：

* **模式.xml**
* **solrconfig.xml**

用于Solr 4.10的标准MLS文件(模式.xml、solrconfig.xml)。

用于Solr 5.x的标准MLS文件(模式.xml、solrconfig.xml)。

标准MLS文件存储在AEM存储库中。

**注意**:Solr文件存储在msrp/文件夹中，但也用于DSRP（无需更改）。

**下载说明**:替换 `solrX` 为 `solr4` 或 `solr5` 根据需要。

1. 使用CRXDE|Lite，找到：

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. 下载到部署了Solr的本地服务器。

   * 找到 `jcr:content` 节点的属 `jcr:data` 性。
   * 选择 `view` 以开始下载。
   * 确保文件以适当的名称和编码(UTF8)进行保存。

1. 按照独立模式或SolrCloud模式的安装说明操作。

#### SolrCloud模式——标准MLS {#solrcloud-mode-standard-mls}

1. 在SolrCloud模式下安装和配置Solr。
1. 准备新配置：

   1. 创建new-config-dir*，如 `solr-install-dir*/myconfig/`

   1. 将现有Solr配置目录的内容复 *制到new-config-dir*

      * 对于Solr4:复制 `solr-install-dir/example/solr/collection1/conf/`
      * 对于Solr5:复制 `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 将下载的 **模式.xml和** solrconfig.xml复制到 **new-config-dir**** ，以覆盖现有文件。


1. [将新配置上传到](#upload-a-configuration-to-zookeeper) ZooKeeper。
1. [创建一个集合](#create-a-collection) ，指定必要的参数，如分片数、副本数和配置名称。
1. 如果在创建集合时*未*提供配置名称，请将此新创建的 [集合与上传到ZooKeeper的配置链接](#link-a-collection-to-a-configuration-set) 。

1. 对于MSRP，请运行 [MSRP重新索引工具](msrp.md#msrp-reindex-tool)，除非这是新安装。

#### 独立模式——标准MLS {#standalone-mode-standard-mls}

1. 以独立模式安装Solr。
1. 如果运行Solr5，请创建一个集合1（与Solr4类似）:

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. 备份 **Solr配置目录中的** 模式.xml和solrconfig.xml **** ，例如：

   * 对于Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * 为Solr5创建： `solr-install-dir/server/solr/collection1/conf/`

1. 将下载的 **模式.xml****** 和solrconfig.xml复制到同一目录。

1. 重新启动Solr。
1. 对于MSRP，请运行 [MSRP重新索引工具](#msrpreindextool)，除非这是新安装。

### 安装高级MLS {#installing-advanced-mls}

为了支持高级MLS，除了自定义模式和Solr配置外，还需要新的Solr插件，以便SRP集合（MSRP或DSRP）。 所有必需项都打包到一个可下载的zip文件中。 此外，安装脚本包含在独立模式部署Solr时使用。

要获取高级MLS包，请参阅文 [档的部署部分中的](deploy-communities.md#aem-advanced-mls) AEM高级MLS。

要开始安装SolrCloud或独立模式，请执行以下操作：

* 将AEM-SOLR-MLS zip存档下载到承载Solr的服务器。
* 解包存档。

#### SolrCloud模式——高级MLS {#solrcloud-mode-advanced-mls}

安装说明——请注意Solr4和Solr5的几点区别：

1. 在SolrCloud模式下安装和配置Solr。
1. 将高级MLS包的内容解压到磁盘。 内容应包括：

   * **模式.xml**
   * **solrconfig.xml**
   * **stopwords/** 文件夹
   * **用户档案/文件夹**
   * **extra-libs/** folder

1. 准备新配置：

   1. 创建 *new-config-dir*

      * 例如 `solr-install-dir/myconfig/`
      * 创建子文件夹 `stopwords/` 和 `lang/`
   1. 将现有Solr配置目录的内容复制 *到new-config-dir*

      * 对于Solr4:复制 `solr-install-dir/example/solr/collection1/conf/`
      * 对于Solr5:复制 `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 将提取的 **模式** .xml和 **solrconfig.xml复制到**** new-config-dir中以覆盖现有文件。
   1. 对于Solr5:复制 `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` 到 `new-config-dir/lang/`
   1. 将提取的 **秒词／文** 件夹复 *制到new-config-dir* ，导致 `new-config-dir/stopwords/*.txt`



1. [将新配置上传到](#upload-a-configuration-to-zookeeper) ZooKeeper
1. 复制新 **用户档案/** 文件夹……

   * 对于Solr4:复制到每个节点的资源／文件夹
   * 对于Solr5:复制到每个Solr安装的server/resources/文件夹。 如果所有节点都位于同一Solr安装目录中，则此步骤仅执行一次。

1. 在SolrCloud中 **** ，在solr-home目录（包含solr.xml）中为每个节点创建一个lib/文件夹。 将以下位置的jar复制到每个节点上的新lib/文件夹：

   * **从高级MLS包中提取的extra-libs/** extra-libs
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

1. [创建一个集合](#create-a-collection) ，指定必要的参数，如分片数、副本数和配置名称。
1. 如果在创建集合时 *未提供配置名* ，请将此新创建的集 [合与上传到ZooKeeper的配置相链接](#link-a-collection-to-a-configuration-set) 。

1. 对于MSRP，请运行 [MSRP重新索引工具](#msrpreindextool)，除非这是新安装。

#### 独立模式——高级MLS {#standalone-mode-advanced-mls}

高级MLS包中包含安装脚本。

将包的内容解压缩到承载独立Solr服务器的服务器后，只需执行安装脚本即可安装必要的资源和配置文件。

* 以独立模式安装Solr。
* 如果运行Solr5，请创建一个集合1（与Solr4类似）:

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* 运行安装脚本：安 [装-v 4|5][-d solrhome][-c集合路径]:

   * -d solrhome

      Solr安装目录

   * -c集合路径

      Solr中的集合路径

   * --帮助

      打印命令行选项

   * -v [4|5]

      为解决方案设置版本

* Solr 4.10.4的示例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0的示例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**注意**:

* 安装脚本将在安装新版本之前先备份模式.xml和solrconfig.xml，然后附加“.orig”

### 关于solrconfig.xml {#about-solrconfig-xml}

solrconfig.xml **文件控制自动提交间隔和搜索可见性** ，并且需要测试和调整。

`<autoCommit>`:默认情况下，AutoCommit间隔(即对稳定存储的硬提交)设置为15秒。 搜索可见性默认为使用预提交索引。

要将搜索更改为使用更新后反映由提交引起的更改的索引，请将包含的内容更 `openSearcher` 改为true。

`autoSoftCommit`:“soft”提交可确保更改可见（索引已更新），但不确保更改同步到稳定存储（硬提交）。 结果是性能得到改进。 默认情况下， `autoSoftCommit` 在包含的设置为-1 `maxTime` 时禁用该选项。
