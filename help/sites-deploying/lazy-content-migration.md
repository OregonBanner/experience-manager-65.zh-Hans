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

为了向后兼容，请在 **/etc** 和 **/content** 从AEM 6.3开始，不会随升级而立即处理或转换。 这样做是为了确保客户应用程序对这些结构的依赖性保持不变。 与这些内容结构相关的功能仍然相同，即使开箱即用的AEM 6.5中的内容将托管在其他位置。

虽然并非所有这些位置都可能自动改变，但有些地方有所延迟 `CodeUpgradeTasks` 也称为“延迟内容迁移”。 这允许客户通过使用此系统属性重新启动实例来触发这些自动转换：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

这将导致 `CodeUpgradeTasks` 迁移期间执行。

虽然目标是高效执行，但此升级过程是同步的，因此会因需要处理的内容数量而出现停机。 建议在生产系统之前评估阶段环境中的执行时间以根据维护窗口进行规划。

由于这通常还需要调整应用程序，因此应该与相应的应用程序部署一起执行此活动。

以下是 `CodeUpgradeTasks` 在6.5中引入：

| **名称** | **相关** **对于AEM版本之前的版本** | **迁移** **类型** | **详细信息** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即时 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即时 | 检测所有 `LiveRelationShips` 从 `VersionStorage` 已删除，并将排除属性添加到父项 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即时 | 在默认设置下重新构建云服务以确保安全 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即时 | 从中删除基于属性的链接 **/content** to **/conf** （由OSGi机制替换），生成相应的OSGi配置 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即时 | 由于merge_preserve处理安全（默认情况下）拒绝规则会覆盖给定权限，因此需要在升级时重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即时 | 利用Html5SmartFile小组件检测组件，搜索组件在内容中的使用情况并重新构建持久性，从而有效地将二进制文件向下移动一个级别，而不将其存储在组件级别。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即时 | 将旧样式项目从 **/etc/projects** to **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即时 | 将容器层引入层级（区域）并调整参照。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即时 | 将固定位置名称设置为目标组件。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即时 | 对6.2结构、实例和通知之前的工作流模型进行复杂转换，然后从备份位置合并回来 **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即时 | 将资产、自定义元数据架构和处理配置文件从 **/apps** to **/conf** 并将元数据架构和元数据配置文件表单从coral2转换为coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即时 | 将资产和自定义搜索彩块化从 **/apps** to **/conf** 并将元数据架构和元数据配置文件表单从coral2转换为coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即时 | 更新收件箱项目以对收件箱项目进行排序（调整元数据以高效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即时 | 通过将 **/conf** 代替 **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即时 | 调整导航结构 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即时 | 将监控功能板的自定义配置从 **/libs** 和 **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即时 | 为了匹配6.3及更高版本的结构，将资产中的processingProfile属性（在6.1之前使用）转换为。 还可调整用户档案的相对路径 **/conf** 代替 **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即时 | 升级任务，在升级时删除过时的CRXDE Lite和Web控制台菜单项。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 延迟 | 移动SRP云配置、社区关注词配置、清理 **/etc/social** 和 **/etc/enablement** （运行延迟迁移时，需要调整任何引用和数据 — 应用程序部分不再依赖于此结构）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 延迟 | 清理 **/etc/cloudsettings** （包含ContextHub配置）。 首次访问时会自动迁移配置。 如果启动延迟内容迁移，并在 **/etc/cloudsettings** 必须在升级之前通过包进行保留，并重新安装包以便隐式转换开始，并在完成后继续卸载包。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 延迟 | 将旧版标题结构调整为用户配置文件节点中的标题。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 延迟 | 将商务内容从 **/etc/commerce** to **/var/commerce**. 在迁移内容期间，会移动对已移动内容的引用，以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 延迟 | 将旧目录设置和Dynamic MediaCloud Services设置从 **/etc** to **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 延迟 | 清理在 **/etc/clientlibs** |
