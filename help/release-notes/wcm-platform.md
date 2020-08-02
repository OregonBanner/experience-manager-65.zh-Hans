---
title: AEM基础和存储库
description: Adobe Experience Manager平台和存储库的发行说明。
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 56%

---


# AEM基础和存储库 {#aem-foundation-repository}

## 更改列表 {#list-of-changes}

### 存储库 {#repository}

* Adobe Experience Manager 6.5 的基础建立在基于 OSGi 的框架（Apache Sling 和 Apache Felix）和 Java 内容存储库 (Apache Jackrabbit Oak 1.10.2) 的更新版本之上。
* 有关已修复问题的概 [述，请参阅Apache Jackrabbit Oak Jira v. 1.10](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt). [0、Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 和 [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)。

>[!CAUTION]
>
>自 AEM 6.3 以后提供的新版 Oak Segment Tar 需要存储库迁移。如果要从旧版TarMK升级，或希望从其他类型的持久性切换新的段Tar，则此步骤是必需的。 For more information on what the benefits of the new Segment Tar are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

### Java 支持 {#java-support}

* 新增对 Java 11 及已支持的 Java 8 的支持.
* 为获取最佳性能，请使用其他值覆盖默认的 GC 值。有关更多信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* Java 11和Java 8维护更新是通过Adobe在AEM相关项目中分发的，如果不能从Oracle公开获得，则通过客户使用进行分发。

### OSGI {#osgi}

* 添加了OSGi Promies和Converter实用程序库。

### 项目和工作流 {#projects-and-workflows}

* New Workflow Model editor introduced in 6.4 has been improved to include more operations like Copy and Publish, Variable support in Workflow steps and enhanced `OR` and `AND` splits.

### 搜索 {#searching}

* 在 Oak 中搜索现在支持动态 Facet。例如，资产搜索中的筛选器边栏会显示估计的结果量。
* 扩展了 QueryBuilder 以提供包含动态 Facet 的结果.

### 安全 {#security}

* 为管理员用户添加了密码到期时间。

### 用户界面 {#user-interface}

对 UI 进行了各种增强，使其更高效，更易于使用。

* AEM 6.5 为用户和组引入了新的权限管 UI，使其更易于查看和配置整套权限和限制，而无需转至 CRXDE。
* 列视图现在也只加载屏幕上可见的条目，并且仅在用户开始滚动时加载更多条目。列表视图和卡片视图已在 6.0 之后的版本中实现了此功能（在 6.4 中进行了改进）。
* 列视图现在包括页面/资产的工作流状态（如果适用）.
* 全选操作是一种快速方法，可以对同一文件夹中的所有页面/资产执行操作.
* 全选操作会尝试对所有页面/资源执行操作，而不仅仅是加载的页面/资源。如果操作未升级以处理批量操作，则会显示警告。

>[!CAUTION]
>
>Adobe不会进一步增强经典UI。 Experience Manager6.5包含经典UI，可实现向后兼容性。 Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).

### 升级 {#upgrade}

* 升级过程在 6.5 中基本保持不变。
* 我们继续支持 6.4 中引入的向后兼容性、升级复杂性评估和可持续升级功能。已针对这些需要的区域进行了特定于版本的更新。
* Pattern Detector 包装已经简化，并且针对可用的源本版本，将有一个到 6.5 的包评估升级。
* 有关升级过程的详细信息，请参阅 [升级文档](/help/sites-deploying/upgrade.md)。

### Web 服务器 {#web-server}

* 快速启动分发将Eclipse Jetty 9.4.15用作servlet引擎(AEM 6.4随9.3.22一起提供)。
