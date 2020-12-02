---
title: 社区的推荐拓扑
seo-title: 社区的推荐拓扑
description: 如何处理用户生成的内容(UGC)
seo-description: 如何处理用户生成的内容(UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---


# 社区{#recommended-topologies-for-communities}的推荐拓扑

自AEM Communities6.1起，已采用一种独特的方法来处理由网站访客（成员）从发布环境提交的用户生成的内容(UGC)。

此方法与AEM平台处理通常由作者环境管理的站点内容的方式有根本不同。

AEM平台使用一个节点存储，将站点内容从作者复制到发布，而AEM Communities则使用一个从未复制的UGC通用存储。

对于通用UGC存储，必须选择[存储资源提供程序(SRP)](working-with-srp.md)。 建议的选项有：

* [DSRP —— 关系存储库资源提供程序](dsrp.md)
* [MSRP - MongoDB存储资源提供程序](msrp.md)
* [ASRP -Adobe存储资源提供程序](asrp.md)

另一个SRP选项[JSRP - JCR存储资源提供程序](jsrp.md)不支持作者的通用UGC存储，并发布环境以同时访问。

需要通用存储将导致以下推荐拓扑。

>[!NOTE]
>
>对于AEM Communities,[UGC从不复制](working-with-srp.md#ugc-never-replicated)。
>
>当部署不包括[公用存储](working-with-srp.md)时，UGC将仅在输入它的AEM publish或作者实例上可见。


>[!NOTE]
>
>有关AEM平台的详细信息，请参见[推荐部署](../../help/sites-deploying/recommended-deploys.md)和[AEM平台简介](../../help/sites-deploying/data-store-config.md)。

## 对于生产{#for-production}

为UGC建立公共存储非常重要，因此基础部署取决于其支持公共存储的能力。

两个示例：

1. 如果UGC的预期卷较高，并且可能有本地MongoDB实例，则选择[MSRP](msrp.md)。

1. 为了获得最佳的页面内容性能，选择[发布场](../../help/sites-deploying/recommended-deploys.md#tarmk-farm)和[ASRP](asrp.md)将提供UGC的最佳缩放，其操作相对简单。

对于这两者，部署可以基于任何OAK微内核。

要选择适当的公用商店，请仔细考虑每个商店的唯一[特性](working-with-srp.md#characteristics-of-srp-options)。

有关Oak微字符的详细信息，请访问[推荐部署](../../help/sites-deploying/recommended-deploys.md)。

### TarMK发布场{#tarmk-publish-farm}

当拓扑为发布场时，相关重要主题为：

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

### 推荐：DSRP、MSRP或ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | 站点内容存储库 | 用户生成的内容存储库 | 存储资源提供程序 | 公用商店 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任何 | JCR | MySQL | DSRP | 是 |
| 任何 | JCR | MongoDB | MSRP | 是 |
| 任何 | JCR | Adobe随需存储 | ASRP | 是 |

### JSRP {#jsrp}


| 部署 | 站点内容存储库 | 用户生成的内容存储库 | 存储资源提供程序 | 公用商店 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK Farm（默认） | JCR | JCR | JSRP | 否 |
| Oak Cluster | JCR | JCR | JSRP | 仅用于发布环境 |

## 对于开发{#for-development}

对于非生产环境,[JSRP](jsrp.md)使用一个作者实例和一个发布实例设置开发环境变得简单。

如果选择[ASRP](asrp.md)、[DSRP](dsrp.md)或[MSRP](msrp.md)进行生产，则还可以使用Adobe点播存储或MongoDB设置类似的开发环境。 有关示例，请参阅[HowTo Setup MongoDB for Demo](demo-mongo.md)。

## 引用 {#references}

* [用户同步](sync.md)

   讨论发布场实例中用户数据的同步。

* [管理用户和用户组](users.md)

   讨论创作和发布环境中用户和用户组的角色。

* UGC [公用存储](working-with-srp.md)

   描述独立于站点内容的社区内容的存储。

* [节点存储和数据存储](../../help/sites-deploying/data-store-config.md)

   基本上，站点内容存储在节点存储中。 对于资产，可以配置数据存储以存储二进制数据。 对于Communities，必须配置公用存储来选择SRP。

* [存储6.3中的元素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   描述两个节点存储实现：Tar和MongoDB。
