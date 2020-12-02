---
title: 开发实践
seo-title: 开发实践
description: 在AEM上开发的最佳实践
seo-description: 在AEM上开发的最佳实践
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 开发实践{#development-practices}

## 根据“完成{#work-according-to-a-definition-of-done}”的定义进行工作

每个团队对“完成”的含义有不同的定义，但有一个定义并确保故事在被接受之前符合定义的标准非常重要。

团队通常指定的一些标准包括：

* 已检查格式的代码
* 添加了评论/Javadoc
* 满足所需的测试覆盖级别
* 通过单元和集成测试
* 在QA环境中验证
* 本地化实现

如果没有明确的DoD，很容易最终出现这样一种情况：许多事情都做了一半，而什么事情都没有真正完成。

### 定义并遵守编码和格式约定{#define-and-adhere-to-coding-and-formatting-conventions}

缩进级别和空白等内容似乎并不重要，但格式正确的代码对于可读性和可维护性有很大帮助。 应以小组身份讨论和商定公约，然后在守则中加以遵循。

### 针对高测试覆盖率{#aim-for-high-test-coverage}

随着项目实施规模的增加，测试它所需的时间也随之增加。 如果没有良好的测试覆盖，测试团队将无法进行扩展，开发者最终将陷入缺陷。

开发人员应练习TDD，在生产代码满足其要求之前编写失败的单元测试。 QA应创建一套自动的验收测试，以确保系统从高级别按预期运行。

有Jackalope和Prosper等自定义框架可简化对JCR API的嘲弄，以确保开发人员在编写单元测试时的工作效率。

### 保持演示就绪{#stay-demo-ready}

系统应在每次迭代结束时向企业进行演示。 通过使系统保持演示就绪状态，该团队将始终处于生产就绪状态的迭代范围内，技术负债可保持在可维护的水平。

### 实施连续集成环境并使用它{#implement-a-continuous-integration-environment-and-use-it}

实施连续集成环境将使您能够轻松、重复地运行单元测试和集成测试。 它还将部署与开发团队脱钩，使开发团队的其他部分更高效，并使部署更稳定、更可预测。

### 通过将构建时间保持在{#keep-the-development-cycle-fast-by-keeping-build-times-low}的低位，快速保持开发周期

如果单元测试运行时间过长，开发者将避免运行它们，并会失去价值。 如果构建和部署代码需要很长时间，人们的操作就会减少。 将缩短构建时间作为优先事项，可确保我们投入测试覆盖和CI基础架构的时间继续提高团队的工作效率。

### 微调声纳和其他静态代码分析工具，并对其报告{#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}执行操作

代码分析工具可能很有价值，但前提是其报告导致开发团队采取行动。 如果不对这些工具提供的分析进行微调，它们生成的建议将不相关，并会失去价值。

### 遵循男孩Scout规则{#follow-the-boy-scout-rule}

男孩Scout有一条规则：“留下比你找到的更好。” 只要开发团队的全体成员都遵守这一规则，在遇到麻烦时收拾东西，代码就会不断改进。

### 避免实施YAGNI功能{#avoid-implementing-yagni-features}

YAGNI（或者您不需要它）功能是当我们期望将来需要某些东西时实施的，即使我们现在不需要它。 理想情况下，我们应该实施目前最简单的工作，并使用持续重构来确保系统的架构随着时间的过去而不断变化。 这将允许我们专注于重要的方面，并防止代码膨胀和功能蠕变。
