---
title: 延迟内容迁移
seo-title: 延迟内容迁移
description: 了解AEM 6.4中的懒惰内容迁移。
seo-description: 了解AEM 6.4中的懒惰内容迁移。
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 6%

---


# 延迟内容迁移{#lazy-content-migration}

为了向后兼容，从AEM 6.3开始的&#x200B;**/etc**&#x200B;和&#x200B;**/content**&#x200B;中的内容和配置不会随升级立即被触碰或转换。 这样做是为了确保客户应用程序对这些结构的依赖性保持不变。 与这些内容结构相关的功能仍然相同，即使开箱即用的AEM 6.5内容将存放在其他位置。

虽然并非所有这些位置都可以自动转换，但有一些延迟的`CodeUpgradeTasks`也称为懒惰内容迁移。 这允许客户通过使用此系统属性重新启动实例来触发这些自动转换：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

这将导致在迁移期间执行`CodeUpgradeTasks`。

虽然目标是高效执行，但此升级过程是同步的，因此会根据需要处理的内容数量导致停机。 建议在生产系统之前评估阶段环境的执行时间，以根据维护窗口进行计划。

由于这通常也需要调整应用程序，因此，应将此活动与相应的应用程序部署一起执行。

以下是6.5中引入的`CodeUpgradeTasks`的完整列表:

| **名称** | **相** **关信息适用于之前的AEM版本** | **迁移** **类型** | **详细信息** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5=&quot;&quot;> | 即时 |  |
| `Cq60MSMContentUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 检测已删除的`VersionStorage`中的所有`LiveRelationShips`，并向父级添加排除属性 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 在默认设置下重新构建云服务以确保安全 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即时 | 删除从&#x200B;**/content**&#x200B;到&#x200B;**/conf**（由OSGi机制替换）的基于属性的链接，生成相应的OSGi配置 |
| `Cq62FormsContentUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 由于merge_preserve在默认情况下处理安全拒绝规则覆盖，因此需要在升级时重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 检测使用Html5SmartFile构件的组件，搜索组件在内容中的使用情况并重新构建持久性，从而有效地将二进制文件向下移动一个级别，而不将其存储在组件级别。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 将旧样式项目从&#x200B;**/etc/projects**&#x200B;移至&#x200B;**/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 将容器层引入层次结构（区域）并调整参照。 |
| `Cq62TargetContentUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 将固定位置名称设置为目标组件。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 对早于6.2结构、实例和通知的工作流模型进行复杂转换，然后从备份位置从&#x200B;**/var/backup**&#x200B;合并回 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即时 | 将资源、自定义元模式和处理用户档案从&#x200B;**/apps**&#x200B;移至&#x200B;**/conf**，并将元数据模式和元数据用户档案表单从coral2转换至coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6=&quot;&quot;> | 即时 | 将资产和自定义搜索彩块化从&#x200B;**/apps**&#x200B;移至&#x200B;**/conf**，并将元数据模式和元数据用户档案表单从coral2转换至coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 更新收件箱用于对收件箱项目排序的项目（调整元数据以有效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6=&quot;&quot;> | 即时 | 通过替换到&#x200B;**/conf**&#x200B;的相对路径代替&#x200B;**/apps**，调整文件夹上的metadataSchema属性 |
| `CQ63MobileAppsNavUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 调整导航结构 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6=&quot;&quot;> | 即时 | 将监视仪表板的自定义配置从&#x200B;**/libs**&#x200B;和&#x200B;**/apps**&#x200B;移动 |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6=&quot;&quot;> | 即时 | 转换资产中的processingProfile属性（在6.1之前使用），以匹配6.3和更高版本的结构。 还调整用户档案到&#x200B;**/conf**&#x200B;的相对路径，而不是&#x200B;**/apps**。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6=&quot;&quot;> | 即时 | 升级任务，在升级时删除过时的CRXDE Lite和Web控制台菜单项。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6=&quot;&quot;> | 延迟 | 移动SRP云配置、社区观察词配置、清理&#x200B;**/etc/social**&#x200B;和&#x200B;**/etc/enablement**（运行延迟迁移时需要调整任何引用和数据 — 不再有任何应用程序部分依赖于此结构）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 延迟 | 清理&#x200B;**/etc/cloudsettings**（包含ContextHub配置）。 配置在首次访问时自动迁移。 如果启动延迟内容迁移并升级&#x200B;**/etc/cloudsettings**&#x200B;中的此内容，则必须在升级前通过包保留并重新安装，以便隐式转换开始，并在完成后卸载包。 |
| `CQ64UsersTitleFixTask` | &lt; 6=&quot;&quot;> | 延迟 | 在用户用户档案节点中将旧版标题结构调整为标题。 |
| `CQ64CommerceMigrationTask` | &lt; 6=&quot;&quot;> | 延迟 | 将商务内容从&#x200B;**/etc/commerce**&#x200B;迁移到&#x200B;**/var/commerce**。 在迁移期间，移动内容并更新对移动内容的引用以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 延迟 | 将旧版目录设置和Dynamic MediaCloud Services设置从&#x200B;**/etc**&#x200B;迁移到&#x200B;**/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6=&quot;&quot;> | 延迟 | 清理&#x200B;**/etc/clientlibs**&#x200B;下现有的旧客户端库 |
