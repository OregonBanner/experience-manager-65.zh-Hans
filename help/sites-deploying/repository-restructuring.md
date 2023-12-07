---
title: AEM 6.5中的存储库重组
description: 了解AEM 6.5中存储库重组的基础知识和推理
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# AEM 6.5中的存储库重组{#repository-restructuring-in-aem}

## 简介 {#introduction}

在AEM 6.4之前，客户代码部署在JCR中不可预测的区域，这些区域在升级时可能会发生更改。 因此，正式AEM版本通常会覆盖自定义代码、配置或内容。 此外，客户更改有时会覆盖AEM产品代码或内容，从而破坏产品功能。

通过清楚地描述AEM产品代码和客户代码的层次结构，可以避免这些冲突。

为此，从AEM 6.4开始，并在未来版本中继续，内容将从/etc重构到存储库中的其他文件夹，同时提供有关内容流向的指南，并遵守以下高级规则：

* AEM产品代码将始终放置在/libs中，这必须使用自定义代码覆盖
* 自定义代码应放在/apps、/content和/conf中

## 对6.5升级的影响 {#impact-on-upgrades}

升级到AEM 6.5时，/etc下的大量内容子集将在存储库的其他文件夹中重复。 这些新位置是引用内容的首选位置。 但是，为使AEM 6.5升级向后兼容/etc文件夹中以前的位置，已进行了每次尝试，因此在大多数情况下，旧位置将继续被AEM代码引用，直到在客户的应用程序中进行主动（在许多情况下是手动）更改为止。 从时间线的角度来看，更改分为两类：

* 对于6.5升级 — 少数/etc重构更改无法向后兼容，因此应该在AEM 6.5升级过程中计划和实施这些修改。
* 在将来升级之前 — 绝大部分/etc重构更改可以推迟到将来升级后的某个时间。 如前所述，AEM 6.5代码将继续引用旧位置，直到修改作为客户版本的一部分进行实施为止。 虽然没有应进行更改的强制时间线，但建议在将来的升级之前进行更改，因为未来的功能可能会依赖引用的新位置。 此外，按照惯例，给定功能的文档将引用新位置，如果仍在使用旧位置，则可能会混淆。

### 重组指南 {#restructuring-guidance}

在计划升级到AEM 6.5时，应参考以下每个解决方案的页面来评估工作量：

* [所有AEM解决方案通用的存储库重组](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites存储库重组](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets存储库重组](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media存储库重组](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms存储库重组](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities存储库重组](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce存储库重组](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

每个页面包含两个部分，对应于必要更改的紧迫性。 “使用6.5升级”部分下的任何问题都应在AEM 6.5升级项目中处理。 您可以选择将“将来升级之前”下的任何内容推迟到升级后。

页面上的每个条目都包含一个“重构指导”字段，该字段详细介绍了推荐的技术策略，以便与新的6.5存储库模型保持一致，从而为先前位于/etc文件夹下的内容引用新位置。 附加“注释”字段可提供任何其他有用的上下文。
