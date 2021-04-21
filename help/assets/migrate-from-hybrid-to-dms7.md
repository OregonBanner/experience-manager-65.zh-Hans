---
title: 从Dynamic Media迁移 — 混合模式到Dynamic Media - S7模式
description: 了解如何将您的Dynamic Media实例迁移到Dynamic Media - S7模式
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
feature: Scene7模式，混合模式
translation-type: tm+mt
source-git-commit: ad67634278088f8f953fde61a3543acdd70537dd
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 关于从Dynamic Media-Hybrid移动到Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid是与Adobe Experience Manager的Dynamic Media集成的旧版本。 混合版本最初在AEM(Adobe Experience Manager)6.1中引入。虽然Adobe继续支持混合模式，但它不是首选模式(Dynamic Media-Scene7是首选模式)。 它还不支持Smart Crop和全景图像等新增功能。 而Dynamic Media-Scene7。

Dynamic Media-Hybrid和Dynamic Media-Scene7之间的其他主要区别包括：

* URL的结构。
* 获取视频。
* 创建和存储图像演绎版。
* 云配置和凭据（配置）。

当您从Dynamic Media-Hybrid移动到Dynamic Media-Scene7时，有两个选项可用。 第一种选择是在AEM上直接提供Dynamic Media-Scene7的新实例。 第二种选择是将现有的Dynamic Media-Hybrid实例迁移到Dynamic Media-Scene7。 此选项概述了在移动过程中要执行的步骤和注意事项。

>[!IMPORTANT]
>
>Adobe建议您不要将Dynamic Media-Hybrid实施迁移到实时生产实例上的Dynamic Media-Scene7。

## 选项1 — 在AEM {#provision-new-dms7}上设置Dynamic Media-Scene7的新实例

只需从Adobe Experience Manager上新配置的Dynamic Media-Scene7实例开始。 除了通过Dynamic MediaCloud Service获取和处理资产外，还强烈建议对资产使用情况、工作流和组件进行Adobe审核。 在许多情况下，自定义组件和工作流可以替换为较新的现成功能。

## 选项2 — 将您的现有Dynamic Media-Hybrid实例迁移到Dynamic Media-Scene7 {#process-for-migrating}

| 步骤 | 任务 | 注意事项 |
|---|---|---|
| 1 | 克隆Dynamic Media-Hybrid Author实例。 | 您应保留现有的Dynamic Media-Hybrid Author实例以用于回退目的，直到成功完成此迁移过程中的其余步骤。 |
| 2 | 开始在Dynamic Media-Scene7模式下克隆的作者实例。 |  |
| 3 | 在Adobe Experience ManagerCloud Services中，使用Dynamic Media-Scene7凭据配置Dynamic Media。 | Adobe需要批准Dynamic Media-Scene7设置。 您将拥有并发的Dynamic MediaM-Hybrid和Dynamic Media-Scene7环境，并且受支持的时间有限。 |
| 4 | 创建迁移捆绑包，根据需要收集资源。<br>删除在初始引入Dynamic Media-Hybrid时创建的本地PTIFF。 | 如果您的Dynamic Media-Hybrid实例中当前所有资源都可用，则该实例的克隆已包括所有资源。 因此，不需要捆绑。 |
| 5 | 运行资产更新工作流，以将资产同步到Dynamic MediaCloud Service。 | Adobe建议批量完成更新工作流，以便进行压缩。 |
| 6 | 迁移查看器、图像和视频预设。 |  |
| 7 | 浏览每个Web内容管理引用的资产并更新其关联的URL。 |  |
| 8 | 迁移任何自定义工作流以支持新的Dynamic Media-Scene7模式（手动更新）。 |  |
| 9 | 验证Web内容管理上传和配置。 |  |
| 10 | 验证后，获得批准禁用Dynamic Media-Hybrid Author（保持回退）。 |  |
| 11 | 在成功使用Dynamic Media-Scene7约一个月后，删除Dynamic Media-Hybrid Author实例。 |  |
