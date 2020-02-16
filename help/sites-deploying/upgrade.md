---
title: 升级到AEM 6.5
seo-title: 升级到AEM 6.5
description: 了解将旧版AEM安装升级到AEM 6.5的基础知识。
seo-description: 了解将旧版AEM安装升级到AEM 6.5的基础知识。
uuid: 45368056-273c-4f1a-9da6-e7ba5c2bbc0d
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: ebd99cc4-8762-4c28-a177-d62dac276afe
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Upgrading to AEM 6.5 {#upgrading-to-aem}

在本节中，我们将介绍如何将AEM安装升级到AEM 6.5:

* [计划升级](/help/sites-deploying/upgrade-planning.md)
* [用模式检测器评估升级复杂度](/help/sites-deploying/pattern-detector.md)
* [AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md)
* [升级过程](/help/sites-deploying/upgrade-procedure.md)
* [升级代码和自定义](/help/sites-deploying/upgrading-code-and-customizations.md)
* [升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [执行就地升级](/help/sites-deploying/in-place-upgrade.md)
* [升级后检查和疑难解答](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [可持续升级](/help/sites-deploying/sustainable-upgrades.md)
* [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md)
* [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring-in-aem65.md)

为了更轻松地引用这些过程中涉及的AEM实例，这些文章中使用了以下术语：

* 源 *实例* ，是您要从中升级的AEM实例。
* 目 *标实例* ，即您要升级到的实例。

>[!NOTE]
>
>作为提高升级可靠性的努力的一部分，AEM已进行了全面的存储库重组。 有关如何与新结构对齐的更多信息，请参阅AEM [中的存储库重组。](/help/sites-deploying/repository-restructuring.md)

## 发生了什么变化？ {#what-has-changed}

以下是AEM最后几个发行版中注意事项的主要更改：

AEM 6.0引入了新的Jackrabbit Oak存储库。 持久性管理器由微内核 [代替](/help/sites-deploying/platform.md#contentbody_title_4)。 从6.1版开始，不再支持CRX2。 需要运行名为crx2oak的迁移工具，才能从5.6.1实例迁移CRX2存储库。 有关详细信息，请 [参阅使用CRX2OAK迁移工具](/help/sites-deploying/using-crx2oak.md)。

如果要使用资产分析，并且您要从AEM 6.2以前的版本升级，则必须迁移资产，并通过JMX bean生成ID。 在我们的内部测试中，在一小时内就迁移了125K个TarMK环境中的资源，但结果可能会有所不同。

6.3为TarMK实施引入了 `SegmentNodeStore`一种新的格式，这是TarMK实施的基础。 如果您是从AEM 6.3之前的版本升级，则这将需要在升级过程中进行存储库迁移，这涉及到系统停机时间。

Adobe工程部估计，此时间约为20分钟。 请注意，无需重新构建索引。 此外，还发布了crx2oak工具的新版本，以使用新的存储库格式。

**从AEM 6.3升级到AEM 6.5时，不需要进行此迁移。**

升级前维护任务已经过优化，可支持自动化。

crx2oak工具命令行使用选项已更改为适合自动化并支持更多升级路径。

升级后检查也变得对自动化友好。

修订的定期垃圾收集和数据存储垃圾收集现在是需要定期执行的常规维护任务。 随着AEM 6.3的推出，Adobe支持并建议进行联机修订清理。 有关如 [何配置这些任务的信息](/help/sites-deploying/revision-cleanup.md) ，请参阅修订清除。

在您开始计划升 [级时，AEM最近引入了Pattern Detector](/help/sites-deploying/pattern-detector.md) ，以评估升级的复杂性。 6.5还强调功能的向后 [兼容性](/help/sites-deploying/backward-compatibility.md) 。 最后，还加入了可持 [续升级](/help/sites-deploying/sustainable-upgrades.md) 的最佳实践。

有关最新AEM版本中其他更改的更多详细信息，请参阅完整的发行说明：

* [https://helpx.adobe.com/cn/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/cn/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/cn/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/experience-manager/6-4/release-notes.html)
* [https://helpx.adobe.com/cn/experience-manager/6-5/release-notes.html](https://helpx.adobe.com/experience-manager/6-5/release-notes.html)

## 升级概述 {#upgrade-overview}

升级AEM是一个多步骤、有时是多月的过程。 以下概述概述了升级项目中包含的内容以及本文档中包含的内容：

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 升级流程 {#upgrade-overview-1}

下图显示了总体推荐流程，重点介绍了升级方法。 请注意我们引入的新功能的参考。 升级应从模式检测器开始(请参阅使用模式检测器评估升级复杂性 [](/help/sites-deploying/pattern-detector.md))，它允许您根据生成的报告中的模式确定要采用的路径以与AEM 6.4兼容。

在6.5中，要使所有新功能向后兼容，需要重点考虑，但是，如果您仍然看到一些向后兼容性问题，兼容性模式允许您暂时推迟开发，以使自定义代码符合6.5规范。此方法可帮助您避免在升级后立即进行开发工作(请参阅AEM 6.5 [中的向后兼容性](/help/sites-deploying/backward-compatibility.md))。

最后，在您的6.5开发周期中，“可持续升级”(请参阅“可持续升级” [](/help/sites-deploying/sustainable-upgrades.md))中引入的功能可以帮助您遵循最佳实践，使未来的升级更高效、无缝。

![6_4_upgrade_overviewprowetch-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)

