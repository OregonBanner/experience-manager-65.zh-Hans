---
title: 延迟内容迁移
seo-title: 延迟内容迁移
description: 了解AEM 6.4中的延迟内容迁移。
seo-description: 了解AEM 6.4中的延迟内容迁移。
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34

---


# 延迟内容迁移 {#lazy-content-migration}

为了向后兼容性，从AEM 6.3开始的 **/etc** 和 **/content** 中的内容和配置不会在升级过程中立即被改动或转换。 这样做是为了确保客户应用程序对这些结构的依赖性保持不变。 与这些内容结构相关的功能仍然相同，即使AEM 6.5现成版本中的内容将托管在其他位置。

虽然并非所有这些位置都可以自动转换，但有一些延迟也 `CodeUpgradeTasks` 称为“延迟内容迁移”。 这允许客户通过使用此系统属性重新启动实例来触发这些自动转换：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

这将导致迁 `CodeUpgradeTasks` 移期间执行该操作。

虽然目标是高效执行，但此升级过程是同步的，因此会根据需要处理的内容数量导致停机。 建议在生产系统之前评估舞台环境上的执行时间以根据维护窗口进行计划。

由于这通常也需要调整应用程序，因此应该与相应的应用程序部署一起执行此活动。

以下是6.5中介 `CodeUpgradeTasks` 绍的完整列表：

| **名称** | **与以****前的AEM版本相关** | **迁移类****型** | **详细信息** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即时 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即时 | 检测所 `LiveRelationShips` 有已删 `VersionStorage` 除的内容，并将排除属性添加到父项 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即时 | 重新构建云服务以在默认设置下实现安全 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即时 | 删除从 **/content到/conf****** （由OSGi机制替换）的基于属性的链接，生成相应的OSGi配置 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即时 | 由于merge_preserve处理安全性（默认情况下），拒绝规则会覆盖给定的权限，因此需要在升级时重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即时 | 检测使用Html5SmartFile构件的组件，在内容中搜索组件的使用情况并重新构建持久性，从而有效地将二进制文件向下移动一个级别，而不将其存储在组件级别。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即时 | 将旧样式项目从 **/etc/projects移至****/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即时 | 将容器层引入层次结构（区域）并调整引用。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即时 | 将固定位置名称设置为目标组件。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即时 | 对早于6.2结构、实例、通知的工作流模型进行复杂转换，然后从备份位置从 **/var/backup合并回来** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即时 | 将资产、自定义元数据架构和处理配置文件从 **/apps** 移到 **/conf** ，并将元数据架构和元数据配置文件表单从coral2转换为coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即时 | 将资产和自定义搜索彩块化从 **/apps移到** /conf **** ，并将元数据架构和元数据配置文件表单从coral2转换到coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即时 | 更新收件箱用于对收件箱项目进行排序的项目（调整元数据以实现有效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即时 | 通过替换到 **/conf的相对路径代替/apps来调整文件夹上的metadataSchema****属性** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即时 | 调整导航结构 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即时 | 从/libs和 ******/apps中移动监控仪表板的自定义配置** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即时 | 转换资产中的processingProfile属性（直至6.1），以匹配6.3和更高版本的结构。 还可调整配置文件到 **/conf的相对路径** ，代替 **/apps**。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即时 | 升级任务，在升级时删除废弃的CRXDE lite和Web控制台菜单项。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 延迟 | 移动SRP云配置、社区观察词配置、清理 **/etc/social和** /etc/enablement **** （在延迟迁移运行时，需要调整任何引用和数据——应用程序部分不再依赖于此结构）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 延迟 | 清除 **/etc/cloudsettings** （包含ContextHub配置）。 配置在首次访问时自动迁移。 如果启动延迟内容迁移并升级，则必须在升级之前通过包保留此内容 **** ，并重新安装该内容以启用隐式转换，完成后将卸载包。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 延迟 | 将旧版标题结构调整为用户配置文件节点中的标题。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 延迟 | 将商务内容从 **/etc/commerce** 迁移 **到/var/commerce**。 在迁移期间，移动内容并更新对移动内容的引用以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 延迟 | 将旧版目录设置和Dynamic Media云服务设置从 **/etc** 迁移到 **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 延迟 | 清理 **/etc/clientlibs下的现有旧版clientlib** |
