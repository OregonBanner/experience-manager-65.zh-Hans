---
title: 智能内容服务培训指南
description: 培训Adobe Sensei的AI服务，将智能标签应用于资产
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 11%

---


# 智能内容服务培训指南 {#smart-content-service-training-guidelines}

为了能够有效标记您的品牌图像，智能内容服务要求培训图像符合特定准则。

## 培训指南 {#guidelines-for-training}

为获得最佳效果，培训集中的图像应符合以下准则：

**数量和大小：**&#x200B;每个标记至少 30 张图像。长边至少 500 像素。

**一致性**: 标记的图像应在视觉上相似。

例如，将所有这些图像标记为（用于培训）并不是一个好 `my-party` 主意，因为它们在视觉上并不相似。

![说明性图像为培训准则的例证](/help/assets/assets/do-not-localize/coherence.png)

**覆盖**: 培训中的图像应该有足够的多样性。 其理念是提供几个但相当多样化的示例，以便Experience Manager学会专注于正确的事情。 如果要对视觉上不相似的图像应用同一标签，请至少包含每种类型的五个示例。

例如，对于标签下 *模式姿势*，为服务包括更多与下面突出显示的图像相似的培训图像，以便在标记过程中更准确地识别类似图像。

![说明性图像为培训准则的例证](/help/assets/assets/do-not-localize/coverage_1.png)

**干扰／阻碍**: 该服务更好地训练那些分散注意力的图像（突出的背景、不相关的伴奏，如有主题的物体／人）。

例如，对于标签 *休闲鞋*，第二幅图像不是很好的培训候选者。

![说明性图像为培训准则的例证](/help/assets/assets/do-not-localize/distraction.png)

**完整性：**&#x200B;如果图像符合多个标记的条件，请在包含培训图像之前添加所有适用的标记。例如，对于 `raincoat` 和 `model-side-view` 等标记，在将其加入培训之前，在符合条件的资产上添加这两个标记。

![说明性图像为培训准则的例证](/help/assets/assets/do-not-localize/completeness.png)

## 限制 {#limitations}

增强的智能标签基于图像及其标签的学习模型。 这些模型并不总是能够完美地识别标记。 智能内容服务的当前版本具有以下限制：

* 无法识别图像中的细微差异。 比如，修身与普通衬衫。
* 无法根据图像的微小图案／部分识别标记。 例如，T恤上的徽标。
* 在支持Experience Manager的区域设置中支持标记。 有关列表语言，请参阅智 [能内容服务发行说明](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html)。

要使用智能标记（常规或增强）搜索资产，请使用资产搜索（全文搜索）。 智能标记没有单独的搜索谓词。

>[!NOTE]
>
>智能内容服务能否训练您的标记并将它们应用于其他图像取决于您用于培训的图像质量。 为获得最佳效果，Adobe建议您使用视觉上相似的图像来针对每个标签培训服务。
