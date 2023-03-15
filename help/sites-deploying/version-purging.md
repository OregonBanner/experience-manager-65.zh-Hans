---
title: 版本清除
seo-title: Version Purging
description: 本文介绍了用于版本清除的可用选项。
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 1%

---

# 版本清除{#version-purging}

在标准安装中，当您在更新内容后激活页面时，AEM会创建页面或节点的新版本。

>[!NOTE]
>
>如果未对内容进行任何更改，您将看到一则消息，指出页面已激活，但不会创建新版本

您可以使用根据请求创建其他版本 **版本控制** 帮他搭便车。 这些版本存储在存储库中，如果需要，可以恢复。

这些版本永远不会被清除，因此存储库大小会随着时间的推移而增长，因此需要管理。

AEM附带了各种机制来帮助您管理存储库：

* 此 [版本管理器](#version-manager)
可以将其配置为在创建新版本时清除旧版本。

* 此 [清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 工具此工具用作监控和维护存储库的一部分。
它允许您根据以下参数干预以删除旧版本的节点或节点层次结构：

   * 存储库中保留的最大版本数。
如果超过此数量，则会删除最早的版本。

   * 存储库中保留的任何版本的最长保留时间。
当版本的使用期限超过此值时，将从存储库中清除该版本。

* 此 [版本清除维护任务](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). 您可以计划版本清除维护任务以自动删除旧版本。 因此，这可以最大程度地减少手动使用版本清除工具的需要。

>[!CAUTION]
>
>为了优化存储库大小，您应该经常运行版本清除任务。 当流量有限时，任务应安排在工作时间以外。

## 版本管理器 {#version-manager}

除了使用清除工具进行显式清除之外，还可以将版本管理器配置为在创建新版本时清除旧版本。

要配置版本管理器， [创建配置](/help/sites-deploying/configuring-osgi.md) 对于：

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下选项可供选择：

* `versionmanager.createVersionOnActivation` （布尔值，默认值： true）指定在激活页面时是否创建版本。
除非将复制代理配置为禁止创建版本，否则将创建版本，版本管理器将遵循此策略。
仅当激活发生在包含的路径上时，才会创建版本 `versionmanager.ivPaths` （见下文）。

* `versionmanager.ivPaths`(字符串[]，默认： `{"/"}`)指定在激活时隐式创建版本的路径，如果 `versionmanager.createVersionOnActivation` 设置为true。

* `versionmanager.purgingEnabled` （布尔值，默认值： false）定义是否在创建新版本时启用清除。

* `versionmanager.purgePaths` (字符串[]，默认： {&quot;/content&quot;})指定创建新版本时要在哪些路径上清除版本。

* `versionmanager.maxAgeDays` （int，默认值： 30）在版本清除时，将删除任何早于配置值的版本。 如果该值小于1，则不会根据版本的存在时间执行清除。

* `versionmanager.maxNumberVersions` （int，默认值5）在版本清除时，将删除任何早于第n个最新版本的版本。 如果该值小于1，则不会根据版本数执行清除。

* `versionmanager.minNumberVersions` （int，默认为0）将保留的最小版本数，不考虑版本保留时间。 如果将该值设置为小于1的值，则不会保留最小版本数。

>[!NOTE]
>
>建议不要在存储库中保留大量版本。 因此，在配置版本清除操作时，请注意不要从清除中排除太多版本，否则存储库大小将无法正确优化。 如果您因业务需求而保留大量版本，请联系Adobe支持以找到优化存储库大小的替代方法。

### 结合使用保留选项 {#combining-retention-options}

定义应如何保留哪些版本的选项( `maxAgeDays`， `maxNumberVersions`， `minNumberVersions`)，可根据您的要求进行组合。

例如，在定义要保留的最大版本数和要保留的最旧版本数时：

* 设置:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 通过以下方式：

   * 过去60天内推出的10个版本
   * 其中3个版本是在过去30天内创建的

* 将意味着：

   * 将保留最后3个版本

例如，在定义要保留的最大AND最小版本数和要保留的最旧版本时：

* 设置:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 通过以下方式：

   * 60天前制作的5个版本

* 将意味着：

   * 将保留3个版本

## 清除版本工具 {#purge-versions-tool}

此 [清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 工具用于清除存储库中节点或节点层次结构的版本。 它的主要用途是通过删除节点的旧版本来帮助您减小存储库的大小。
