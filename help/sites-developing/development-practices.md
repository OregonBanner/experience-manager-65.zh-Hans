---
title: 开发实践
seo-title: Development Practices
description: 在AEM上进行开发的最佳实践
seo-description: Best practices for developing on AEM
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---

# 开发实践{#development-practices}

## 根据完成的定义工作 {#work-according-to-a-definition-of-done}

每个团队对“完成”的含义都有不同的定义，但重要的是要有一个定义，并确保故事在被接受之前满足定义的标准。

团队通常指定的某些标准包括：

* 已审查用于格式化的代码
* 已添加Comments/Javadoc
* 满足要求的测试覆盖率级别
* 通过单元测试和集成测试
* 已在QA环境中验证
* 已实施本地化

如果没有一个定义明确的DoD，那么很容易出现这样的情况：许多事情已经完成了一半，而没有任何事情是真正完整的。

### 定义并遵守编码和格式惯例 {#define-and-adhere-to-coding-and-formatting-conventions}

缩进级别和空格可能看起来并不重要，但具有正确格式化的代码对于可读性和可维护性大有帮助。 应将各项公约作为一个小组进行讨论和达成一致意见，然后在守则中加以遵循。

### 旨在实现高测试覆盖率  {#aim-for-high-test-coverage}

随着项目实施规模的增长，测试它所需的时间也会增长。 没有良好的测试覆盖率，测试团队将无法扩展，开发人员最终将被埋没在漏洞之中。

开发人员应该实践TDD，在符合其要求的生产代码之前编写失败的单元测试。 QA应创建一组自动化的验收测试，以确保系统在高级别时按预期工作。

提供了一些自定义框架（如Jackalope和Prosper），可以更轻松地模拟JCR API，以确保开发人员在编写单元测试时的工作效率。

### 保持演示就绪 {#stay-demo-ready}

系统应在每次迭代结束时向企业演示。 通过将系统保持为演示就绪状态，团队将始终处于生产就绪的迭代中，并且可以将技术债务保持在一个可维护的水平。

### 实施持续集成环境并使用它 {#implement-a-continuous-integration-environment-and-use-it}

通过实施持续集成环境，您可以轻松、重复地运行单元测试和集成测试。 它还将使部署与开发团队脱钩，使团队其他部分更高效，并实现更稳定和可预测的部署。

### 通过缩短构建时间来保持快速开发周期 {#keep-the-development-cycle-fast-by-keeping-build-times-low}

如果单元测试需要很长时间才能运行，开发人员将避免运行这些测试，从而失去其价值。 如果构建和部署代码需要很长时间，那么人们会减少此类操作的频率。 将缩短构建时间作为首要任务可以确保我们投入到测试范围和CI基础架构上的时间将继续提高团队的工作效率。

### 微调Sonar和其他静态代码分析工具并对其报告执行操作 {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

代码分析工具可能很有价值，但前提是其报告需要开发团队采取行动。 如果不对这些工具提供的分析进行微调，这些工具生成的建议将变得无关紧要，并将失去其价值。

### 遵守男孩Scout规则 {#follow-the-boy-scout-rule}

“男孩Scout”有条规矩：“不要把它弄得比你发现更好。” 只要开发团队的所有成员都遵守此规则，并在遇到问题时进行清理，代码就会不断改进。

### 避免实施YAGNI功能 {#avoid-implementing-yagni-features}

YAGNI（或您不需要它）功能是我们预计将来会需要某种东西（即使现在不需要它）时所实施的功能。 理想情况下，我们应实施目前最简单的方法，并使用连续重构来确保系统架构随时间推移而不断变化。 这样，我们就可以专注于重要的内容，并防止代码膨胀和特征蠕变。
