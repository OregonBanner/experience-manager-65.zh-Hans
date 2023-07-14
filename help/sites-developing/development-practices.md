---
title: 开发实践
description: 在Adobe Experience Manager上进行开发的最佳实践。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# 开发实践{#development-practices}

## 根据完成的定义工作(DoD) {#work-according-to-a-definition-of-done}

每个团队对“完成”的含义都有不同的定义，但重要的是要有一个定义，并确保故事在被接受之前满足定义的标准。

团队通常指定的某些标准包括：

* 已审查用于格式化的代码
* 已添加Comments/Javadoc
* 满足要求的测试覆盖率级别
* 通过单元测试和集成测试
* 已在QA环境中验证
* 已实施本地化

如果没有一个定义明确的DoD，那么很容易陷入这样一种局面：许多事情已经完成了一半，而没有任何事情是真正完整的。

### 定义并遵守编码和格式惯例 {#define-and-adhere-to-coding-and-formatting-conventions}

缩进级别和空格可能看起来并不重要，但具有正确格式化的代码对于可读性和可维护性大有帮助。 应将各项公约作为一个小组进行讨论和达成一致意见，然后在守则中加以遵循。

### 旨在实现高测试覆盖率  {#aim-for-high-test-coverage}

随着项目实施规模的增长，测试它所需的时间也会增长。 如果没有良好的测试覆盖率，测试团队就无法扩展，开发人员最终会被埋没在漏洞之中。

开发人员应该实践测试驱动开发(TDD)，在满足其要求的生产代码之前编写失败的单元测试。 QA应创建一组自动化的验收测试，以确保系统在高级别时按预期工作。

提供了一些自定义框架（如Jackalope和Prosper），可以更轻松地模拟JCR API，以确保开发人员在编写单元测试时的工作效率。

### 保持演示就绪 {#stay-demo-ready}

系统应在每次迭代结束时向企业演示。 通过将系统保持为演示就绪状态，团队将始终处于生产就绪的迭代中，并且可以将技术债务保持在一个可维护的水平。

### 实施持续集成环境并使用它 {#implement-a-continuous-integration-environment-and-use-it}

通过实施持续集成环境，您可以轻松而重复地运行单元测试和集成测试。 它还使部署与开发团队脱钩，使团队其他部分更高效，并促成更稳定和可预测的部署。

### 通过缩短构建时间来保持快速开发周期 {#keep-the-development-cycle-fast-by-keeping-build-times-low}

如果单元测试需要很长时间才能运行，开发人员将避免运行这些测试，从而失去其价值。 如果构建和部署代码需要很长时间，那么人们会减少此类操作的频率。 将缩短构建时间作为首要任务可以确保您在测试覆盖率和CI基础架构方面投入的时间能够继续提高团队的工作效率。

### 微调Sonar和其他静态代码分析工具并对其报告执行操作 {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

代码分析工具可能很有价值，但前提是其报告需要开发团队采取行动。 如果不对这些工具提供的分析进行微调，它们生成的建议就会变得无关紧要，从而失去价值。

### 遵守男孩Scout规则 {#follow-the-boy-scout-rule}

“男孩Scout”有条规矩：“不要把它弄得比你发现更好。” 只要开发团队的所有成员都遵守此规则，并在遇到问题时进行清理，代码就会不断改进。

### 避免实施YAGNI功能 {#avoid-implementing-yagni-features}

YAGNI（您不需要它）功能是我们预计将来会需要某种东西（即使现在不需要它）时所实施的功能。 理想情况下，我们应实施目前最简单的方法，并使用连续重构来确保系统架构随时间推移而不断变化。 这使我们专注于重要内容，并防止代码膨胀和特征爬升。
