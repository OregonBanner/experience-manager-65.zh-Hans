---
title: 从Dynamic Media迁移 — 混合模式迁移到Dynamic Media - S7模式
description: 了解如何将您的Dynamic Media实例迁移到Dynamic Media - S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7模式，混合模式
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 2%

---

# 关于从Dynamic Media — 混合到Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是Dynamic Media与Adobe Experience Manager集成的较旧版本。 混合版本最初在Adobe Experience Manager 6.1中引入。虽然Adobe继续支持混合模式，但它不是首选模式；Dynamic Media-Scene7是首选使用模式。 混合模式也不支持智能裁剪和全景图像等新功能，而Dynamic Media-Scene7则支持这些功能。

Dynamic Media-Hybrid和Dynamic Media-Scene7之间的其他主要区别包括：

* URL的结构。
* 摄取视频。
* 创建和存储图像演绎版。
* 云配置和凭据（配置）。

从Dynamic Media-Hybrid迁移到Dynamic Media-Scene7时，有两个选项可用。 第一种选择是，只需在Experience Manager上配置一个新的Dynamic Media-Scene7实例即可。 第二个选项是将现有的Dynamic Media-Hybrid实例迁移到Dynamic Media-Scene7。 此选项在表格中概述了在移动过程中需要注意的步骤和注意事项。

>[!IMPORTANT]
>
>Adobe建议您不要在实时生产实例上将Dynamic Media-Hybrid实施迁移到Dynamic Media-Scene7。

## 选项1 — 在Experience Manager上提供Dynamic Media-Scene7的新实例 {#provision-new-dms7}

您只需在Adobe Experience Manager上使用新的、已配置的Dynamic Media-Scene7实例即可开始使用。 除了通过Dynamic MediaCloud Service获取和处理资产之外，还强烈建议对资产使用情况、工作流和组件进行Adobe审核。 通常，您可以使用较新的现成功能替换自定义组件和工作流。

## 选项2 — 将现有的Dynamic Media-Hybrid实例迁移到Dynamic Media-Scene7 {#process-for-migrating}

| 步骤 | 任务 | 注意事项 |
|---|---|---|
| 1 | 克隆Dynamic Media — 混合创作实例。 | 维护您的现有Dynamic Media-Hybrid Author实例以用于回退，直到成功完成此迁移过程中的其余步骤为止。 |
| 2 | 在Dynamic Media-Scene7模式下启动克隆的创作实例。 |  |
| 3 | 在Adobe Experience ManagerCloud Services中，使用Dynamic Media-Scene7凭据配置Dynamic Media。 | Adobe必须批准Dynamic Media-Scene7配置。 因此，您拥有受Adobe支持的并发Dynamic MediaM-Hybrid和Dynamic Media-Scene7环境，但该环境的时间有限。 |
| 4 | 创建迁移包，以便您可以根据需要摄取资产。<br>删除在初始摄取到Dynamic Media-Hybrid期间创建的本地PTIFF。 | 如果Dynamic Media-Hybrid实例中当前所有资产都可用，则的克隆已包含所有资产。 因此，不需要包。 |
| 5 | 运行资产更新工作流，以便将资产同步到Dynamic MediaCloud Service。 | Adobe建议您分批执行更新工作流，以便进行压缩。 |
| 6 | 迁移查看器预设、图像预设和视频预设。 |  |
| 7 | 浏览每个引用Web内容管理的资产并更新其关联的URL。 |  |
| 8 | 迁移要支持新Dynamic Media-Scene7模式的任何自定义工作流（手动更新）。 |  |
| 9 | 验证Web内容管理的上载和配置。 |  |
| 10 | 验证后，获得批准禁用Dynamic Media-Hybrid Author（作为回退进行维护）。 |  |
| 11 | 在成功使用Dynamic Media-Scene7大约一个月后，删除Dynamic Media-Hybrid创作实例。 |  |
