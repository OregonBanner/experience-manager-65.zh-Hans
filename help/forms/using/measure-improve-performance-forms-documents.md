---
title: 衡量和提高表单的有效性和转换率
description: AEM Forms与Adobe Target和Adobe Analytics解决方案集成，可让您测量并提高表单的性能和转化率。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# 衡量和提高表单的有效性和转换率{#measure-and-improve-effectiveness-and-conversion-of-forms}

## 挑战 {#the-challenge-br}

组织日益增强能力，鼓励其客户跨多个渠道使用数字自助服务进行交易。 但是，在缺乏一对一反馈机制的情况下，衡量成功并通过数字表单实验来增强客户体验并提高转化率变得很有挑战性。

为了最大限度地提高ROI，组织必须监控其客户与服务的交互方式，并试验其数字工件（表单）以改进客户体验。 要衡量成功并定义改进策略，组织需要获得以下问题的答案：

* 有多少客户尝试使用我的表单访问或进行交易？
* 其中有多少人成功完成了交易？
* 有多少人放弃了这个形式？
* 客户面临问题的问题领域有哪些？
* 我带来了哪些更改以及如何测试哪些更改可提高转化率？

## 解决方案 {#the-solution}

AEM Forms集成 [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) 解决方案 —  [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) 和 [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html)  — 可以帮助您监控和分析表单的执行情况，并让您试验并确定提高转化率的体验。

## 工作流 {#the-workflow}

下面我们来详细了解如何衡量表单的性能并提高表单的转化率。

### 目标受众 {#target-audience}

* 负责营销策略和成功的业务用户和分析员
* 负责基础架构和解决方案设置和维护的IT人员

### 涉及的AEM Forms组件和功能 {#aem-forms-components-and-features-involved}

* 自适应表单
* 与Adobe Analytics集成，以收集、整理和报告客户与您的自适应表单的交互
* 与Adobe Target集成以运行自适应表单的A/B测试

### 假设 {#assumptions}

* 您已拥有Adobe Marketing Cloud帐户并注册了Analytics和Target解决方案。
* 您有一个已发布的自适应表单，客户可以访问。

### 工作流步骤 {#workflow-steps}

#### 步骤1：在AEM Forms中配置Analytics和Target  {#step-configure-analytics-and-target-in-aem-forms-br}

**配置Analytics**

要深入了解客户与表单的交互，您需要首先在AEM Forms中配置Analytics。 执行以下步骤：

1. 在Adobe Analytics中创建报表包
1. 在AEM中创建云服务配置
1. 在AEM中创建云服务框架
1. 在AEM中配置AEM Forms Analytics配置服务
1. 在AEM中对表单启用分析

有关详细步骤，请参阅 [为自适应表单配置分析和报表](../../forms/using/configure-analytics-forms-documents.md).

**配置Tar**

要为自适应表单创建和运行A/B测试，请在AEM Forms中配置Target，如中所述 [在AEM Forms中设置并集成Target](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### 第2步：查看分析报表 {#step-view-analytics-report-br}

当您的客户访问启用了Analytics的表单并与之交互时，其交互将在高度安全的Analytics数据库中捕获。 数据库由客户端分段，并通过安全连接进行访问。

您可以从启用了Analytics的表单的AEM中查看报表并分析数据。 要查看报表，请执行以下操作：

1. 在AEM服务器上，导航到 **Forms > Forms和文档**.
1. 选择要为其生成分析报表的表单。
1. 单击Analytics报表图标。 此时会显示报表。

让我们看一下Analytics为表单收集和报告的数据点。

**Forms分析报表**

自适应表单分析报表可在表单级别捕获以下关键绩效指标(KPI)：

* **平均填充时间**：填写表单所用的平均时间
* **展示次数**：表单在搜索结果中出现的次数

* **节目**：表单被呈现或打开的次数
* **草稿**：表单另存为草稿的次数

* **提交内容**：提交表单的次数
* **中止**：用户未完成表单而离开的次数
* **访问/提交次数**：每次提交的访问次数比率

此外，您还可以在表单中获取有关每个面板的以下详细信息：

* **时间**：面板及其字段上的平均逗留时间（秒）

* **错误**：每1000个表单呈现的面板及其字段上遇到的错误数

* **帮助**：用户每1000个表单演绎版访问面板及其字段的上下文帮助的次数

![自适应表单的示例Analytics报表](assets/summary-report.png)

有关Forms Analytics报表的更多详细信息，请参阅 [查看和了解AEM Forms Analytics报表](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>您可以在Adobe Marketing Cloud上的Analytics帐户中查看详细报告，并更深入地了解客户及其与您的表单的交互。

#### 步骤3：分析数据点 {#step-analyze-data-points}

在此步骤中，您将分析分析报表中的数据点并推断表单的执行情况。 如果达不到成功KPI，您将根据数据构建假设，并找到可能的解决方案来解决问题。 例如：

* 如果表单的平均填写时间高于您的预期，则您的表单可能让客户难以理解，表单可能未使用标准术语，表单过长等等。 在这种情况下，您可能希望简化表单结构和字段，重新设计表单设计，缩短表单长度，或者为非标准表单字段添加帮助说明和示例。
* 如果数据表明大多数客户都在访问表单面板的帮助，则很明显客户对于要填写什么信息感到困惑。 您可能需要使用替代术语或为该面板添加一些示例输入和帮助描述。
* 如果表单的中止或放弃率高于预期，则可能是由于表单渲染时间过长、客户无意中登陆表单或表单过于复杂所致。 在这种情况下，您可能需要优化搜索结果中显示的表单描述、简化表单、优化表单以加快加载速度等。

一旦您分析完这些数据点并得出一个假设，请在表单中进行所需的更改。

#### 步骤4：验证您的分析和修复 {#step-validate-your-analysis-and-fixes}

在此步骤中，您将验证在表单中所做的更改，并验证它是否影响转化率。

**运行A/B测试**

AEM Forms与Target的集成允许为自适应表单创建A/B测试。 在A/B测试中，您可以实时向客户随机展示表单的不同体验，以了解哪个体验效果更佳或导致转化率更高。 一旦您掌握了重要数据，表明某个体验提供了比另一个体验更好的转化，您就可以将该体验声明为入选者，此后，该体验将成为对所有客户可见的默认体验。

有关为自适应表单创建A/B测试的更多信息，请参阅 [自适应表单的A/B测试](../../forms/using/ab-testing-adaptive-forms.md).

![自适应表单的A/B测试摘要报告示例](assets/ab-test-report-4.png)

## 最佳实践 {#best-practices}

真正的最佳实践是您在执行此工作流时自我标识的最佳实践。 它们特定于您的环境和要求。 通过工作流捕获您的学习内容，并将其作为最佳实践进行记录。

有关设计表单和运行A/B测试的一些建议如下：

**Forms设计**

* 保持表单简单、简短且易于导航。 使用定向提示进行导航。
* 对表单字段使用标准或常用术语。
* 通过示例或帮助解释用户可能感到困惑的字段和所需输入。
* 尽可能在用户输入内容时对其进行验证，以避免在提交表单时出现错误。
* 优化桌面和移动设备的布局。
* 自动填充已知用户的信息。

**A/B测试**

* 在运行A/B测试之前，构建假设并识别成功量度。
* 在替代体验中尽可能减少变化（最好一次变化一个），以了解影响转化率的因素。
* 经常测试以消除低效。
