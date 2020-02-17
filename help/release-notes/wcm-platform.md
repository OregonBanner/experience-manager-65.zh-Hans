---
title: AEM Foundation 和存储库
description: 以下发行说明特定于 Adobe Experience Manager 6.3 AEM 平台和存储库。
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# AEM Foundation 和存储库{#aem-foundation-repository}

## 更改列表 {#list-of-changes}

### 存储库 {#repository}

* Adobe Experience Manager 6.5 的基础建立在基于 OSGi 的框架（Apache Sling 和 Apache Felix）和 Java 内容存储库 (Apache Jackrabbit Oak 1.10.2) 的更新版本之上。
* Please see [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) and [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) for a full overview of fixed issues.

>[!CAUTION]
>
>* 自 AEM 6.3 以后提供的新版 Oak Segment Tar 需要存储库迁移。如果您是从旧版TarMK升级，或者希望从其他类型的持久性切换新的区段Tar，则此步骤是必需的。 For more information on what the benefits of the new Segment Tar are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).
>



### Java 支持 {#java-support}

* 新增对 Java 11 及已支持的 Java 8 的支持
* 为获取最佳性能，请使用其他值覆盖默认的 GC 值。有关更多信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* Adobe 将分发 Java 11 和 Java 8 维护更新，以便客户在 Oracle 未公开提供时在 AEM 相关项目中使用

### OSGI {#osgi}

* 添加了OSGi Promies和Converter实用程序库

### 项目和工作流 {#projects-and-workflows}

* 改进了 6.4 中引入的新工作流模型编辑器以包含更多操作，如复制和发布、工作流步骤中的变量支持以及增强的 OR 和 AND 拆分。

### 搜索 {#searching}

* 在 Oak 中搜索现在支持动态 Facet。例如，资产搜索中的筛选器边栏会显示估计的结果量。
* 扩展了 QueryBuilder 以提供包含动态 Facet 的结果

### 安全 {#security}

* 为管理员用户添加了密码到期时间。

### 用户界面 {#user-interface}

对 UI 进行了各种增强，使其更高效，更易于使用。

* AEM 6.5 为用户和组引入了新的权限管 UI，使其更易于查看和配置整套权限和限制，而无需转至 CRXDE。
* 列视图现在也只加载屏幕上可见的条目，并且仅在用户开始滚动时加载更多条目。列表视图和卡片视图已在 6.0 之后的版本中实现了此功能（在 6.4 中进行了改进）
* 列视图现在包括页面/资产的工作流状态（如果适用）
* “全选”操作是一种快速方法，可以对同一文件夹中的所有页面/资产执行操作
* “全选”操作尝试对所有页面/资产执行操作，而不仅仅是对已加载的页面/资产。如果尚未升级操作以处理批量操作，将会显示一个警告对话框

>[!CAUTION]
>
>* Adobe 不打算进一步增强经典 UI。AEM 6.5 包含经典 UI，从早期发行版升级的客户可以继续按原样使用它。Note that Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).
>



### 升级 {#upgrade}

* 升级过程在 6.5 中基本保持不变。
* 我们继续支持 6.4 中引入的向后兼容性、升级复杂性评估和可持续升级功能。已针对这些需要的区域进行了特定于版本的更新。
* Pattern Detector 包装已经简化，并且针对可用的源本版本，将有一个到 6.5 的包评估升级。
* Please see the [Upgrade documentation](/help/sites-deploying/upgrade.md) for more details on upgrade procedure.

### Web 服务器 {#web-server}

* 快速启动分发将Eclipse Jetty 9.4.15用作servlet引擎（AEM 6.4随9.3.22一起提供）

