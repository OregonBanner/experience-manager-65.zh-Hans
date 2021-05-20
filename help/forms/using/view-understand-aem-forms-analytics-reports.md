---
title: 查看和了解AEM Forms分析报表
seo-title: 查看和了解AEM Forms分析报表
description: AEM Forms与Adobe Analytics集成在一起，为您提供有关已发布自适应表单的摘要和详细分析。
seo-description: AEM Forms与Adobe Analytics集成在一起，为您提供有关已发布自适应表单的摘要和详细分析。
uuid: b15ba5f3-aea7-40f5-893e-aaf3834cbc33
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 3690fa80-6332-4df8-afea-77b5490fe0d1
docset: aem65
exl-id: c5a4e6f6-f331-41e9-a0a9-51a30df6e2cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# 查看和了解AEM Forms分析报表{#view-and-understand-aem-forms-analytics-reports}

Adobe Experience Manager Forms与Adobe Analytics集成，允许您捕获和跟踪已发布的表单和文档的性能量度。 分析这些量度的目的是，根据使表单或文档更易用所需更改的数据做出明智决策。

## 设置Analytics {#setting-up-analytics}

AEM Forms中的分析功能作为AEM Forms附加组件包的一部分提供。 有关安装附加组件包的信息，请参阅[安装和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

除了附加组件包之外，您还需要一个Adobe Analytics帐户。 有关解决方案的信息，请参阅[Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)。

拥有AEM Forms附加组件包和Adobe Analytics帐户后，请将Adobe Analytics帐户与AEM Forms集成，并按照[配置Analytics和报表](../../forms/using/configure-analytics-forms-documents.md)中的说明，启用对表单或文档的跟踪。

### 如何记录用户交互信息{#how-user-interaction-information-is-recorded}

当用户与表单交互时，交互将被记录并发送到Analytics服务器。 以下列表指示了各种用户活动的服务器调用：

* 每次访问每个字段2次呼叫
* 1次面板访问
* 保存1
* 提交2
* 保存2
* 帮助1
* 每次验证错误1
* 表单演绎版为1 +默认面板访问为1 +默认第1次现场访问为1
* 2表单放弃

>[!NOTE]
>
>此列表并不详尽。

### 查看分析报表{#summary-report}

执行以下步骤以查看分析报表：

1. 登录到AEM门户，地址为`https://[hostname]:'port'`
1. 单击&#x200B;**Forms > Forms和文档**。
1. 选择要查看其分析报表的表单。
1. 选择&#x200B;**更多> Analytics报表**。

![analytics报告](assets/analyticsreport.png)

**A.Analytics** 报表命令

AEM Forms显示表单和表单中每个面板的analytics报表，如下所示。

![自适应表单的摘要报告](assets/analyticsdashboard_callout.png)

**A.** 转 **化B.** 表单级别摘要 **C.** 面板级别摘要 **D.** 访客的浏览器 — 过滤 **E.** 访客的操作系统 — 过滤 **F.** 访客语言 — 过滤

默认情况下，会显示最近七天的分析报表。 您可以查看最近15天、最近1个月等的报表，或指定日期范围。

>[!NOTE]
>
>“最近7天”和“最近15天”等选项不包含生成分析报表当天的数据。 要包含当天的数据，您需要指定包含当天的日期范围，然后运行报表。

![日期范围](assets/date-range.png)

### 自适应表单和HTML5表单的转化图{#conversions-graph-for-adaptive-and-html-forms}

通过表单级别转化图，您可以深入了解表单在以下关键绩效指标(KPI)上的表现：

* **演绎版**:表单的打开次数
* **访客**:表单的访客数
* **提交**:提交表单的次数

![转化图](assets/conversion-graph.png)

### 自适应表单和HTML5表单的Analytics报表{#analytics-report-for-adaptive-and-html-forms}

通过表单级别摘要部分，您可以深入了解表单在以下关键绩效指标(KPI)上的执行情况：

* **平均填充时间**:填写表单所花费的平均时间。当用户在表单上花费时间但未提交时，该时间不会包含在此计算中。
* **演绎版**:表单已呈现或打开的次数
* **草稿**:表单被保存为草稿的次数
* **提交**:已提交表单的次数
* **中止**:用户开始填写表单后离开而不填写表单的次数
* **独特访客**:表单由独特访客呈现的次数。有关独特访客的更多信息，请参阅[独特访客、访问和客户行为](https://helpx.adobe.com/analytics/kb/unique-visitors-visitor-behavior.html)。

![扩展的表单级别摘要分析报表](assets/analytics-report.png)

### 面板报告{#bottom-summary-report}

面板级别摘要部分提供了有关表单中每个面板的以下信息：

* **平均填充时间**:无论是否提交了表单，面板平均逗留时间
* **遇到错误**:用户在面板中的字段中遇到的平均错误数。“遇到的错误”是通过将字段中的总错误除以表单的呈现次数得出的。
* **访问的帮助**:用户访问面板中字段的上下文内帮助的平均次数。“帮助访问”是通过将字段的“帮助”访问总次数除以表单的呈现次数得到的。

#### 详细的面板报告{#detailed-panel-report}

您还可以通过单击面板报表中某个面板的名称来查看每个面板的详细信息。

![详细的面板报告](assets/panel-report-detailed.png)

详细报表显示面板中所有字段的值。

面板报表包含三个选项卡：

* **时间报表**（默认）：显示在面板中填写每个字段所花费的时间（以秒为单位）
* **错误报表**:显示用户在填写字段时遇到的错误数
* **帮助报表**:访问特定字段的帮助的次数

如果有多个面板可用，则可以在这些面板之间导航。

### 过滤器：浏览器、操作系统和语言{#filters-browser-os-and-language}

“浏览器分发”、“操作系统分发”和“语言分发”表按表单用户的浏览器、操作系统和语言显示呈现版本、访客和提交。 默认情况下，这些表最多显示5个条目。 您可以单击显示更多以显示更多条目，然后单击显示更少返回常规的五个或更少条目。

要进一步过滤分析数据，您可以单击任何表中的条目。 例如，如果在“浏览器分发”表中单击Google Chrome，则报表将再次呈现，并显示与Google Chrome浏览器相关的数据，如下所示：

![应用于Analytics报表的过滤器 — Google Chrome  ](assets/filter-1.png)

如果在应用过滤器后查看面板报表，则面板报表数据也会根据应用的过滤器显示。

应用过滤器后：

* 由于一次只能应用一个过滤器，因此分发表变为只读。
* 应用的过滤器表会消失。
* 您可以单击“关闭”按钮（在下面突出显示）以删除应用的过滤器。

![“关闭”按钮可删除应用的过滤器](assets/close-filter.png)

### A/B测试{#a-b-testing}

如果您为表单启用了A/B测试并设置了，则报表页面中会有一个下拉列表，可用于显示A/B测试报表。 A/B测试报表显示您设置的两个表单版本的比较性能。

有关A/B测试的更多信息，请参阅[创建和管理自适应表单的A/B测试](../../forms/using/ab-testing-adaptive-forms.md)。
