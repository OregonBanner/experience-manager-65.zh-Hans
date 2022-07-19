---
title: 升级到AEM 6.5
seo-title: Upgrading to AEM 6.5
description: 了解将旧版AEM安装升级到AEM 6.5的基础知识。
seo-description: Learn about the basics of upgrading an older AEM installation to AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
source-git-commit: 02fc145d5ec1458d1f71a2f353b56b944a267f3e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 2%

---

# 升级到AEM 6.5 {#upgrading-to-aem}

在本节中，我们将介绍如何将AEM安装升级到AEM 6.5:

* [规划升级](/help/sites-deploying/upgrade-planning.md)
* [利用模式检测器评估升级复杂度](/help/sites-deploying/pattern-detector.md)
* [AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md)

<!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [升级过程](/help/sites-deploying/upgrade-procedure.md)
* [升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md)
* [升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [执行就地升级](/help/sites-deploying/in-place-upgrade.md)
* [升级后检查和疑难解答](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [可持续升级](/help/sites-deploying/sustainable-upgrades.md)
* [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md)
* [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md)

为了更便于引用这些过程中涉及的AEM实例，在这些文章中使用了以下术语：

* 的 *来源* 实例是您从中升级的AEM实例。
* 的 *目标* 实例是您升级到的实例。

>[!NOTE]
>
>作为提高升级可靠性努力的一部分，AEM进行了全面的存储库重组。 有关如何与新结构保持一致的更多信息，请参阅 [AEM中的存储库重组。](/help/sites-deploying/repository-restructuring.md)

## 更改了哪些内容？ {#what-has-changed}

以下是在最近几个版本的AEM中对注释的主要更改：

AEM 6.0引入了新的Jackrabbit Oak存储库。 持久性管理器由 [微核](/help/sites-deploying/platform.md#contentbody_title_4). 从版本6.1开始，不再支持CRX2。 需要运行名为crx2oak的迁移工具，才能从5.6.1实例迁移CRX2存储库。 有关更多信息，请参阅 [使用CRX2OAK迁移工具](/help/sites-deploying/using-crx2oak.md).

如果要使用AEM Insights ，并且您从低于6.2的版本进行升级，则必须迁移资产，并通过JMX Bean生成ID。 在我们的内部测试中，TarMK环境中的12.5万个资产在一小时内迁移，但结果可能有所不同。

6.3为 `SegmentNodeStore`，这是TarMK实施的基础。 如果您从AEM 6.3以前的版本进行升级，则在升级过程中需要进行存储库迁移，这涉及到系统停机。

Adobe工程部估计这大约需要20分钟。 请注意，无需重新编制索引。 此外，还发布了新版crx2oak工具，以使用新的存储库格式。

**从AEM 6.3升级到AEM 6.5时，无需进行此迁移。**

升级前维护任务已进行优化以支持自动化。

crx2oak工具命令行使用选项已更改为对自动化友好，并支持更多升级路径。

升级后检查也使自动化友好。

对修订版本和数据存储垃圾收集的定期垃圾收集现在是需要定期执行的例行维护任务。 随着AEM 6.3的推出，Adobe支持并建议进行在线修订清理。 请参阅 [修订清理](/help/sites-deploying/revision-cleanup.md) 以了解如何配置这些任务的信息。

AEM最近引入 [图案检测器](/help/sites-deploying/pattern-detector.md) 在您开始规划升级时，评估升级的复杂性。 6.5还重点关注 [后向兼容性](/help/sites-deploying/backward-compatibility.md) 功能。 最后， [可持续升级](/help/sites-deploying/sustainable-upgrades.md) 中的“隐藏主体”和“显示主体”。

有关最近AEM版本中更改的其他内容的更多详细信息，请参阅完整的发行说明：

* [Adobe Experience Manager 6.4 的一般发行说明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/release-notes.html?lang=zh-Hans)
* [Adobe Experience Manager 6.5最新Service Pack发行说明](/help/release-notes/release-notes.md)

## 升级概述 {#upgrade-overview}

升级AEM是一个多步骤、有时为多月的过程。 提供了以下概要，概述了升级项目中包含的内容以及本文档中包含的内容：

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 升级流程 {#upgrade-overview-1}

下图显示了总体推荐流程，重点介绍了升级方法。 请注意我们引入的新功能的参考。 升级应从模式检测器开始(请参阅 [利用模式检测器评估升级复杂度](/help/sites-deploying/pattern-detector.md))，您应该根据生成的报表中的模式确定要与AEM 6.4兼容的路径。

6.5中重点介绍了如何使所有新功能向后兼容，但在您仍然看到一些向后兼容性问题时，兼容性模式允许您暂时推迟开发，以使自定义代码与6.5兼容。此方法有助于您在升级后立即避免开发工作(请参阅 [AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md))。

最后，在6.5开发周期中，“可持续升级”下引入的功能(请参阅 [可持续升级](/help/sites-deploying/sustainable-upgrades.md))可帮助您遵循最佳实践，使未来升级更高效、更无缝。

![6_4_upgrade_overviewfrowt-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
