---
title: 推荐的社区拓扑
seo-title: 推荐的社区拓扑
description: 如何处理用户生成的内容(UGC)
seo-description: 如何处理用户生成的内容(UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 社区{#recommended-topologies-for-communities}的推荐拓扑

自AEM Communities 6.1起，已采用一种独特的方法来处理网站访客（成员）从发布环境提交的用户生成内容(UGC)。

此方法与AEM平台处理网站内容的方式有根本不同，网站内容通常由创作环境管理。

AEM平台使用一个节点存储，该存储会将站点内容从作者复制到发布，而AEM Communities则会为从未复制的UGC使用一个通用存储。

对于常用的UGC存储，需要选择[存储资源提供程序(SRP)](working-with-srp.md)。 建议的选项包括：

* [DSRP — 关系数据库存储资源提供程序](dsrp.md)
* [MSRP - MongoDB存储资源提供程序](msrp.md)
* [ASRP -Adobe存储资源提供程序](asrp.md)

另一个SRP选项[JSRP - JCR存储资源提供程序](jsrp.md)不支持创作环境和发布环境的通用UGC存储，以便两者都访问。

需要公共存储会导致以下推荐的拓扑结果。

>[!NOTE]
>
>对于AEM Communities，从不复制[UGC](working-with-srp.md#ugc-never-replicated)。
>
>当部署不包含[公共存储](working-with-srp.md)时，UGC将仅在输入UGC的AEM发布或创作实例上可见。


>[!NOTE]
>
>有关AEM平台的更多信息，请参阅[推荐部署](../../help/sites-deploying/recommended-deploys.md)和[AEM平台简介](../../help/sites-deploying/data-store-config.md)。

## 用于生产{#for-production}

为UGC建立公共存储库是必不可少的，因此基础部署取决于其支持公共存储的能力。

两个示例：

1. 如果UGC的预期卷高且可能有本地MongoDB实例，则选择为[MSRP](msrp.md)。

1. 为了优化页面内容的性能，选择[发布场](../../help/sites-deploying/recommended-deploys.md#tarmk-farm)和[ASRP](asrp.md)可通过相对简单的操作来优化UGC的缩放比例。

对于这两种情况，部署可能基于任何OAK微内核。

要选择适当的公用商店，请仔细考虑每个商店的唯一[特性](working-with-srp.md#characteristics-of-srp-options)。

有关Oak微核的更多详细信息，请访问[推荐部署](../../help/sites-deploying/recommended-deploys.md)。

### TarMK发布场{#tarmk-publish-farm}

当拓扑为发布场时，相关重要主题包括：

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

### 建议：DSRP、MSRP或ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | 网站内容存储库 | 用户生成的内容存储库 | 存储资源提供程序 | 公用商店 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任何 | JCR | MySQL | DSRP | 是 |
| 任何 | JCR | MongoDB | MSRP | 是 |
| 任何 | JCR | Adobe按需存储 | ASRP | 是 |

### JSRP {#jsrp}


| 部署 | 网站内容存储库 | 用户生成的内容存储库 | 存储资源提供程序 | 公用商店 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK场（默认） | JCR | JCR | JSRP | 否 |
| Oak群集 | JCR | JCR | JSRP | 仅发布环境选项 |

## 用于开发{#for-development}

对于非生产环境，[JSRP](jsrp.md)可以简化使用一个创作实例和一个发布实例来设置开发环境的过程。

如果为生产选择[ASRP](asrp.md)、[DSRP](dsrp.md)或[MSRP](msrp.md)，则还可以使用Adobe按需存储或MongoDB来设置类似的开发环境。 有关示例，请参阅[HowTo Setup MongoDB for Demo](demo-mongo.md)。

## 引用 {#references}

* [用户同步](sync.md)

   讨论发布场实例之间用户数据的同步。

* [管理用户和用户组](users.md)

   讨论用户和用户组在创作和发布环境中的角色。

* UGC [公用商店](working-with-srp.md)

   描述将社区内容与网站内容分开的存储。

* [节点存储和数据存储](../../help/sites-deploying/data-store-config.md)

   基本上，站点内容存储在节点存储中。 对于资产，可以将数据存储配置为存储二进制数据。 对于Communities，必须配置公共存储以选择SRP。

* [存储元素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   描述两个节点存储实施：Tar和MongoDB。
