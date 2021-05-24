---
title: AEM平台简介
seo-title: AEM平台简介
description: 本文提供了AEM平台及其最重要组件的一般概述。
seo-description: 本文提供了AEM平台及其最重要组件的一般概述。
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 0%

---

# AEM Platform{#introduction-to-the-aem-platform}简介

AEM 6中的AEM平台基于Apache Jackrabbit Oak。

Apache Jackrabbit Oak旨在实施可扩展且性能卓越的分层内容存储库，以用作现代世界级网站和其他要求苛刻的内容应用程序的基础。

它是Jackrabbit 2的后续版本，由AEM 6用作其内容存储库CRX的默认后端。

## 设计原则和目标{#design-principles-and-goals}

Oak实施[JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html)(JCR 2.0)规范。 其主要设计目标是：

* 更好地支持大型存储库
* 多个分布式群集节点以实现高可用性
* 性能更佳
* 支持许多子节点和访问控制级别

## 架构概念{#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### 存储 {#storage}

存储层的用途是：

* 实施树模型
* 使存储可插拔
* 提供聚类机制

### Oak Core {#oak-core}

Oak Core在存储层中添加了多个层：

* 访问级别控制
* 搜索和索引
* 观察

### Oak JCR {#oak-jcr}

Oak JCR的主要目标是将JCR语义转换为树操作。 它还负责：

* 实施JCR API
* 包含实现JCR约束的提交挂接

此外，现在还可以实施非Java，这是Oak JCR概念的一部分。

## 存储概述{#storage-overview}

Oak存储层为内容的实际存储提供了一个抽象层。

目前，AEM6中提供了两种存储实施：**Tar存储**&#x200B;和&#x200B;**MongoDB存储**。

### 焦油存储{#tar-storage}

Tar存储使用tar文件。 它将内容存储为较大区段内的各种类型记录。 日记帐用于跟踪存储库的最新状态。

它围绕以下几项关键设计原则构建：

* **不可变区段**

内容存储在区段中，其大小最大可达256KiB。 它们不可变，因此可以轻松缓存经常访问的区段，并减少可能损坏存储库的系统错误。

每个区段都由唯一标识符(UUID)来标识，并包含内容树的连续子集。 此外，区段可以引用其他内容。 每个区段会保留其他引用区段的UUID列表。

* **地区**

相关记录（如节点及其直接子项）通常存储在同一区段中。 这使得搜索存储库的速度非常快，并且避免了对于每个会话访问多个相关节点的典型客户端而言，大多数缓存缺失。

* **紧实度**

记录格式在大小方面进行了优化，以降低IO成本，并尽可能地适应缓存中的内容。

### Mongo存储{#mongo-storage}

MongoDB存储利用MongoDB进行分片和群集。 存储库树保存在一个MongoDB数据库中，其中每个节点都是一个单独的文档。

它有几个特点：

* 修订

对于内容的每次更新（提交），将创建一个新修订版本。 修订版本基本上是一个包含三个元素的字符串：

1. 从上生成的计算机的系统时间派生的时间戳
1. 用于区分使用相同时间戳创建的修订的计数器
1. 创建修订版的群集节点ID

* 分支

支持分支，它允许客户端存放多个更改，并通过单个合并调用使其可见。

* 以前的文档

MongoDB存储通过每次修改将数据添加到文档中。 但是，仅当明确触发清理时，它才会删除数据。 当满足特定阈值时，将移动旧数据。 以前的文档仅包含不可变数据，这意味着它们仅包含已提交和合并的修订。

* 群集节点元数据

有关活动和非活动群集节点的数据保存在数据库中，以便于群集操作。

具有MongoDB存储的典型AEM群集设置：

![chlimage_1-85](assets/chlimage_1-85.png)

## 跟Jackrabbit 2有什么不同？{#what-is-different-from-jackrabbit}

由于Oak旨在向后兼容JCR 1.0标准，因此用户级别几乎不会发生任何更改。 但是，在设置基于Oak的AEM安装时，您需要考虑一些显着的差异：

* Oak不会自动创建索引。 因此，需要创建自定义索引。
* 与Jackrabbit 2不同，Oak会话始终反映存储库的最新状态，而Oak会话则反映从获取会话时存储库的稳定视图。 这是由于Oak所基于的MVCC模型所致。
* Oak不支持同名同级(SNS)。

## 其他平台相关文档{#other-platform-related-documentation}

有关AEM平台的更多信息，另请查看以下文章：

* [在AEM 6中配置节点存储和数据存储](/help/sites-deploying/data-store-config.md)
* [Oak查询和索引](/help/sites-deploying/queries-and-indexing.md)
* [AEM 6中的存储元素](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM with MongoDB](/help/sites-deploying/aem-with-mongodb.md)
