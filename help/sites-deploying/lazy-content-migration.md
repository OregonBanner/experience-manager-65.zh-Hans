---
title: 延迟内容迁移
seo-title: Lazy Content Migration
description: 了解AEM 6.4中的延迟内容迁移。
seo-description: Learn about Lazy Content Migration in AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 6%

---

# 延迟内容迁移 {#lazy-content-migration}

为了向后兼容，中的内容和配置 **/etc** 和 **/content** 从AEM 6.3开始，升级后不会立即进行接触或转换。 这样做是为了确保客户应用程序对这些结构的依赖关系保持不变。 即使开箱即用的AEM 6.5中的内容将托管在另一个位置，与这些内容结构相关的功能仍然相同。

虽然并非所有这些地点都可自动转换，但有一些位置是延迟的 `CodeUpgradeTasks` 也称为延迟内容迁移。 这允许客户通过使用此系统属性重新启动实例来触发这些自动转换：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

这将导致 `CodeUpgradeTasks` 将在迁移期间执行。

虽然目标是高效执行，但此升级过程是同步的，因此会根据需要处理的内容量而产生停机。 建议在生产系统之前评估暂存环境中的执行时间，以计划相应的维护窗口。

由于这通常还需要调整应用程序，此活动应该与相应的应用程序部署一起执行。

以下是以下内容的完整列表 `CodeUpgradeTasks` 在6.5中引入：

| **名称** | **相关** **对于以下版本之前的AEM** | **迁移** **类型** | **详细信息** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即时 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即时 | 全部检测 `LiveRelationShips` 起始日期 `VersionStorage` ，并将排除属性添加到父级 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即时 | 根据默认设置重新构建cloudservices以提供安全 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即时 | 从删除基于属性的链接 **/content** 到 **/conf** （替换为OSGi机制），生成相应的OSGi配置 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即时 | 由于merge_preserve处理默认的安全拒绝规则会覆盖给定的权限，因此需要在升级时重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即时 | 利用Html5SmartFile小组件检测组件，在内容中搜索组件的使用情况并重新构建持久性，有效地将二进制文件下移一层，而不是将其存储在组件级别。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即时 | 移动旧样式项目 **/etc/projects** 到 **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即时 | 将容器图层引入层级（区域）并调整引用。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即时 | 将固定位置名称设置为目标组件。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即时 | 先于6.2结构、实例、通知，然后从备份位置合并回的工作流模型的复杂转换 **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即时 | 从以下位置移动资产、自定义元数据架构和处理配置文件 **/apps** 到 **/conf** 和将元数据架构和元数据配置文件表单从coral2转换为coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即时 | 将资源和自定义搜索Facet从 **/apps** 到 **/conf** 和将元数据架构和元数据配置文件表单从coral2转换为coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即时 | 更新收件箱项目以排序收件箱项目（调整元数据以实现高效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即时 | 通过将相对路径替换为，调整文件夹上的metadataSchema属性 **/conf** 取代 **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即时 | 调整导航结构 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即时 | 将监视仪表板的自定义配置从 **/libs** 和 **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即时 | 翻译Assets中的processingProfile属性（直到6.1使用）以匹配6.3及更高版本结构。 还可以将配置文件的相对路径调整为 **/conf** 取代 **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即时 | 升级任务，用于在升级时删除过时的CRXDE Lite和Web控制台菜单项。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 延迟 | 移动SRP云配置、社区标语配置、清理 **/etc/social** 和 **/etc/enablement** （运行延迟迁移时需要调整任何引用和数据 — 任何应用程序部分都不应再依赖于此结构）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 延迟 | 清理 **/etc/cloudsettings** （包含ContextHub配置） 首次访问时自动迁移配置。 如果开始延迟内容迁移时同时升级此内容，请 **/etc/cloudsettings** 必须在升级之前通过包进行保留并重新安装，以便隐式转换生效，并且在完成后后续卸载包。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 延迟 | 将旧版标题结构调整为用户配置文件节点中的标题。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 延迟 | 从以下位置迁移商务内容 **/etc/commerce** 到 **/var/commerce**. 在迁移期间，将移动内容并更新对已移动内容的引用，以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 延迟 | 从迁移旧版目录设置和Dynamic MediaCloud Services设置 **/etc** 到 **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 延迟 | 清理下存在的旧版clientlibs **/etc/clientlibs** |
