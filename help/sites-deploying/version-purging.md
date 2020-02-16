---
title: 版本清除
seo-title: 版本清除
description: 本文介绍了用于清除版本的可用选项。
seo-description: 本文介绍了用于清除版本的可用选项。
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# 版本清除{#version-purging}

在标准安装中，在更新内容后激活页面时，AEM会创建页面或节点的新版本。

>[!NOTE]
>
>如果未进行任何内容更改，您将看到一条消息，指明页面已激活，但不会创建新版本

您可以使用Sidekick的“版本控制”选项卡 **在请求时** ，创建其他版本。 这些版本存储在存储库中，并可在需要时恢复。

这些版本从不被清除，因此存储库大小会随着时间而增大，因此需要进行管理。

AEM随附各种机制，可帮助您管理存储库：

* 版本 [管理](#version-manager)器可以将其配置为创建新版本时清除旧版本。

* 清除 [版本工具](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 。此工具用于监视和维护存储库。
它允许您根据以下参数干预删除旧版本的节点或节点层次结构：

   * 存储库中要保存的最大版本数。
超出此数量时，将删除最旧版本。

   * 存储库中保存的任何版本的最大年龄。
当版本的年龄超过此值时，将从存储库中清除该版本。

* “版 [本清除”维护任务](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。 您可以计划“版本清除”维护任务，以自动删除旧版本。 因此，这会最大限度地减少手动使用版本清除工具的需求。

>[!CAUTION]
>
>要优化存储库大小，您应经常运行版本清除任务。 当流量有限时，应在工作时间以外安排任务。

## 版本管理器 {#version-manager}

除了使用清除工具进行显式清除外，还可以将版本管理器配置为在创建新版本时清除旧版本。

要配置版本管理器，请 [为以下对象创建配置](/help/sites-deploying/configuring-osgi.md) :

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下选项可供选择：

* `versionmanager.createVersionOnActivation` (Boolean，默认值：true)指定在激活页面时是否创建版本。
创建版本时，除非将复制代理配置为禁止创建版本（由版本管理器承担）。
仅当激活发生在包含于中的路径上时(请参阅下 `versionmanager.ivPaths` 文)，才创建版本。

* `versionmanager.ivPaths`(字符串[]，默认值：)指 `{"/"}`定激活时隐式创建版本的路径(如 `versionmanager.createVersionOnActivation` 果设置为true)。

* `versionmanager.purgingEnabled` (Boolean，默认值：false)定义是否在创建新版本时启用清除。

* `versionmanager.purgePaths` (字符串[]，默认值：{&quot;/content&quot;})指定在创建新版本时要清除版本的路径。

* `versionmanager.maxAgeDays` (int, default:30)在清除版本时，将删除比配置值更早的任何版本。 如果该值小于1，则不会根据版本的年龄执行清除。

* `versionmanager.maxNumberVersions` （int，默认5）在清除版本时，将删除第n个最新版本之前的任何版本。 如果值小于1，则不根据版本数执行清除。

* `versionmanager.minNumberVersions` (int, default 0)将保留的最小版本数（无论使用期限如何）。 如果将该值设置为小于1的值，则不保留最低版本数。

>[!NOTE]
>
>建议不要在存储库中保留大量版本。 因此，在配置版本清除操作时，请注意不要从清除中排除太多版本，否则存储库大小将无法正确优化。 如果您因业务需要而保留大量版本，请联系Adobe支持部门以找到优化存储库大小的其他方法。

### 组合保留选项 {#combining-retention-options}

定义应如何保留的版本( `maxAgeDays`、 `maxNumberVersions`、 `minNumberVersions`)的选项可根据您的要求组合。

例如，在定义要保留的最大版本数时，以及要保留的最旧版本时：

* 设置:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 通过以下方式：

   * 过去60天内制作了10个版本
   * 过去30天内创建的版本中的3个

* 威尔的意思是：

   * 最后3个版本将保留

例如，在定义要保留的最大AND最小版本数和要保留的最旧版本数时：

* 设置:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 通过以下方式：

   * 60天前制作的5个版本

* 威尔的意思是：

   * 将保留3个版本

## 清除版本工具 {#purge-versions-tool}

清 [除版本工具](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) ，用于清除存储库中节点或节点层次结构的版本。 其主要用途是通过删除旧版本的节点来帮助您减小存储库的大小。
