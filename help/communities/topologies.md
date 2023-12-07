---
title: 推荐的社区拓扑
description: 如何处理用户生成的内容(UGC)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# 推荐的社区拓扑 {#recommended-topologies-for-communities}

自AEM Communities 6.1起，采用了一种独特的方法来处理网站访客（成员）从发布环境提交的用户生成内容(UGC)。

此方法与AEM平台处理通常从创作环境管理的站点内容的方式存在根本性的不同。

AEM平台使用节点存储区，将站点内容从创作复制到发布，而AEM Communities使用单个通用存储区来存储UGC，且永远不会复制该存储。

对于常见的UGC存储，需要选择 [存储资源提供程序(SRP)](working-with-srp.md). 建议的选项包括：

* [DSRP — 关系数据库存储资源提供程序](dsrp.md)
* [MSRP - MongoDB存储资源提供程序](msrp.md)
* [ASRP -Adobe存储资源提供程序](asrp.md)

一个其他SRP选项， [JSRP - JCR存储资源提供程序](jsrp.md)中，不支持将公共UGC存储区用于作者和发布环境的访问。

要求公用存储会导致以下推荐的拓扑。

>[!NOTE]
>
>对于AEM Communities， [从不复制UGC](working-with-srp.md#ugc-never-replicated).
>
>当部署不包含 [公用存储](working-with-srp.md)，UGC将仅在输入它的AEM发布或创作实例上可见。
>

>[!NOTE]
>
>有关AEM平台的更多信息，请参阅 [建议的部署](../../help/sites-deploying/recommended-deploys.md) 和 [AEM平台简介](../../help/sites-deploying/data-store-config.md).

## 用于生产 {#for-production}

为UGC建立一个公共存储区是必不可少的，因此底层部署取决于它是否能够支持一个公共存储区。

两个示例：

1. 如果UGC的预期容量很高，则可以选择使用本地MongoDB实例 [MSRP](msrp.md).

1. 为获得页面内容的最佳性能，请选择 [发布场](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) 和 [ASRP](asrp.md) 将通过相对直接的操作提供最佳的UGC扩展。

对于这两者，部署可能基于任何OAK微内核。

要选择适当的常用存储，请仔细考虑独特的 [特征](working-with-srp.md#characteristics-of-srp-options) 各自的。

有关Oak微内核的更多详细信息，请访问 [建议的部署](../../help/sites-deploying/recommended-deploys.md).

### TarMK发布场 {#tarmk-publish-farm}

当拓扑是发布场时，重要的相关主题包括：

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

### 建议：DSRP、MSRP或ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | 站点内容存储库 | 用户生成的内容存储库 | 存储资源提供程序 | 公用存储 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任何 | JCR | MySQL | DSRP | 是 |
| 任何 | JCR | MongoDB | MSRP | 是 |
| 任何 | JCR | Adobe按需存储 | ASRP | 是 |

### JSRP {#jsrp}


| 部署 | 站点内容存储库 | 用户生成的内容存储库 | 存储资源提供程序 | 公用存储 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK场（默认） | JCR | JCR | JSRP | 否 |
| Oak集群 | JCR | JCR | JSRP | 仅用于发布环境 |

## 用于开发 {#for-development}

对于非生产环境， [JSRP](jsrp.md) 简化了用一个创作实例和一个发布实例设置开发环境的过程。

如果选择 [ASRP](asrp.md)， [DSRP](dsrp.md) 或 [MSRP](msrp.md) 对于生产，还可以使用Adobe按需存储或MongoDB设置类似的开发环境。 有关示例，请参见 [如何设置MongoDB以进行演示](demo-mongo.md).

## 引用 {#references}

* [用户同步](sync.md)

  讨论在发布场实例之间同步用户数据。

* [管理用户和用户组](users.md)

  讨论用户和用户组在创作和发布环境中的角色。

* UGC [公用存储](working-with-srp.md)

  描述社区内容与站点内容分开的存储。

* [节点存储和数据存储](../../help/sites-deploying/data-store-config.md)

  基本上，站点内容存储在节点存储中。 对于Assets，可以将数据存储配置为存储二进制数据。 对于Communities，必须配置公共存储以选择SRP。

* [存储元素](../../help/sites-deploying/storage-elements-in-aem-6.md)

  描述两个节点存储实施：Tar和MongoDB。
