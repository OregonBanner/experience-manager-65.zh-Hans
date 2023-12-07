---
title: AEM平台简介
description: 本文概述AEM平台及其最重要的组件。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# AEM平台简介{#introduction-to-the-aem-platform}

AEM 6中的AEM平台基于Apache Jackrabbit Oak。

Apache Jackrabbit Oak致力于实施可扩展且性能优异的分层内容存储库，用作现代世界一流的网站和其他要求苛刻的内容应用程序的基础。

它是Jackrabbit 2的后续版本，被AEM 6用作其内容存储库CRX的默认后端。

## 设计原则和目标 {#design-principles-and-goals}

Oak实施 [JSR-283](https://jcp.org/en/jsr/detail?id=283) (JCR 2.0)规范。 其主要设计目标为：

* 更好地支持大型存储库
* 多个分布式群集节点以实现高可用性
* 更好的性能
* 支持许多子节点和访问控制级别

## 架构概念 {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### 存储 {#storage}

存储层的目的是：

* 实施树模型
* 使存储可插拔
* 提供群集机制

### Oak Core {#oak-core}

Oak核心在存储层中添加了多个层：

* 访问级别控制
* 搜索和编制索引
* 观察

### Oak JCR {#oak-jcr}

Oak JCR的主要目标是将JCR语义转换为树操作。 它还负责：

* 实施JCR API
* 包含实施JCR约束的提交挂接

此外，非Java实施现在是可行的，并且是Oak JCR概念的一部分。

## 存储概述 {#storage-overview}

Oak存储层为内容的实际存储提供了一个抽象层。

目前，AEM6中提供了两种存储实施： **Tar存储** 和 **MongoDB存储**.

### Tar存储 {#tar-storage}

Tar存储使用tar文件。 它将内容存储为较大区段中的各种类型的记录。 日记帐用于跟踪存储库的最新状态。

它围绕几个关键设计原则构建：

* **不可变区段**

内容存储在区段中，这些区段最长可达256 KB。 它们不可变，因此可以轻松缓存经常访问的区段，并减少可能损坏存储库的系统错误。

每个区段由唯一标识符(UUID)标识，并包含内容树的连续子集。 此外，区段可以引用其他内容。 每个区段都会保留其他引用区段的UUID列表。

* **地区**

节点及其直接子节点等相关记录存储在同一区段中。 这样，对于每个会话访问多个相关节点的典型客户端，可以快速搜索存储库并避免大多数高速缓存未命中。

* **紧凑性**

记录的格式针对大小进行了优化，以降低IO成本并尽可能在缓存中容纳更多内容。

### Mongo存储 {#mongo-storage}

MongoDB存储使用MongoDB进行分片和群集。 存储库树保留在一个MongoDB数据库中，其中每个节点是一个单独的文档。

它有几个特点：

* 修订版

对于内容的每次更新（提交），都会创建一个新修订版本。 修订版本基本上是一个字符串，其中包含三个元素：

1. 从生成时间戳的计算机的系统时间派生的时间戳
1. 用于区分使用相同时间戳创建的修订版的计数器
1. 创建修订版的群集节点ID

* 分支

支持分支，允许客户端暂存多个更改，并在单个合并调用中使其可见。

* 以前的文档

MongoDB存储会在每次修改时将数据添加到文档。 但是，它仅在明确触发清理时删除数据。 当满足特定阈值时，将移动旧数据。 以前的文档只包含不可变数据，这意味着它们只包含已提交和合并的修订。

* 群集节点元数据

有关活动和非活动群集节点的数据保存在数据库中，以方便群集操作。

使用MongoDB存储的典型AEM群集设置：

![chlimage_1-85](assets/chlimage_1-85.png)

## 与Jackrabbit 2有何不同？ {#what-is-different-from-jackrabbit}

由于Oak向后兼容JCR 1.0标准，因此用户级别几乎没有任何变化。 但是，在设置基于Oak的AEM安装时，必须考虑一些显着差异：

* Oak不会自动创建索引。 因此，必要时必须创建自定义索引。
* 与Jackrabbit 2不同，Oak会话始终反映存储库的最新状态，而Jackrabbit 2则反映从获得会话时起存储库的稳定视图。 原因是Oak所基于的MVCC模型。
* Oak不支持同名同级(SNS)。

## 其他平台相关文档 {#other-platform-related-documentation}

有关AEM平台的更多信息，另请查看以下文章：

* [在AEM 6中配置节点存储和数据存储](/help/sites-deploying/data-store-config.md)
* [Oak查询和索引](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6中的存储元素](/help/sites-deploying/storage-elements-in-aem-6.md)
* [带有MongoDB的AEM](/help/sites-deploying/aem-with-mongodb.md)
