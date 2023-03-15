---
title: 从Dynamic Media — 混合模式迁移到Dynamic Media - S7模式
description: 了解如何将Dynamic Media — 混合模式实例迁移到Dynamic Media - S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---

# 关于从Dynamic Media-Hybrid迁移到Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是Dynamic Media与Adobe Experience Manager集成的旧版本。 混合版本最初是在Adobe Experience Manager 6.1中引入的。虽然Adobe继续支持混合模式，但它不是首选模式；首选使用Dynamic Media-Scene7模式。 混合模式也不支持智能裁切和全景图像等新功能，而Dynamic Media-Scene7则支持这些功能。

Dynamic Media-Hybrid和Dynamic Media-Scene7之间的其他主要区别包括：

* URL的结构。
* 视频摄取。
* 创建和存储图像演绎版。
* 云配置和凭据（配置）。

从Dynamic Media-Hybrid迁移到Dynamic Media-Scene7时，有两个选项可用。 第一个选项是仅在Experience Manager上配置新的Dynamic Media-Scene7实例。 第二个选项是将现有Dynamic Media-Hybrid实例迁移到Dynamic Media-Scene7。 此选项概述了移动过程中需要执行的步骤和注意事项，如下表所示。

>[!IMPORTANT]
>
>Adobe建议您不要在实时生产实例上将Dynamic Media-Hybrid实施迁移到Dynamic Media-Scene7。

## 选项1 — 在Experience Manager上配置新的Dynamic Media-Scene7实例 {#provision-new-dms7}

只需考虑在Adobe Experience Manager上通过新的Dynamic Media-Scene7配置实例从头开始。 除了通过Dynamic MediaCloud Service摄取和处理资源外，还强烈建议对资源使用情况、工作流和组件进行Adobe审核。 通常，您可以使用较新、现成可用的功能替换自定义组件和工作流。

## 选项2 — 将现有Dynamic Media — 混合实例迁移到Dynamic Media-Scene7 {#process-for-migrating}

| 步骤 | 任务 | 注意事项 |
|---|---|---|
| 1 | 克隆Dynamic Media — 混合创作实例。 | 维护现有的Dynamic Media — 混合创作实例以用于回退目的，直到此迁移过程中的其余步骤成功完成。 |
| 2 | 在Dynamic Media-Scene7模式下开始克隆创作实例。 |  |
| 3 | 在Adobe Experience ManagerCloud Services中，使用Dynamic Media-Scene7凭据配置Dynamic Media。 | Adobe必须批准Dynamic Media-Scene7配置。 因此，您拥有受Adobe支持的并发Dynamic MediaM-Hybrid和Dynamic Media-Scene7环境，但仅限于有限的时间内。 |
| 4 | 创建迁移捆绑包，以便您可以根据需要摄取资产。<br>删除初始引入Dynamic Media-Hybrid期间创建的本地PTIFF。 | 如果所有资源当前在Dynamic Media — 混合实例中均可用，则克隆的已包含所有这些资源。 因此，不需要捆绑。 |
| 5 | 运行资源更新工作流，以便您可以将资源同步到Dynamic MediaCloud Service。 | Adobe建议分批执行更新工作流以允许压缩。 |
| 6 | 迁移查看器、图像和视频预设。 |  |
| 7 | 浏览每个引用Web内容管理的资产并更新其关联的URL。 |  |
| 8 | 迁移您要支持新Dynamic Media-Scene7模式的任何自定义工作流（手动更新）。 |  |
| 9 | 验证Web内容管理上传和配置。 |  |
| 10 | 验证后，获得禁用混合创作Dynamic Media的批准（作为回退进行维护）。 |  |
| 11 | 成功使用Dynamic Media-Scene7大约一个月后，删除Dynamic Media-Hybrid Author实例。 |  |
