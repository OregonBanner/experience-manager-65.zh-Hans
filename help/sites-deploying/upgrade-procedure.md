---
title: 升级过程
seo-title: 升级过程
description: 了解升级AEM所需遵循的过程。
seo-description: 了解升级AEM所需遵循的过程。
uuid: 81126a70-c082-4f01-a1ad-7152182da88b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 5c035d4c-6e03-48b6-8404-800b52d659b8
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 升级过程 {#upgrade-procedure}

>[!NOTE]
>
>由于大多数AEM升级都是就地执行的，因此升级过程将需要作者层停机。 通过遵循这些最佳实践，可以将发布层停机时间减至最少或消除。

在升级AEM环境时，您需要考虑升级创作环境或发布环境之间的方法差异，以最大限度地减少作者和最终用户的停机时间。 本页概述了升级AEM 6.x版本上当前运行的AEM拓扑的高级过程。由于创作层和发布层以及基于Mongo和TarMK的部署之间的过程不同，因此每层和微内核都列在单独的部分中。 执行部署时，我们建议先升级您的创作环境，确定成功与否，然后继续到发布环境。

## TarMK作者层 {#tarmk-author-tier}

### 起始拓扑 {#starting-topology}

本节假定的拓扑由在TarMK上运行的具有Cold Standby的作者服务器组成。 从作者服务器复制到TarMK发布群。 虽然此处未说明，但此方法也可用于使用卸载的部署。 请确保在作者实例上禁用复制代理之后并在重新启用它们之前，升级或重新构建新版本上的卸载实例。

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### 升级准备 {#upgrade-preparation}

![升级准备作者](assets/upgrade-preparation-author.png)

1. 停止内容创作

1. 停止备用实例

1. 在作者上禁用复制代理

1. 运行 [升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)。

### 升级执行 {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. 运行 [就地升级](/help/sites-deploying/in-place-upgrade.md)
1. 根据需要更新调 *度程序模块*

1. QA验证升级

1. 关闭作者实例。

### 如果成功 {#if-successful}

![if_successful](assets/if_successful.jpg)

1. 复制升级的实例以创建新的Cold Standby

1. 启动作者实例

1. 启动Standby实例。

### 如果失败（回滚） {#if-unsuccessful-rollback}

![回滚](assets/rollback.jpg)

1. 启动Cold Standby实例作为新的主实例

1. 从Cold Standby重建创作环境。

## MongoMK作者群集 {#mongomk-author-cluster}

### 起始拓扑 {#starting-topology-1}

此部分的假定拓扑由一个MongoMK作者群集组成，该群集至少包含两个AEM作者实例，由至少两个MongoMK数据库支持。 所有作者实例共享一个数据存储。 这些步骤应同时适用于S3和文件数据存储。 从作者服务器复制到TarMK发布群。

![mongo拓扑](assets/mongo-topology.jpg)

### 升级准备 {#upgrade-preparation-1}

![mongo_upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. 停止内容创作
1. 克隆数据存储以进行备份
1. 停止除一个AEM作者实例外的所有实例，即您的主作者
1. 从复制副本集（即主Mongo实例）中删除除一个MongoDB节点外的所有节点
1. 更新主作 `DocumentNodeStoreService.cfg` 者上的文件以反映您的单个成员复制副本集
1. 重新启动主作者，以确保正确重新启动
1. 在主作者上禁用复制代理
1. 在 [主作者实例上运行升级前维护](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) 任务
1. 如有必要，使用WiredTiger将主Mongo实例上的MongoDB升级到版本3.2

### 升级执行 {#Upgrade-execution-1}

![mongo-execution](assets/mongo-execution.jpg)

1. 在主 [作者上运行就地升级](/help/sites-deploying/in-place-upgrade.md) 。
1. 根据需要更新调度程序或Web *模块*
1. QA验证升级

### 如果成功 {#if-successful-1}

![mongo-secondary](assets/mongo-secondaries.jpg)

1. 创建新的6.5作者实例，它连接到升级的Mongo实例

1. 重建从群集中删除的MongoDB节点

1. 更新文 `DocumentNodeStoreService.cfg` 件以反映完整的复制副本集

1. 重新启动作者实例，一次一个

1. 删除克隆的数据存储。

### 如果失败（回滚） {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. 重新配置辅助作者实例以连接到克隆的数据存储

1. 关闭升级的作者主实例

1. 关闭升级的Mongo主实例。

1. 启动次Mongo实例，其中一个实例作为新的主实例

1. 在辅助作 `DocumentNodeStoreService.cfg` 者实例上配置文件，以指向尚未升级的Mongo实例的复制集

1. 启动辅助作者实例

1. 清理升级的作者实例、Mongo节点和数据存储。

## TarMK Publish Farm {#tarmk-publish-farm}

### TarMK Publish Farm {#tarmk-publish-farm-1}

此部分假定的拓扑由两个TarMK发布实例组成，前面是由负载平衡器前面的Dispatchers实例。 从作者服务器复制到TarMK发布农场。

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### 升级执行 {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. 在负载平衡器上停止Publish 2实例的通信
1. 在 [Publish 2上运行预升级维护](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
1. 在Publish [2上运行就地升级](/help/sites-deploying/in-place-upgrade.md) 。
1. 根据需要更新调度程序或Web *模块*
1. 刷新调度程序缓存
1. QA通过防火墙后的调度程序验证Publish 2
1. 关闭发布2
1. 复制Publish 2实例
1. 开始发布2

### 如果成功 {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. 启用流量以发布2
1. 停止发布1的流量
1. 停止Publish 1实例
1. 将Publish 1实例替换为Publish 2的副本
1. 根据需要更新调度程序或Web *模块*
1. 刷新Publish 1的Dispatcher缓存
1. 开始发布1
1. QA通过防火墙后的调度程序验证Publish 1

### 如果失败（回滚） {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. 创建发布1的副本
1. 将Publish 2实例替换为Publish 1的副本
1. 刷新Publish 2的Dispatcher缓存
1. 开始发布2
1. QA通过防火墙后的调度程序验证Publish 2
1. 启用流量以发布2

## 最终升级步骤 {#final-upgrade-steps}

1. 启用流量以发布1
1. QA通过公共URL执行最终验证
1. 从创作环境中启用复制代理
1. 恢复内容创作
1. 执行 [升级后检查](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)。

![final](assets/final.jpg)

