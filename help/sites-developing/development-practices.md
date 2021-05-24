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
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# 开发实践{#development-practices}

## 根据{#work-according-to-a-definition-of-done}的定义工作

每个团队对“已做”的含义有不同的定义，但重要的是要有一个，并确保故事在被接受之前符合定义的标准。

团队通常指定的一些标准包括：

* 已审核格式的代码
* 添加了注释/Javadoc
* 满足所需的测试覆盖级别
* 通过单元和集成测试
* 已在QA环境中验证
* 已实施本地化

如果没有明确定义的DoD，很容易在这样一种情况下结束：许多事情都做到了一半，但什么事都没有真正完成。

### 定义并遵守编码和格式约定{#define-and-adhere-to-coding-and-formatting-conventions}

缩进级别和空格等内容似乎并不重要，但格式正确的代码有助于提高可读性和可维护性。 公约应作为一个团队进行讨论并商定，然后在守则中加以遵守。

### 针对高测试覆盖率{#aim-for-high-test-coverage}

随着项目实施的规模越来越大，测试它所需的时间也会越来越长。 如果没有良好的测试覆盖，测试团队将无法进行扩展，开发人员最终会陷入错误。

开发人员应练习TDD，在生产代码满足其要求之前编写失败的单元测试。 QA应创建一组自动的验收测试，以确保系统能够从高级别按预期工作。

有一些可用的自定义框架（如Jackalope和Prosper），可简化对JCR API的嘲弄，以确保开发人员在编写单元测试时的工作效率。

### 演示就绪{#stay-demo-ready}

系统应在每次迭代结束时向企业演示。 通过将系统保持为演示就绪状态，该团队将始终处于生产就绪状态的迭代过程中，并且技术负债可以保持在可维护的级别。

### 实施连续集成环境并使用{#implement-a-continuous-integration-environment-and-use-it}

通过实施连续的集成环境，您可以轻松、重复地运行单元测试和集成测试。 它还将部署与开发团队脱钩，使团队的其他部分更高效，并使部署更稳定、更可预测。

### 通过将构建时间保持在{#keep-the-development-cycle-fast-by-keeping-build-times-low}的较低水平，可快速保持开发周期

如果单元测试需要较长的时间才能运行，开发人员将避免运行这些测试，并且会失去价值。 如果构建和部署代码需要较长时间，则人们执行此操作的频率会较低。 将短构建时间作为优先事项，可确保我们在测试覆盖和CI基础架构方面投入的时间将继续提高团队的工作效率。

### 微调声纳和其他静态代码分析工具并对其报告执行{#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}操作

代码分析工具可能很有价值，但前提是其报表导致开发团队采取行动。 如果不对这些工具提供的分析进行微调，则这些工具生成的推荐将不相关，并且会失去价值。

### 遵循男孩Scout规则{#follow-the-boy-scout-rule}

男孩Scout有一条规则：“留它比你找到的好。” 只要开发团队的所有成员都遵守这一规则，在遇到麻烦时清理一下，代码就会不断改进。

### 避免实施YAGNI功能{#avoid-implementing-yagni-features}

YAGNI（或You Not Need It）功能是当我们期望未来需要某些东西时实施的，即使我们现在不需要它。 理想情况下，我们应该实施目前最简单的工作方式，并使用连续重构来确保系统的架构随时间的推移而不断发展。 这样，我们就可以专注于重要的方面，并防止代码膨胀和特征蠕变。
