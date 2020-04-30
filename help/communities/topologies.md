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
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# 推荐的社区拓扑 {#recommended-topologies-for-communities}

自AEM Communities 6.1起，已采用一种独特的方法来处理由站点访客（成员）从发布环境提交的用户生成的内容(UGC)。

此方法与AEM平台处理通常从创作环境管理的站点内容的方式有根本区别。

AEM平台使用一个节点存储，它将站点内容从作者复制到发布，而AEM Communities则为从不复制的UGC使用一个通用存储。

对于通用UGC存储，必须选择一个 [存储资源提供者(SRP)](working-with-srp.md)。 建议的选项有：

* [DSRP —— 关系数据库存储资源提供程序](dsrp.md)
* [MSRP - MongoDB存储资源提供商](msrp.md)
* [ASRP - Adobe存储资源提供商](asrp.md)

另一个SRP选项 [JSRP - JCR存储资源提供者](jsrp.md)，不支持作者的公用UGC存储和发布环境访问这两个访问。

需要公共存储将导致出现以下推荐的拓扑。

>[!NOTE]
>
>对于AEM Communities, [UGC从不复制](working-with-srp.md#ugc-never-replicated)。
>
>当部署不包括公用 [商店](working-with-srp.md),UGC将仅在输入AEM发布实例或作者实例上可见。


>[!NOTE]
>
>有关AEM平台的详细信息，请参 [阅建议的部署](../../help/sites-deploying/recommended-deploys.md)[和AEM平台简介](../../help/sites-deploying/data-store-config.md)。


## 针对制作 {#for-production}

为UGC建立公共存储非常重要，因此基础部署取决于其支持公共存储的能力。

两个示例：

1. 如果UGC的预期卷数较高，并且可能有本地MongoDB实例，则选择 [MSRP](msrp.md)。

1. 为获得最佳的页面内容性能，选择发布场和 [ASRP](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) , [](asrp.md) 将提供UGC的最佳缩放，且操作相对简单。

对于这两者，部署可能基于任何OAK微内核。

要选择适当的常用商店，请仔细考虑每个商店 [的独特](working-with-srp.md#characteristics-of-srp-options) 特点。

有关Oak微内核的更多详细信息，请访 [问推荐部署](../../help/sites-deploying/recommended-deploys.md)。

### TarMK Publish Farm {#tarmk-publish-farm}

当拓扑为发布场时，相关重要主题为：

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

### 建议：DSRP、MSRP或ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | 站点内容存储库 | 用户生成的内容存储库 | 存储资源提供者 | 公用商店 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任何 | JCR | MySQL | DSRP | 是 |
| 任何 | JCR | MongoDB | MSRP | 是 |
| 任何 | JCR | Adobe随需应变的存储 | ASRP | 是 |

### JSRP {#jsrp}


| 部署 | 站点内容存储库 | 用户生成的内容存储库 | 存储资源提供者 | 公用商店 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK Farm（默认） | JCR | JCR | JSRP | 否 |
| Oak Cluster | JCR | JCR | JSRP | 仅供发布环境 |

## 面向开发 {#for-development}

对于非生产环境, [JSRP](jsrp.md) 使用一个作者实例和一个发布实例建立开发环境变得简单。

如果为生 [产选择ASRP](asrp.md)、 [DSRP](dsrp.md) 或 [MSRP](msrp.md) ，则还可以使用Adobe点播存储或MongoDB设置类似的开发环境。 有关示例，请参 [阅HowTo Setup MongoDB for Demo](demo-mongo.md)。

## 引用 {#references}

* [用户同步](sync.md)

   讨论发布农场实例中用户数据的同步。

* [管理用户和用户组](users.md)

   讨论创作和发布环境中用户和用户组的角色。

* UGC公 [用商店](working-with-srp.md)

   描述与站点内容分开的社区内容的存储。

* [节点存储和数据存储](../../help/sites-deploying/data-store-config.md)

   基本上，站点内容存储在节点存储中。 对于资产，可以将数据存储配置为存储二进制数据。 对于Communities，必须配置一个公共存储来选择SRP。

* [AEM 6.3中的存储元素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   描述两个节点存储实现：Tar和MongoDB。
