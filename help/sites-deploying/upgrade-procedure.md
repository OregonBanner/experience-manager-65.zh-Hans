---
title: 升级过程
seo-title: Upgrade Procedure
description: 了解升级AEM所需的过程。
seo-description: Learn about the procedure you need to follow in order to upgrade AEM.
uuid: 81126a70-c082-4f01-a1ad-7152182da88b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 5c035d4c-6e03-48b6-8404-800b52d659b8
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 5242600c-2281-46f9-a347-d985b4e319b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# 升级过程 {#upgrade-procedure}

>[!NOTE]
>
>由于大多数AEM升级都是在原地进行执行的，因此升级过程将需要停机Author层。 通过遵循这些最佳实践，可以最大限度地减少或消除发布层停机时间。

在升级AEM环境时，您需要考虑升级创作环境或发布环境之间方法上的差异，以最大程度地减少作者和最终用户的停机时间。 此页概述了升级AEM 6.x版本上当前运行的AEM拓扑的高级过程。由于该过程在创作层和发布层以及基于Mongo和TarMK的部署之间有所不同，因此每个层和微内核都列在单独的部分中。 在执行部署时，我们建议先升级创作环境，确定是否成功，然后继续发布环境。

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## TarMK创作层 {#tarmk-author-tier}

### 起始拓扑 {#starting-topology}

此部分假设的拓扑包含在TarMK上运行的带有冷备用的Author服务器。 从创作服务器复制到TarMK发布场。 虽然这里未说明，但也可以将此方法用于使用卸载的部署。 请确保在作者实例上禁用复制代理之后以及重新启用它们之前，在新版本上升级或重建卸载实例。

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### 升级准备 {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. 停止内容创作

1. 停止备用实例

1. 在作者上禁用复制代理

1. 运行 [升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### 升级执行 {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. 运行 [就地升级](/help/sites-deploying/in-place-upgrade.md)
1. 更新Dispatcher模块 *如果需要*

1. QA验证升级

1. 关闭创作实例。

### 如果成功 {#if-successful}

![if_successful](assets/if_successful.jpg)

1. 复制已升级的实例以创建新的冷备用

1. 启动创作实例

1. 启动备用实例。

### 如果不成功（回滚） {#if-unsuccessful-rollback}

![回滚](assets/rollback.jpg)

1. 启动Cold Standby实例作为新的主实例

1. 从冷备用重新构建创作环境。

## MongoMK创作聚类 {#mongomk-author-cluster}

### 起始拓扑 {#starting-topology-1}

此部分的假定拓扑包含一个MongoMK创作聚类，其中至少具有两个AEM创作实例，并至少由两个MongoMK数据库支持。 所有创作实例都共享数据存储。 这些步骤应同时适用于S3和文件数据存储。 从创作服务器到TarMK发布场的复制操作。

![mongo-topology](assets/mongo-topology.jpg)

### 升级准备 {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. 停止内容创作
1. 克隆数据存储以进行备份
1. 停止所有AEM创作实例，但只停止一个主要作者
1. 从副本集（您的主Mongo实例）中删除除一个MongoDB节点之外的所有节点
1. 更新 `DocumentNodeStoreService.cfg` 文件，以反映单个成员副本集
1. 重新启动主要作者以确保其正确重新启动
1. 在主作者上禁用复制代理
1. 运行 [升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 在主创作实例上
1. 如有必要，请使用WiredTiger将主Mongo实例上的MongoDB升级到3.2版

### 升级执行 {#Upgrade-execution-1}

![mongo-execution](assets/mongo-execution.jpg)

1. 运行 [就地升级](/help/sites-deploying/in-place-upgrade.md) 在主要作者上
1. 更新Dispatcher或Web模块 *如果需要*
1. QA验证升级

### 如果成功 {#if-successful-1}

![mongo-secondaries](assets/mongo-secondaries.jpg)

1. 创建新的6.5创作实例，连接到升级后的Mongo实例

1. 重建从群集中删除的MongoDB节点

1. 更新 `DocumentNodeStoreService.cfg` 用于反映完整复制副本集的文件

1. 每次重新启动一个创作实例

1. 删除克隆的数据存储。

### 如果不成功（回滚）  {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. 重新配置辅助创作实例以连接到克隆的数据存储

1. 关闭已升级的创作主实例

1. 关闭升级后的Mongo主实例。

1. 启动辅助Mongo实例，并将其中一个实例作为新的主实例

1. 配置 `DocumentNodeStoreService.cfg` 辅助创作实例上的文件，指向尚未升级的Mongo实例的副本集

1. 启动辅助创作实例

1. 清理升级的创作实例、Mongo节点和数据存储。

## TarMK发布场 {#tarmk-publish-farm}

### TarMK发布场 {#tarmk-publish-farm-1}

此部分的假设拓扑包含两个TarMK发布实例，由Dispatcher前导，后者又由负载平衡器前导。 从创作服务器到TarMK发布场的复制操作。

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### 升级执行 {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. 在负载平衡器处停止流向Publish 2实例的流量
1. 运行 [升级前维护](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 发布时2
1. 运行 [就地升级](/help/sites-deploying/in-place-upgrade.md) 发布时2
1. 更新Dispatcher或Web模块 *如果需要*
1. 刷新Dispatcher缓存
1. QA通过防火墙后面的Dispatcher验证Publish 2
1. 关闭发布2
1. 复制发布2实例
1. 开始发布2

### 如果成功 {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. 启用流量以发布2
1. 停止流量以发布1
1. 停止发布1实例
1. 将Publish 1实例替换为Publish 2副本
1. 更新Dispatcher或Web模块 *如果需要*
1. 刷新Publish 1的Dispatcher缓存
1. 开始发布1
1. QA通过防火墙后面的Dispatcher验证Publish 1

### 如果不成功（回滚） {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. 创建Publish 1副本
1. 将Publish 2实例替换为发布1的副本
1. 刷新Publish 2的Dispatcher缓存
1. 开始发布2
1. QA通过防火墙后面的Dispatcher验证Publish 2
1. 启用流量以发布2

## 最终升级步骤 {#final-upgrade-steps}

1. 启用流量以发布1
1. QA从公共URL执行最终验证
1. 从创作环境启用复制代理
1. 继续内容创作
1. 执行 [升级后检查](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![final](assets/final.jpg)
