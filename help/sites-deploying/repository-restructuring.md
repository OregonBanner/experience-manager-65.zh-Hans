---
title: AEM 6.5中的存储库重组
seo-title: AEM 6.5中的存储库重组
description: 了解AEM 6.5中存储库重组的基础知识和推理
seo-description: 了解AEM 6.5中存储库重组的基础知识和推理
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
translation-type: tm+mt
source-git-commit: 97b2da315fac6f84fcba6d4464bf8dd1d690cfd1
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# AEM 6.5{#repository-restructuring-in-aem}中的存储库重组

## 简介 {#introduction}

在AEM 6.4之前，客户代码部署在JCR的不可预测区域，这些区域可能会在升级时发生更改。 因此，正式的AEM版本通常会覆盖自定义代码、配置或内容。 此外，客户更改有时会覆盖AEM产品代码或内容，破坏产品功能。

通过清晰地定义AEM产品代码和客户代码的层次结构，可以避免这些冲突。

为此，从AEM 6.4开始，并在将来的版本中继续，内容将从/etc重组到存储库中的其他文件夹，并遵循以下高级规则，指导内容向何处移动：

* AEM产品代码将始终放在/libs中，自定义代码不得覆盖
* 自定义代码应放在/apps、/content和/conf中

## 对6.5升级的影响{#impact-on-upgrades}

升级到AEM 6.5时，/etc下的大部分内容将复制到存储库中的其他文件夹中。 这些新位置是引用内容的首选位置。 但是，每次尝试使AEM 6.5升级都向后兼容/etc文件夹中的先前位置，因此在大多数情况下，旧位置将继续由AEM代码引用，直到在客户的应用程序中主动进行更改（在很多情况下是手动进行的）。 从时间轴的角度来看，有两类别更改：

* 升级——有些/etc重组更改不向后兼容，因此应计划并实施作为AEM 6.5升级的一部分的修改。
* 在将来升级之前——大多数/etc重组更改都可以推迟到将来升级后的某个时间。 如前所述，AEM 6.5代码将继续引用旧位置，直到作为客户版本的一部分实施修改。 虽然没有强制更改的时间线，但建议在将来升级之前进行更改，因为将来的功能可能依赖于引用的新位置。 此外，根据惯例，某个特定功能的文档将引用新位置，因此，如果仍在使用旧位置，可能会令人混淆。

### 重组指南{#restructuring-guidance}

在计划升级到AEM 6.5时，应参考以下各个解决方案页面以评估工作成果：

* [所有AEM解决方案通用的存储库重组](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites库重组](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets库重组](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets动态媒体存储库重组](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms库重组](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities库重组](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM商务存储库重组](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

每个页面都包含与必要更改的紧急程度对应的两个部分。 “升级6.5版”部分下的任何内容都应作为AEM 6.5升级项目的一部分处理。 “将来升级前”下的任何内容都可以选择推迟到升级后。

页面上的每个条目都包含一个“重组指导”字段，该字段详细介绍了与新的6.5存储库模型相协调的推荐技术策略，以便以前位于/etc文件夹下的内容引用新位置。 附加的“备注”字段提供任何其他有用的上下文。
