---
title: 从Dynamic Media —— 混合模式迁移到Dynamic Media - S7模式
description: 了解如何将Dynamic Media —— 混合模式实例迁移到Dynamic Media - S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: f466193a259d9e8869d7f79eafda1be20869e4af

---


# 关于从Dynamic Media-Hybrid移动到Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是与Adobe Experience Manager的Dynamic Media集成的一个旧版本。 Hybrid版本是首次在AEM(Adobe Experience Manager)6.1中引入的。虽然Adobe继续支持混合模式，但它不是首选模式（Dynamic Media-Scene7是首选模式）。 它还不支持Smart Crop和全景图像等新增功能。 而Dynamic Media-Scene7则提供。

Dynamic Media-Hybrid和Dynamic Media-Scene7之间的其他主要区别包括：

* URL的结构。
* 摄取视频。
* 创建和存储图像演绎版。
* 云配置和凭据（配置）。

从Dynamic Media-Hybrid移动到Dynamic Media-Scene7时，有两个选项可用。 第一个选项是在AEM上只需提供Dynamic Media-Scene7的新实例。 第二个选项是将Dynamic Media-Hybrid的现有实例迁移到Dynamic Media-Scene7。 此选项概述了移动过程中要执行的步骤和注意事项。

>[!IMPORTANT]
>
>Adobe建议不要在实时制作实例上将Dynamic Media-Hybrid实施迁移到Dynamic Media-Scene7。

## 选项1 —— 在AEM上配置Dynamic Media-Scene7的新实例 {#provision-new-dms7}

只需在Adobe Experience Manager上使用Dynamic Media-Scene7的新配置实例，即可开始新操作。 除了通过Dynamic Media Cloud服务获取和处理资产外，还强烈建议对资产使用情况、工作流和组件进行Adobe审核。 在许多情况下，自定义组件和工作流可以替换为较新的现成功能。

## 选项2 —— 将Dynamic Media-Hybrid的现有实例迁移到Dynamic Media-Scene7 {#process-for-migrating}

| 步骤 | 任务 | 注意事项 |
|---|---|---|
| 1 | 克隆Dynamic Media-Hybrid Author实例。 | 您应当保留Dynamic Media-Hybrid Author的现有实例以用于回退目的，直到成功完成该迁移过程中的其余步骤。 |
| 2 | 开始在Dynamic Media-Scene7模式下克隆的作者实例。 |  |
| 3 | 在Adobe Experience Manager Cloud Services中，使用Dynamic Media-Scene7凭据配置Dynamic Media。 | Adobe需要批准Dynamic Media-Scene7配置。 您将拥有并发的Dynamic MediaM-Hybrid和Dynamic Media-Scene7环境，它们将在有限时间内受支持。 |
| 4 | 创建迁移捆绑包，以根据需要收集资源。<br>删除在初始引入Dynamic Media-Hybrid过程中创建的本地PTIFF。 | 如果您的Dynamic Media-Hybrid实例中当前提供所有资产，则其克隆已包括所有资产。 因此，不需要捆绑。 |
| 5 | 运行资产更新工作流，以将资产同步到Dynamic Media Cloud Service。 | Adobe建议批量完成更新工作流，以便进行压缩。 |
| 6 | 迁移查看器、图像和视频预设。 |  |
| 7 | 浏览每个Web内容管理引用的资产并更新其关联的URL。 |  |
| 8 | 迁移任何自定义工作流以支持新的Dynamic Media-Scene7模式（手动更新）。 |  |
| 9 | 验证Web内容管理上传和配置。 |  |
| 10 | 在验证后，请获得批准以禁用Dynamic Media-Hybrid Author（保持回退）。 |  |
| 11 | 在Dynamic Media-Scene7成功使用约一个月后，删除Dynamic Media-Hybrid作者实例。 |  |
